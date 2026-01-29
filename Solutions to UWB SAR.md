### Frequency Domain Approaches:
- As described, there are many [[UWB SAR Challenges]], which break down the conventional narrowband SAR model and hence reduce the quality of our results.
- For moderate wide bandwidths (WB but not UWB), classical frequency domain algorithms can still produce viable results with careful parameter tuning, small scenes and limited squint.
- Can still provide viable results with modified variants of the algorithm.

### Time-Domain Algorithms:
- A time domain algorithm such as backprojection works since it uses the exact range algorithm for each pixel and makes no narrowband assumptions.
- However, it has a large computational complexity. Growth in computing power and research into FPGA implementations can improve speed and efficiency.
- Variants of the algorithm such as fast backprojection and approximate backprojection.

### Hybrid Approaches

### Data Driven and Deep Learning Approaches
- See [[ML and DL techniques]] and [[Model Based Deep Learning]].
- Often used with [[Compressed Sensing]].
- Start with model based reconstruction and then use CNNs or other networks to remove artifacts and speckle, improve focus, apply superresolution or denoise.
- Learn a network that approximates the inverse of the forward SAR operator. This can be an "unrolled" iterative reconstruction approach, where each layer mimics a step in physics-based algorithm, supplemented with learned priors.
- Also some work of a end to end network where input is raw SAR data and the output is an image. Required large labelled datasets, and may not generalise well for different aspect angles or different carrier and bandwidth choices.

### Compressed Sensing:
- See [[Compressed Sensing]].
- Heavily linked to [[Model Based Deep Learning]] and [[ML and DL techniques]].
- We can formulate the problem as a compressive sensing and sparse reconstruction problem. We assume that the scene is sparse and try to reconstruct using sparse recovery.