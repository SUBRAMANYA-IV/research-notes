## What
- model that describes the complex permittivity of a material given several parameters
- solves the short-comings of the [[forouhi-bloomer]] model

## Why
- solves the short coming of other models such as the [[forouhi-bloomer]] and [[brendel-bormann]]
	- [[forouhi-bloomer]]: Incorrect asymptotic behavior, can lead to non-zero extinction coefficients at regions below the bandgap
	- non-[[hermitian]] behavior
## How
- Has parameters:
$$
\epsilon=\text{relative permittivity}\newline
$$
$$
E=\text{photon energy (eV)}
$$
$$
\epsilon_{\infty}=\text{value of relative permittivity at infinite energy (limit)}
$$
$$
\chi^{tl}=\text{a value related to the electric susceptibility of the material}
$$
- Overall equation is given by
$$
\epsilon(E)=\epsilon_{\infty}+\chi^{TL}(E)
$$
- describes the imaginary permittivity, and uses a [[kramers-kronig]] transformation to map it to the real-space
- Fitting parameters are given as 
$$
A: \text{fitting parameter related to the strength of the lorentzian oscillator}
$$
$$
C: \text{fitting parameter related to the broadening of the lorentzian oscillator}
$$
$$
E_{0}: \text{fitting parameter related to the resonant frequency of the lorentzian oscillator}
$$
$$
E_{g}: \text{fitting parameter related to the bandgap of the material}
$$
- equation can be given as 
$$
\mathcal{I}(\chi^{TL}(E)=\begin{cases}
-\frac{1}{E}\frac{AE_{0}C(E-E_{g})^2}{(E^2-E_{0}^2)+C^2E^2}, \text{if } E<E_{g} \\ \\
0, \text{otherwise}
\end{cases} \\
$$
 $$
 \mathcal{R}( \chi^{XT}(E))=\frac{2}{\pi}\int_{E_{g}}^\infty \frac{\xi\mathcal{I}(\chi^{TL}(\xi))}{\xi^2-E^2}d\xi
 $$
- [[kramers-kronig]] transform can be referenced on the Wikipedia page
![[Pasted image 20251005223804.png]]

###### Tags
- #models
- #math 
- #physics 
