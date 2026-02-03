#### Types of memories used
###### Figure 1: Classification of Memory 
![[Pasted image 20251208034547.png]]
- **Read-Write Memory**
	- memories that can both be written to and read from
	- **Random Access**
		- Any memory location can be accessed at any time
	- **Non-Random Access**
		- structured read/write order; stored values cannot be read at random, must be accessed in some order relative to which they were stored 
		- e.g, FIFO maintains first in first out structure 
	- **DRAM**
		- recall that DRAM consists of a transistor or capacitor; reading is **destructive**, requires a read to be followed with a **write** of the same value
	- **SRAM**
		- consists of 2 inverters feeding into each other, written to via a bit line and accessed via 2 transistors; technically pass gate logic? 
- **Non-volatile read-write memory**
	- **EPROM**
		- Erasable Programmable Read Only Memory
	- **EEPROM**
		- electrically erasable version of EPROM
- **Commonalities among all memories** 
	- N-words of M-bits wide are accessible, i.e 1 standard word of data 
	- laid out in arrays, grids
	- accessed by encoded addresses (in the case of Random Access memories?)
	- **implemented as dynamic circuits**
		- i.e, precharge and discharge stages; combinational logic depends on the clock

#### Memory Arrays
###### Figure 2: Example of memory array with 16 8 bit words
![[Pasted image 20251208040822.png]]
- **Wordline**: axes along which whole words are stored, i.e 16,32,64 etc. 
- **Bitline**: axes along with bits *of* a word are stored
- Design works for smaller memories; but what about larger ones like 256 8 bit words?
	- bit line sense and write remains the same complexity, but address is now a 
	- 8 to 256 decoder, complicated, expensive combination circuitry, slower access times, etc. 

#### Bit-planes
###### Figure 3: splitting of bitlines to reduce delay
![[Pasted image 20251208043139.png]]
- Splits the address into two components; upper 5 bits selects the **word line** across **all** bitplanes
- lower 2 bits selects the **bitline** across **all** bit planes. 
- combined, yields the 8 bit word, split across 8 bit planes
- using a single bit plane like the previous example, would require  height of $2^8=256$ bits tall for the bitline, and 8 bits wide for the wordline. 
- using bit planes, reduces the bitline height to 128 bits. 
#### Figure 4: example of bitplane
![[Pasted image 20251208044858.png]]
- each block stores $128WL \times 32:1 BL$
	- i.e, 128 words of size 32 bits; $32*128=4096$ bits. 
- bits $[4:0]$ selects 1 of 32 bit lines
- bits $[11:5]$ selects 1 of 128 word lines

#### Hierarchical Banking
###### Figure 5
![[Pasted image 20251208045953.png]]
- offers better aspect ratio, shorter wires *within* blocks AND block address activity activates only 1 block, giving power savings. 

#### Timing for memory reads and writes
- recall that almost all memories operate as **dynamic memories**, the combinational logic relies on a precharge and evaluation stage. 
###### Figure 6: example of read/write process from dynamic memory![[Pasted image 20251208050545.png]]
- Address presented to the memory **must** be stable before the evaluation stage, in this case the low-clock cycle. 
- Data_in must be stable before a write to the bitlines, during the precharge state. 
- If a bitline is **falsely discharged**, it is catastrophic
	- no possible recovery, and wrong data will be read out
- must ensure that the **address** has propagated through the decoder (word-line decoder) before allowing the bitlines to discharge

###### Figure 7: construction of ROM memory
![[Pasted image 20251208053708.png]]
- while the clock is **high**, the signal is first **inverted**, hence the pre-charging PMOS is activated, charging all the bitlines to 1. 
- while the bitline is charged to 1, the signal $d_{out}[0]\dots d_{out}[n]$ is driven by a weak inverter. 
- when the clock is **low**, inverted signal becomes **high**
	- turns of pre-charging PMOS
	- at this time, address should be decoded, and all the NMOS devices in a given line will be turned on
	- bitlines will be discharged through this NMOS to ground, which will drive the bit line **low**
	- signal becomes inverted, sets the output of the bitline to **high**
	- second PMOS is required to maintain state. 
- Note that the **sensing** inverter should have a **high skew**, i.e faster transition from **Low to High**
	- given that during the precharge phase all the lines will be pre-charged to 1