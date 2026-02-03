- Recall Fan-in refers to the number of inputs to a given logic gate
	- high fan in leads to higher input capacitance
	- higher input capacitance leads to slower charging times (i.e, times required to reach threshold voltage for a given technology)
	- overall leads to delays in turning on/off for devices. 
	- Especially present in *series connections*

#### Figure 1: high-fan in devices
![[Pasted image 20251123162630.png]]
- For the NAND-3 device, the Pull-down network consists of 3 NMOS devices in series. This leads to both higher equivalent resistance, as well as the junction/gate capacitance between each device. 
- NAND-3 suffers from longer $t_{pHL}$. while NOR suffers from longer $t_{pLH}$

#### Domino Logic family 
- attempt to address this draw back of high-fan in cmos devices. 
- **Advantages** 
	- Only a Pull-down network, less transistors (fewer devices)
	- Pull-down network is n-devices which are inherently stronger than p-devices (recall carrier mobility)
	- **IMPORTANT**: $t_{pLH}$ is 0 since output is *pre-charged*
	- lower Loader Capacitance CL
		- Less Diffusion capacitance
			- given domino logic doesn't require large PMOS networks, the diffusion area at the output node is smaller, yielding smaller load capacitance 
		- Less gate capacitance in successive stages
			- because the *next* stage doesn't require a PMOS, you only drive NMOS inputs, hence lower load
	- **Very fast!**
- For Domino logic, the output will *pre-charge* in the *pre-charge phase*, and either discharge or **not** in the evaluate stage depending on the inputs to the PDN
#### Figure 2.1: timing of domino logic
![[Pasted image 20251123183702.png]]
#### Figure 2.2: Example of domino-logic schematic
![[Pasted image 20251123184153.png]]
- note that domino logic relies on the fact that when the clock is *low*, the pre-charge device (PMOS) is high, hence charging the output node to be high. this charge is stored in the total capacitance (junction, wire, etc)
- during evaluation (i.e, clock is high), the pre-charge PMOS is shut-off while the evaluation NMOS (bottom) is opened. 
- if the PDN is evaluated to be "true", the charge stored in the output-net is discharged through the PDN to ground, yielding a 0. otherwise, remains at a 1
- explains the idea that $t_{pLH}=0$, as its always *assumed* that the result should be 1. 

### Drawbacks of Domino Logic
1) pre-charged node can discharge *during* the evaluation phase due to leakage. puts a **lower bound** on the operating frequency
	- If the evaluation phase holds for too long, the output nets charge can be discharged through the various routes to ground due to leakage
2) Low $NM_{L}$, or Low noise-margin for logic LOW levels. 
	- recall that $NM_{L}=V_{IL}-V_{OL}$, or that the noise-margin for a low signal is the different between the maximum voltage that's recognized as a logic 0 and the output is recognized as a 1(?)
	- intuitively, this describes the range of input values which is permitted to maintain an output that can be recognized as 1
	- for CMOS logic, this is a **much** bigger region, as its *static* in nature (not time-variant); even if NMOS and PMOS are both conducting, it *can* still drive the output to a high-output
	- In contrast, domino logic is *time dependent*. If the input is even *slightly* turned on, this can lead to sub-threshold leakage from the NMOS PDN, as well as the overall PDN being "turned on" at **any** $V_{in}>V_{tn}$. 
3) Input **CANNOT** glitch during evaluate stage. Inputs **have** to be a stable (0,1) or make a single transition (0->1, 1->0) transition *during* the evaluate stage. If not, it is considered a **glitch** and the node will falsely discharge, and there is **no recovery** in that clock cycle
	- Compare this to CMOS: can evaluate *combinationally*: change values multiple times in a clock cycle, as it doesn't rely on stored charge to yield a correct output
	- in contrast, once the domino logic "accidentally" discharges its stored charge, there's no way to "recharge" it during the evaluation stage; correct result for that clock cycle is permanently lost, so glitches are **FAR** more dangerous in domino logic
4) Capacitive coupling to outputs can discharge the output
	- recall for domino logic, charge that's
	- used to evaluate the output is just stored in the output net via capacitance. 
	- if there exists some other form of capacitance or capacities coupling, this can lead to the output being *discharged* unintentionally, leading to incorrect results. 
5) Cascading Domino logic: Problem occurs when a *second* domino gate outputs a signal (out-2) that is 1 and needs to **stay** at 1. Yet it requires an input coming from the output of first gate (out-1) which should be 0 and stay 0. However, at the beginning of the common evaluate stage, out-1 takes a bit of time to discharge from pre-charge phase from 1 to 0 through its PDN. 
	- Specifically, Consider 2 cascading domino gates
	- the **correct** logical values during the evaluate stage *should* be out-1=0, out-2=1. 
	- but in **reality**, both dynamic nodes are out-1=1,out-2=1. 
	- during the evaluation stage, the second gate would "see" that the output of the first gate is high (even if its supposed to be low). based on this, the gate could discharge its stored charged, leading to a similar situation described in problem 3. 
6) High power consumption: recall that the activity factor, or switching factor, $\alpha$ is a part of the power equation $P_{d}=\alpha fCV_{dd}^2$. Domino requires pre-charging in every clock cycle. Also the logic puts a load on the clock which has the highest activity factor. 
### Solutions to Domino (Dynamic) Logic
1) **Leakage in pre-charge node**: Add a half keeper which will sustain the output in the evaluate stage
#### Figure 3.1: Half keeper
![[Pasted image 20251123195645.png]]
2) **Low noise margin**: just be careful lol
	- Keep input routes short
	- look out for sources of cross-talk
	- shield routes or half-shield routes
	- keep spacing greater than minimum
3) **Input cannot be allowed to glitch during evaluate stage**: Always start a domino chain from a latch which latches the input to PDN during evaluate stage (i.e, if $CLK=1$, latch and evaluate)
	- Latch maintains stage during high-clock period (non-transparent), hence doesn't allow inputs to change a this time.
#### Figure 3.2: input latching for domino chain
![[Pasted image 20251123195953.png]]
4) **Capacitive couple**: same solution as part 3
5) **Cascading domino gates**: Invert the dynamic node and feed into next gate. 

#### When to use Domino Logic?
- **all memories are built as dynamic logic**
- the PDN is basically an array of cells in this case
	1) Register Files
	2) ROM's
	3) SRAM and caches (... but S in SRAM is static, right?)
- Use domino when **speed is needed at all cost**

#### Figure 4: Example of pipelined stages in 