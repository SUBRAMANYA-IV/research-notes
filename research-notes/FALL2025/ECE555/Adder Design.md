### 1-bit Full Adder
- Conventional adder model, easy to chain together to form an n-bit adder
- However, large delays for larger chains of full adders
	- for result to be valid, carry must propagate through entire chain until last full adder, long combination delay, hence large critical path
- Generate: $G=AB$
	- If the *current bit* being inspected should **independently** create a carry  bit
- Propagate: $P=A \oplus B$
	- if the *current* bit being inspected would allow a carry in to be propogated
	- consider $C_{in}=1$: $C_{out}=1$ if $A=1, B=1$. 
		- Note that, though current cell would *technically* produce a carry if both A and B were 1, this is considered 2 seprate actions: a **kill** AND a **generate**
- Kill: $K=\bar{A} \bar{B}$
	- if the *current* cell being inspected would lead to a carry-in **not** being propgated
	- Note how this **only** occurs when both A and B are both 0. 

- Using these terms, an equation to recursively describe the full adder can be given by 
$$
C_{o}(G,P)=G+PC_{i}
$$
- i.e, if the carry out will be generated from the current cell can be determined as a function of the current cells generate, propagate and carry in function. 
$$
S(G,P)=P \oplus C_{i}
$$
- i.e, the current cell yielding the bit-wise sum of 1 can be determined as a function of the propagate and carry in

### Mirror Adder implementation
![[Pasted image 20251113190315.png]]
- transistor schematic for implementation of an adder circuit
- Note that the circuit is **not** dual (kill and generate components)
- exploits relations in $S$ and $C_{out}$ to reduce transistor count
- Can be chained to form multi-bit adder, **though** every other bit-slice will need to be inverted

### Multi-Bit Addition

#### Mirror adder with inverting stage for a Ripple Carry Adder (RCA)
![[Pasted image 20251113190710.png]]
- simplest, most area-efficient implementation of an adder
- **but** slow for N>8
- Carry has to "ripple" through N stages
#### Carry Bypass Adder
![[Pasted image 20251113190824.png]]
- RCA delay is **always** proportional to N (large for N>8)
- *but*, certain "cases" can be optimized. Gives a **Carry Bypass Adder (CBA)**
- still conventional ripply-carry structure, **but** bit slices can be "split" using a mux
	- If $BP$ is 0, implies that not all cells propogate, hence must manually wait/check for generates in the previous cell slice
	- **BUT**, if $BP$ is 1, implies that any carry **will** be carried, hence $C_{in}$=$C_{out}$. Saves entire critical path
		- **BUT** only for certain situations
- Still linear with N, but reduced slope
#### Carry Select Adder
- Compute the carry-out $C_{out}$ and sum for **both** cases preemptively, and then depending on actual carry in value, select the mux for the given case. 
![[Pasted image 20251113191920.png]]
- For example, in the LSB cell (bits [3:0]), determines the sum of A and B if carry was 0 **and** if carry was 1. 
- if carry in is 1, mux selects case of 1 a the sum for bits [3:0]. Otherwise, result for carry of 0.
#### Square Root CSA
![[Pasted image 20251114143242.png]]
- Change the bit length of each stage to follow a linear progression (ie, stage 1=2 bits, stage 2 =3 bits, stage 3=4 bits, stage 4=5 bits)
- main idea is that later stages require more time to compute the sum for both cases of the carry, hence the carry can "arrive" later, as the *critical path* would be the computation, **not** the arrival f the carry bit. 
- 