Date: 2023-11-08
Time: 11:28
Tags:
Up: 

---
# Robotics1

## Gear
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

## Risoluzione Encoder
La formula per la risoluzione degli Encoder è sempre la stessa:
$$
\Delta_{gradi} = \frac{360}{2^N}
$$
Oppure, se si cerca in radianti:
$$
\Delta_{rad} = \frac{2\pi}{2^N}
$$
Se ci si trova in "quadratura" significa che dividiamo l'encoder in 4 (90° ciascuno), cosi si deve modificare la formula in:
$$
\Delta_{gradi} = \frac{360}{4 \cdot 2^N}
$$
Idem per i radianti.
Il numero di "pulse", sono esattamente $2^N$.
Vengono fornite due risoluzioni, o lineari o angolari, per passare da lineari ad angolari bisogna:
$$
Risoluzione(radianti) = \frac{Risoluzione(lineare)}{Raggio}
$$


---
# References
