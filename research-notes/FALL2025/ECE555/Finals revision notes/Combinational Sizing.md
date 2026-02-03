#### Logical Effort
- g: logical effort captures how complex is a gate compared to an inverter (always logical effort of 1)
- h: electrical effort, ratio if output to input capacitance
- stage effort: product of logical and electrical effort
- p: parasitic delay
- normalized delay of a gate is given by d=gh+p
![[Pasted image 20251215102625.png]]
![[Pasted image 20251215102706.png]]
- **NOTE**: parasitic delay is given as the sum of capacitances of all gates that **connect directly to the output net**
![[Pasted image 20251215102819.png]]
- for inverter, both PMOS and NMOS are the only gates driving the output, hence just them
- for NAND2, only 3 of the gates directly drive the output, hence the sum of these. 
- 