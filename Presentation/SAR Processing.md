←[[UWB Considerations]] 

## Compressed Sensing
- Sub-Nyquist sampling reduces computational load. Motivation for use in UWB SAR.
- General expression:
$$y = Ax + n$$
- Reconstruction takes the form of some optimisation problem that can be solved by some iterative algorithm.
$$\min||x||_0~~\text{s.t}~||y-Ax||_2 \leq \epsilon$$
$$\hat{x} = \text{argmin}\frac12||y-Ax||_2^2 + \lambda R(x)$$
- Computational cost, Model mismatch, Choice of transform and parameters
## Deep Learning
- 'Black-Box' DL techniques
- Raw SAR Data -> Image
- Requirements of large volumes of data and generalisation is not guaranteed.
## Model-Based Deep Learning
- Bridge between Compressed Sensing and Deep Learning.
- Common method involves loop unrolling.
- Parameters in the reconstruction procedure can be key in determining convergence and imaging precision (step size, regularisation ) etc.
- Each iteration to be treated as a specific network layer.

## Resources
[# Sparsity-Driven Synthetic Aperture Radar Imaging: Reconstruction, autofocusing, moving targets, and compressed sensing](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=6832835)
[Sparse Synthetic Aperture Radar Imaging from Compressed Sensing and Machine Learning: Theories, applications, and Trends](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9968096)
[Airborne FMCW SAR Sparse Data Processing via Frequency-Scaling Algorithm](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9104872)[FMCW SAR Sparse Imaging Based on Approximated Observation: An Overview on Current Technologies](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9170786)
[FMCW SAR Imaging Based on Compressed Sensing](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9332350)
[Compressed FMCW SAR Image Reconstruction](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9905031)
[Sparse Scene Recovery for High-Resolution Automobile FMCW SAR via Scaled Compressed Sensing](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=8805113)
[Airborne FMCW SAR Sparse Imaging: Initial Results](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=8631544)
[Wavenumber Domain Algorithm-Based FMCW SAR Sparse Imaging](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=8723593)
[RDAnet: A Deep Learning Based Approach for Synthetic Aperture Radar Image Formation](https://arxiv.org/pdf/2001.08202)[Model Based Deep Learning](https://arxiv.org/pdf/2012.08405)
