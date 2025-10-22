2025-10-16 09:42
## What
- Fourier transform f the lattice. 
	- The direct/real lattice is a periodic function in the physical space, such as the [[bravais lattice]]. 
	- the reciprocal lattice exists in the k-space, or [[Misc Theory#spatial frequency|spatial frequency]]. 
- Consider a basic plane wave given by 
$$
\Psi_{k}(r)=\Psi_{0}e^{\vec{k}\vec{r}}
$$
- with $\vec{k}$ being any arbitrary wave vector, and consider a [[bravais lattice]] which is the set of vectors 
$$
\vec{R}=m \vec{a_{1}}+n \vec{a_{2}}+o \vec{a_{3}}
$$
- with $m,n,o$ being arbitrary *integer* coefficients, and the vectors ${\vec{a_{i}}}$ being the *primitive translation vectors* of the [[bravais lattice]]

- the [[Reciprocal Lattice]] can be defined as the *set* of wave vectors $\vec{k}$ for which the corresponding plane waves $\Psi_{k}(\vec{r})$ which have the *periodicity* of the [[bravais lattice]] $\vec{R}$. 
	- Importantly, the plane wave has the same periodicity f the lattice if, when you shift the plane-wave by **any lattice vector** the wave "looks" the same, ie
$$
\Psi_{k}(\vec{r})=\Psi_{k}(\vec{r}+\vec{R})
$$
$$
\Psi_{0}e^{i \vec{k}\vec{r}}=\Psi_{0}e^{i \vec{k}(\vec{r}+\vec{R})}
$$
- this results in the condition that 
$$
e^{i \vec{k}\vec{R}}=1, \vec{k}\vec{R}=2\pi l, l\in \mathbb{Z}
$$

- so far this yields the definition, but doesn't yield the vectors/basis. 
- set of wave vectors "permissible" can be given, with some arbitrary basis $\vec{b_{i}}$

$$
\vec{k}=p \vec{b_{1}}+q \vec{b_{2}}+r \vec{b_{3}}
$$
- these parameters **must** satisfy the aforementioned requirement of having the *dot product* between $\vec{k}$ and $\vec{R}$ being $2\pi$ periodic, ie
$$
\begin{pmatrix}
p & q & r
\end{pmatrix}
\begin{bmatrix}
    \vec{b_{1}}\cdot\vec{a_{1}} & \vec{b_{1}}\cdot\vec{a_{2}}& \vec{b_{1}}\cdot\vec{a_{3}} \\
    \vec{b_{2}}\cdot\vec{a_{1}} & \vec{b_{2}}\cdot\vec{a_{2}}& \vec{b_{2}}\cdot\vec{a_{3}} \\
   \vec{b_{3}}\cdot\vec{a_{1}} & \vec{b_{3}}\cdot\vec{a_{2}}& \vec{b_{3}}\cdot\vec{a_{3}} \\
\end{bmatrix}
\begin{pmatrix}
m \\ 
n \\  
o 
\end{pmatrix}=2\pi l
$$
- any basis for ${\vec{b_{i}}}$ can be chosen, hence a set **orthogonal** to the [[bravais lattice]] basis would be simple, yielding
$$
\vec{b_{i}} \cdot \vec{a_{j}}=2\pi \delta_{ij}
$$
- dividing the result by $2\pi$, the matrix yields a unit matrix which can be written as 
$$
pm+qn+ro=l
$$
- $m,n,o$ are still arbitrary integers, hence combination must be solved for every possible value. 

- recalling that the chosen basis is orthogonal to the [[bravais lattice]] basis, we can set rules for the chosen basis such that 
$$
\vec{a_{1}}\cdot \vec{b_{2}}=\vec{a_{1}}\cdot\vec{b_{3}}=0
$$
$$
\vec{b_{1}}=c \cdot(\vec{a_{2}} \times \vec{a_{3}})
$$
- where $c$ is some constant that needs to be found.
- we can apply the relation $\vec{b_{1}} \cdot \vec{a_{1}}=2\pi$ to get
$$
c=\frac{2\pi}{\vec{a_{1}}\cdot(\vec{a_{2}}\times \vec{a_{3}})}
$$
$$
V:=\vec{a_{1}} \cdot(\vec{a_{2}}\times \vec{a_{3}})
$$
- notice how the denominator yields the **volume** of the parallelepiped spanned by the primitive translation vectors of the original [[bravais lattice]]. 
	- This value remains *invariant* under cyclic permutations of the indices. 
- this finally yields our basis vectors for the reciprocal lattice, which can be given by 
$$
\vec{b_{1}}=2\pi*\frac{\vec{a_{2}}\times \vec{a_{3}}}{V}
$$
- and for all cyclic permutations of above. 
## Why
##### Diffraction and Scattering
- given the set of reciprocal-lattice basis vectors $\{\vec{b_{i}}\}$, which yield the set of possible wave-vectors $\vec{k}$, constructive, scattering (x-ray, electron, etc) will result in constructive interference or peaks only when the change in wave vector
$$
\Delta \vec{k}=\vec{k'}-\vec{k}=G
$$
- equals a reciprocal lattice vector $G$. This satisfies the **Laue condition**, which is equivalently [[Bragg's law]]

##### Band Structure and Bloch's theorem
- When solving Schrodinger's equation in a periodic potential (ie, crystal lattice), the electron wave functions are [[Bloch waves]]
$$
\psi_{k}(\vec{r})=e^{i \vec{k} \cdot \vec{r}}u_{\vec{k}}(\vec{r})
$$
- where $u_{\vec{k}}(\vec{r})$ has the same *periodicity* as the lattice
- This leads to...
	- Energy Band Diagrams $E(\vec{k})$
	- [[Brillouin zone]]'s, which are defined directly from the reciprocal lattice. 
	- yields understanding of band gaps, effective masses and crystal momentum. 
## How

