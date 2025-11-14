2025-11-04 09:31
## What
- **Edge Disjoint path**: given 2 paths $p_{1}$ and $p_{2}$, $p_{1} \cap p_{2}$ are [[Edge Disjoint Paths]] if 
$$
\forall e_{1} \in p_{1}, \forall e_{2}\in p_{2}, e_{1}\neq e_{2}
$$
- ie, path $p_{1}$ and $p_{2}$ share **no common edges**
- **BUT**, they are allowed to have common *vertices*
- **goal**: find the number of edge disjoint paths from nodes $s$ to $t$
## How

##### Case 1: Directed Graph
- Choose source and sink as the 2 nodes for the problem
- set the capacity of all nodes to 1
- perform max flow: **max flow represents number of edge disjoint paths**
##### Case 2: Undirected Graph 
- choose source and sink as 2 nodes for the problem
- for every edge on the graph, turn it into **2 directed edges**
- perform max flow function
- Case where 2 nodes "feed" into each other: detect cycle, set both to 0. 

##### Recovering the k edge-disjoint paths
- given the graph with know unit flows, we can simply extract the path by performing DFS on all edges with flow 1
- when encountering a cycle, set the cycles nodes to 0 and then call the DFS again on the end node. 


###### tags
#compsci 
#algorithm 
