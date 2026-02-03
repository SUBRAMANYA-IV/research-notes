- *predict* branch outcome (T or N) in the **IF** stage
- assume branches resolve in **ID** stage
##### Figure 1-2: Taken-prediction
![[Pasted image 20251118091143.png]]
- the beq instruction *predicts* that it will be taken, hence in the next cycle, loads target instruction in
- successfully taken!
![[Pasted image 20251118091246.png]]
- predict **not** taken in IF stage of first instruction
- assumes not taken, so loads instruction ADD into IF stage
- but at the same time, branch is resolved in ID stage for beq; realize we *should* have taken the branch. Flush incorrect prediction
- load correct instruction

#### Branch History Table
