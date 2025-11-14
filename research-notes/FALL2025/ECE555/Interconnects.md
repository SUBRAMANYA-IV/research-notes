- In older nodes, interconnects were **flat** and had **wide spacing** between them, leading to low capacitances that could just be ignored
- but as devices became more "dense" in devices, interconnects had to become closer together *and* grow vertically (maintain constant cross sectional area, maintain same resistivity)
	- Hence, Majority of capacitance came as **parallel plate capacitance from interconnect to ground/bulk**

###### Newer Interconnects
![[Pasted image 20251114144454.png]]
- However, now interconnects are taller and close together. 
	- Flat faces facing each other, with the air acting as a dielectric: forms a capacitor! 
- paralel plate between interonnect and bulk is now a small percent of the total capacitance. 

###### Graph of technology-size and components of capacitance. 
![[Pasted image 20251114144636.png]]
- Graph demonstrates that with **newer** nodes (ie, smaller design rule), this leads to ground playing a smaller component of the total capacitance while the line-to-line increases. 

#### Mitigating Cross Talk

###### Increase spacing between interconnects
![[Pasted image 20251114144848.png]]
- Increase Spacing to reduce Cross talk between interconnects
	- **Note**: reducing capacitance also reduces power consumption ($P=CV^2f$)
	- Not always possible due to real-estate constraints. 

###### Shielding
![[Pasted image 20251114145038.png]]
- Shield using power and ground lines in between interconnects
	- Field lines terminate on VDD/VSS so no line-to-line victim/attacker
	- easy to do because VDD/VSS anyway needs to be routed
![[Pasted image 20251114145609.png]]
- Interleaving bits of *different* busses also helps
	- **does not** solve cross talk noise, but if different busses switch at different times, it mitigates timing push out issues. 2

### Modeling Wire resistance and Capacitance
