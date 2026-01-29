### L1: Imaging Radar and its Applications

- Radar (Radio Detection and Ranging) is an instrument whose fundamental measurement is the distance from a sensing antenna to an object.

#### Fundamental Process of Radar
- The radar transmits a pulse at time $0$, which propagates a distance $r$ to the surface, and also back to the radar. Therefore the total distance travelled is $2r$. For a signal that travels at the speed of light $c$, the total round trip time is given by $$\tau = \frac{2r}{c}$$
- This can also be rearranged for distance to get $$r = \frac{c \tau}{2}$$
- We define the key terminology of range (across-track) and azimuth (along track). Consider a airborne radar. The area of the surface which is parallel to the direction of travel of the radar is called the azimuth (along track) and the direction of the surface perpendicular to the direction of the radar is called the range (cross track).


### L2: The Radar Equation

- The quality of the radar measurements depends on the combination of radar system parameters, imaging geometry, and surface characteristics.
- All forms of the radar equation yield some form of the quality of the radar measurement in terms of the signal to noise ratio.
	- The power received in the absence of the scattering object is the noise, denoted by $P_n$.
	- If there is a scatterer present, we add the signal power $P_S$ so the total power received in this case is $P_s + P_n$.
- We define the SNR as such $$SNR = \frac{P_s}{P_n}$$
	- For imaging radar, we want to achieve a SNR of at least 10, however, levels of 100 to 1000 can sometimes be achievable.

#### Derivation of the Radar Equation
- We suppose the transmitted generates a pulse with transmit power $P_t$. We consider the power density on a sphere of radius equal to the distance from the radar to the scatterer $R$. $$Power ~Density = \frac{P_t}{4 \pi R^2}\frac{\omega}{m^2}$$
- In this case, the power is not used very efficiently since the object that we want to measure fills only a very small fraction of the total surface area. Hence, we use an antenna that concentrates most of the energy in a single direction, ideally towards the object. The degree of concentration is the directivity gain $G$. 
- We consider the given relation, note $A$ denotes the antenna area. $$\delta = \frac{4 \pi A}{\lambda^2}$$
### L3: Imaging Radar Geometry

- We define the radar as moving with a velocity $v$ which is in the $x$ direction. We consider the range to a point on the ground at $(x,y,-z)$. $$r = \sqrt{x^2 + y^2 + z^2}$$
- The beamwidth of the range pattern is $\frac{\lambda}{w}$ where $w$ is the width of the antenna. The azimuth beamwidth is given by $\frac{\lambda}{l}$ where $l$ is the length of the antenna.
- The look angle which we denote as $\theta$ is the angle between the vector pointing straight down below the radar, to the point $P$ that we are observing. 
- During approximations where we consider the earth to be flat, the look angle is said to be equal to the incidence angle. This approximation is true for airborne radars, but cannot be used in the case for spaceborne radars. We note the important relations.
$$sin(\theta) = \frac{y}{r}$$
$$cos(\theta) = \frac{z}{r}$$
#### Mapping a Swath:
- The swath refers to the strip of the earths surface which is imaged by the radar as it moves across the flight path.
- The distance $y$ to the centre of the swath is: $$y_{center} = \sqrt{r^2_{center} - z^2}$$
	- Using the definition of $sin(\theta)$ and $cos(\theta)$ with our geometry we have:
$$y_{center} = r_{center}~sin(\theta) = \frac{z~sin(\theta)}{cos(\theta)} = z~\tan(\theta)$$
- We can then define similar relations for $y_{near}$ and $y_{far}$.
$$y_{near}=z~tan(\theta - \frac{\lambda}{2w})$$
$$y_{far}=z~tan(\theta + \frac{\lambda}{2w})$$
- With all these formulations, we can define the swath width as $y_{near} - y_{far}$ $$=z[tan(\theta + \frac{\lambda}{2w})-tan(\theta - \frac{\lambda}{2w})]$$
- In the case where the swath narrow:
$$=\frac{z~\frac{\lambda}{w}}{cos^2(\theta)}$$
- In order to find the size of the illuminated area, we can calculate the product of the swath width and the azimuth beamwidth:
$$=\frac{z~\frac{\lambda}{w}}{cos^2(\theta)}*\frac{r \lambda}{l}$$
- The antenna for a radar system does not always point broadside to the platform. Broadside means the line of sight of the radar is perpendicular to the direction of travel. The amount of deviation from broadside is called the squint. Positive values indicate forward squint while negative angles indicate backwards squint. Squint angle is denoted by $\phi$.
$$sin(\theta)=\frac{\sqrt{x^2 + y^2}}{r}$$
$$cos(\theta) = \frac{z}{r}$$
$$sin(\phi)=\frac{x}{\sqrt{x^2 + y^2}}$$
- We can also define a composite squint angle which combines these angles where $sin(sq) = sin(\theta)sin(\phi)$ $$=sin(sq) = \frac{x}{r}$$
#### Spherical Earth Constructions 
- In the cases of spaceborne radar, the spherical nature of the earth needs to be accounted for.
- We use our new geometric model and the laws of spherical trig. We get the following results:
$$cos(\theta) = \frac{r^2+(z+r_e^2)^2-r_e^2}{2r(z+r_e)}$$
$$\frac{sin(\beta)}{r}=\frac{sin(\theta)}{r_e}$$
### L4: Pulse Imaging Radar form of the Radar Equation
- Recall the projected range beamwidth (swath):
$$=\frac{z \lambda}{w~cos^2(\theta)}=\frac{r\lambda}{w~cos(\theta)}$$
- Also the projected azimuth beamwidth:
$$=\frac{r \lambda}{l}$$
- This gives the resulting area:
$$Area=\frac{r^2 \lambda^2}{lw~cos(\theta)}$$
#### Projected Pulse in Scattering Area
- As the true reflectivity distribution in time is convolved with the transmit pulse, at any given time in the echo we are receiving energy from more than one point of the ground.
- Hence, the size of the scattering area in the range direction contributing to the echo at any given time is the length illuminated by one pulse length, projected onto the ground.
- For a pulse $\tau$ in time, the length in meters is $$\delta = \frac{c \tau}{2}$$ and on the ground. $$\delta_{gnd} = \frac{c \tau}{2 sin(\theta)}$$
#### Resolution
- Resolution refers to the minimum distance in which two objects are distinguishable.
- We consider the range resolution.
$$\delta_{r} = \frac{c \tau}{2~sin(\theta)}$$
- For a pulse length of $\tau$ then the bandwidth can be given by approximately $1/\tau$.
$$\delta_r = \frac{c}{2~bw~sin(\theta)}$$
- We note that increasing the signal bandwidth decreases resolution. 

### L5: Range Modulation, Processing and Pulse Compression:
- We note that SNR of an imaging filter depends only on the energy of the transmit pulse which is the product of the pulse length and peak power, while the range resolution depends on pulse length.
- We have a design trade-off. To get fine resolution we want to transmit short pulses, but to obtain high SNR we wand very high peak power.

#### The Matched Filter
- Each point in a radars image reflects a version of the transmitted pulse back to the receiver. We would like to isolate the signal from its surrounding noise and measure its amplitude accurately.
- A matched filter is one with the conjugate response of the transmitted signal.
- Suppose our radar transmits a waveform $s(t)$. The echo received at the echo is a scaled version of that plus noise:
$$r(t)=\alpha s(t - \tau)+n(t)$$
- The impulse response of our filter which is the matched filter is given by:
$$h(t) = s^* (-t)$$

#### Chirps
- The most widely used range modulation is the so called chirp waveform. This consists of a a linearly swept frequency pulse. 
$$f(t) = st + f_0$$
where $s$ denotes the chirp slope and $f_0$ denotes the starting frequency.
- Phase is the integral of the angular frequency, so the phase for the chirp may be expressed as 
$$\phi(t) = 2\pi s \frac{t^2}{2} + 2\pi f_c t + \phi_0$$
$$\phi(t) = \pi s{t^2} + 2\pi f_c t + \phi_0$$
Where $\phi_0$ is some arbitrary constant of integration.
- Our transmitted waveform becomes:
$$s(t) = exp(-j~ [\pi s{t^2} + 2\pi f_c t + \phi_0])$$
- Since the range of frequencies is from $f_0$ to $f_1$, the bandwidth of the chirp is $f_1 - f_0$.

### L6: Practical Issues in Data Processing
- We have seen that we can describe an echo from a patch on the ground as a convolution of the actual surface reflectivity with the transmitted waveform.
$$s(t) = r(t) * b(t)$$
where $s(t)$ is the received signal, r(t) is the reference signal and $b(t)$ is the true image brightness distribution.
- We have also seen that the correlation of the signal with the reference signal obtains an image $i(t)$ that approximates $b(t)$
$$i(t) = s(t) * r(t)$$
- Very often the range processor of a radar system is called the correlator because its job is to correlate the received echoes with the known reference signals.

### L7: Other Range Processing Issues
- Consider the equation developed previously:
$$i(t) = b(t) * (r(t) \star r(t))$$
- The range impulse response can be given by:
$$= r(t) \star r(t)$$
- Or in the frequency domain
$$= R^*(s)R(s)=|R(s)|^2$$
For a chirp signal with a high time bandwidth product, and centred at 0 frequency, the spectrum is given by a rectangular function with width equal to the bandwidth.
- We recall that in frequency domain this is a $sinc$ function. This sinc function has a peak to null width of $1/BW$.
- The chirp improves compression by a factor of the time-bandwidth product, and generates sidelobes.
- The presence of sidelobes implies that a target will not only generate its main lobe response, but also a trail of sidelobes.
- We consider some of the properties on the $sinc$ function.
	1. Alternating sidelobes decreasing in amplitude.
	2. Evenly spaced sidelobes at unit spacing.
	3. Amplitude of a sidelobe is approximately: $\frac{-1}{2}$(amp of next sl + amp of previous sl)
- If we were to add to every sidelobe the average of the sidelobes on either side, then we would approximately cancel the sidelobes. We can do this by adding every sidelobe to the average of the values on either side. This can be done by doing a convolution with two $\delta$ functions. This operation is very simple when done in frequency domain.

### L8: I/Q vs Offset Video
#### Azimuth Resolution and Image Formation:
- We begin by looking at a real aperture system. In the case of the real aperture radar, we cannot distinguish scatterers at different along track position within the antenna beam
- Every time a EM wave propagates its wavelength, its phase advances by $2\pi$. We can relate range to phase
$$\phi(t) = \frac{4\pi}{\lambda}r(t)$$
- If the radars signal is not monochromatic (single frequency), then the phase will be less well defined. In our case, we can assume the modulation is small compared to its operating frequency, then we can treat the signal as if all its energy were concentrated at a single frequency.  This breakdown in the wideband case.

#### The Doppler Effect
- We consider a train travelling towards a stationary observer. Due to the trains motion towards you, each waveform is emitted a litter closer to the previous waveform than we would expect from the wavelength. The new wavelength $\lambda'$ is shorter by the amount the train travels in the time required for one wavelength
$$\lambda' = \lambda - v \Delta t = \lambda - \frac{v \lambda}{c}$$
where $c$ in this case denotes the speed of sound.
- We can get the following relation
$$\Delta f = \frac{2vu}{\lambda}$$

### L9: Doppler history and a point target
- We now consider the doppler frequency of a point at some location within our antenna beam.
- We recall the relation between velocity and doppler frequency:
$$f_d = \frac{2vu}{\lambda}$$
where $v$ is the velocity vector of the radar, and $u$ is a unit vector from the radar to the object.
- We want to express doppler in terms of our SAR geometry. The vector from the radar to the object $R$ is.
$$R=(x,y,z)$$
- We say that velocity is in the $x$ direction:
$$v=(v_x,y,z)$$
- Hence:
$$f_d = \frac{2}{\lambda}(v_x,y,z)\frac{(x,y,z)}{|R|} = \frac{2}{\lambda}v_x \frac{x}{|R|}$$
- Since $r = |R|$
$$f_d =  \frac{2}{\lambda}v_x \frac{x}{r}$$
- We want to relate our doppler frequency $f_d$ to our look and squint angles. Using results from [[Complete Notes#Mapping a Swath|Mapping a Swath]] we obtain:
$$f_d=\frac{2v}{\lambda}sin(\theta)~sin(\phi)=\frac{2v}{\lambda}sin(sq)$$
- We consider the implications of this for our imaging. We consider the illuminated part of a radar swath at one instant of time. Each vertical line denotes one range resolution element or range bin, obtained by processing the element in range.
- For a given energy bin $n$, the radar consists of energy from scatterers from many positions $P$ in azimuth. If we could distinguish among these, we could improve our resolution in the azimuth direction. We can distinguish these based on the formula for doppler frequency $f_d$.
- Hence by decomposing the echo from a given range bin into separate frequency components, we can solve for the squint angles and hence the positions of the various scatterers. This method in deriving azimuth is called the range-doppler mapping. It is equal to a technique called unfocussed SAR processing.

#### Implementation of Unfocused SAR algorithm
- Since we want to sort the energy from a range bin by frequency, a single way to generate the unfocused SAR image is to simply to calculate the fourier transform of each range bin.
- The platform is moving during the pulsing period, therefore not exactly the same illuminated by each pulse.
- The platform is in motion along the $x$ direction, so the value of $x$ is a function of time. We want to define a coordinate system which is fixed on the object and examine the range as the radar flies by.
- We define a time 0 in which the radar is closest to the point $P$. When the radar is at position at $x'$ this is given by $v$t.
- The range is then given by:
$$r(t) = \sqrt{(vt)^2 + y^2 + z^2}$$
- We define $r_0$ as the distance of the closest approach:
$$r(t) = \sqrt{(vt)^2 + r_0^2}$$
- We consider what the measured phase of the signal will be as a function of time:
$$\phi(t) = -\frac{4 \pi}{\lambda}r(t) = -\frac{4 \pi}{\lambda}\sqrt{(vt)^2 + r_0^2}
$$
This equation is known as the phase history of the scatterer at range $r_0$ and time $t$ = 0.
- We want to relate this to the doppler frequencies
$$f=\frac{1}{2\pi}\frac{d\phi}{dt}$$
$$f(t)=\frac{1}{2\pi}\frac{d}{dt}[-\frac{4 \pi}{\lambda}\sqrt{(vt)^2 + r_0^2}~] = -\frac{2}{\lambda}\frac{d}{dt}\sqrt{r_0^2 + (vt)^2}$$
$$=-\frac{2v}{\lambda}sin(\theta)~sin[(\phi(t))]$$
which is achieved after taking the derivative and simplifications.

### L10: Derivation of unfocussed processor resolution

### L11: The Doppler Centroid

- In many instances, the radar antenna is not pointed exactly broadside to the line of flight, we often dont know exactly where the antenna is pointed. This means we have some unknown squint angle.
- Consider an antenna squinted by some unknown angle $\phi$.
- We consider the plane in motion. At any point in time, the range bin $r_0$ contains scatterers ranging in doppler frequency from $f_{d2}$ t0 $f_{d1}$, which may or may not contain the broadside point $f_d = 0$.
- In the case where we have no squint angles, we have zero doppler when the antenna is broadside. We dont have this where have a squint angle.
- A simple method of estimating $f_d$ is to plot a spectrum of doppler frequency and numerically evaluate its centroid. However there are challenges associated with this
	1. The reflectivity may not be constant
	2. The $prf$ may be too low to eliminate wrap around of the spectra.
#### Average Phase Shift
- Another approach is to evaluate the average phase shift from line to line in azimuth. The largest signals will on average be those from the centre of the antenna beam, suppose we determine the phase shift from line to line in azimuth. The largest signals on average, will be those at the centre of the antenna beam. Suppose we determine the phase shift at each range bin from line to line in azimuth and weight by amplitude. After enough averaging the result will be dependent on the antenna beam pointing.

#### Relationship of Centroid to area Imagined
- Consider a patch illuminated by a squinted radar, and its range of doppler frequencies. We use the composite squint angle in this case. We map each location $x$ on the ground to frequency units.
$$f_d = \frac{2v}{\lambda}sin(sq)=\frac{2v}{\lambda}\frac{x}{r}$$
- Note that the return is weighted by the antenna pattern somewhat distorting the image. If we want to evaluate the image with an fft, the image consists of two pieces which need to be put together to form the full patch without any discontinuities. One way around this is to steer the image to zero doppler. This means to force the antenna beam to peak at 0 frequency as if the boresight was truly at 0. This is done by multiplying the azimuth signal by a complex carrier equal in frequency to the negative of the doppler centroid.
- Denote the sequence of azimuth values as $az(j)$
$$az'(j) = az(j)~e^{-j2\pi f_{centroid} i/prf} $$
#### A multi-look unfocussed processor
- We need a method to process patch by patch and overlay the looks to form a complete image.

I am looking to understand SAR theory. I am currently looking at processing in azimuth, and one think that slightly confuses me currently is the doppler centroid, especially what it is and why it is pivotal, as well as some of the fundamental parts of the doppler frequencies and doppler shift. My current understanding is that as we move towards and away from the target, the signal undergoes a doppler shift as a result of this motion. So is the position in which we are the closest to out target, a point of zero doppler, as in the signal undergoes no doppler shift. If this is the case, why does this occur? Furthermore, I want to ask about the cases in which the radar in not pointed directly broadside, as in there exists some squint angle. I am told in the case in which the radar is pointed broadside, we have s peak at the point of 0 doppler, at the point of closest approach, however, this is not the case when we have a positive squint for example.

### L12: Azimuth
- We once again consider our SAR geometry. By pythagoras we have:
$$r(t)=\sqrt{r_0^2+v^2t^2}$$
- In many cases we cases we assume that the antenna length $l$ is much greater than the wavelength.
$$r(t)=r_0 \sqrt{1 + \frac{v^2 t^2}{r_0^2}}$$
This is approximately equal to:
$$r_0+\frac{1}{2}\frac{v^2t^2}{r_0}$$
- We can then write:
$$\phi(t) = -\frac{4 \pi}{\lambda}[r_0+\frac{1}{2}\frac{v^2t^2}{r_0}]$$
- We can neglect the constant phase term:
$$\phi(t) = -\frac{2 \pi}{\lambda}\frac{v^2}{r_o}t^2$$
We note that the azimuth response of the radar echo is also a chirp function. 
$$f(t) = \frac{1}{2 \pi} \phi'(t) = -\frac{2v^2}{\lambda r_0}t$$
$$s = \frac{1}{2\pi}\phi''(t) = -\frac{2v^2}{\lambda r_0}$$

- Knowing the chirp rate, we can then apply the same kind of matched filter in azimuth that we used in the range processing operation. We can define a reference signal and correlate it against the distribution in azimuth resolution in azimuth.
- Now we can evaluate the resolution achievable by matched filter processing in azimuth. We know that the resolution will be reciprocal of the bandwidth. But we need to know what is our equivalent of the pulse length in azimuth. This is simply the time that the target is illuminated for by the antenna.
- So for velocity $v$ and azimuth beamdwidth $\frac{r_0 \lambda}{l}$ 
$$t_{az} = \frac{r_0 \lambda}{vl}$$
$$BW_{az} =  -\frac{2v^2}{\lambda r_0}~\frac{r_0 \lambda}{vl} = -\frac{2v}{l}$$
- Our resolution in seconds is:
$$\delta_t = \frac{l}{2v}$$
- Our resolution in meters is just $v~\delta_t$ 
$$\delta_{az} = \frac{l}{2}$$
- Therefore our azimuth resolution is independent of wavelength, velocity, range etc and is dependent entirely on the antenna length.

#### SAR Processing Algorithm
- We consider two sequences of complex azimuth samples. As these two bins are at different ranges, the reference matched filters are different in that the chirp slopes are inversely proportional to the range. Hence, a new reference signal is needed for each azimuth bin, rather than using the same one over again as was done in the range processing case.

#### Squinted Geometries
- The radar may be pointed at boresight, hence the majority of the energy many not come from the zero doppler location.
- $r_dc$ is the range from, the object to the radar at the time or location when the antenna goes through the antenna boresight. 
- In this situation, rather than being symmetrical about zero doppler, the azimuth frequency spectrum is shifted equal to the doppler centroid.

### L13: SAR Processing Algorithm:
- We have seen that the phase history of an azimuth point scatterer forms a chirp signal like the one we used for range modulation.
- The centroid represents a carrier frequency in which the chirp is imposed. The two important quantities for azimuth signal representations are the chirp rate $f_R$ and the doppler centroid $f_{DC}$.
$$f_R = -\frac{2v^2}{\lambda r_{DC}}$$
$$f_{DC} = -\frac{2v^2 t_{DC}}{\lambda r_{DC}}$$
### L14: Setting SAR Processing Parameters:

### L15: Range Migration:
- When we are processing in azimuth, we isolate the objects of a given range by implementing the matched filter along lines of constant ranges or range bins, in the range compressed image.
- The width of a range bin is the range spacing, or approximately, the range resolution of the system. 
- We want to consider what happens when the range history exceeds the widths of the range bin. This means that the energy from a given object would be spread over several bins, therefore using a single column matched filter will not be suitable. This is called range migration.
- We recall the form of range history:
$$r^2(t) = r^2_{DC} + v^2t'~^2+2v^2t_{DC}t'$$
We have both quadratic and linear term. In non-squinted geometries, the linear term goes to 0 since we have $t_{DC} = 0$. Sometimes the quadratic term is called range curvature, and the linear term is called range walk.
- This formula can be approximated as:
$$r(t) = r_{DC} + \frac{1}{2}\frac{v^2t'~^2}{r_{DC}}+\frac{v^2t_{DC}t'}{r_{DC}}$$
- Since the constant term does not change with time it can be ignored for now. We define the spacing in range as $\frac{C}{2f_s}$
- Migration will be larger for longer integration times and also for larger squint angles.
- We can try and visualise the migration in our picture of the range compressed data. This can be done by plotting the path taken by a scattering point as it makes it through the antenna beam. We have a parabolic range history.
- An approach to dealing with this problem involves predistorting the range compressed image. By shifting the rows of the matrix back and forth we can align the echo from a given reflector in a single column, thus we can read the data from that column and compress it with our SAR matched filter.
- While the range histories of the echoes are offset by different amounts in time, in the frequency domain all points at the same range go through identical frequency. All points start at the same doppler frequency, decrease at the same rate, and exit at the same doppler.
- Interpolation methods can also be used.






