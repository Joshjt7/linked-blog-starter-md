- Refer to [[Complete Notes]] for some details.

### SAR Model From Literature:

***A Novel Range Cell Migration Correction Algorithm for Highly Squinted SAR Imaging
- The received signal from $p$ is given by:
$$s(\tau, X) = \text{rect}(\frac{\tau - \Delta t}{T_p})\text{rect}(\frac{X - x_0 - x}{L})~\text{exp}[j2\pi(-f_c \Delta t + \frac{\alpha (\tau - \Delta t)^2}{2})]$$
	with $\Delta t = 2R(X;r,x)/c$

***Precision SAR Processing Using Chirp Scaling
- After demodulation, the response from a point scatterer located at range $r$ at azimuth time $t = 0$:
$$pp(\tau , t;r) = a(t,r)s_0(\tau - \frac{2R(t;r)}{c})\text{exp}[-j\frac{4\pi}{\lambda}R(t;r)]$$
***Digital Processing of Synthetic Aperture Radar Data
- The data is first demodulated to baseband. The demodulated radar signal received from a point target can be modelled as:
$$    S(\tau,\eta) = w_r[\tau - \frac{2R(\eta)}{c}]w_a[\eta - \eta_c]  e^{-j\frac{4\pi f_0}{c}R(\eta)}e^{j\pi s(\tau - \frac{2R(\eta)}{c})^2}$$

***Performance Evaluation of Frequency-Domain Algorithms for Chirped Low-Frequency UWB SAR Data Processing
- The phase of the demodulated baseband signal can be described as:
$$\Phi(\tau,t_a;r_0) = -\frac{\pi}{\lambda_c}r(t_a;r_0) + \pi\gamma[\tau-\frac{2r(t_a;r_0)}{c}]^2$$
***A Modified Non Linear Chirp Scaling Algorithm For Highly Squinted SAR on Maneuvering Platform
- Supposing that the transmitted pulses are linearly modulated in frequency. It can be expressed as the echo signal from the point $Q$ on the range frequency domain as:
$$S(f_r,t_a;R(t_a)) = w_r(f_r)w_a(t_a)~\text{exp}(-j\pi\frac{f_r^2}{\gamma})~\text{exp}(-j\frac{4\pi}{c}(f_c + f_r)R(t_a))$$
***A New Subaperture NonLinear Chirp Scaling Algorithm for Real Time UWB-SAR Imaging
- Assuming that the antenna has a rectangle pattern, the stripmap SAR echoes from a point target can be expressed by:
$$s(t_e) = \text{rect}(\frac{t_e - \frac{2r}{c}}{T_p})~\text{exp}(-j\frac{4\pi f_c r}{c} + j\pi K(t_e - \frac{2r}{c})^2)$$ ***A Modified Nonlinear Chirp Scaling Algorithm Based on the Numerical Estimation
- After demodulation to baseband, the signal is written as:
$$s(\tau,t) = p_r(\tau - \frac{2R(t)}{c})w_{az}(t)~\text{exp}(-j4\pi f_c \frac{R(t)}{c})$$

***An Improved Chirp Scaling Algorithm with Capability Motion Compensation for SAR
- The baseband signal can be expressed:
$$s(\tau,\eta) = A_0W_r(\tau - \frac{2R(\eta)}c)W_a(\eta - \eta_c)~\text{exp}(-j\frac{4\pi R(\eta)}\lambda)~\text{exp}(-j\pi K_r (\tau - \frac{2R(\eta)}{c})^2)$$

### Complete passage on SAR signal model

With the individual range and azimuth components considered, the full SAR signal model should be considered. The SAR signal can be presented in different domains and under different simplifying assumptions and approximations. Each domain can place certain emphasis on some of the important properties seen within SAR. Using the approximated form of the range equation, the received signal can be written as
$$
    S(\tau,\eta) = w_r[\tau - \frac{2R(\eta)}{c}]w_a[\eta - \eta_c]  e^{-j\frac{4\pi r_0}{\lambda_c}}e^{-j\pi s_a \eta^2}e^{j\pi s(\tau - \frac{2R(\eta)}{c})^2}$$
This form of the signal shows the range envelope, the azimuth envelope, the azimuth phase term, the linear frequency modulation of the azimuth signal and the range term. It is important to consider the conditions of validity which allow for the approximated form of the range equation. The approximation is generally valid for the cases of low squint angle and when aperture length is moderated. By applying a Fourier transform in azimuth, the signal in the range doppler domain can be seen. The range cell migration in this domain can be expressed as a function of the azimuth frequency, which combines the approximated form of the range equation and the azimuth chirp.
$$R_{rd}(f_{\eta}) \approx R_0 + \frac{\lambda^2 R_0}{8V_r^2}f_{\eta}^2$$
Another Fourier transform in range gives us the SAR signal is the two-dimensional frequency domain. The phase within this domain can be written as:
$$\theta_{2df} \approx \frac{\pi f_{\eta}^2}{K_a'}-\frac{\pi f_{r}^2}{K_r}-\frac{4\pi(f_0 + f_{\tau})R_0}c$$
This phase terms also shows the range migration. The forms of the signals above are not valid in all cases. With this model, we have simplified range migration and approximate range-azimuth coupling. First, as discussed above, the approximation of the range equation is not valid in the general case.  Furthermore, the narrowband approximation is also used which models the signal with just $\lambda_c$ or $f_c$. This is valid when the bandwidth of the signal is significantly smaller than the centre frequency, which is true for narrowband signals but not in the UWB regime. A more general form of the SAR signal therefore needs to be derived. From the received baseband signal, a range Fourier transform followed by an azimuth Fourier transform. The phase of the received signal can be written in the form.
$$\Phi(f_r,f_a;r_0) = -\pi\frac{f_r^2}{\gamma} - \frac{4\pi r_0}{c}\sqrt{(f_c + f_r)^2 - (\frac{cf_a}{2v})^2}$$

This phase term contains the azimuth modulation, the range cell migration as well as the coupling between range and azimuth. We get a migration factor which is of the form:
$$=\sqrt{1-\frac{V_r^2 \eta^2}{R^2(\eta)}}$$

 sbb​(tf​,ts​)​=∬σ(x,y;finst​)R2(ts​;x,y)1​exp{−2α(finst​)R(ts​;x,y)}⋅exp{−jc4πfc​​R(ts​;x,y)−jc4πμ​R(ts​;x,y)tf​+jc24πμ​R2(ts​;x,y)}dxdy.​