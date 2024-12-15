# Lecture9: probability Review for Reinforcement Learning

> Notes taken by [squarezhong](https://github.com/squarezhong)
> Repo address: [squarezhong/SDM5008-Lecture-Notes](https://github.com/squarezhong/SDM5008-Lecture-Notes)

[toc]

## Probability and Conditional Probability

### Probability

#### Definition

A formal way to quantify the uncertainty of our knowledge about the physical world.

#### Formalism: Probability Space $(\Omega,\mathcal{F},P)$

- $\Omega$ : **sampling space**: a set of all possible outcomes (maybe infinite)
- $\mathcal{F}$ : **event space**: collection of events of interest (event is a subset of $\Omega$)
- $P$ : $\mathcal{F} \rightarrow [0,1]$ **probability measure**: assign event in $\mathcal{F}$ to a real number between 0 and 1.

#### Axioms of Probability

- $P(A) \geq 0$
- $P(\Omega) = 1$
- $A \cap B = 0 \Rightarrow P(A \cup B) = P(A) + P(B)$

#### Important consequences

- $P(\emptyset) = 0$
- Law of total probability: $P(B) = \sum_i^{n}P(B\cap A_i)$ for any partitions $\{A_i\}$ of $\Omega$
  - A collection of sets $A_1, \cdots, A_n$ is called a partition of $\Omega$ if
    - $A_i \cap A_j = \emptyset$, for all $i \neq j$
    - $A_1 \cup A_2 \cdots \cup A_n = \Omega$

### Conditional Probability

#### Definition

$$
P(A|B) \triangleq \frac{P(A\cap B)}{P(B)}
$$

- $(\Omega,\mathcal{F},P) \rightarrow (\tilde{\Omega},\tilde{\mathcal{F}},\tilde{P)}$
- $\tilde{\Omega} = B$
- $\tilde{\mathcal{F}}$ = all subsets of $B$

#### Bayes rule

$$
P(A|B) = \frac{P(A|B)P(A)}{P(B)}
$$

#### Independent

$A$ and $B$ are called (statistically) independent if

- $P(A|B) = P(A)$ or $P(A\cap B) = P(A)P(B)$



## Random Variables and Random Vectors

### Deterministic variable and random variable

- $z$ is a **deterministic variable** (single-valued variable), which means $z$ can take only one value that may or may not be known
- $z$ is a **random variable** (multi-valued variable), which means $z$ can take multiple (even infinite) possible values, each value occurs with certain probability

### probability measure

- Discrete random variable: **probability mass function** (pmf)
- Continuous random variable: **probability  density function** (pdf)



#### Random vector

- n-dimensional random vector $X = \begin{bmatrix} X_1 \\ X_2 \\ \vdots \\ X_n \end{bmatrix}$
- density function $f(x) ,x \in R^{n}$
- probability evaluation: $P(X\in A) = \int_A f(x)dx$

#### Expectation of a random vector $X \in R^{n}$

- Continuous: $E(X) = \triangleq \int_{R^n} x f(x) dx$
- Discrete: $E(X) = \sum_x x \cdot \text{Prob}(X=x)$
- $E(X) = \begin{bmatrix} E(X_1) \\ E(X_2) \\ \vdots \\ E(X_n) \end{bmatrix}$

#### Linearity of Expection:

Expection of $AX$ with deterministic constant $A \in R^{m \times n}$

- $E(AX) = AE(X)$
- $E(AX+BY) = AE(X) + BE(Y)$

## Jointly Distributed Random Vectors and Conditional Expectation

Jointly distributed random vectors: $X \in R^{n}, Y \in R^{m}$

- Joint density function: $(X,Y) \sim f_{XY}(x,y)$

- Marginal density: $X \sim f_X(x), Y \sim f_Y(y)$

  $f_X(x) = \int_{R^{m}}f_{XY}(x,y)dy, f_Y(y) = \int_{R^n}f_XY(x,y)dx$ 



#### Conditional probability

$$
p_{X|Y}(X=i|Y=j) = \frac{p_{XY}(X=i,Y=j)}{\sum_i p_{XY}(X=i,Y=j)} \\
f_{X|Y}(x|y) = \frac{f_{XY}(x,y)}{f_Y(y)}
$$

#### Law of total probability

- $f_X(x)=\int_{R^m}f_{X|Y}(x|y) f_Y(y) dy$
- $f_Y(y)=\int_{R^n}f_{Y|X}(y|x) f_X(x) dx$

#### Independent 

$X$ is independent to $Y$, denoted by $X \bot Y$ **iff** $f_{XY}(x,y)=f_X(x) f_Y(y)$

#### Conditional expectation

- Continuous: $E(X|Y = y) = \int_{R^n} x f_{X|Y}(x|y) dx$
- Discrete: $E(X|Y = y) = \sum_i i \cdot \text{Prob}(X=i|Y=y)$

- $E(X) = \sum_y E(X|Y=y) \cdot p_Y(Y=y)$
- $E(g(X,Y)) = \sum_y E(g(X,Y)|Y=y) \cdot p_Y(Y=y)$

