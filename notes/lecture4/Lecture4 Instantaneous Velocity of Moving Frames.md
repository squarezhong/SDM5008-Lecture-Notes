# Lecture4: Instantaneous Velocity of Moving Frames

[TOC]

## Instantaneous Velocity of Rotating Frame

$$
\dv{}{t}R_A(t) = [\omega_A(t)]R_A(t) \Rightarrow
[\omega_A(t)] = \dot{R}_A(t)R_A^{-1}(t)
$$

**Proof**:

- In world coordinate

$$
\begin{align}
& R_A(t) = 
\begin{bmatrix}
\hat{x}_A & \hat{y}_A & \hat{z}_A
\end{bmatrix} \\

& \dot{\hat{x}}_A = \omega_A \times \hat{x}_A \\
& \dot{\hat{y}}_A = \omega_A \times \hat{y}_A \\
& \dot{\hat{z}}_A = \omega_A \times \hat{z}_A \\

& \dot{R}_A = 
\begin{bmatrix}
\dot{\hat{x}}_A & \dot{\hat{y}}_A & \dot{\hat{z}}_A
\end{bmatrix} =
\omega_A \times R_A = [\omega_A]R_A\\

& \prescript{o}{}{\dot{R}_A} = 
[\prescript{o}{}{\omega_A}]\prescript{o}{}{R_A}
\Rightarrow [\prescript{o}{}{\omega_A}] = 
\prescript{o}{}{\dot{R}_A} \prescript{o}{}{R_A^{-1}}
\end{align}
$$



- In {A} frame

  Remember that $[R\omega] = R[\omega]R^T$

$$
\begin{align}
\prescript{A}{}{\omega_A} &= 
\prescript{A}{}{R_o} \prescript{o}{}{\omega_A}\\

[\prescript{o}{}{\omega_A}]&= 
\prescript{o}{}{\dot{R}_A} \prescript{o}{}{R_A^{-1}}\\

[\prescript{A}{}{\omega_A}] &=
[\prescript{A}{}{R_o} \prescript{o}{}{\omega_A}]\\ 

&= \prescript{A}{}{R_o}
[\prescript{o}{}{\omega_A}]
\prescript{A}{}{R_o^T} \\

&=\prescript{A}{}{R_o}
\prescript{o}{}{\dot{R}_A} 
\prescript{o}{}{R^{-1}_A}
\prescript{o}{}{R_A} \\

&=\prescript{A}{}{R_o}
\prescript{o}{}{\dot{R}_A} \\

[\prescript{A}{}{\omega_A}] &=
\prescript{o}{}{R_A^{-1}}
\prescript{o}{}{\dot{R}_A}

\end{align}
$$

  

## Instantaneous Velocity of Moving Frame

$$
\dv{}{t}T_A(t) = [\mathcal{V}_A(t)]T_A(t) \Rightarrow
[\mathcal{V}_A(t)] = \dot{T}_A(t)T_A^{-1}(t)
$$

You can find the proof in noted lecture slide. The process is similar to rotation frame.
