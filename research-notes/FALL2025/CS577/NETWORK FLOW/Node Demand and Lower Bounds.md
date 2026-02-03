### Node Demands
- each node has  demand $d_{v}$:
	- if $d_{v}<0$: a source that *requires* that $f^{in}(v)-f^{out}(v)=d_{v}$; the node **must** be "providing" a net out-flow of flow
	- if $d_{v}=0$: an internal node such that $f^{in}(v)-f^{out}(v)=0$
	- if $d_{v}>0$: a sink that *demands* $f^{out}(v)-f^{in}(v)=d_{v}$
- $S$ is the set of sources
- $T$ is the set of sinks

- **goal**: Feasibility: does there exist a flow that satisfies the conditions

###### Lemma 10
- if there **is** a feasible flow, then $\sum_{v \in V}d_{v}=0$
- **proof**:
	- Suppose that $f$ is a valid flow, then, by definition for all $v$, $d_v=f^{in}(v)-f^{out}(v)$.
		- for all vertices, their respective node-demands are satisfied by the flow-in and flow-out of the node
	- for every edge $e=(u,v), f^{out}_{e}(u)=f^{in}_{e}(v)$
		- i.e, the net flow out of node $u$ *through* edge $e$ is equal to the new flow *into* node *v* through edge *e*.
	- hence, this implies that $f^{out}_{e}(u)-f^{in}_{e}(v)=0$
	- Proves Lemma 10