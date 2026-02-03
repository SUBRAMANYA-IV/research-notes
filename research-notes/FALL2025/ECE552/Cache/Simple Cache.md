###### Figure 1: simplest cache model
![[Pasted image 20251117185852.png]]
- only considers the **load** instruction
- word-addressable address space
- consists of a single, word-size storage location to remember last loaded value

- Whenever memory returns data, store it in the cache
- need to know *what* address this data corresponds to, so store a "tag"
- also include a "valid" status bit to know if the content of that line is usable 

-  direct **memory** to **pipeline** yields approximately 1 op / 100 cycles
- using a cache reduces this to **1 op/ 1 cycle**

#### Example
###### Figure 2: Program with simple cache
![[Pasted image 20251117202227.png]]
- figure shows a setup with a simple cache with **2 lines of capacity**
- **instruction flow**
	- load I1 into EX/MEM pipeline stage: cache is **combinational**, so immediately know that a miss occurred: stall
		- at next clock edge, get data from memory, store into cache
		- at *next next* clock edge, get data from cache and store into local register
	- load I2 into memory: Miss,Stall, etc etc. 
	- I3 leads to a **hit**, as tag 1 is already present in cache
	- I5 leads to an *eviction* of content stored at tag 5, as this was the **least recently used** (policy, LRU)
- **Overhead**: how much of the cache entry is *metadata* instead of useful data
	- Note that in the example above, 1 bit is used to signify if the line is valid, and 4 bits (encoding tag values between 0 and 15) is used as *metadata* instead of raw data. 
	- Data is encoded in 8 bits (250 requires 8 bits to encode)
	- hence, **overhead** is given as $\frac{1+4}{8}=62.5\%$. 
	- **larger overhead is bad**: indicates that more bits are wasted in describing metadata instead of actual, usable data. 

#### Increasing Block Size
###### Figure 3: Comparison of different block sizes
![[Pasted image 20251117203426.png]]
- **block**, or a **cache line**, refers to the smallest unit of data that the cache moves between memory and cache. i.e, a fixed-size chunk of memory that the cache treats as **one unit**
	- ie, in a block size of *1 byte (8 bits)*, every block contains *1 byte* of data
	- in a block size of *2 bytes (16 bits*, every block contains *2 bytes* of **contiguous memory data**
- In the example given above
	- **case 1**: 1 block of cache contains 1 byte (word) of memory 
		- Requires $\log_{2}(\text{\# blocks in memory})=\log_{2}16=4 \text{ bits}$
	- case 2: 1 block of cache contains 2 words of memory (in this case, a byte)
		- blocks of cache in memory: $\frac{16}{2}=8$
		- requires $\log_{2}(8)=3$ bits
		- **NOTE**: overhead is the number of bits used as meta data **per block of cache**
		- hence, yields an overhead of $\frac{3+1}{8+8}=25\%$, as now a single block of cache can hold **2 bytes of data**
- **Tag Value From Address**:
	- Given a block size $N$, the tag from address can simply be given as 
	$$
	tag=\left\lfloor  \frac{\text{address}}{\text{block size}}  \right\rfloor 
	$$
	- For example, an address of 11 (decimal) yields tag of 5
		- Note how the *floor* function is used here: it retrieves blocks of contiguous data **aligned** to the data-memory
###### Figure 4: Tag and Offset
![[Pasted image 20251117210209.png]]
- To distinguish words within the *same* block, we need $\log_{2}(\text{block size})$ additional bits. 
	- For the case of block size 2, requires 3 bits to encode entire address, and 1 bit to encode **offset**
- **Intuition**: the tag segregates the memory into $2^{\text{tag}}$ number of contiguous blocks of words, while the offset specifies where *inside* each block the desired word is located
- **WHY?**: this just recreates the original memory organization, right? you still need the same number of bits to represent the number of blocks, and the offset *within* each block...right?
	- Kinda... However, recall that **the cache's blocks are not contiguous, evenly incremented** like the actual DRAM memory is 
	- for example, at a given time the cache can contain like 0,8,4,2...
	- hence, requires **comparators** to get the requested address/tag: paralel in nature (needs to be fast), and hence **expensive in hardware**. 
###### Figure 5: example of multi-line cache blocks
![[Pasted image 20251117232325.png]]

#### Participation Question 2
![[Pasted image 20251117233339.png]]
- recall that an integer on a 32 bit system is **4 bytes**
- implies that, at any given time, the cache contains 4 consecutive integers in a given block
-  ```int A[256]``` allocates 256 contiguous lines in memory
- iterates through the loop, accessing the **same index** 4 times in a row, then incrementing to the next
	- At first retrieval,miss due to cache being empty
	- fetch 16-byte block, i.e $A[0] \to A[3]$, store in cache
	- 3 hits *each* due to temporal locality for $A[0] \to A[3]$, hence $3*4=12$ hits for temporal locality
	- 3 hits for spatial locality 
	- once $i=4$, misses again, and must repeat process. 
	- in total, *should* be

#### Tags
#computer_architecture
#ece552
#cache 