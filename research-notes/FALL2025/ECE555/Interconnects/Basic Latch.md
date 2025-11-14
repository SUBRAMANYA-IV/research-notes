![[Pasted image 20251110144250.png]]
- basic implementation of a basic latch, where the inverter-cycle **maintains** a state, read during high-enable
- Note that a voltage drop occurs across the nmos during enable due to using nmos as a pull-up transistor
![[Pasted image 20251110144340.png]]
- solved by using a pass gate to drive the high/low via pmos/nmos devices. 
- However, still leads to contention between D and N1 due to driving the same net
![[Pasted image 20251110144506.png]]
- Solved by adding a pass gate to the output of the feedback inverter;
	- When **EN=0**, pass-gates PMOS is held **high** and NMOS held **high**, leads to direct connection to N1, maintains state when latch is not transparent. 
	- When **EN=1**, PMOS is held **low** and NMOS is held **low** (via inverter connected to gate), leading to the transmission gate "blocking" the output of the feedback inverter into the main inverter. Solves issue of net-contention
	- 