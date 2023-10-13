Date: 2023-08-03 
Time: 01:20
Tags: #codice 

---
# mpc_thesis

1. Il codice definisce una funzione `mpc_iteration!` che esegue un'iterazione dell'algoritmo MPC al tempo `t`. La funzione prende in input numerosi parametri e variabili e aggiorna le matrici di cronologia con i risultati dell'ottimizzazione.
2. Vengono utilizzati i pacchetti `JuMP` e `Gurobi` per la modellazione matematica e l'ottimizzazione. `JuMP` è un linguaggio di modellazione e `Gurobi` è un risolutore.
3. Il codice definisce variabili decisionali (`@variable`) per i flussi di potenza dalla rete (`p_grid`), la potenza da una turbina (`u_res`), la potenza da un sistema di stoccaggio energetico (`u_ess`), e la potenza assorbita da una macchina (`u_ev`). Inoltre, ci sono variabili di stato (`x1` e `x2`) che rappresentano lo stato del sistema.
4. Il codice definisce vincoli (`@constraint`) che impongono le dinamiche del sistema, il bilanciamento della potenza, i vincoli di potenza e i vincoli di stato nell'orizzonte temporale.
5. Il codice definisce la funzione obiettivo (`@objective`), che rappresenta il costo da minimizzare. L'obiettivo include termini che penalizzano le deviazioni dagli stati desiderati (`x1_ref` e `x2_ref`), le deviazioni di potenza dai valori desiderati (`u_hat_ev`), e l'uso della rete elettrica.
6. Viene chiamata la funzione `optimize!` per risolvere il problema di ottimizzazione e trovare le azioni di controllo ottimali nell'orizzonte temporale.
7. I risultati dell'ottimizzazione vengono quindi memorizzati nelle rispettive matrici di cronologia per essere utilizzati nella successiva iterazione dell'algoritmo MPC

``` jl
using JuMP
using Gurobi

#funzione per l'mpc, con parametri e variabili
function mpc_iteration!(t::Int64, N::Int64, T::Float64, q1::Float64, q2::Float64, r::Float64, r1::Float64, s1::Float64, s2::Float64, c::Float64, M::Float64, p_min_grid::Float64, p_max_grid::Vector{Float64}, u_min_ess::Vector{Float64}, u_max_ess::Vector{Float64}, u_min_ev::Float64, u_hat_ev::Vector{Float64}, u_min_res::Float64, u_max_res::Vector{Float64}, w_res::Vector{Float64}, x1_min::Vector{Float64}, x1_max::Vector{Float64}, x1_0::Float64, x1_ref::Float64, x2_min::Vector{Float64}, x2_max::Vector{Float64}, x2_0::Float64, x2_ref::Float64, p_grid_history::Vector{Float64}, u_res_history::Vector{Float64}, u_ess_history::Vector{Float64}, u_ev_history::Vector{Float64}, x1_history::Vector{Float64}, x2_history::Vector{Float64})

mdl = Model(Gurobi.Optimizer)
if t == 1
	@variable(mdl, p_grid[t:t+N-1]) #potenza fornita/prelevata dalla rete elettrica
else
	@variable(mdl, p_grid[t-1:t+N-1]) #potenza fornita o prelevata dalla rete elettrica
	@constraint(mdl, p_grid[t-1]==p_grid_history[t-1]) #garantisce la continuità
end

@variable(mdl, u_res[t:t+N-1]) #potenza fornita dalla turbina
@variable(mdl, u_ess[t:t+N-1]) #potenza fornita/assorbita dallo storage
@variable(mdl, u_ev[t:t+N-1]) #potenza assorbita dalla macchina
@variable(mdl, x1[t:t+N]) #variabile di stato 1
@variable(mdl, x2[t:t+N]) #variabile di stato 2

@constraint(mdl, [i=t:t+N-1], x1[i+1]==x1[i]+T*(u_ess[i])) #aggiornamento x1
@constraint(mdl, [i=t:t+N-1], x2[i+1]==x2[i]+((3600*T)/M)*(w_res[i]-u_res[i])) #aggiornamento x2
@constraint(mdl, [i=t:t+N-1], p_grid[i]==u_ess[i]+u_ev[i]-u_res[i]) #equazione bilanciamento rete
@constraint(mdl, [i=t:t+N-1], u_min_ev<=u_ev[i]<=u_hat_ev[i]) #vincolo potenza EV
@constraint(mdl, [i=t:t+N-1], u_min_ess[i]<=u_ess[i]<=u_max_ess[i]) #vincolo potenza ESS
@constraint(mdl, [i=t:t+N-1], u_min_res<=u_res[i]<=u_max_res[i]) #vincolo potenza turbina
@constraint(mdl, [i=t:t+N], x1_min[i]<=x1[i]<=x1_max[i]) #vincolo x1
@constraint(mdl, [i=t:t+N], x2_min[i]<=x2[i]<=x2_max[i]) #vincolo x2
@constraint(mdl, [i=t:t+N-1], p_min_grid<=p_grid[i]<=p_max_grid[i])  #vincolo potenza rete
@constraint(mdl, x1[t]==x1_0) #condizione iniziale x1
@constraint(mdl, x2[t]==x2_0) #condizione iniziale x2

#funzione obiettivo
if(t==1)
	@objective(mdl, Min, s1*(x1[t+N]-x1_ref)^2+s2*(x2[t+N]-x2_ref)^2+sum((q1*(x1[i]-x1_ref)^2+q2*(x2[i]-x2_ref)^2+r*(p_grid[i])^2+c*(u_ev[i]-u_hat_ev[i])^2) for i=t:t+N-1))
else
	@objective(mdl, Min, s1*(x1[t+N]-x1_ref)^2+s2*(x2[t+N]-x2_ref)^2+sum((q1*(x1[i]-x1_ref)^2+q2*(x2[i]-x2_ref)^2+r*(p_grid[i])^2+r1*(p_grid[i]-p_grid[i-1])^2+c*(u_ev[i]-u_hat_ev[i])^2) for i=t:t+N-1))
end

optimize!(mdl) #risoluzione del problema di ottimizzazione

#memorizza i risultati nelle corrispondenti matrici di dati storici
for i=t:t+N-1
	p_grid_history[i]=value(p_grid[i])
	u_res_history[i]=value(u_res[i])
	u_ess_history[i]=value(u_ess[i])
	u_ev_history[i]=value(u_ev[i])
	x1_history[i]=value(x1[i])
	x2_history[i]=value(x2[i])  
end

x1_history[t+N]=value(x1[t+N])
x2_history[t+N]=value(x2[t+N])
end
```

---
# References


