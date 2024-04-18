Date: 2024-04-18
Time: 12:24
Tags:
Up: 

---
# Calibration

Nel seguente esame: [MidTerm2020](https://www.diag.uniroma1.it/deluca/rob2_en/WrittenExamsRob2/Robotics2_Remote_Midterm_Test_2019-20_20.04.15.pdf), nel calcolare la derivata di $f$ rispetto a un parametro ($\alpha$) della DH table, viene utilizzata l'espansione di Taylor. Normalmente sarebbe stato sufficiente calcolare la derivata. Questo è dovuto al fatto che avendo il valore nominale, vogliamo sapere la variazione rispetto a quel particolare valore. Se avessi calcolato unicamente la derivata avrei ottenuto la sensibilità, non l'errore rispetto al valore nominale. Normalmente nei 2R non è necessario utilizzare Taylor per la semplicità del problema stesso. Si usa Taylor quando il robot è molto complesso, molto non-lineare.


${}^{i}{\omega}_i = {}^{i-1}R_i(q_i) \left( {}^{i-1}{\omega}_{i-1} + (1 - \sigma_i)\dot q_i \ {}^{i-1}{z}_{i-1} \right)$
${}^{i}{v}_i = {}^{i-1}R_i(q_i) \left( {}^{i-1}{v}_{i-1} + \sigma_i \dot q_i {}^{i-1}{z}_{i-1} + {}^{i-1}\dot{\omega}_i \times {}^{i-1}r_{i-1,i}\right)$
$v_{ci} = v_i + \omega_i \times r_{ci}$

---
# References
