# Lecture6: Velocity Kinematics-Geometric and Analytic Jacobian of Open Chain

> Notes taken by [squarezhong](https://github.com/squarezhong)
> Repo address: [squarezhong/SDM5008-Lecture-Notes](https://github.com/squarezhong/SDM5008-Lecture-Notes)

[TOC]

## Velocity Kinematics

Derive the **Jacobian Matrix**: lineariezd map from joint velocities $\dot{\theta}$ to the spatial velocity $\mathcal{V}$ of the end effector (frame {b}). 

- Twist representation $\rightarrow$ **Geometric Jacobian**

  $\mathcal{V_b}=J(\theta)\dot{\theta}$

- Local coordinate of $SE(3)$ $\rightarrow$ **Analytic Jacobian** 
  
  Let $x \in \mathbb{R}^p$ be the task space variable
  
  e.g. some of Cartesain + Euler angle of end-effector frame
  $$
  \begin{aligned}
  & x = g(\theta_1,\theta_2,...\theta_n) \\
  & \dot{x}=\dv{}{t}(g(\theta_1,...\theta_n))=
  \underbrace{\frac{\partial g}{\partial \theta}}_{\text{Analytic Jacobian}}\dot{\theta}=
  J_a(\theta)\dot{\theta}\\
  & \frac{\partial g}{\partial \theta}\in \mathbb{R}^{n_x\times n}
  \end{aligned}
  $$
  
- Relation between Geometric Jacobian and Analytic Jacobian

  $J_a(\theta)=E(x)J(\theta)$

  where $E(x)$ can be easily found with given parameterization $x$

## Geometric Jacobian Derivations

In general, the end-effector twist $\mathcal{V}=(\omega,v)$
$$
\mathcal{V}_b = 
\begin{bmatrix}
J_1(\theta) & J_2(\theta) &\cdots& J_n(\theta)
\end{bmatrix}
\begin{bmatrix}
\dot{\theta}_1 \\
\dot{\theta}_2 \\
\vdots\\
\dot{\theta}_n \\
\end{bmatrix}
$$
where $\theta = (\theta_1,\theta_2,\cdots,\theta_n)$,

$J_i(\theta)$ is the screw axis of joint $i$ when all other joints do not move (i.e. $\forall j\neq i,\dot{\theta}_j=0$)



In coordinate free notation, $J_i(\theta) = \mathcal{S}_i(\theta)$

Using local coordinate
$$
\prescript{i}{}{J_i} = \prescript{i}{}{\mathcal{S}_i},\quad i=1,2,\cdots,n
$$
In fixed frame {0}
$$
\begin{equation}\tag{1}
\prescript{0}{}{J_i}(\theta) =
\prescript{0}{}{X_i}(\theta)
\prescript{i}{}{S_i},
\quad i=1,2,\cdots,n
\end{equation}
$$
where $\prescript{0}{}{X_i}(\theta)$ is the change of coordinate matrix for special velocities.

Recall the proof we did in Lecture5
$$
\begin{equation}\tag{2}
T_{i}(\theta)=
e^{[\prescript{0}{}{\bar{\mathcal{S}}_1}]\theta_1}
e^{[\prescript{0}{}{\bar{\mathcal{S}}_2}]\theta_2}
...
e^{[\prescript{0}{}{\bar{\mathcal{S}}_i}]\theta_i}
M
\Rightarrow
\prescript{0}{}{X_i}(\theta) =
[\text{Ad}_{\prescript{0}{}{T_i}(\theta)}]
\end{equation}
$$


To calculate more efficiently, we then derive a **recursive** Jacobian
$$
\begin{equation}\tag{3}
\prescript{0}{}{J_i(\theta)} = 
\prescript{0}{}{\mathcal{S}_i(\theta)} =
[\text{Ad}_{\hat{T}(\theta_1,\cdots,\theta_{i-1})}]
\prescript{0}{}{\bar{\mathcal{S}}_i}
\end{equation}
$$
where $\hat{T}(\theta_1,\cdots,\theta_{i-1}) = 
e^{[\prescript{0}{}{\bar{\mathcal{S}}_1}]\theta_1}
e^{[\prescript{0}{}{\bar{\mathcal{S}}_2}]\theta_2}
\cdots
e^{[\prescript{0}{}{\bar{\mathcal{S}}_{i-1}}]\theta_{i-1}}$



## Analytic Jacobian Derivations

You should have learned it in traditional robotics course.

