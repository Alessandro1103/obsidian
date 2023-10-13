Modifico tutte le variabili di camilla dipendenti dalla turbina per distinguerle da quelle del fotovoltaico:
- $w^{res}(t) -> w^{res}_{wt}(t)$ 
- $u^{res} -> u^{res}_{wt}$ (e così anche i min e max)
e aggiungiamo le seguenti:
- $w^{res}_{pv}(t)$

Devo anche ricordarmi di modificare il sistema visto che la mia turbina non è collegata alla batteria
Sul programma di camilla ho una funzione obiettivo nel seguente modo:
$$
\begin{split}
	\min_{u}\bigg\{s(x(t_i+N)-x^{ref})^2+\sum_{t=t_i}^{t_i+N-1} 
	\bigg[q(x(t)-x^{ref})^2+rp(t)^2+c\big(u^{ev}(t)-\hat u^{ev}(t)\big)^2\bigg]
	\bigg\}
\end{split}
$$
che nel codice è:
```julia
if(t==1)
	@objective(mdl, Min, s1*(x1[t+N]-x1_ref)^2+s2*(x2[t+N]-x2_ref)^2+sum((q1*(x1[i]-x1_ref)^2+q2*(x2[i]-x2_ref)^2+r*(p_grid[i])^2+c*(u_ev[i]-u_hat_ev[i])^2) for i=t:t+N-1))
else
	@objective(mdl, Min, s1*(x1[t+N]-x1_ref)^2+s2*(x2[t+N]-x2_ref)^2+sum((q1*(x1[i]-x1_ref)^2+q2*(x2[i]-x2_ref)^2+r*(p_grid[i])^2+r1*(p_grid[i]-p_grid[i-1])^2+c*(u_ev[i]-u_hat_ev[i])^2) for i=t:t+N-1))
end
```

Le variabili da specificare sono:
`t, N, T, q, r, s, c, x, x_ref, p_grid, u_ev, u_hat_ev`
dove si dividono:
- q = q1, q2
- r = r, r1
- s = s1, s2
- x = x1, x2
che abbiamo specificato in [[Legenda]]

Se vogliamo aggiungere delle stazioni collegate ad un fotovoltaico prendiamo le variabili del fotovoltaico: [[Prima riunione#Formalizzazione con PV|Formalizzazione PV]]
La variabile "nuova" é $w^{res}$, che dovremo aggiungere alla chiamata a funzione, e che per semplicità verificheremo opposta a quella della turbina. Questa contribuisce alla potenza all'allaccio ovvero la variabile `p_grid` diversa nella [[Prima riunione|Formalizzazione WT]] 

$p(t)=u^{ess}(t)+u^{ev}(t)-u^{res}_{wt}(t)-w^{res}_{pv}(t)$
**Errore**

Se io facessi così mischierei la produzione di fotovoltaico e turbina, invece essendo due aree di ricarica ho bisogno di due richieste. Dividiamo quindi $u^{ev}$ in due sotto aree:
- $u^{ev}(t) -> u^{ev}_{wt}(t)$
e aggiungiamo $u^{ev}_{pv}(t)$

e di conseguenza dobbiamo dividere p(t) in due equazioni differenti
- $p(t) -> p(t)_{wt}$
e aggiungiamo $p(t)_{pv}$

$p(t)$ sarà la somma delle due $p_{grid}$, che potrò semplicemente verificare tra i constraint
Devo invece modificare la funzione obiettivo, per quanto riguarda le richieste di potenza dai veicoli:
- $c(u^{ev}(t)-\hat u^{ev}(t))^2$ $->$ $c(u^{ev}_{pv}(t)-\hat u^{ev}_{pv}(t))^2 + c(u^{ev}_{wt}(t)-\hat u^{ev}_{wt}(t))^2$

_Non so ancora se posso usare due c diverse, devo capire cosa è c_

così dobbiamo anche modificare la funzione obiettivo, da così:
```julia
if(t==1)
	@objective(mdl, Min, s1*(x1[t+N]-x1_ref)^2+s2*(x2[t+N]-x2_ref)^2+sum((q1*(x1[i]-x1_ref)^2+q2*(x2[i]-x2_ref)^2+r*(p_grid[i])^2+c*(u_ev[i]-u_hat_ev[i])^2) for i=t:t+N-1))
else
	@objective(mdl, Min, s1*(x1[t+N]-x1_ref)^2+s2*(x2[t+N]-x2_ref)^2+sum((q1*(x1[i]-x1_ref)^2+q2*(x2[i]-x2_ref)^2+r*(p_grid[i])^2+r1*(p_grid[i]-p_grid[i-1])^2+c*(u_ev[i]-u_hat_ev[i])^2) for i=t:t+N-1))
end
```
a:
``` julia
if t == 1
  @objective(mdl, Min, s1*(x1[t+N] - x1_ref)^2 + s2*(x2[t+N] - x2_ref)^2 + sum((q1*(x1[i] - x1_ref)^2 + q2*(x2[i] - x2_ref)^2 + r*(p_grid[i])^2 + c*(u_ev_wt[i]-u_hat_ev_wt[i])^2 + c*(u_ev_pv[i]-u_hat_ev_pv[i])^2) for i=t:t+N-1))
else
  @objective(mdl, Min, s1*(x1[t+N] - x1_ref)^2 + s2*(x2[t+N] - x2_ref)^2 + sum((q1*(x1[i] - x1_ref)^2 + q2*(x2[i] - x2_ref)^2 + r*(p_grid[i])^2 + r1*(p_grid[i]-p_grid[i-1])^2 + c*(u_ev_wt[i]-u_hat_ev_wt[i])^2 + c*(u_ev_pv[i]-u_hat_ev_pv[i])^2) for i=t:t+N-1))
end
```

in [[mpc_thesis]] "mia", non ho usato il @variable su w_res_pv, perche @variable si usa unicamente su variabili di ottimizzazione. Quella è fissa invece

# Prima simulazione

Ho considerato una temperatura semplice:
- vento costante: 11 m/s 
- sole costante: 40 kW

richiesta totale uguale a quella di camilla, dimezzata su due stazioni. Quindi quando camilla aveva $\hat u^{ev}=500$ adesso $\hat u^{ev}_{pv} + \hat u^{ev}_{wt} = 500$  

# Situazioni di interesse

[Pala eolica | Enel Green Power | Enel Green Power](https://www.enelgreenpower.com/it/learning-hub/energie-rinnovabili/energia-eolica/pala-eolica)

Vedendo la cartina italiana, sul carico del vento:
![[Pasted image 20230824160210.png]]
![[Pasted image 20230824160717.png]]
oltre a simulare delle situazioni potrei fare delle considerazioni su dove è meglio posizionare determinate fonti. E prendere dati più attendibili

In generale potrei considerare dei valori di vento come:
- 27.00 m/s (fonte: [Zone di vento dell'Italia secondo l'Eurocodice (dlubal.com)](https://www.dlubal.com/it/zone-di-carico-neve-vento-e-sismiche/vento-uni-en-1991-1-4.html#&center=41.55130251974308,12.575786829000004&zoom=5&marker=41.904505,12.494169))
- 11.00 m/s (fonte: Camilla, [Conoscere la velocità media del vento (consulente-energia.com)](http://www.consulente-energia.com/eolico-velocita-media-vento-italia-mappe-ventosita-italiana-metri-montagna-collina-pianura-mare-quali-sono-zone-piu-ventose-eolica.html))

E quindi creare situazioni come:
## Meteo
1. **Giornata soleggiata**:
    - Energia Solare (w_res_pv): 100 kW
    - Velocità del Vento (v_wind): 5 m/s
2. **Nuvoloso con vento moderato**:
    - Energia Solare (w_res_pv): 40 kW
    - Velocità del Vento (v_wind): 10 m/s
3. **Pioggia e vento**:
    - Energia Solare (w_res_pv): 20 kW
    - Velocità del Vento (v_wind): 15 m/s
4. **Torna il sole**:
    - Energia Solare (w_res_pv): 60 kW
    - Velocità del Vento (v_wind): 7 m/s
5. **Giornata calma senza vento**:
    - Energia Solare (w_res_pv): 80 kW
    - Velocità del Vento (v_wind): 2 m/s
## Domanda

**Stazione di Ricarica Solare:**

1. **Momento di alta richiesta solare:** Durante le ore di punta diurne, quando il sole splende intensamente, la domanda aumenta. Supponiamo che per 4 ore durante il giorno, la domanda aumenti del 50% rispetto alla media.
2. **Momento di bassa richiesta solare:** Durante le ore serali e notturne, la domanda si riduce. Supponiamo che per 6 ore durante la notte, la domanda scenda al 70% della media.
3. **Momento di alta richiesta con entrambe le fonti stressate:** In alcune giornate nuvolose e ventose, entrambe le fonti energetiche sono stressate. Supponiamo che per 2 ore, la domanda aumenti del 70% rispetto alla media.
4. **Momento di bassa richiesta solare ed eolica:** Durante le ore diurne poco ventose e nuvolose, entrambe le fonti producono meno energia e la domanda si mantiene normale.

**Stazione di Ricarica Eolica:**

1. **Momento di alta richiesta eolica:** Durante le ore ventose del giorno, la domanda aumenta. Supponiamo che per 5 ore durante il giorno, la domanda aumenti del 40% rispetto alla media.
2. **Momento di bassa richiesta eolica:** Durante le ore poco ventose, la domanda scende. Supponiamo che per 4 ore durante il giorno, la domanda scenda al 80% della media.
3. **Momento di alta richiesta con entrambe le fonti stressate:** Quando ci sono giornate poco ventose e nuvolose, entrambe le fonti sono sotto stress. Supponiamo che per 3 ore, la domanda aumenti del 60% rispetto alla media.
4. **Momento di bassa richiesta solare ed eolica:** Durante le ore notturne poco ventose e nuvolose, la domanda si mantiene normale.

## Validazione codice

Supponiamo di avere una giornata solare tipica con condizioni solari favorevoli e vento moderato. Vogliamo verificare se il codice riesce a gestire correttamente la variazione di domanda durante diverse fasi della giornata.

Profilo di Domanda (per entrambe le stazioni):

1. Dalle 8:00 alle 10:00: La domanda aumenta del 30% rispetto alla media a causa dell'uso intensivo di veicoli durante l'orario di lavoro.
    
2. Dalle 12:00 alle 14:00: La domanda raggiunge il picco, aumentando del 50% rispetto alla media, poiché molti veicoli vengono collegati durante la pausa pranzo.
    
3. Dalle 18:00 alle 20:00: La domanda aumenta nuovamente del 40% rispetto alla media poiché molte persone tornano a casa dal lavoro e collegano i loro veicoli.
    
4. Dalle 22:00 alle 24:00: La domanda si riduce al 70% della media poiché molte persone hanno già completato la ricarica dei veicoli e l'attività complessiva è diminuita.

## Situazione estrema (quasi irrealizzabile)

Immagina una giornata eccezionalmente nuvolosa e senza vento. Durante questa giornata, si verifica un picco di domanda eccezionale dovuto a un evento speciale che coinvolge l'uso intensivo di veicoli elettrici.

Profilo di Domanda (per entrambe le stazioni):

1. Dalle 12:00 alle 16:00: La domanda aumenta costantemente e raggiunge un picco di 3 volte la media a causa di un evento pubblico che richiede la partecipazione di un gran numero di veicoli elettrici.
2. Dalle 16:00 alle 20:00: La domanda rimane costantemente elevata, mantenendosi a 2,5 volte la media, poiché l'evento si protrae.
3. Dalle 20:00 alle 24:00: La domanda diminuisce leggermente ma rimane ancora al doppio della media poiché molte persone continuano a utilizzare i loro veicoli.

In questa situazione estrema, non c'è energia solare ed eolica disponibile a causa delle condizioni meteorologiche sfavorevoli. Il tuo codice deve affrontare la sfida di soddisfare una domanda eccezionalmente elevata senza l'apporto delle fonti rinnovabili.

# MPC

# Seconda parte

Vogliamo ottimizzare il sistema di domanda, $\hat u^{ev}$ dividendola in: 
$$
\hat u^{ev} = \hat u_{pv}^{ev} + \hat u_{wt}^{ev} = \alpha \cdot \hat u^{ev} + (1-\alpha) \cdot \hat u^{ev}
$$
- $\hat u^{ev}$ = domanda di potenza totale (deciso da me), espressa in kW
- $\hat u^{ev}_{pv}$ = domanda di potenza per fotovoltaico
- $\hat u^{ev}_{wt}$ = domanda di potenza per turbina
- $\alpha$ = variabile di ottimizzazione per distribuire la domanda

Noi vogliamo distribuire la domanda di energia in base a tutte considerazioni come: quale stazione ha più energia disponibile, quale è meno piena etc.

probabilmente questa non è la risposta giusta
$$
\begin{aligned}
	& x_{pv}(t+1) = x_{pv}(t) + T \cdot \hat u^{ev}_{pv}\\
	& x_{wt}(t+1) = x_{wt}(t) + T \cdot \hat u^{ev}_{wt}\\
\end{aligned}	
$$

Per ora sostituisco nel codice:
- $\hat u^{ev}_{pv} -> \hat u^{ev} \cdot \alpha$
- $\hat u^{ev}_{wt} -> \hat u^{ev} \cdot (1-\alpha)$
