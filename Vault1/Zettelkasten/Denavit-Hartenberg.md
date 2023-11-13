
Date: 2023-11-08
Time: 16:27
Tags: #Università #Robotics
Up: [[Robotics1]]

---
# Denavit-Hartenberg

I parametri del modello D-H sono i seguenti:
- $\alpha_i$ = l'angolo tra $z_i$ e $z_{i-1}$, ruotato attorno l'asse $x_{i}$ (positivo - regola mando destra con pollice verso di me - counter clockwise)
- $a_i$ = la distanza tra $z_i$ e $z_{i-1}$, lungo l'asse $x_{i-1}$ (positivo se ci spostiamo nella stessa direzione di $x_i$)
- $d_i$ = la distanza tra $x_i$ e $x_{i-1}$, lungo l'asse $z_{i-1}$ (positivo se ci spostiamo nella stessa direzione di $z_{i-1}$)
- $\theta_i$ = l'angolo tra $x_i$ e $x_{i-1}$, ruotato attorno l'asse $z_{i-1}$ (positivo - regola mando destra con pollice verso di me - counter clockwise)

La matrice totale che si forma è la seguente:
![[Pasted image 20231109112559.png]]


Condizioni:
La matrice di rotazione R(3,3) deve avere il determinante = $\pm 1$

1. Per prima cosa si disegnano gli assi sui joint, avendo così l'asse $z_i$.
2. Se dovesse essere presente un gripper, allora $z_e$ sarà lungo il punto di gancio.
3. Vedendo la rotazione di $\theta$ (come con la regola della mano destra della corrente lungo il filo e il campo magnetico) troviamo il verso di $z_i$
4. Si vede l'intersezione fra i vari assi, per costruire i riferimenti (sempre $z_i$). Se l'intersezione non c'é, allora ci si muove lungo la normale.
5. Per disegnare $x_i$ serve verificare l'intersezione tra $z_i$ e $z_{i-1}$, se presente $x_i$ allora $x_i$ sarà normale al piano disegnato dai due assi; il verso è una convenzione, normalmente si sceglie concorde con l'asse precedente. Se $z_i$ e $z_{i-1}$ sono due joint R collegati tramite un link, $x_i$ seguirà l'asse.
6. Per trovare la distanza $d_i$ la prima cosa da fare è verificare che esista una normale comune a $z_{i-1}$ e $z_i$. Se questa non esiste probabilmente, bisogna trasporre $z_{i-1}$ di una distanza $d_i$.

Nel creare la tabella si segue un ordine specifico:
1. Si vede $\theta_i$
2. Si verifica $\alpha_i$

---
# References
