# Lecture11: Policy Gradients for Reinforcement Learning

> Notes taken by [squarezhong](https://github.com/squarezhong)
> Repo address: [squarezhong/SDM5008-Lecture-Notes](https://github.com/squarezhong/SDM5008-Lecture-Notes)

[toc]

## Problem Formulation

- RL Problem: find optimal policy $\pi^*$
  $$
  V^{*}(s)=\max\limits_{\pi}(E_{\tau \sim \pi}(R(\tau)|S_0=s))
  $$

- Parameterize policy by a parameter vector $\theta$, denote:

  - $\pi_{\theta}:=\pi_{\theta}(\cdot | s)$
  - $P_{\theta}(\tau)$: the likelihood of trajectory $\tau$ under policy $\pi_{\theta}$

  $$
  \begin{equation}
  P_{\theta}(\tau) = P(s_0) \prod_{t=0}^{T-1} \pi_{\theta}(a_t|s_t) P(s_{t+1}|s_t, a_t)
  \end{equation}
  $$

- Reformulate the MDP problem as an optimization problem

  - assume $s_0$ distribution is included in trajectory likelihood $P_{\theta}(\tau)$

  - Utility function:
    $$
    U(\theta) = E_{\tau \sim P_{\theta}(\tau)}[R(\tau)]=
    \sum_{\tau}P_{\theta}(\tau) R(\tau)
    $$

  - RL problem reduces to finding the optimal policy parameter $\theta$
    $$
    \max_{\theta} U(\theta) =
    \max_{\theta} \sum_{\tau} P_{\theta}(\tau) R(\tau)
    $$

    - $\theta$: dim is high
    - $U(\theta)$: hard to compute (approximate)

  - Policy gradient use $1^{st}$ order gradient ascend method

## Derivation of Policy Gradient

Optimize $U(\theta)$ involves evaluating $U(\theta)$

- think of $\tau$ as a random variable (in trajectory space)
- By monte carlo: $U(\theta) = \sum_{\tau}P_{\theta}(\tau) R(\tau) \approx \frac{1}{N} \sum_i R(\tau^{(i)}), \quad \tau^{(i)} \overset{\text{iid}}{\sim} P_{\theta}(\tau)$

### Compute $\nabla_{\theta} U(\theta)$

$$
\nabla_{\theta} U(\theta) =
\frac{\partial}{\partial \theta} 
\sum_{\tau} P_{\theta}(\tau) R(\tau) =
\sum_{\tau} R(\tau) \frac{\partial}{\partial \theta} P_{\theta}(\tau)
$$

Note the fact that $\frac{\nabla_{\theta} P_{\theta}(\tau)}{P_{\theta}(\tau)} = \nabla_{\theta} \log(P_{\theta}(\tau))$

Then

$$
\begin{aligned}
\nabla_{\theta} U(\theta) &= \sum_{\tau} R(\tau) P_{\theta}(\tau) \frac{\nabla_{\theta} P_{\theta}(\tau)}{P_{\theta}(\tau)} = \sum_{\tau} R(\tau) P_{\theta}(\tau) \nabla_{\theta} \log(P_{\theta}(\tau)) \\
&= \mathop{E}\limits_{\tau \sim P_{\theta}(\tau)}
\left(R(\tau) \nabla_{\theta} \log(P_{\theta}(\tau))\right) \\
&\approx \frac{1}{N}\sum_{\tau} 
R(\tau^{(i)}) \nabla_{\theta} \log(P_{\theta}(\tau^{(i)}))
\quad \text{(monte carlo)}
\end{aligned}
$$

Substitute concrete expression
$$
\begin{aligned}
\nabla_{\theta} \log P_{\theta}(\tau) &= \nabla_{\theta} 
\left(
\log P(s_0) +
\sum_{t=0}^{T-1} \log \pi_{\theta}(a_t|s_t) +  \log P(s_{t+1}|s_t, a_t)
\right) \\
&= \nabla_{\theta} \sum_{t=0}^{T-1} \log \pi_{\theta}(a_t|s_t)
\end{aligned}
$$
Then
$$
\begin{aligned}
\nabla_{\theta} U(\theta) &=
\mathop{E}\limits_{\tau \sim P_{\theta}(\tau)}
\left(
R(\tau) \nabla_{\theta} \sum_{t=0}^{T-1} \log \pi_{\theta}(a_t|s_t)
\right) \\
&= \frac{1}{N} \sum_i R(\tau^{(i)}) 
\nabla_{\theta} \sum_{t=0}^{T-1} \log \pi_{\theta}(a_t^{(i)}|s_t^{(i)})
\quad \text{(monte carlo)}
\end{aligned}
$$

### Summary of Policy Gradient Derivation

- Roll out trajectories $\tau^{(i)} \sim P_{\theta}(\cdot),\ i=1,\cdots,N$

- Compute the empirical mean $\hat{g} = \frac{1}{N} \sum_i R(\tau^{(i)}) 
  \nabla_{\theta} \sum_{t=0}^{T-1} \log \pi_{\theta}(a_t^{(i)}|s_t^{(i)})$

- By Monte Carlo, we know $E(\hat{g}) = \nabla_{\theta} U(\theta)$

- In practice, the sample mean estimate $\hat{g}$ has a high variance and many ways can be used to reduce the variance, leading to different algorithms.

## Value Estimation

### Algorithm: MC estimation, for estimating state values

#### Notation

For a finite trajectory $\tau = \{s_t, a_t, r_{t+1}\}_{t=0}^{T-1}$
$$
G_t = G(s_t) = R(\tau|S_0 = s_t) = r_{t+1}+ \gamma r_{t+2} + \cdots + \gamma^{T-1}r_T
$$
Corollary:
$$
G(s_t) = r_{t+1} + \gamma G(s_{t+1})
$$

#### Process 

- Input: policy $\pi$ to be evaluate
- Output: $V_{\pi}^{*}(s)$
- Init: 
  - $V(s) \in \mathbb{R},\ \forall s \in \mathbb{S}$  
  - an empty list $R(s),\ \forall s \in \mathbb{S}$  

---

Loop for each episode: (termination: $\max V_{\pi}^{[k+1]}(s_t) - V_{\pi}^{[k]}(s_t) \leq \Delta$)

​	generate $\tau = \{s_t, a_t, r_{t+1}\}_{t=0}^{T-1}$ using $\pi$

​	$G_t \leftarrow 0$

​	Loop for each time step $t = T-1, T-2, \cdots, 0$:

​		$G_t \leftarrow r_{t+1} + \gamma G_{t+1}$

​		$R(s_t)$ append $G_t$

$\hat{V_{\pi}}(s_t) \leftarrow \text{average}(R(s_t))$

---

Above is the **"every visit"** condition.

This calculates the value function for all possible states?

#### Examples

- [Frozen Lake]([Frozen Lake - Gym Documentation](https://www.gymlibrary.dev/environments/toy_text/frozen_lake/))

- [Example Code]([rl-start/notebook/value_estimation.ipynb at master · clearlab-sustech/rl-start](https://github.com/clearlab-sustech/rl-start/blob/master/notebook/value_estimation.ipynb))

#### Incremental Implementation

$$
\begin{equation}
V_{\pi}^{[m+1]}(s_t) = V_{\pi}^{[m]} + \frac{1}{m+1}
\left(
G_t^{[m+1]} - V_{\pi}^{[m]}(s_t)
\right)
\end{equation}
$$

New Estimation $\leftarrow$ Old Estimation + $\alpha$ (New Observation - Old Estimation)

This significantly reduces the storage requirements and makes the estimation real-time.

Derivation:


$$
\begin{aligned}
V_{\pi}^{[m+1]}(s_t) &= 
\frac{1}{m+1} \sum_{i=1}^{m+1} G_t^{[i]} \\
&= \frac{1}{m+1} \left( \sum_{i=1}^{m} G_t^{[i]} + G_t^{[m+1]}\right) \\
&= \frac{1}{m+1} \cdot m \cdot \frac{1}{m} \left( \sum_{i=1}^{m} G_t^{[i]} + G_t^{[m+1]}\right) \\
&= \frac{m}{m+1} V_{\pi}^{[m]}(s_t) + \frac{1}{m} G_t^{[m+1]}\\
&= \frac{1}{m+1} 
\left(
(m+1) V_{\pi}^{[m]}(s_t) - V_{\pi}^{[m]}(s_t) + G_t^{[m+1]}
\right) \\
&= V_{\pi}^{[m]}(s_t) + 
\frac{1}{m} \left( G_t^{[m+1]} - V_{\pi}^{[m]}(s_t) \right)
\end{aligned}
$$
