- a time series is a sequence of feature vectors indexed at **time** $t$, e.g $\{x_{1},x_{2},\dots x_{T}\},x_{t} \in R^d,t \in Z^+$
- **Goal**: predict output (target) $\{y_{1},y_{2}\dots y_{T}\}$
	- prediction: $y_{t}=f(x_{s};s<t)$; i.e **causal**
		- the prediction of time $t$ can **only** be a function of all inputs **up to** time $t$; cant "look into" the future. 
	- Filtering/smoothing: $y_{t}=f(x_{s}:|s-t|<T_{0})$, **Not causal**
		- i.e, the prediction at time $t$, $y_t$ can be a function of all features $x_{s}$, such that the time index $s$ is within a **window** of $T_0$ around the target time $t$
		- examples include rolling-window variance or noise reduction algorithms
- Mathematical model: random processes. Data arriving at different time instances are **not** statistically independent!
$$
\{x_{t};0<t<T\}\to\{y_{t};0<t<T\}
$$
#### Time series model pre-processing

#### Tradition time series models

###### Autoregressive model (AR)
$$
y_{t}=c+\sum^Q_{n=1}a_{n}y_{t-n}+e_{t}
$$
- model order of $Q$: i.e, looks $Q$ time-samples into the past for current prediction
- $e_{t}$ represents white noise, such that $E\{e_{t}\}=0$ and that...
	- $E\{e_{t}e_{s}|t=s\}=\sigma^2$ : the expected value of noise at the same time is equal to the variance
	- $E\{e_{t}e_{s}|t \neq s\}=0$: statistically independent 
- **NOTE**: the output at time-index $t$ is a function of **PREVIOUS OUTPUTS**

###### Moving Average model (MA)
$$
x_{t}=d+\sum^P_{m=1}b_{m}e_{t-m}+e_{t}
$$
- the output at time $t$ is a function of some constant offset $d$, along with a window of previous-time values $t-P$. 
- $e_{t-m}$ represents the white noise measured at previous time indices.
- $b_m$ are coefficients that specify how *previous* noise shocks influence the current value
- $e_t$ is simply the current white noise
- Moving Average model essentially propagates noise through time, incorporating the idea that noise at previous time indices influence the current output value. 
#### ARMA (Auto-regressive, moving average model)
$$
y_{t}=c+\sum^Q_{n=1}a_{n}y_{t-n}+e_{t}+\sum^P_{m=1}b_{m}e_{t-m}
$$
- model that incorporates both the auto regressive AM model **and** the moving average MA model. 
#### Linear regression for AR model
- 1-step prediction: predicting $x_{t}$ based on $\{x_{t-1},x_{t-2}\dots x_{t-P}\}$
$$
\hat{x}_{t}=\sum^P_{i=1}a_{i}x_{t-i}
$$
- the predicted value $\hat{x}_{t}$ can be modeled as a weighted sum of previous outputs
- want to choose the vector $\vec{a}$ such that the error between actual value at time $t$, $x_{t}$ and predicted $\hat{x}_{t}$ is minimized, i.e
$$
min_{\{a_{i};1<i<P\}}||x_{t}-\sum^P_{i=1}a_{i}x_{t-i}||^2
$$

#### Latent AR model
- using a latent variable (state variable) to summarize all the previous inputs
- current state is a function of previous state **and** current input
- current output is a function of current state
###### Figure 1: Latent AR model
![[Pasted image 20251205052549.png]]
- use latent states $h$ to summarize all previous inputs

#### Forecasting mode and data partitioning 
- time series is an **ordered data type**: the positions *in* the sequence is as important as the content at each index. 
- **Data partitioning**
	- training and validation data must *precede* the testing data 
- **Forecasting mode**
	- one step prediction: predict $y(t+1)$ based on observations up to time $t$
	- further time predictions can just recursively use 1-step predictions. Of course, the prediction error will propagate/accumulate in this case. 



