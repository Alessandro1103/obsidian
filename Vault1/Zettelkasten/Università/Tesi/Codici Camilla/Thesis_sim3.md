Date: 2023-08-04
Time: 22:16
Tags: #codice

---
# Thesis_sim3

``` jl
include("mpc_thesis.jl")
using Plots
using LaTeXStrings
  
plot_font = "Computer Modern"
default(
	fontfamily=plot_font,
	linewidth=2,
	framestyle=:box,
	label=nothing,
	grid=true
)
scalefontsizes(1.5)
  
durata_simulazione = 324
t_i = 1
t_f = 20
  
# Finestra temporale per MPC
N = 36
  
# Tempo di campionamentp
T = 5.0/60 #5 minuti/60->ore
  
# Pesi per MPC
q1 = 5.0
q2 = 1.5 #rad al secondo scendono più rapidamente dei kilowatt
r = 15.0
r1 = 8.0
s1 = 6.0
s2 = 5.5
c = 100.0
#quali sono i valori dei singoli termini, u-u_ev vicini quindi numero piccolo, x2 vicino a x2_ref ma siamo disposti a sacrificarne i umeri
#i pesi devono controbilanciare i diversi pesi tra loro.
#Con c molto grande e q2 molto piccolo, u_ev vicino ma omega lontano
  
temp = zeros(durata_simulazione)
  
# Momento angolare della turbina
M = 3000.0 #kg*m^2/s grandi variazioni di potenza poca di velocità
# Velocità di sincronismo
w_s = 2*pi*50
  
# Limiti della potenza di allaccio
p_min_grid = 0.0
p_max_grid = zeros(Float64, durata_simulazione)
for i=1:durata_simulazione
	p_max_grid[i] = 400.0
end
  
# Limiti della potenza della batteria
u_min_ess = zeros(Float64, durata_simulazione)
u_max_ess = zeros(Float64, durata_simulazione)
for i=1:durata_simulazione
	u_min_ess[i] = -200.0
	u_max_ess[i] = 200.0
end
  
# Potenza richiesta dal veicolo
u_min_ev = 0.0
u_hat_ev = zeros(Float64, durata_simulazione)
  
for i=1:12
	u_hat_ev[i] = 50.0
end
for i=13:24
	u_hat_ev[i] = 100.0
end
for i=25:42
	u_hat_ev[i] = 0.0
end
for i=43:51
	u_hat_ev[i] = 50.0
end
for i=52:60
	u_hat_ev[i] = 100.0
end
for i=61:66
	u_hat_ev[i] = 150.0
end
for i=67:78
	u_hat_ev[i] = 200.0
end
for i=79:96
	u_hat_ev[i] = 250.0
end
for i=97:102
	u_hat_ev[i] = 150.0
end
for i=103:114
	u_hat_ev[i] = 100.0
end
for i=115:132
	u_hat_ev[i] = 50.0
end
for i=133:138
	u_hat_ev[i] = 0.0
end
for i=139:141
	u_hat_ev[i] = 100.0
end
for i=142:150
	u_hat_ev[i] = 150.0
end
for i=151:156
	u_hat_ev[i] = 200.0
end
for i=157:159
	u_hat_ev[i] = 250.0
end
for i=160:162
	u_hat_ev[i] = 350.0
end
for i=163:168
	u_hat_ev[i] = 400.0
end
for i=168:177
	u_hat_ev[i] = 300.0
end
for i=178:180
	u_hat_ev[i] = 250.0
end
for i=181:190
	u_hat_ev[i] = 100.0
end
for i=191:193
	u_hat_ev[i] = 50.0
end
for i=193:204
	u_hat_ev[i] = 0.0
end
for i=205:219
	u_hat_ev[i] = 50.0
end
for i=220:225
	u_hat_ev[i] = 150.0
end
for i=226:228
	u_hat_ev[i] = 200.0
end
for i=229:230
	u_hat_ev[i] = 250.0
end
for i=231:234
	u_hat_ev[i] = 300.0
end
for i=235:246
	u_hat_ev[i] = 500.0
end
for i=247:249
	u_hat_ev[i] = 400.0
end
for i=250:252
	u_hat_ev[i] = 300.0
end
for i=253:264
	u_hat_ev[i] = 200.0
end
for i=265:270
	u_hat_ev[i] = 50.0
end
for i=271:274
	u_hat_ev[i] = 0.0
end
for i=275:280
	u_hat_ev[i] = 50.0
end
for i=281:288
	u_hat_ev[i] = 150.0
end
  
# Limiti della potenza immessa in rete dalla turbina
u_min_res = 0.0
u_max_res = zeros(Float64, durata_simulazione)
for i=1:durata_simulazione
	u_max_res[i] = 200.0
end
  
ro = 1.225
radius = 6
w_s = 2*pi*50
g = 106.32
m = 2000 #7.5 : 2500 = radius : m
  
v_wind = zeros(Float64, durata_simulazione)
for i=1:12
	v_wind[i] = 10.5
end
for i=13:24
	v_wind[i] = 11.5
end
for i=25:42
	v_wind[i] = 10.0
end
for i=43:51
	v_wind[i] = 11.0
end
for i=52:60
	v_wind[i] = 11.5
end
for i=61:78
	v_wind[i] = 12.5
end
for i=79:96
	v_wind[i] = 13.0
end
for i=97:132
	v_wind[i] = 12.0
end
for i=133:150
	v_wind[i] = 10.5
end
for i=151:162
	v_wind[i] = 11.5
end
for i=163:168
	v_wind[i] = 13.0
end
for i=168:190
	v_wind[i] = 12.5
end
for i=191:219
	v_wind[i] = 10.5
end
for i=220:225
	v_wind[i] = 11.5
end
for i=226:234
	v_wind[i] = 12.0
end
for i=235:246
	v_wind[i] = 13.0
end
for i=247:252
	v_wind[i] = 12.5
end
for i=253:264
	v_wind[i] = 11.5
end
for i=265:274
	v_wind[i] = 11.0
end
for i=275:288
	v_wind[i] = 10.0
end
  
lambda = zeros(Float64, durata_simulazione)
C_p = zeros(Float64, durata_simulazione)
Pmech = zeros(Float64, durata_simulazione)
for k=1:durata_simulazione
	lambda[k] = w_s*radius/(g*v_wind[k])
	C_p[k] = 0.73((151/lambda[k]) -13.2)*exp(-18.4/lambda[k])
	Pmech[k] = 0.5*ro*(radius^2)*pi*((v_wind[k])^3)*C_p[k]
end
  
 
w_res = zeros(Float64, durata_simulazione)
for i=1:durata_simulazione
	w_res[i] = Pmech[i]
end
  
# Limiti dello stato di carica
x1_min = zeros(Float64, durata_simulazione+1)
x1_max = zeros(Float64, durata_simulazione+1)
for i=1:durata_simulazione+1
	x1_min[i] = 0.0
	x1_max[i] = 300.0
end
x1_0 = 170.0
x1_ref = 170.0
  
# Limiti della velocità angolare della turbina
x2_min = zeros(Float64, durata_simulazione+1)
x2_max = zeros(Float64, durata_simulazione+1)
for i=1:durata_simulazione+1
	x2_min[i] = w_s*(1 - 0.3)
	x2_max[i] = w_s*(1 + 0.3)
end
x2_0 = w_s
x2_ref = w_s
  
# ----------------- Controlli e grandezze da controllare
  
p_grid_history = zeros(Float64,durata_simulazione)      
u_res_history = zeros(Float64,durata_simulazione)  
u_ev_history = zeros(Float64,durata_simulazione)    
u_ess_history = zeros(Float64,durata_simulazione)
x1_history = zeros(Float64,durata_simulazione+1)
x2_history = zeros(Float64, durata_simulazione+1)
  
solving_times = zeros(Float64,durata_simulazione)
  
#---- Per grafici
k = zeros(Int64, durata_simulazione)
for i=1:durata_simulazione
	k[i] = i
end
k1 = zeros(Int64, durata_simulazione+1)
for i=1:durata_simulazione+1
	k1[i] = i
end
  
temp = zeros(durata_simulazione)
  
x1_history[1] = x1_0
x2_history[1] = x2_0
  
#----MPC loop
for t = 1 : durata_simulazione
	#---- Find solution
	if(t > durata_simulazione - (N-1))
		global N -= 1
	end
	println(t)
	println(N)
	solving_times[t] = @elapsed mpc_iteration!(t, N, T, q1, q2, r, r1, s1, s2, c, M, p_min_grid, p_max_grid, u_min_ess, u_max_ess, u_min_ev, u_hat_ev, u_min_res, u_max_res, w_res, x1_min, x1_max, x1_history[t], x1_ref, x2_min, x2_max, x2_history[t], x2_ref, p_grid_history, u_res_history, u_ess_history,  u_ev_history, x1_history, x2_history)
end
```


---
# References
