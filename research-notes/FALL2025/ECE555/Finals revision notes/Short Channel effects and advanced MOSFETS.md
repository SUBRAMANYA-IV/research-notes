![[Pasted image 20251215022835.png]]
- For the saturation region, include additional component that indicates change in current with continued application of voltage. 

#### Threshold voltage
- in reality, a function of many components
![[Pasted image 20251215023114.png]]
![[Pasted image 20251215023124.png]]
- since most of the components are purely a function of device fabrication, the main component is the **source bulk bias** component

#### Body Effect
![[Pasted image 20251215023219.png]]
- source bulk voltage for an NMOS device can be exploited for various device behavior 
	- Positive (forward biased) source bulk voltage leads to higher threshold voltage, lower leakage, etc. 

#### Short Vs Long Channel Effects
![[Pasted image 20251215024400.png]]
- For short channel transistors (modern transistors), additional drawbacks/effects occur
- **Velocity Saturation**
	- Electrons accelerated to maximum, saturating velocity at a given applied voltage/potential (electric field over a given distance)
![[Pasted image 20251215024511.png]]
- reaches saturation voltage **earlier** for a given drain-source voltage
![[Pasted image 20251215024557.png]]
- first formula shows linear current equation for long channel transistors
- second equation shows **saturation** current equation for **long channel transistors**, **WITH** long-channel effects
- third equation shows linear current equation for **short channel** transistors
- fourth and fifth equation show **saturation** current equation for **short channel** transistors, accounting for both **saturation velocity/voltage** **AND** **channel length modulation/pinchoff**
![[Pasted image 20251215024808.png]]
**MAIN DIFFERENCES**
- **CURRENT**
	- **LONG CHANNEL**: square law for current vs gate voltage
	- **SHORT CHANNEL**: linear relationship between gate voltage and current
- **SATURATION**
	- **LONG CHANNEL**: Saturation dictated by threshold voltage and gate voltag
	- **SHORT CHANNEL**: saturation is (almost) completely a function of saturation voltage, which is less than the threshold/gate voltage. 
	- 