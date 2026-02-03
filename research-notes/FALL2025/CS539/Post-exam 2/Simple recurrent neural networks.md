- An RNN is basically a **nonlinear**, learned **ARMA** model. 
- recall that an ARMA model (Auto-regressive, moving average) model is given by
$$
y_{t}=\sum^Q_{n=1}a_{n}y_{t-n}+\sum^P_{m=1}b_{m}e_{t-1}+e_{t}
$$
- where the AR component dictates how the current output is a function of previous outputs
- and where the MA component dictates how the current output is a function of past noise or shocks
- note that the entire ARMA model is **linear**: sum of products. 
-  simple RNN cell can be given by
$$
h_{t}=\tanh(W_{h}h_{t-1}+W_{x}x_{t})
$$
- which dictates that the current hidden state, $h_t$, is a **nonlinear** function of the previous state and a scalar weight ($W_{h}h_{t-1}$) and the weighted current input ($W_{x}x_{t}$)

#### RNN with hidden states
###### Figure 1: Simple RNN with hidden states
![[Pasted image 20251205061808.png]]
- Feed-forward network
	- $H=\phi(XW_{xh}+b_{h})$ with an input $X_{n \times d}$, weight $W_{xh}$, and bias $b_{h}$
	- $O=HW_{hq}+b_{q}$, where $O_{n \times q}$ is the output activation 
- Recurrent network
	- $H_{t}=\phi(XW_{xh}+H_{t-1}W_{hh}+b_{h}),O_{t}=H_{t}W_{hq}+b_{q}$
#### Character level language model using RNN
###### Figure 2: example of a RNN with characters
![[Pasted image 20251205063211.png]]
- note how the input sequence is an ordered set of features, specifically characters. 
- 