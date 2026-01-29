Feedback:
**Understanding of the problem and motivation**
  The interim report presents a reasonable problem formulation. The student demonstrates an understanding of the advantages and challenges of Ultra‑Wideband (UWB) FMCW SAR for high‑resolution imaging, and explains why conventional narrowband SAR processing techniques are not directly suitable in the UWB regime. The link from physical limitations to the need for new image‑formation algorithms is discussed, though this could be sharpened further as the work progresses.
**Proposed implementation and methodology**
  The proposed implementation in Chapter 3 provides a sensible planned starting point for the technical work. The formulation of UWB FMCW SAR image formation as a linear inverse problem and the construction of the forward operator H from the signal model are clearly laid out. The subsequent introduction of the subsampling operator and dictionary indicates a planned pathway towards compressed‑sensing and model‑based deep‑learning approaches based on the same physical model.
**Possible improvement: azimuth resolution**
  The azimuth resolution given in equation (2.3) depends only on the length of the antenna array. This expression is widely used in the literature but is derived under narrowband array assumptions (e.g. element spacing of half a wavelength). Since this project focuses on the wideband case, it is important to recognise that the normalised array size (normalised by half‑wavelength, which itself depends on frequency) varies across the band. I strongly recommend that the student revisit the azimuth‑resolution derivation with this in mind, and clarify how the expression should be interpreted in the UWB setting. A similar point has also been raised independently in Ziyu’s feedback.
**Possible improvement (recommended by Ziyu): narrative on technical challenges**
  The narrative in Section 2.2.1 would be clearer if the narrowband case were presented before the UWB case. For readability, it would be helpful to first derive the standard narrowband / pulsed (or narrowband FMCW) SAR signal model and the usual simplifications, and then explicitly identify which assumptions break down in the UWB regime and how the model must be modified. This ordering would make the “UWB challenges” story more coherent and easier for the reader to follow.
**Possible improvement: use case study**
  It is clear from the discussion that the virtual array size depends on the platform speed. I strongly recommend that the student carry out a concrete use‑case study: for a given frequency band (e.g. X‑band or the 76–81 GHz mmWave band), what range of platform velocities causes the commonly used narrowband theory and associated approximations to fail? Quantifying this would help to motivate the technical work more strongly and to make the UWB challenges more tangible.
**Possible improvement: the technical approach**
  Section 2.4.1 on compressed sensing, together with equations (3.1)–(3.5), gives the impression that the project may primarily follow a particular compressed‑sensing approach from the literature. Although equation (3.3) already incorporates a UWB SAR signal model, it is not yet clear how the proposed approach directly addresses the unique challenges of UWB SAR beyond adopting a forward model.
  It may be helpful to structure the technical goals in a step‑by‑step manner: 
  1. Based on the use‑case study, first formulate the inverse problem without sparsity assumptions or subsampling, and analyse the challenges in solving it. In particular, clarify whether a direct FFT‑based solution (as in conventional SAR) is possible, and if not, why.
  2. Develop an efficient algorithm that exploits FFT or related structure wherever possible to accelerate the solution of this full‑data inverse problem. 
  3. Then assume that the SAR image is sparse in some transform domain (e.g. the waveform transform used in coursework) and investigate how to reformulate the problem and solve it efficiently under this sparsity prior. 
  4.  Only after these steps, consider whether measurement undersampling is practical in the chosen use case and, if so, how to design and solve the corresponding compressed‑sensing problem efficiently. 
This staged approach would help to define a clearer, UWB‑specific contribution rather than primarily implementing an existing CS framework.
Other possible improvements
  In Ziyu’s independent feedback, several additional detailed suggestions were made. I would encourage the student to discuss those points directly with Ziyu, as they may help refine both the theoretical treatment and the eventual implementation strategy.
Wei

Key points:
- Sharpen the link between physical limitations and the need for new-image formation algorithms.
- Formula of the azimuth resolution should be re-derived. Current formulation is derived under the narrowband conditions.
- Carry out a case study (X-band or 78-81 GHz mmWave band). Quantify where the challenges lie to make the work more tangible.
- The technical goals could follow a path of:
	1. First formulate the inverse problem without sparsity or subsampling and analyse the challenges in solving it. Key her is forming the inverse problem without sparsity. This should involves clarity in whether a FFT based solution is possible, and if not, why. 
	2. Develop an efficient algorithm that exploits FFT or related structure to accelerate the solution.
	3. Next, assume the SAR image is SAR image is sparse in some transform domain and investigate how to reformulate the problem and solve it efficiently with the sparse prior.
	4. Then consider if the under sampling is practical, and if so, how do we solve the problem.

