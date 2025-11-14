### Flop Timing Specifications
- $t_{su}$: setup time
	- Minimum duration during which the data must be stable **before the clock edge**
- $t_{hold}$: Hold time
	- Minimum duration during which the data must be stable **after** the clock edge
- $clk 2 q$: clock to output delay
	- **propagation time** from the input to the output. 

- For Latches, all the previous values are determined with respect to **when we lose the opportunity to latch/measure a value**
- This occurs during the **falling edge** of a latch, hence, for a **latch**
	- Setup-time: time *before* a falling edge that the signal must be valid
	- Hold-time: time *after* a *falling* edge that the signal must be valid
	- **clk2q**: Time after a *rising* edge where the output of a flop, $Q$, represents the input. 
![[Pasted image 20251113192656.png]]
### Setup Time Requirement
![[Pasted image 20251113192907.png]]
- For the given diagram, at the rising edge, data must travel from $D1$ to $D2$ through the computational delay: are there any errors?
- At a rising clock edge, data at $D1$ **must** propagate through the first flops clk2q, must travel through computational delay, AND must arrive at $D2$ *before* the next rising edge, ie he period $T_{clk}$
$$
T_{clk}\geq t_{su}+clk2q+t_{comb}
$$
- in this example, $T_{clk}$ is **too fast**, implying that by the time data arrives at $D_2$, it violates the setup time... hence becoming a **setup time violation** 
- **Setup time violation**: frequency too high/clock too fast, data doesn't have time to be "stable" to meet setup time requirements for flops. 
### Hold time requirement
- at rising clock edge, first flop "throws" a signal, through combinational logic, to input of flop 2, $D2$. 
- normally, this "new" value arrives *after* the hold time of the second flop, so that there isn't any metastability
	- Note that if Flop 2 "read" the same value as what Flop 1 did (ie, "also" read D1), this would act as a direct wire from D1 to the output. Not intended behavior
![[Pasted image 20251113194539.png]]
- Some paths propogate the input/change faster, leading to changes in $D_{2}$ before the second flop can register it. 
- **next** sample must NOT reach $D_{2}$ *before* the hold time passes! (**Race condition**)
$$
t_{hold}\leq clk 2 q +t_{min}
$$
### Clock Skew
- the global clock (gclk) is distributed in a "balanced" tree
- However, due to *on die* variation and load mismatches, the clock tree develop a skew
	- if a clock branch is driving something with a high load or capacitance, leads to offsets/slew
##### Changes to Setup Time
![[Pasted image 20251113200309.png]]
- Clock signal to flop 2 arrives 1 nanosecond *later* than to flop 1
- In this case, leads to the following
$$
T_{clk}+t_{skew}\geq t_{su}+clk 2 q +t_{comb}
$$
- in this case, the clck skew gives us *more* time to work with, more slack
##### Changes to Hold time
![[Pasted image 20251113200511.png]]
- rising edge for *second flop* is "offset" by 1ns compared to first flop
- essentially "eats into" our hold-time period/slack, giving equation
$$
T_{hold}+t_{skew}\leq clk 2 q+t_{min}
$$
- in this case, hold time requirement is **violated**, hence circuit is not guaranteed to function correctly. 

### Negative Clock Skew
- What if the clock signal "moves" in the opposite direction?
- ie, second flop receives the clock signal *earlier* than the first flop
- relatively, leads to a **negative clock skew**
- Previous expressions remain the same, but the sign of $t_{skew}$ is now negative
- "eats" into setup time, leading to **setup time violation**
- gives more leeway in *hold time*, possibly resolving any **hold time violations**R