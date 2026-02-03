- so far, working with the abstraction that all programs have **full, private access** to memory. I.e, the program has access to the *entire* 32 address. 
	- But in reality, multiple programs run at the same time
	- what if two programs try to write to the same memory address?
#### Figure 1: system view multitasking 
![[Pasted image 20251216221021.png]]
- recall that the static data is the storage location for **global variables** and **static variables**, i.e variables which retain their value across function calls. 
	- this region is loaded when the program starts
- the heap is where the program explicitly requests blocks of memoryd ruing **runtime** to store data like arrays whose size *isn't* known until the program is running
- the **stack** is used for *function calls*: each time a function is called, a new **stack frame** is pushed onto the stack
- note that the physical memory, DRAM is smaller than the sum of *all* the program's memory. 
#### Memory: 2 issues
- Second issue is that even if only one program is running, modern computers have 64 bit address spaces
	- No computer has $2^{64}$ bytes of memory 
	- what happens if a computer tries to write to an address $0\times FF\dots FFF$?
	- should it just crash? (of course not)

#### Solution
- Modern systems use the same solution for both problems: **virtual memory**
- each program **thinks** it has full, private access to memory (can safely index any address from $0 \times 0\dots 0 -0 \times F\dots FFF$)
- **hardware AND software** transparently maps these addresses to distinct addresses in DRAM and hard disk/SSD
#### Goals of virtual memory
1) **TRANSPARENCY**
	- one program doesn't need to know how other programs are using memory
2) **PROTECTION**
	- No program can access the data of any other program
3) **Programs NOT limited by DRAM capacity**
	- each program can have more data than DRAM size

#### Basics of Virtual Memory
- **virtual** implies the use of a level of *indirection*
- virtual memory hardware changes the **virtual address the programmer sees** to the **physical one the memory chips see**

#### Figure 2: Virtual to Physical memory translation
![[Pasted image 20251216221918.png]]
- figure demonstrates how the programmer and the program "thinks" its using memory
	- i.e, on a read/write, the programmer and program think they're accessing the byte stored at location 0x800, but during run time, this address is translated to the physical address of 0x3C00 by the MMU
#### Figure 3: Example of 2 programs using virtual memory
![[Pasted image 20251216222224.png]]
- figure demonstrates how 2 programs map their virtual memories to physical memory in DRAM
- this figure solves issues 1 and 2 of multitasking 
	- program A doesn't need to know how program B is using its memory to allocate its own useage of memory 
	- the programs are mapped such that they never overlap, or access each others memory, making them **protected**
#### How to translate address?
- address translation isn't *entirely* done by the hardware
- gets help from the **operating system** (one of the key features/reasons for an operating system)
- **What is an operating system?**
	- a special set of programs that have the following properties
	- **always running** (after the system boots)
	- in charge of **managing the hardware resources** for all other running programs
		- e.g, initializing memory for starting a program, managing the file system, choosing when a particular program gets to run, etc. 
	- and **translating virtual addresses into physical addresses**
	- Operating system handles address translation by keeping a data structure in **main memory**: the **page table**
#### Virtual memory terminology
- Memory is divided into fixed size chunks called **pages** (e.g, 4 KB for x86)
- the size of a physical page is **equal** to the size of a virtual page. 
- the **virtual address** is composed of...
	- a virtual page number: identifies *which* page, i.e which 4 KB block of memory within the programs massive virtual address space the CPU is trying to address
	- a page offset field (low order of bits): identifies the *byte location* within that page. 
- Translating a virtual address into physica address:
	- requires translating *page number*, i.e which 4KB block of physical memory to access
	- keep the page offset the same: i.e, within the 4KB block, which byte do you want to access?
#### Translation process
1) **input**: a program provides a Virtual Address (to the MMU?)
2) **Lookup**: the **virtual page number** is used as a *key* to lookup an entry in the page table
	- Recall that the page table is a mapping between virtual pages and physical pages. i.e, if a virtual address call is attempting to access the virtual page of index 5, the page table would translate this into a physical page number of say, 1023
3) **output**: the page table entry provides the corresponding **Physical Page Frame Number (PPN)**: this PPN ells the system *where* the requested page is located in the physical RAM
4) **Construction**: the PPN combined with the original **page offset** (which is unchanged** to construct the final **Physical Address**
	- Recall that the Upper bits correspond to pages while lower bits correspond to the page offset. 

- **Example process**
	- program attempts to load value stored at *virtual* memory location 0x123
	- Upper 20 bits are 0, while lower 12 bits gives an offset of 123. virtual page is given as 0
	- in the **page table**, the virtual page of 0 is mapped to the **physical** page of say, 20. 
	- indicates that within the RAM, the equivalent *virtual* address is located in the index-20 page, or 4Kb block

#### Page Table
- page table is a *map* that the computer uses to locate data. 
	- index of the *entry* is the virtual page number
	- value **stored** at that entry is the corresponding Physical Page Frame Number (PPN), which is the starting location in physical RAM. 
- each process has its **own** page table:
	- maintained by the OS
	- page tables themselves are kept in memory by the OS, and OS knows the physical address of the page tables. 
	- No address translation is required by the OS for accessing the page tables. 
#### Figure 4: Page table
![[Pasted image 20251216225816.png]]
- ensures that page table entries *across* different programs dont contain the same **physical page number**
#### Why pages?
- otherwise, requires a mapping entry for every single element of memory
	- i.e, for every virtual address, must store some entry to "translate" it into the physical memory 
- destroys spatial locality otherwise
	- e.g, if a virtual memory attempts to read 2 subsequent bytes, i.e 0X1 and 0X2, if paging was not used, in physical memory this *could* correspond to addresses 0x1 and 0xF. Terrible for spatial locality. 
- Eliminates external fragmentation
	- available memory gets split into many small, **non-contiguous** blocks. Due to padding, leads to significant memory wastage

#### Components of a Page Table
#### Figure 5: simple page table
![[Pasted image 20251216230445.png]]
- **Page Table Register**: contains the address that points to the *beginning* of the page table in main memory. Recall that each program has its own page table. 
- Virtual page number indexes the page table, and the value stored at that index corresponds to the physical page number. Page offset is maintained. 

#### How to not be limited by DRAM capacity? 
- Take a system with 8GB of RAM. given a page size of 4KB, this implies that the RAM can have a total of ~2 million pages. 
- Use the **disk** as a temporary space in case memory capacity is exhausted
	- called the **swap partition** in linux-based systems. 
- **problem**: without a fallback, if the physical RAM is exhausted, the OS will have to kill processes to free up memory, leading to crashes or instability 
- **swapping**: when RAM is full, the OS's memory management unit identifies the memory pages that are currenly *inactive* (based on OS replacement polciy). It then copies these pages from the fast RAM to the slow swap space on the disk
- **swap space**: emergency overflow area. primary purpose is to maintain system stability when the physical RAM is full. 
- we can mark a page table entry as **invalid**, indicating that the data for that page doesn't exist in *main memory* (i.e, DRAM) but instead is located on the **disk**
- looking up a page table entry that corresponds to disk is called a **page fault**
#### Figure 6: Page fault
![[Pasted image 20251216232239.png]]
- Page table register points to the start of a page table for a given program
- program attempts to access some virtual memory location
- upper bits are used as the page-index
- **however**, the entry in the **page table** is marked as **invalid**, meaning that the page being looked up **does not exist in DRAM**, leading to a **page fault**
- How to handle a page fault
	1) Stop the process
	2) Pick a page from the current programs page-table to replace
	3) **write back the data**: i.e, transfer all the data corresponding with the evicted *physical* page from DRAM to Disk
	4) **get the referenced page**: i.e, copy the data from **disk** to **DRAM** for the requested page
	5) Update the page table with the new mapping 
	6) reschedule the process. 

#### Role of OS vs Computer Architecture 
#### Figure 7: difference between OS and architecture in memory management
![[Pasted image 20251216232746.png]]

#### Class problems 
- Consider a system with the following parameters: 
	- virtual address space: 32 bits
	- physical memory: 1GB (2^30 bytes)
	- page size: 4kb (2^12 bytes)
	- page table entry overhead: 3 bytes (valid, dirty, read only, etc). 
###### Calculate the number of bits used for the **page offset**
- page offset responsible for indexing within a page. given a page is of size 4kb, 12 bits required for page offset
###### Calculate the number of bits required for the physical page number
- physical page number needs to access each 4kb block/page within the *physical* memory: given that the memory has 2^30 bits, each 4kb block has 2^12 bits, then it can be divided into 2^(30-12) or 2^(18) physical pages, which requires 18 bits to index. 
###### Calculate the number of bits required for the virtual page number
- the Virtual address space spans 32 bits, implying 2^32 bytes of memory. this can be divided into 4 KB blocks **equal to the physical page size**, giving 2^(32-12) or 2^20 virtual pages. this requires 20 bits to index. 
###### Calculate the total number of page table entries. 
- given that each virtual page corresponds to the index in the page table, this implies there should be 2^20 entries in the page table. 
###### Calculate the total size (in bytes) of the page table
- there are 2^20 entries in the page table, each containing an 18 bit physical page number. In addition to this, theres a 3 byte overhead, implying (18/8+3) bytes per entry, and 2^20 entires. 
