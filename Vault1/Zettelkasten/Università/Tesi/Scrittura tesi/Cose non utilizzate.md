Date: 2023-09-19
Time: 20:43
Tags:

---
# Ricarica bidirezionale e l'uso delle batterie al litio (V2G e V2H)
La ricarica intelligente dei veicoli elettrici (EV) comporta vantaggi quali la riduzione dei costi operativi, un utilizzo s---ostenibile delle batterie e la promozione della mobilità elettrica. Sviluppare questo tipo di tecnologie può portare innumerevoli benefici. Una evoluzione degli attuali sistemi di ricarica, è la cosiddetta Ricarica bidirezionale. È una tecnologia che consente ai veicoli elettrici non solo di ricevere energia ma, qualora fosse necessario di immagazzinarla per fornirla poi in futuro a griglie di ricarica o le stesse abitazioni del proprietario.


## V2G
Il V2G è una tecnologia che consente il trasferimento bidirezionale di energia tra veicoli e la rete elettrica. Questo processo coinvolge conversioni di energia attraverso circuiti elettronici per adattare la potenza. L'integrazione di veicoli ibridi plug-in (PHEV) con reti intelligenti è di grande interesse per migliorare l'efficienza della rete. Veicoli ibridi caricano le batterie tramite il combustibile, mentre i veicoli elettrici le ricaricano dalla rete, ma entrambi sono utilizzati nella tecnologia V2G. Durante la ricarica, i veicoli sono collegati a stazioni di ricarica con convertitori di potenza e trasformatori collegati alla rete principale. Questi veicoli possono anche funzionare come alimentatori di energia ininterrotta (UPS). Vengono caricati quando la produzione di elettricità è alta o i prezzi dell'energia sono bassi, e possono vendere l'energia alla rete durante i periodi di carico di punta, migliorando l'affidabilità e l'efficienza del sistema energetico.

![[Pasted image 20230915165925.png]]

## V2H

Questa tecnologia riguarda l'utilizzo dell'energia immagazzinata nelle batterie dei veicoli elettrici per alimentare le abitazioni. Durante i periodi di bassa domanda energetica, come di notte, le batterie dei veicoli possono essere caricate e poi l'energia immagazzinata può essere ceduta alla rete quando la richiesta è alta. Un sistema V2H prevede un veicolo elettrico collegato a una stazione di ricarica. Un sistema di gestione energetica e un gestore del carico domestico operano in parallelo al veicolo. Un interruttore controllabile determina se cedere energia alla rete principale o utilizzarla internamente. Quando l'interruttore è aperto, il veicolo alimenta le abitazioni, monitorato dal sistema di gestione energetica. La capacità delle batterie domestiche varia da 3 a 30 kWh. Di conseguenza, la tecnologia V2H sfrutta l'energia dei veicoli elettrici per alimentare le case. L'infrastruttura è simile al V2G, ma si concentra sul trasferimento di energia alle abitazioni, agli edifici o ad altri veicoli elettrici. Tuttavia, le condizioni critiche includono la quantità di energia: da 5 a 10 kW per le case, 10-15 kW per gli edifici e 15-30 kW per i veicoli.

![[Pasted image 20230915165907.png]]


## Batterie 

Dato che l'EV diventerà un oggetto dai molti scopi, come quelli citati sopra, ha bisogno di migliorare l'elemento che più di tutti rappresenta una sfida e una opportunità di sviluppo, le batterie. Per quanto attualmente le batterie ricaricabili utilizzate sui EV siano principalmente al litio, è importante definire le 4 tipologie principali: batterie al piombo, batterie al nichel, batterie al litio e batterie post-litio. 

### Batterie al piombo

Inventate da Gastone Planté nel 1859, come la prima tipologia di batteria ricaricabile. Nonostante il progresso tecnologico sono tra le batterie più usate tuttora. Il motivo per la sua popolarità è l'affidabilità e il bassissimo costo. Il lato negativo sta nella durabilità. Il fatto di scaricare la batteria completamente ne riduce fortemente la capacità. A seconda della quantità di energia prelevata, l'acido di piombo offre da 200 a 300 cicli di scarica/carica. Questo fenomeno di invecchiamento è accelerato da temperature elevate e da scariche particolarmente violente.
Il piombo acido può andare da 1.7 V quando è scarica fino a 2.4 V quando è carica. Nel caso delle auto, la batteria è composta da 6 elementi al piombo acido, con il risultato di circa 12 V. 
Il suo funzionamento è molto interessante:

![[Batteria al piombo.png]]

Le molecole che si trovano nella soluzione acquosa ($H_2SO_2$ al $33\%$), si dissociano, rilasciando elettroni che passano dal polo negativo al positivo. All'interno della sostanza avviene uno squilibrio chimico che viene continuamente riequilibrato, tramite degli scambi elettrochimici tra i due elettrodi e la soluzione acquosa. Questo avviene fino a quando l'acido solforico scende fino ad una certa soglia rispetto a all'acqua.

Scarica: $Pb + PbO_2 + 2H_2SO_4 → 2PbSO_4 + 2H_2O$

- $H_2SO_2$ = Acido solforico
- $PbO2$ = Diossido di piombo
- $Pb$ = Piombo spugnoso
- $PbSo_4$ = Solfato di piombo
- $H_2O$ = Acqua
### Batterie al nichel

Nel 1899, fu introdotta la batteria al nichel-cadmio, rappresentando un notevole passo avanti rispetto alla batteria al piombo, che all'epoca era l'unica opzione ricaricabile disponibile. Nel corso degli anni, la tecnologia delle batterie al nichel-cadmio ha subito diverse evoluzioni significative. Una di queste evoluzioni ha portato alla creazione delle batterie NiCd ad alta capacità, che hanno aumentato la quantità di energia immagazzinata, ma con l'inconveniente di una minore durata nel numero di cicli di ricarica.

Oltre alle NiCd, altre varianti importanti includono le batterie al nichel-metallo idruro (NiMH) e al nichel-idrogeno (NiH). Le batterie NiMH, in particolare, hanno guadagnato popolarità tra i consumatori come alternativa alle pile alcaline usa e getta degli anni '90, che erano note per la loro vita limitata e l'efficienza di scarica.

Nel processo di scarica di una batteria NiCd, al livello dell'anodo, gli ioni $OH^-$ vengono convertiti in acqua, generando ioni idrossido liberi. Nel frattempo, gli ioni metallici nell'anodo subiscono un processo di ossidazione. Nel catodo, gli ioni di idrogeno reagiscono con gli ioni idrossido liberi per formare acqua. Il processo di carica è il medesimo ma in ordine inverso.

Scarica: $NiOOH + MH → Ni(OH)_2 + M$

- $NiOOH$ - Idrossido di nichel 
- $MH$ - Idrossido di metallo
- $Ni(OH)_2$ - Idrossido di nichel
- $M$ - Metallo 

### Batterie al litio e post

Inizialmente, la batteria al litio è stata sviluppata come una soluzione non ricaricabile con un enorme potenziale elettrochimico. Tuttavia, le prime versioni ricaricabili avevano un problema significativo: durante il processo di ricarica e scarica ripetuto, si formavano detriti nell'anodo. Queste particelle potevano penetrare il separatore della batteria, causando cortocircuiti pericolosi. Inoltre, la temperatura della batteria tendeva ad aumentare rapidamente, a volte sfociando in un pericoloso "sfiato con fiamma".

La svolta in questo scenario problematico si è verificata quando è stata introdotta una soluzione che utilizzava ioni di litio in modo non metallico. Sony è stata la pioniera in questo campo, introducendo la prima batteria al litio-ion (Li-ion) sul mercato. Questa innovazione rappresentava una svolta significativa.

Il processo di scarica di una batteria al litio inizia quando gli ioni di litio nell'anodo si spostano attraverso l'elettrolita verso il catodo, generando una corrente elettrica. Nel catodo, avviene una reazione chimica che rilascia energia utilizzata per alimentare il dispositivo. Questo processo comporta una diminuzione della concentrazione di ioni di litio nell'anodo e un aumento nel catodo, creando una differenza di potenziale che genera una tensione elettrica per alimentare il dispositivo.
Il processo di carica è il medesimo ma con ordine inverso.

Scarica: $LiCoO2 → Li + CoO2$

- $LiCoO2$ = Ossido di litio-cobalto
- $Li$ = Litio
- $CoO_2$ = Diossido di cobalto

Sono dotate di anodo ad alta percentuale di litio (da qui il nome) e il catodo generalmente ad alta densità di carbonio.


Le batterie sperimentali vivono principalmente nei laboratori protetti e comunicano con il mondo esterno attraverso rapporti promettenti ma unilaterali, spesso per attirare investitori. Infatti si hanno solo informazioni parziali su molti tipi batterie moderne. Di quelle più conosciute, molte derivano dal litio stesso, usando altre combinazioni chimiche. Maxwell Technology, per esempio, ha sviluppato l'elettrodo a secco che potrebbe aumentare l'energia specifica delle batterie al litio-ionico (Li-ion) del 50%, con il potenziale di raggiungere 500Wh/kg con risparmi nei costi di produzione.


### Conclusione

I nostri sistemi di batterie più comuni oggi sono le Li-ion e quelle al piombo. Tuttavia, entrambi i sistemi presentano sfide e limitazioni che richiedono una soluzione migliore. Sembrano emergere progressi, seppur in maniera graduale e eterogenea tra diverse alternative.
Memorizzare l'energia elettrica in modo economico rimane una delle sfide ancora irrisolte nella società moderna.
Per quanto riguarda la longevità, si stanno compiendo progressi nella batteria al litio-ion grazie all'uso di materiali catodici a cristallo singolo. Ottenere una vita più lunga e una capacità più elevata è guidato dall'industria dei veicoli elettrici che cerca una durata della batteria di 15 anni. 



---

# MPC

Il Model predictive control è una tecnica di controllo utilizzata per gestire sistemi dinamici. Non descrive una strategia di controllo particolare, ma identifica un insieme diversificato di approcci che si basano chiaramente sul modello utilizzato per rappresentare il processo. Basandosi su questo modello dinamico elabora una previsione del comportamento del modello stesso. Ottimizzare questa previsione significa trovare una miglior decisione che porta a un miglior risultato. I modelli sono quindi alla base di ogni forma di MPC. Il controllo si muove con il sistema, quindi ad ogni passo si propone una nuova previsione, più precisa della precedente. C'é quindi un momento iniziale in cui si instaura una prima idea. Comprendere i passi già compiuti permette anche di determinare in maniera piuttosto accurata lo stato iniziale del problema. La cosa che distingue l'MPC da un controllo convenzione è che la legge di controllo viene calcolata online. 
È fortemente versatile, può essere applicato su diversi sistemi, tra cui modelli dinamici lineari, input-output, distribuiti e così via. Di interesse è l'applicazione sul modello discreto, dimensionalmente finito, lineare a tempo invariante:
$$
\begin{aligned}
	& x(k+1) = Ax(k) + Bu(k) \\
	& y(k) = Cx(k) + Du(k) \\
	& x(0) = x_0
\end{aligned}
$$
dove $k \in N$. 

La tecnica "Receding Horizon", che rappresenta il funzionamento dell'MPC lavora su un loop che si risolve solo quando il tempo rimanente da analizzare si riduce a 0. È un processo metodico che segue alcuni punti fondamentali. Prima di tutto, all'inizio di ogni intervallo di campionamento, si effettua una previsione del comportamento futuro del sistema, utilizzando il modello definito in momento precedente. Viene formulato un problema di ottimizzazione per un orizzonte finito detto "orizzonte di predizione". Questo problema cerca di trovare la migliore sequenza di ingressi di controllo al fine di minimizzare una funzione di costo. Generalmente la funzione di consto è quadratica, per rendere le soluzioni uniche e computazionalmente efficienti. Infatti essendo quadratica, la funzione è convessa, il che rende il punto di minimo globale più facile da trovare. Successivamente il primo passo delle sequenza ottimale di ingressi di controllo viene applicato al sistema. Gli altri passi nella sequenza ottimale sono scartati. Questo processo viene ripetuto ciclicamente ad ogni intervallo di campionamento. Quando si arriva all'ultimo passo è possibile trovare dei pesi che si distinguono rispetto ai precedenti. Questo avviene perché spesso nella funzione obiettivo è inserito un costo terminale, che rappresenta il costo associato allo stato finale, spesso usato per raggiungere il requisito di stabilità del sistema. 

È importante definire dei vincoli che rendano il sistema sicuro e ben ottimizzato. Diversi sono i vincoli applicabili, quelli poi che vanno usati nel concreto dipendono dal problema; i più comuni sono quelli su ingresso, uscita e stato:
$$
\begin{aligned}
	& \underline u \leq u(k) \leq \overline u \\
	& \underline y \leq y(k) \le \overline y \\
	& \underline x \leq x(k) \le \overline x \\
\end{aligned}
$$
Per evitare variazioni brusche nei comandi di controllo, si può impostare dei vincoli anche sulla derivata degli ingressi.  Per il problema di questa tesi sono stati usati solo i precedenti. Sono utilizzabili anche ulteriori vincoli, non necessari in questo caso, ovvero vincoli sui tempi di campionamento, vincoli di sicurezza e ulteriori vincoli su variabili di controllo aggiuntive.



---
# References
