Formulario di Fisica Tecnica
============================

## Conversioni di pressione
- $1$ bar = $10^5$ Pa
- $1$ atm = $101325$ Pa
- $1$ ata = $98066.5$ Pa

# Gas Ideali

## Equazione di stato
$$PV = nRT$$ dove 
$R = 8314 \frac{J}{Kmol \cdot K}
= 8.314 \frac{KJ}{Kmol\cdot K}$

$$Pv = \frac{M}{M_m}RT = MR^*T \rightarrow Pv = R*T$$
dove $v = \frac{V}{M}$ e $\Delta V = M\Delta v$

## Lavoro
$$\delta l = Fds = PSds = PdV$$
$$l^\rightarrow = \int Pdv = R^*T \ln\left(\frac{v_f}{v_i}\right)$$

## Capacità termica
$$C_x = \left( \frac{\delta Q^\rightarrow}{dT} \right)_x$$

## Calore specifico
$$c_x = \frac{C_x}{M} = \frac{1}{M}\left( \frac{\delta Q^\rightarrow}{dT} \right)_x$$

## Relazione di Mayer
$$c_p = c_v + R^*$$

| $c_v$ | $c_p$ | Gas |
|-------|-------|-----|
| $\frac{3}{2}R$ | $\frac{5}{2}R$ | Monoatomico |
| $\frac{5}{2}R$ | $\frac{7}{2}R$ | Biatomico |
| $\frac{6}{2}R$ | $\frac{8}{2}R$ | Poliatomico |

## Trasformazioni politropiche

$$n = \frac{c_x - c_p}{c_x - c_v}$$

$$P_iv_i^n = cost.$$

$$P_av_a^n = P_bv_b^n$$

| Trasformazione | n |
|-------|-------|
| Isoterma ($T=cost$) | $n=1$ |
| Isocora ($v=cost$) | $n=\pm\infty$ |
| Isobara ($P=cost$) | $n=0$ |
| Adiabatica ($q=cost$) | $n=k=\frac{c_p}{c_v}$ |

## Lavoro nelle trasformazioni politropiche

$$l = \int_{v_1}^{v_2} Pdv = P_1v_1 \ln \frac{v_2}{v_1} = P_1v_1 \ln \frac{P1}{P2}$$

## Entalpia
$$h = u + Pv$$
$$H = Mh = M(u + Pv) = U + PV$$

## Variazione di Entalpia
$$\Delta H = Mc_p\Delta T$$

Nei gas perfetti
$$\Delta h = h_2 - h_1 = c_p (T_1 - T_2)$$
$$\Delta H = M(h_2 - h_1) = M c_p (T_1 - T_2)$$

## Variazione di energia interna
$$\Delta U = m \Delta u = Q^\leftarrow - L^\rightarrow$$

Nei gas perfetti
$$\Delta U = Mc_v\Delta T$$

## Variazione di entropia
$$\Delta S = M\left(c_p \ln \frac{T_1}{T_2} - R^* \ln \frac{P2}{P1} \right)$$

$$\Delta S = m\Delta s= S_{Q^\leftarrow} + S_{Irr}$$

# Sistemi Aperti

## Portata volumetrica
$$\dot m = \frac{\dot V}{v}$$

## Bilancio d'energia
$$\dot E = \sum_i \dot E_i^\leftarrow$$

## Energia associata al trasporto di massa
$$E_m = \sum_i m_i \left( u + gz + \frac{\omega^2}{2}\right)_i$$

## Potenza associata al trasporto di massa
$$\dot E_m = \sum_i \dot m_i^\leftarrow \left( u + gz + \frac{\omega^2}{2}\right)_i$$

## Bilancio di potenza in regime stazionario
In regime stazionario, cioè quando $|\dot m_{in}| = |\dot m_{out}| = |\dot m|$

$$\dot m (h_{out} - h_{in}) = \dot Q^\leftarrow - \dot L^\rightarrow$$

## Bilancio d'entropia
$$\dot S = \sum_i \dot m_i^\leftarrow si + \dot s_q^\leftarrow + \dot s_{irr}$$

## Bilancio di entropia in regime stazionario
$$\dot m \Delta s = \dot S_Q + \dot S_{irr}$$

# Macchina aperta

## Dispositivo adiabatico

$$-\dot L = \dot m (h_{out} - h_{in})$$

$$\dot S_{irr} = \dot m (s_{out} - s_{in})$$

## Diffusore ($\omega\downarrow$) / Ugello ($\omega\uparrow$)

$$h_{in} - h_{out} + \frac{\omega_{in}^2-\omega_{out}^2}{2}$$

## Scambiatore di calore
$$\dot m_{in}^\leftarrow (h_{in} - h_{out}) + \dot Q = 0$$
$$\dot m_{in}^\leftarrow (s_{in} - s_{out}) + \dot S_Q^\leftarrow + \dot S_{irr} = 0$$
## Valvola di laminazione

$$h_{in} = h_{out}$$
$$\dot m (s_{in} - s_{out}) + \dot S_{irr} = 0$$

## Rendimento nelle macchine aperte

$$\eta_{2p} = \frac{\eta_{Reale}}{\eta_{Ideale}} = \frac{\dot L_R}{\dot L_I} = \frac{h_1 - h_2'}{h_1 - h_2}$$
$$\eta_{2p} = \frac{\epsilon_{F,Reale}}{\epsilon_{F,Ideale}}$$
$$\eta_{2p} = \frac{\epsilon_{PdC,Reale}}{\epsilon_{PdC,Ideale}}$$

### Macchine motrici
$$\eta_{Ideale} = 1-\frac{T_F}{T_C} = \frac{L}{Q_C}$$
$$\dot L_{Ideale} = \eta_{Ideale}\dot Q_C = \dot m c_p (T_1 - T_{2,Ideale})$$


### Macchine motrici
$$\epsilon_{F, Ideale} = 1-\frac{T_F}{T_C - T_F}$$

$$\epsilon_{PdC, Ideale} = 1-\frac{T_C}{T_C - T_F}$$

