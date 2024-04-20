Date: 2024-04-19
Time: 23:14
Tags: #Robotics 
Up: [[Robotics2]]

---
# Robotics2 appunti

Ricordarsi che $r_{ci}$ è scrivibile come: $r_{ci} = {}^0A_i \ \begin{pmatrix} {}^ir_{ci}\\ 1 \end{pmatrix}$, cioè pensare a muovere i link tramite **coordinate omogenee** questo può tornare utile per tutte le dimensioni con centro di massa. Citato nel [Esame 2023](https://www.diag.uniroma1.it/deluca/rob2_en/WrittenExamsRob2/Robotics2_Midterm_Test_2022-23_23.04.19.pdf) esercizio 2.

Nel calcolo dei **centri di massa** si considera la distanza dal link i al link i-1. Citato nel [Esame 2023](https://www.diag.uniroma1.it/deluca/rob2_en/WrittenExamsRob2/Robotics2_Midterm_Test_2022-23_23.04.19.pdf) esercizio 4.

Per estrarre i valori $a$ dalla matrice $g(q)$ per la linearizzazione, basti raccogliere i valori dipendenti da un singolo $q$. Citato nell'esame [Esame 2021](https://www.diag.uniroma1.it/deluca/rob2_en/WrittenExamsRob2/Robotics2_Remote_Midterm_Test_2020-21_21.04.14.pdf). 

Ricordarsi che se devo verificare che una task sia fattibile devo eseguire il Range della matrice dei task ovvero J. Citato nell'esame [Esame 2020](https://www.diag.uniroma1.it/deluca/rob2_en/WrittenExamsRob2/Robotics2_Remote_Midterm_Test_2019-20_20.04.15.pdf)

Nel seguente esame: [Esame 2020](https://www.diag.uniroma1.it/deluca/rob2_en/WrittenExamsRob2/Robotics2_Remote_Midterm_Test_2019-20_20.04.15.pdf), nel calcolare la derivata di $f$ rispetto a un parametro ($\alpha$) della DH table, viene utilizzata l'espansione di Taylor. Normalmente sarebbe stato sufficiente calcolare la derivata. Questo è dovuto al fatto che avendo il valore nominale, vogliamo sapere la variazione rispetto a quel particolare valore. Se avessi calcolato unicamente la derivata avrei ottenuto la sensibilità, non l'errore rispetto al valore nominale. Normalmente nei 2R non è necessario utilizzare Taylor per la semplicità del problema stesso. Si usa Taylor quando il robot è molto complesso, molto non-lineare.

## Formule

Accelerazione: 
$$
\begin{cases} 
	\ddot{q} = J^{\#} (\ddot{p}_d - \dot{J}(q) \dot{q}) \\ 
	\ddot{p} = J(q)\ddot{q} + \dot{J}(q) \dot{q}
\end{cases}
$$


---
# References
