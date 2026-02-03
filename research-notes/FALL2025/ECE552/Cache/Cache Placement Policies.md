- answer the question "where can a block of memory go"
- [[cache associativity]] is a spectrum; [[fully-associative]] is on one extreme of the spectrum, and [[direct-associative]] is on the other end. 

#### Fully-associative cache
- *any* memory block can go into *any* cache line
- **no index field**; the entire decision is based on tag-matching
- requires **comparing against every tag** -> lots of hardware
- very flexible, very low [[conflict misses]]
#### Direct-Mapped cache
- each memory address can go in **exactly one slot**
- uses **index bits** to choose the single allowed line
- requires just **one comparator** 
- super cheap, super fast, but **highly prone to [[conflict misses]]**

- recall that, in all previous examples, the tags could be located anywhere; no ordering, no grouping, hence every tag had to be compared to get the desired address
###### Figure 1: Example of a Direct-mapped cache
![[Pasted image 20251118043641.png]]
##### IMPORTANT
- BIG difference between 
	- "every block has its own location in cache" **FALSE**
	- "every block can *only* go to one place in cache" **TRUE!**
- for example, the later implies that "every memory address with bits 00 at index $M[2:1]$ can **only** go to cache line-index 0"
- So a general flow for searching things up in a direct mapped cache goes like 
	- I know that if the block I want is in the cache, it HAS to be at this location
	- check the tag of that location: if it matches, HIT!
	- then retrieve the specific *word* from the cache, given by block offset. 

#### Figure 2: Direct mapped, write-back, allocate-on-write cache
![[Pasted image 20251118051856.png]]
- **IMPORTANT**: note how a replacement policy is **useless** here
	- for a direct-mapped cache, we *already know* where the block retrieved from memory must go: there's a single place it **can** go. 
	- hence, no point of LRU, as no decision to make
- First load instruction **misses**:
	- load contents of memory addresses $M[0],M[1]$ into **Cache index 0**
		- note how the addresses are 0000 and 0001: LSB corresponds to offset, 0 corresponds to index bit (hence, index 0), and MSB 2 bits corresponds to the tag bits: used for validation that correct content is there. 
- Second load instruction **misses**
	- $5_{10}=0101_2$, hence first checks index 1 of the cache
	- checks the *tag* of index 1. $01\neq00$, hence we know its a **miss**
	- must load the required block into cache
- Third store instruction **misses**
	- $2_{{10}}=0010_{2}$, hence index bit is 1. 
	- given **write-back** policy, *only* modify memory once cache is evicted
	- fetch data-block $0010,0011$ into cache-index 1, set tag bits as 00
	- modify word at offset 0
	- **set dirty bit**
- fourth store instruction **misses**
	- $7_{10}=0111_{2}$, hence index bit is 1, which is occupied by previous store
	- Write content of cache-index 1 to memory
	- load content of $0110,0111$ into the cache-index 1
	- write contents of register 1 into cache-index 1, offset 1
- fifth load instruction is a **hit**
	- $4_{10}=0100$, hence index-bit is 0
	- check tag bit at index 0: **matches**
	- nice! found a hit, now load the content of that memory from cache into register 2

#### Set-Associative cache
- mid way between [[fully-associative]] and [[direct-associative]].

#### Figure 3: 2 way set-associative cache
![[Pasted image 20251118054833.png]]
#### Example 1
- *Given 32-bit addresses and 64B blocks, what is the number of tag bits for a 16-way associative 128KB cache?*
	- assume byte-addressable
	- 64B blocks means block-offset bits=6 bits
	- total number of lines is hence $\frac{128*1000}{64}=2000$ 
	- 16 way associative implies that each set has 16 lines, hence 125 sets
	- to encode 125 sets, requires 7 bits
	- rest of the bits goes to tag bits, 19 bits. 

#### Example 2
![[Pasted image 20251118062107.png]]
- First Load instruction **misses**:
	- load content of memory address $M[0], M[1]$
	- $1_{10}=0001_{2}$. set-index is 0, and tag bit is 00. 
		- can be put *anywhere* within set 0
- second load instruction **misses**:
	- $5_{10}=0101_{2}$. set index is 0, and tag bit is 01
	- load into set 0, look for empty block. 
- third store instruction **misses**:
	- $7_{10}=0111_{2}$. set index is 1, and tag bit is 01
	- **allocate-on-write policy**: load contents of $0110,0111$ into the cache
	- write contents of $R[2]$ to this location, and set dirty bit
- fourth store instruction **hits**:
	- $4_{10}=0100_{2}$. set index is 1, and tag bit is 01. HIT!
	- offset bit is 0. write to word in block, set dirty bit.
- fifth load instruction is a **hit**:
	- $0_{10}=0000_{2}$. Set is 0, tag is 00. HIT!
	- load content from cache into register 
- sixth load instruction **misses**:
	- $8_{10}=1000_{2}$. set is 0, tag is 10. 
	- **evict least-recently used block**
	- Write evicted block to memory
	- load contents of requested memory into cache
	- 

#### Tags
#computer_architecture
#ece552
#cache 