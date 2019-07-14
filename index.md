
# Introduction
We study the fluctuations around the interface formed by competitive erosion on a cylinder.
The problem was studied by xyz and some of the main results used in this article are...

## General Definition of competitive erosion on a graph

## Background for key results from the conformal map paper and limit shape theorem
### Interface for general simply connected domain is conformally invariant
#### Show the simulations here

### The interface on the cylinder domain converges quickly to a known the line
#### Show the simulations for various N

# Our main results
We consider competitive erosion on a cylinder. We find the following correlation function for a continuous interface with interface height $$h(x)$$ at two points $$x$$ and $$x'$$ is given by
$$
\begin{align*}
\Sigma(x, x') = \frac{1}{4 \pi n^2} \log( 2 - 2 \cos(x-x')).
\end{align*}
$$

The above correlation function [ADD EQUATION LABELS] indicates that the distribution of the fluctuations can be expressed by a gaussian distribution.

To do so, we want to find the stationary distribution of the markov chain for competitive erosion on a cylinder.
In the process we will find that we can formulate this process as the Ornstein Uhlenbeck (OH) equation which is a Gaussian process, a Markov process, and is temporally homogeneous. By showing that we can formulate it as the OH equation, we can directly use the results from the OH equation's general study.


## Fluctuations results (Gaussian free field)
### The boundary value problem
[We defined this earlier:
Assume that a simply connected red and blue region. Red region is $$R$$ and blue region is $$B$$. Interface from blue perspective if $$\partial B$$ and interface from red perspective is $$\partial R$$.]

The random walk of a blue particle initialized at the bottom boundary can be expressed as a markov chain with the following transition matrix $$P$$:

$$
P_{ij} =
\begin{cases}
      1 & i = j and i \in \partial B
      0 & i = j \\
      0 & i \in \partial B \\
      1/order(i) & i \sim j \\
      0 & else
   \end{cases}
$$

The particle is initially uniformly distributed along the lower boundary of $$B$$ and is represented by the vector:
$$w_i = \begin{cases}
      1/N & i.y = 0 \\
      0 & else  \\
   \end{cases}
$$

Now, let $$v = (x', h(x'))$$, and let $$Q$$ be the matrix without the contributions from the interface,

$$
\begin{align*}
\mathbb{P}[v \ before \ anywhere \ else \ on \ interface] &= \sum_{t - neighbors of v} 1/4 \sum_{i=0}^{\infty} (Q^i w)_ t \\
\end{align*}
$$

We can reformulate this as a boundary value problem for $$g: V \rightarrow \mathbb{R}$$ such that for $$v \in \partial B$$ $$g(v) = \mathbb{P}[v \ before \ anywhere \ else \ on \ interface]$$.

For $$v \in \partial B$$ we have $$(I - P) w = 0$$ however
$$
\begin{align*}
\Delta v &= v - 1/4 (v_{below} + v_{left} + v_{right} + v_{up}) \\
\end{align*}
$$

For the bottom boundary we have $$v \in Bottom$$ letting $$d_n v = 1/N$$:
$$
\begin{align*}
(I - P) v &= 1/N + v - 1/3 (v_{left} + v_{right} + v_{up}) \\
      &= v - 1/4 (v_{below} + v_{left} + v_{right} + v_{up}) \\
      &= \Delta v
\end{align*}
$$
which means we extended the bottom boundary.

#### Adding small Perturbations
#### Integral Kernel
### Introduce Poisson Process
### Set up Stochastic Diff Equations
### Deduce Ornstein Uhlenbeck Process
#### Use the OH results to deduce stationary distribution and covariance

#  Some more interesting/fun simulations of different domains
