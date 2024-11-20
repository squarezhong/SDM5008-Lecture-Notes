# Lecture7: Rigid-Body Dynamics

> Notes taken by [squarezhong](https://github.com/squarezhong)
> Repo address: [squarezhong/SDM5008-Lecture-Notes](https://github.com/squarezhong/SDM5008-Lecture-Notes)

[toc]

## Spatial Force (Wrench)

### Definition

Consider a rigid body with many forces on it and fix an arbitrary point $O$ in space

The net effect of these forces can be expressed as 

- A **net force** $f$, acting along a line passing through $O$

- A **moment** $n_O$ about point $O$



**Spatial Force (Wrench)** is given by the 6D vector
$$
\mathcal{F}=
\begin{bmatrix}
n_O \\f
\end{bmatrix}
$$

### Plücker Coordinate Systems

Given a frame {A}, the Plücker coordinate of a spatial force $\mathcal{F}$ is given by
$$
\prescript{A}{}{\mathcal{F}}=
\begin{bmatrix}
\prescript{A}{}{n_{o_A}} \\
\prescript{A}{}{f}
\end{bmatrix}
$$

- Coordinate transform
  $$
  \prescript{A}{}{\mathcal{F}}=
  \prescript{A}{}{X_B^*}
  \prescript{B}{}{\mathcal{F}}\quad
  \text{where}\ 
  \prescript{A}{}{X_B^*}=
  \prescript{B}{}{X_A^T}
  $$



### Wrench-Twist Pair and Power

Suppose a rigid body has a twist $\prescript{A}{}{\mathcal{V}}=(\prescript{A}{}{\omega},\prescript{A}{}{v_{o_A}})$ and a wrench $\prescript{A}{}{\mathcal{F}}=(\prescript{A}{}{n_{o_A}},\prescript{A}{}{f})$ act on the body. Then the power is
$$
P = (\prescript{A}{}{\mathcal{V}})^T\ \prescript{A}{}{\mathcal{F}}
$$

### Joint Torque

$$
P=\mathcal{V}^T \mathcal{F} = (\hat{\mathcal{S}}^T \mathcal{F})\dot{\theta} \triangleq \tau\dot{\theta}
$$

$\tau = \hat{\mathcal{S}^T \mathcal{F}} = \hat{\mathcal{S}} \mathcal{F}^T$ is the projection of the wrench onto the screw axis, i.e. the effective part of the wrench.

- $\tau$ can be referred to as joint "torque" or **generalized force**

## Spatial Momentum

### Rotational Inertia

Rotational Inbertia $\bar{I} = \int_V \rho(r)[r][r]^T dr$

- $\rho(\cdot)$ is the density function of the body
- $\bar{I}$ depends on coordinate system (constant if origin coincides with CoM)

### Spatial Momentum

- Linear momentum (动量)

  $L \triangleq mv_c$

- Angular momentum about CoM

  $\phi_c = \bar{I}\omega$

- Angular momentum about a point $O$

  $\phi_o = \sum_i \overrightarrow{Or_i}\times(m_iv_i) = \phi_c + \overrightarrow{OC}\times L$ 



Spatial Momentum:
$$
h \triangleq
\begin{bmatrix}
\phi_r \\ L
\end{bmatrix}
$$
n is the reference point.



- Coordinate transform:
  $$
  \prescript{A}{}{h} = 
  \prescript{A}{}{X_B^*}
  \prescript{B}{}{h}
  $$
  

### Spatial Inertia

Spatial inertia $\mathcal{I}$ is given by
$$
h = \mathcal{I} \mathcal{V}
$$
Let {C} be a frame whose origin coincide with CoM. We have
$$
\prescript{C}{}{h}=
\begin{bmatrix}
\prescript{C}{}{\bar{I}}
\prescript{C}{}{\omega}\\
m \prescript{C}{}{v_c}
\end{bmatrix}=
\begin{bmatrix}
\prescript{C}{}{\bar{I_c}} & 0\\
0 & mI_3
\end{bmatrix}
\begin{bmatrix}
\prescript{C}{}{\omega}\\
\prescript{C}{}{v_c}
\end{bmatrix}
$$
Then
$$
\prescript{C}{}{\mathcal{I}}=
\begin{bmatrix}
\prescript{C}{}{\bar{I_c}} & 0\\
0 & mI_3
\end{bmatrix}
$$

- Coordinate Transform
  $$
  \prescript{A}{}{\mathcal{I}}=
  \prescript{A}{}{X_C^*}
  \prescript{C}{}{\mathcal{I}}
  \prescript{C}{}{X_A}
  $$
  

