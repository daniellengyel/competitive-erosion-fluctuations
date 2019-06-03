

# Introduction
We study the fluctuations around the interface formed by competitive erosion on a cylinder.
The problem was studied by xyz and some of the main results used in this article are...

## Definition  
Competitive erosion is... Represented as a MC.

Consider the following probabilistic model. Let $n$ be a positive integer. Take the cylindrical graph $$\text{Cyl}_n$$ with vertices $$(\frac{1}{n} \Z) / \Z \times \frac{1}{n} \Z \cap [0, 1]$$, and with edges connecting adjacent lattice points, and suppose that we have two probability measures $\mu_1$ and $\mu_2$ on the vertex set. Initialize a $S(0)$ to be some subset of the vertices of size $k$. We will define a Markov chain on subsets $S$ of size $k$. To get to $S(t + 1)$ from $S(t)$, pick a vertex from $\mu_1$ and have it take a simple random walk in the graph until it reaches $S(t)^c$, and call the vertex where it stops $X_t$. Then pick a square from $\mu_2$ and walk it until it reaches $S(t) \cup \{ X_t \}$, and call the vertex where it ends up $Y_t$. Then set
$$S(t+1) = (S(t) \cup X_t) \setminus Y_t \;\;.$$ 
In other words, if we think of $S(t)$ as the blue squares and $S(t)^c$ as the red squares, we do the following two steps to get to the next time step:
\begin{enumerate}
  \item  Initialize a point according to $\mu_1$ and random walk it until it hits a red square, then turn that square blue.
  \item Initialize a point according to $\mu_2$ and random walk it until it hits a blue square, then turn that square red.
\end{enumerate}

## Background for key results from the conformal map paper and limit shape theorem
Here we introduce the limit shape and conformal map results and support them with simulations.

# Our main results
Brief description of our result (could potentially be put in the introduction as well)

## Fluctuations results (Gaussian free field)
here we plot our results and do the math

#  Some more interesting/fun simulations of different domains
