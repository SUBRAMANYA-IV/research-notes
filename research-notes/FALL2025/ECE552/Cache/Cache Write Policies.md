#### What about stores?
- if the memory location is in the cache:
	- send it to cache
	- should it also be sent to memory? **write-through policy**
- if its **not** in the cache
	- write it *into* cache? **allocate-on-write policy**
	- write it directly to memory *without* cache allocation? **no allocate-on-write policy**
#### Write-through Cache
###### Figure 1: Example of Cache with write-through and allocate-on-write
![[Pasted image 20251118002224.png]]
- First load instruction **misses**
	- loads memory addresses 0 and 1 into cache
	- sets valid bit
	- tag is set as 000
	- then load $M[1]$ into $R[1]$
- Second load instruction **misses**
	- load content of memory addresses $M[6],M[7]$ into cache
	- sets valid bit
	- sets tag as 011
- third **store** instruction leads to **write-through**
	- content of $R[2]$ is **simultaneously** written to cache tag 000, offset 0 AND memory 0000
- fourth **store** instruction leads to **allocate-on-write**
	- destination in memory is address 0101, hence tag would be 010
	- store contents of

#### Write-back cache
- Defer writing data to main memory until the cached data is **replaced or flushed**
- Do we need to write-back ALL evicted lines? NO!
	- only need to write back blocks that have been **modified**
	- Keep a **dirty bit**: reset this bit when the line is allocated, set when the **block is stored into**. if a block is **dirty** when evicted, write its data back into memory
		- i.e, load an entire block for a read operation, but if no changes were made to the block, no point in writing back to memory
###### Figure 2: Example of Cache with Write-back and 
![[Pasted image 20251118010150.png]]
- first load instruction **misses**
	- load memory $M[1],M[2]$ into cache block
	- set dirty bit to 0
	- set tag to 000
	- set valid bit to 1
- second load instruction **misses**
	- load memory $M[6],M[7]$ into cache
	- set dirty bit to 0
	- set tag to 011
- Third store instruction **hits**
	- store content of register $R[2]$ into cache tag of 000, offset of 0
	- **set the dirty bit**
- Fourth store instruction **misses** (target address is **not** in the cache)
	- load the content of target address into cache, $M[4],M[5]$
	- change tag to 010
	- Store content of register $R[5]$ into cache tag of 010, offset of 1
	- **set the dirty bit**
- Fifth load instruction **misses**
	- **evict** LRU cache block: in this case, cache block with tag 000
	- dirty bit is set, so first write to memory
	- then read content of memory $M[10],M[11]$
	- set tag as 101
	- **set dirty bit to 0**
- **TLDR**: Write-back works best when we write to a particular address multiple times before evicting
###### Figure 3: Recap
![[Pasted image 20251118011725.png]]
- **Store With No Allocate**: Write to memory, don't *load* anything into the cache
	- **Hit**
		- **Write Back**: Just write to Cache; wait until eviction to write to memory
		- **Write Through**: *immediately* write to both cache and memory
	- **Miss**
		- **Write Back**: *just* write to memory; remember, we're doing **store with no allocate**
		- **Write Through**: *just* write to memory; remember, we're doing **store with no allocate**
- **Store With Allocate**: Write to memory, and in certain cases *load from memory into cache first*
	- **Hit**
		- **Write Back**: Write to cache, wait until eviction to write to memory with dirty bit
		- **Write Through**: *immediately* write to both cache and memory
	- **Miss**
		- **Write back**: Read from memory to cache, allocate to LRU block, *then* write to cache. Wait until eviction to write to memory with dirty bit
		- **Write Through**: Read from memory to cache, allocate to LRU bloc, *then* write to **both Cache and Memory, at the same time**

#### Tags
#computer_architecture
#ece552
#cache 