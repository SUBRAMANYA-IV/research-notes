#### Input Pre-processing 
###### Figure 1: distribution of data before and after pre-processing
![[Pasted image 20251205031427.png]]
- recall that in most models, normalizing data yields many advantages
	- zero-centering means ReLU activations happen more often, as neural nets assume that inputs are distributed around 0. 
		- reduces saturation of functions like tanh and sigmoid
		- speeds up convergence
	- keeps gradients stable (avoid dominance by large features)
	- makes the **loss surface well-conditioned, hence faster convergence**

#### Batch normalization
###### Figure 2: example of batch normalization layer in forward-pass network
![[Pasted image 20251205031829.png]]
- usually inserted after a fully connected or convolutional layer, and **before non-linearity** 
- standardize data range in *internal* layers
	- i.e, similar to data normalization in pre-processing, but applies the same logic *during* training
- accelerates convergence
- normalized vector can be given by
$$
\hat{x}^{k}=\frac{x^k-E[x^k]}{\sqrt{ var[x^k] }}
$$
- where $k$ is the *channel* or *dimension* of the input vector. 
- given the batch-normalization layer works with **batches**, the mean and variance for each channel is computed across every element **of the batch**
	- i.e, suppose that the samples being used are $32 \times 32 \times 3$ images, i.e $32 \times 32$ pixels in dimension with 3 channels (red, green, blue). 
	- **mean and variance are not calculated for each sample individually**
	- instead, calculated over the **entire batch and all spatial locations in that channel**
	- given a batch size of $B$, then each *channel* has a shape $B \times 32 \times 32$. 
	- for channel 1 (Red):
$$
\mu_{1}=\frac{1}{BHW}\sum^B_{b=1}\sum^{32}_{h=1}\sum^{32}_{w=1}x_{b,1,h,w}
$$
$$
\sigma_{1}^2=\frac{1}{BHW}\sum(x_{b,1,h,w}-\mu_{1})^2
$$

- so **each channel gets its own mean/variance**, but computed using **all pixels** of that channel across the **whole batch**

- However, after all this, normalization might "loose" **too much information**
- the output of the batch-normalization layer hence has one additional component, to introduce any **offsets** or **stretch (variance)**
$$
y^k=\gamma^k \hat{x}^k+ \beta^k
$$
- where $\gamma^k$ is a **learnable** scalar for channel $k$, which literally scales the data by some factor (multiplying each value in the channel-tensor)
- and where $\beta^k$ is a **learnable** shift parameter for channel $k$. 
	- if $\gamma=\sigma$ and $\beta=\mu$, batch normalization layer becomes an identity transformation (i.e, input tensor is same as output tensor)\
	- if $\gamma=1$ and $\beta=0$, batch normalization becomes pure normalization (output has a mean of 0 and a variance of 1)
- **NOTE**: at test time, batch normalization layer functions differently
	- the mean/standard deviation is **not computed** based on the batch; instead, a single fixed empirical mean of activation during training is used. 

#### Regularization: Dropout
- regularization technique for reducing over-fitting in neural networks
	- recall that introducing to many layers/neurons can lead to overfitting to the training data, and will loose its ability to generalize
- to prevent the notion of "too many neurons", during training, in each forward pass, randomly set some neurons to 0. probability of dropping is a hyperparameter, 0.5 is common. 
###### Figure 3: single neuron dropout example
![[Pasted image 20251205034336.png]]
- consider a single neuron; at test time, the output of the neuron is given by
$$
E\{a\}=w_{1}x+w_{2}y
$$
- assuming a dropout probability of 0.5, during training, the outputs expected value would be 
$$
E\{a\}=\frac{1}{4}(w_{1}x+w_{2}y)+\frac{1}{4}(w_{1}x+0y)+\frac{1}{4}(0x+0y)+\frac{1}{4}(0x+w_{2}y)=\frac{1}{2}(w_{1}x+w_{2}y)
$$
- simpler formula: **at test time, multiply by the dropout probability**
- implying that the **output at test time = expected output at training time**
- **dropout should only be used for fully connected layers**
#### Early stopping
- stop training the model when the accuracy on the **validation set** decreases, or train for a long time
- always keep track of the model snapshot that worked **best** on validation
###### Figure 4: early stopping and snapshots
![[Pasted image 20251205041525.png]]

