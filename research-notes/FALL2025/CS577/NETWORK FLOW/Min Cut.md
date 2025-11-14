2025-11-12 08:01
## What
###### Recall Cuts
- A cut: partition of Vertices $V$ into sets $(A,B)$ with $s \in A$ and $t \in B$
- **cut capacity**: $c(A,B)=\sum_{\text{e out of A}}c_{e}$
	- ie, the capacity of flow from set $A$ to set $B$ is equal to the sum of capacities of edges that connect a given node from set $A$, $s$, to a given node in set $B$, $t$. 
## How
- ###### Lemma 4
	- Let $f$ be any $s-t$ flow, and $(A,B)$ be any $s-t$ cut. Then, $v(f)=f^{out}(A)-f^{in}(A)=f^{in}(B)-f^{out}(B)$
	- recall that $v(f)$ represents the total value of the flow (a scalar, integer)
	- just the flow exiting the source and entering the sink
- ###### Lemma 5
	- let $f$ be any $s-t$ cut. Then, $v(f)\leq c(A,B)$
		- Formally, $c(A,B)$ can defined as 
			$$c(A,B)=\sum_{{(u,v) \in E, u \in A, v \in B}}c(u,v)$$
		- ie, the capacity of flow between sets of nodes $A$ and $B$ is equal to the sum of capacities of edges between nodes $u \in A$ and $v \in B$. 
	- combines **Lemma 4** with the fact that **all flows must obey capacity constraints**, ie $f(u,v)\leq c(u,v)$
	- 
- ###### Theorem 6
	- if $f$ is an $s-t$ flow such that there is no $s-t$ path in graph $G_f$, then there is an $s-t$ cut $(A^*,B^*)$ in $G$ for which $v(f)=c(A^*,B^*)$
		- if the **augmented graph** $G_f$ doesn't have any path from $s \to t$. This implies that...
			- a) There is no **forward residual edge** for any possible path $s \to t$: i.e, all forward edges on every path are saturated; maximum capacity
			- b) There are no **backward residual edges** in a path to $t$: i.e, $f(u,v)=0$. Demonstrates that there's no way to reroute previously assigned flow to free up a better path
			- Overall, this implies that the current residual graph $G_f$ is at max-flow/max-capacity
		- if the residual graph $G_{f}$ is a max-flow graph, this means there exists a partition of nodes into sets $A^*,B^*$ such that the **capacity** between these two sets is equal to the max-flow of the graph.
- **Proof of theorem 6**
	- Let $A^*$ be the set of nodes for which $\exists(s-v)$ path in the residual graph $G_{f}$, and let $B^*=V\setminus A^*$ 
		- i.e, all nodes $v$ such that there exists a path from the source *to* node $v$ are included in the set $A^*$
		- as a result, $B^*$ would just be the set of nodes where there exists no path from the source to said node. 
	- consider an edge $e=(u,v)$: Claim $f(e)=c_e$
		- i.e, given nodes from set $A^*$ to $B^*$ that contain an edge, in this case $u$ and $v$ respectively, the flow between these two nodes should be *saturating*, or equal to the capacity of edge $e=(u,v)$
	- consider edge $e=(u',v')$: Claim $f(e)=0$
		- i.e, there is zero flow *from* set $B^*$ and set $A^*$
	- These two assumptions will satisfy the requirement that

$$
v(f)=f^{out}(A^*)-f^{in}(A^*)=\sum_{u \in A^*, v \in V^*}c(,v)
$$
- equates the *flow value* to the *cut capacity*
- 


###### tags

