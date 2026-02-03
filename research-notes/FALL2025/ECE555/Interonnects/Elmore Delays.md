#### Figure 1: RC network used by CAD ![[Pasted image 20251123044208.png]]
- CAD tools model wire RC delays as a distributed network; ie, **not** a lump-resistance driving a lump-capacitance, but instead the RC being a continuous distribution along the length of the wire
- exact solution for figure 1 would require a 5th order differential equation. MASSIVE PAIN IN THE ASS!!!
- Instead, use **Elmore Delay** Model for a simple 1st order approximation 
- whats the Elmore delay from **Vin** to **n3** (or each node)?
	1) break down the delay as summation of **node-to-node** "segment" delays from the start node to the target node (to measure delay between start and target)
	2) compute one node-to-node as the resistance of the segment multiplied by the summation of all downstream capacitance *seen* at the end of the segment
- **Example**:
	- for equivalent RC between Vin and N3, elmore delay can be given as
$$
RC_{n_{3}}=R_{1}(C_{1}+C_{2}+C_{3}+C_{4}+C_{5})+R_{2}(C_{2}+C_{3}+C_{4}+C_{5})+R_{3}(C_{3}+C_{4}+C_{5})
$$
- intuitively, $R_{1}$ contributes to the **charging** of capacitors $C_{1}\dots C_{5}$
- $R_{2}$ contributes to the charging of $C_{2}\dots C_{5}$
- $R_3$ contributes to the charging of $C_{3}\dots C_{5}$
- In an alternate view, you can look at **which capacitors** need to be charged through which devices to get the node equation in question
$$
RC_{n3}=C_{1}R_{1}+C_{2}(R_{1}+R_{2})+C_{3}(R_{1}+R_{2}+R_{3})+(C_{4}+C_{5})(R_{1}+R_{2}+R_{3})
$$
- intuitively, capacitor 1 needs to be charged through resistor 1, capacitor 2 needs to be charged through resistor 1 and 2, etc. Note that the target node here is node 3, so capacitors 4 and 5 are assumed to be "drive" or "charged" by resistors 1,2,3 but **NOT** 4 and 5, as these don't contribute to the charging of node 3. 

#### More accurate RC models
#### Figure 2: $\pi$ and $T$ models. 
![[Pasted image 20251124145201.png]]
- instead of a lump resistance driving a lump capacitance, the $\pi$ and $t$ models give more accurate descriptions of the wires behavior. 
- the "larger" the model, the closer it comes to modeling an nth degree differential equation (charging and discharging of each capacitance). 
#### Figure 3: More realistic example of RC network
![[Pasted image 20251123155738.png]]
- For example, might be asked to find the delays from $V_{in}$ to $n_{3}$ and $n_{5}$
- For $n_{3}$
	- $R_{1}(C_{1}+C_{2}+C_{3}+C_{4}+C_{5})+R_{3}(C_{3}+C_{4}+C_{5})$
	- in the path from $V_{in}$ to $n_{3}$, the path contains the resistors $R_{1}$ and $R_{3}$. Examining the network, it can be easily deduced which capacitors each resistor is driving, and so the total RC can be given as the sum of these. 
	- Using the "follow the capacitor approach, the equivalent expression can be given
		- $R_{1}C_{1}+R_{1}C_{2}+(R_{1}+R_{3})C_{3}+(R_{1}+R_{3})C_{4}+(R_{1}+R_{3})C_{5}$
- for $n_{5}$
	- $R_{1}(C_{1}+C_{2}+C_{3}+C_{4}+C_{5})+R_{3}(C_{3}+C_{4}+C_{5})+R_{5}C_{5}$
#### RC delay growth
- **RC delay grows quadratically with length**
- **Example**: consider  $2000 \mu m$ M5 line at $140 nm$ wide. the route itself has $0.3 pF$ capacitance. It drives a $0.1pF$ load. the resistance of driver is $R_{eq}=300 \Omega$
#### Figure 4: Equivalent model
![[Pasted image 20251123160550.png]]
- The provided model is built assuming that each segment is $1000 \mu m$ in length, and a $\pi$ model is being used for a segment. 
- Elmore delay is given by 
	- $\tau=300*0.4+652*0.325+642*0.175=441ps$
- If targeting 1 Ghz, this delay gets significant. Solution? **Use Repeaters!**
#### Figure 5: Repeater
![[Pasted image 20251123160919.png]]
- In this case, each inverter/repeater drives its *own* net. i.e, splits the network into 2 separate nets, so that the first inverter **only** drives until node 2 (capacitor 2), and the second inverter/repeater drives until node 5 (capacitor 5). 
- New Expression is given as 
	- $300(0.075+0.075+0.01)+642(0.075+0.01)+300(0.1+0.15)+642(0.1+0.075)=290 ps$
- Shows how the delay is significantly below that