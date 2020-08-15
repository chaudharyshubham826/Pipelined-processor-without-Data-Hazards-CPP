# Pipelined-processor-without-Data-Hazards-CPP

Assignment_9 README
Done by:              Shubham               2018CS10641
	             Deepanshu Singh           2018CS10892

⦁	Please make a "out.txt" file for the output of the program and "instructions.txt" for the input instructions in the same folder as this file. Also, the test cases are in same folder as this file.
⦁	Instructions should be of the form "add $t1, $t2, $t3" with no extra spaces.

		In this assignment, we have taken our work forward from previous assignment by adding "forwarding" when data hazards are detected, and thus improving pipeline performance. This program also implements instructions in five stages, namely "if, id, ex, mem and wb". There is no possibilty of structural hazard because we have separate instruction and data memories. But specific actions as taken if any data or control hazard is detected. As in previous assignments, the control hazards are taken care in same manner as done in Assignment 8, but forwarding is added for data hazards. Four registers are used for storing the values during the pipeline execution, implemented as struct in C++. Four registers are for IF/ID register, ID/EX register, EX/MEM register and MEM/WB register.
Instruction memory: Instructions are read from a input file "instructions.txt" and stored in the instruction memory. Instruction memory is of the type <vector<vector<string>>. For ex, "add $t1, $t2, $t3" would be stored as {"add", "$t1", "$t2", "t3"} on the instruction memory.
Data memory: Data memory is an array of integers.
Action on a Data hazard or Control hazard:  If any data hazard is detected, instead of stalling the pipeline, the data is forwarded to the execution stage and pipeline works normally without a stall. But, in the case of "load word data hazard"(when the instruction next to the lw instruction is dependent on the data written by lw instruction), pipeline must be stalled because the data required is only available after MEM stage, so pipelined is stalled for one cycle using the same implementation as done in Assignment 8, for stalling. After stall of one cycle, the forwarding unit comes in action and pipeline again works normally. Stalls are implemented as inserting "nop" instructions which do nothing(No operation). After the stall, the nop instruction from the instruction memory is removed as soon as the hazards are safe to allow further instructions to proceed normally.
Output: Output is written to the "out.txt" file. It prints the register and memory first. Then, during each cycle, the program print the instruction number which is in the stage1, 2, 3, 4 and 5, the register file contents and the data memory.

Comparison in performance in terms of clock cycles as well as IPC:
				The performance of the pipelined processor is better when forwarding was implemented for data hazards. It can be seen both from no. of clock cycles as well as the IPC, as shown below:
Case 1
Performance on a small test case when the processor is stalled on a data hazard:
 
Performance on a small test case on overcoming data hazard by forwading+stalling(1 stall in case of lw hazard):
 

Case 2
Performance on a large test case when the processor is stalled on a data hazard:
 
Performance on a small test case on overcoming data hazard by forwading+stalling(1 stall in case of lw hazard):
 

	
	Clearly, there is a significant improvement in both clock cycles consumed and IPC. This can make a day and night difference when normal day to day computations are done, i.e, when the test cases are very large!!!
