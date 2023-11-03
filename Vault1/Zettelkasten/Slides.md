Date: 2023-11-03
Time: 23:02
Tags:
Up: 

---
# Analisi e Controllo di un Sistema di Generazione Energetica Sostenibile con Aree di Ricarica

---

# Introduzione al Progetto

Questo progetto si focalizza sull'analisi e il controllo di un sistema di generazione energetica sostenibile, integrato con aree di ricarica per veicoli elettrici. Prima di parlare della struttura, è importante analizzare lo scopo che questo progetto si pone. Avendo una domanda x di energia, nel nostro caso da autoveicoli elettrici, vogliamo soddisfare tale richiesta al limite delle possibilità che le fonti rinnovabili ci permettono, riducendo al minimo l'uso della "rete". La rete per noi rappresenta una produzione esterna che sarebbe meglio non utilizzare per motivi legabili alla sostenibilità o al risparmio.

---

# Struttura 1

Le fonti rinnovabili prima citate sono quella eolica e solare. Diverse possono essere le configurazioni accettabili per gestire l'interazione fra 2 stazioni di ricarica. Quella scelta in questo progetto è la seguente:

![[Progetto senza titolo.png]]


Quella da noi utilizzata comprende, 2 aree di ricarica:
1. abbiamo collegate stazioni di ricarica, pannello fotovoltaico, e una batteria, un collegamento alla "rete", tutto quanto tramite BUS
2. abbiamo collegate stazioni di ricarica, turbina eolica, un collegamento alla "rete", tutto quanto tramite BUS
Tutte queste sono collegate poi alla "rete", ovvero una fonte esterna, il cui uso vorremmo ridurre a zero.
In questa arrangiamento, le due stazioni di ricarica sono in grado di interagire tra di loro; ciò avviene al fine di ottimizzare l'utilizzo delle rispettive fonti energetiche. È altamente plausibile che le loro prestazioni si alternino, massimizzando l'efficienza di ciascuna stazione a turno. 

---

# Componenti

- **Turbine Eoliche**: Convertiamo l'energia cinetica del vento in energia elettrica mediante turbine
- **Pannelli Solari Fotovoltaici**: Catturiamo la luce solare e la convertiamo direttamente in energia elettrica
- **Sistemi di Accumulo**: Utilizziamo batterie per immagazzinare l'energia prodotta e renderla disponibile quando richiesta
- **Aree di Ricarica**: Punti di ricarica per veicoli elettrici

---

# Turbine Eoliche

Il principio chiave di funzionamento della turbina eolica è quello del DFIG.
Per comprenderlo meglio partiamo da una semplice analisi di un motore SCIM (squirrel cage):
Abbiamo 2 corpi:
- Rotore, dove sono presenti 3 avvolgimenti, distanziati di 120° che non sono collegati ad alcun generatore di corrente.
- Statore, dove anche qui sono presenti 3 avvolgimenti, collegati alla rete in corrente alternata trifase. 
$$ 
\begin{aligned}
	& I_a=I_0 \cdot cos(\omega_s t) \\
	& I_b=I_0 \cdot cos(\omega_s t + \frac{2}{3}\pi) \\
	& I_c=I_0 \cdot cos(\omega_s t + \frac{4}{3}\pi)
\end{aligned}
$$
dove $\omega_s$ è la velocità di sincronismo pari a $2 \pi f_s$
La corrente su ciascun avvolgimento, genera un campo magnetico. Avendo invece una corrente sinusoidale, la direzione rimane la stessa, il verso si alterna ogni mezzo giro, il modulo varia con l'onda sinusoidale. 
Con 3 campi magnetici generati, possiamo calcolare la risultante con sovrapposizione degli effetti, ovvero un campo magnetico che ruota con velocità $\omega_s$. 
$\omega_r$ era invece la velocità di rotazione del rotore.
Quando $\omega_s=\omega_r$, il campo magnetico rimane fisso, il flusso non cambia e quindi la $fem$ indotta è 0, perciò non scorre corrente.
Se $\omega_s>\omega_r$, il campo ruota con $\omega_{slip}=\omega_s-\omega_r$, il flusso viene quindi diverso da 0 e il campo ruota in senso antiorario, il rotore viene frenato, fornendo l'energia generata.
Se $\omega_s<\omega_r$, il campo ruota con $\omega_{slip}=\omega_s-\omega_r$, il flusso viene quindi diverso da 0 e il campo ruota in senso orario, il rotore viene sostenuto nel moto, la macchina sta prelevando energia della rete.
La macchina viene detta macchina asincrona perché la pulsazione della corrente sul rotore è diversa dalla pulsazione della corrente sullo statore.

Un DFIG è un tipo specifico di generatore asincrono che ha un rotore a gabbia di scoiattolo ma con un'importante aggiunta: è dotato di un sistema di alimentazione esterno per il rotore che consente di controllare la corrente elettrica nel rotore. Questa corrente generata controllata può essere utilizzata per regolare la velocità e la potenza del generatore. Essenzialmente, il DFIG è in grado di funzionare sia come generatore che come motore, a seconda della direzione e dell'ampiezza della corrente di alimentazione nel rotore.


---

# Funzione obiettivo

$$
\begin{split}
	\min_{u}\bigg\{s(x(t_i+N)-x^{ref})^2+\sum_{t=t_i}^{t_i+N-1} 
	\bigg[q(x(t)-x^{ref})^2+rp(t)^2+c\big(u^{ev}(t)-\hat u^{ev}(t)\big)^2\bigg] \bigg \}
\end{split}
$$

Questa funzione obiettivo rappresenta 3 requisiti fondamentali:
-   Il nostro obiettivo è garantire che la quantità di energia prelevata dall'area di servizio al punto di consegna rimanga stabile senza picchi di consumo energetico, il che implica un profilo di consumo "dolce" rappresentato dalla funzione $p(t)$, la cui ampiezza è limitata. Per ottenere ciò, introduciamo il termine $rp(t)^2$ nella funzione obiettivo, cercando di minimizzarlo. Questo mira a ridurre la potenza richiesta al punto di allaccio, poiché una potenza più elevata comporterebbe costi operativi aggiuntivi per l'area di servizio.
- Parallelamente, desideriamo fornire ai clienti una quantità di energia $u^{ev}$ che sia il più possibile simile alla loro effettiva richiesta $\hat u^{ev}$. Tuttavia, questi due obiettivi sono in contrasto tra di loro: se cerchiamo di ricaricare alla massima potenza al punto di allaccio, ciò può portare a picchi di consumo energetico elevato; al contrario, se scegliamo una potenza di ricarica minima, l'energia fornita potrebbe risultare insufficiente. La funzione obiettivo agisce come un compromesso tra queste due esigenze.
- Inoltre, consideriamo la gestione dell'energia immagazzinata, che cerca di ottimizzare i due obiettivi sopra descritti. Questo viene realizzato fornendo temporaneamente una potenza elevata e consentendo una ricarica più lenta attraverso il termine $(x(t)-x^{ref})^2$ nella funzione obiettivo. Siamo disposti a caricare e scaricare l'accumulatore di energia, a condizione che lo stato di carica della batteria non si allontani eccessivamente dal valore di riferimento $x^{ref}$ in modo asintotico.

Sono tutti obiettivi che vanno in contrapposizione tra loro

---

# Formalizzazione WT

$$\begin{aligned}
	& x_1(t+1)=x_1(t)+Tu^{ess}(t)\\
	& x_2(t+1)=x_2(t)+\frac{T}{M}(w^{res}(t)-u^{res}(t))\\
	& p(t)=u^{ess}(t)+u^{ev}(t)-u^{res}(t)
	\end{aligned}
$$

$x_1(t)$ = è la variabile di stato di carica dello storage
$x_2$ = è la velocità angolare della macchina
$T$ = campionamento
$M$ = momento angolare
$u^{ess}$ = potenza rilasciata/assorbita dallo storage (alla batteria è associato un inverter, e questo oggetto è controllato, che ci permette di capire la corrente scambiata)
$u^{ev}$ = potenza assorbita dai veicoli
$u^{res}$ = la potenza elettrica che viene immessa dalla turbina in rete
$w^{res}$ = la potenza meccanica sulla turbina per la presenza del vento
$p(t)$ = potenza assorbita da tutta l'area di servizio al punto di allaccio con la rete di distribuzione (dove si trova il contatore)

---

# Formalizzazione PV

$$
\begin{aligned}
    & x(t+1) = x(t) + Tu^{ess}(t) \\
    & p(t) = u^{ess}(t) + u^{ev}(t) - w^{res}(t) \\
\end{aligned}
$$

$x(t)$ = dinamica dello stato di carica dello storage, espresso in KWh
$u^{ess}$ = potenza rilasciata/assorbita dallo storage (alla batteria è associato un inverter, e questo oggetto è controllato, che ci permette di capire la corrente scambiata)
$u^{ev}$ = potenza assorbita dai veicoli
$w^{res}$ = potenza (non controllabile) generata dal fotovoltaico
$T$ = tempo di campionamento
$p(t)$ = potenza assorbita da tutta l'area di servizio al punto di allaccio con la rete di distribuzione (dove si trova il contatore)

---

# Simulazioni 1


---
# Struttura 2

Questo è il prossimo obiettivo da elaborare

![[Progetto senza titolo.png]]

Abbiamo 2 casistiche:
- Rimuoviamo la comunicazione tra le due stazioni di ricarica e imponiamo un nuovo controllo. Invece che distribuire l'energia tra le due stazioni per soddisfare la domanda, distribuiamo la domanda per soddisfare l'energia disponibile.
- Stessa situazione della precedente ma non rimuoviamo la comunicazione, variamo energia e domanda a seconda della disponibilità 


---

# Simulazioni 2

---


---
# References