Date: 2023-08-03 
Time: 01:44
Tags: #Tesi #Università #Appunti 
Up: [[Tesi]]

---
# Seconda riunione

## Approfondimento turbina eolica

Come funziona una turbina eolica?
Abbiamo una turbina con 3 pale, collegata ad un albero, un gear box (moltiplicatore di giri), un ulteriore albero collegato a un rotore, immaginiamolo come un rotore a corrente continua, che gira attorno a uno statore collegato alla rete.

![[Pasted image 20230427171456.png]]

Il fluido arriva alle pale, che viene convertita in energia meccanica rotazionale, e come ultima una conversione in energia elettrica.

### Aspetto meccanico

La potenza del flusso d'aria che colpisce la turbina è esprimibile con la seguente formula (energia per unità di tempo):
$$P_v=\frac{1}{2}\rho AV^3$$
$A$ è l'area spazzata dalla turbina
$\rho$ è la densità dell'aria
$V$ è la velocità del flusso d'aria

![[Pasted image 20230427171831.png]]

Il flusso d'aria è descritto dal tubo (tubo di flusso), che impatta sulla turbina, le cui pale ruotando vanno a spazzare un'area esprimibile con la formula: $\pi R^2$ 

Non tutta questa energia si trasforma in energia meccanica rotazionale.
Infatti come si vede dalla formula la porzione convertibile è definita tramite $C_p$, anche detto coefficiente di potenza (compreso tra 0 e 1):
$$P_r=C_p(\lambda,\beta)\cdot P_v = \frac{1}{2}\rho\pi R^2\cdot C_p(\lambda,\beta)\cdot V^3$$
- $\beta$ è l'angolo che la pala offre al vento (pitch angle), l'asse longitudinale della pala, è l'angolo di rotazione rispetto a tale asse. 

![[Pasted image 20230428032435.png]]

La pala è come un ala, variando l'angolo, la potenza trasferita sulla pala cambia. Immaginiamo che questo angolo sia costante, e che sia quello più ottimale possibile, ovvero quella situazione in cui la conversione di energia meccanica è massima.


- $\lambda$ tip speed ratio: $\lambda=\frac{\Omega_r \cdot  R}{V}$

$\Omega_r$ è la velocità angolare (tangenziale, ovvero della punta della pala) di rotazione di tutta la turbina
$R$ è la lunghezza della pala
$V$ è la velocità del vento stesso

Moltiplicando $\Omega_r$ (tempo$^{-1}$) per $R$ (lunghezza) otteniamo una velocità.

La cosa è di interesse perché si vede sperimentalmente, che questo coefficiente $C_p(\lambda,\beta)$ ha una forma di questo tipo:

![[Pasted image 20230427172859.png]]
Ovvero una curva, che dato un $\lambda$ particolare $C_p$ è massimo, vuol dire che per ogni valore della velocità del vento $V$, esiste un valore ottimo di $\Omega_r$ in corrispondenza del quale $C_p$ è massimo e quindi si ha la massima estrazione di potenza dal flusso d'aria.

Teoricamente/idealmente è possibile estrarre il 59% (limite di Betz) del flusso d'aria, più realisticamente è 35-40%.

Potrei fare un controllo della turbina in maniera tale per far si che $\Omega_r$ insegua un valore di riferimento che dipende dalla velocità del vento. Questa cosa nella pratica ha un limite, perché il vento V è un segnale nel tempo che può variare molto velocemente. Dovrei fare un anello di controllo, tale che il riferimento di $\Omega_r$  vari con la stessa velocità con cui varia $V$, cioè il mio obiettivo deve avere la stessa frequenza di cambiamento del vento. Ma questa è una cosa molto difficile, poiché la turbina è un oggetto altamente massivo, ha quindi costanti di tempo meccaniche di circa secondi (molto lente rispetto alla possibile variazione del vento).

A sinistra abbiamo la potenza estratta da vento, in basso abbiamo la velocità di $\Omega$
![[Pasted image 20230427173908.png]]
Si vede l'andamento della potenza rispetto alla velocità $\Omega_r$ per diversi valori della velocità del vento, esiste un valore di $\Omega_r$ dove tali curve sono massime.

### Aspetto elettrico

#### Squirrel Cage Induction Machine

[Video spiegazione e animazione](https://www.youtube.com/watch?v=AQqyGNOP_3o&ab_channel=Lesics)

Sul rotore sono presenti 3 avvolgimenti indipendenti, distanziati di 120°, senza generatore/non alimentati

![[Pasted image 20230427174934.png]]

Questo oggetto (quello in alto) gira intorno a uno statore, che anche lui a sua volta contiene 3 avvolgimenti da cui escono 3 coppie di poli/fili

![[Pasted image 20230427175053.png]]

Cosa accade se connetto lo statore alla rete? Nasceranno 3 correnti.
$$ 
\begin{aligned}
	& I_a=I_0 \cdot cos(\omega_s t) \\
	& I_b=I_0 \cdot cos(\omega_s t + \frac{2}{3}\pi) \\
	& I_c=I_0 \cdot cos(\omega_s t + \frac{4}{3}\pi)
\end{aligned}
$$
cioè una terna trifase simmetrica di correnti, supponendo che la rete sia bilanciata 

Guardando lo statore dall'alto, vedo 3 fili, percorsi da una corrente con lo stesso modulo ma con sfasamento di 120°

Avendo una spira percorsa da corrente questa genera un campo magnetico
Questa è la rappresentazione di una corrente costante.

![[Pasted image 20230427175752.png]]

Avendo invece una corrente sinusoidale, la direzione rimane la stessa, il verso si alterna ogni mezzo giro, il modulo varia con l'onda sinusoidale.


![[Pasted image 20230427175955.png]]
Se sommo i 3 contributi ottengo la stessa cosa che ottengo nello spazio di stato, quando vado a guardare la traiettoria di un oscillatore armonico semplice.
$$
	\begin{aligned}
	& x_1=x(t)=x_0 \cdot sen(\omega t) \\
	& x_2=\dot x(t)=x_0 \cdot \omega  \cdot sen(\omega t) \\
	\end{aligned}
$$

Otteniamo una ellisse
Otteniamo un campo magnetico B, che ruota con velocità agolare $\omega_s$

![[Pasted image 20230427180620.png]]

Come si può ottenere questo risultato? Prendo le correnti di prima, le elevo al quadrato e le sommo tra loro, ottengo quindi (circa):

$$
\begin{aligned}
	I_a^2+I_b^2+I_c^2=I_0^2
\end{aligned}
$$
rimane una circonferenza in un spazio di dimensione $R^3$

Guardiamo ora il rotore, concentrandoci solo su una spira :
![[Pasted image 20230427181233.png]]

$\omega_r$ (credo che si intenda $\Omega_r$ di prima), che rappresenta la velocità del rotore, ovvero la velocità generata, non ha alcun tipo di correlazione con $\omega_s$

Se ci dovessimo piazzare sul rotore, a che velocità vedremmo ruotare il campo $B$? 
$$\omega_{slip}=\omega_s-\omega_r$$

Slip significa scorrimento -> il campo di induzione B ruota nel sistema di riferimento del rotore ad una velocità di scorrimento $\omega_{slip}$
 
Richiamiamo la legge di Faraday-Neumann-Lenz sull'induzione magnetica
Il flusso concatenato sulla spira varia nel tempo? No, perché il campo di induzione magnetica è costante (rispetto al rotore). Siccome non c'è variazione di flusso, non c'è neanche corrente indotta.

Immaginiamo ora che $\omega_s>\omega_r$, questo vuol dire che $B$ ruota con una $\omega_{slip}$ positiva, cioè in senso antiorario, c'é corrente indotta? Si perché il flusso non è costante, la corrente indotta ha inoltre forma sinusoidale, e con pulsazione $\omega_{slip}$

==Macchina asincrona: il rotore può ruotare a una velocità angolare diversa rispetto alla pulsazione dei segnali elettrici dello statore==

La corrente che percorre il lato destro della spira, è entrante o uscente? 
Ricordiamo anche la legge di Lagrange, per il campo ovvero:

$$
\begin{aligned}
	\oint_S(\vec B) = \int_S \vec B \cdot \hat n \; dS
\end{aligned}
$$

$\hat n$ è il versore ortogonale alla spira
Quando faccio $\vec B \cdot \hat n$ sono sempre sulla normale alla spira, mentre il vettore gira, il flusso diminuisce, Faraday ci dice che la corrente indotta deve essere opposta a quella che l'ha generata, quindi deve andare a diminuire $B$ e per farlo la corrente deve essere entrante a destra.


Applicando la seconda Legge di Laplace per i campi applicati alle correnti, generanti delle forze:

$$
\begin{aligned}
	d \vec F = Id \vec l \times \vec B
\end{aligned}
$$

![[Pasted image 20230428053632.png]]



![[Pasted image 20230427183026.png]]

La $\omega$ è la $\omega_r$ usata prima
Il primo caso è detto sub-sincrono perche $\omega_s<\omega_r$ 
Il secondo caso è detto sopra-sincrono perche $\omega_s>\omega_r$ 

Dal punto di vista energetico, il primo caso, il rotore viene sostenuto nel moto, la macchina sta prelevando energia della rete; il secondo caso, il rotore viene frenato, fornendo l'energia generata. Questo genere di macchina quindi funziona sia come generatore che come motore.

### Doubly Fed Induction Machine

Possiamo alterare il comportamento di questo oggetto per farlo funzionare sempre come un generatore anche in condizioni di sub-sincronismo?
Ma dove sta scritto che gli avvolgimenti del rotore devono essere cortocircuitati?
Se io applico una tensione di controllo sull'avvolgimento di rotore, prima su di essi vi era solo corrente indotta, ora abbiamo una somma fra le due. Se la corrente di controllo è in grado di invertire il segno complessivo della corrente che si trova sull'avvolgimento (cioè invertire puntino e croce) ne caso della macchina-motore, allora ricadiamo nel caso della macchina-generatore.

Come faccio a introdurre questo controllo?
Tramite un doppio convertitore, un sistema con inverter:

![[Pasted image 20230428152148.png]]

Prendo 3 fili che prelevano le 3 tensioni, la mando in un convertitore che produce corrente continua, il secondo inverter darà una tensione con frequenza pari alla frequenza di slip, che andrò ad applicare al rotore.
Questi 3 avvolgimenti sono uguali tra loro, percorsi dalla stessa corrente ma sfasata di 120°, e quindi alimentati dalla stessa tensione sfasata di 120°, le tensioni di controllo non sono 3 tensioni indipendenti; poiché, quanti sono i gradi di libertà sono associati a una terna trifase simmetrica? Cioè quante grandezze posso modificare mantenendo la proprietà di simmetricità? 2, modulo e fase

Quello che voglio fare è un cambio di variabili, tramite una matrice di trasformazioni (Park Transformation)

$$
	\begin{aligned}
	T(\alpha) = 
	\begin{bmatrix}
		\hat e_d^t \\
		\hat e_q^t \\
		\hat e_0^t
	\end{bmatrix}
	= \frac{2}{3}
	\begin{bmatrix}
		cos(\alpha) & cos(\alpha - \frac{2\pi}{3}) & cos(\alpha + \frac{2\pi}{3})) \\
		-sin(\alpha) & -sin(\alpha - \frac{2\pi}{3}) & -sin(\alpha + \frac{2\pi}{3})) \\
		\frac{1}{2} & \frac{1}{2} & \frac{1}{2} \\
	\end{bmatrix}
	
	\end{aligned}
$$
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
$X_d$ componente diretta
$X_q$ componente quadratura 
$X_0$ componente omopolare

Queste variabili non hanno un riscontro fisico, sono variabili che vivono in un dominio fittizio, ma in questo sistema di coordinate sarà più semplice costruire il modello del processo da controllare.
Arriveremo a scrivere la rappresentazione con lo spazio di stato della turbina:

![[Pasted image 20230428161820.png]]
Le prime due sono puramente elettriche, una equazione meccanica, che sopravviverà nel nostro modello

![[Pasted image 20230428161925.png]]
2 uscite, potenza attiva e potenza reattiva

---
# References