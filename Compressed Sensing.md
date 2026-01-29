### Fundamentals
- Refer to notes in [[Topics in Large Dimensional Data Processing]].
- Moving from a purely Fourier transform type processing paradigm to one that couples physics-motivated sensing with models with some form of sparsity-based priors.
- SAR image formation can be treated as a class of ill-posed inverse problems.
- CS theory tells us that it can precisely reconstruct a sparse or compressible signal from fewer measurements beyond Nyquist sampling with sparse technologies.
- Computational complexity is usually very large because an iterative solution is needed to find the optimal imaging result.
- There is a need for alternative methods of image formation. The desire for high resolution means wideband signals, long apertures giving many channels, many pulses and many frequencies. This means we would need huge data volumes and heavy processing loads so the traditional processing pipeline hits practical limits. This is especially true in the case for UWB SAR.
- We can view SAR images as:
$$y = A\mathbf{x} + n$$
	and we assume sparsity or compressibility of $\mathbf{x}$.
- The basic principle of sparse SAR imaging is to integrate the physical SAR sensing model and a sparse prior known as sparse representation.
- The three main categories of CS in SAR imaging are greedy, convex and Bayesian algorithms.

### Algorithmic Perspective
1. **Forward Projection:** If this were the true scene, what raw data would I see.
$$\hat{y}^{(k)} = Ax^{(k)}$$
2. **Residual:** What part of the data is unexplained?
$$r^{k} = y -\hat{y}^{(k)}$$
3. **Backprojection:** Where in the image could this residual energy come from?
$$g^{k} = A^Hr^{(k)}$$
4. **Gradient step**: Adds energy where the residual scatterers exist
$$x^{(k + 1/2)} = x^{k} + \mu g^{k}$$
5. **Sparsity Enforcement:** Removes weak, unexpected pixels
$$x^{k+1} = softThreshold(x^{k+ 1/2})$$

- [[Model Based Deep Learning]] and [[ML and DL techniques]] can naturally fit in here where we unroll the ISTA iterations and replace soft-threshold with CNNs. This can give better sparsity models, better denoising and better convergence.

### Compressed Sensing in SAR
- We can derive the discrete SAR observation model as
$$s = \Theta H \mathbf{x} + n$$
	where $s$ is the sampling echo data, $\mathbf{x}$ is the field to be reconstructed, $n$ is the noise, $H$ is the matrix of the exact SAR observation (the forward operator) and $\Theta$ denotes the undersampling operator.
- We can express this as an optimisation problem in the generalised form.
$$min_x R(\mathbf x), s.t.||s - \Phi \mathbf x||_2^2 \leq \epsilon$$
	where $\Phi = \Theta H$ is the measurement matrix,  $R(\mathbf x)$ is an objective function from the prior of $\mathbf x$, and the second term is the data fidelity term using the Euclidean distance. This essentially says among all the images that explain the data up to noise level $\epsilon$, choose the one that best matches the prior. This is the inverse problem formulation. 
- In the literature of CS, a sparse prior is used to perfectly reconstruct $\mathbf{x}$ with high probability. It is assumed that $\mathbf x$ is sparse, or compressible to be sparse in a transformed domain, denoted as $\mathbf x = \Psi a$ using a dictionary $\Psi$, then we can rewrite our original model as  $s = Ta + n$ where $T = \Phi \Psi$ using a sparse constraint. This can be expressed as:
$$min_a ||a||_0, s.t.||s-Ta||_2^2 \leq \epsilon$$
	where $||.||_0$ is the $\ell_0$ norm of a vector and counts the number of non zero entries. 

### Greedy Algorithms
- The basic principle of the greedy method is to decompose the sampled data into a combination of several atoms from $T$ and identify the support of the underlying signal in an iterative manner with sparse signal estimation. 
- A greedy algorithm builds the sparse support step by step. At each step is asks which coefficients would most reduce the residual error and then adds coefficients to the active set. 
- Examples include OMP, SP, MP etc.
- These algorithms are often very sensitive to noise and turbulence such as model error.

### Convex Algorithms
- This involves replacing the $\ell_0$ norm with some reasonable approximations such as the $\ell_p$ norm ($0 < p \leq 1$), the problem can then be transformed to:
$$min_x||a||_p^p, s.t.||s- Ta||_2^2 \leq \epsilon$$
- This can be replaced by unconstrained regularisation using Lagrange multipliers which can be formulated as:
$$min_a ||s- Ta||_2^2 + \gamma_p ||a||_p^p$$ 
### Key Points of Discussion
- Some limitations of the sparsity model for SAR imaging:
	- A predesigned dictionary $\Psi$ is usually used to enforce the sparsity constraint. The choice of $\Psi$ is generical empirical to the measured data without being data adaptive. The performance highly depends on the established model of CS during sparse reconstruction.
	- High complexity due to the iterative solution manner.

### Low Rank Methods
- While CS primarily enforce sparsity in some fixed basis/dictionary, low-rank methods ensure low-dimensional subspace structure in matrices and tensors.
- If you arrange your data into a matrix, say $Y$, low rank means only a few sigular values of $Y$ are nonzero or significant. This can be seen as sparsity in a special transform domain, like the SVD domain.
- We have the following model
$$S = \Phi(X) + N$$
- The generalised problem of matrix completion can be expressed as:
$$min_X~rank(X) s.t. ||S - \Phi(X)||_2^2 \leq \epsilon$$

### ML/DL
- Learns the right model or representation from the data rather than hand-designing $\Psi$ and $R()$.
- DL has also be incorporated with CS, known as deep CS.

#### IHT and IST
- We can take a classical iterative sparse reconstruction algorithm, see that each iteration looks like a neural network layer, then unroll a finite number of iterations into a deep network and learn the parameters from the data. This is an example of [[Model Based Deep Learning]]. More detail in [[Model Based Deep Learning#Deep Unfolding|Unrolled Networks]].
- To solve the minimum $\ell_1$ norm of CS, the IHT/IST algorithm can be decomposed as:
$$a_k^+ = a_k - \rho T^H(Ta_k -s)$$
$$a_{k+1} = argmin_a||a-a_k^+||_2^2 + \gamma ||a||_1$$
	where $a_{k+1}$ and $a_k$ are he estimations of $a$ at the given iterations, and $\rho$ is the updating step. Then $a_{k+1}$ can be estimating using hard/soft thresholding as
	$$a_{k+1} = E(a_k^+, \gamma)$$
- For IHT/IST algorithm, the parameters such as $\rho$ and $\gamma$ are very important to determine the iteration, convergence and image precision. Using an unrolled version of the traditional IHT/IST algorithm can overcome many of the drawbacks. The $k^{th}$ iteration can be treated as a single network layer.
- This layer contains a sequence of operations of data multiplication, summation and thresholding, which is the same as a neural network. The total $k$ iterations of IHT/IST can be unfolded into a form of DNN with $k$ layers.
- The $kth$ layer can be formulated as such
$$a_{k+1} = \Gamma(W_ka_k + b_k\gamma)$$
$$W_k = I - \rho T^HT$$
$$b_k = \rho T^H s$$
where $W_k$ and $b_k$ are the weight matrix and bias vector respectively. 
- The training of such a model can be implemented on available data using a loss function:
$$min_{W_k,b_k, \gamma}\sum_{l=1}^L||G(s^l;W_k,b_k,\gamma) - a^l||_2^2$$
	where $G$ denotes the forward.
- Usually gradient based algorithms can be used to solve this.

#### ADMM
- [[Model Based Deep Learning]] 
- A similar process can be done with ADMM.
- The ADMM procedure of an $\ell_1$ norm CS solution can be expressed as:
$$a_{k+1} = argmin_{a} ||s - Ta||_{2}^2 + \frac{\mu}{2}||a - \mu_k + v_k||_2^2$$
$$u_{k+1} = argmin_{u} = \frac{\mu}{2}||a_{k+1} - u + v_k||_2^2 + \gamma||u||_1$$
$$v_{k+1} = v_k + a_{k+1} - u_{k+1}$$
	where $u$ and $v$ are auxiliary variables, and $\mu$ denotes the penalty coefficients. This can be solved as:
$$a_{k+1} = (T^H T + \mu I)^{-1}(T^Hs + \mu(v_k - u_k))$$
$$u_{k+1} = E(a_{k+1} + v+k, \frac{2\gamma}{\mu})$$
$$v_{k+1} = v_k + a_{k+1} - u_{k+1}$$
- ADMM allows for all of the parameters $\mu$, $\gamma$ and $\Psi$ to be learned on training data. The learning of $\Psi$ is a major characteristic of an ADMM network.

### Key Challenges

#### Measurement Matrix Construction
- The overall measurement matrix $\Theta$ combines:
	- The undersampling operator and the SAR observation matrix  (forward model)$H$.
- They are critical since they determine whether CS can succeed and they determine computational cost.
- We want random or psuedo-random sampling. In SAR hardware this is hard to implement, so practical schemes use quasi random or structured patterns.
- Therefore a key challenge is to design $\Theta$ that is hardware feasible, has good CS properties and works in 2D for best performance.
- Furthermore, to solve SAR imaging we need the exact $H$. We need the forward model $H$ and the reverse $H^H$. This can be very computationally expensive, so fast approximations of $H$ are often derived.
- A key challenge is to balance the accuracy of $H$ (full physics, wideband) against efficiency.

#### Sparse Representation
- In CS, we need the image to be sparse or compressible in some dictionary.
- For SAR, we have complex valued images with random phase due to coherent processing and speckle noise. This means SAR images are not clearly sparse in some dictionary especially for dense and cluttered scenes.
- A challenge is finding a dictionary or transform in which real SAR images are truly sparse or compressible. This is hard and scene dependent and there is no universally accepted best dictionary.
- We may need adaptive/learned transforms that handle phase, speckle etc.

### Non-ideal Factors and Model Mismatch:
- H is not exact in real systems since platforms do not fly in perfectly straight, we have motion errors due to turbulence and other errors which cause distortions in H.
- This means we have model mismatch and basis mismatch.
- To alleviate this, we propose sparsity-driven autofocusing but these are complex and computation heavy.

### FMCW Papers
- Papers that explicitly reference [[FMCW]].
- In order to apply the theory of compressed sensing, first a sparse representation of the model must be established.
- CS assumes that the scenes reflectivity $\alpha$ is sparse in some domain (sometimes in the image domain itself, or after a transform such as wavelets).
- After distance correction, the baseband can be modelled as a known complex exponential as a function of time . The measurement matrix can be constructed:
$$\Phi=\exp (-j\frac{4\pi K_rR }ct)$$
- $t$ is the measurement times and $R$ is the discretised slant ranges. Each range cell/location contributes a term with a certain phase term after discretisation.

$$\Phi = \begin{bmatrix} \exp (-j\frac{4\pi K_rR_1 }ct_1) &\dots &\exp (-j\frac{4\pi K_rR_{NN} }ct_1)\\\vdots &\ddots &\vdots \\\exp (-j\frac{4\pi K_rR_1 }ct_M) &\dots &\exp (-j\frac{4\pi K_rR_NN }ct_M)\end{bmatrix}$$
- We can write $y = \Phi\alpha$, with the unknown coefficients can be established by a reconstruction algorithm. This is the forward CS model. This can be written as some optimisation problem.
$$\min||x||_0~~\text{s.t}~||y-\Phi\alpha|| \leq \epsilon$$
- The process of minimising the $\ell_0$ norm is a NP-hard problem. Many algorithms have been proposed to do this including greedy algorithms such as OMP.

- High resolution SAR imaging systems require more bandwidth and a larger synthetic aperture. On board storage, computing and downlink transmission of data is a major bottleneck in these high resolution SAR. This motivates compression technique to efficiently compress the acquired raw data and also guarantee robust reconstruction. Sub-Nyquist SAR based on CS techniques are a major area of exploration for high resolution SAR image reconstruction.