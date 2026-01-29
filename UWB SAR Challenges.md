[[UWB]] SAR introduces challenges in processing that conventional [[Synthetic Aperture Radar#SAR Processing|SAR processing]] algorithms are not able to solve. 

*" In the UWB regime, Doppler frequency shifts become significantly coupled with the signal bandwidth, introducing new challenges in image formation and focusing."* - [[Updated Description]]

- Frequency domain algorithms are the standard approach in SAR processing. However, they are unable to produce good quality results in the UWB case. This is due to long integration times needed for UWB SAR.
- Most frequency-domain methods require interpolation of data in frequency domain. This can result in errors that degrade image quality.
- Classical algorithms assume that the carrier frequency dominates the bandwidth $B << f_c$ which would imply that wavelength is approximately constant and doppler is approximately linear.
- Traditional SAR processing assumes that range and azimuth processing can be separated. This is only true when bandwidth is small, range migration is small and squint angle is small. This is not the case in the UWB case since range phase couples to azimuth in a frequency dependent way.
- In UWB SAR, range migration becomes nonlinear and frequency dependent. There is severe range migration in UWB SAR.
- In narrowband SAR, we have $B/f_{c} << 1$ which means that we have a small frequency change across the entire bandwidth. In UWB, we have $B/f_{c} > 0.2$, meaning variations in frequency need to be considered. This leads to many challenges. 

### Range Cell Migration
[[Synthetic Aperture Radar#Range Cell Migration|Range Migration]] is a bigger problem in UWB SAR compared to conventional narrowband SAR. UWB SAR has very small small range resolution, large bandwidth and long synthetic aperture lengths. This means that RCM spans many cells.
- Large [[Synthetic Aperture Radar#Integration Angle|Integration Angle]] leads to severe range migration.

### Range Curvature
- For a given point, the radar to target distance is given by $$R(x) = \sqrt{R_{0}^2+x^2}$$
- This is a hyperbola. This hyperbola shape us called range curvature.
- In conventional SAR, the signal wavelength is nearly constant over the bandwidth, and the hyperbolic range curve is the same for all frequencies.
- But in UWB SAR, the bandwidth is large meaning lower frequencies experience different effective ranges, and the difference between hyperbolic range curves are different across the spectrum.
- This causes frequency dependent range migration.
- The received phase signal is given by $$\phi(x,f) = -\frac{4 \pi f}{c}R(x)$$
- We see phase depends both on radars position and frequency. In narrowband SAR, this dependence is mild.
- We perform a Taylor series expansion of $R(x)$ and substitute into phase. We see we have higher order terms multiplied by $f$, which leads to range azimuth coupling.
- The phase along the azimuth direction depends on targets range and the phase along the range depends on azimuth position. This means the range and azimuth are not separable.
- Different frequencies see different effective ranges. This means that different frequencies have different phase curvature. This is differential range curvature.

### Motion Compensation
- Motion compensation corrects deviations in the radar platforms trajectory from the ideal straight flight path.
- In narrowband SAR, motion errors correspond to small phase shifts.
- In UWB SAR, the situation is much more complex.

### Doppler
- Doppler refers to frequency shift due to relative velocity.
- The Doppler history is the entire time-varying Doppler as the radar passes a target. 
- The average doppler frequency over the aperture is the Doppler Centroid.

### Overview of UWB SAR Challenges 
- The core foundation of narrowband or conventional SAR is that $B/f_c << 1$ meaning that the centre frequency is much larger than bandwidth. In the UWB case, it is often said that $B/f_c > 0.2$.
- The narrowband assumption that we have in turns allows for further simplifying assumptions to be made. 
	- A key assumption is that across a single pulse, is that wavelength can be treated as approximately constant. Our transmitted pulse is a chirp, so therefore has a linearly varying frequency, hence also varying wavelength across its duration. In the narrowband case, we assume that wavelength is constant, determined by the centre frequency. This hence means phase is dependent only on range, and not frequency.
	- Another key assumption is that the phase can be linearised around the carrier which allows separation of azimuth and range. This separation of range and azimuth is a fundamental aspect of the frequency domain SAR processing algorithms. The received signal is a function of the product between fast time and slow time.
	- As well as this, we can say that doppler is frequency independent, with the shift proportional to $f_c$. This allows for a single azimuth matched filter to be used.
	- Furthermore, we assume that the propagation delay is frequency independent.
- As well as breakdown of assumptions, UWB SAR amplify existing phenomena in narrowband SAR, creating additional challenges.
	- Phenomena such as range migration become frequency dependent.
	- Motion errors and motion compensation.
- These issues and challenges motivate development in UWB SAR image formation.

#### Full Model Description
- For our SAR model:
	- Platform position at slow time : $=r_p(\eta)$ 
	- Target position: $=r_t$
	- Instantaneous slant range: $=R(\eta) = ||r_p(\eta) - r_t||$ 
- We consider the complex passband transmit signal: $s_{tx}(t) = R\{s_{bb}(t)e^{j2 \pi f_c t}\}$ 
	- Where $s_{bb}(t)$ is the baseband envelope. 
- The received signal is a scaled and delayed version of the signal that was sent:
$$s_{rx}(\eta, t) \propto s_{bb}(t - \tau)e^{j2\pi f_c (t - \tau)}$$
- The radar brings the signal back down to baseband and we substitute $\tau = \frac{2 R(\eta)}{c}$.
- The received baseband signal from a point target at slow time $\eta$ after demodulation and matched filtering to $s_{bb}$.
$$S(\eta, t) \propto \sigma e^{-j \frac{4 \pi}{\lambda_c}R(\eta)}p(t - \frac{2 R(\eta)}{c})$$
	- $\sigma$ is target reflectivity 
	- $p()$ is the compressed pulse shape.
- This is already assuming matched filtering around a carrier $f_c$. The key step for narrowband is how $R(\eta)$ is approximated.
- In the true wideband case, the received signal should be written in frequency as:
$$S(\eta, f) \propto \sigma(f)P(f)e^{-j \frac{4 \pi f}{c} R(\eta)}$$
	- $f$ is the absolute frequency.
	- $P(f)$ is the spectrum of the transmitted pulse.
	- The phase term is linear in $f$, not just $f_c$.
- Narrowband assumptions:
	1. Phase variations across the band is small compared to that at the carrier. Under narrowband behaviour, the second factor is treated mainly as range delay, and not coupling with azimuth.
$$e^{-j \frac{4 \pi f}{c}R(\eta)} = e^{-j \frac{4 \pi f_c}{c}R(\eta)} e^{-j \frac{4 \pi \Delta f}{c}R(\eta)} $$
	2. Wavelength approximately constant:
$$\lambda(f) = \lambda_c = \frac{c}{f_c}$$
#### Range Azimuth Coupling
- Recalling our signal in narrowband case:
$$S(\eta, t) \propto \sigma e^{-j \frac{4 \pi}{\lambda_c}R(\eta)}p(t - \frac{2 R(\eta)}{c})$$
- We can apply range compression via matched filtering in fast time.
	- The peak $p()$ aligns at $t = \frac{2 R_0}{c}$
	- Near the peak, we treat $R(\eta)$ in the argument as approximately constant in $t$.
	- In narrowband SAR, the range resolution is relatively coarse, so a given range bin is large. Even though the target is moving, the target dose not move enough to leave that cell. We say the peak happens at a given fixed time.
$$S_{rc} \propto \sigma e^{-j \frac{4 \pi}{\lambda_c}R(\eta)}h_r(\tau - \frac{2 R_0}{c})$$
- This therefore means that the azimuth dependent term is only in the phase $e^{-j \frac{4 \pi}{\lambda_c}R(\eta)}$, while the range response $h_r()$ is independent of $\eta$ for that scatterer.
	- Range processing: Done purely in $t$/$\tau$
	- Azimuth processing: Done purely in $\eta$.
- We have separable processing.

- In UWB, the correct frequency domain expression is:
$$S(\eta, f) \propto \sigma(f)P(f)e^{-j \frac{4 \pi f}{c} R(\eta)}$$
	- Define a baseband frequency $f_b = f - f_c$
$$S(\eta, f_b) \propto \sigma(f_c + f_b)P(f_b)e^{-j \frac{4 \pi (f_c + f_b)}{c} R(\eta)}$$
$$S(\eta, f_b) \propto \sigma(f_c + f_b)P(f_b)e^{-j \frac{4 \pi (f_c)}{c} R(\eta)}e^{-j \frac{4 \pi (f_b)}{c} R(\eta)}$$
	- The phase term involving $f_b$ is coupled to $R(\eta)$, which depends on slow time $\eta$.
	- The term with $f_b$ and $R(\eta)$ acts as a time shift operator. The term B in the frequency domain, a phase shift that is linear in frequency corresponds to a time shift in the time domain. In the narrowband case $f_b$ is very small, so the time shift caused by the second term is small. Not the case in the UWB case, as $f_b$ is large so the time shift is massive.
	- This also relates to range cell migration.
- To do range compression, we apply a filter approximately matched to $P(f_b)e^{-j \frac{4 \pi f_b}{c}}$, but since $R(\eta) \neq R_0$ and $\eta \neq 0$, the residual phase becomes:
$$\Delta \phi(\eta, f_b) = -\frac{4 \pi f_b}{c}(R(\eta) - R_0)$$
- The residual phase term corresponds to shift and distortion in the range domain that depends on $\eta$.
- We have the true signal, and after matched filtering the filter should perfectly cancel the phase of the incoming signal. In standard processing, we usually use a stationary filter tuned to a fixed reference distance $R_0$. When you multiply the true signal by this filter, the phases add together. The $R_0$ in the filter tries to cancel the $R(\eta)$ in the signal. This results in the residual phase term.
- This term behaves like a time shift operator. This leads to errors.

#### Doppler Model
- In narrowband SAR, the doppler frequency shift can be given by:
$$f_D(\eta) \approx \frac{2v_r(\eta)}{\lambda_c}$$
	- Near broadside and closest approach, we say that $v_r(n)\approx - \frac{v^2}{R_0}\eta$ 
	- So Doppler is approximately linear in $\eta$ near the scene centre, and is independent of signal frequency.
- We consider the true doppler shift for a frequency $f$:
$$f_D(f,\eta)=\frac{2f}{c}v_r(\eta)$$
$$f_D(f_c + f_b,\eta)=\frac{2(f_c+f_b)}{c}v_r(\eta)=\frac{2f_c}{c}v_r(\eta)+\frac{2f_b}{c}v_r(\eta)$$
	- Narrowband SAR drops the second term. However, this term is non negligible in UWB case. Doppler becomes frequency dependent across the band.
	- The second term shows the doppler spread. As $f_b$ is large in UWB, this term creates a range of doppler shifts for a single target at single moment of time.
- Azimuth compression filter becomes frequency dependent. The azimuth matched filter must depend on azimuth frequency and range frequency.
- We have coupling of range frequency and azimuth doppler.

#### Range Migration:
- Range migration is the classical problem that the energy of a point target does not stay in a single range bin across the synthetic aperture, but moves through multiple bins.
- We define the two-way time delay:
$$t_{delay}(\eta) = \frac{2R(\eta)}{c}$$
- We also have a reference range:
$$t_0 = \frac{2R_0}{c}$$
- We can define range migration in time as:
$$\Delta t(\eta) = t_{delay}(\eta) - t_0 = \frac{v^2}{cR_0}\eta^2$$
- Under narrowband assumptions:
	- The range component of the signal can be treated as being driven by a fixed carrier geometry $f_c$.
	- The effect of bandwidth on the shape of the range-compressed peak is mostly captured by the matched filter.
- In UWB, we have frequency dependent range migration.
#### Azimuth Processing:
- We recall the narrowband phase:
$$\phi(\eta) \approx -\frac{4 \pi}{\lambda_c}R(\eta) = -\frac{4 \pi}{\lambda_c}(R_0 + \frac{v^2}{2R_0}\eta^2)$$
- After range compression and RCM correction at the correct range bin, the azimuth signal for a point target is:
$$s_{az}(\eta, \tau_0) \approx ~\sigma w_a(\eta) e ^{-j\frac{4 \pi}{\lambda_c}(R_0 + \frac{v^2}{2R_0}\eta^2)}$$
	- $w_a(\eta)$ is the antenna weighting
	- We can also drop the constant phase term.
- We can rewrite
$$s_{az}(\eta, \tau_0) \approx ~\sigma w_a(\eta) e ^{-j \alpha_c \eta^2}$$
	- Where $\alpha_c = \frac{4 \pi v^2}{2 \lambda_c R_0}$
	- This is a 1D chirp in slow time $\eta$ which depends on the carrier $f_c$.
- We use the same azimuth filter for all range bins.

- We now consider the UWB case
$$\phi(f_b, \eta) = - \frac{4 \pi(f_c + f_b)}{c}R(\eta) =  - \frac{4 \pi f_c}{c}R(\eta) - \frac{4 \pi f_b}{c}R(\eta)$$
$$\phi(f_b, \eta) =- \frac{4 \pi(f_c + f_b)}{c}(R_0 + \frac{v^2}{2R_0}\eta^2)$$
	- We have a constant term independent of $\eta$
$$\phi(f_b) = - \frac{4 \pi(f_c + f_b)}{c}R_0$$
	- We have a quadratic term which is the azimuth chirp
$$\phi(f_b,\eta) = - \frac{4 \pi(f_c + f_b)}{c}\frac{v^2}{2R_0}\eta^2$$
	- The azimuth chirp depends of $f_b$. Different frequencies experience slightly different azimuth chirp behaviour.
- In UWB, the correct matched filter must match the full 2D phase:
$$\phi(f_b,\eta) = - \frac{4 \pi(f_c + f_b)}{c}R(\eta)$$
	- The ideal matched filter is:
$$H_{2D}(f_b, \eta) \approx w_a(\eta)e^{+j \frac{4 \pi (f_c + f_b)}{c}R_{ref}(\eta)}$$
	- Where $R_{ref}$ is the hypothesised range trajectory used for focussing
- The filter depends on both $f_b$ and $\eta$ 

#### Wavenumber 
- Wavenumber is the spatial equivalent of frequency. Instead of telling us of how many cycles occur per second, wavenumber tells you how many cycles occur per meter.
- Range wavenumber:
$$k_r = \frac{4 \pi f}{c}$$
- The exact propagation for monostatic SAR is:
$$k_x^2 + k_y^2 = k^2 =  (\frac{2 \pi f}{c})^2$$
- Under appropriate assumptions, we can write the relation which connects azimuth and range wavenumbers. 
$$k_r^2 + k_a^2 \approx (\frac{4 \pi f}{c})^2$$
- In wideband:
	- The term $\frac{4 \pi f}{c}$ changes across the band.
	- The mapping from measured coordinates $(k_r, k_a)$ to scene spatial frequencies $(k_x, k_y)$ is frequency dependent.

#### Overview of Practical UWB SAR Processing Challenges
1. Loss of separability.
2. Frequency dependent doppler and defocus.
3. Algorithmic complexity

$$-\pi \frac{f_r^2}{\gamma} - \frac{4 \pi r_0}{c}\sqrt{(f_c + f_r)^2 - (\frac{cf_a}{2v})^2}$$