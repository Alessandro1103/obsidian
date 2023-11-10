Date: 2023-11-08
Time: 16:27
Tags: #Università #Robotics
Up: [[Robotics1]]

---
# Denavit-Hartenberg

I parametri del modello D-H sono i seguenti:
- $\alpha_i$ = l'angolo tra $z_i$ e $z_{i-1}$, il verso di rotazione è rivolto verso l'asse $x_i$
- $\theta_i$ = l'angolo tra $x_i$ e $x_{i-1}$, il verso di rotazione è rivolto verso l'asse $z_i$ 
- $d_i$ = l'offset (distanza) fra gli assi $z_i$ e $z_{i-1}$
- $a_i$ = la lunghezza del braccio

La matrice totale che si forma è la seguente:
![[Pasted image 20231109112559.png]]


Condizioni:
La matrice di rotazione R(3,3) deve avere il determinante = $\pm 1$

- Per trovare la distanza $d_i$ la prima cosa da fare è verificare che esista una normale comune a $z_{i-1}$ e $z_i$. Se questa non esiste probabilmente, bisogna trasporre $z_{i-1}$ di una distanza $d_i$.

Quando si svolge un esercizio i passi per il completamento sono i seguenti:
1. Trovare gli assi di rotazione e applicarci z
2. Verificare la direzione di z, verificando le rotazioni rispetto al sistema precedente
3. Piazzare x in modo che soddisfi gli angoli nella tabella


---
# References
