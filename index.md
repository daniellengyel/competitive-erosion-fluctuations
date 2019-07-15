
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

We define a function $$g: B \cup \partial B \rightarrow \mathbb{R}$$ by the following boundary value problem:

$$
\begin{align*}
     g(v) &= 0 \ for \ v  \in \partial B \\
     \Delta g(v) &= 0 \ for \ v \in B \\
     d_n g(v) &= 1/n \ for \ v \in B \ s.t. \  v.y = 0
\end{align*}
$$

We now show that the function which satisfies these conditions has the property that for $$v \in \partial B$$ $$d_n g(v) = \mathbb{P}[v \ before \ \partial B \setminus \{v\}]$$ [should be true by uniqueness?].

The random walk of a blue particle initialized at the bottom boundary can be expressed by a markov chain with the following transition matrix $$P$$ ($$i, j \in B \cup \partial B$$):

$$
P_{ij} =
\begin{cases}
      1 & i = j \ and \ i \in \partial B
      0 & i = j \\
      0 & i \in \partial B \\
      1/order(i) & i \sim j \\
      0 & else
   \end{cases}
$$

Since the particle is initialized following a uniform distribution along the lower boundary of $$B$$ we represent the initial state of the markov state by the vector $$w \in \mathbb{R}^{|B \cup  \partial B|}$$:

$$w_i = \begin{cases}
      1/N & i.y = 0 \\
      0 & else  \\
   \end{cases}
$$

We now find the expected number of times we reach $$v \in \partial B$$ starting at $$w$$. To reach $$v$$ the markov chain has to reach one of the neighbors of $$v$$.
The probability that the markov chain reaches a neighbor $$a$$ of $$v$$ starting from $$w$$ in $$k$$ steps is $$(w_{-}^t Q^k)_ a$$ where $$Q$$ is the transition matrix $$P$$ and $$w_{-}$$ is $$w$$ without the entries corresponding to $$\partial B$$ squares.


$$
\begin{align*}
\mathbb{E}[v \in \partial B entries] &= \sum_{t \sim v} 1/4 \sum_{i=0}^{\infty} (w^t Q^i)_ t \\
\end{align*}
$$

since the expected number of entries into the interface is 1 we have:

$$
\begin{align*}
\mathbb{E}[v \in \partial B \ entries] &= \mathbb{P}[v \ before \ \partial B \setminus \{v\}] \\
\end{align*}
$$

We now define $$\phi: \partial B \cup B \rightarrow \mathbb{R}$$ to be:

$$
\phi(v) = \begin{cases}
      0 & v \in \partial B \\
      -1/4 \sum_{i=0}^{\infty} (w_{-}^t Q^i)_ v & else
\end{cases}
$$

Note that for $$v \in \partial B$$:

$$
\begin{align*}
    d_n \phi(v) &= \sum_{t \sim v \ and t \in B} \phi(t) \\
    &= \mathbb{P}[v \ before \ \partial B \setminus \{v\}] \\
\end{align*}
$$
[is this how normal derivative works lol ]


[note: set g to be \delta w and argue that we extend the vector delta w by 0 and everything else accordingly. Then the probability will become the normal of g. Also, absorb the 1/4 in delta w ]
We now define a function $$g$$ which


For $$v \in B$$ and $$v \not \in B_{lower}$$ we have $$(I - P_{-}) \phi(v) = \Delta \phi(v) = w_{-}(v) = 0$$ and by definition of $$\phi$$ we have for $$v \in \partial B$$ $$\phi(v) = 0$$.
Lastly, for $$v \in B_{lower}$$ we also want $$\Delta \phi(v) = 0$$ which we get by:

$$
\begin{align*}
(I - P) \phi(v) &= \phi(v) - 1/3 (\phi(v_{left}) + \phi(v_{right}) + \phi(v_{up})) = w_{-}(v) = 1/N \\
\rightarrow   \Delta \phi(v) &=  3/4 (I - P) \phi(v) - \frac{3}{4N} = 0\\
by \ letting \ d_n \phi(v_{bottom}) &= -\frac{3}{4N} \\
\end{align*}
$$

#### Adding small Perturbations
#### Integral Kernel
### Introduce Poisson Process
### Set up Stochastic Diff Equations
### Deduce Ornstein Uhlenbeck Process
#### Use the OH results to deduce stationary distribution and covariance

#  Some more interesting/fun simulations of different domains
