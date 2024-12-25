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

  - Policy gradient use $1^{st}$ order gradient ascend method

## Derivation of Policy Gradient

