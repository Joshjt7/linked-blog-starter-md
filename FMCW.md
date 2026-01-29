- The way the SAR signal model changes in the FMCW case compared to pulsed radar needs to be considered.
- Focus on the airborne FMCW case.
- In FMCW, the commonly used stop and go assumption is no longer valid.
- In pulsed 
- When FMCW radar is used, the transmitted signal can be expressed in the form:
$$s_t = \text{exp}(j2\pi(f_ct +\frac12\alpha t^2))$$
	where $f_c$ is the carrier frequency
- In stationary scenarios, the received signal is delayed version of the transmitted:
$$s_t = \text{exp}(j2\pi(f_c(t-\tau) +\frac12\alpha (t-\tau)^2))$$
	where $\tau$ is the time delay.
- In dechirp-on-receive systems, the received and transmitted signals are mixed in order to reduce the required system-sampling rate. The mixing generates the intermediate frequency (or beat) signal:
$$\text{exp}(j2\pi(f_c\tau +\alpha t\tau-\frac12\alpha\tau^2))$$
- The delay time is range dependent:
$$\tau = \frac{2R(t,\eta)}{c}$$
$$R(t,\eta) = \sqrt{R_0^2 + u^2(t-\eta)^2} \approx R_\eta + \frac{u^2\eta}{R_\eta}t$$
	with $R_\eta = \sqrt{R_0^2 + (u\eta)^2}$ 
- We can now write:
$$s(t,\eta) = \text{exp}(j2\pi[f_c(\frac{2R_\eta}{c}-\frac{f_d\lambda}{c}t)+at(\frac{2R_\eta}c-\frac{f_d\lambda}ct)-\frac{2a}{c^2}R_\eta^2+\frac{2a}{c^2}R_\eta f_d\lambda t - \frac{af_d^2\lambda^2}{2c^2}t^2])$$
	where $f_d = -\frac{2}{\lambda}\frac{u^2\eta}{r_\eta}$ 

- Combing the beat signal with the approximated range equation:
$$y(t,t_a) = \exp(-j\frac{4\pi R}{\lambda})\exp(-j\frac{4\pi RK_r t}{c}+j2\pi f_d t)\text{exp}(j\frac{4\pi K_r}{c^2}R^2)$$
	The first term is the phase required for azimuth focussing, the second term is the phase in the range direction after de-chirp, and the third term is the residual phase term.
- The instantaneous difference in frequency between the transmit and receive waveform is known as the beat frequency.
- The time delay between the transmitted and echo cannot be directly measured. However, it can be estimated based on $f_{beat}$.
- Measurement of the the beat frequency allows us to determine the range $R$ to a detected target because it is directly related to the target delay.
$$f_{beat} = \frac{2K_rR}{c}$$
- If either the target or the radar platform moves, the range is no longer constant. This results in a doppler shift of the carrier. 
$$f_{If} \approx \frac{2K_RR_0}{c}+\frac{2V_R}{\lambda}$$
- The movement induces another term in the doppler frequency.
- Therefore in FMCW SAR, both delay and Doppler contribute to the same beat frequency band. This is coupling.

$$\Phi(f_\tau,f,r_0) = \frac{4\pi \alpha r_0}{c}\sqrt{(f_0+f)^2-[\frac vc(f_0+f)+\frac{cf_{\tau}}{2\alpha v}]^2}-2\pi f_{\tau}\frac f{K_r}+2\pi f_{\tau} \tau_0 - 4\pi \alpha (f_0+f)\frac{r_c}{c}-4\alpha \pi \frac{r_c}{c}f_{\tau}$$
$$\sigma(\tau_0,r_0)\exp[-j2\pi f_0 (\tau_d -\tau_c)]\exp[-j2\pi K_r (\tau_d - \tau_c)(t-\tau_c)]\exp[-j2\pi K_r (\tau_d - \tau_c)]$$
with $\tau_d$ being the delay $\tau_c$ being delay of the reference.

$$r_k(t)=\int\rho(x)\exp\{-j(w_0\tau(x)+2\alpha \tau(x)-\alpha\tau(x)^2)\}dx+\eta_k(t)$$

$$$$

[An Overview of Advances in Signal Processing Techniques for Classical and Quantum Wideband Synthetic Apertures]
### Resources

[Airborne FMCW SAR Sparse Data Processing via Frequency-Scaling Algorithm](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9104872) 

[FMCW SAR Sparse Imaging Based on Approximated Observation: An Overview on Current Technologies](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9170786)

[FMCW SAR Imaging Based on Compressed Sensing](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9332350)

[Compressed FMCW SAR Image Reconstruction](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9905031)

[Sparse Scene Recovery for High-Resolution Automobile FMCW SAR via Scaled Compressed Sensing](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=8805113)

[Airborne FMCW SAR Sparse Imaging: Initial Results](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=8631544)

[Wavenumber Domain Algorithm-Based FMCW SAR Sparse Imaging](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=8723593)
[Data Processing of Airborne FMCW SAR Sliding Spotlight](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9652334)

[Airbrone FMCW SAR Signal Processing Using Back-Projection Algorithm Correcting Continuous Motion Effect](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=8898863)

[Study on the Echo Signal Model and R-D Imaging Algorithm For FMCW SAR](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=7455466)

[Signal Processing for FMCW SAR](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=4373378)

[FMCW SAR: From Design to Realisation](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=7729284)

