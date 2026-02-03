![[Pasted image 20251215040117.png]]
![[Pasted image 20251215040313.png]]
![[Pasted image 20251215040325.png]]
- NMOS in cutoff, PMOS in linear
	- Output voltage is Vdd, for PMOS drain source is 0, **but** input/gate voltage is "greater than" threshold, **hence** in linear region
- NMOS in saturation, PMOS in linear
	- as Vin increases, NMOS starts conducting: Output is already known to be close to Vdd, hence in saturatio
	- PMOS is still turned on, and in linear region (drain-source is still less than gate voltage)
- NMOS and PMOS in saturation
	- I.E, **BOTH** are conducting (BADDDDD)
#### VTC
![[Pasted image 20251215041845.png]]
- Point at which a strong "1" or strong "0" is interprereted, is the location where the derivative equals **negative 1**
#### Propagation Delays
![[Pasted image 20251215041924.png]]
- propagation of high to low (from output as the reference) is given by the time between input waveform hitting 50%, and output hitting 50% in that transition
- fall and rise time is defined as the signal slopes between 10% and 90%. 

#### VTC: Margins
![[Pasted image 20251215042108.png]]
- **VOH**: dictates the minimum output voltage that will be read as a logical HIGH
- **VOL**: dictates maximum output voltage that will be read as a logical LOW
- **VIL**: maximum input voltage that will be read as a LOW
- **VIH**: minimum input voltage that will be read as a HIGH
- **VTH**: input voltage at which Output is half of the rail-to-rail voltage
![[Pasted image 20251215042334.png]]
- Cases for the input/output
	- if the first gate drives a significantly higher *low*, then Vin is shifted "right"
	- indicates that theres a much smaller noise margin *low* region, where noise can "spill over" into the sloped region, leading to noise/uncertainty on the output
	- hence, defined as the difference between **current** gates maximum voltage thats recognized as a logical Low, and the **previous** gates maximum output driven as a **low**
#### Beta Ratios
![[Pasted image 20251215043040.png]]
- beta is defined as the product of hole mobility **and** width
	- Higher Beta indicates higher beta for pmos-> indicates stronger pull up network, indicates that when the input is low (and the PMOS is turned on), PMOS turns on "stronger" than NMOS->rightward shift of curve
- 