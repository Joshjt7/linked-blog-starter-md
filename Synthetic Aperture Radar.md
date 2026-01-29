
## Tutorial on Synthetic Aperture Radar

### Introduction
- SAR systems have a side-looking imaging geometry that are based on pulsed radar installed on a platform with forward motion.
- The flight direction is denoted as the azimuth and the line of sight is denoted as the range.
- A major drawback of SLAR (Side-Looking Airborne Radar) is the moderate to low azimuth resolution, which is dependent on the distance.
- Focus on [[Plan#🧭 1️⃣ Stage 1 Strengthen your SAR fundamentals (conceptual mastery)|SAR Fundamentals]] 

### Basic SAR principles 
- EM waves are sequentially transmitted and the backscattered echoes are collected by the radar antenna.
- A coherent combination of the received signals allows the construction of a virtual aperture that is much longer than the physical antenna length.
- SAR sensors commonly use frequency modulated pulsed waveforms for transmission with the chirp signals. The instantaneous frequency is varied linearly over time $f_{i} = k_{r}t$  where $k_{r}$ is known as the chirp rate. This yields the bandwidth $B_{r}=k_{r}t$. 
- We defines some key notation.
	- $r_{0}$ : this is the distance of closest approach.
	- $v$ : the speed of the moving platform
	- $r(t)$ : distance from the antenna to the target.
- At any time $t$, the distance between the radar and a point on the ground can be given by. $$r(t) = \sqrt{r^2_{0}+(vt)^2} = r_{0} + \frac{(vt)^2}{2r_{0}}$$
	- The approximation on the right can be made since in general $vt$ is much smaller than $r_{0}$. This then allows for Taylor series expansion and we can ignore the higher order terms.
- Time in the range direction is often denoted by *fast time* and time in azimuth is denoted by *slow time*. 
- The range variation of a point target over time is directly related to the azimuth phase: $$\phi(t) = \frac{-4 \pi r(t)}{\lambda}$$
- The slant range resolution is inversely proportional $\delta_{r}$ to the system bandwidth. $$\delta_{r} = \frac{c_{0}}{2B_{r}}$$
- The azimuth resolution $\delta_{a}$ is provided by the construction of the synthetic aperture. It is given by half the length of the antenna. $$\delta_{a} = \frac{d_{a}}{2}$$
- The beamwidth of an antenna of length $d_{a}$ can be approximated as $\Theta_a = \frac{\lambda}{d_{a}}$. The corresponding synthetic aperture length is given by $L_{sa} = \Theta_{a}r_0 = \frac{\lambda r_{0}}{d_{a}}$ .
- A long synthetic aperture is favorable since it results in a narrow virtual beamwidth $\Theta_{sa} = \frac{\lambda}{2L_{sa}}$. (note we have the divide by 2 due to the path from transmission to reception).
- From this, we can see that a short antenna length yields a fine azimuth resolution. This is because a radar with a short antenna sees any point on the ground for longer, which is equivalent to a longer virtual antenna and this a higher azimuth resolution.
- The received echo signal data forms a two-dimensional data matrix of complex samples. The complete processing can be understood as two separate matched filter operations along the range and azimuth dimensions.
	- Each range line is multiplied in the frequency domain by the complex conjugate of the spectrum of the transmitted chirp. This only reveals information about the relative distance between the radar and any pulse on the ground.
	- The same reasoning is seen in azimuth. The signal is convolved with its reference function which is the complex conjugate of the response expected from a point target on the ground. The azimuth signal can be modelled as: $$s_a(t) = A \sqrt{\sigma_0}~exp(i\phi^{scatt})~exp(-i\frac{4\pi}{\lambda}r(t))$$
		- $A$ accounts for the dependency of the received signal with system parameters such as transmit power and losses. The radar cross section is given by $\sigma_0$ and $\phi^{scatt}$ is the scattering phase. $\frac{4\pi r(t)}{\lambda}$ denotes the phase variation due to changing direction.
- The range reference function in the match filtering process is dependent only on the transmitted chirp, whereas the azimuth reference function depends on the geometry and is adapted to the range.
- A quantitative measure of the signal processing quality is possible by investigating the impulse response function. 
- Range Cell Migration (RCM) is a property originating from the fact that the distance between the radar and any fixed point on the ground is changing with the synthetic aperture time.

### Range Cell Migration
- Range migration is the effect where a single stationary target appears at different range bins over time.
- This means that the target moves through range in the SAR data even though it is not physically moving. This happens because the distance between the radar and the target changes as the radar flies past.
- Consider the distance to a point on the ground as the radar moves. This point is initially far away, then gets closer, and then far away. So in raw SAR data, the target appears as a curved track.
- SAR processing algorithms assume that for a target all the echo energy is in the same range bin. We need to correct for range cell migration.

- Consider a point target at closest range $R_0$ when $\eta = 0$:
$$R(\eta) \approx R_0 + \frac{v^2}{2R_0} \eta^2$$
- After demodulation, we have a residual phase term.
$$\Delta \phi(\eta, f_b) = -\frac{4 \pi f_b}{c}(R(\eta) - R_0)$$
- This phase term can be expressed as some time delay:
$$\Delta \tau(\eta) = \frac{2}{c}(R(\eta) - R_0) \approx \frac{v^2}{cR_0} \eta^2$$
- RCM appears as a frequency dependent phase term proportional to $f(R(\eta) - R_0)$. This is true regardless of narrowband vs UWB, as any time shift is always represented as frequency dependent linear phase term.
- Combining the range formula and the residual phase term:
$$\phi_{res}(f, \eta) \approx -\frac{4 \pi f_c}{c} \frac{v^2}{2R_0} \eta^2 - \frac{4 \pi f_b}{c} \frac{v^2}{2R_0} \eta^2$$
- We define
$$\alpha_c = \frac{4 \pi f_c v^2}{2cR_0}$$
$$\alpha_f(f_b) = \frac{4 \pi f v^2}{2cR_0}$$
- We therefore have:
$$\phi_{res  } \approx -\alpha_c \eta^2 - \alpha_f(f) \eta^2$$
	- The first term denotes the azimuth chirp and the second term is the RCM term.

### Integration Angle
- The total angle over which the radar receives echoes from a target as the platform moves.
- It is the change in look angle from the radar platform to the target during the time the target remains inside the antenna beams.
- Integration angle in SAR systems tend to be very large.
- During the radars flight point, a fixed point on the ground is far ahead of the radar, then broadside, then behind the radar. During this time, the radars angle look angle to the point changes. This angle sweep is called the integration angle.

### Squint Angle
- Squint angle is the angle between the radars pointing direction and the direction perpendicular to the flight path.
### SAR Processing:
- At each antenna position, radar illuminates the target by transmitting RF signals. The radio waves impinge on the target and reflections are received by the radar.
- Collected raw data is processed to obtain the image of target in a spatial domain with higher cross-range resolution.
- Processing can fall into two approaches:
	- Time domain:
		- Global back projection (GBP):
		- Fast backpropagation.
		- Polar format algorithm (PFA)
	- Frequency domain:
		- Range doppler algorithm
		- Chirp scaling algorithm.
		- Omega-k algorithm.

#### The Range Doppler Algorithm
- The range doppler is one of the original, fundamental SAR methods.
- Range Compression:
	- FFT in fast time to range frequency.
	- Matched filtering
	- IFFT back to obtain range compressed data
- Azimuth FFT:
	- For each range bin, perform FFT in slow time to get azimuth frequency.
- RCM correction in frequency domain:
	- Narrowband model implies a known RCM curve as a function of $f_{\eta}$.
	- Often done by phase compensation.
- Azimuth compression:
	- Each range frequency bin is essentially a 1D azimuth chirp.
	- Apply an azimuth matched filter.
	- IFFT to return to slow time and obtain a focussed image.

- Narrowband assumptions used
	- Described in [[UWB SAR Challenges#Overview of UWB SAR Challenges|SAR narrowband assumptions]]. 
	- Phase is modelled at the carrier only:
$$\phi(\eta) \approx -\frac{4 \pi}{\lambda_c} R(\eta)$$
	- Doppler and azimuth chirp rate depend of $f_c$, but not on the frequency within the band.
	- RCM is described by a single quadratic function in slow time that is independent of fast time frequency.
- Breakdown in UWB
	- We have a frequency dependent azimuth phase. The azimuth chirp rate varies with frequency across the band. RD algorithm uses a single azimuth matched filter based on $f_c$.
	- We have frequency dependent range migration.
	- Coupling of phase and azimuth.

#### Chirp Scaling Algorithm
- The core idea is to underdo RCM without explicit 2D interpolation. This can be achieved by applying quadratic phase multiplications in $f$ and $\eta$ so that the frequency dependent shifts due to RCM are converted into phase variations that can be corrected by 1D operations.
	1. Multiply the data by a "chirp scaling" phase factor
	2. Perform FFT in azimuth
	3. Inverse FFT in azimuth, IFFT in range as needed.
- Under narrowband approximations:
	- Any appearances of $f_c + f_b$ are approximated by $f_c$.
	- Higher order dependencies on $f_b$ are neglected or simplified.
- Breakdown in UWB regime:
	- Geometry must use the full frequency and not just $f_c$.
	- Frequency dependent RCM.
	- Frequency dependent azimuth chirp rate.
- The chirp scaling is designed to convert this frequency dependent shift into something that can be corrected by 1D operations.
- The chirp scaling algorithm applies a quadratic (chirp) phase multiplication.
- After applying $e^{j \Phi_{cs}}$, the energy from each target is aligned in range in a way that can be corrected by subsequent 1D transforms.
- In the narrowband assumptions, the dependence of RCM phase on $f$ is well approximated as linear. Higher order frequency behaviour is small enough to be neglected or absorbed into simple corrections.
- In UWB case, higher order terms are relevant, so the dependence becomes strong and nonlinear.
#### Omega - K algorithm 
- Refer to [[Wavenumber Domain]]
- Can be known as the Omega-K algorithm or the Range-Migration algorithm.

##### Wavenumber
- We introduce the wavenumber/spatial frequency: $k = \frac{2 \pi}{\lambda} = \frac{2 \pi f}{c}$.
- As we have two way travel, the effective range wave number can be written in the form of:
$$k = \frac{4 \pi f}{c}$$
- The wavevector has components in range and azimuth:
$$k^2 + k_r^2 + k_a^2$$
- The dispersion relation becomes:
$$k_r^2 + k_a^2 = (\frac{4 \pi f}{c})^2$$
##### SAR Data in the Frequency Domain
- We recall the phase of the returned signal:
$$\phi(f, \eta) \approx - \frac{4 \pi f}{c} R(\eta)$$
- After demodulation near $f_c$ and range compression we can write:
$$S(\eta, f_b) \propto P(f_b)e^{-j \frac{4 \pi (f_c + f_b)}{c} R(\eta)}$$
- Moving to 2D frequency where we take the 1D fourier transform in azimuth time:
$$S(f_b, f_a) = \int{S(\eta, f_b),e^{-2j\pi f_a \eta}} ~d\eta$$
##### Idea of Omega-K
- Transforms data to $(k_r, k_a)$
- Uses the dispersion relation to map the measured data onto the scene spatial frequency domain.
- Apply a 2D phase compensation
- Inverse FFT to obtain the image.
$$Image(r) \approx \int \int S(f_r f_a)e^{+j \phi_{prop}(f_r,f_a;r )}~df_r df_a$$
##### Narrowband Omega-K:
1. Range Compression
	- This is done by matched filtering
	- FFT over $\tau$ to get $S(f_r, \eta)$
2. Azimuth FFT
	- We compute the azimuth FT to get $S(f_r, f_a)$ 
	- Now the data naturally lives in $(f_r, f_a)$.
	- The ideal data satisfies a relation that is equivalent to the dispersion relation.
$$\phi(f_r,f_a) \approx -\frac{4\pi R_0}{c}\sqrt{(f_c + f_r)^2 - (\frac{cf_a}{2v})^2}$$
	- This is the wideband 2D phase.
3. Narrowband approximation
	- With the narrowband approximation, we freeze at $f_c$.
	- The dependence on $f_r$ inside the square root is linearised, and $f_c$ is used in place.
4. Stolt interpolation:
	- For a given target, its contribution in $(f_r, f_a)$ spce lies along the curve defined by dispersion relation. 
	- The data is remapped onto a uniform grid in spatial frequencies via stolt interpolation.
	- This removes the range migration
- The dispersion relation maps from the measured domain $(f_r, f_a)$ to scene spatial frequencies $(k_x, k_y)$.
- We start with the measured data $S(f_r, f_a)$, whose phase encodes the true geometry.
- We want to interpret these data as samples of the scenes fourier transform in spatial frequencies $(k_x, k_y)$.
- The dispersion relation tells us for a given $(f_r, f_a)$, the corresponding spatial frequencies magnitude is $k_{eff}(f_r, f_a).$
- The Omega-K algorithm uses this to remap the data onto the grid where the coordinates represent linear spatial frequencies, so the phase is a simple linear function so the 2D inverse FFT over the grid directly yields
#### Backprojection
- Backprojection is a time-domain SAR image formation method that:
	- Uses the exact range geometry between radar and each image pixel for each pulse.
	- Applies the corresponding time-delay alignment and phase correction to the data.
	- Sums contribution from all pulses to get pixel reflectivity.
- Frequency domain rely on narrowband approximations for simplicity, separability and efficiency while backprojection uses no such approximations and directly implements the physics based inverse.
- This means BP is more accurate, flexible but more computationally expensive.
- For each image pixel, backprojection collects all the energy from all pulses that would have come from that pixel, applies the correct phase, and sums them. 