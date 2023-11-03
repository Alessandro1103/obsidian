Date: 2023-11-03
Time: 23:00
Tags: #MatLab 
Up: [[MatLab]]

---
# MatLab

Per cercare indicazioni per funzioni di cui non conosciamo il funzionamento possiamo utilizzare **help** ... seguito dalla funzione oppure **doc** ... che ci riporta direttamente alla documentazione.


# Comandi di base

- **clc**: pulisce il prompt, cancellando le operazioni precedenti
- **clear all**: cancella tutte le informazioni in memoria
- **close all**: chiude tutte le finestre aperte

# Matrici

Per definire una matrice si utilizzano parentesi quadre, gli spazi per separare gli elementi in riga e ; per andare alla riga successiva.  A = [1 -5;2 1/4]
Se invece scriviamo:
- A(1,2) restituisce l'elemento sulla riga 1, colonna 2
- A(:,1) restituisce la prima colonna
- A(2,:) restituisce la seconda riga

L'inversa si calcola con "inv"
Il determinante con "det"
Il rango con "rank"
"size" restituisce il numero di righe e colonne
La trasposta con " ' " dopo la matrice (es. A')
Gli autovalori con "eig". Usandola [V,D]=eig(A) restituisce una matrice V con gli autovettori come colonne e una matrice diagonale D con gli autovalori
La matrice identità si ottiene con "eye"
La matrice di zero con "zeros"
La matrice di uno con "ones"
Una matrice di numeri casuali con "rand"

## Istruzioni logiche

La sintassi di un controllo di flusso si fa nel seguente modo:

``` matlab
if expression1
	statements
elseif expression2
	statements
else
	statements
end
```

# Vettori

- **min, max**: otteniamo minimo e massimo
- **sort**: ordinamento crescente/descrescente
- **length**: numero di elementi
Possiamo usare ":" per generare vettori riga: 
t = 1:5 ==> [1 2 3 4 5]
t = 0:0.5:2 ==> [0 0.5 1 1.5 2]

# Cicli

Esempi per:

- FOR: 
```matlab
for k=1:step:n
	statements
end
```

- WHILE
```matlab
while condition
	statements 
end
```

# Grafici

Per aprire una finestra si usa il comando **figure(n)** dove n è il numero della figura considerata. Se si vuole conservare l'output usiamo **hold on**. 

## Plot
Per creare figure 2D usiamo **plot**

![[Pasted image 20230420224637.png]]
Possiamo aggiungere altre impostazioni:
- xlabel(), ylabel()
- title
- legend
- axis

## SubPlot
Si possono generare anche più plot sulla stessa finestra

![[Pasted image 20230420230247.png]]

## Surf
Per creare figure 3D usiamo **surf**

# Equazione Differenziale

La simulazione si divide in alcuni passaggi
- Definizione di un intervallo di tempo e del vettore/matrice soluzione
- Assegnazione della dinamica, solitamente tramite una funzione da definire
- Scelta di un "solver": ode45, ode23, ode23s ...

Questo esempio risolve l'equazione:
$$x'(t)=sin(t)x(t)$$

```matlab
tspan=[0 10];
x0=1;
[t x]=ode45(@equazione,tspan,x0);

function dx=equazione(t,x)
dx=sin(t)*x;
end
```


![[Pasted image 20230420231315.png]]


# Sistema Lineare

In questo caso proviamo a risolvere il seguente sistema:
$$ x'(t)=Ax(t) $$ 
su un intervallo $[0,10]$ con condizione iniziale $x(0)=[4 -2]$
La matrice A è 
$$ A= \begin {vmatrix}-0.5 & 2\\ -2 & -0.5 \end{vmatrix} $$

```matlab
global A
A=[-0.5 2;-2 -0.5];
x0=[4 -2];
tspan=[0 10];
[t x]=ode45(@sistema, tspan, x0);

figure(1)
plot(x(:,1),x(:,2)) %Grafico della traiettoria (x1,x2)

figure(2)
subplot(2,1,1)
plot(t,x(:,1)) %Grafico del primo stato (t,x1)
subplot(2,1,2)
plot(t,x(:,2)) %Grafico del secondo stato (t,x2)

function dx=sistema(t,x)
global A
dx=A*x
end
```


Vediamo ora un sistema di controllo:
Dato un sistema vogliamo determiantre la matrice di controllabilità e stabilire se il sistema è controllabile, e in caso assegnare degli autovalori desiderati alla matrice a ciclo chiuso

```matlab
C=ctrb(A,B) %matrice di controllabilità
s=size(A); %s è il vettore delle dimensioni di A, s=[n n]
if rank(C)<s(1)
	error('Il sistema non è controllabile')
else
	q=-s(1):-1; %vettore di autovalori desiderati (-1, ... ,-n)
	K=acker(A,B,q);
	eig(A-B*K) %test
```

## Sistema a tempo discreto

Per simulare una dinamica a tempo discreto, si può utilizzare una tecnica ricordiva all'interno di un ciclo 'for'

```matlab
x(:,1)=x0;
for k=2:numero_passi
	x(:,k)=sistema(k-1,x(k-1));
```

## Discretizzazione

Supponiamo di avere un sistema a tempo continuo: $x'(t)=Ax(t)+Bu(t)$ e di volerlo discretizzare:
- con Eulero: $x((k+1)\Delta t)=(I+\Delta tA)x(k\Delta t)+\Delta tBu(k\Delta t)$
- quello corretto: $x((k+1)\Delta t)=e^{A\Delta t}x(k\Delta t)+(\int_{0}^{\Delta t}e^{As}Bds)u(k\Delta t)$

Scegliamo il tempo di campionamento **deltaT**
Definiamo lo stato discreto **x(:,k)**
Definiamo la dinamica discretizzata **sistema_discr(k,x)**

## Controllo quantizzato

Vogliamo simulare il comportamento di un sistema a tempo continuo, ma con un controllo che cambia a istanti di tempo discreti:

```matlab
n_passi=tfin/deltaT;
u=controllo(0,x0);
x=x0;
t=0;
for k=1:n_passi;
	tspan=[(k-1)*deltaT k*deltaT]; %sottointervallo di campionamento
	[s z]=ode45(@sistema_quantizzato,tspan,x0); %soluzione del sistema nel sottointervallo
	t=[t;s]; %composizione degli istanti di tempo del sottointervallo
	x=[x;z]; %composizione degli istanti di tempo del sottointervallo
	x0=z(end,:); %calcolo del nuovo valore iniziale per il prossimo sottointervallo
	u=controllo(k,x0); %calcolo del nuovo controllo per il prossimo sottointervallo
end
```

## Dominio di Laplace

- **tf(num, den)** = crea una funziona trasferimentoin ordine decrescente di grado
- **tfdata(H,'v')** = fornisce vettori contenenti il numeratore e il denominatore della funzione di trasferimento H
- **pole(H)** e **zero(H)** = poli e zeri
- **ss2tg(A,B,C,D)** = funzione trasferimento dalla matrice di stato
- **ssdata(H)** = rappresentazione di stato dalla matrice di trasferimento
- **bodeplot(H)** = diagramma di bode
- **nyquistplot(H)** = diagramma di nyquist
- **rlocus(H)** = luogo delle radici


---
# References
