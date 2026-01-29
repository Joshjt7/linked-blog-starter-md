### FMCW Model
*Currently, the [[FMCW]] model is not wideband, present the wideband model in FMCW SAR.*
- First we consider the transmitted signal:
$$s_t(t) = \exp(j2\pi f_c t+j\pi K_r t^2)$$
	where $f_c$ is the carrier frequency, $K_r = B/T_r$ is the modulated frequency slope rate, $B$ is the signal bandwidth, $T_r$ is the signal frequency sweep period.
- The transmitted signal is a delayed version of the transmitted signal:
$$s_r(t) = \exp(j2\pi f_c (t-\tau) + j\pi K_r (t-\tau)^2)$$
	where $\tau$ is the echo delay.
$$\tau = \frac{2R(t,\eta)}{c} = \frac{2\sqrt{R_0^2 + v^2(t+\eta)^2}}{c}$$
- The de-chirped IF echo signal is obtained after receiving echo mixing with the sending signal:
$$s_{if} = \exp(-j2\pi K_r \tau t)\exp(-j2\pi f_c \tau)\exp(j\pi K_r \tau^2)$$
	the first exponential term is the phase information in the range direction of the target. The second exponential is the doppler phase history in the azimuth direction, and the third exponential term is the residual video phase.
---------
- Under the conditions of large bandwidth and FMCW, the range walk during the pulse duration can’t be neglected, so that a modifiedk algorithm is adopted.
- The delay time can be written as:
$$\tau = [R(t+\tau) + R(t)]/c$$
	where $R(t)$ is the instantaneous slant range of total time variable $t$.
- The delay time can be calculated as:
$$\tau = 2\delta[\frac{R(t)}{c}+\frac{v^2}{c^2}(\eta + t')]$$
	where $\eta$ is azimuth time variable and the Doppler factor $\delta$ is defined as $\delta$ as $\delta = \frac{1}{1-\frac{v^2}{c^2}}$. The beat signal can be written as:
$$s_{beat}(\eta, t', f_r) = \sigma \exp(-j4\pi \delta(f_c + f_r)[\frac{R(\eta + t')}{c} + \frac{v^2}{c^2}(n+t')])$$
- Applying the FT with respect to the time variable $\eta$ to obtain the PTRS. The phase is:
$$\Phi(f_a,f_r) = \frac{4\pi \delta R_0}{c}\sqrt{(f_c + f_r)^2 - [\frac{v}{c}(f_c+f_r+\frac{cf_a}{2\delta v})]^2}-2\pi f_a \frac{f_r}{K}$$
- Compared to the pulsed SAR, the 2-D spectrum has additional range–azimuth coupling term and range walk term which are introduced by the variation of the slant range during the long pulse duration

### UWB FMCW Signal Model
- The platform trajectory as a function of slow time $t_p$:
$$r_p(t_p) =\begin{bmatrix}x_p(t_p) \\y_p(t_p)\\h\end{bmatrix}$$
- The baseband complex envelope:
$$s_{tx}(t) = \exp\{j2\pi(f_xt +\frac12\mu t^2)\}$$
- For a point $\textbf{r}$, the propagation delay can be written as:
$$\tau(t_p;x,y) = \frac{2R(t_p;x,y)}{c}$$
- The received baseband signal:
$$s_{rx}(t,t_p;x,y)\approx\sigma(x,y)s_{tx}(t-\tau(t_p;x,y))$$
$$s_{rx}(t,t_p;x,y)=\sigma(x,y)s_{tx}(t) = \exp\{j2\pi(f_x(t-\tau(t_p;x,y)) +\frac12\mu (t-\tau(t_p;x,y)^2))\}$$
- De-chirping is performed which involves mixing with a replica of the transmitted chirp
$$s_{bb}(t,t_p;x,y)=s_{rx}(t,t_p;x,y)s^*_{tx}(t)$$
- We get the beat signal:
$$s_{bb}(t,t_p;x,y) = \sigma(x,y)\exp(-j2\pi \mu \tau(t_p) t)\exp(-j2\pi f_c \tau(t_p))\exp(j\pi \mu \tau(t_p)^2)$$
- The total dechirped baseband signal is obtained by integrating over the scene:
$$s_{bb}(t,t_p;x,y) = \int\int\sigma(x,y)\exp(-j2\pi \mu \tau(t_p;x,y) t)\exp(-j2\pi f_c \tau(t_p;x,y))\exp(j\pi \mu \tau(t_p;x,y)^2)$$
- Substituting with the two way delay:
$$s_{bb}(t,t_p;x,y) = \int\int\sigma(x,y)\exp(-j\frac{4\pi \mu}{c} R(t_p;x,y) t)\exp(-j\frac{4\pi f_c}{c} R(t_p;x,y))\exp(j\frac{4\pi \mu}{c} R(t_p;x,y)^2)$$
	- This is a continuous time-wideband FMCW SAR forward model
- In frequency-domain:
$$S_{rx}(f;t_p,\textbf{r}) = S_{tx}(f)H(f;t_p,\textbf{r})$$
	- Where $H$ denotes the transfer function.
$$S_{rx}(f;t_p) = \int\int \sigma(x,y)S_{tx}(f)\exp\{-j2\pi k(f)R(t_p;x,y)\}$$
	- With $\lambda(f) = \frac{2\pi}{k(f)}$ 
- Narrowband assumptions may use $k(f) \approx k_c$.
- In UWB, we have frequency dependent PSF. Range migration depends on frequency and PSF differs per frequency.
- Severe range azimuth coupling.
- Including stop and go requires $R(t_p+t;x,y)$. 
- For a chirp of duration $T_c$ and platform speed $v$, motion during the sweep is:
$$\Delta x \approx vT_c$$
- The scattering function may display possible frequency dependence.
$$\sigma(x,y;f)$$
- The two-way propagation delay from transmit at time $t'$ to target $\textbf{r}$ and back to the platform at $t$ satisfies:
$$t-t'=\tau(t,t';x,y)$$
- For monostatic radar:
$$\tau(t,t';x,y) = \frac{2}{c}R(\frac{t+t'}{2};x,y)$$
- A scatterer at $(x,y)$ sees the transmitted waveform delayed by $\tau(t,t';x,y)$ and scaled by $\sigma(x,y;f)$. In the single-scatter, single-bounce, scalar approximation. the received baseband signal is:
$$s_{rx}(t) = \int\int \sigma(x,y)s_{tx,p}(t-\tau_{eff}(t;x,y))a(t;x,y)~dxdy$$
	where $\tau_{eff}(t;x,y)$ is the effective two way delay and $a(t;x,y)$ includes amplitude spreading.
- The exact FMCW receive model is:
$$s_{rx}(t_p+\tilde{t})=\int\int \sigma(x,y)A_{tx}(\tilde{t}-\tau)$$
- In FMCW processing we mix the received signal with a replica of the transmitted chirp:
$$s_{bb}(\tilde{t},t_p) = \int\int\sigma(x,y)A_{tx}(\tilde{t} - \tau_{eff})A_{tx}(\tilde{t})a(t_p+t;x,y)\exp(j\phi_{tx}(\tilde{t}-\tau_{eff})-j\phi_{tx}(\tilde{t}))~dx ~dy$$
- Substituting phase and neglecting amplitude envelopes:
$$s_{bb}(\tilde{t},t_p)$$
- Received baseband signal:
$$s_{\text{rx}}(t) = \int\int\sigma(x,y;f)A_{tx}(\tilde{t}-\tau_{\text{eff}})a(t;x,y)\exp\{j2\pi[f_c(\tilde{t}-\tau_{eff}+\frac12\mu(\tilde{t}-\tau_{eff})^2]+j\phi_{NL}(\tilde{t}-\tau_{eff})\}~dx~dy$$
- Considering the range compressed signal:
$$S_R = \int s_{dc}(t,\eta)e^{-j2\pi f_r t}dt$$
$$=T_p~\text{sinc}[T_p(f_r - k_r\tau)]e^{j\pi \Phi_{rc}}$$
$$\Phi_{rc}=\frac{2k_r R T_p}{c_0}-f_r T_p+\frac{4k_r R^2}{c_0^2}+\frac{4f_0 R}{c_0}-\frac{4f_R}{c_0}$$
### Wideband Model
- Wideband nature comes from how you treat the dependence of the spatial wavenumber and range over the band.
- Spatial phase carries the full frequency dependence across the bandwidth.
### UWB Challenges
*Present [[UWB SAR Challenges]] in a mathematical manner to fully convince yourself that these challenges exist.*
- Consider range-azimuth coupling and range migration effects.
### Inverse Model
*Formulate the inverse model with [[Compressed Sensing]] knowledge*


### References

[Low Cost UWB X-Band LFMCW SAR]


I am doing some research into FMCW UWB SAR, and I am looking at trying to form the wideband signal model. I recognise the challenges observed in UWB SAR such as severe range-azimuth coupling, frequency dependent doppler and range migration. Furthermore, I recognise that FMCW SAR may well invalidate stop-and go, leading to further complexities in the signal. I see in the literature that the intermediate frequency/beat signal can be written along the lines of s_{if} = \exp(-j2\pi K_r \tau t)\exp(-j2\pi f_c \tau)\exp(j\pi K_r \tau^2), but I fail to see how the standard model is narrowband, and how I can explicitly show the wideband signal model, and then mathematically show the challenges faced in UWB SAR. I understand that the important parts to consider are the changing wavelength across the chirp, and factors that affect the amplitude such as the frequency dependent scattering effects, but these effects on the amplitude are not the important ones. My question is, how should the signal be presented that fully encapsulates the wideband dynamics. Answer the question from the perspective of a UWB SAR practitioner, looking to share the knowledge.