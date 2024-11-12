# Lecture3 Exponential Coordinate of Rigid Body

[TOC]

## Exponential Coordinate of $SO(3)$

exp: $[\hat{\omega}]\theta \in so(3) \rightarrow R = \displaystyle e^{[\hat{\omega}]\theta} \in SO(3)$

log: $R \in SO(3) \rightarrow [\hat{\omega}]\theta \in so(3)$



the vector $\hat{\omega}\theta$ is called the *exponential coordinate* for the $R$, or the canonical coordinates of the $SO(3)$.



Taylor expansion:
$$
R = \displaystyle e^{[\hat{\omega}]\theta} = I + \theta [\hat{\omega}] + \frac{\theta^2}{2!}[\hat{\omega}]^2 + \frac{\theta^3}{3!}[\hat{\omega}]^3+... 
$$
Take the first two order components and do some approximation

**Rodrigue's Formula**
$$
e^{[\hat{\omega}]\theta} = I + [\hat{\omega}]\sin(\theta)+[\hat{\omega}]^2(1-\cos(\theta))
$$


### Logarithm of Rotations

$\tr(R)=1+2 \cos(\theta)$

- If $R=I$, then $\theta=0$, $\hat{\omega}$ is undifined

- If $\tr(R)=-1$, then $\theta=\pi$, $\hat{\omega}$ equal to one of the following 
  $$
  \hat{\omega} \in \{\displaystyle 
  \frac{1}{\sqrt{2(1+r_{33})}}
  \begin{bmatrix}r_{13} \\ r_{23} \\ 1+r_{33}\end{bmatrix},
  \frac{1}{\sqrt{2(1+r_{22})}}
  \begin{bmatrix}r_{12} \\ r_{22} \\ 1+r_{32}\end{bmatrix},
  \frac{1}{\sqrt{2(1+r_{11})}}
  \begin{bmatrix}r_{11} \\ r_{21} \\ 1+r_{31}\end{bmatrix},
  \}
  $$
  
  i.e. rotate about one axis (x, y, or z) for 180 degrees. 

- Otherwise, $\theta = \cos^{-1}(\frac{1}{2}(\tr(R)-1)) \in [0,\pi)$ and $[\hat{\omega}] = \frac{1}{2\sin(\theta)}(R-R^T)$

## Euler Angles

There is a very intuitive fact:

- Pre-multiply = extrinsic rotation

- Post-multiply = intrinsic rotation

XYZ corresponds to roll-pitch-yaw respectively 

## Exponential Coordinate of $SE(3)$

### Exponential Map of $se(3)$: from Twist to Rigid-Body Motion

W.l.o.g., assume $\|\omega\|=1$
$$
\displaystyle T = e^{[\mathcal{V}]\theta} = 
\begin{bmatrix}
e^{[\omega]\theta} & G(\theta)v \\
0 & 1
\end{bmatrix},
\text{with}\
G(\theta) = I\theta + (1-\cos(\theta))[\omega] + (\theta-\sin(\theta))[\omega]^2
$$

### Log of $SE(3)$: from Rigid-Body Motion to Twist

screw axis $S=(\omega,v)$
$$
[\mathcal{S}] = 
\begin{bmatrix}
[\omega] & v \\
0 & 0
\end{bmatrix}
\in se(3)
$$
$$
T=\displaystyle e^{[\mathcal{S}]\theta}=
\begin{bmatrix}
R & p \\
0 & 1
\end{bmatrix}
\in SE(3)
$$

- if $R = I$, then $\omega=0, v=p/\|p\|, \theta=\|p\|$

- Use logarithm of rotation to determine $\omega$ and $\theta$, then
  $$
  v = G^{-1}(\theta)p, \text{where}\ G^{-1}(\theta) = \frac{1}{\theta}I - \frac{1}{2}[\omega]+(\frac{1}{\theta}-\frac{1}{2}\cos{\frac{\theta}{2}})[\omega]^2
  $$
