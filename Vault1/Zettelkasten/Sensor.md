Date: 2023-11-09
Time: 12:53
Tags: #Università #Robotics 
Up: [[Robotics1]]

---
# Sensor

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
La risoluzione si trasmette come con i gear:
$$
Risoluzione(motore) = n \cdot Risoluzione(carico)
$$


---
# References
