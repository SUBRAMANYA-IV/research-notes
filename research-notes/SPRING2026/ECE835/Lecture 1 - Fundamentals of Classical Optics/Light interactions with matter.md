- Linear momentum of a photon can be given by
$$
\vec{P}=\hbar  \vec{k}
$$
- where $\hbar$ is the **reduced plancks constant**, which is simply $\frac{h}{2\pi}$, where $h$ is just planks constant. 
- recall that $\vec{k}$ is the wave vector, which is given by $|\vec{k}|=\frac{2\pi}{\lambda}$.
- Electromagnetic fields only interact with **charges** and **currents**:
	- interactions are described by the lorentz force law, which is given by
$$
\vec{F}=q(\vec{E}  +\vec{v}  \times  \vec{B})
$$
	- Which states that the force a charge $q$ experience is equal to the presence of an electric field $\vec{E}$, and the **cross product** between its *velocity vector* $\vec{v}$ and the magnetic field $\vec{B}$
		- Recall that electrons in a magnetic field experience a force *normal* to their velocity and magnetic field vector. 
- So what are the ways photon can interact with matter/charged particles?
	- change in particles Energy
		- Absorption, emission, heating, electronic transition (inter-band transition). 
	- Change in the particles **linear momentum**
		- Solar sail, radiation pressure, etc. 
	- Change in the charged particles angular momentum
		- Polarization(?), optical pumping(?)
##### Atomic polarizability 
- When light transmits *through* a medium, the electric field of the beam, i.e $\vec{E(t)}$ displaces **bound charges** inside the medium from their equilibrium positions. 
	- Displacement creates a [[dipole moment]]
$$
\vec{p}=\sum_{i} q_{i}r_{i}
$$
	- Where $q_{i}$ and $r_{i}$ represent individual charges and their respective displacement from their equilibrium positions. 
	- This displacement can be generalized o
	$$
	\vec{p}=\alpha  \vec{E}
	$$
	- where $\alpha$ represents the **polarizability** of an electron cloud, belonging to an atom or molecule. Is a measure of how **easily** this cloud is distorted by an external, electric field. this is a **scalar** value in isotropic materials, but is a tensor in anisotropic materials (i.e, sensitive to polarizability in specific directions). 
	- **macroscopic** polarizability is given by $\vec{P}=N  \vec{p}$, where $N$ is the density of charges.
	- the **dipole-field interaction energy** can be given by 
	$$
	U_{\int}=-\vec{p}  \cdot  \vec{E}=-\frac{1}{2}  \alpha  |\vec{E}|
	$$
		- This defines the potential energy stored in the system due to the polarization. 

#### What happens when a charge is driven back and forth? 
- When a charge oscillates, the following occurs
	- The charge accelerates 
	- its electric field changes in time, i.e $\frac{dE}{dt}$
	- A time-varying electric field generates a [[curl]]ing magnetic field, as stipulated by amperes law ($\nabla  \times  B$)
	- a time varying magnetic field creates [[curl]]ing electric field
	- the two reinforce each other and detach from the charge $\to$ radiation. 
###### Accelerating electric charges. 
- when an electric charge accelerates, it perturbs the surrounding electric field, which propagates outward. This can be given by the equation
$$
\vec{F}(t)=-\frac{q_{1}q_{2}}{4\pi\epsilon_{0}c^2} \frac{1}{r}*\vec{a}\left( t-\frac{r}{c} \right)_{\perp}\left( t-\frac{r}{c} \right)
$$
-  This equation denotes how the force experienced by a charge, a distance $r$ away from the accelerating charge, is given as the *direction* of acceleration, $\vec{a}(t)$. 
	- $\vec{a\left( t-\frac{r}{c} \right)}$ describes the acceleration of the first charge that *caused* the currently experienced force by the second charge. 
- Recall that the dipole moment is described as the displacement of charges from their equilibrium position. the time dependent dipole moment can be given by
$$
\vec{p}(t)=e  \cdot  \vec{d}=  \hat{z}p_{0} \cos(\omega t)
$$
- 