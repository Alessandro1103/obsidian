**Parametri (Inputs):**

- `t`: Il tempo corrente.
- `N`: Numero di passi nell'orizzonte di predizione.
- `T`: Intervallo temporale tra i passi (periodo di campionamento).
- `q1`, `q2`, `r`, `r1`, `s1`, `s2`, `c`: Pesi e costanti utilizzate nella funzione di costo per penalizzare le deviazioni delle variabili di stato e le azioni di controllo.
- `M`: Fattore di conversione tra energia e potenza.
- `p_min_grid`, `p_max_grid`: Limiti di potenza per la rete elettrica.
- `u_min_ess`, `u_max_ess`: Limiti di potenza per il sistema di storage dell'energia (ESS, Energy Storage System).
- `u_min_ev`, `u_hat_ev`: Limiti di potenza elettrica e potenza massima per il veicolo elettrico (EV, Electric Vehicle).
- `u_min_res`, `u_max_res`: Limiti di potenza per la risorsa (es. pannelli solari, turbine eoliche, resource, ecc.).
- `w_res`: Potenza meccanica sulla turbina
- `x1_min`, `x1_max`, `x2_min`, `x2_max`: Limiti delle variabili di stato `x1` e `x2`.
- `x1_0`, `x2_0`: Condizioni iniziali delle variabili di stato `x1` e `x2`.
- `x1_ref`, `x2_ref`: Valori di riferimento desiderati per le variabili di stato `x1` e `x2`.
- `p_grid_history`, `u_res_history`, `u_ess_history`, `u_ev_history`, `x1_history`, `x2_history`: Vettori che contengono la storia delle azioni di controllo, variabili di stato e altre grandezze utili.

**Variabili (Variables):**

- `p_grid`: Potenza fornita o prelevata dalla rete elettrica (azione di controllo).
- `u_res`, `u_ess`, `u_ev`: Potenza erogata dalla risorsa, dal sistema di storage dell'energia (ESS) e dal veicolo elettrico (EV) (azioni di controllo).
- `x1`, `x2`: Variabili di stato del sistema elettrico.

**Descrizione della Funzione:** La funzione `mpc_iteration!` risolve un problema di ottimizzazione che cerca di minimizzare una funzione di costo, tenendo conto delle equazioni di dinamica del sistema e dei limiti delle variabili di stato e delle azioni di controllo. L'ottimizzazione viene eseguita utilizzando il pacchetto JuMP con il solver Gurobi.

La funzione è progettata per essere chiamata iterativamente ad ogni istante di tempo `t` per adattare il controllo in base alle nuove misurazioni e predizioni. Dopo l'ottimizzazione, i risultati vengono memorizzati nelle variabili `p_grid_history`, `u_res_history`, `u_ess_history`, `u_ev_history`, `x1_history` e `x2_history` per essere utilizzati nelle chiamate successive della funzione.

L'obiettivo principale dell'algoritmo MPC è regolare le azioni di controllo per mantenere le variabili di stato vicino ai valori di riferimento e minimizzare il costo associato a tali azioni. Questo tipo di controllo predittivo è particolarmente utile quando è necessario gestire un sistema soggetto a vincoli e dinamiche complesse, come un sistema energetico o un sistema di produzione soggetto a fluttuazioni delle risorse rinnovabili.