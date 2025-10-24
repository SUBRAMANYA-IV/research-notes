2025-10-23 19:11
## What
- *optical* method for investigating the [[complex refractive index]] and [[Dielectric]] properties of thin films. 
- measures the change of [[polarization]] upon reflection *or* transmission and compares it to a model
- can be used to characterize composition, roughness, thickness, crystalline nature, doping concentration, electrical conductivity and other properties.  

## How
###### Basic Principles
- measures the change in polarization  the incident radiation (known polarization/state) interacts with the material structure of interest (reflected, absorbed, scattered, transmitted). 
- polarization change is quantified by the **amplitude ratio**, $\psi$ and the phase difference $\Delta$. 
- Most models assume that the sample is comprised of discrete, well defined layers that are optically **homogeneous** and [[Solid Structures#Isotropic|Isotropic]]. Violations of these properties requires 
###### Experimental Setup
- Electromagnetic Radiation is emitted by a light source and linearly polarized by a polarizer. 
- reflected waves pass through a second polarizes (called the analyzer) and falls into the detector. 
- the incident and reflected beam span the *plane of incidence*
	- ie, plane described by the vectors of the incident beam, reflected beam (or the vector normal to the surface of the material)
- light which is polarized **parallel** to the *plane of incidence* is p-polarized
- light which is polarized **perpendicular** to the plane of incidence is s-polarized.
![[Pasted image 20251023202527.png]]
###### Data Acquisition
- Measures the complex reflection ratio $\rho$ of a system, which may be parameterized by the amplitude component $\psi$ and the phase difference $\Delta$. 
- the amplitudes of the p and s components after reflection and normalized to their initial value (ie, a fraction/percent of the incident intensity) are denoted by $r_s$ and $r_{p}$ respectively. 
- the angle of incidence is chosen close to the [[Brewster angle]] of the sample to ensure a maximal difference in $r_p$ and $r_s$. 
- ellipsometry measures the complex *reflectance* ratio $\rho$, which is given by 

$$
\rho=\frac{r_{p}}{r_{s}}=\tan(\Psi)\cdot e^{i\Delta}
$$
###### Data Analysis
- Indirect method, ie the measured values cannot be converted directly into the optical constants of the sample
- must use a model such as [[tauc-lorentz]] or [[forouhi-bloomer]]. 
- Using the aforementioned models and an iterative procedure (least-squares minimization) unknown optical constants and/or thickness parameters are varied, and $\Psi$ and $\Delta$ values are calculated using the [[Fresnel Equations]]. 
## Why


