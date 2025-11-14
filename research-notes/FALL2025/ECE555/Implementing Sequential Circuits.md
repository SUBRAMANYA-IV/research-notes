### One bit static memory using Bit-stability
![[Pasted image 20251114134455.png]]
- a single inverter has the given VTC
- 2 inverters in the given arrangement leads to 2 points of stability at $V_{out}$ and $V_{in}$
- able to hold memory, but need a way to "write" to this cell

![[Pasted image 20251114134621.png]]
- structure of a basic latch. 
- Only able to 'write' a value to the cell whenever clock is high 
- **Issues**:
	- note how if D is high, nmos acts as a pull-up transistor, hence leads to a voltage drop of $V_{th}$ between D and $n_{1}$
	- inverter $fb$ will fight back. that is, will compete with $D$.
		- ie, if stored value is 0, $fb$ is outputting a 0. $D$ driving a 1 leads to contention at net $n1$, leading to $fb$ trying to maintain a 0 while $D$ is attempting to drive a 1. 
###### Address the Vt drop issue
![[Pasted image 20251114135007.png]]
- Issue of weak-drive can be solved by using a pass gate
	- When Enable is high, NMOS is on, inverter drives low, turns PMOS on
- **still** suffers from 2 issues:
	- Drive strength f input to overcome contention of $fb$ path: $D$ **needs** to be stronger than $fb$, so either $fb$ needs to be resized (W/L) to be weaker, or gate driving $D$ needs to become stronger
	- **Loading on output to avoid a charge share write back**
###### Cutting Contention due to feedback path
![[Pasted image 20251114135251.png]]
- Add a transmission gate to the feedback path
	- disconnect the feedback during a write operation
	- contention is now solved; only a single value drives the net during a write stage

