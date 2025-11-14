- 2025-11-04 08:08
## What
- The residual graph $G_{f}$ represents the *current state* of the network given the **current flow** $f$
- it shows, at the current moment, **where** and **how much** additional flow can still be pushed through the network, **including undoing some flow**
## How
- for every pair of vertices $(u,v)$, we have
$$
r(u,v)_{forwad}=c(u,v)-f(u,v)
$$
$$
r(u,v)_{backward}=f(u,v)
$$
- allows you to encode the idea of "freeing" flow in one place, to allow flow to another. 
![[Pasted image 20251104084329.png]]
- in the following, it can be reasoned 
	- Before: A was sending l 8 units through D
	- Now: algorithm finds a better route, $A \to B \to T$
	- But $A$ cant **create** flow; only direct it
	- so "pull" 4 units back from D and push those 4 units into $B \to T$

## Forward Residual Flow
- 
###### tags

#compsci 