2### Problem Statement
![[Pasted image 20251031152741.png]]
- Set of requests, $\sigma=\{r_{1},\dots,r_{n}\}$
- a request given by $r_{i}=\{s_{i},f_{i},v_{i}\}$, where
	- $s_i$ is the start time
	- $f_i$ is the end time
	- $v_i$ is the weight/value of the given task
- **Goal**: generate a compatible schedule $S$ that has the maximum value
- Compatible schedule is constrained by
$$
S\forall r_{i},r_{j} \in S, f_{i}\leq s_{j} \lor f_{j}\leq s_{i}
$$

#### Recursive Solution:
- assume $\sigma$ ordered by *finish* time, $f_{i}$. ascending. 
- find the optimal value in sorted $\sigma$ of first $j$ items:
	- find largest $i<j$ such that $f_i \leq f_j$
	- $OPT(j)=max(OPT(j-1),OPT(i)+v_{j})$
		- case 1: exclude job $j$, optimal *until* ordering $j-1$. 
		- case 2: include job $j$
			- cant overlap anything that ends *after* $s_j$
			- hence find the last compatible job $i<j$ with $f_i\leq s_{j}$
			- if $j$ is included, total value becomes $v_j+OPT(i)$ 

###### Proof of Optimality
- By Strong induction on $j$.
- **Base case**: $j=0$ or $j=1$. only 1 optimal solution. 
- **Inductive Step**
	- By inductive hypothesis, we have optimal solution for $j-1$ and optimal solution for $i$
		- recall $j-1$ is case for *not* choosing current job, and $i$ is the **last** compatible job *if* we chose current job j
	- 