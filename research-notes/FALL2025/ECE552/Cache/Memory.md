- So far, only 2 types of memory have been covered
	- Register File: small array of words, stores values that are immediately used, or in the near future.
	- Memory: larger array of words, stores values for long-term storage. 

#### Types of memory
- **Registers**
	- Inside the CPU itself
	- **very expensive**: impractical to make all memory out of registers
	- **fastest** kind of memory: read times in the picoseconds
	- 
- **SRAM**
	- Each cell is made of 6 transistors
	- Volatile: needs *constant* power to maintain data
	- fast: ~1ns read time for small, high speed designs
	- Still (area wise) large. 
	- can only put ~MB's on a chip
![[Pasted image 20251117171435.png]]
- **DRAM**
	- Logically similar to SRAM
	- less expensive than SRAM
	- each cell is made of a transistor and capacitor
	- can put 10's of GB on current machines
	- Volatile, needs constant power to keep data
	- **destructive read**: must *rewrite* on a read (discharges capacitor on a read)
	- Slower than SRAM: needs ~50ns to access
		- CPU must stall for **dozens** of cycles on each memory load
![[Pasted image 20251117171633.png]]
- **Disk**
	- Hard-drives store bits as magnetic charges on a spinning disk
	- **non-volatile**: holds information even when no power is supplied
	- **very slow**: ~3,000,000 ns
	- **very cheap**:~0.0001$ per mb

#### Memory Hierarchy 
- only need to access a small amount of data at a time
- Use **SRAM** to store data that's immediately required
	- called the **cache**
	- able to keep up with processor clock speed
	- small (~kilobytes)
- use large amount of **DRAM** as main memory
	- can scale to ~gigabytes in size
![[Pasted image 20251117172401.png]]

#### A closer look
- Recall that in the projects, instruction memory and data memory were provided as single, homogeneous constructs given by the test bench
- in reality, entire blocks of instruction and data memory are loaded into the cache from the **dram memory**, hereafter just referred to as the memory. 
###### Figure 3: Detailed Memory Hierarchy
![[Pasted image 20251117173922.png]]
- the model above demonstrates this principle
- Note how the L-1 cache is *split*, i.e instructions and memory data are stored in separate caches
	- Pros: Maximizes bandwidth and minimizes latency (better physical proximity, different requirements)
- L-2 and L-3 caches are unified, meaning data and instructions are stored in the same physical cache. 
	- Pros: Flexible allocation of space for max capacity 
	- reduced complexity and cost (less access ports)
- **inclusive Vs Exclusive Caching**
	- **IMPORTANT**: different from split/unified cache!
	- **Inclusive**: ie, a block X in L-1 **must** also be in L-2
		- + faster miss handling
		- + simplified coherence (e.g, L-2 acts as a single point of truth)
		- - wasted capacity (duplicate of value held in both L-1 and L-2)
		- - backward invalidation overhead 
	- **Exclusive**: i.e, a block X in L-1 **must not** be in L-2
		- + maximizes capacity (No duplicates of data/instructions)
		- - slower miss handling
		- - not coherent

#### Example
###### Figure 4: CPU with cache access
![[Pasted image 20251117175142.png]]
- instruction attempts to load content of memory into register t1
- *after* instruction is loaded into EX/MEM Stage
	- at rising clock edge, attempts to access memory address from cache
	- Cache reads are **combinational**, so once instruction is loaded into EX/MEM, can immediately tell if a value is present in the cache or not. 
	- at the next rising clock edge, look up 4000 (causes a miss, hence a fetch from DRAM)
	- at next rising clock edge, look up 4000 **again** (this time, should be loaded into cache)

#### Memory locality
- **Temporal Locality**
	- Program accesses the same memory location repeatedly 
- **Spatial Locality**
	- Program accesses *nearby* locations around the same time
###### Figure 5: memory accesses in a loop
![[Pasted image 20251117182817.png]]
- Note how the inner loop has $I$ as its access index
- for each value of $I$, the **same value** is accessed 4 times in a row, with respect to the $J$ index. 
- this demonstrates *temporal* locality, as the same value is accessed multiple times in a short span of time
- conversely, an arrays values are allocated in a single, contiguous block of memory, hence accessing values $A[0] \to A[7]$ demonstrates *spatial* locality
###### Figure 6: Comparison of performance. 
![[Pasted image 20251117183357.png]]
- recall that arrays in memory are "unrolled" from a 2-d representation in code to a 1-d allocation in memory
- ie, arrayInt goes from a 2-d matrix of dimensions 20,000x20,000 to a 2-d array of dimensions 1x400,000,000.
	- Accessing index $(i,j)$ in 2-d implies the $ith$ **row** and $jth$ **column**
	- accessing index $(i,j)$ in 1-d implies index $i*20,000+j$ in a 1-d array. 
- Hence, the first loop would be FAR more efficient: accesses values indexed along the 1-d array between $0\leq j\leq20,000$, and then increments $i$> 
- conversely, second would be incredibly inefficient: i and j are swapped here, hence the expression becomes $\text{index}=20,000*j+i$, hence incrementing the index by 20,000 each time a new value is accessed; bad spatial locality 

#### Tags
#computer_architecture
#ece552
#cache 