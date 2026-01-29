### Conjugate Gradient
- CG is used to solve the linear system
$$Ax = b$$
- The above is equivalent to the following minimisation problem (recalling the form of the OLS estimator):
$$min_x ~\phi(x) := \frac{1}{2}x^TAx - b^T x$$
- At the algorithm level, the key difference between the conjugate gradient and the gradient descent method is the choice of the search direction. In gradient descent, the line search direction is the gradient descent direction $-r_k$. The conjugate gradient method uses a descent direction $p_k$ such that $<p_k, p_{k-1}>_A = 0$.
- A set of nonzero vectors $\{p_0, p_1, ..., p_k \}$ is said to be conjugate with respect to the positive semi definite matrix $A$ if 
$$p_i^TAp_j = 0 $$
	for all $i \ne j$.   
- A point $x^* \in \{x : x = x_0 + span\{p_0, p_1, ..., p_k\} \}$ minimises 
$$\phi(x) = \frac{1}{2}x^T Ax - b^Tx$$
	if and only if
	$$r(x^*)p_i = 0$$
	for all $i = 0,1,...,k$

### Proximal Gradient
- Line search algorithms typically assume that the objective function is continuously differentiable. The proximal gradient method is applied to non-differentiable objective function.
- Proximal gradient method is to solve the optimisation problems of the following form
$$min_x \{F(x) = f(x) + g(x) : x \in \mathbf{R}^n\}$$
	where $f(x)$ is continuously differentiable and $g(x)$, can be non-differentiable nut must be proximal.
- The proximal operator is defined as:
$$Prox_{\gamma ~g}(z) := argmin_x ~g(x) + \frac{1}{2\gamma}||x - z||^2$$
- A proximal function is a function that has closed form proximal operator.

### ADMM
- The alternating direction of multipliers is designed to solve convex optimisation problems by breaking them into smaller pieces.

### Sparse Inverse Problems
- **Definition**: A sparse signal is the one which contains only a small number of non-zero elements compared to its dimension.
- **Sparse Inverse Problem:** Given the observation $y$ and the matrix $A$, try to find a sparse $x$ such that $y \approx Ax$.
- Normal optimisation techniques cannot be applied to solve the sparse inverse problems. This is because $\ell_0$ pseudo-norm is neither continuous/differentiable nor convex. The gradient descent approach cannot be directly applied, and there might be many local minimisers.  
- We define the indicator function:
$$\delta(x) = \{_{0~~{if~x = true }}^{+\infty~~if~x=false}$$
### Greedy Algorithms - OMP
- We solve the difficult problem
$$min_{x} ~\delta(||x||_0  \leq S) + \frac{1}{2}||y-Ax||^2$$
	by solving the sequence of easier problems:
	$$min_{x} ~\delta(||x||_0  \leq 1) + \frac{1}{2}||y-Ax||^2$$

### Other Greedy Algorithms:
- If:
	- The columns of A are normalised.
	- Columns A are near orthogonal.
	then $A^Ty = A^TAx \approx Ix$. We then try to solve:
	$$min_{x} ~\delta(||x||_0  \leq S) + \frac{1}{2}||y-Ax||^2$$
- In OMP:
	- One index is added per iteration.
	- Analysis is based on near orthogonality of column pairs.
- In Others:
	- Multiple indices are updated per iteration.
	- Analysis is based on near orthogonality of sub-matrices.
- The hard thresholding function sets all but the largest $S$ elements to 0.

### Lasso
- One popular approach to solve the sparse linear inverse problem is to replace the nonconvex objective function $\ell_0$ with the convex $\ell_1$ norm,
- The LASSO problem:
$$min_x \frac{1}{2}||y-Ax||_2^2 + \lambda ||x||_1$$
	The $\ell_1$ norm promotes sparsity.
- The main difficulty in solving LASSO is that the objective function is not differentiable. This means that gradient descent methods cannot be directly applied.