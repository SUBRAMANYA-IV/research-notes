2025-10-09 08:23
###### Abstract
- Obtained the complex dielectric function of amorphous $Ge_{1-x}Sn_{x}(0\leq x\leq_{0}.07)$ alloys using *spectroscopic* ellipsometry between 0.4 to 4.5 eV ($\text{3100 nm to 275 nm}$)
- uses a [[kramers-kronig]] consistent [[cody-lorentz]] dispersion model
- compositional dependence of band gap energy $E_{g}$ and parameters associated with the [[Lorentzian oscillator]] were determined. 
##### Conclusions
- Demonstrates compositional dependence of parameters 

$$
\begin{align}
&E_{g}: \text{Band gap energy*} \\
&E_{c}/E_{0}: \text{resonant frequency of the Lorentzian oscillator}  \\
&\Gamma: \text{parameter related to the broadening of the Lorentzian oscillator} \\
&A: \text{parameter related to the strength of the lorentzian oscillator}


\end{align} \\ \\

$$
- Complex dielectric response between Pure Germanium and Germanium-Tin alloy are incredibly similar, but with a consistent red-shift (ie, left shift when plotting against eV) as the Tin composition increases. 
- **phosphorous implantation had little to no effect on the complex-dielectric response of Germanium-Tin Alloy.**
- gives a linear relationship between Tin composition and $E_{c},E_{g}$
- also plots the relationship between strength parameter $A$ and eV, along with broadening parameter $\Gamma$ vs eV, but doesn't provide a fit/regression
	- Todo: attempt to use multiple regression models against the given data (linear, polynomial, exponential, etc), and determine which one yields the smallest error compared against current theoretical readings. 
###### Details
###### Notes
- paper utilizes a modified version of the [[tauc-lorentz]] model called the [[cody-lorentz]] model. 
- introduces additional features to model:
	- behavior/onset of the [[urbach tail]] ($E_{t}$)
	- onset of Lorentzian behavior of absorption with respect to $E_{g}$ ($E_{p}$)
- Below shows a comparison of the standard [[tauc-lorentz]] vs modified [[cody-lorentz]] models. 
- **paper uses exact same model of ellipsometer as we have: J. A Woolman V-Vase ellipsometer**
- Distinction between [[Solid Structures#Amorphous] |Amorphous]] and [[Solid Structures#Crystalline | crystalline]] semiconductors, and their behavior 
	- amorphous semiconductors lack critical peaks, and lead to a smoother, curved profile
	- crystalline semiconductors, due to their long-range crystalline order, have critical peaks often defined by $E_{0}, E_{1},E_{1}+\Delta_{1},E_{0}',E_{2}$
	- [[Solid Structures#Amorphous] |Amorphous]] semiconductors have a relaxation of the [[k-selection rule]]
	- 

###### Tauc-Lorentz Model

$$
\mathcal{I}(\chi^{TL}(E)=\begin{cases}
-\frac{1}{E}\frac{AE_{0}C(E-E_{g})^2}{(E^2-E_{0}^2)+C^2E^2}, \text{if } E>E_{g} \\ \\
0, E\leq E_{g}
\end{cases} \\
$$

###### Cody-Lorentz Model

$$
\epsilon_{2}(E)=\begin{cases} 
\frac{(E-E_{g})^2}{(E-E_{g})^2+E_{p}^2}*\frac{AE_{c}\Gamma E}{(E^2-E_{c}^2)^2+\Gamma ^2E^2};E>E_{t}\\ \\
\frac{E_{t}}{E}\left[ \frac{E-E_{g}^2}{(E-E_{g})^2+E_{p}^2} \right]\left[ \frac{AE_c\Gamma E}{(E^2-E_{c}^2)^2+\Gamma^2E^2} \right]e^{\frac{E-E_{t}}{E_{u}}};0<E\leq E_{t}


\end{cases}
$$
##### tags
#paper
#GeSn





