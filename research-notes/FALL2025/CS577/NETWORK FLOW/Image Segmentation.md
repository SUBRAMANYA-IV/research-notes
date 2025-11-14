2025-11-04 10:00
## What
- Goal is to Separate the foreground to the background of a given image
![[Pasted image 20251104100109.png]]
- Let $P$ be a set of pixels in an image. We want to separate $P$ into set $A$ and $B$, where $A$ is the set of foreground pixels and $B$ is the set of background pixels. 
- for pixel $i$:
	- $a_i>0$ is the like hood of $i$ being in the foreground
	- $b_{i}>0$ is the like hood of $i$ being in the background
- for each adjacent pixel $j$: $p_{ij}=p_{ji}$ is a separation penalty paid when $i$ and $j$ are not **BOTH** in $A$ or $B$
## How
- Maximize the function
$$
q(A,B)=\sum_{i \in A} a_{i}+\sum_{j \in B}b_{j}-\sum_{i,j \in P:|A \cup\{i,j\}|=1}p_{ij}
$$

###### tags
#compsci 
#algorithm 
