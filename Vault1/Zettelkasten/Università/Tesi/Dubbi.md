Potrei inserire un elemento per rendere più smooth i p_grid
È sbagliato mettere subito richieste alte? Quei passi non sono ottimizzati dall'MPC. 
Posso aumentare r
Dovrei inserire p_grid_pv etc nella funzione obiettivo?

potrei aver sbagliato il modello:

``` julia
@constraint(mdl, [i = t:t+N-1], p_grid_pv[i] == u_ess[i] + u_ev_pv[i] - w_res_pv[i])
@constraint(mdl, [i = t:t+N-1], p_grid_rete[i] == p_grid_rete_to_wt[i] + p_grid_rete_to_pv[i])
@constraint(mdl, [i = t:t+N-1], p_grid_pv[i] == p_grid_rete_to_pv[i] + p_grid_wt_to_pv[i] - p_grid_pv_to_wt[i])
```

mi fa strano che `p_grid_pv` sia il risultato sia dei valori di ingresso e di uscita, ma anche il risultato delle produzioni e consumi