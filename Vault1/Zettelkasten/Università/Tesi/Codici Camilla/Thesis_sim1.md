Date: 2023-08-05
Time: 15:23
Tags: #codice 

---
# Thesis_sim1

``` jl
# Carica dei pacchetti necessari
include("mpc_thesis.jl")
using Plots
using SpecialFunctions
using LaTeXStrings

# Impostazioni predefinite per i grafici
plot_font = "Computer Modern"
default(
    fontfamily=plot_font,
    linewidth=2,
    framestyle=:box,
    label=nothing,
    grid=true
)
scalefontsizes(1.5)

# Definizione di una funzione per generare una campana di Gauss
function gaussian_bell(n, μ, o)
    x = LinRange(-15o, 15o, n)
    y = (1125.0*(exp.(-0.5*((x.-μ)/o).^2)/(o*sqrt(2π)))).+50.0
    return y
end

# Definizione dei parametri del sistema
μ = -0.05  # Media
o = 1.0    # Deviazione standard

durata_simulazione = 324   # 288 passi

t_i = 1
t_f = 20

# Finestra temporale per MPC
N = 36

# Tempo di campionamento
T = 5.0/60  # 5 minuti/60->ore

# Pesi per MPC
q1 = 5.0
q2 = 1.5   # rad al secondo scendono più rapidamente dei kilowatt
r = 15.0
r1 = 8.0
s1 = 6.0
s2 = 5.5
c = 25.0

# Quali sono i valori dei singoli termini, u-u_ev vicini quindi numero piccolo, x2 vicino a x2_ref ma siamo disposti a sacrificarne i numeri
# I pesi devono controbilanciare i diversi pesi tra loro.
# Con c molto grande e q2 molto piccolo, u_ev vicino ma omega lontano

# Definizione e inizializzazione delle variabili del sistema
temp = zeros(durata_simulazione)
M = 3000.0  # Momento angolare della turbina (kg*m^2/s grandi variazioni di potenza poca di velocità)
w_s = 2*pi*50  # Velocità di sincronismo

# Limiti della potenza di allaccio alla rete elettrica
p_min_grid = 0.0
p_max_grid = zeros(Float64, durata_simulazione)
for i = 1:durata_simulazione
    p_max_grid[i] = 400.0
end

# Limiti della potenza del sistema di storage dell'energia (ESS)
u_min_ess = zeros(Float64, durata_simulazione)
u_max_ess = zeros(Float64, durata_simulazione)
for i = 1:durata_simulazione
    u_min_ess[i] = -200.0
    u_max_ess[i] = 200.0
end

# Potenza richiesta dal veicolo elettrico (EV)
u_min_ev = 0.0
u_hat_ev = zeros(Float64, durata_simulazione)
bell = gaussian_bell(288, μ, o)
for k = 1:288
    u_hat_ev[k] = bell[k]
end
for k = 289:durata_simulazione
    u_hat_ev[k] = u_hat_ev[k-1]
end

# Limiti della potenza immessa in rete dalla risorsa (es. pannelli solari, turbine eoliche, ecc.)
u_min_res = 0.0
u_max_res = zeros(Float64, durata_simulazione)
for i = 1:durata_simulazione
    u_max_res[i] = 200.0
end

# Serie storica di produzione di potenza dalla risorsa
w_res = zeros(Float64, durata_simulazione)
ro = 1.225
radius = 6
g = 106.32

# Vento sulla turbina
v_wind = zeros(Float64, durata_simulazione)
for k = 1:durata_simulazione
    v_wind[k] = 11.0
end

lambda = zeros(Float64, durata_simulazione)
C_p = zeros(Float64, durata_simulazione)
Pmech = zeros(Float64, durata_simulazione)
for k = 1:durata_simulazione
    lambda[k] = w_s * radius / (g * v_wind[k])
    C_p[k] = 0.73 * ((151 / lambda[k]) - 13.2) * exp(-18.4 / lambda[k])
    Pmech[k] = 0.5 * ro * (radius^2) * pi * ((v_wind[k])^3) * C_p[k]
end

# Energia meccanica prodotta
w_res = zeros(Float64, durata_simulazione)
for i = 1:durata_simulazione
    w_res[i] = Pmech[i]
end

# Limiti dello stato di carica dell'energia
x1_min = zeros(Float64, durata_simulazione + 1)
x1_max = zeros(Float64, durata_simulazione + 1)
for i = 1:durata_simulazione + 1
    x1_min[i] = 0.0
    x1_max[i] = 300.0
end
x1_0 = 170.0
x1_ref = 170.0

# Limiti della velocità angolare della turbina
x2_min = zeros(Float64, durata_simulazione + 1)
x2_max = zeros(Float64, durata_simulazione + 1)
for i = 1:durata_simulazione + 1
    x2_min[i] = w_s * (1 - 0.3)
    x2_max[i] = w_s * (1 + 0.3)
end
x2_0 = w_s
x2_ref = w_s

# Definizione e inizializzazione delle variabili storiche
p_grid_history = zeros(Float64, durata_simulazione)
u_res_history = zeros(Float64, durata_simulazione)
u_ev_history = zeros(Float64, durata_simulazione)
u_ess_history = zeros(Float64, durata_simulazione)
x1_history = zeros(Float64, durata_simulazione + 1)
x2_history = zeros(Float64, durata_simulazione + 1)

solving_times = zeros(Float64, durata_simulazione)

k = zeros(Int64, durata_simulazione)
for i = 1:durata_simulazione
    k[i] = i
end
k1 = zeros(Int64, durata_simulazione + 1)
for i = 1:durata_simulazione + 1
    k1[i] = i
end

x1_history[1] = x1_0
x2_history[1] = x2_0

# MPC loop
for t = 1 : durata_simulazione
    # Trova la soluzione per il problema di ottimizzazione MPC
    if t > durata_simulazione - (N-1)
        global N -= 1
    end
    solving_times[t] = @elapsed mpc_iteration!(t, N, T, q1, q2, r, r1, s1, s2, c, M, p_min_grid, p_max_grid, u_min_ess, u_max_ess, u_min_ev, u_hat_ev, u_min_res, u_max_res, w_res, x1_min, x1_max, x1_history[t], x1_ref, x2_min, x2_max, x2_history[t], x2_ref, p_grid_history, u_res_history, u_ess_history, u_ev_history, x1_history, x2_history)
end
```


---
# References
