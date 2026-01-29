
### Radar
- Radar in the general sense involves sending pulses towards a given towards a target. A key metric in radar is the time delay, or the round trip time. This is the fundamental aspect that allows us to detect the range of a radar.
### Synthetic Aperture Radar
- The range resolution is dependent on the bandwidth of the signal. A larger bandwidth gives a larger range resolution providing motivation for radar systems that utilise larger bandwidth.
- The azimuth resolution can be derived to be determined only on the length of the antenna. A small antenna results in a larger synthetic aperture, giving finer range resolution. This is an interesting result, since the azimuth resolution is independent of many of the important system parameters of a radar system.
- The fundamental property which defines SAR is a given point target can be viewed from many different positions, which effectively simulates the effects of a large synthetic aperture. This coherent summation of energy from different positions is what results in a improved azimuth resolution compared to other radars such as RAR.
- A key point in SAR is the effect of range migration. Range migration is the effect where the energy from a given target is spread over many range bins, which leads to degradation in image quality if left uncorrected. Dealing this forms a key part of SAR processing.
- SAR can employ either pulsed of continuous wave (CW) modes of operation. These different modes have different properties. FMCW is often the chosen mode for compact systems such as UAVs due to the lower power requirements. Pulsed radar and FMCW have slightly different ideas behind them.

#### Pulsed SAR
- For pulsed SAR, FM or chirp pulses are sent according to the PRI. The time delay encodes range, while the phase encodes azimuth position. The phase can also be refereed to as the azimuth chirp, and is it analogous to the doppler frequency which arises due to the motion of the radar platform.
- In the expressions of the signal model, varying assumptions and approximations are used in order to derive simplified expressions. These approximations are often valid in the low squint and narrowband cases, but the validity may need to be carefully considered when moving to other modes of SAR operation, such as UWB SAR.
- The assumptions include the approximated form of the range equation and the narrowband assumption. These result in a simplified expression for range migration and allow for range and azimuth decoupling. Range and azimuth decoupling is key for algorithms such as the range-doppler algorithm since it allows for independent processing of the range and azimuth data.

#### FMCW SAR
- FMCW SAR involves the continuous transmission of the chirp signal, whereas pulsed radar transmits at regular intervals, and between transmissions, the receiver waits for the return.
- FMCW can add additional considerations when compared to pulsed SAR. The two of these are not directly analogous to one another.
- The FMCW signal is transmitted, and the received signal is a time delayed version of the transmitted signal.
- FMCW systems often employ a de-chirp on receive, which involves mixing the received signal with a replica of the transmitted chirp. This results in the beat signal or the intermediate frequency signal.
- In FMCW, the validity of the stop and go assumption needs to be considered. Th stop and go assumptions effectively states that the platform of the radar remains approximately stationary during the transmission of the pulse. If this is concluded to not hold, the range equation as a function of both fast and slow time needs to be considered.

### Current SAR Processing:
- Conventional SAR processing algorithms are based on frequency domain approaches. They combine Fourier transforms with matched filtering in some combination. They then employ some method in order to correct range migration. 
- For UWB SAR, these approaches are not always optimal. They perform well on conventional/narrowband SAR applications where the trade-off between efficiency and accuracy is appropriate. The breakdown of fundamental assumptions in UWB case often mean these conventional approaches are no longer appropriate.

### Novel SAR Processing techniques
- Alternative methods to SAR processing need to be explored in order to find methods that can be suitable for UWB applications. The leading approaches that are to be considered are compressed sensing, deep learning or model-based deep learning.
- Compressed sensing is one of the leading and most researched alternative methods of SAR processing. To guarantee high-resolution SAR image, a high sampling rate is mandatory according to the traditional Nyquist sampling theorem. CS allows for an attractive alternative which can produce complete recovery of the original signal with fewer measurements than the Nyquist rate.
- Other methods have been presented in the literature, such as pure 'black-box' deep learning techniques which go from the raw SAR data to the image. These have specific challenges relating to the need of huge amounts of data and issues regarding generalisation.


