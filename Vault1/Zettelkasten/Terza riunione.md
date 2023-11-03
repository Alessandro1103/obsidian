Date: 2023-11-03
Time: 23:04
Tags: #Tesi #Università #Appunti
Up: [[Tesi]]

---
# Terza riunione

## Approfondimento

![[Pasted image 20230504170124.png]]
Vogliamo scrivere il modello dinamico di questa macchina a induzione, in particolare quella a doppia induzione. Dobbiamo scrivere le equazioni a maglia di ciascuno di questi circuiti.
Posso vedere la prima colonna a sinistra come una maglia come 3 avvolgimenti di rotore, che hanno ciascuno una propria resistenza, una propria induttanza e una induttanza mutua con gli altri avvolgimenti del circuito.
In particolare ci interessa come varia la corrente in vicinanza degli avvolgimenti destri e sinistri.
$$
\begin{aligned}
	 V_{sk}=R_sI_{sk}+\frac{d}{dt}\phi_{sk}\\
	 V_{rh}=R_rI_{rh}+\frac{d}{dt}\phi_{rh}\\ \\
\end{aligned}
$$
con $k\in\{a,b,c\}$ e  $h\in\{a,b,c\}$
$\phi$ è un flusso che scrivo come: 
$$
\begin{aligned}
	& \phi_k=\sum_i{L_{ki}(\theta) \cdot I_i}
\end{aligned}
$$

$L_{ki}$ è l'induttanza mutua
la moltiplichiamo per la corrente ($I_i$), ma questa induttanza dipende dalla posizione reciproca, entrano quindi in gioco seni e coseni, portando le equazioni a essere non lineari.

Le equazioni di maglia sono semplici, ma i flussi, sono prodotti di paramenti dipendenti dagli angoli per corrente, che quindi sono prodotti non lineari. Il modello diventa quindi troppo complicato, inoltre le variabili Kirchhoff non sono buone variabili per rappresentare i gradi di libertà della terna simmetrica.

### Nuovo sistema di coordinate
Bisogna introdurre un nuovo sistema di coordinate
Prendiamo il sistema di riferimento di Park, quando consideriamo una terna trifase simmetrica (la X può rappresentare sia la corrente, sia il voltaggio, sia il flusso$\dots$), questa terna che dipende dal tempo, si può interpretare come un punto in uno spazio $R^3$, che si muove al variare del tempo secondo le leggi che descrivono la terna:

$$
	\begin{pmatrix}
		X_a \\
		X_b \\
		X_c 
	\end{pmatrix}
	= 
	\begin{pmatrix}
		X \;cos(\omega t)\\
		X \;cos(\omega t - \frac{2\pi}{3}) \\
		X \;cos(\omega t + \frac{2\pi}{3}) 
	\end{pmatrix}
$$
Viene introdotto ragionando sul tipo di traiettoria che questa terna trifase esegue nello spazio $R^3$, che tipo di traiettoria corrisponde a questa legge di moto?

Prima considerazione:
per costruzione la terna è fatta tale che sommando le componenti la somma faccia zero, se la somma vettoriale è 0 anche quella scalare è 0:

$$
\begin{aligned}
	X_a+X_b+X_c=0
\end{aligned}
$$

questa è equazione rappresentante un piano quindi sono elementi perpendicolari a $(1\; 1\; 1)$, la traiettoria giace solo un piano, non su tutto $R^3$
posso riscriverla anche come: 

$$
\begin{aligned}
	(1\;1\;1)\
	\begin{pmatrix}
		X_a\\
		X_b\\
		X_c
	\end{pmatrix}
	=0
\end{aligned}
$$

Facendone il quadrato, e sommandole, ottengo:
$$
\begin{aligned}
X_a^2+X_b^2+X_c^2=X^2\left[cos^2\omega t+cos^2\left(\omega t-\frac{2\pi}{3}\right) + cos^2\left(\omega t +\frac{ 2\pi}{3}\right)\right] =
\end{aligned}
$$
ricordando che:
$$
\begin{aligned}
cos^2x  = \left(\frac{e^{ix}+e^{-ix}}{2}\right)\left(\frac{e^{ix}+e^{-ix}}{2}\right)=\frac{2+e^{2ix}+e^{-2ix}}{4} = \frac{1}{2}\left(1+cos2x\right)
\end{aligned}
$$
questo porta a:
$$
\begin{aligned}
=\frac{X^2}{2}\left[3+cos2\omega t + cos\left(2\omega t-\frac{4\pi}{3}\right)+cos\left(2\omega t+\frac{4\pi}{3}\right)\right]
\end{aligned}
$$
quindi la soluzione finale porta a:
$$
\begin{aligned}
X_a^2+X_b^2+X_c^2=\frac{3}{2}X^2
\end{aligned}
$$
Che cosa rappresenta questa equazione? Una sfera, che ha raggio $\sqrt{\frac{3}{2}}X$
Quindi sappiamo che la traiettoria appartiene alla superficie di una sfera centrata nell'origine, ma deve anche appartenere ad un piano che è ortogonale, o meglio i cui vettori sono ortogonali, al vettore $(1\;1\;1)$. La traiettoria si svolge all'intersezione nel piano e una sfera, ovvero una circonferenza (come prevedibile visto i 2 soli gradi di libertà della terna). 

Ci accorgiamo che non servono 3 coordinate per rappresentare una terna trifase, ce ne bastano 2. Considero una nuova base di vettori nello spazio, eliminando i vettori di base di Kirchhoff 
$$
\begin{Bmatrix}
\begin{pmatrix}
1\\ 0\\ 0 
\end{pmatrix}
\begin{pmatrix}
0\\ 1\\ 0 
\end{pmatrix}
\begin{pmatrix}
0\\ 0\\ 1
\end{pmatrix}
\end{Bmatrix}
$$
e vado a prendere 3 nuovi vettori di base:
2 che giacciono sul piano dove avviene il moto, e il terzo che è proprio il vettore $(1\;1\;1)$ che è ortogonale al piano. Se la terna è simmetrica, la terza componente nel nuovo sistema è sempre 0, perché il moto è sul piano.
I 2 vettori posso prenderli fissi, oppure come fa Park, dipendenti dal tempo, cioè due vettori che ruotano sul piano alla stessa velocità della terna, per esempio posso prendere come primo vettore (diretto) di base la terna stessa:
$$
\begin{aligned}
e_d=\left(cos\omega t+cos\left(\omega t-\frac{2\pi}{3}\right) + cos\left(\omega t + \frac{2\pi}{3}\right)\right)^t
\end{aligned}
$$
Il secondo vettore (quadratura) di base lo scelgo ancora sul piano, indipendente e ortogonale al primo. Per farlo mi basta sfasare gli angoli di $\frac{\pi}{2}$:
$$
\begin{aligned}
e_q=\left(cos\left(\omega t+\frac{\pi}{2}\right)+cos\left(\frac{\omega t-2\pi}{3}+\frac{\pi}{2}\right) + cos\left(\frac{\omega t + 2\pi}{3}+\frac{\pi}{2}\right)\right)^t
\end{aligned}
$$
(t rappresenta trasposizione)
ovvero:
$$
\begin{aligned}
e_q=\left(-sin\omega t-sin\left(\omega t-\frac{2\pi}{3}\right) - sin\left(\omega t + \frac{2\pi}{3}\right)\right)^t
\end{aligned}
$$
L'ultimo (omopolare) abbiamo detto essere:
$$
\begin{aligned}
e_0=\left(1\;1\;1\right)^t
\end{aligned}
$$
Sono tutti ortogonali tra loro, ma non ortonormali (dobbiamo vedere quando vale il modulo di $e_q$ ed $e_d$):
![[Pasted image 20230504221543.png]]
![[Pasted image 20230504223232.png]]
(manca la radice, errore slide)
Mettendo questi vettori per riga su una matrice e ottengo:
![[Pasted image 20230504223338.png]]
dove $\alpha=\omega t$ 

I vettori di base normalizzati, abbiamo preso i vettori riga, per calcolare la matrice di trasformazione, dovrei prendere i 3 vettori metterli in colonna, calcolare l'inversa, e i vettori riga dell'inversa sono proprio quelli che rappresentano i vettori sinistri della matrice di trasformazione, ma visto che la base è ortonormale la matrice inversa è uguale alla matrice trasposta. 

Matrice di trasformazione di coordinate
Se io quindi applico questa matrice a una terna trifase ottengo una nuova terna in un nuovo sistema di coordinate:
$$
	\begin{pmatrix}
		X_d \\
		X_q \\
		X_0 
	\end{pmatrix}
	= T(\alpha)
	\begin{pmatrix}
		X_a\\
		X_b \\
		X_c 
	\end{pmatrix}
$$
Se la terna è simmetrica solo 2 dei 3 elementi saranno diversi da 0

### Equazioni di DFIG
Per ottenere le equazioni di circuito nel sistema di riferimento di Park utilizziamo la trasformazione inversa sulle equazioni di Kirchhoff dello statore e del rotore
$$
	\begin{pmatrix}
		X_a(t)\\
		X_b(t) \\
		X_c(t) 
	\end{pmatrix}
	= T(\alpha)^t
	\begin{pmatrix}
		X_d(t) \\
		X_q(t) \\
		X_0(t) 
	\end{pmatrix}
$$
Scriviamo in forma vettoriale le equazioni di Kirchhoff:
$$
\begin{aligned}
	\begin{pmatrix}
		V_{sa}(t)\\
		V_{sb}(t)\\
		V_{sc}(t)
	\end{pmatrix}
	= R_s
	\begin{pmatrix}
		I_{sa}(t)\\
		I_{sb}(t)\\
		I_{sc}(t)
	\end{pmatrix}
	+\frac{d}{dt}
	\begin{pmatrix}
		\phi_{sa}(t)\\
		\phi_{sb}(t)\\
		\phi_{sc}(t)
	\end{pmatrix}
	\\\\
		\begin{pmatrix}
		V_{ra}(t)\\
		V_{rb}(t)\\
		V_{rc}(t)
	\end{pmatrix}
	= R_r
	\begin{pmatrix}
		I_{ra}(t)\\
		I_{rb}(t)\\
		I_{rc}(t)
	\end{pmatrix}
	+\frac{d}{dt}
	\begin{pmatrix}
		\phi_{ra}(t)\\
		\phi_{rb}(t)\\
		\phi_{rc}(t)
	\end{pmatrix}
\end{aligned}
$$
![[Pasted image 20230504233528.png]]
 A un certo punto abbandono l'equazione omopolare, poiché sempre identica 0=0 e arrivo dopo una serie di calcoli a:
 ![[Pasted image 20230504233731.png]]

Uguagliando a zero la prima, la terza e la quarta equazione, sono anche le equazioni della macchina a induzione. Analogamente si possono trasformare le equazioni di flusso:
![[Pasted image 20230504233932.png]]

che portano alle Equazioni di Stato:
![[Pasted image 20230504234047.png]]
dove $L_r'=L_r-\frac{M^2}{L_s}$  chiamata induttanza transitoria, sono dei coefficienti che (sulle slide si può vedere meglio) vanno a moltiplicare la corrente per definire il flusso
$L_r$ è l'autoinduttanza del rotore
$L_s$ è l'autoinduttanza di statore
$M$ è l'induttanza mutua

Aggiungiamo la solita equazione di coppia meccanica:
![[Pasted image 20230504234107.png]]

dove la $\tau_m$ (coppia meccanica) è definita come:
$$
\begin{aligned}
\tau_m=\frac{P_{mech}}{\Omega}
\end{aligned}
$$
$P_{mech}$ è la potenza meccanica
$\Omega$ è la velocità angolare

ma la $P_{mech}$ è la stessa già discussa in precedenza:
$$
\begin{aligned}
P_{mech}=\frac{1}{2}\rho\pi R^2C_p(\lambda,\beta)v^3
\end{aligned}
$$
la $\tau_e$ (coppia elettrica è invece) è definita come:
$$
\begin{aligned}
\tau_e=\frac{MV_s}{L_s\omega_s}I_{qr}
\end{aligned}
$$

è più conveniente avere come variabile di stato non $\omega$ ma $\omega_{slip}$ (omega di scorrimento)

#### Forma finale

Equazioni di stato:
![[Pasted image 20230504234913.png]]

lo stato sono le derivate a sinistra, e dipendono dal tempo, gli ingressi sono $V_{dr}$ (componente diretta del rotore) e $V_{qr}$ (componente in quadratura del rotore), questi sono nel sistema di Park i due gradi di libertà della terna simmetrica. $\tau_m$ è l'ultimo elemento dipendente dal tempo (a differenza della macchina sincrona, perché in realtà qui la $\tau$ è ricavata anche tramite la velocità angolare, è la coppia meccanica applicata dalla turbina per effetto del vento

Uscita:
![[Pasted image 20230504235505.png]]

Ci interessa la potenza elettrica generata (attiva e reattiva), calcolata a partire dalla definizione di potenza elettrica:
$$
\begin{aligned}
P=\frac{3}{2}\;VI\;cos\phi
\end{aligned}
$$
esprimibile tramite calcoli formulati nelle slide:
$$
\begin{aligned}
P=V_d\;I_d+V_q\;I_q
\end{aligned}
$$
e da questa si arriva a quelle scritte nella soluzione.

### Controllore

Il modello ottenuto è di questa forma:
![[Pasted image 20230505001036.png]]

Abbiamo un processo, ingresso e uscita, e vogliamo controllare l'uscita
Ci basterebbe controllare $I_{qr}$, per ora abbiamo ottenuto:
...
![[Pasted image 20230504173803.png]]

la coppia meccanica $\tau_m$ è il disturbo che tiene in vita la turbina, che voglio renderne gli effetti buoni, voglio evitare che le fluttuazioni generino fluttuazioni interne, regolandone gli effetti.

Si procede scegliendo un controllo che ha 2 componenti, potrei scegliere $V_{dr} in modo da cancellare il termine non lineare: $\omega_{slip}I_{qr}$ + una seconda componente che diventerà il nuovo controllo, il tutto prenderà la seguente forma:

![[Pasted image 20230505003324.png]]

La prima dinamica è disaccoppiata dalla seconda

Nella seconda equazione devo scegliere $\bar V_{qr}$ per regolare $I_{qr}$, ma questo è un passabasso del primo ordine

Ottenendo come funzione trasferimento:
$$
\begin{aligned}
\frac{I_{dr}}{V_{dr}} = \frac{I_{qr}}{V_{qr}} =\frac{1}{R_r+sL_r'} 
\end{aligned}
$$

Nella terza equazione notiamo che $I_{qr}$ influenza la $\tau_e$ della equazione meccanica, andando a modificare la $\omega_{slip}$. In questo caso si possono rifare le considerazioni sulla velocità angolare ($\tau_m$ ><= $\tau_e$), dove se la $\tau_m$ è troppo diverso da $\tau_e$ ci allontaniamo troppo dalla $\omega$ di sincronismo

Lo sforzo del convertitore è tanto grande quanto è grande la differenza tra $\omega$ e $\omega_s$

Quello che farà il mio controllore è stabilire l'ingresso che arriverà alla funzione di trasferimento:
![[Pasted image 20230504175746.png]]

---
# References

