#### Virtual Memory Performance 
- To translate a virtual address into physical address, we must first acess the page table in physical memory. i.e, before the CPu can even read/write the data, it must look up that virtual-to-physical mapping (DRAM access). 
- if its an N-level page table, must do N total loads before getting physical page number. 
- for each level:
	- compute index from virtual address
	- use index to load entry from memory
	- that entry (i.e, index's corresponding value) tells where the next-level *table* begins
	- Example (2-level):
		- given VPN, inspect upper bits to index first-level table
		- load value stored at that index (**first load**)
		- use that loaded value to index second-level table 
		- load value stored at that index (**second load**)
		- this is the **virtual-to-physical page map**, or the **page number**
- for a **load** instruction, you must...
	- read the page table entries (N reads, where N is number of levels)
	- read actual data from physical address
- for a **STORE** instruction, you must...
	- read the page table entries (N reads, where N is number of levels)
	- Write the actual data to the physical address. 

#### Translation look-aside buffer (TLB)
- fix this performance problem by avoiding min memory in the translation from virtual to physical pages
- buffer common translations in a TLB, a fast cache memory dedicated to storing a small subset of valid V-to-P translations. 
#### Figure 1: TLB diagram
![[Pasted image 20251217022746.png]]
- Note how the TLB here is a fully associative set, i.e only contains a tag. 
- note how the TLB doesn't contain an offset, as each block is just 1 page table entry
- inspecting the virtual page unmber being requested, compares it against the tag. If it matches, then its a **TLB hit**
- from here, the corresponding **physical page number** is accessed
- physical address is formed by joinig the physical page number and the page offset
- this address then goes through the standard cache hit/miss protocol
- if **miss**, then perform a page walk
#### Page walk
- for each level:
	- extract index bits from the virtual address
	- use bits to select an entry from that page-table level
	- read that entry from memory
	- that entry gives the physical address of the next-level page table
- repeat until the leaf page-table entry, which contains he physical page number. 
- finally, combine the physical page number with the pge offset to produce the physical address
- insert this translation into the TLB buffer for future use. 
#### TLB reach
- TLB reach = number of TLB entires * page size
- e.g, 64 entries with 4 kb pages = 256 kb reach. 

#### Implementations of the TLB 
##### Physical (PIPT cache)
- **Physically indexed, physically tagged** 
- both set index and tag are derived from the physical address