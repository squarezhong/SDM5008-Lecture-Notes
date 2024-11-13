# Lecture5: Product of Exponential and Kinematics of Open Chain

> Notes taken by [squarezhong](https://github.com/squarezhong)
> Repo address: [squarezhong/SDM5008-Lecture-Notes](https://github.com/squarezhong/SDM5008-Lecture-Notes)

[toc]

## Kinematics

- **Forward Kinematics**

  Given joint variables $\theta=(\theta_1,\theta_2,...,\theta_n)$, derive the configuration of the end-effector frame $T=(R,p)$.

- **Velocity Kinematics**

  Derive the **Jacobian Matrix**: lineariezd map from joint velocities $\dot{\theta}$ to the spatial velocity $\mathcal{V}$ of the end effector. 

## Product of Exponential Formula Derivations

### Definition

Define $\prescript{0}{}{\bar{\mathcal{S}}_i} = \prescript{0}{}{\bar{\mathcal{S}}_i(0,...,0)}$ : the screw axis of joint $i$ expressed in frame {0} when the robot is at the home position. It is a constant.

The overall forward kinematics:
$$
T_{sb}(\theta_1,\theta_2,...,\theta_n)=
\underbrace{
e^{[\prescript{0}{}{\bar{\mathcal{S}}_1}]\theta_1}
e^{[\prescript{0}{}{\bar{\mathcal{S}}_2}]\theta_2}
...
e^{[\prescript{0}{}{\bar{\mathcal{S}}_n}]\theta_n}
}_{PoE}
M
$$

### Proof

For simplicity, assume that $n=2$

Apply screw motion along $\prescript{0}{}{\bar{\mathcal{S}}_1}$ first:
$$
\begin{equation}
T_{sb}(\theta_1,0) = 
e^{[\prescript{0}{}{\bar{\mathcal{S}}_1}]\theta_1}M
\end{equation}
$$
Now screw axis for joint 2 has been changed. The new axis:
$$
\prescript{0}{}{\mathcal{S}_2}=
\prescript{0}{}{\mathcal{S}_2}(\theta_1,0)
\neq \prescript{0}{}{\bar{\mathcal{S}}_2}
$$

$$
\prescript{0}{}{\bar{\mathcal{S}}_2} 
\xrightarrow{\hat{T_1}=
e^{[\prescript{0}{}{\bar{\mathcal{S}}_1}]\theta_1}}
\prescript{0}{}{\mathcal{S}_2}(\theta_1)=
\underbrace{
[\text{Ad}_{\hat{T_1}}]
}_{6\times6}
\prescript{0}{}{\bar{\mathcal{S}}_2}
$$

Fact: 
$$
\text{If}\
\mathcal{S}' = [\text{Ad}_T]\mathcal{S} 
\Leftrightarrow
[\mathcal{S}'] = T[\mathcal{S}]T^{-1}
$$
Then
$$
\begin{align}
\displaystyle
e^{[\prescript{0}{}{\bar{\mathcal{S}}_2(\theta_1)}]\theta_2} 
&=
e^{[[\text{Ad}_{\hat{T_1}}]
\prescript{0}{}{\bar{\mathcal{S}}_2}]\theta_2} \\
&=
e^{\hat{T_1}[\prescript{0}{}{\bar{\mathcal{S}}_2}]\hat{T_1}^{-1}}\\
&=
\hat{T_1}e^{[\prescript{0}{}{\bar{\mathcal{S}}_2}]\theta_2}\hat{T_1}^{-1}\\
\end{align}
$$
Finally
$$
\begin{align}
T_{sb}(\theta_1,\theta_2) &=
e^{[\prescript{0}{}{\mathcal{S}_2}]\theta_2}
T_{sb}(\theta_1,0) \\
&=
\hat{T_1}
e^{[\prescript{0}{}{\bar{\mathcal{S}}_2}]\theta_2}
\hat{T_1}^{-1}
e^{[\prescript{0}{}{\bar{\mathcal{S}}_1}]\theta_1}
M \\
&=
\hat{T_1}
e^{[\prescript{0}{}{\bar{\mathcal{S}}_2}]\theta_2}
M \\
&=
e^{[\prescript{0}{}{\bar{\mathcal{S}}_1}]\theta_1}
e^{[\prescript{0}{}{\bar{\mathcal{S}}_2}]\theta_2}
M
\end{align}
$$

> Note that $\hat{T_1}=e^{[\prescript{0}{}{\bar{\mathcal{S}}_1}]\theta_1}$ and $T^{-1}T=I$

