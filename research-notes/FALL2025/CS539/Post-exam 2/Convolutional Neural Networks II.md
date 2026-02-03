#### 2D convolution:
- given an image $A=M \times N$ image, and a filter kernel of dimensions $F \times F$, such that the filters dimensions follows $F<min\{M,N\}$
- Let the output of the convolution of $A$ and $C$ be a matrix $C$, then for $1<i<M-F+1$, $1<j<N-F+1$
##### Figure 1: convolution equation 
![[Pasted image 20251203191035.png]]
- if the image is padded such that $P=\frac{F-1}{2}$ zeros around the matrix $A$, then the convoluted image is equal to the original image, i.e $A=C$
- **NOTE**: though this is referred to as convolution, in engineering this is actually **cross correlation** 
	- recall from ECE 330 that you "flip" the convolution matrix in the time-domain and *then* "slide" it across, to maintain temporal consistency 

#### Padding
- allows us to use convolution layer without shrinking the height and width of the volumes
- important, as repeated convolution would lead to the image shrinking deeper into the network, eventually dissapearing or losing all its important information.
- helps keep information at the **border** of the image. Without padding, few values at the next layer would be affected by pixels at the **edges** of an image. 
- **Padding terms**
	- **valid** padding: no padding
	- **same** padding: padding so that the output dimension is the same as the input dimension. 

#### Transpose Convolution
- **Normal Convolution**
	- takes a large input, produces a smaller output 
	- e.g, $3 \times 3$ input, $2 \times 2$ convolution kernel, yields an output of $2 \times 2$
- **Transpose Convolution**
	- does the *reverse* spatial effect
	- takes a small input, produces a **larger** output. 
- in conventional convolution, a kernel is "slid over" the entire input image, setting that "location" in the output tensor as the sum-of-products of the weights of the kernel and values of the image
- in transpose convolution, each weight of the *kernel* is multiplied by the value of the pixel. 
- **adds** or **accumulates** that result in a specific location in the output tensor
#### Figure 2: Equation for transpose convolution
![[Pasted image 20251204151212.png]]
- Given an input matrix $X$ of dimension $H \times W$, and a transpose-convolution kernel $W$ of dimension $F \times F$, the output tensor is of dimension $(H+F-1) \times (W+F-1)$. 
- element-wise, for the $(i,j)$ index of input $X$, the output will be modified such that
$$
y_{i:i+F,j:j+F}=y_{i:i+F,j:j+F}+X_{i,j} \cdot W
$$
- i.e, the values of y between indices $[i,i+F]$ (dimension of the transpose convolution kernel), and similarly $[j,j+F]$ are modified by adding the kernel scalar-multiplied by the value of the image at location $i,j$
- **transpose convolution with stride**
#### Figure 3: example and equation for transpose
![[Pasted image 20251204152137.png]]
#### Transpose Convolution + Stride + Padding
- in the context of transpose convolution, padding $P$ in refers to deleting $P$ columns and rows from each side of the *output* activation matrix. 
- Overall, the generalized equation can be given as
$$
(S \cdot(H-1)+F-2P)\times(S \cdot(W-1)+F-2P)
$$
