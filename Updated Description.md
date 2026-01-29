To, Joshua

Sorry for errors in my original project description.

Below is an updated list of some suggested readings that may help you get started. Please pay particular attention to the end section of the third reference, which explicitly discusses model-based deep learning techniques.

It would be great if you could develop a brief project plan based on these materials. The intended application scenario is aligned with what is discussed in the third and last references. The purpose of this exercise is to assess your ability to grasp fundamental concepts and identify new opportunities for your project.

Please keep me updated on your progress using our project meetings — both in understanding the materials and in developing your own ideas and plan.

Best wishes,

Wei

Synthetic Aperture Radar (SAR) is widely recognized for its ability to generate high-resolution images independent of weather or lighting conditions. The resolution of a SAR system is strongly tied to its operational bandwidth: while conventional systems use moderate bandwidths to achieve meter-level resolution, ultrawideband (UWB) operation enables sub-meter or even centimeter-scale imaging. At the same time, SAR achieves azimuth resolution by exploiting Doppler information, which is intrinsically frequency dependent. In the UWB regime, Doppler frequency shifts become significantly coupled with the signal bandwidth, introducing new challenges in image formation and focusing. This creates a fertile research direction: conventional narrowband algorithms are no longer optimal, and new signal processing strategies are required to unlock the full potential of UWB SAR. For a student project, this provides the opportunity not only to explore high-resolution imaging but also to innovate in algorithm design, with genuine potential for publishable outcomes in the SAR community.

The project will begin with a theoretical study of SAR imaging geometry and the role of frequency in Doppler-based azimuth resolution. Building on this foundation, the student will design and implement novel processing approaches for UWB SAR, such as frequency-dependent focusing techniques, wideband Doppler compensation, or adaptive reconstruction methods. Simulations in Julia will be used to validate the proposed algorithms, supported by experiments on synthetic datasets. By directly addressing the fundamental issue of Doppler–frequency coupling in ultrawideband SAR, the project will both strengthen the student’s technical expertise and create a strong platform for producing original results suitable for conference or journal publication.

---

### **RF Sensing Basics**

* **Iovescu, Cesar, and Sandeep Rao. “The Fundamentals of Millimeter Wave Radar Sensors.” Texas Instruments (2020): 1–7.**  
  This article introduces the operation principles of millimeter-wave (mmWave) radar sensors, explaining how range, velocity, and angle are extracted from FMCW signals. It emphasizes the technology’s benefits—such as high precision, compact size, and robustness—for automotive and industrial applications.

* **Rao, Sandeep. *MIMO Radar.* Texas Instruments. [[https://www.ti.com/lit/an/swra554a/swra554a.pdf](https://www.ti.com/lit/an/swra554a/swra554a.pdf)**](https://www.ti.com/lit/an/swra554a/swra554a.pdf]\(https://www.ti.com/lit/an/swra554a/swra554a.pdf\)** "https://www.ti.com/lit/an/swra554a/swra554a.pdf](https://www.ti.com/lit/an/swra554a/swra554a.pdf)**")  
  This note explains the basics of Multiple-Input Multiple-Output (MIMO) radar, which uses multiple transmit and receive antennas to create a virtual array for enhanced angular resolution. It discusses key implementation aspects including antenna design, waveform orthogonality, and signal processing techniques.

* **Rao, Sandeep, Rajan Narasimha, and Shunqiao Sun. “Signal Processing Challenges in Automotive Radar.” *ICASSP 2025 – IEEE International Conference on Acoustics, Speech and Signal Processing (ICASSP).* IEEE, 2025.**  
  The paper identifies major challenges in automotive radar signal processing, including interference mitigation, high-density scene analysis, and sensor fusion. It highlights the need for advanced algorithms to handle large data volumes from high-resolution MIMO radar systems.

---

### **Synthetic Aperture Radar (SAR)**

* **Moreira, Alberto, et al. “A Tutorial on Synthetic Aperture Radar.” *IEEE Geoscience and Remote Sensing Magazine* 1.1 (2013): 6–43.**  
  This comprehensive tutorial presents the fundamental principles of SAR imaging, including data acquisition, focusing algorithms, and geometric considerations. It also surveys advanced techniques such as polarimetric and interferometric SAR for Earth observation and terrain mapping.

* **Montuori, Antonio, Fabio Rocca, and Deodato Tapete. “Multi-Frequency SAR Surveys: Possibilities and Applications.” *IGARSS 2022 – IEEE International Geoscience and Remote Sensing Symposium.* IEEE, 2022.**  
  The study investigates how multi-frequency SAR systems enhance surface and subsurface characterization. By combining data from different frequency bands, it demonstrates improved sensitivity to target features and wider applicability in environmental and geoscientific monitoring.