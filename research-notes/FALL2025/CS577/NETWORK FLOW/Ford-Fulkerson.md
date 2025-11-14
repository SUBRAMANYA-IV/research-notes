 2025-10-30 09:47
## What
- [[greedy]] algorithm that computes the [[maximum flow]] in a [[flow network]]. 
- maximum flow can be defined the maximum amount of *something* that can be moved from one node to another
	- usually, from the source node to the sink node
## Why
## How
- key idea of algorithm: 
	- given there is a path from the source to the sink, with available capacity on all edges in the path, we send flow along one of the paths. then we find another path, and so on. a path with available capacity is called an [[augmenting path]]
- Done by finding **augmenting paths**
- Augmenting paths are paths that...
	- path that are **non full** and **forward**
	- path that is **non empty** and **backward**
	- ie, any path that still has capacity for flow
- Uses [[Residual Graph]]'s to allow "undoing" of actions


###### General Algorithm 
- find an augmenting path
- compute the bottle neck capacity, ie the edge in the path with the smallest capacity
- augment each edge and total flow

###### Example 1
![[Pasted image 20251104051825.png]]
- **step 1**
	- choose a random path: for example, $S \to D \to T$
	- bottle neck capacity here is $A \to D$, with a max flow rate of 8
	- update each edge with this bottle neck
![[Pasted image 20251104052201.png]]
- **step 2**
	- choose another random path: in this case, $S \to C \to D \to T$
	- bottle neck capacity here is **2**, as edge $D \to T$ has a capacity for 2
	- update all other nodes in the path with this bottle neck
![[Pasted image 20251104052347.png]]
- **step 3**
	- specifically choose a node with a backward edge, ie $D \to A$. Even though the edge is *directed* from $D \to A$. 
	- in this path, bottle neck is given by $A \to B$ with a value of **4**
	- via residual graph, $r(D,A)=8$, implying that
	- increment edges $S \to C, C \to D, A \to B, B\to T$
	- **decrement** edge 
- **Step n-1**
	- Maximum flow is found when no more augmenting paths can be formed

###### Analyzing the algorithm
- **Observation 1**
	- If all capacities are integers, then all $f(e)$ (flow into an edge), residual capacities, and maximum flow rate $v(f)$ are integers at every iteration. 
- **Lemma 1**
	- $v(f')>v(f)$, where $v(f')=v(f)+BottleNeck(P,G_{f})$ for an augmenting path $P$ in $G_f$
	- **Proof**: By definition of $P$, first edge of $p$ is an out edge from $s$ that we *increase* by $BottleNeck(P,G_{f})=q$. By the law of conservation, this will give $q$ more flow. 
- **theorem 2**
	- Let $C=\sum_{\text{e out of s}}c_{e}$, the $FF$ method terminates in at most $C$ iterations
		- $C$ defines the sum of residual capacities of edges that go *out* of node s
	- Lemma 1 demonstrates that flow strictly increases at each iteration. Hence, the *residual capacity* out of node $s$ decreases by at least 1 at each iteration
- **theorem 3**
	- suppose all capacities are integers, then the FF method has a run time of $O(mC)$

###### Algorithm
- Let $G(V,E)$ be a graph, and for each *edge* from $u$ to $v$, let $c(u,v)$ be the capacity of said edge, and $f(u,v)$ be the actual flow. 
- **goal**: find the maximum flow from source $s$ to sink $t$. 
- After every step in the algorithm, the following properties are maintained. 

| Type                 | Expression                                                    | Explanation                                                                                                                                                                           |
| -------------------- | ------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Capacity Constraints | $\forall(u,v) \in E: f(u,v)\leq c(u,v)$                       | flow along any given edge in set of edges $E$ cannot exceed the capacity                                                                                                              |
| Skew Symmetry        | $\forall(u,v) \in E:f(u,v)=-f(v,u)$                           | net flow from $u$ to $v$ must be the opposite of the net flow from $v$ to $u$. Ie, conservation of flow                                                                               |
| Flow conservation    | $\forall u\in V:u\neq s \cap u\neq t, \sum_{w \in V}f(u,w)=0$ | the new flow to a node is 0, **except** for the source and sink nodes, $s,t$.                                                                                                         |
| Value(f)             | $\sum_{(s,u) \in E}f(s,u)=\sum_{(v,t)\in E}f(v,t)$            | for the *sum of flows with the source as a common node* and the *sum of flows with the drain as a common node*<br>ie, **flow leaving from s must be equal to the flow arriving at t** |


###### Tags
#algorithm
#compsci
