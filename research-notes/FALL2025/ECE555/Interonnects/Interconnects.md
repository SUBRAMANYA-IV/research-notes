- in olden days, interconnects were **wide** and **flat**
	- less capacitance *between* interconnects (lower flat-area between the two)
	- Most capacitance came from **Parallel plate capacitance** between substrate and the interconnects
- As technology scaled smaller, aspect ratio of wires changed
	- **height** grew to maintain constant cross-sectional area, minimizing resistance 
	- **width** decreased, to make more space for interconnects 
- Lead to **parallel plate** capacitance as a component of **total** capacitance decreasing, now **line to line** became majority component
#### Figure 1: Factors of Capacitance for a given design rule (node-size)
![[Pasted image 20251123014715.png]]
### Mitigating Cross Talk
- **Increasing interconnect spacing**
	- Obvious solution, reduces line-to-line capacitance
	- **reducing capacitance also reduces power**: Recall $P=CV^2f$
	- not always possible due to real-estate constraints 
- **Shielding** 
	- field lines terminate on VDD/VSS, so no line-to-line victim/attacker 
	![[Pasted image 20251123015046.png]]
- **Interleaving** 
	- does not necessarily reduce cross talk noise, but different busses with different signals reduces like hood of timing push out issues. 
	![[Pasted image 20251123015102.png]]
- **Orthogonal Layers**
	- Alternate metal lays are **orthogonal**. 
	- good for routing reasons, and minimizes line-to-line capacitance between *parallel* routes on different metal layers
	- if followed, parallel routes on different layers will have **two dielectric thickness** between them
	- Signals on adjacent layers will only be coupled by the small intersection area

#### Modeling wire resistance and capacitance
- **Resistance** 
	- when $R_{driver}\gg R_{Wire}$ then a lumped capacitance is a reasonable approximation 
	- **however**, chips are now large, and drivers are faster $\to$ wire RC component becomes significant!
- Consider the example of  metal-5 wire with length of $1000 \mu m$ and width of $140nm$
	- Wire itself has a capacitance of $0.15pF$ and the equivalent resistance (wire and load) of $642 \Omega$. Inverter drives a $0.2 pF$ Load
#### Figure 2: Equivalent Model
![[Pasted image 20251123020852.png]]
- recall that for an RC network, the delay is given by 
$$
V(t)=V_{DD}(1-e^{-t/RC})
$$
- which represents the rising voltage across the capacitor as a step-function. 
- a net is considered "on" at 50% of $V_{dd}$, hence solving for $t$, we get
$$
e^{-t/RC}=0.5
$$
$$ t=-RC\ln(0.5), \ln(0.5)\approx_{0}.69$$
$$t\approx 0.69RC$$
- this expression yields the time it takes for the voltage across a capacitor to reach half of the initial step-response function provided
- solving for $t$ in this case, we get $t=0.155ns$, which is over **15%** of our period if our target frequency is $1GHz$
- Shows that wire-loads are a **big** factor in performance. 
- **is a lumped RC model a good approximation?**
	- i.e, assume that the *entire* routing capacitance is driven **through** a lumped wire resistance? 
		- from the model, assumes that **ALL** of the resistance drives the capacitance of the wire and load
		- in reality, both *resistance* AND *capacitance* is distributed along the wire

#### More accurate ways to model RC networks
#### Figure 3: alternative models to lumped-sum RC
![[Pasted image 20251123030831.png]]
- figure demonstrates more accurate models of the RC networks when driving a load
- so... when to use **lumped sum** (easy to calculate/model) vs **T1/Pi** models?
- **short interconnects within a cell or block**
	- RC is likely negligible, a lumped C is enough
- **Long routes**:
	- RC needs to be counted when the interconnect resistance approaches that of the driver
#### Figure 4: distribution of interconnect lengths
![[Pasted image 20251123031307.png]]
- demonstrates that majority of interconnects are short, local, intra-cell and intra-block wires.
- another portion are **inter-cell** interconnects. Likely to be biggest source of problems, as both widely used *and* have significant RC networks
- longest interconnects are for global signals. need to be engineered upfront. 
#### RC delay after place-and-route
- Modeling RC is a pain in the ass because the resistance creates **new nodes** that are not present in the schematic
- cross-probing becomes hard
#### Figure 5.1: pre-layout schematic
![[Pasted image 20251123032221.png]]
#### Figure 5.2: post-layout, post PEX schematic
![[Pasted image 20251123032236.png]]
- RC extracted view will contain *distributed resistance and capacitance* model of the wire
- resistors create new nodes in the *extracted* netlist that are not present in the schematic netlist/view
- makes cross-probing a pain in the ass. 
