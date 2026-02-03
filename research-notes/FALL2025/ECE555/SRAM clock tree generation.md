- recall that a typical memory hierarchy is given by multiple levels of cache
- takes advantage of locality 
![[Pasted image 20251205144301.png]]

#### SRAM Design
- 6-transistor cell
	- based on the same "cross coupled inverter cell"; 2 inverters=4 transistors
	- 1 pass transistor to write
	- 1 pass transistor to read
 ![[Pasted image 20251205144632.png]]
 - **both write and read are differential**
	 - differential read makes it faster
	 - only need to develop around 50-100mV f difference between $BL$ and $BL_{n}$
 - 