 2025-10-30 09:47
## What
- [[greedy]] algorithm that computes the [[maximum flow]] in a [[flow network]]. 
## Why
## How
- key idea of algorithm: 
	- given there is a path from the source to the sink, with available capacity on all edges in the path, we send flow along one of the paths. then we find another path, and so on. a path with available capacity is called an [[augmenting path]]

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
