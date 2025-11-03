2025-10-30 09:23
## What
- graph type problem
![[Pasted image 20251030093055.png]]
- 2 special types of nodes: [[Source]] and [[Sink]]
	- all "flow" must be *sourced* from node S and must "end up" in *sink* t
	- flow function: $f: E\to R^+; f(e)$ is the flow *across* edge $e$
- **Flow Conditions**
	- each node has a capacity, or **maximum amount that can flow through it**
		- given by $e \in E, 0\leq f(e)\leq c_{e}$
		- ie, e is an edge, and $f(e)$ is the flow function. limits the flow through an **edge** to be between 0 and maximum $c_e$
	- conservation: for each vertex $v \in V /\{s,t\}$ (ie, not including source or sink)
		- $\sum_{\text{e into v}}f(e)=f^{in}(v)=f^{out}(v)=\sum_{e out of v}f(e)$
		- ie, 
###### tags
#compsci

