#### What a program wants
- A memory space of arbitrary size
	- More memory than the system physically has
- to think its the **only** program running
	- load/store addresses are defined independent of the environment
- Protection from the misuse of data
	- some data is private, read only, executable, etc. 
#### review: virtual memory 
- with virtual memory, can think of main memory (DRAM) as  **cache**
- **Block size**
	- pages, usually 4kb or larger
- **associativity**
	- Fully associative, i.e a cache block (or in this case, a page) can be placed anywhere within memory 
- **replacement policy**
	- managed by the OS
- **Write policy**
	- Write-back
		- A write to DRAM results in a page being marked as **dirty**: upon eviction, gets written to the disk, otherwise not. 
	- write-allocate
		- a write to a location not within main memory results in an eviction of a page from the page table, retrial of the requested page, and then writing to that page. 
- **NOTE**: recall that the stack grows **down**, i.e *decrementing address*. hence, all processes think their stack starts at the address 0XFFFFFFFF, and each push onto the stack "decrements" this address, i.e 0XFFFFFFFC, 0xFFFFFFF8, etc.
###### Exercise 1
- Assume a 32 bit machine with 64 Kb pages and 256 MB physical memory: calculate the number of bits for...
- ###### Virtual address offset
	- each page is 64 KB. 64=2^6, 1 KB=1024 bytes=2^10 bytes. 2^6 * 2^10 gives 2^16 bytes per page, requiring 16 bit virtual AND physical page offset. 
- **Virtual Page Number**
	- independent of physical constraints, only dependent on system bit size. 32 bit machine, hence 2^32 total bytes. each page is 2^16 bytes, hence 2^(32-16) or 2^16 virtual pages, requiring 16 bits for the virtual page number
- **Physical address offset**
	- equal to the virual page offset, or 16 bits. 
- **Physical Page number**
	- physically constrained. 1 megabyte=1024 kb, 1kb=1024 bytes, 1 megabyte=2^(10+10) bytes, or 2^20 bytes. 256=2^8, hence 2^28 total bytes in physical memory. Each page is given to be 2^16 bytes, hence the physical memory can have 2^12 pages, requiring 12 bits to encode. 
###### Exercise 2
- how big is  page table in the following machine? 
	- 32 bit machine
	- 4 Kb pages
	- 4 Bytes per page table entry
- ###### Size of page table
	- each program believes it has access to entire 32 bit memory space, hence 2^32 bytes. 
	- each page is 4 kb=2^(610+2)=2^12 bytes
	- virtual memory hence contains 2^(20) pages
	- page table will need to be of same size (mapping each virtual page to a physical page), hence will have 2^20 entries. 
	- each entry is 4 bytes big, hence 4 * 2^20 bytes in total for the page table. 
	- 2^20 is 1 megabyte, hence 4 megabytes per page table.


#### Page table organization
- single-level page table occupies *continuous* region in **physical memory** (DRAM). 
	- in previous example, every page table will be 4 megabytes big, **regardless of how much virtual memory is used**
	- even a tiny program will use an entire 4 megabytes of memory **just** for the page table!
#### Multi Level Page tables
- method for making page tables **smaller**:
	- tree of page tables
	- at last level, tables contain Page Table Entries (i.e, mapping of virtual memory to physical memory)
	- at first levels, table contains pointers to *later level* page tables
	- different bits of **virtual page number** are used to index into different levels: L1 uses MSb
###### Figure 1: example of multi-level page table
![[Pasted image 20251217002937.png]]
#### Example of multi level page tables
- Assume 32 bit machine with 4 Kb pages 
- assume 4 byte page-table entries and each L2 Page Table is 4 KB in size
	- each virtual address space is 32 bits large, and each page is 4kb large. 
	- 2^32 bits for virtual address space, and each virtual page is 2^(2+10) bits large. 
	- 2^12 bits for the page offset, and 2^20 bits for the virtual page number. 
	- Divide the 20 bits of the virtual page number into 2 parts: L1 VPN and L2 VPN
	- L2 is the final/leaf of the tree, hence is the *actual* page table entries. Given that each L2 Page table entry is 4kb in size (i.e, can contain 2^12 mappings from virtual page numbers to physical page numbers), and that a single entry is 4 bytes large, this means 2^(12-2) locations are required, 2^10. 
	- The remaining bits are used for the L1 VPN. 

#### Example 2:
- ###### Assume program with 2MB of code, 64 Kb of stack, 16 MB of heap. How much storage is used for the Page Tables?
	- a single program will have a virtual address space of 2^32 bits. 
	- given that page table *entry* is 4 bytes large, and that each L2 page table is 4KB in size. 4Kb=2^(2+10)
	- 2^20 bits used for VPN's, can be split into L1 and L2. 
	- 2MB=2 * 2^20 =2^21 bytes for code
		- given each page table is 4kb=2^12 bytes in size, program requires 2^9 pages. 
		- recall that 2^10 bits are required to address each 4kb page entry table, ad since 2^9<2^10, only 1 L2 page entry table is required
	- 64 kb=2^(6+10)=2^16 bytes of memory for the stack
		- given each page table is 2^12 bytes, stack requires 2^(16-12)=2^4 pages
		- given that a single page entry table can address 2^10 pages, only requires 1 L2 page entry table 
	- 16 MB=2^(4+20)=2^24 byes for the heap. 
		- given each page table is 2^12 bytes, requires 2^12 pages, or 4 * 2^10 pages. 
		- each page table can address 2^10 pages, so requires 4 page tables 
		- requires 4 L2 PT's. 
- In total, only 4 KB of pages are allocated. Far less than 4Mb for a single level page entry table
#### How can you organize the multi-level page table?
- only allocate the second (and later) page tables when needed
- program starts: everything is invalid, only first level is allocated 
![[Pasted image 20251217014003.png]]
- As more accesses are done, second level page tables are allocated. 
![[Pasted image 20251217014045.png]]
###### Figure 2: Detailed view of 2 level page table 
![[Pasted image 20251217014122.png]]
- page table register points to the beginning of the page table for a given program
- first level offset indexes into the first level page entry table 
- content of indexed location points to the beginning of the second level page table 
- 2nd level offset indexes into the physical page number 
- page offset accesses specific byte
#### Example 3: 
- Continuing from previous example. Each page table entry is 4 bytes large. 
- **what is the least amount of memory that can be used? when would this happen?**
	- least amount of memory is used when program just starts: no second level page table exists, and the first level page table is just empty. 
	- 2 ^ 12 bytes required. 
- **what is the most amount of memory that could be used? when would this happen?**
	- occurs when the program has allocated a page in every one of the first level page entry table. 
	- first level page table is addressed by 10 bits, so 2^10 values. 
	- 4 kb for first level page table, and 1024* 4kb for each second level page table. This is equivalent to 2^(10+10+2)=2^22 bytes
- **how much memory is used for this memory access pattern?**
	- 0x00000ABC,0x00000ABD,0x10000ABC,0x20000ABC
	- initially, only allocate first level page table. all values in this table are empty/invalid. 
	- first access, page fault: read from disk. L1 VPN=000, L2 VPN=000, offset=ABC
	- second access, page hit: L1 VPN=000, L2 VPN=00