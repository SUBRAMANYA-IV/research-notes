#### Cache Miss Rate
- **Local Miss Rate**
	- percentage of accesses to *specific* cache that are missing, given by $M_{r}(L_{i})=\frac{M(L_{i})}{A(L_{i})}$
	- i.e, just the ratio of misses to accesses for a specific cache (L1,L2, etc)
- **Global Miss Rate**
	- Misses **per instruction** (e.g, 1 MPKI=1 miss per 1000 instructions)

#### Cache Performance
- **Average Memory Access Time (AMAT)**: average time it takes (in cycles) between when a processor *issues a request* (to the cache/memory hierarchy) for an address and when it is received by the processor. 
	- Recall that fetches must propogate through the memory hierarchy, hence depends on number of caches/levels 
	- e.g, L1 cache with access latency $t_{L_{1}}$ and **local miss rate** $m_{L_{1}}$
		- $AMAT=t_{L_{1}}+m_{L_{1}}*t_{mem}$
	- e.g, L1 cache+L2 cache
		- $AMAT=t_{L_{1}}+m_{L_{1}}(t_{L_{2}}+m_{L_{2}}*t_{mem})$
- yields a recursive function with number of caches/memory hierarchy. 
- 
#### Tags
#computer_architecture
#ece552
#cache 