- Each iteration of a line search method computes a search direction $p_k$ and then decides how far to move along that direction. The search direction often takes the form:
$$p_k = -B_k^{-1}\nabla f_k$$
	where $B_k$ is symmetric and non-singular matrix. In the steepest descent method, $B_k$ is simply the identity matrix $I$, while in Newtons method, $B_k$ is the exact Hessian. In quasi-Newton methods, $B_k$ is an approximation to the Hessian that is updated at every iteration.

**Step Length:**
- We want a step length $\alpha_k$ that gives a substantial reduction of $f$, but we do not want to spend too much time taking this decision.
- A popular inexact line search condition stipulates that $\alpha_k$ should first of all give sufficient decrease in the objective function $f$, as measured by the inequality:
$$f(x_k +\alpha p_k) \leq f(x_k) + c_1\alpha\nabla f_k^T p_k$$
	the reduction in $f$ should be proportional to both the step length $\alpha_k$ and the directional derivative $\nabla f_k^T p_k$. The inequality is sometimes called the Armijo conditions.
- We introduce another condition to ensure that the algorithm makes reasonable progress. To rule out unacceptably short steps, we introduce a second requirement, called the curvature conditions, which require $\alpha_k$ to satisfy.
$$\nabla f(x_k + \alpha_k p_k)^T p_k \ge c_2 \nabla f_k^T p_k$$
- The sufficient decrease and curvature conditions are known c