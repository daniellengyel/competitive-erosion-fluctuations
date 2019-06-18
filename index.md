

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
(Assume that both that there is one simply connected red and blue region.
  Let $$B$$ be the region in which all squares are blue and $$\del B$$ be the interface -- i.e. the set of lowest red squares for every x-coordinate.)

Let $$h(x): \mathbb{Z} \rightarrow \mathbb{Z} $$ be the y-coordinate of the first red square for the given x-coordinate -- such a function will define the interface. We now want to find the probability that a randomly initialized particle will hit $$h(x')$$ before any other point on the interface.

We can view the random walk of the particle as a markov chain with the following transition matrix $$P$$ with the states being $$B \cup \del B$$:
$$
P_{ij} =
\begin{cases}
      0 & i = j \\
      0 & i, j \in \del B  \\
      1/order(i) & i \sim j  
   \end{cases}
$$



#### Adding small Perturbations
#### Integral Kernel
### Introduce Poisson Process
### Set up Stochastic Diff Equations
### Deduce Ornstein Uhlenbeck Process
#### Use the OH results to deduce stationary distribution and covariance

#  Some more interesting/fun simulations of different domains
