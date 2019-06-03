# Hello World
## Introduction
## Simulations
<iframe width="525" height="525" seamless="seamless" frameBorder="0" scrolling="no" src="visualization/CompEros2.html"></iframe>

{% raw %}
  $$a^2 + b^2 = c^2$$ --> note that all equations between these tags will not need escaping! 
 {% endraw %}

# Introduction

# Set up
Consider the following probabilistic model. Let $n$ be a positive integer. Take the cylindrical graph $\text{Cyl}_n$ with vertices $(\frac{1}{n} \Z) / \Z \times \frac{1}{n} \Z \cap [0, 1]$, and with edges connecting adjacent lattice points, and suppose that we have two probability measures $\mu_1$ and $\mu_2$ on the vertex set. Initialize a $S(0)$ to be some subset of the vertices of size $k$. We will define a Markov chain on subsets $S$ of size $k$. To get to $S(t + 1)$ from $S(t)$, pick a vertex from $\mu_1$ and have it take a simple random walk in the graph until it reaches $S(t)^c$, and call the vertex where it stops $X_t$. Then pick a square from $\mu_2$ and walk it until it reaches $S(t) \cup \{ X_t \}$, and call the vertex where it ends up $Y_t$. Then set
$$S(t+1) = (S(t) \cup X_t) \setminus Y_t \;\;.$$
In other words, if we think of $S(t)$ as the blue squares and $S(t)^c$ as the red squares, we do the following two steps to get to the next time step:
\begin{enumerate}
  \item  Initialize a point according to $\mu_1$ and random walk it until it hits a red square, then turn that square blue.
  \item Initialize a point according to $\mu_2$ and random walk it until it hits a blue square, then turn that square red.
\end{enumerate}

It is proven in \cite{GLPP} that if we take $n$ very large and the measures $\mu_1$ and $\mu_2$ are taken to be uniform along the lower and upper bases of the cylinder, respectively, then as $n \rightarrow \infty$ we see a deterministic macroscopic boundary, or interface, form between the set $S(t)$ and $S(t)^c$ if we randomly sample from the stationary distribution $\pi_n$. In particular, if $|S(t)| = \alpha n^2$, then with probability $\rightarrow 1$, this interface is very close to the flat line $y = \alpha$, with fluctuations occurring at scale smaller than $n$. In the literature on 2d interface growth models similar to this one, this deterministic macroscopic boundary would be called an \textbf{limit shape}. We do not give a rigorous definition of this phenomenon in this note. Limit shapes occur in many models similar to this one, such as tiling models, dimer models (probability measures on the set of perfect matchings on a bipartite graph), and the vertex models, and the study of these phenomena originates from the field of statistical mechanics. See \cite{K} for an overview of these phenomena in the case of dimer models, and see \cite{C} and \cite{BG} for a general overview of modern progress in the field.

Our \textbf{main goal} in this note is twofold: On the one hand, we simulate the Markov Chain in order to approximately sample from its stationary distribution, and we present numerical results and conjectures regarding the exact scale of the fluctuations. On the other hand, we describe a heuristic analytical analysis of the fluctuations, and ultimately arrive at the following
\begin{conjecture}
As $n \rightarrow \infty$, the correlation function of the interface height $h(x)$ at two points $x$ and $x'$ is given by
\begin{align*}
\Sigma(x, x') = \frac{1}{4 \pi n^2} \log( 2 - 2 \cos(x-x'))  \;\;.
\end{align*}
\end{conjecture}
It follows from this that the fluctuations of the interface occur at scale $\frac{1}{n}$. Furthermore, the above operator is inverse to a Dirichlet to Neumann operator, and since this operator is conformally invariant, it implies that at leading order the fluctuations are conformally invariant, which is beautiful as it has already been proven in \cite{GP} that the limit shape is conformally invariant.


We present some standard definitions to begin. Suppose we have a finite graph $G = (V, E)$.
Define the Laplacian as the linear operator $\Delta$ on functions $f : V \rightarrow \R$ defined by
$$(\Delta f)(v) = \sum_{w \sim v} f(v) - f(w) = \deg(v) f(v) - \sum_{w \sim v} f(w)$$
where $v \in V$, and the sum is over vertices adjacent to $v$.
If $G$ is $r$-regular, then it is clear that $\Delta = r I - A$, where $A$ is the adjacency matrix of the graph and $I$ is the identity.

For a function $f$, the \textbf{discrete differential} of the function, denoted by $d f$, gives a \textbf{flow} on the edges $(v, w)$ defined by $df(v, w) = f(w) - f(v)$. A flow $\omega$ is a function on edges such that $\omega(v, w) = - \omega(w, v)$. If we have a flow $\omega$, denote the \textbf{divergence} of $\omega$ by
$$d^* \omega(v) \defeq \sum_{w \sim v} \omega(v, w) \;\;.$$
Note also that it follows from this that $d^* \circ d = - \Delta$.


# Limit Shape Theorem

\subsection{The Level Set Heuristic}
We present a simple and beautiful heuristic argument from \cite{GLPP}, which we have slightly altered, as this will be important for our calculations in later sections. Let us have a simply connected domain $D \subset \R^2$ with analytic boundary $\partial D$ (so that the boundary is preserved under conformal transformations). Suppose we split this region into a blue region $S_1$ and a red region $S_2$ separated by an interface $B$, so that $D = S_1 \sqcup S_2 \sqcup B$. Further suppose that we have two measures $\mu_1, \mu_2$ (probability density functions) whose supports are in $\partial D \cap S_1$ and $\partial D \cap S_2$ respectively. Then, consider the discrete boundary value problem of finding $g : \frac{1}{n}\Z^2 \cap D \rightarrow \R$ such that
\begin{align}
\begin{cases}
    & \Delta g = 0 \\
    & \frac{\partial}{\partial \nu} g = \mu_1 - \mu_2 \;\; \text{on the boundary } \partial D \;\;.
\end{cases}
    \label{eqn:pdeg}
\end{align}

Then, we can also define the mixed boundary value problems on $S_1$ and $S_2$, respectively by
\begin{align}
    & \begin{cases}
            \Delta g_1 = 0 \\
            g_1 = 0 \;\; \text{on } B \\
            \frac{\partial}{\partial \nu} g_1 = \mu_1 \;\; \text{on } S_1 \cap \partial D
            \label{eqn:g1}
    \end{cases} \\
    & \begin{cases}
            \Delta g_2 = 0 \\
            g_2 = 0 \;\; \text{on } B \\
            \frac{\partial}{\partial \nu} g_2 = \mu_2 \;\; \text{on } S_2 \cap \partial D
            \label{eqn:g2}
    \end{cases}
\end{align}

where in \eqref{eqn:g1} and \eqref{eqn:g2}, $g_1 : \frac{1}{n}\Z^2 \cap S_1 \rightarrow \R$ and $g_2 : \frac{1}{n}\Z^2 \cap S_2 \rightarrow \R$, respectively. Then, we can extend both $g_1$ and $g_2$ to be $0$ outside of their domains, and ultimately we have $\Delta (g - (g_1 - g_2)) = 0$ exactly everywhere in the interior of $S_1$ or the interior of $S_2$. Further, in these regions both $g_1 - g_2$ and $g$ satisfy the same Neumann boundary condition on $\partial D$. Suppose one can further show that with the correct choice of interface $B$, we can justify the formula
$$\Delta(g - (g_1 - g_2)) (x) = 0 \;\;, x \in B \;\;.$$
Then, it should be true that $g = g_1 - g_2$ up to a constant.

The claim is that, if $B$ is the true limiting interface of competitive erosion, then for $x \in B$, $\Delta g (x) \approx \Delta(g_1-g_2)(x)$. Supposing one can do this, we then have that since $g_1 = g_2 = 0$ on the interface $B$, it must be the case that $g$ is constant on $B$. Since the interface is a level set of the greens function $g$, it must be conformally invariant, as the Greens function itself is conformally invariant. Furthermore, in any domain in which one could compute the greens function, whether via conformal mapping or otherwise, one could also compute the interface by finding some constant $K$ such that the fraction of lattice sites in the domain with $g(v) < K$ is approximately equal to $\alpha$ (the fraction of blue sites). The interface will be given by $g = K$.

Now we attempt to give heuristic justification of the formula
\begin{equation}
\Delta(g_1-g_2)(x) \approx 0
\label{eqn:int}
\end{equation}
for $x \in B$, if $B$ is the true interface. Let $\p_{\mu_i}$ be the probability measure on random walks that start according to $\mu_i$ and are absorbed when first entering $B$. Now define $\omega$ as a flow on the blue sub-graph (the portion of the lattice in $S_1$) as follows. For any edge $(v, w)$ away from the boundary (oriented in the positive $x$ or $y$ direction), let
\begin{align*}
\omega (v, w) &= \p_{\mu_1}( \text{the walk cross the edge from $v \rightarrow w$} ) \\
& \;\;\;\;\; - \p_{\mu_1}( \text{the walk will cross the edge from $w \rightarrow v$} ) \;\;.
\end{align*}
Note that since $d^* \omega = 0$ on the interior of $S_1$ (because the net frequency of a random walk's flow through a vertex on the interior of the graph is $0$) and since $\omega$ satisfies the correct boundary conditions, if one can find a function $f$ on the blue vertices such that $d f = \omega$ and $f = 0$ on $B$, then one has $f = g_1$. Further, it is in fact true that the true $g_1$ will satisfy $d g_1 = \omega$. In other words, $g_1$ will be the potential function of the flow $\omega$. Now on the interface, $\Delta g_1 (x) \approx \omega(x, x - \frac{1}{n} e_i)$ (where $i$ is either $1$ or $2$). Furthermore, if $B$ is the true interface, it should be true that for $x \in B$, the probability of a red walk hitting $x$ is roughly equal to the probability of a blue walk hitting $x$. Therefore, we have that $-\Delta g_1 \approx - \Delta g_2$ on the interface, so that we have approximately, $\Delta (g_1 - g_2) = 0$, which implies \eqref{eqn:int}.

\section{Attempt at Analytic Proof of GFF/Ornstein–Uhlenbeck Fluctuations}

\subsection{Small perturbations}
Consider the PDE \eqref{eqn:g1} in the case of the cylinder. On the lattice approximating the cylinder, we hope to solve the following discrete boundary value problem in the region of blue vertices:
\begin{align*} \label{discrete:1}
    g_1 : \Cyl_n \cap \{(x, y) : y \leq h(x)\} \rightarrow \R \\
    \Delta g_1(x,y) = 0 \\
    g_1 (x,h(x)) = 0\\
    d g_1 (x,y) |_{y = 0} = \mu = 1/n
\end{align*}

where $d f$ denotes the discrete differential of a function $f$ on the lattice sites, and by $d g_1 (x,y) |_{y = 0}$, we mean $d g_1$ restricted to the (vertical) edges from the lower boundary of the cylinder. Also, $h(x)$ is defined to be the first red site with horizontal coordinate $x$. From here on (for consistency) define $S_1 = \{(x, y) : y \leq h(x)\}$, and let $B = \text{graph}(h)$ be the interface.


Suppose that $h(x)$ is obtained by sampling some smooth function in the lattice points on the unit circle, which we also call $h$ by abuse of notation. Further, assume that $g_1$ is also approximately obtained by sampling a smooth function
\begin{align*}
    f : \R / \Z \times [0, 1] \cap S_1 \rightarrow \R \;\;.
\end{align*}


Now assume that $n$ is large, and that there is a well defined interface which is near the limit shape. In other words, assume that
$$ h(x) = 1/2 + \delta h(x)$$
where $\delta h(x)$ is a small variation. Then, we look for a solution of the form
\begin{align*}
    f = f_0 + \delta f
\end{align*}
where $\delta f$ is some (hopefully small) function, and $f_0$ is the solution obtained from solving the problem with the flat interface $h = h_0 \equiv 1/2$. Note that in this case $f_0(x, y) = y - \frac{1}{2}$, as this solves the boundary value problem exactly with $h = h_0$.

Now we plug $f =  f_0 + \delta f$ into the boundary value problem, and see what PDE we obtain for $\delta f$. The first and third conditions become $\Delta \delta f = 0$ and $\partial_y \delta f = 0$, respectively. If we taylor expand around $h_0$ (recall we are now dealing with smooth functions), the second condition becomes
\begin{align*}
0 &=f_0(x,h(x)) + \delta f (x,h(x)) \\
&= f_0(x,h_0) + \delta h \partial_y f_0(x, h_0) + \delta f (x,h_0) + O(\delta h \partial_y \delta f) \\
&\approx \delta h \partial_y f_0(x, h_0) + \delta f (x,h_0)
\end{align*}
where here we assume $O(\delta h \partial_y \delta f)$ is in fact negligible. We know that $\partial_y f_0(x, h_0) = 1$ by the explicit formula. So ultimately we get the mixed boundary condition pde:
\begin{align*}
    \Delta \delta f &= 0 \\
     \delta f(x, h_0) &= - \delta h(x) \\
    d( \delta f ) |_{y = 0} &= 0 \;\;.
\end{align*}

Now, it is possible to find some family of solutions (a matrix) $R(x, y, x')$ such that $R(x, h_0, x') = -\delta_{x, x'}$ (we simply replace the second boundary condition with the dirac delta function). Then, we have
\begin{align}
    \delta f(x,y) = \sum_{x' \in C_n} R(x, y,x') \; \delta h(x') \;\;.
    \label{eqn:6}
\end{align}
Further, it is reasonable to assume that as $n \rightarrow \infty$, $R$ will converge to some integral kernel $\tilde{R}$, such that $\tilde{R}(x, h_0, x') = \delta(x - x')$ (here we mean the dirac-delta), and for a function $\varphi$,
$$\sum_{x' \in C_n} R(x, y,x') \; \varphi(x') \approx n \int_{S^1} \tilde{R}(x,y,x') \; \varphi(x') \; dx'\;\;.$$
The discrete differential in the normal direction, $d_\nu$, converges to $\frac{1}{n} \partial_\nu$, where $\partial_\nu$ is the continuum normal derivative. So therefore, we ultimately get  $$\sum_{x' \in C_n} d_\nu R(x, h(x),x') \; \varphi(x') \approx  \int_{S^1}\partial_\nu \tilde{R}(x,h(x),x') \; \varphi(x') \; dx'\;\;.$$
From here on we will drop the tilde and assume $R$ is simple the integral kernel.

Now recall our interpretation of $f$. It should be the case that $d_\nu f|_{B}$ is the probability density function of where the random walk ends. So now, for a single blue step of the chain, $ \delta h $ satisfies the recurrence relation
\begin{align*}
    \p[\delta h(x) \rightarrow \delta h(x) + \frac{1}{n} ] &\approx 1/n + \int_{S^1} \partial_\nu R(x,h(x),x') \; \delta h(x') \; dx' \\
    &\approx 1/n + \int_{S^1} \partial_\nu R(x,h_0,x') \; \delta h(x') \; dx'
\end{align*}
for $x \in \frac{1}{n}\Z / \Z$, where again here we have used a first order approximation by evaluating the integral kernel at $h_0$, based on our assumption that $\delta h$ is small. Note that we can, in the exact same way, carry out this argument for the PDE \eqref{eqn:g2} (except we will need a minus sign next to the second term because the orientation will be different) and obtain an approximation for the density of where the red random walk will land. We have over the course of one red step in the chain,
\begin{align*}
    \p[\delta h(x) \rightarrow \delta h(x) - \frac{1}{n} ] &\approx 1/n - \int_{S^1} \partial_\nu R(x,h(x),x') \; \delta h(x') \; dx' \\
    &\approx 1/n -  \int_{S^1} \partial_\nu R(x,h_0,x') \; \delta h(x') \; dx' \;\;.
\end{align*}


\subsection{A new process}




Now we make a small diversion and meander around for a while to see where we end up. Let
\begin{align}
\lambda^{+}(x) &= 1/n + \int_{S^1} \partial_\nu R(x,h_0,x') \; \delta h(x') \; dx' \\
\lambda^{-}(x) &= 1/n - \int_{S^1} \partial_\nu R(x,h_0,x') \; \delta h(x') \; dx'
\end{align}
and consider a new, and related, continuous time model in which, $\forall x \in C_n$
\begin{align}
\delta h(x) &\rightarrow \delta h(x) + \frac{1}{n} \;\; \text{with rate } \lambda^{+}(x)  \\
\delta h(x) &\rightarrow \delta h(x) - \frac{1}{n} \;\; \text{with rate } \lambda^{-}(x) \;\;.
\end{align}

Recall that $n$ is large (so in particular $1/\sqrt{n}$ is small), and thus over a time span of $\sqrt{n}$, the interface $\delta h$ only changes by $O(\frac{1}{\sqrt{n}})$, which ultimately gives a negligible contribution to $\lambda^{\pm}$. Thus, we estimate the change over a time interval of $\sqrt{n}$ with the assumption that the $\lambda^{\pm}$ all stay constant over this time interval. By the central limit theorem, if $PP_\lambda$ is a Poisson point process on the real line, the number of points in the interval $[t, t + \Delta t]$ over long time intervals $\Delta t$ limit to Gaussian distributions with mean and variance $\lambda \Delta t$. We also have re-scaled our Poisson processes by $\frac{1}{n}$, and the time interval is $\sqrt{n}$, so the mean will be $\lambda \frac{1}{\sqrt{n}}$ and the variance will be $\lambda \frac{\sqrt{n}}{n^2} = \lambda \frac{1}{n^{3/2}}$. Thus, at some fixed $x$ coordinate (which we suppress to unclutter the calculation below) we have
\begin{align*}
   \delta h_{t+\sqrt{n}}-\delta h_{t} &= \N(\frac{1}{\sqrt{n}} \lambda^+,\frac{1}{n^{3/2}} \lambda^+) -   \N(\frac{1}{\sqrt{n}} \lambda^-,\frac{1}{n^{3/2}} \lambda^-)\\
    &= \frac{2}{\sqrt{n}} \int_{S^1} \partial_\nu R(x,h_0,x') \; \delta h(x') \; dx' + \N(0, \frac{1}{n^{3/2}} \lambda^+) - \mathcal{N}(0,\frac{1}{n^{3/2}} \lambda^-)
\end{align*}


If we make the coordinate change $t = \tau n$, then a timespan of $\sqrt{n}$ in units of $t$ is $\frac{1}{\sqrt{n}}$ in units of $\tau$. So if we consider the time-rescaled process $\phi_{\tau} = \delta h_{n \tau}$, and we formally set $d \tau =\frac{1}{\sqrt{n}}$, $d \phi_{\tau} = \phi_{\tau + \frac{1}{\sqrt{n}}} - \phi_{\tau}$, we get
\begin{align*}
    d \phi_{\tau}(x)
    &= \frac{2}{\sqrt{n}} \int_{S^1} \partial_\nu R(x,h_0,x') \; \phi_\tau (x') \; dx' + \sqrt{\frac{1}{n} \lambda^+} d W_\tau + \sqrt{\frac{1}{n}\lambda^-} d W_\tau \\
    &= 2 \int_{S^1} \partial_\nu R(x,h_0,x') \; \phi_\tau (x') \; dx' d \tau + \sqrt{\frac{1}{n} \lambda^+_n} d W_\tau + \sqrt{\frac{1}{n}\lambda^-_n} d W_\tau  \\
    &= 2 \int_{S^1} \partial_\nu R(x,h_0,x') \; \phi_\tau (x') \; dx' d \tau + \frac{1}{\sqrt{n}}\sqrt{\lambda^+_n + \lambda^-_n} d W_\tau \\
    &= 2 \int_{S^1} \partial_\nu R(x,h_0,x') \; \phi_\tau (x') \; dx' d \tau  + \frac{1}{n}\sqrt{2} d W_\tau
\end{align*}
where $W_\tau$ is the Weiner process. Recall that by the above we really mean the system of equations
\begin{equation}
   d \phi_{\tau}(x)
    = 2 \int_{S^1} \partial_\nu R(x,h_0,x') \; \phi_\tau (x') \; dx' d \tau + \frac{1}{n}\sqrt{2} d W_\tau
    \label{eqn:L}
\end{equation}
for $x = 0, 1/n, 2/n, \dots, (n-1)/n$, where each Weiner process $W_\tau$ is independent. Note also that the convolution with the kernel $\partial_\nu R$ is really approximating a matrix multiplication by an $n$ by $n$ matrix $D$. So if we re-write this process using a vector $\textbf{x}_\tau \in \R^n$ (zero indexed) defined by $\textbf{x}_\tau[i] = \phi_{\tau}(i / n)$, then we have
\begin{equation}
   d \textbf{x}_\tau
    = 2 D \textbf{x}_\tau d \tau + \frac{1}{n}\sqrt{2} d \textbf{W}_\tau
    \label{eqn:orn}
\end{equation}
where $\textbf{W}_\tau$ is an n-dimensional Weiner process (a vector $n$ of independent Weiner processes). This is exactly the $n$-dimensional version of the \textbf{Ornstein–Uhlenbeck process}. In the $n$-dimensional Ornstein–Uhlenbeck process with the above coefficients it is well known that the covariance matrix $\Sigma$ will be given by the relation
\begin{align*}
  D \Sigma + \Sigma D^T = \frac{1}{n^2}I
\end{align*}
and since for us the matrix $D$ turns out to be symmetric (we will see this in the next section), we have that
$\Sigma = \frac{1}{2 n^2}D^{-1}$.

\section{Checking the Result}
\subsection{Finding the kernel $\partial_\nu R$}
Recall that, as a continuum kernel, $R$ solves the boundary value problem
\begin{align*}
    \Delta_{(x, y)} R &= 0 \\
     R(x, h_0, x') &= \delta(x - x') \\
   \partial_\nu R |_{y = 0} &= 0 \;\;.
\end{align*}
Now recall that $R$ actually has physical meaning for our system (it should determine the correlations). Furthermore, our system is trivially invariant under shifts of the coordinates, so we can set our coordinates such that the interface $h_0$ is at $y = 0$. Furthermore, for large $n$, the system should be almost identical if we sent the bottom boundary of the cylinder to $- \infty$, since for large $n$ the probability density function for where the random walk last hits the line $y = -1/2$ before hitting the interface will tend to the uniform one over the lattice sites. Also, we can rescale the $x$-coordinate so that the cylinder becomes $\R / (2 \pi \Z)$.
Note that we can write
\begin{align*}
\delta(x-x') = \sum_{k=-\infty}^\infty e^{i k (x-x')}
\end{align*}
so the solution to the problem with this delta is
\begin{align*}
   R(x,y,x') = \sum_{k=-\infty}^\infty e^{i k (x-x')} (A e^{k y} + B e^{-k y} )
\end{align*}
where $A$ and $B$ will be determined by the boundary conditions. Thus, our boundary conditions give us
\begin{align*}
    A  + B  &= 1 \\
    A k e^{k y} + B k e^{-k y} |_{y=-\infty} &= 0 \;\;.
\end{align*}
Thus by the second equation, for positive $k$ we have $A = 1$, $B = 0$, and for $k \leq 0$ we have $A = 0$ and $B = 1$. So ultimately we arrive at the solution
\begin{align*}
R(x,y,x') = \sum_{k=-\infty}^\infty e^{i k (x-x')} e^{|k| y} \;\;.
\end{align*}
Note that the normal derivative of $R$, $\partial_y R|_{y=0}$ (the normal derivative is $\partial_y$ because the interface is now flat), is known in the context of physics as the Dirichlet to Neumann operator. We can now compute it in this case to be
\begin{align*}
\partial_y R(x,0,x') = \sum_{k=-\infty}^\infty e^{i k (x-x')} |k| \;\;.
\end{align*}
Thus, the functional inverse to the kernel $\partial_y R(x, h_0, x')$ is given by
\begin{align*}
L(x,x') = \sum_{k=-\infty}^\infty e^{i k (x-x')} \frac{1}{|k|}
\end{align*}
and one can check that this gives the function
\begin{align*}
L(x,x') = \log( 2 - 2 \cos(x-x')) \;\;.
\end{align*}
If we had not rescaled the $x$-axis and if we also kept track of a factor of $2 \pi$ when taking the normal derivative, and also a factor of $1/(2 n^2)$ for the covariance matrix, we would have obtained that
\begin{align*}
\Sigma(x,x') = \frac{1}{4 \pi n^2} \log( 2 - 2 \cos(x-x')) \;\;.
\end{align*}
In the next section we will present our comparison of this result with our numerical results.
