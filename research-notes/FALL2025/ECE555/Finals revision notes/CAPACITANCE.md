**TIME REQUIRED TO CHARGE AND DISCHARGE** capacitances is the **MAIN** component of delay in a CMOS circuit

- **EXISTS A SOURCE OF CAPACITANCE BETWEEN ANY 2 COMBINATIONS OF PORTS IN A TRANSISTOR** 

#### Gate Capacitance: Complex Model
- Composed of 2 main components: **Intrinsic and overlap**
	- **Intrinsic**: due to the actual gate/channel overlap. voltage **dependent** 
	- **Overlap**: Gate usually extends into the source/drain channels, this being the *overlap* between the two. voltage **independent**

###### Gate capacitance in Cutoff
- Intrinsic capacitance is **voltage dependent**: depends on the region of operation
- In cutoff, zero gate bias is applied
- no depletion or inversion region is formed in the bulk of the device
- recall that capacitors in **series** have **lower** equivalent capacitance 
- As voltage is increased close to the threshold voltage, the "bottom" plate of the capacitnce moves **down** from the oxide, in effect reducing the capacitance. 
![[Pasted image 20251215032542.png]]
###### Gate capacitance in Linear Region
- Forms an inversion region below the oxide layer
- acts as 2 capacitors in series (gate-> oxide -> inversion, inversion->depletion->substrate)
![[Pasted image 20251215033215.png]]
###### Gate capacitance in Saturation 
- intrinsic capacitance is mostly concentrated around the gate to source
	- recall that as Vds increases, drain source voltage increases, leading to pinchoff, or the concentration of the depletion region near the source. 
![[Pasted image 20251215033350.png]]

#### Gate capacitance: overlap
![[Pasted image 20251215033430.png]]

# Diffusion Capacitance 
- a.k.a parasitic capacitance and depletion capacitance
- due to depletion regions formed around the PN junctions of drain and body and source and body 
- depletion region acts as an **insulator** between p and n types
![[Pasted image 20251215033539.png]]
- Perimeter is given by the width (not counting junction away from the channel), plus 2 times the length of the channel
![[Pasted image 20251215033736.png]]
**NOTE**: unit is given as **capacitance per unit length**
