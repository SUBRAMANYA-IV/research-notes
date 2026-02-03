- applying back propagation in RNN is called back propagation through time
- requires to expand (or unroll) the computational graph of an RNN one time step at a time
- the same parameters are *repeated* through the unrolled network
- hence, the gradient with respect to each parameter must be summed across all places that the parameter occurs in the unrolled net
###### Figure 1: Example of BPTT
![[Pasted image 20251205063811.png]]
- recall that in an RNN, the current hidden state is a function of both the *previous* hidden state, as well as the current input/weight. 
- the $D$ block is a delay operator, which simply stores and passes on the previous hidden state.
- the top figure is the compact representation, while the bottom is the **unrolled** representation
- the output of timestep $t$, $O_{t}$, is the current state passed through an **activation function**, i.e $O_{t}=g(h_{t})$ 
- the output at time step $t-1$ is given by $O_{t-1}$, which again is a function of the current time steps hidden state, $h_{t-1}$
#### BPTT equations 
###### Figure 2: Equations
![[Pasted image 20251205070700.png]]
- **Equation 1**
	- the loss $L$ with respect to the current time-steps output $o_{t}$ is simply the derivative of the original loss function, given by 
	$$
	L=\frac{1}{T}\sum^T_{t=1}l(o_{t},y_{t})
	$$
- **Equation 2**
	- recall that the output at time step $t$ is given by $o_{t}=W_{qh}h_{t}$
	- so the derivative with respect to the weight $W_{qh}$ is simply $h_{t}$
	- essentially saying that the loss with respect to the **final weight** is the product of losses through all time steps, *propogate*
	- $\frac{DL}{dO_{t}}$ was previously given to be the loss with respect to *just* the output, and $\frac{do_{t}}{dW_{qh}}$ is the change in output at time step $t$ with respect to the output weight $W_{qh}$. multiplying these two yields the sum-equation, which just says that the loss with respect to output weight is equal to the sum of losses with respect to the outputs over **all** time steps, multiplied by the hidden state
- **Equation 3**
	- The loss with respect to the hidden state at the **final time step** $T$ is given as the product of the final weight and the loss with respect to the output at the final time. 
- **Equation 4**
	- the loss with respect to a hidden state $h_{t}$ at **any** given time step $t$ 
