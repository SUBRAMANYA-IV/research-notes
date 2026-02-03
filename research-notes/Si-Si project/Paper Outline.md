![[20210813_Si_Al2O3_Si_Diode_Manuscript_DJV without highlights.pdf]]

#### Notes
- **Point D: CV measurement to determine if there are any residual charges or interface traps?**
	- introduces new energy levels at the interface of junctions, leading to unwanted behavior 
		- lowering threshold voltage shifts
		- degradation 
		- noise (flicker noise, generation/recombination noise)
		- Recall that CV measurements apply a DC and AC voltage, leading to the formation of depletion regions of various widths, making the device act as a capacitor
		- interfacial traps should lead to accumulation of charges at said pinning/interfacial states, leading to the depletion region not "growing" as quickly for a given voltage?
- **Point E: Using Al2O3 or HfO2 as interface materials for comparision?**
	- Paper mentions just esting out multiple HfO2 pieces at the same time to optimize annealding temp/time by seeing which conditions yield the best devices. 
	- *maybe* perform the study using both aluminum and halfnium oxide to see performance between the two?
	- use TEM/SEM to image the cross section of the diodes to see the interfacial layers between the two. 
	- **use silvaco TCAD to simulate the ideal diode**
		- Either use athena to simulate epitaxial growth methods to simulate "realistic" diode
		- **OR**, use TCAD deck builder directly to compare performance against completely ideal diodes?
		- 