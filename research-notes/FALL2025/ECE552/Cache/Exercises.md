###### Exercise 1
 - *Assume that the L1 cache is only accessed for load and store instructions. The global L1  miss rate is MG1 = 1/30 and the local L1 miss rate is ML1 = 10%. What fraction of instructions in the program are a load or a store?*
	- Global miss rate is given with respect to misses per unit instruction
	- if global miss rate is 1/30, implies 1 miss (load or store) per 30 instructions
	- local miss rate is given with respect to misses/accesses
	- 10% local miss rate implies 1/10, ie 1 miss per 10 accesses. 
	- $\frac{\text{1 miss}}{\text{30 instructions}}\div\frac{\text{1 miss}}{10 accesses}=\frac{\text{10 accesses}}{30 instructions}=\frac{1}{3}$
##### Exercise 2
- *in a typical memory hierarchy, the accesses to the L2 cache are the misses from the L1 cache. Given: Global L1 Miss Rate: MG1=1/20, Global L2 Miss Rate: MG2=1/80, what is the local miss rate of the L2 cache?*
	- global miss rate is given as **miss\num_instructions**
		- L1: 1 miss per 20 instructions, L2: 1 miss per 80 instructions
	- L2 is **only** accessed when L1 misses, hence
		- L2 access/instruction=L1 miss/instruction=1/20=$A$
		- L2 miss/instruction=1/80=$B$
		- L2 miss/access=$B/A=\frac{1}{4}$
##### Exercise 3
- *Assume A 1-cycle L1 with 5% miss rate, 10 cycle L2 with 20% miss rate, 50 cycle main memory. How much higher is AMAT if L2 was removed?*
	- original AMAT given as
		- $1+0.05*(10*0.2*(50))=2$
	- if L2 was removed, L1 directly accesses memory, giving
		- $1+0.05*(50)=3.5$
##### Exercise 4
- *assume a 5 stage pipelined processor that stalls on every cache miss. the base CPI is 1 (with an L1 access time of 1 cycle). The running program consists of 30% load/store instructions. the L1 instruction cache miss rate is 2%. the L1 data cache miss rate is 10%. The main memory access latency is 10 cycles.*
	- **NOTE**: load/store only applies to *data cache* not instruction.
	- for 5 stage pipelined, assume it fetches 1 instruction per cycle. 
	- Base CPI+I-Stall cycles + D-stall cycles
		- $1+0.02*10+0.3*0.1*10=1.5$, 1.5 CPI

##### Exercise 5
- 

##### Exercise 6
![[Pasted image 20251118075840.png]]
- 64B per block, all holding integers, so 16 integers per block
- 32768 integers, so full iteration leads to loading of 
##### Exercise 8
![[Pasted image 20251118085541.png]]
- **write-allocate**: if writing to memory and not in cache, load into cache first
- cache is total of 64 bytes
- a single block is 16 bytes
- 64/16=4 blocks of data
- 2 way associative, ie each set has 2 blocks
- 2 sets, hence set_index=1 bit
- byte addressable, so smallest unit is a byte, hence for 16 byte block, 4 offset bits
- tag bits=11

##### Exercise 9
![[Pasted image 20251118090035.png]]
- Period=2 nanoseconds
- main memory latency=50 clock cycles
- base cpi is 1
- stall due to instruction cache: $0.03*50$
- stall due to data cache: $0.06*(0.15+0.2)*50$
- stall due to branch: $0.4*0.2*1$
- stall due to load-use: 