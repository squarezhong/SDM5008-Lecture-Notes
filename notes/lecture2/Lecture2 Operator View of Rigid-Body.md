# Lecture2 Operator View of Rigid-Body
## Rotation Operation vis ODE

Consider a rotation with unit angular velocity $\hat{\omega}$
$$
\begin{equation}
\dot{p}(t) = \hat{\omega} \times p(t) = [\hat{\omega}]p(t), \text{with}\ p(0)=p_0 
\end{equation}
$$
There is linear ODE solution: $p(t) = e^{[\hat{\omega}]t}p_0$

At $t = \theta$, the point has been rotated by $\theta$ degree, $p(\theta) = e^{[\hat{\omega}]\theta}p_0$

## Rotation Matrix as a Rotation Operator

(*coordinate free*)

Rotation matrix can be written as $R = \text{Rot}(\hat{\omega},\theta) \triangleq e^{[\hat{\omega}]\theta}$

i.e. rotation operation about $\hat{\omega}$ by $\theta$

### Rotation Matrix Properties

- $RR^T=I$	definition

- $R_1R_2 \in SO(3)$ if $R_1,R_2\in SO(3)$    

  product of rotation matrices is also a rotation matrix

- $\|Rq-Rp\|=\|p-q\|$  

  rotation matrix preserves distance

- $R(v\times \omega)=(Rv)\times(R\omega)$

  rotation matrix preserves orientation

- $R[\omega]R^T=[R\omega]$

## Rotation Operator in Different Frames

Consider the same rotation operation $\text{Rot}(\hat{\omega,\theta})$

In frame-{A} and frame-{B}
$$
\prescript{A}{}{\hat{\omega}} = \prescript{A}{}{R_B} \prescript{B}{}{\hat{\omega}}
$$

$$
\prescript{A}{}{\text{Rot}(\prescript{A}{}{\hat{\omega}},\theta)} = \prescript{A}{}{R_B} \prescript{B}{}{\text{Rot}(\prescript{B}{}{\hat{\omega}},\theta)} \prescript{B}{}{R_A}
$$

You can think like this: 
There is a point in frame {A}, first we transform it to frame {B}, then do rotation, finally transform back to frame {A}. This should be equivalent to rotation in frame {A}.

 ## Rigid-Body Operation via ODE

$$
\begin{equation}
\dot{p}(t) = \omega \times p(t) + v \rightarrow 
\begin{bmatrix}
\dot{p}(t) \\ 0
\end{bmatrix} =
\begin{bmatrix}
[\omega] & v \\
0 & 0
\end{bmatrix}
\begin{bmatrix}
p(t) \\ 1
\end{bmatrix}
\end{equation}
$$

Solution to equation (2) is
$$
\begin{bmatrix}
p(t) \\ 1
\end{bmatrix} =
\text{exp}
(
\begin{bmatrix}
[\omega] & v \\
0 & 0
\end{bmatrix} t
)
\begin{bmatrix}
p(0) \\ 1
\end{bmatrix}
$$


For any twist $\mathcal{V} = (\omega,v)$
$$
[\mathcal{V}] = 
\begin{bmatrix}
[\omega] & v \\
0 & 0
\end{bmatrix}
$$
The above definition also applies to screw axis $\mathcal{S} = (\omega,v)$

With this notation, the solution to (2) is
$$
\tilde{p} = \displaystyle e^{[\mathcal{V}]t}\tilde{p}(0) = e^{[\mathcal{S}]\theta}\tilde{p}(0)
$$


Define $SE(3) = \{([\omega],v):[\omega]\in SO(3), v\in \mathbb{R}^3\}$

Any $T\in SE(3)$ can be written as $T=\displaystyle e^{[\mathcal{S}]\theta}$

## Homogeneous Transformation as Rigid-Body Operator

- $\tilde{p}^{\prime} = T \tilde{p}$: "rotate" $p$ about screw axis $\mathcal{S}$ by $\theta$ degree
- $TT_A$: "rotate" {A} frame about $\mathcal{S}$ by $\theta$ degree
- $T \leftrightarrow T_B^{-1}TT_B$

## Rigid-Body Operation of Screw Axis

After transformation $T = (R,p)$, screw axis $\mathcal{S}$ becomes
$$
\mathcal{S}^{\prime} = [{Ad}_T]S
$$
$[{Ad}_T] \triangleq \begin{bmatrix}R & 0 \\ [p]R & R \end{bmatrix}$
