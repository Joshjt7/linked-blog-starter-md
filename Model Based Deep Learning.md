- A component of [[ML and DL techniques]].
- We often encounter inverse problems, where the goal is to recover a latent signal or image $x$, from a set of indirect and corrupt measurements $y$.
$$y=H(x) + n$$
where $H$ is the forward operator, representing a known physical distortion process and $n$ denotes additive noise.
- To find a meaningful solution, we must impose constraints on the desired signal $x$. This leads to a standard desired optimisation framework.
	1. Data Fidelity: The estimated signal $\hat{x}$ must be consistent with the observed measurements $y$. When processed by the forward operator $H$, it must be close to $y$.
	2. Prior Knowledge: The estimated signal $\hat{x}$ should conform to our prior belief about what constitutes a natural or valid signal
- The trade off can be formulated as a optimisation problem:
$$\hat{x}=argmin_{x}~ F(x,y) + \lambda R(x)$$
Where $F(x,y)$ represents the data fidelity term. It penalises inconsistencies between the prediction $D(x)$ and the measurement $y$. $R(x)$ is the regularisation term. It penalises solutions that do not conform to prior knowledge.

### Loop Unrolling
- We always start with the SAR forward model derived from the known physical model of the process.
$$s = Ta + n$$
	where s is the raw SAR data, T is the forward operator, $a$ is the reflectivity map we want to uncover and $n$ is the noise.
#### Deep Unfolding with IHT/IST
- Refer to [[Compressed Sensing#ML/DL|Unrolled Methods]].
- We can write iterative update steps:
	1. Gradient step:
	$$a_k^+ = a_k - \rho T^H(Ta_k -s)$$
	2. Proximal (shrinkage) step:
	$$a_{k+1} = argmin_a||a-a_k^+||_2^2 + \gamma ||a||_1$$
- We recall the objective function
$$f(a) = ||s - Ta||_2^2 + \gamma||a||_1$$
- The gradient of the data term is:
$$\nabla_a ||s-Ta||_2^2 = 2T^H(Ta-s)$$
	We often absorb the factor 2 into a step size.
- After the gradient step, we want to incorporate the $\ell_1$ penalty. 
- For IHT/IST algorithm, the parameters such as $\rho$ and $\gamma$ are very important to determine the iteration, convergence and image precision. This motivates a learnable version of the iterative algorithm
- We can write this in standard NN form. The $kth$ layer can be formulated as such
$$a_{k+1} = \Gamma(W_ka_k + b_k\gamma)$$
$$W_k = I - \rho T^HT$$
$$b_k = \rho T^H s$$
- In classical algorithms, our $W_k$ and $b_k$ are fixed by the known measurement operator $T$ and the step size $\rho$.
- In the unrolled network these are learnable parameters and are trained with data.

#### Deep Unrolling with ADMM
- Refer to [[Compressed Sensing#ADMM|ADMM Unrolled]].
- We are again solving the $\ell_1$ regularised CS problem for sparse coefficients.
$$f(a) = ||s - Ta||_2^2 + \gamma||a||_1$$
- ADMM is used to split the problem into simpler subproblems by introducing an auxiliary variable.
1. Split variable: $a = u$
	- Introduce $u$ such that:
	$$min_{a,u}~||s - Ta||_2^2 + \gamma||a||_1 ~~~~s.t.~a = u$$
	- ADMM solves this constrained problem by forming an augmented Lagrangian and alternating updates for $a,u$ and a dual variable $v$.
2. ADMM iterations:
	1. a-update (reconstruction/data fit):
	$$a_{k+1} = argmin_{a} ||s - Ta||_{2}^2 + \frac{\mu}{2}||a - \mu_k + v_k||_2^2$$
		solves a quadratic least squares problem balancing data fit and closeness to $u_k,v_k$.
	2. u-update (sparsity/denoising):
	$$u_{k+1} = argmin_{u} = \frac{\mu}{2}||a_{k+1} - u + v_k||_2^2 + \gamma||u||_1$$
		solves an $\ell_2 + \ell_1$ problem
	3. Dual / multiplier update:
	$$v_{k+1} = v_k + a_{k+1} - u_{k+1}$$
		update the dual variable to enforce consistency.
3. Closed-form updates:
	1. a-update:
		- Minimising the quadratic yields the linear system:
		$$a_{k+1} = (T^H T + \mu I)^{-1}(T^Hs + \mu(v_k - u_k))$$
		- This is the data reconstruction step. Combines information from the SARA data $s$, from the prior estimate and dual and then solved.
	2. u-update:
		- The solution is soft-thresholding:
		$$u_{k+1} = E(a_{k+1} + v+k, \frac{2\gamma}{\mu})$$
		- This is the denoising/sparsity enforcement step.
	3. v-update:
		- The dual update is:
		$$v_{k+1} = v_k + a_{k+1} - u_{k+1}$$
4. ADMM modules:
	- ADMM can be viewed as having a reconstruction module, denoising module and a update module.
5. Turning ADMM into a deep network:
	- In the same manner as IHT/IST, you can unroll $K$ ADMM iterations into $K$ layers of a network with each layer performing reconstruction, denoising and a dual update. 
	- $\mu, \gamma$ and any linear operators used in the reconstruction module become trainable parameters. 
	- The denoising step becomes a learned soft thresholding with learnable thresholds or a generic CNN denoiser.
---
### Synthetic Aperture Radar Imaging Meets Deep Unfolded Learning: A comprehensive review

### Imaging Modelling


### Papers

https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=10781458
[“SAR imaging based on deep unfolded network with approximated observation,”]
https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9277912
https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9869652
https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=10562772
https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9883406