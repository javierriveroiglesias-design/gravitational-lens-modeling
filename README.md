# gravitational-lens-modeling

Gravitational Lens Modeling of JWST Einstein Rings with PyAutoLens

Jupyter notebooks that model gravitational lenses from JWST NIRCam imaging and reconstruct the unlensed background source galaxy hidden inside each lensed image.

This was developed during a summer research internship as a Student Researcher II for the STEM Endowment at the University of La Verne and I still work on it during my free time.

What this project does

A massive foreground galaxy bends the light of a distant galaxy behind it, sometimes stretching it into arcs or a complete Einstein ring. What I've done for this project is it works backward from that distorted image.

The steps I took for this project which can be replicated:

Load real JWST imaging, a noise map, and a PSF for a lens system.
Mask the data around the lens and ring.
Fit a lens mass model and a source light model to the image using Bayesian nested sampling.
Use the best-fit mass model to trace the light back through the lens and reconstruct the source galaxy as it would look without lensing.
Lens systems modeled

All systems come from the COSMOS-Web Lens Survey (COWLS).

System	Notes
COSJ100024+015334	The "COSMOS-Web ring" Lens z = 2.02, source z = 5.10 (spectroscopic), Einstein radius about 0.77". Most thoroughly modeled system.
COSJ095921+020638	Lensed quad. Lens z = 0.4694, Einstein radius about 0.71".
COSJ100013+023424	Lens z = 0.890, Einstein radius about 1.45".
COSJ095914+021219	Lens z about 1.05, Einstein radius about 1.48".

Source redshifts are not published for the last three systems, so a placeholder of z = 2.0 is used for them. This affects the physical interpretation (distances, scaling) rather than the shape of the fit, but results for those systems should be treated as preliminary.

Methods
Mass model: isothermal (SIE) profile for the lens galaxy.
Lens light: Sersic profile (plus an experimental second compact Sersic component to reduce leftover central light after subtraction).
Source light: parametric Sersic profile.
Sampler: Nautilus nested sampling through PyAutoFit.
Acceleration: JAX, running on GPU where available.
Color imaging: WCS-aligned false-color composites (F444W / F277W / F150W) built with astropy and reproject.

Results and status
Reconstructions were compared against published results for the COSMOS-Web ring (see References).

References
Nightingale et al. 2025, The COSMOS-Web Lens Survey (COWLS) I: Discovery of >100 high redshift strong lenses in contiguous JWST imaging, MNRAS 543, 203. https://arxiv.org/abs/2503.08777
Mahler et al. 2025, The COSMOS-Web Lens Survey (COWLS) II: Depth, resolution, and NIR coverage from JWST reveals 17 spectacular lenses, MNRAS Letters 544, L8. https://arxiv.org/abs/2503.08782
Mercier et al. 2024, The COSMOS-Web ring: in-depth characterization of an Einstein ring lensing system at z~2, A&A 687, A61. https://arxiv.org/abs/2309.15986
Shuntov et al. 2025, The COSMOS-Web ring: Spectroscopic confirmation of the background source at z = 5.1, A&A 696, L14. https://arxiv.org/abs/2502.20136
van Dokkum et al. 2023, independent discovery of the same ring (JWST-ER1).
PyAutoLens: https://github.com/Jammy2211/PyAutoLens

Acknowledgments

Built on the open-source PyAutoLens, PyAutoFit, Nautilus, JAX, and Astropy projects, and on the public COWLS data release.

Author

Javier, University of La Verne
