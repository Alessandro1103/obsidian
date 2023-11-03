Created on date 2023-08-03 at 01:43
Status:
Tags: #Tesi #Università #Appunti 

---
# Prima riunione

## Spiegazione1 (Concentrato su Camilla)

Obiettivo Camilla: è quello di sviluppare un controllore per la gestione ottima di un'area di servizio che ospiti colonnine di ricarica con la presenza di una turbina eolica e un sistema di storage (evoluzione del lavoro numero 3 (pdf)).
Obiettivo De Luca: è quella di cominciare a sviluppare il tema di coordinamento tra due aree di servizio diverse, due aree di servizio clone/semplificare rispetto a quelle che farà Camilla, con una rottura di simmetria: una colonna collegata a una turbina una a un pannello fotovoltaico.


### Formalizzazione con PV
PV = fotovoltaico


$$
\begin{aligned}
    & x(t+1) = x(t) + Tu^{ess}(t) \\
    & p(t) = u^{ess}(t) + u^{ev}(t) - w^{res}(t) \\
\end{aligned}
$$

$x(t)$ = dinamica dello stato di carica dello storage, espresso in KWh
$u^{ess}$ = potenza rilasciata/assorbita dallo storage (alla batteria è associato un inverter, e questo oggetto è controllato, che ci permette di capire la corrente scambiata)
$u^{ev}$ = potenza assorbita dai veicoli
$T$ = tempo di campionamento
$p(t)$ = potenza assorbita da tutta l'area di servizio al punto di allaccio con la rete di distribuzione (dove si trova il contatore)
$w^{res}$ = potenza (non controllabile) generata dal fotovoltaico

Le potenze sono positive se è assorbita, negativa se generata

I controlli li indichiamo per convenzione con u, e denominiamo l'apice per descrive a cosa fanno riferimento
I disturbi li indichiamo per convenzione con w

Quindi nella prima equazione, al tempo $T$ moltiplico la potenza $u^{ess}$ per $T$, ottengo una energia che sto aggiungendo/sottraendo. 

Nella seconda equazione, vediamo il bilancio energetico


$$
\begin{aligned}
    & 0 \leq u^{ev}(t) \leq \hat u^{ev}(t) \\
    & - u^{ess,max}(t) \leq u^{ess}(t) \leq u^{ess,max}(t) \\
    & x^{min}(t) \leq x(t) \leq x^{max}(t) \\
    & 0 \leq p(t) \leq p^{max}(t)
\end{aligned}
$$

$u^{ev}$ è una potenza assorbita, quindi positiva, con cappuccio ($\hat u^{ev}$) intendo la potenza richiesta dai veicoli (assorbimento massimo dei veicoli, sommati tra loro se più di 1). Questa dipende dal tempo, perche dipende dal numero di veicoli presenti nell'area di servizio.

In conclusione per ricavarci i valori controllabili ($u^{ess}$ e $u^{ev}$) noi ci affidiamo a una funzione obiettivo

Funzione obiettivo (di costo):
$$
\begin{split}
	\min_{u}\bigg\{s(x(t_i+N)-x^{ref})^2+\sum_{t=t_i}^{t_i+N-1} 
	\bigg[q(x(t)-x^{ref})^2+rp(t)^2+c\big(u^{ev}(t)-\hat u^{ev}(t)\big)^2\bigg]
	\bigg\}
\end{split}
$$
rappresenta 3 requisiti fondamentali:
- vogliamo che la potenza assorbita dall'area di servizio al punto di consegna non abbia picchi di potenza -> profilo dolce, $p(t)$ limitata. Quindi inseriamo nella funzione obiettivo una $rp(t)^2$ cercando di minimizzarla (minimizzazione della potenza al punto di allaccio, perché tanto più è alta tanto più l'operatore che esercisce l'area dovrà sostenere dei costi operativi maggiori)
- fornire ai clienti una potenza $u^{ev}$ quanto più vicina alla domanda effettiva $\hat u^{ev}$.
Questi 2 obiettivi sono in conflitto tra loro, se ricarico a massimo potenza al punto di allaccio ci sarà altrettanta potenza elevata, viceversa con potenza minima. La funzione obiettivo serve a questo
- Lo storage cerca di ottimizzare le precedenti 2 richieste, fornendo potenza richiesta (alta, temporaneamente) e venendo ricaricato lentamente: $(x(t)-x^{ref})^2$. Siamo disposti a caricare e scaricare la batteria purché lo stato di carica della batteria non si discosti troppo dal punto di riferimento $x^{ref}$ (asintoticamente)
Sono tutti obiettivi che vanno in contrapposizione tra loro.

Il disturbo w è positivo perche è energia pulita generata ma è una funzione del tempo, una grandezza potenzialmente aleatoria, che quindi può modificare parecchio il comportamento dei controlli. 

Il primo pezzo della funzione obiettivo è detto terminal cost: $s(x(t_i+N)-x^{ref})^2$
La sommatoria che è a destra va da $t_i$ fino a $t_i+N-1$, il termini iniziale è il termine 
con $t=t_i+N$, lo abbiamo tirato fuori perchè $x$ è una variabile estensiva, definita fino al tempo finale $t_i+N$, mentre le potenze $p(t)$ e $u^{ev}$ sono potenze definite fino al tempo $t_i+N-1$. 

Cosa accade quando aggiungiamo la turbina eolica? (sempre millie)
Il fotovoltaico lo trattiamo come un hardware non controllabile, la turbina eolica la trattiamo in maniera controllabile:

### Formalizzazione con WT
WT=turbina eolica

Mentre una batteria immagazzina energia elettrica, una turbina in rotazione è un oggetto che ha una sua energia cinetica, e immagazzina energia elettrica tramite questa energia cinetica. La turbina è soggetta a due momenti di forza, che sono parenti dei due momenti della Swing Equation: $J\frac{dw_m}{dt}+D_d w_m=\tau_t-\tau_e$, una che mantiene la turbina in movimento e una frenante ($\tau_t-\tau_e$). 
In questo caso la coppia meccanica è dovuta alla presenza del vento (offerta di energia), 
esiste anche qui una coppia elettromagnetica (domanda di energia), poiché la turbina è collegata a un azionamento elettrico, è possibile stabilire quanta potenza elettrica è immessa dalla turbina in rete.

$$\begin{aligned}
	& x_1(t+1)=x_1(t)+Tu^{ess}(t)\\
	& x_2(t+1)=x_2(t)+\frac{T}{M}(w^{res}(t)-u^{res}(t))\\
	& p(t)=u^{ess}(t)+u^{ev}(t)-u^{res}(t)
	\end{aligned}
$$

$x_1(t)$ è la variabile di stato di carica dello storage
$x_2$ è la velocità angolare della macchina
$T$ campionamento
$M$ inerzia della macchina
$u^{res}$ è la potenza elettrica che viene immessa dalla turbina in rete
$w^{res}$ è la potenza meccanica sulla turbina per la presenza del vento
$p(t)$ è  potenza assorbita da tutta l'area di servizio al punto di allaccio con la rete di distribuzione (dove si trova il contatore)

La seconda equazione, è l'equazione di stato della velocità angolare. Una variante della Swing Equation.
Giocando con $u_{res}$ e $w_{res}$ possiamo decidere la velocità angolare della macchina:
- se $u_{res}$ = $w_{res}$ non aggiungiamo ne energia elettrica o meccanica, quindi $x_2$ rimane costante
- se $u_{res}>w_{res}$ la turbina rallenta -> $x_2$ rallenta
- se $u_{res}<w_{res}$ la turbina accelera -> $x_2$ accelera

La situazione ideale è quella in cui la turbina riesce a fornire tutta la potenza richiesta dai veicoli ovvero dove $p(t)$ è uguale a 0

Nella funzione obiettivo abbiamo $x(t)$ ma questo comprende sia $x_1$ sia $x_2$, quindi ogni qualsiasi volta sia presente $x$ o $x^{ref}$ parliamo di un vettore.

## Spiegazione1 (Concentrato su Alessandro)

Si vorrebbe avere 2 aree di servizio, la prima con il modello sopracitato, quindi con un pannello fotovoltaico sia con turbina; mentre la seconda area di servizio è semplificata, magari con il solo fotovoltaico. Quale strategia dobbiamo adottare per coordinare le due aree di servizio?

Immaginiamo che una delle due aree sia scarsamente carica rispetto all'altra, possimo adottare 2 strategie:

- Strategia in potenza: le due stazioni sono elettricamente connesse quindi è possibile trasferire potenza da un area all'altra (tutto ancora da modellare)
- Strategia in domanda: le due stazioni non sono elettricamente connesse, andiamo quindi a modellare $\hat u_{ev}$, perché se assumo che $\hat u$ sia composta da $\hat u_1$ e $\hat u_2$ che fungono da addendi per la richiesta finale, posso dire che questo valore non è semplicemente un input al problema, ma potrebbe essere un input che dipende dallo stato dell'area di servizio. Detto in parole diverse, voglio che $\hat u$ cioè la domanda complessiva di potenza sulle due aree, la vado a ripartire tra le due aree (cioè mando le macchine all'area 1 o 2), ma questa ripartizione è dinamica dipendente dallo stato di carica delle varie aree.

---
# References

