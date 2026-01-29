←[[Presentation]]
→[[UWB Considerations]] 

## Key Points
- Range to a target:
$$r = \frac{c\Delta t}{2}$$
- Range Resolution:
$$\delta_r = \frac{c}{2B_r}$$
- Azimuth Resolution:
$$\delta_a = R_0\frac{\lambda}{2L_{sa}}\approx \frac{d_a}{2}$$
### Pulsed SAR
- Range equation:
$$R(\eta) = \sqrt{R_0^2 + V_r^2 \eta^2} \approx R_0 + \frac{V_r^2\eta^2}{2R_0}$$
- Azimuth Frequency:
$$f_D = \frac{2V_r^2f_c}{cR_0}$$
- Demodulated baseband signal:
$$    s(\tau, \eta) = A_0w_r(\tau - \frac{2R(\eta)}{c})w_a(\eta - \eta_c)e^{-j\frac{4\pi f_c R_0}{c}}e^{-j\pi \eta^2 \frac{2V_r^2f_c}{cR_0}}e^{j\pi K_r{[\tau - \frac{2R(\eta)}{c}]^2}}$$
- Range migration :
$$    R(f_\eta) = R_0 + \frac{\lambda^2 R_0}{8V_r^2}f_\eta^2$$
- Full phase:
$$    \theta_a(f_\tau, f_\eta) = -\pi \frac{f_\tau^2}{K_r} - \frac{4\pi R_0}{c}\sqrt{(f_c + f_\tau)^2 - (\frac{cf_\eta}{2V_r})^2}$$
- Migration Factor:
$$    D = \sqrt{1-\frac{c^2 f_\eta^2}{4V_r^2 (f_c + f_\tau)^2}}$$

### FMCW SAR
- Range encoded as the beat frequency $f_b(\eta)$ as opposed to time delay.
- Validity of stop and go:
$$R(\eta,\tau) \approx R(\eta) + \frac{V_r^2\eta}{R(\eta)}\tau$$
- Beat Signal:
$$s(\tau,\eta) = \exp(-j\frac{4\pi R}{\lambda})\exp(-j\frac{4\pi RK_r \tau}{c}+j2\pi f_d \tau)\text{exp}(j\frac{4\pi K_r}{c^2}R^2)$$
- Doppler and beat frequency become tightly coupled
## Resources

[Tutorial on Synthetic Aperture Radar](https://skynet.ee.ic.ac.uk/notes/Radar_10a_other_Radar_2pageformat_with_SARtutorial.pdf)
[Digital Processing of Synthetic Aperture Radar Data](file:///C:/Users/josh5/Downloads/DigitalProcessingofSyntheticApertureRadarData_AlgorithmsandImplementation-ArtechHouse2005%20(4).pdf)
[Synthetic Aperture Radar: Systems and Signal Processing]()



