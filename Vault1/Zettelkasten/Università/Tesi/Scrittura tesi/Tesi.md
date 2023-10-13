# Cose da fare prima di considerare finito il lavoro

- [ ] 

---
# Titolo

Stazioni di Ricarica Intelligenti: Ottimizzazione delle Risorse Energetiche con Energia Rinnovabile e Controllo Predittivo

---
# Sommario (10/10)

Questo sommario offre un'anteprima degli scopi, delle motivazioni e delle ricerche presenti all'interno della tesi. L'obiettivo perseguito consiste nell'implementazione di un sistema di gestione e controllo per due stazioni destinate alla ricarica di veicoli elettrici (EV), focalizzando l'attenzione sull'utilizzo di risorse a basso impatto ambientale. 
Al fine di raggiungere questo obiettivo, è stato deciso di sfruttare due delle risorse rinnovabili più ampiamente disponibili in Italia, ossia l'energia eolica e l'energia solare. 
Per ottimizzare l'utilizzo delle risorse ambientali, sono stati incorporati, nell'ambito del progetto, sia turbine eoliche che pannelli fotovoltaici. Ogni stazione di ricarica è stata dotata di uno di questi sistemi, con l'intento di renderli l'unica fonte di energia per ciascuna stazione. Per ciascuna di queste, sono stati implementati controlli e supporti al fine di garantire una gestione efficiente dell'energia prodotta. Per i pannelli fotovoltaici, è stato introdotto un sistema di accumulo che consente di immagazzinare l'energia in eccesso quando la produzione supera la domanda. Per la turbina eolica, è stato integrato un sistema di controllo DFIG che regola la velocità delle pale, per aumentare la produzione durante i picchi di domanda.
Tuttavia, si riconosce che questa visione di dipendenza esclusiva dalle energie rinnovabili è attualmente difficile da realizzare in modo completo e affidabile. Pertanto, è stata inclusa nel sistema una fonte esterna di produzione che può essere utilizzata, in maniera simbolica, a pagamento; soprattutto in caso di necessità. 
Ciascuna stazione comprende delle colonnine di ricarica, un sistema di produzione tra quelli citati precedentemente e nel caso del fotovoltaico uno storage. Tra queste stazioni è presente un punto di allaccio che mette in connessione le 2 stazioni e la fonte esterna.
L'implementazione del sistema è stata sviluppata su 2 setup: il primo in cui è possibile scambiare energia tra le stazioni, oltre a riceverla dalla fonte esterna, e il secondo dove invece è possibile direzionare i veicoli tra le stazioni.  Si vuole presentare poi un setup conclusivo che unisce i vincoli elencati precedentemente. Visto che una soluzione non esclude l'altra perché non unirle e verificare quanto il sistema migliori rispetto alle situazioni precedenti.
Per controllare sia l'energia sia gli EV, il controllo impiegato è stato quello del Model Predictive Control (MPC). Questa tecnica è estremamente versatile e può essere applicata in una varietà di contesti. Tuttavia, è essenziale sviluppare un modello accurato che rappresenti adeguatamente il sistema da controllare, al fine di utilizzare con successo l'MPC. Il termine "predittivo" deriva dalla capacità del sistema di effettuare previsioni sul suo comportamento futuro, entro un certo numero di passi successivi. Per fare ciò, è necessario che il sistema operi in tempo reale e calcoli le azioni di controllo per un orizzonte di previsione futuro tramite un intervallo di campionamento.
Dal punto di vista pratico, l'implementazione di questo approccio è stata effettuata utilizzando il linguaggio di programmazione Julia, in cui sono stati sviluppati e compilati i modelli matematici necessari. Per risolvere i complessi problemi matematici associati all'MPC, è stato utilizzato il solver Gurobi.

# Introduzione (10/10)

Guardando qualsiasi rivista, telegiornale o social media, è facile notare un tema ricorrente, ovvero quello dell'eco-sostenibilità. Questo argomento ha ottenuto ampia copertura, ma può essere riassunto in maniera molto semplice come la capacità di un'attività o di un prodotto di essere sostenibile, cioè di non causare danni irreversibili all'ambiente o alla società. Ultimamente, sta diventando un principio fondamentale per coniugare la prosperità umana e la preservazione dell'ambiente ed è stato un processo che si è evoluto parallelamente all'impatto che l'uomo ha avuto sul mondo. In particolare, questa influenza umana è andata di pari passo con una trasformazione energetica. A partire dalla rivoluzione industriale, ogni progresso fatto ha utilizzato una fonte energetica sempre diversa, spesso peggiore della precedente. Raggiunta una consapevolezza del pericolo che si stava generando, si è cercato di spostarsi verso fonti di energia più sostenibili, come l'elettricità prodotta tramite sistemi green, l'idrogeno, il nucleare e così via. Il sistema elettrico, in molte applicazioni, funge da intermediario ed è considerato un passo avanti rispetto ai sistemi di combustione tradizionali. Tuttavia, è importante notare che potrebbe essere sostituito in futuro da fonti energetiche ancora più sostenibili. È necessario dire che questo sistema sta diventando valido solamente grazie alla produzione di energia green, che riduce il costo di produzione ed è quindi più accessibile all'utente medio. L'approccio alle risorse green è complicato e dipende dall'ambiente. Non ci si può affidare a una sola risorsa, poiché questa non garantirebbe una fornitura continua. Bisogna quindi cercare di variare in modo eterogeneo per avere sempre una fonte attiva pronta a rispondere alla domanda.
Di conseguenza, ci si è adoperati per l'analisi di due stazioni di ricarica. La prima stazione comprende una serie di colonnine di ricarica per i veicoli EV, di cui non interessa il numero ma la potenza richiesta in totale, perché su quella si dovrà lavorare. Tramite un collegamento a BUS, queste colonnine condividono lo stesso circuito di una turbina eolica DFIG, che sfrutta il suo sistema controllato per accelerare o rallentare le pale a seconda della domanda. Questa stazione non ha la possibilità di immagazzinare corrente, a differenza della seconda, che nel suo sistema di storage permette l'accumulo di energia non utilizzata. Anche la seconda presenta un numero non rilevante di colonnine collegate ad uno storage e, in questo caso, a una serie di pannelli fotovoltaici. I pannelli non presentano un sistema di controllo, poiché non esiste un equivalente applicabile alla turbina. Si potrebbero applicare dei controlli di tracciamento per ruotare il sistema in base alla fonte di energia, ma per semplicità sono stati esclusi anche dalla turbina. Centrale a tutto il progetto è l'intersezione fra le stazioni e una fonte esterna. Questo allaccio permette di sviluppare progetti e ideare strategie che consentano l'uso intelligente di tutti i dispositivi disponibili. Il progetto iniziale mira a analizzare come l'algoritmo intenda risolvere i problemi di domanda e se, come ci aspettiamo, metterà in comunicazione le stazioni. Il secondo mira a confrontare la soluzione ottenuta dalla condivisione di energia con la distribuzione di domanda; in altre parole, una volta scollegate le stazioni e modificando la direzione dei veicoli EV tra le varie stazioni, quale risultato si ottiene rispetto al precedente? Il terzo cerca di fornire una soluzione ottimale mescolando i due setup ideati per la stazione, cercando di evidenziare il miglioramento rispetto ai singoli. 

---
# Introduzione 2

Nel corso della storia umana, uno degli scopi primari dell'umanità è stato costantemente quello di migliorare la propria qualità di vita. Questo desiderio ha attraversato diverse epoche, dai nostri avi che sviluppavano tecniche di cucitura per sopravvivere al freddo, fino ai giorni nostri, in cui la tecnologia svolge un ruolo fondamentale nella comunicazione globale tra le persone. Questo percorso di miglioramento ha comportato la ricerca e la risoluzione di problemi sempre più complessi, che sembrano essere sempre più vicini alle nostre capacità. Ad esempio, se guardiamo alla storia dei mezzi di trasporto, la transizione all'elettrico è sempre stato qualcosa di immaginabile, non troppo lontano dalle menti delle persone. Ciò che ne ha ritardato la comparsa è il fattore tecnologico, che non permetteva a questi veicoli di confrontarsi con quelli già esistenti. In sostanza, il divario tra veicoli elettrici e veicoli a combustione era troppo ampio, le caratteristiche che sfruttavano la corrente non riuscivano a dare prospettiva a questi progetti. 
Con l'avvento di nuove tecnologie e soprattutto con l'utilizzo di risorse rinnovabili, molti dei problemi associati ai veicoli elettrici sono stati risolti. L'uso di risorse rinnovabili, che si rigenerano ad un ritmo maggiore rispetto al consumo umano, ha contribuito a ridurre i costi e migliorare l'implementabilità di questi veicoli. 
L'approccio alle risorse green è però ancora molto complicato. Non si può affidare un'intera infrastruttura a una sola risorsa, poiché questa non garantirebbe una fornitura continua. Per questo motivo si cerca di combinare più risorse per creare una sorta di coesione, garantendo un bilancio energetico sempre positivo. 
Per affrontare questo problema, nel contesto di questa tesi, è stata ideata un'infrastruttura che sfrutta due risorse complementari: l'energia solare e l'energia eolica. Queste risorse vengono impiegate in due stazioni di ricarica destinate ai veicoli elettrici.
Per entrare più nello specifico, la prima stazione è composta da una serie di colonnine di ricarica destinate ai veicoli EV. Il numero esatto di colonnine non è di grande rilevanza, poiché la potenza richiesta può variare da veicolo a veicolo. Pertanto, ci si è concentrati sulla determinazione di una potenza massima. Tuttavia, per scopi di chiarezza nel progetto, è stato fornito un numero approssimativo di 10 colonnine per stazione. Tramite un collegamento a BUS, queste colonnine condividono lo stesso circuito di una turbina eolica DFIG, che sfrutta il suo sistema controllato per accelerare o rallentare le pale a seconda della domanda. Questa stazione non ha la possibilità di immagazzinare corrente, a differenza della seconda, che nel suo sistema di storage permette l'accumulo di energia non utilizzata. Anche questa presenta 10 colonnine di ricarica, collegate stavolta, ad uno storage e a una serie di pannelli fotovoltaici. I pannelli non presentano un sistema di controllo, poiché non esiste un sistema equiparabile applicato alla turbina. Si potrebbero applicare dei controlli di tracciamento per ruotare il sistema in base alla fonte di energia, ma per semplicità questa opzione non è stata presa in considerazione. 
Centrale a tutto il progetto è l'intersezione fra le stazioni e il collegamento a una fonte esterna. Questo allaccio permette di sviluppare progetti e ideare strategie che consentano l'uso intelligente di tutti i dispositivi disponibili. 
Il progetto iniziale mira ad analizzare come l'algoritmo intende risolvere i problemi di domanda e se, come ci aspettiamo, metterà in comunicazione le stazioni. Il secondo obiettivo è quello di confrontare i risultati ottenuti dalla condivisione di energia con la distribuzione di domanda, ovvero valutare quale sia l'effetto di scollegare le stazioni e redistribuire i veicoli EV tra di esse rispetto alla situazione precedente Il terzo vuole mostrare come il sistema di controllo non si limiti all'utilizzo di un solo sistema di controllo, ma sia in grado di utilizzare entrambi.

---
# Indice


---
# Lista abbreviazioni etc

SCIM = Squirrel Cage Induction Motor (Motore a Induzione a Gabbia di Scoiattolo)
DFIG = Doubly Fed Induction Generator (Generatore a Induzione Doppiamente Alimentato)
EV = Electric Vehicle (Veicolo Elettrico)
MPC = Model Predictive Control (Controllo Predittivo)
IEC = International Electrotechnical Commission (Commissione Elettrotecnica Internazionale)
AC = Alternating Current (Corrente alternata)
CC = Direct Current (Corrente continua)
RCD = Residual Current Device (Dispositivo di Corrente Residua)
EVSE = Electric Vehicle Supply Equipment (Apparecchiatura per l'Alimentazione di Veicoli Elettrici)
CCS = Combined Charging System (Sistema di Ricarica Combinata)
DAFI = Directive Alternative Fuel Initiative (Iniziativa Direttiva sui Carburanti Alternativi)
AFIR = Alternative Fuel Infrastructure Regulation (Regolamento sull'Infrastruttura per i Carburanti Alternativi)
MASE = Ministro dell'ambiente e della sicurezza energetica
IRENA = International Renewable Energy Agency (Agenzia Internazionale per l'Energia Rinnovabile)
EASE = European Association for Storage of Energy (Associazione Europea per l'Accumulo di Energia)
V2G = Vehicle-to-Grid (Veicolo-alla-Rete)
LQ = Linear Quadratic (Lineare Quadratico)


---

# Modello

In questa sezione si discuterà la struttura che il modello deve avere e le varie componenti che verranno descritte singolarmente nei capitoli successivi.
**Immagini**
L'immagine in questione offre una rappresentazione chiara di tutte le diverse configurazioni considerate nelle varie simulazioni. La struttura in essa delineata include una fonte di energia al di fuori del nostro controllo. L'utilizzo di questa fonte è fortemente scoraggiato, poiché potrebbe impedire lo sviluppo di un sistema di ricarica intelligente. Per rispondere alle esigenze energetiche, sarebbe più auspicabile che le stazioni siano in grado di condividere energia tra di loro. A questa fonte sono connesse in

# Colonnine di ricarica

Con l'aumento del numero di EV, l'infrastruttura di ricarica, per agevolare l'uso dei veicoli, sta diventando fondamentale. Avere molte disponibilità di queste infrastrutture permette una ricarica rapida che non crea disagio tra gli utilizzatori di veicoli elettrici. Generalmente, ciascuna infrastruttura dispone di molteplici colonnine di ricarica, e ciascuna colonnina può avere diverse prese di allaccio, che possono fornire a loro volta diversi livelli di potenza. Consentire ai veicoli elettrici una maggiore disponibilità e una ricarica rapida permette la circolazione più veloce di tali veicoli.

Per le stazioni di ricarica la norma di riferimento è la IEC 61851-1, ovvero uno standard internazionale per i veicoli elettrici, pubblicata dall'IEC (International Electrotechnical Commission). Questa norma classifica le modalità di connessione dei veicoli elettrici alla rete di alimentazione in 5 diversi modi.
- Modo 1: è un tipo di connessione molto semplice. Viene utilizzato per veicoli elettrici di piccola taglia come biciclette elettriche e scooters. L'EV viene direttamente collegato a una rete AC, con limite di 16A e un voltaggio che varia tra i 250 e i 480V. In Italia è stato vietato per la ricarica pubblica. Essendo utilizzabile solo in ambito domestico, si usa principalmente una spina domestica, Schuko. Inoltre non presenta l'RCD, che invece è sempre presente negli altri modi. L'RCD è un dispositivo di sicurezza elettrica che è in grado di rilevare e interrompere automaticamente il flusso di corrente in un circuito quando viene rilevata una corrente residua o di dispersione. 
- Modo 2: permette la connessione tramite prese di corrente più potenti, con voltaggio tra 230 e 400V e fino a 32A. Anche in questo caso l'Italia non ha permesso l'uso in ambiente pubblico, infatti si ritorna agli ambienti domestici (Schuko) e anche industriali. Integrato con il sistema è presente un controllore del processo di ricarica ovvero l'In-Cable Control and Protection Device.
- Modo 3: si usa lo stesso voltaggio de modo 2. Sono stazioni di ricarica fisse, dette colonnine o Wall Box, e a differenza del modo 2, non presentano un controllore lungo il cavo, ma questo è già incorporato nella struttura principale, l'EVSE, ovvero un equipaggiamento di servizio per veicoli elettrici. 
- Modo 4: l'EVSE (Electric Vehicle Service Equipment), in questo caso è utilizzato per la conversione di corrente AC in CC. Queste stazioni incorporano quindi, oltre ai sistemi di controllo e protezione, il caricabatterie che regola la corrente di ricarica direttamente erogata alle batterie del veicolo. Viene utilizzato principalmente per la ricarica veloce, tra i 22 e i 350kW.
- Modo 5: questa modalità è specifica per la ricarica di e-bike e simili. Si utilizza una tensione molto bassa e particolarmente sicura, ovvero i 120V. L'infrastruttura in questo caso è una semplice presa in corrente alternata.

Con lo standard IEC 62196, sviluppato sempre dall'IEC, sono definiti i connettori da utilizzare nell'uso dell'industria automobilistica. Questa normativa descrive 3 design differenti con differenti configurazioni che supportano: 
- carica monofase fino a 16A, senza contatto del pilota di controllo
- ricarica monofase fino a 32A
- ricarica trifase fino a 63A (solo per i tipi 2 e 3)
Ciascun design include connettori maschio e femmina, nel seguente formato:
- una presa femmina sull'apparecchiatura di alimentazione del veicolo elettrico
- una spina maschio su uno degli estremi del cavo
- un connettore femmina sull'estremità opposta del cavo
- una entrata maschio sul veicolo stesso EV
L'EVSE può essere una stazione fissa, nel qual caso il cavo è permanentemente collegato e solo le ultime due interfacce sono rilevanti. In Europa, possono essere offerte stazioni non fisse, in cui il cavo è staccabile e sono presenti tutte e quattro le interfacce.
- Tipo 1: ha anche il nome di connettore Yazaki o connettore J1772 il connettore presenta un forma rotonda con 5 contatti utilizzati per 2 conduttori di corrente alternata, un conduttore di protezione e due pin di segnale. Questi pin di segnale servono per la funzione di controllo e la rilevazione di prossimità. Quando il connettore viene inserito nell'ingresso del veicolo viene bloccato in posizione da un meccanismo di chiusura meccanica integrato nel connettore stesso. Ha un limite di corrente, imposto dall'IEC, pari a 32A, in America fino a 80A. Non diffuso in Italia poiché non consente la ricarica trifase.
- Tipo 2: noto come connettore Mennekes. Presenta una forma rotonda appiattita su un lato, con fino a 7 contatti a pin e manicotto per un massimo di 4 conduttori AC, un conduttore protettivo e due pin di segnale utilizzati per la funzione di controllo e per la rilevazione di prossimità. Lo IEC ha imposto un limite di 63A con un massimo di 70 solo per apparecchiature monofase. Per lo standard Europeo ogni stazione di ricarica deve avere a disposizione una presa di tipo 2.
- Tipo 3: conosciuto come connettore Scame. La forma è un ovale appiattito su due lati, con fino a 7 contatti a pin e manicotto per un massimo di 4 conduttori AC, un conduttore protettivo e uno o due pin di segnale per la rivelazione di prossimità e per la funzione di controllo. Un perno ne permette l'aggancio per mantenere la spina in posizione.
  La EV Plug Alliance ha proposto 2 connettori dotati di interruttori, un tipo 3A, per la ricarica monofase, e un tipo 3C, per la ricarica rapida trifase.
- Tipo 4: anche noto come CHAdeMO, utilizzato in Giappone e in alcuni paese Europei. Utilizza il protocollo CAN-bus per la trasmissione di segnali di controllo. Il CAN-bus è stato progettato per funzionare anche in ambienti fortemente disturbati dalla presenza di onde elettromagnetiche.
Da menzionare è anche il Combined Charging System (CCS), ovvero un sistema di ricarica veloce ad alta tensione e corrente continua. Combina connettori di tipo 1 e 2 producendo 2 standard utilizzati da molte industrie automobilistiche:
- CCS Combo 1: utilizzato in Nord America, basato sul Tipo 1 per la ricarica a corrente alternata e un connettore aggiuntivo per la ricarica continua
- CCS Combo 2: utilizzato in Europa, basato sul Tipo 2 per la ricarica a corrente alternata e un connettore aggiuntivo per la ricarica continua

In particolare l'ACEA nel 2011 ha raccomandato l'uso del Tipo 2 Modo 3 come standard unico europeo, sia per case che per luoghi pubblici. E visto che IEC non ha imposto che in un cavo devono esserci gli stessi tipi di connettori, l'ACEA ha imposto che i produttori di veicoli elettrici devono equipaggiare i veicoli elettrici con prese Tipo 1 o Tipo 2, mentre le stazioni di ricarica dovranno avere sia Tipo 2 che Tipo 3. 

L'Italia, volendo abbracciare il mondo dei veicoli elettrici, è dovuta ricorrere a delle norme che ne permettessero una crescita direzionata. Nel 2016 venne presentato con forza un Decreto Legislativo conosciuto come DAFI (Directive Alternative Fuel Initiative) che implementa al livello nazionale, la direttiva 2014/64/EU, sullo sviluppo di infrastrutture alternative al combustibile. Fornisce anche delle linee guida per la sostituzione di autovetture, autobus, e veicoli di servizio degli enti pubblici, che se dovessero essere sostituiti, il 25% dei rimpiazzi deve consistere in EV, veicoli ibridi etc. Anche se questo Decreto è ormai molto datato, è stato uno dei primi notevoli passi avanti che l'Italia ha dovuto fare verso il l'elettrico. Infatti ancora oggi sono in corso alcuni contenuti che il Decreto forniva:
- Le stazioni di ricarica pubbliche devono fornire complessivamente almeno 1kW per ogni veicolo utilitario leggero ed elettrico a batteria
- Entro il 2025 devono essere disponibili stazioni di ricarica rapida con 150 kilowatt lungo le autostrade a distanze di 60 km e rifornimenti di idrogeno a distanze di 150 km.
- L'AFIR regola le opzioni di pagamento, e fornisce un quadro giuridico per tutti i membri dell'UE.

Per direzionare ulteriormente le spese sono successivamente usciti numerosi decreti, pubblicati dal MASE (Ministro dell'ambiente e della sicurezza energetica), che stanziano centinaia di milioni di euro e che definiscono tipologie di progetti e spese ammissibili, per ciascuna regione.
Grazie quindi a numerosi incentivi, anche da parte di molte aziende private, sono previsti più di 21000 stazioni di ricarica entro il 2026, che opereranno sia nelle zone urbane che non. 


---
# Turbina eolica (10/10)
Nel corso di pochi anni, il settore dell'energia fotovoltaica ha sperimentato un notevole incremento, attribuibile a diversi fattori chiave, tra cui una crescente sensibilizzazione ambientale, avanzamenti tecnologici e riduzione dei costi, incentivi governativi e un aumento della domanda energetica a livello globale.

In termini di investimenti globali nel settore delle energie rinnovabili, secondo dati raccolti da IRENA, la maggior parte di questi fondi è destinata all'energia solare fotovoltaica e all'energia eolica. Tuttavia, va notato che lo sfruttamento di queste risorse non è uniforme, ma dipende in gran parte dalla geografia di ciascun paese. In Italia, ad esempio, sono presenti parchi eolici in quasi tutte le regioni, con una capacità complessiva lorda di 11.858.430 kW. Tuttavia, la distribuzione di questi impianti è molto eterogenea, con una concentrazione maggiore nelle regioni del Sud, tra cui Campania, Puglia, Basilicata, Calabria, Sicilia e Sardegna, che primeggiano in termini di produzione pro capite.

Dal punto di vista strutturale, esistono vari tipi di turbine eoliche, con dimensioni che variano notevolmente. Ci sono turbine domestiche con un diametro di circa 2 metri, ma anche turbine di dimensioni più classiche, come quelle utilizzate nelle pale eoliche con un diametro di circa 80 metri. La più grande al mondo ha raggiunto dimensioni impressionanti di 164 metri.

## Approfondimento Turbina

Per quanto riguarda il funzionamento delle turbine eoliche, è importante notare che non è possibile catturare l'intera energia del vento. Ciò è dovuto all'angolo di inclinazione delle pale della turbina rispetto al vento, che può variare e influenzare la potenza rotazionale trasmessa. In realtà, molte turbine sono dotate di pale regolabili per ottimizzare l'efficienza.

La potenza generata da una turbina eolica è influenzata da vari fattori chiave. Per calcolare questa potenza, è utilizzata la seguente formula:
$$P_v=\frac{1}{2}\rho AV^3$$
Dove $P_v$ rappresenta la potenza del flusso d'aria, $\rho$ è la densità dell'aria, $A$ è l'area attraversata dalle pale della turbina (calcolabile come $\pi R^2$, con $R$ che rappresenta il raggio delle pale), e $V$ è la velocità del vento.

Va notato che non tutta l'energia cinetica del vento può essere convertita in energia meccanica rotazionale. La quantità convertibile è definita dal coefficiente di potenza ($C_p$), che può variare da 0 a 1. Questo coefficiente è influenzato dall'angolo di inclinazione delle pale ($\beta$) e dal tip speed ratio ($\lambda$).

Il tip speed ratio è un parametro chiave e viene calcolato come:
$$\lambda=\frac{\Omega_r \cdot  R}{V}$$

Dove $\Omega_r$ è la velocità angolare di rotazione della punta delle pale della turbina, $R$ è la lunghezza delle pale e $V$ è la velocità del vento.

Il coefficiente di potenza ($C_p$) varia in base a $\lambda$ e $\beta$ secondo una curva caratteristica. In generale, $C_p$ raggiunge il massimo a un certo valore di $\lambda$. Ciò implica che per ogni velocità del vento ($V$), esiste un valore ottimale di $\Omega_r$ che massimizza l'estrazione di potenza dall'aria.

In teoria, è possibile estrarre fino al 59% del flusso d'aria, ma nella pratica, i rendimenti realistici sono più spesso compresi tra il 35% e il 40% a causa di perdite e inefficienze.

Tuttavia, regolare la velocità di rotazione ($\Omega_r$) in modo che segua la variazione della velocità del vento è una sfida complessa. Il vento può variare rapidamente nel tempo, mentre la turbina ha una grande inerzia meccanica, il che significa che risponde lentamente alle variazioni del vento. Questa inerzia rappresenta una sfida nella regolazione della turbina per massimizzare la potenza estratta.

## SCIM

Per quanto riguarda il generatore, questo è posizionato tra un moltiplicatore di giri, applicato alle pale, e la rete elettrica. Serve per convertire la potenza meccanica in corrente elettrica. Il generatore, in questo caso un Doubly Fed Induction Generator (DFIG), è essenzialmente un motore elettrico a induzione, composto da due componenti principali: uno statore e un rotore a gabbia di scoiattolo. Per comprendere il funzionamento del DFIG, è importante spiegare prima la logica del motore a induzione a gabbia di scoiattolo (SCIM).

Il rotore dello SCIM ha 3 avvolgimenti indipendenti, distanziati di 120°, cortocircuitati, e quindi non alimentati. Lo statore, d'altra parte, contiene 3 avvolgimenti da cui escono 3 coppie di fili attraverso cui passa una corrente trifase alternata, descritta dalle seguenti equazioni:
$$ 
\begin{aligned}
	& I_a=I_0 \cdot cos(\omega_s t) \\
	& I_b=I_0 \cdot cos(\omega_s t + \frac{2}{3}\pi) \\
	& I_c=I_0 \cdot cos(\omega_s t + \frac{4}{3}\pi)
\end{aligned}
$$
Dove $\omega_s$ rappresenta la velocità di sincronismo, legata alla frequenza di alimentazione ($f$), generalmente 50 Hz in Europa. Questo sistema consente la definizione di una "rete bilanciata".

Se una corrente scorre su ciascuno di questi fili, essendo questa una sinusoide, il modulo varierà nel tempo; così come la direzione che varierà ogni semiperiodo, generando un campo magnetico variabile nel tempo $\vec B$. Se si considera il contributo di ciascun avvolgimento, la risultante è un vettore $\vec B$ che traccia un'ellisse alla velocità angolare $\omega_s$. Quando si è posizionati sul rotore e si prende come riferimento il rotore stesso, il campo magnetico $\vec B$ ruota alla velocità:
$$\omega_{slip}=\omega_s-\omega_r$$
dove $\omega_r$ è la velocità angolare delle pale $\Omega_r$ per un moltiplicatore di giri $n$.
Richiamando la formulazione di Faraday-Neumann-Lenz:
$$f.e.m. = \frac {\partial \Phi(\vec B)}{\partial t}$$
Questo spiega perché il motore è chiamato asincrono. Se $\omega_s = \omega_r$, il campo magnetico generato $\vec B$ rimane costante, quindi il flusso rimane costante e la forza elettromotrice indotta è pari a zero. In altri casi, quando c'è una variazione tra $\omega_s$ e $\omega_r$, il campo magnetico varia nel tempo, generando una corrente indotta diversa da zero, e ciò porta alla generazione di una forza elettromotrice, come descritto dalla seconda legge di Laplace:
$$	d \vec F = Id \vec l \times \vec B$$
In particolare se $\omega_s>\omega_r$, il campo ruota in senso antiorario e tramite il grafico sottostante, semplificato ad una sola spira, si può notare che il moto sia sostenuto da tale forza. Al contrario se $\omega_s<\omega_r$, il campo ruota in senso orario generando attrito. Quello di nostro interesse è il secondo perché fornendo resistenza, fornisce l'energia generata.
Il primo comportamento è quello di un motore, che consuma energia; è il comportamento di un generatore.

![[Pasted image 20230912172143.png]]
Nei casi a e b si è in sub-sincronismo, nei casi c e d in sovra-sincronismo

## Doubly Fed Induction Machine

Per controllare la direzione della corrente elettrica generata, è possibile applicare una tensione di controllo sull'avvolgimento del rotore. Questo consente di invertire la situazione da motore a generatore. Il sistema può generare corrente anche in situazioni di sub-sincronismo, grazie ai principi illustrati in precedenza. Questo tipo di generatore è chiamato Doubly Fed Induction Generator (DFIG) e offre una maggiore flessibilità e controllo rispetto ai generatori asincroni tradizionali.

![[Pasted image 20230912173646.png]]
Schema della turbina con DFIG

---
# Pannello fotovoltaico (10/10)

Nel giro di pochi anni, il settore dell'energia fotovoltaica ha sperimentato un notevole incremento, dovuto a una serie di fattori chiave. Questi includono una crescente consapevolezza ambientale, miglioramenti nelle tecnologie e nei costi, incentivi governativi e una crescente domanda energetica, tra altri.

In Italia, le regioni con il maggior numero di impianti fotovoltaici si trovano principalmente nel Nord del Paese. Tuttavia, in termini di energia pro capite prodotta, le regioni del Centro e del Sud si distinguono.

Il cuore dei sistemi fotovoltaici è rappresentato dalle celle fotovoltaiche. Attualmente, le più diffuse sono quelle in silicio cristallino, che solitamente hanno una forma quadrata e una superficie di circa 100 cm^2. Per garantire la corretta esposizione al sole, vengono utilizzate strutture di supporto, mentre morsetti posizionati agli estremi di ogni modulo consentono la raccolta della corrente generata. Il materiale predominante nelle celle fotovoltaiche è il silicio, che viene utilizzato in diverse forme:
- Silicio monocristallino: sebbene più costoso, può raggiungere un'efficienza che oscilla tra il 18% e il 21%.
- Silicio policristallino: sfrutta in modo più efficace la resa durante l'intera giornata, ma la sua efficienza massima si attesta intorno al 15%.
- Film sottile/Silicio amorfo: spesso molto sottile e flessibile, può essere utilizzato come un foglio, il che lo rende estremamente versatile. Tuttavia, l'efficienza è più bassa, generalmente tra il 5% e il 10%, e la sua durata di vita è limitata.

![[Pasted image 20230913115517.png]]

L'andamento della produzione di energia segue una curva caratteristica che consente il monitoraggio anche durante le ore notturne. Tuttavia, il comportamento delle celle può deteriorarsi significativamente se esposte per periodi prolungati ad alte temperature, poiché ciò influenza la larghezza della banda proibita. La banda proibita è l'intervallo in cui gli elettroni non possono passare dallo stato di valenza a quello di conduzione; con l'aumento della temperatura, questa banda si allarga, richiedendo un maggiore apporto di energia per consentire il passaggio degli elettroni.
Nel processo di assemblaggio del modulo fotovoltaico, le celle sono spesso protette da agenti atmosferici attraverso l'uso di diversi materiali:

- Lastra di vetro, che offre elevata trasparenza e, se temperata, maggiore robustezza fisica.
- Foglio sigillante (EVA), che gestisce la tenuta agli agenti esterni e fornisce un buon isolamento dielettrico.
- Isolante (Tedlar): utilizzato per migliorare lo scambio termico.

![[Pasted image 20230913121749.png]]

Escludendo situazioni di surriscaldamento, che possono essere gestite mediante un sistema di raffreddamento, l'attenzione principale è rivolta alle situazioni in cui il sole è presente. Pertanto, un sistema di controllo notturno per il pannello fotovoltaico non è necessario. In conclusione, ciò che otteniamo dai pannelli fotovoltaici è una grandezza non controllabile, che si può considerare come un disturbo.




---
# Storage (10/10)

L'accumulo di energia riveste un ruolo di fondamentale importanza nei sistemi energetici intermittenti, come quelli basati su energia solare ed eolica. Questo perché consente di sincronizzare l'offerta energetica con la domanda in modo più efficiente. Un esempio tangibile di questa sinergia è l'utilizzo dei veicoli elettrici (EV), che possono essere ricaricati durante le ore notturne, quando il sistema di produzione potrebbe essere fuori servizio, sfruttando l'energia accumulata durante l'intera giornata. Nel nostro contesto specifico, è stata data priorità alla carica delle batterie come misura preventiva, preparando il sistema ad affrontare picchi di domanda inattesi, che sarebbero altrimenti difficili da soddisfare senza un adeguato accumulo di energia.

Sebbene una batteria al litio possa soddisfare le nostre esigenze, è essenziale considerare una varietà di sistemi di accumulo energetico, ognuno con i propri vantaggi e svantaggi. Alcuni di questi potrebbero non essere adatti al nostro caso particolare, in quanto potrebbero differire notevolmente in termini di condizioni ambientali e obiettivi. Questi sono i sistemi di accumulo maggiormente utilizzati attualmente:
- Le batterie al litio son il tipo più comune di sistema di accumulo di energia utilizzato nelle stazioni di ricarica per veicoli elettrici. Queste batterie operano attraverso reazioni chimiche tra gli elettrodi positivi e negativi immerse in un elettrolita a base di litio. Durante la scarica, gli ioni di litio si spostano dall'anodo al catodo, generando energia elettrica, la fase di carica avviene il contrario. I vantaggi sono diversi e importanti, con questo tipo di batteria si ha una elevata densità energetica, il che significa che possono immagazzinare una grande quantità di energia in un piccolo spazio. Sono altamente efficienti nell'accumulare ed erogare energia, con perdite minime. Nonostante le dimensioni minime hanno una vita utile piuttosto lunga, che permette loro di essere particolarmente versatili. Tuttavia le batterie al litio possono essere costose poiché le risorse di litio sono limitate.
  Attualmente, le batterie agli ioni di litio possono essere assemblate utilizzando diverse celle, e la tensione di uscita varia in base al numero di celle presenti. Di solito, una singola cella di una batteria al litio funziona a una tensione di circa 3,6V.
- Le batterie al piombo-acido utilizzano una soluzione di acido solforico come elettrolita e piombo come materiale attivo negli elettrodi. Durante la carica il piombo di ossida, durante la scarica si riduce generando energia. Le batterie al piombo sono notevolmente meno costose rispetto a quelle al litio. Questo dipende dalla semplicità dei materiali e dalla grande storia che racconta. Al contrario delle batterie al litio hanno una densità relativamente bassa, il che implica che servono batterie più grandi per contenere la stessa energia contenuta in quelle al litio.
- I super-condensatori accumulano energia tramite l'accumulo di carica su superfici porose. Possono immagazzinare grandi quantità di energia sotto forma di campo elettrico. Hanno una capacità di carica e scarica molto rapida, con una vita utile altrettanto lunga. Il grande svantaggio di questi dispositivi si trova nella densità elettrica, che anche qui non ha paragoni con quella delle batterie al litio.
- Le pompe di accumulo utilizzano energia elettrica per pompare acqua in serbati posti a un livello superiore durante i periodi di abbondanza di energia e poi rilasciarla per generare energia idroelettrica quando necessario. Posseggono una vita utile altissima con alta efficienza, ma richiedono opportune condizione topografiche e costi di investimento iniziali elevati.
- I Flywheel sono sistemi che usano l'energia cinetica generata da un volano e la rilasciano quando necessario. Posseggono una reattività immediata, una lunga vita utile ma bassa densità energetica con sistemi di controllo avanzati.


![[Pasted image 20230913163648.png]]

Come evidenziato nella tabella qui sopra, emerge chiaramente che l'energia idroelettrica di pompaggio rappresenta l'opzione più conveniente e in costante crescita. Nonostante ciò, l'energia basata sull'idrogeno costituisce una prospettiva intrigante, sebbene necessiti ancora di ulteriori sviluppi prima di poter essere considerata una valida alternativa su larga scala.

Infine, è fondamentale sottolineare i notevoli benefici ambientali associati a questi sforzi. Secondo i dati raccolti dall'Associazione Europea per l'Accumulo di Energia (EASE), l'Europa avrà bisogno di implementare una capacità di accumulo energetico pari a 187 GW entro il 2030. Questo obiettivo è cruciale per sostenere in modo concreto la crescita e l'adozione delle fonti rinnovabili, contribuendo significativamente a mitigare i cambiamenti climatici e a garantire un futuro sostenibile per le generazioni a venire.

---
# Formalizzazione (10/10)

## Metodo di controllo

Uno dei metodi di controllo più avanzati e potenti utilizzati in una vasta gamma di settori industriali e applicazioni di ingegneria è il Model Predictive Control. L'MPC non stabilisce una strategia di controllo definita, ma identifica un insieme diversificato di approcci che si basano chiaramente sul modello utilizzato per rappresentare il processo. L'obiettivo dell'MPC è trovare un segnale che minimizzi una funzione obiettivo o funzione di costo, che rappresenta le dinamiche e gli obiettivi del sistema. Per trovare questa soluzione ha necessariamente bisogno di un modello dinamico del sistema ben descritto, che metta a disposizione stato e uscite controllabili o misurabili. Con questa semplice condizione è possibile generare qualsiasi controllo su qualsiasi modello, è infatti molto utilizzato per la sua semplicità e versatilità. 

Per comprendere i risultati ottenuti dall'MPC, bisogna capire il suo funzionamento di base. Il modello svolge un ruolo essenziale poiché costituisce la prima fase di un ciclo di analisi e computazione che è essenziale per l'implementazione del controllo. Successivamente vengono definiti gli obiettivi di controllo desiderati. Tra questi obiettivi ci possono essere il raggiungimento di un determinato setpoint, la minimizzazione o massimizzazione di una funzione di costo etc. Viene fornito al controllore un arco temporale di lunghezza $N$, l'obiettivo dell'MPC è trovare una serie di ingressi che nell'orizzonte temporale minimizzi l'uscita. In poche parole l'MPC cerca di capire cosa succederà nei successivi $N$ passi per elaborare un ingresso adeguato. Le previsione delle uscite del sistema possono essere rappresentate come $\hat y (t+k|t)$ per $k=1,\dots,N$ dove $k$ rappresenta il numero di passi nel futuro che stiamo cercando di prevedere. Mentre l'ingresso controllato è rappresentabile come $u(t+k|t)$ per $k = 0,\dots,N-1$. La scelta del numero di campioni da considerare è importante e dipende dalla memoria del processo. In generale il campione dell'uscita al passo $k$ è influenzato dai campioni precedenti dell'uscita fino all'istante $k-n$ e dei campioni dell'ingresso fino all'istante $k-n+m$ dove $m \leq n$. Se $m$ fosse maggiore di $n$ cadremmo in una situazione di non causalità. Quindi, una volta calcolato il primo passo, il controllo si applica sull'uscita che va da $k = 2,\dots ,N+1$, cioè iterativamente il controllo si sposta di un passo aggiustando i calcoli fatti in precedenza e svolgendone di nuovi. Questa situazione è principalmente influenzata dai fattori di disturbo, poiché i risultati previsti non necessariamente corrispondono ai risultati effettivi. I controlli vengono calcolati sulla base di un criterio di ottimizzazione per seguire una traiettoria di riferimento, che come detto precedentemente, può essere un setpoint o una funzione di minimo. Il segnale di controllo accettato viene processato mentre gli altri vengono scartati, poiché all'istante successivo ci saranno nuovi ingressi $(u(t_0), u(1), \dots , u(t_0+N-1))$.

In conclusione l'MPC ha bisogno unicamente di queste informazioni:

- Finestra a Orizzonte Mobile: Questo è un intervallo temporale che inizia da un punto di partenza arbitrario $t_0$ e si estende fino a $t_0+N$.
- Orizzonte di Previsione: Questo parametro rappresenta quanto lontano nel futuro vogliamo fare previsioni ed è determinato dalla dimensione $N$ della finestra temporale.
- Controllo a Orizzonte Mobile: Nonostante la finestra di pianificazione includa previsioni per un periodo più lungo (orizzonte di previsione), viene implementato solo il primo passo della sequenza di controllo ottimale ad ogni passo di campionamento, ignorando i passi futuri.
- Informazioni di Sistema: Nella fase di previsione, è necessario disporre di informazioni rilevanti sullo stato del sistema fino all'istante $t_0$. 
- Modello: Un modello accurato che descriva le dinamiche del sistema in modo soddisfacente. Un buon modello consente di fare previsioni precise sul comportamento futuro del sistema.
- Vincoli di Controllo: Vincoli che limitano i valori ammissibili dei segnali di controllo, garantendo che siano all'interno di limiti fisici o operativi.
- Vincoli di Stato: Vincoli sui valori ammissibili dello stato del sistema durante il periodo di previsione. Questi vincoli assicurano che il sistema rimanga all'interno di condizioni sicure o accettabili.
- Vincoli di Ottimizzazione: Vincoli aggiuntivi sulle variabili di ottimizzazione che influenzano il problema di controllo.

Un ultima menzione si potrebbe fare alle funzioni LQ. Queste funzioni di costo portano a problemi di ottimizzazione più semplici da risolvere, tendono a generare soluzioni "localmente" ottime senza ambiguità di segno.


**funzione minimo quadratica**

## Funzione obiettivo

Per realizzare delle simulazioni adeguate abbiamo bisogno di un modello valido che evidenzi esattamente quali siano gli obiettivi di controllo. Dobbiamo trattare quindi di variabili controllabili, ed evitare variabili indipendenti dal sistema come il vento o l'intensità di luce che colpisce i nostri pannelli. Per realizzare un controllo adeguato e pesare le variabili secondo necessità, utilizziamo una Funzione obiettivo:
$$
\begin{split}
	\min_{u}\bigg\{s(x(t_i+N)-x^{ref})^2+\sum_{t=t_i}^{t_i+N-1} 
	\bigg[q(x(t)-x^{ref})^2+rp(t)^2+c\big(u^{ev}(t)-\hat u^{ev}(t)\big)^2\bigg]
	\bigg\}
\end{split}
$$
dove $N$ rappresenta l'orizzonte di previsione.
Da questa formalizzazione è possibile modellare tutte le situazioni che possono essere di nostro interesse. Per ora ci riduciamo a discutere gli obiettivi già evidenti in questa formula: 

- Fornire ai clienti una potenza $u^{ev}(t)$ quanto più vicina alla domanda effettiva $\hat u_{ev}(t)$
- Lo stato $x(t)$, da specificare in un secondo momento, più vicino allo stato di riferimento $x^{ref}(t)$
- Evitare picchi di potenza richiesta dalla rete $p(t)$. Il vincolo all'interno della funzione obiettivo infatti si può riscrivere come $r(p(t) - p^{ref}(t))^2$, dove $p^{ref} = 0$ 

I pesi che vengono assegnati a ciascun requisito dipendono dall'obiettivo che il nostro modello. Idealmente vorremmo che tutto venga realizzato al massimo delle possibilità, ma visto che gli obiettivi sono in contrasto tra di loro bisogna riuscire a proporzionare in maniera corretta i moltiplicatori. 

Porre gli obiettivi non è sufficiente affinché i risultati siano soddisfacenti, se non imponiamo dei limiti fisici potrebbero esserci dei guasti o semplicemente staremmo descrivendo una situazione irrealizzabile nella vita reale. 

## Storage $x_1(t)$
$$
\begin{aligned}
    & x_1(t+1) = x_1(t) + Tu^{ess}(t) \\
    & x_1^{min}(t) <= x_1(t) <= x_1^{max}(t) \\
    & -u^{ess,min}(t) <= u^{ess}(t) <= u^{ess,max}(t) \\
\end{aligned}
$$

dove $x_1(t)$ rappresenta la dinamica dello stato di carica dello storage, $u^{ess}(t)$ è la potenza rilasciata o assorbita dallo storage in ogni istante di tempo, moltiplicata per il tempo di campionamento $T$.
L'evoluzione dello stato di carica è rappresentato dal primo vincolo: il valore al tempo $t+1$ è dato dalla somma di quello attuale $t$ e dalla potenza ricevuta/assorbita successivamente. Il limite massimo imposto allo storage dipende solo dalle possibilità fisiche realizzabili, mentre il valore minimo, cioè quello di uno storage scarico è 0. È da specificare che essendo $u^{ess}(t)$ uno scambio di potenza, deve essere compresa in un intervallo simmetrico sia negativo che positivo. Per far comprendere la cosa in maniera più diretta, $u^{ess,min}(t)$ è stato considerato un valore positivo, con davanti un meno.

## Velocità angolare $x_2(t)$

$$
\begin{aligned}
	& x_2(t+1)=x_2(t)+\frac{T}{M}(w^{res}(t)-u^{res}(t)) \\
	& x_2^{min}(t) <= x_2(t) <= x_2^{max}(t) \\
	& u^{res,min}(t) <= u^{res}(t) <= u^{res,max}(t)
\end{aligned}
$$

dove $x_2(t)$ rappresenta la velocità angolare della macchina, $u^{res}(t)$ è la potenza elettrica che viene immessa dalla turbina in rete, sottratta alla potenza meccanica $w^{res}(t)$ sulla turbina generata dalla presenza del vento. T rappresenta il tempo di campionamento, e M l'inerzia della macchina. La prima equazione descrive lo stato della velocità angolare. Modificando $u^{res}(t)$ e $w^{res}(t)$ possiamo gestire la velocità angolare della macchina.
 - Se $u_{res} = w_{res}$ non vengono aggiunte ne potenze elettriche ne meccaniche, quindi $x_2$ rimane costante
 - Se $u_{res} > w_{res}$ stiamo aggiungendo una quantità negativa che rallenta $x_2$
 - Se $u_{res} < w_{res}$ vi è un contributo allo stato attuale e quindi $x_2$ accelera
Il valore minimo che $x_2(t)$, nel suo corretto funzionamento, non è 0, normalmente le turbine sono progettate per bloccarsi quando la velocità del vento che le colpisce è minore di un certo valore. $u^{res}(t)$ invece è una grandezza unidirezionale che quindi può essere solo positiva.


## Potenza non immessa dalla turbina
$$
\begin{aligned}
	& P_v = \frac{1}{2} \rho AV^3 \\
	& P_r=C_p(\lambda,\beta)\cdot P_v = \frac{1}{2}\rho\pi R^2\cdot C_p(\lambda,\beta)\cdot V^3 \\
	& \lambda=\frac{\Omega_r \cdot  R}{V} \\
\end{aligned}
$$
Il simbolo $P_v$ denota la potenza cinetica contenuta nel flusso d'aria che interagisce con la superficie de la pala di una turbina eolica. Questa superficie può essere descritta come l'area compresa all'interno del cerchio di raggio $R$ (la lunghezza della pala). La potenza meccanica generata dal flusso d'aria deve essere trasformata in potenza meccanica rotazionale utilizzando un parametro noto come coefficiente di potenza ($C_p$). Questo coefficiente è una funzione che dipende da un rapporto adimensionale chiamato $\lambda$, con il suo valore massimo solitamente raggiunto intorno a 0,4. L'angolo $\beta$, che rappresenta l'inclinazione fissa della pala rispetto al vento. Per convenzione immaginiamo questo angolo come fisso, realisticamente sarebbe possibile muoverlo a seconda della direzione del vento.. Il rapporto $\lambda$ è definito come il rapporto tra la velocità angolare di rotazione della turbina $\Omega_r$ (la velocità tangenziale alla punta della pala) e la velocità del vento incidente. Questo parametro riflette l'efficienza della pala nella cattura dell'energia cinetica del vento.

## Potenza all'allaccio
Di base il nostro progetto comprende 2 stazioni quindi a seconda di come vogliamo distribuire la potenza alcuni vincoli possono variare. Ciascun modello applica delle condizioni sui seguenti vincoli rendendoli funzionali per il modello stesso.
$$
\begin{aligned}
	& p_{rete}(t) = p_{wt}(t) + p_{pv}(t) \\
	& p_{wt}(t) = u^{ev}_{wt}(t) - u^{res}_{wt}(t) \\
	& p_{pv}(t) = u^{ess}(t) + u^{ev}_{pv}(t) - u^{res}_{wt}(t) \\
	& p_{rete}^{min}(t) <= p_{rete}(t) <= p_{rete}^{max}(t) \\
\end{aligned}
$$
Il nodo centrale funge da ponte per condividere potenza in tutte le direzioni. La prima equazione rappresenta l'equilibrio delle potenze. La seconda e la terza equazione mostrano l'equilibrio di ciascuna stazione, tra potenze generate e consumate. 
Nell'ultima equazione, $p_{rete}^{min}(t)$ potrebbe essere negativa. Questo significherebbe che laddove la quantità di energia prodotta fosse più alta del fabbisogno, l'eccedenza può essere immessa in rete con un guadagno proporzionale.

## Potenza per i veicoli

$$
\begin{aligned}
	& u^{ev,min}_{wt} <= u^{ev}_{wt} <= \hat u^{ev}_{wt} \\
	& u^{ev,min}_{pv} <= u^{ev}_{pv} <= \hat u^{ev}_{pv} \\
\end{aligned}
$$
I vincoli di minimo possono essere sostituiti direttamente con 0. Sarebbe possibile considerare valori negativi ma si dovrebbe parlare di una tecnologia ancora lontano dall'uso quotidiano, il V2G (vehicle to grid).

## Decisione domanda
Nella seconda e terza situazione abbiamo distribuzione della domanda inclusa nel problema di ottimizzazione, quindi dobbiamo imporre dei vincoli ulteriori e l'introduzione di alpha. 

$$
\begin{aligned}
	& \hat u^{ev}_{pv}(t) = \hat u^{ev}(t) \cdot alpha(t) \\
	& \hat u^{ev}_{wt}(t) = \hat u^{ev}(t) \cdot (1 - alpha(t)) \\
\end{aligned}
$$

In questo modo il sistema si arricchisce e nella stessa funzione obiettivo, un termine che prima era impostato da noi, diventa una variabile di decisione su cui il sistema può lavorare per rendere più facile il proprio lavoro.

$$

$$


---
# Simulazioni (0/10)

In questo capitolo vengono affrontate tutte le simulazioni che possono interessare il nostro problema. 


---
# Conclusioni (0/10)
​

---
# Citazioni 

[](https://books.google.it/books?id=qzvzWxCLRGMC&lpg=PA1&ots=lpHL7DLqKE&dq=Energia%20rinnovabile&lr&hl=it&pg=PA1#v=onepage&q&f=false)
[](https://www.enelgreenpower.com/)
[](https://download.terna.it/terna/5%20-%20PRODUZIONE_8db99b7e93be883.pdf)
[](https://download.terna.it/terna/3%20-%20IMPIANTI%20GENERAZIONE_8db99b7c8a48aab.pdf) 
[](https://www.annualreviews.org/doi/pdf/10.1146/annurev.eg.14.110189.001325)
[](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=6910809)
[](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9923066)
[](https://batteryuniversity.com/)
[](https://sites.engineering.ucsb.edu/~jbraw/mpc/MPC-book-2nd-edition-4th-printing.pdf)
[](https://www.acea.auto/files/charging_20110511.pdf)
[](https://www.e-station.it/guida-alla-ricarica.html)
[](https://elettricomagazine.it/emobility/ricarica-veicoli-elettrici-4-modi-norma-iec-61851-1/)
[](https://www.acea.it/guide/batterie-al-litio)
