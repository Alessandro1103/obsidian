Date: 2023-11-08
Time: 11:28
Tags: #Università #Robotics 
Up: [[Robotics1]]

---
# Transmission

## Gear
Il gear reduction è in generale calcolato come:
$$
\frac{Driven}{Driver} = Gear Ratio
$$
In un problema ti possono essere dati 2 valori per ciascun gear, il numero di denti o il raggio dell gear. Di base le formule da seguire sono le seguenti:
$$
\frac{N_1}{N_2} = \frac{r_2}{r_1}
$$
dove N sono il numero di denti e r il raggio.
Quando ci si trova davanti a una serie di gear, uno collegato all'altro, basta moltiplicare il numero di denti per capire la proporzione che si ottiene alla fine.
$$
\theta_m = \theta \cdot N
$$
dove N rappresenta la proporzione dei denti dei vari gear.

## Coppia
La formula dipende dalla direzione che stiamo vedendo:
$$
\tau_m = J_m\ddot{\theta}_m + \frac{1}{n}\Big(J_l\ddot{\theta}_l\Big)
$$
$$
\tau_l = J_l\ddot{\theta}_l + n\Big(J_m\ddot{\theta}_m\Big)
$$
dove "m" è per il motore, "l" per load (carico)
Altra formula molto utile è:
$$
n = \sqrt{\frac{J_u}{J_m}}
$$

---
# References
