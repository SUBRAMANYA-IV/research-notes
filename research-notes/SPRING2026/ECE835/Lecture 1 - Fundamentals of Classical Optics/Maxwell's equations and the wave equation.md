$\vec{E}$ and $\vec{B}$ are the vector electric and magnetic fields. 

#### Gauss's law
- Gauss's law states the following 
	$$\vec{\nabla}\cdot    \vec{E}=\frac{\rho}{e_{0}}\text{: Differential Form}$$
$$\oint{\vec{E}\cdot  d\vec{A}}=\frac{\rho}{e_{0}}\text{: Integral form}$$
- relates an electric charge to the resulting electric field.
- integral form states that electric flux through a closed surface enclosing a charge is equal to the enclosed electric charge divided by the permittivity of free space. 
- the differential form utilizes the divergence theorem to equate volume and surface area. 
- **Recall that divergence is a measure of how much a vector field acts like a "source" or "sink" in a vector space. 
- Recall that the $\nabla$ operator in this context is the **vector of partial derivative operators**, i.e $\nabla=\left( \frac{d}{dx},  \frac{d}{dy},  \frac{d}{dz} \right)$, representing the rate of change in the Cartesian directions at a given point in space. 

#### Gauss's law for magnetism 
- Gauss's law extended to magnetism states that 
$$\vec{\nabla}\cdot  \vec{B}=0$$
- i.e, that there is no net "source" or "sink" over a given space for a magnetic field
- or, that **magnetic monopoles do not exist**
#### Maxwell-Faraday's Law of Induction
- Faraday's law of induction states that
$$ \vec{\nabla}\times   \vec{\epsilon}=-\frac{d\vec{B}}{dt}\text{: Differential Form}$$
$$\oint_{C}{E \cdot{dl}=-\frac{d}{dt}\int \int_{S}{B\cdot dS}}\text{: Integral Form}$$
- states that a **time varying** magnetic field always accompanies a spatially varying, **non-conservative** electric field. 
	- Recall that **conservative** implies that the line integral in a **conservative** vector field is path independent; i.e, the path used to travel from point A to point B does not influence the value of the line integral 
	- **non-conservative** electric field implies that work is being done in the field
		- Work around a closed loop is NON zero. 
- Integral form states that the line integral of the electric field around a closed loop $C$ is equal to the negative change in flux $\phi_{B}$ through the surface $S$
#### Amperes Law
- Amperes Law states that 
$$
 \nabla \times B=\mu_{0}(J+\epsilon_{0}\frac{dE}{dt})\text{: Differential Form}
$$
$$\oint B \cdot dl=\int \int_{S}(\mu_{0}J+\mu_{0}\epsilon_{0} \frac{dE}{dt})\text{: Integral Form}$$
- integral form states that the magnetic field induced around a closed loop is equal to the current passing through a given surface. 
	- Second component of $\epsilon_{0}\frac{dE}{dt}$ represents the [[displacement current]]

#### Deriving the Wave Equation
- Recall that Faraday's law of induction states the following. 
$$
 \vec{\nabla}\times   \vec{\epsilon}=-\frac{d\vec{B}}{dt}\text{: Differential Form}
$$
- which states that...
	- the [[curl]] of the electric field yields a time varying magnetic field...
	- OR, that a time-varying magnetic field through a coil induces an electric field. 
		- This is more notable in the integral form vs the differential form. 
- taking the curl on both sides of the equation, this yields
$$
\vec{\nabla^2}   \vec{\epsilon}=-\frac{d}{dt}(\vec{\nabla}  \times  \vec{B})
$$
- Substitute $\vec{\nabla}  \times  \vec{B}$ with the amperes law expression, yielding
$$
\frac{d}{dt}\left( \mu_{0}J+\mu_{0}\epsilon_{0} \frac{dE}{dt} \right)
$$
- Note that this expression assumes a *constant current*, $J$, with respect to time, hence this can be set to 0. 
- This finally yields 
$$
\vec{\nabla^2}  \vec{E}=\frac{d^2}{dt^2}(\mu_{0}  \epsilon_{0} \vec{E})
$$
- The solution to this equation is in the form 
$$
\vec{E}(\vec{r},t)=\mathrm{Re}(\vec{E_{0}}e^{i(\vec{k}  \cdot  \vec{r}-\omega t)})
$$
- this represent the propagating wave. 
- $\vec{E_{0}}$ represents the polarization vector and amplitude. 
	- includes the properties of **direction** (direction the electric field points while oscillating), Magnitude (maximum field strength)
	- **in free space**, maxwell's equation constrains it such that $\vec{k}  \cdot  \vec{E_{0}}=0$, i.e the direction of propagation of the wave (given by $\vec{k}$) is perpendicular to the direction of *oscillation* of the wave (given by $\vec{E_{0}}$)
- $\vec{k}$ and $\omega$ are two similar quantities in different dimensions. 
	- $\vec{k}$ represents how "fast" the wave oscillates *in space*
	- $\omega$ represents how fast the wave oscillates *in time*. 
	- **NOTE**; these two values are NOT independent; the constraint $\omega=c|k|$ must hold. 


#### Energy of waves
- the electric and magnetic components of an E.M wave can be given as
$$
E(\vec{r},t)=E_{0}e^{i(\vec{k}  \cdot  \vec{r}-\omega t)}\hat{n}
$$
$$
\vec{B}(r,t)=\frac{\vec{E_{0}}}{c}e^{i(\vec{k}  \cdot  \vec{r}  -\omega t)}(\hat{k}  \times  \hat{n})
$$
- where we take the "vector" component of $\vec{E_{0}}$ out as $\hat{n}$ instead, leaving $E_{0}$ to be the magnitude of the electric filed, a **scalar** value. i.e, $\hat{n} \perp   \hat{k}$
- Given that the magnetic field is normal to the electric field, and propogates in the same direction (i.e, the same $\vec{k}$), then the oscillation vector of the magnetic field is given by $\hat{k}  \times  \hat{n}$
###### Energy density of a wave
- energy density describes the energy per unit volume, or $\frac{J}{m^3}$ and is given by 
$$
u=\epsilon_{0}   |\vec{E}|^2=\frac{B^2}{\mu_{0}}
$$
- The energy flux, or [[poynting vector]], is given by 
$$
\vec{S}=\frac{1}{\mu_{0}}(\vec{E}  \times   \vec{B})
$$
	- this gives the energy transfer per unit area, per unit time, in the units of $\frac{J}{m^2  \cdot  s}$
	- describes the amount of energy being transferred through a surface per unit time. 
- the intensity (average power per area) is given as
$$
I=  <|\vec{S}|>  =\frac{cu}{2}
$$

