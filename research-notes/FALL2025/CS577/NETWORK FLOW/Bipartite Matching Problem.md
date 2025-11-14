2025-11-04 09:30
## What
- Given a Bipartite graph $G=(V=U \cup Y,E)$
- all edges go between set of nodes $X$ and $Y$
- matching: $M \subseteq E$ 
	- $M$ is a subset of edges from the graph
- **Goal**: find largest matching (cardinality)
	- i.e, set of *pairs* of nodes/edges such that every node is "paired" with at most 1 partner, AND no node can be "matched" twice. 
	- given edges $(x,y)$ and $(x',y')$, if these nodes are matching, then $x \neq x'$ and $y \neq y'$

## How
###### Convert Bipartite graph into flow Network
![[Pasted image 20251113155621.png]]
- Add a source $S$ and connect it to all nodes in set $X$
- add a sink $T$ and connect it to all nodes in set $Y$
- Capacity of all edges is 1
##### Theorem 10
- For a matching $M$, $|M|=k$ in $G \iff \exists f \text{ for } G'$ where $v(f)=k$, and the edges carrying the flow correspond to the edges of $M$
	- A bipartite Graph has a matching of size $k$ *if and only if* the corresponding flow network has a flow value of $k$, where the edges that carry said flow correspond exactly to the matched pairs. 
- ###### Proof
	- if $|M|=k$, construct $f$ based on $(u,v) \in M$
		- $f(s,u)=1$: total flow from source to nodes in set $U$ must equal $k$.
		- $f(u,v)=1$: total flow between nodes $u,v$ must be 1, and total to $k$
		- $f(v,t)$=1: flow from a node in set $Y$ to the sink $T$ must be equal to 1, and sum to a total of $k$


###### tags

