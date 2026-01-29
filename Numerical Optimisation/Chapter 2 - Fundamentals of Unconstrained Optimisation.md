In unconstrained optimisation, we minimise an objective function that depends on real variables, with no restrictions at all on the values of these variables. The mathematical formulation is:
$$\underset{x}{\min}f(x)$$
- Usually, we lack a global perspective on the function $f$. All we know are the values on $f$ and maybe some of its derivative at a set of points.

**What is a Solution?**
- We aim to find a global minimiser of $f$, a point where the function attains its least value.
- A point $x^*$ is a global minimiser if $f(x^*)\leq f(x)$ for all $x$. 
- The global minimiser can be difficult to find since our knowledge of $f$ is usually only local. Most algorithms are able to only find a local minimiser. 
- A point $x^*$ is a local minimiser if there is a neighbourhood $\mathcal N$ if $x^*$ such that $f(x^*)\leq f(x)$ for all $x \in \mathcal N$.
- FONC: 
	- If $x^*$ is a local minimiser and $f$ is continuously differentiable in an open neighbourhood of $x^*$, then $\nabla f(x^*) = 0$.
- SONC:
	- If $x^*$ is a local minimiser of $f$ and $\nabla^2 f$ exists and is continuous in an open neighbourhood of $x^*$, then $\nabla f(x^*) = 0$ and $\nabla^2f(x^*)$ is positive semidefinite.
- SOSC:
	-  If $x^*$ is a strict local minimiser of $f$ and $\nabla^2 f$ exists and is continuous in an open neighbourhood of $x^*$, then $\nabla f(x^*) = 0$ and $\nabla^2f(x^*)$ is positive definite.
- When $f$ is convex, any local minimiser $x^*$ is a global minimiser of $f$. 

**Algorithms:**
- All algorithms for unconstrained optimisation problems require the user to supply a starting point $x_0$.
- Optimisation problems start at a starting point and terminate when either no more progress can be made, or when it seems that a solution point has been approximated with sufficient accuracy.

**Line Search:**
- In line search algorithms, the algorithm chooses a direction $p_k$ and searches along this direction from the current iterate $x_k$ for a new iterate with a lower function value. The distance to move along $p_k$ can be found by approximately solving the 1D minimisation problem to find step length $\alpha$.
$$\underset{\alpha > 0}{\min}f(x_k+\alpha p_k)$$
- In general, algorithms, generate a limited number of trial step lengths until it finds one that loosely approximates the minimum.
- Line search methods work by fixing the direction $p_k$ and then finding a appropriate step length $\alpha_k$. 
- The steepest descent direction $-\nabla f_k$ is the most obvious choice for search directions for a line search method.
- Another important search direction is the Newton direction which is derived from the second-order Taylor series approximation to $f(x_k +p)$.
- The newton direction is obtained by finding the vector that $p$ that minimises $m_k(p)$. By setting the derivative $m_k(t)$ to zero, we obtain the following explicit formula.
$$p_k^N = -(\nabla^2 f_k)^{-1}\nabla f_k$$
- The newton direction is reliable when the difference between the true function $f(x_k + p)$ and its quadratic model $m_k(p)$ is not too large.
- The Newton direction can be used in a line search method when $\nabla^2 f_k$ is positive definite.
- The natural step size for Newton methods is a unit step size $\alpha = 1$. The drawback of the Newton method is the need for the Hessian which can be expensive to compute.
- Quasi-Newton search methods do not require the computation of the Hessian, instead using an approximation.