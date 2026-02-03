#### Single filter, multiple channels
- most images are given in 3 dimensions; height, width and *channels*
	- recall that channels convey various information about the image. most often, its the Red-Green-Blue channels, but can take the form of any kind of "different" information
- When an input has more than one channel, the filter should have a **matching** number of channels. 
- Note that for a convolution kernel with multiple channels, each channel is *specific* to the input channel: dont confuse for the idea of "3d convolution". 
- Output of a multi-channel kernel is given by the convolution of each kernel's channel with the input-tensors corresponding channel, **then** summing across the values. 
###### Figure 1: Example of multi-channel convolution
![[Pasted image 20251204155211.png]]
#### Multiple filters, multiple channels
- each filter can be used to extract specific information or features from an input tensor; i.e, vertical edges, horizontal edges, gradients, colors, etc. 
###### Figure 2: Example of multi-channel, multi-filter convolution
![[Pasted image 20251204155958.png]]
- number of filters dictates the number of output channels that will be present
- note the number of multiplications that occur given the above example
	- each filter has 3 channels, each of dimension $3 \times 3$
	- 2 of such filters
	- used as kernels in the convolution of an input tensor of dimension $6 \times 6 \times 3$
	- note how the *output dimension*, i.e $4 \times 4$, is the same as the number of convolutions perform (i.e,output of filter 1's convolution with input tensor is the result of $4 \times 4$ convolution steps)
	- results in $(4 \times 4 \times 2) \times(3 imes 3 \times 3)=864$ multiplications. 

#### $1 \times 1$ Convolution
###### Figure 3: Example of $1 \times 1$ convolution kernels
![[Pasted image 20251205025417.png]]
- $1 \times 1$ convolution kernels can be used to "merge" together channels of the input layer
- recall that each filter applied to the input tensor gives a single channel as the output
- hence in the aforementioned example, an input tensor of dimension $6 \times 5 \times 5$ which has a $1 \times 1 \times 5$ kernel gives an output shape of $6 \times 6 \times 1$, and given 2 of these filters are applied, the output tensor is of dimension $6 \times 6 \times 2$. 

#### Adding non-Linear activation
- like most layers, a non-linear element is introduced via ReLU or Tanh activation. 
###### Figure 4: Convolution layer with activation function.
![[Pasted image 20251205025845.png]]
- activation functions don't modify the dimensions of the post-convolution tensor, instead modifying each element in accordance with the activation function **and** adding an offset. Note that the *same* bias is applied to all elements of a given layer, hence $b=[b_{1},b_{2}]$, and broadcasting it results in $Y[:,:,0]+=b_{1},Y[:,:,1]+=b_{2}$

#### Short hand notation for convolutional layers
###### Figure 5: example of notation
![[Pasted image 20251205030355.png]]
- convolution kernel of dimension $3 \times 3 \times 3$, with stride of $1$, and no padding. given there are 2 filters, the output dimension should be $(6-3+1) \times (6-3+1) \times (2)$

#### Pooling layer
- used to reduce the size of the representations and to sped up calculations
- also forces the model to focus on the "strongest" features/aspects of a tensor, ignoring weaker components
###### Figure 6: pooling examples
![[Pasted image 20251205030612.png]]
- max pooling simply takes the "maximum" value as the max-pooling kernel is slid over the input tensor. 
	- in the example above, an $4 \times 4$ input tensor is transformed into a $2 \times 2$ tensor, with the kernel of being of size $2 \times 2$. this implies a stride of $2$. 
- Average pooling takes the average value as the average-pooling kernel is slid over the input tensor. 
###### Figure 6: pooling over multiple channels
![[Pasted image 20251205030849.png]]
- pooling is applied independently across all channels, hence input/input channel shape does not change. 
- Pooling only has hyerparameters of size (f) and stride (s) and type (max or avg), but otherwise **does not have weights to learn**
- 