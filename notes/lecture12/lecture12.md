# Lecture12: Value Estimation

> Notes taken by [squarezhong](https://github.com/squarezhong)
> Repo address: [squarezhong/SDM5008-Lecture-Notes](https://github.com/squarezhong/SDM5008-Lecture-Notes)

[toc]

## Algorithm: MC estimation, for estimating state values

### Notation

For a finite trajectory $\tau = \{s_t, a_t, r_{t+1}\}_{t=0}^{T-1}$
$$
G_t = G(s_t) = R(\tau|S_0 = s_t) = r_{t+1}+ \gamma r_{t+2} + \cdots + \gamma^{T-1}r_T
$$
Corollary:
$$
G(s_t) = r_{t+1} + \gamma G(s_{t+1})
$$

### Process 

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

### Examples

- [Frozen Lake]([Frozen Lake - Gym Documentation](https://www.gymlibrary.dev/environments/toy_text/frozen_lake/))

- [Example Code]([rl-start/notebook/value_estimation.ipynb at master · clearlab-sustech/rl-start](https://github.com/clearlab-sustech/rl-start/blob/master/notebook/value_estimation.ipynb))

### Incremental Implementation

$$
\begin{equation}
V_{\pi}^{[m+1]}(s_t) = V_{\pi}^{[m]} + \frac{1}{m+1}
\left(
G_t^{[m+1]} - V_{\pi}^{[m]}(s_t)
\right)
\end{equation}
$$

New Estimation $\leftarrow$ Old Estimation + $\alpha$ (New Observation - Old Estimation)

This significantly reduces the storage requirements.

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
\frac{1}{m+1} \left( G_t^{[m+1]} - V_{\pi}^{[m]}(s_t) \right)
\end{aligned}
$$

## From Monte-Carlo (MC) to Temporal Difference (TD)

- Limitation of MC methods: require finished episodes

- TD: $G_t \approx r_{t+1} + \gamma \hat{V}_{\pi}(s_{t+1})$, applies if some applications have very long episodes

$$
V_{\pi}^{[m+1]}(s_t) = V_{\pi}^{[m]}(s_t) + \alpha
\left(
\underbrace{r_{t+1}^{[m+1]} + \gamma \hat{V}_{\pi}(s_{t+1})}_{\text{TD Target}}
- V_{\pi}^{[m]}(s_t)
\right)
$$

The right side of $\alpha$ is call **TD Error**

### TD with $n$-step returns

- 1-step TD: $G_t \approx r_{t+1} + \gamma \hat{V}_{\pi}(s_{t+1})$

- 2-step TD: $G_t \approx r_{t+1} + \gamma r_{t+2} + \gamma^2 \hat{V}_{\pi}(s_{t+2})$

- n-step TD: $G_t \approx r_{t+1} + \gamma r_{t+2} + \cdots + \gamma^{n-1}r_{t+n} + \gamma^n\hat{V}_{\pi}(s_{t+n})$
- Monte Carlo methods could be considered as $\infty$-step TD methods.

### Rules for action-values

- MC: $Q_{\pi}^{[m+1]}(s_t,a_t) = \frac{1}{m+1} \sum_{i=1}^{m+1} G_t^{[i]}$
- MC-incremental: $Q_{\pi}^{[m+1]}(s_t, a_t) = Q_{\pi}^{[m]}(s_t,a_t) + \frac{1}{m+1}(A_t^{[m+1]} - Q_{\pi}^{[m]}(s_t,a_t))$
- $n$-step TD: $G_t \approx r_{t+1} + \cdots + \gamma^{n-1} r_{t+n} + \gamma^n\hat{Q_{\pi}}(s_{t+n},a_{t+n})$

### Trade-off between bias and variance: 

- MC methods: unbiased, high variance
- TD methods: biased, low variance
- $n$-step TD methods: the choice of $n$ serves as a **trade-off** between bias and variance in value estimation

### $\lambda$-return

Another method to trade off between the bias and variance of the estimator. Empirically better than fixed $n$-step return.

#### $TD(\lambda)$ algorithm

Estimating the value functions using the  TD method computed with the $\lambda$-return.

