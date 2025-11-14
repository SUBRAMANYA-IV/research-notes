2025-11-08 15:58
## What
- MZI, or Mach–Zehnder interferometer
- Method to determine various properties by extracting information from interference patterns. 
## How
- splits a coherent, collimated beam into 2 paths, gives one of them a different phase delay, and then recombines them to produce interference at the output. 
- Given that the two arms of the optical path have lengths $L_{1}$ and $L_{2}$ and effective refractive index $n_{eff}$, then the phase difference between them is given by 
$$
\Delta \phi=\frac{2\pi n_{eff}(L_{1}-L_{2})}{\lambda}
$$
- when recombined: 
	- if $\Delta \phi=0,2\pi\dots$, the waves interfere constructively, implying high transmission
	- if $\Delta \phi=\pi,3\boldsymbol{\pi}..$, they interfere destructively, implying low transmission. 

- Changes in the $\Delta \phi$ component can yield information on the change in refractive index, and in turn the properties of whatever is being measured. 
- In the context of microfluidics, the analyte (cell, fluid, molecule) needs to *interact* with the [[evanescent field]] of one of the wave guide arms
- usually done in 1 of 3 ways
	- **fluidic channel on top of one arm**
		- a micro-channel (PDMS or glass) runs over one arm of the interferometer 
		- when a cell or particle passes over it, it perturbs the local refractive index around the wave guide 
		- the evanescent field (~100-200 nm penetration into the fluid) picks up that change, altering $n_{eff}$
	- **Surface functionalization**
		- The top of one arm is coated with a biochemical receptor layer (antibody, DNA probe, etc)
		- binding event changes the local refractive index, leads to phase shift
		- 
###### tags

