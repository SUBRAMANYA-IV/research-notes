- if our cache is getting a lot of misses, we must find out the *cause* of these misses. 
- **Cache misses happen for 3* reasons**
	- **Compulsory (cold) miss**
		- we've never accessed this data before, hence need to fetch it from memory, resulting in a miss
		- *if infinite-size cache, every miss is a cold miss*
	- **Capacity miss**
		- cache is not large enough to hold all the data
		- *if fully-associative finite cache, every miss that isn't a cold miss is a capacity miss*
	- **Conflict miss**
		- cache is large enough to hold data, but was replaced due to overly restrictive associativity
		- *else, if miss occurs in n-way cache, it is a conflict miss*
		- ie, empty spaces/blocks are available, but requested block from memory is **forced** to be assigned to a full set, resulting in (unnecessary) eviction, leading to a miss

#### Cache performance based on parameters
- how does changing parameters like the block size, cache size and associativity impact performance?

##### Block Size
- Block size is the number of words associated with an address tag
- **too small blocks**
	- doesn't exploit spatial locality well
	- have larger *tag* overhead 
- **too large blocks**
	- too few total number of blocks
	- useless data transferred between memory and cache
	- extra bandwidth, energy consumed
![[Pasted image 20251118072017.png]]
##### Cache size
- too large cache adversely affects hit and miss latency
- **too small a cache**
	- doesn't exploit temporal locality well 
		- i.e, results in frequent evictions, needs to repeatedly fetch from memory
![[Pasted image 20251118072233.png]]
- **working set**: the set of data application references within a time interval 

##### Associativity 
- How many blocks can map to the same index/set?
- **Larger Associativity**
	- lower miss rate, less variation among programs
	- diminishing returns
- **smaller associativity**
	- lower cost



#### Tags
#computer_architecture
#ece552
#cache 