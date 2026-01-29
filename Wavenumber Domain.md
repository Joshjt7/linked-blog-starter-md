- $k$ is the spatial frequency measured in $rad~m^{-1}$, and is often denoted by the wavenumber:
$$k = \frac{2 \pi f}{c } = \frac{2\pi}{\lambda}$$
- By definition, we get the dispersion relation in the general case:
$$\omega^2 = c^2 k^2$$
- For SAR, due to two way travel the effective wavenumber is:
$$k_r = \frac{4 \pi f}{c}$$
- In 2Dm the dispersion relation becomes:
$$k_r^2 + k_a^2 = (\frac{4 \pi f}{c})^2$$
Where $k_r$ denotes the range wavenumber and $k_a$ denotes the azimuth wavenumber.

### Relation to Omega-K algorithm:
- After demodulation and range compression, we get a signal in terms of range frequency $f_r$ and azimuth time $\eta$.
- We take the Fourier transform in azimuth to get:
$$S(f_r, f_a)$$
- We want to relate our frequencies to the wavenumber.
- They can be related by the dispersion relation:
$$k_r^2 + k_a^2 = (\frac{4 \pi(f_c + f_r)}{c})^2$$
- For a point at slant range $R_0$, the phase in the 2D frequency domain is roughly:
$$\phi(f_r, f_a) = -R_0~k_{eff}(f_r, f_a)$$
	where
$$k_{eff}(f_r, f_a) = \sqrt{k_r^2 + k_a^2}=\sqrt{(\frac{4 \pi (f_c + f_r)^2}{c})}$$
- This is then often re-written in the useful form:
$$\phi(f_r, f_a) = -\frac{4 \pi R_0}{c} \sqrt{(f_c + f_r)^2 - (\frac{cf_a}{2v})^2}$$
- This is the distance multiplied by the effective wavenumber.
- This is some of the key theory behind the Omega-K algorithm.
- The Omega-K algorithm uses this data to remap the data onto a grid where:
	- The coordinates correspond to linear spatial frequencies.
	- The phase is a simple linear function.
	- A 2D inverse FFT directly yields the function.

### Note on Narrowband and UWB
- Up to this point for the derivation of the phase term, no narrowband assumptions have been used to get there
- A frequency narrowband assumption used later on:
	- The term inside the square root can be simplified to:
	$$(f_c + f_r)^2 \approx f_c^2 + f_cf_r$$
	- We also treat 
	$$f_c^2 >> (\frac{cf_a}{2v})^2$$
	- This leads to a Taylor Expansion such as
	$$\sqrt{(f_c + f_r)^2 - (\frac{cf_a}{2v})^2}\approx f_c +  \frac{f_r}{1 - (\frac{cf_a}{2vf_c})^2} - \frac{(\frac{cf_a}{2v})^2}{2f_c} + ... \approx f_c + f_r - \frac{(\frac{cf_a}{2v})^2}{2f_c}$$
- In the UWB case:
	- $f_r$ is no longer a small perturbation around $f_c$
	- The curvature of the dispersion relation changes significantly across the band.
	- Using a truncated Taylor series misinterprets the true phase.
	- This leads to phase errors.

- Stolt Mapping