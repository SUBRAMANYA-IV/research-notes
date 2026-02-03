09- For amperes law, recall that a change in an electric field is equivalent to moving charges, or **current**. 
- Second component of ampere's generalized law is the displacement current, relating a shifting/changing electric field with respect to time with current. 

#### Waves
- Recall that starting off with Faraday's law of induction, we can perform. 
$$
\nabla \times\left( \nabla \times e=-\frac{dB}{dt} \right)
$$
- moving the curl into the time derivative, we get 
$$
\text{LHS}: \nabla \cdot \nabla \cdot e-\nabla^2e
$$

$$
\text{RHS}: -\frac{d}{dt}(\mu_{0}e_{0}e)=\nabla^2 \cdot e
$$
- A solution to this simultaneous, second order differential equation by
![[Pasted image 20260126134052.png]]
- this yields the wave equation in a vaccum. 
- what about a non-magnetic medium? 
- If dealing with a medium, replace epsilon with the permittivity of the given medium. 
- assumes that the medium is non-magnetic, hence permeability is unaffected. 
- this all relates back to [[complex refractive index]], which then defines the relation between ratio of speeds of light in differing mediums. 
- $c^2=n^2v^2$, v is the frequency. 

#### Energy properties of light waves. 
- **Monochromatic plane waves in a vacuum**
	- Monochromatic: single frequency
	- Plane waves: Uniform wave fronts. 
- Electric field and magnetic field are in phase and perpendicular to one another. 
![[Pasted image 20260126135106.png]]
- Energy density of a wave is given by
![[Pasted image 20260126135141.png]]
- energy is contribute dby both magnetic and electric field, given by 
$$
u_{e}+u_{B}
$$
- Energy *flux* in turn defines the energy per unit area time. Given by
![[Pasted image 20260126135300.png]]
- normal to both the electric and magnetic field, along the $k$ vector, or the direction of propagation. 

#### Day 2
- conditions for linear polarization is such that $e_{0,x}=0$ or $e_{0,y}=0$
	- recall that $e_{0}$ represents the magnitude of the wave in that direction, in this case the cartesian direction. 
\epsilon

#### Interference. 
- given the experiment where 2 beams are "combined" using a beam spliter
- The detector only measures the **intensity** of the incoming/incident wave
	- I.e, recall $I=\frac{1}{2}c \vec{e_{1}} \cdot  \vec{e_{2}}$
	- The resulting intensity will hence be given by 

$$I=\frac{1}{4}\epsilon_{0}c(\epsilon_{x}^*\epsilon_{x}+\epsilon_{y}^*\epsilon_{y})$$
#### Relating photon properties to wave properties. 
- Photoelectric effect let us know that...
	- Kinetic energy of an electron depends on the frequency of the light
		- Energy of a photon is given by $E=h\mu$, where $\mu$ is the frequency of the light. 
		- work function is a property inherit to a material, dictating how much work or energy must be incident on the surface of the material such that electrons are freed. 
#### Properties of photons
- Energy density of a wave (energy per volume) is given by 
$$
u=\epsilon_{0}|\vec{E}|^2
$$
- the poynting vector is given by 
$$
\vec{S}=\frac{1}{\mu_{0}}(\vec{\epsilon} \times  \vec{B})
$$
- intensity (average power by area) is given by 
$$
I=\frac{cu}{2}
$$
- based on the intensity, mean frequency, we can determine the number of photons that pass through a given point per second. 
- The Linear momentum of a photon can be iven by
$$
\vec{P}=\hslash k
$$
- **NOT** to be confused with dipole moment. 

#### Light interaction with matter. 
- EM fields only interact with charges and currents:
	- Interaction described by lorentz force law
$$
\vec{F}=q(\vec{\epsilon} +\vec{v} \times  \vec{B})
$$
	- Where $\vec{F}$ is the force acting on a moving charge with velocity $\vec{v}$
	- When talking about light interacting with nominally neutral objects like a wall or mirror, we are reffering to its interactions with **bound charges (dipoles) and induced currents**
	- when interacting with materials, the electric field of the beam displaces bound charges inside the medium from their equilibrium positions. 
	- Dipole-field interaction energy is given by
	$$
	U_{\int}=-\vec{p} \cdot  \vec{\epsilon}
	$$
	- the dipole moment can be given by 
	$$
	\vec{p}=\sum_{i} q_{i}r_{i}
	$$

#### What happens when a charge is being driven back and forth?
- Oscillating charges leads to radiation of Electromagnetic Waves. 
- **REVIEW**: Dipole radiationmoment
- 
