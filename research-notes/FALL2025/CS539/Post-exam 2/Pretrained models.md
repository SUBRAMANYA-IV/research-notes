#### Residual blocks
#### Figure 1: Residual block
![[Pasted image 20251205041842.png]]
- **regular block**
	- takes an input $x$ and transforms it, giving an output $f(x)$
	- the output may be **very** different from $x$, hence the network must "learn" the **entire transformation** from scratch
- **residual block**
	- a residual block tries to learn only the *difference* between an input and output: $f(x)=g(x)+x$
	- where $x$ is the input block, $g(x)$ is the transformation learned by weight layers. 
- suppose the "desired" function should be very close to the identity, i.e $f(x)=x$
- a normal block must learn $f(x)=x$, but a residual block only needs to know that $g(x)=0$
- in very deep networks, gradients tend to shrink as they pass backwards through many layers
- lower layers **stop learning**
- the network gets "stuck"
- note that for the gradient flow, when using a residual connection you get the following:

$$
f(x)=g(x)+x\to \frac{df(x)}{d(x)}=\frac{dg(x)}{d(x)}+1
$$
- the important part is the "+1" component
	- even if the gradient $\frac{dg}{dx}$ becomes tiny, the gradient **still** flows backward unchanged through the skip connection
