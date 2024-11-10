# Lecture 1: Rigid Body Configuration and Velocity

[TOC]

## Math Basics

### Skew symmetric representation

cross product can be expressed as matrix product

$a \times b = [a]b$
$$
a = \begin{bmatrix}a_1 \\ a_2 \\ a_3\end{bmatrix} \leftrightarrow [a] = \begin{bmatrix} 0 & -a_3 & a_2 \\ a_3 & 0 & -a_1 \\ -a_2 & a_1 &0\end{bmatrix}
$$
$[a] = -[a]^T$

### Special Orthogonal Group

$$
SO(n) = \{R \in \mathbb{R}^{n\times n}: R^T R=I, det(R)=1\}
$$



## Rigid Body Velocity (Twist)

Pick an arbitrary reference point $r$, then for any body-fixed point on the body

$v_p = v_r + \omega \times \overrightarrow{rp}$

$v_r$ is the speed of $r$ w.r.t. rigid body fixed frame.

### Definition

Twist, namely spatial velocity

Spatial velocity is a set of **parameters**, not the absolute velocity.

$\mathcal{V}_{r} = (\omega_r, v_r)$

### Change Reference for Twist

$\prescript{A}{}{\mathcal{V}} = \prescript{A}{}{X_B} \prescript{B}{}{\mathcal{V}}$

$T = (R,p)$

$\prescript{A}{}{X_B} = [{Ad}_T] \triangleq \begin{bmatrix}R & 0 \\ [p]R & R \end{bmatrix}$

## Geometric Aspect of Twis: Screw Motion

### Definition

Screw Motion: screw axis ${q,\hat{s},h}$ + rotation speed $\dot{\theta}$

- $\hat{s}$: unit vector in the directrion of the rotation axis
- $q$: any point on the rotation axis
- $h$: **screw pitch**: the ratio of the linear velocity along the screw axis
  to the angular velocity about the screw axis

Theorem (Chasles): **Every rigid body motion can be realized by a screw
motion.**  

### Transformation

#### Screw Motion to Twist

Fix a reference frame {A} with origin $o_A$

$\prescript{A}{}{\omega} = \prescript{A}{}{\hat{s}} \dot{\theta}$

$\prescript{A}{}{v_{o_A}} = \prescript{A}{}{v_q}+\prescript{A}{}{\omega}\times (-\prescript{A}{}{q}) = \prescript{A}{}{\hat{s}}(h\dot{\theta}) - \prescript{A}{}{\omega} \times \prescript{A}{}{q}$

#### Twist to Screw Motion

- $\omega=0$, pure translation

​	$\hat{s}=\displaystyle\frac{v}{\|v\|},\ \dot{theta}=\|v\|,\ h=\infin,$ $q$ can bre arbitrary

- $\omega \neq 0$

  $\hat{s}=\displaystyle\frac{\omega}{\|\omega\|},\ \dot{\theta}=\|\omega\|,\ q=\frac{\omega \times v}{\|\omega\|^2},\ h = \frac{\omega^Tv}{\|\omega\|^2}$

Here $v$ is the velocity of the reference point, not the velocity along the screw axis.

### Screw Representation of a Twist

Twist with a unit speed,
$$
\mathcal{V} = \hat{\mathcal{S}}\dot{\theta}
$$
$\hat{S} \leftrightarrow  (\hat{s},h,q), \dot{\theta}=1$



