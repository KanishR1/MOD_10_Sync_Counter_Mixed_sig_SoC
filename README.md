# Mixed Signal Circuit Design and Simulation Marathon
# MOD-10 Synchronous Counter
- [Abstract](#abstract)
- [Reference Circuit Diagram](#reference-circuit-diagram)
- [Reference Waveform](#reference-waveform)
- [Circuit Details](#circuit-details)
- [Truth Table](#truth-table)
- [Software Used](#software-used)
  * [eSim](#esim)
  * [NgSpice](#ngspice)
  * [Makerchip](#makerchip)
  * [Verilator](#verilator)
- [Circuit Diagram in eSim](#circuit-diagram-in-esim)
- [Verilog Code](#verilog-code)
- [Makerchip](#makerchip-1)
- [Makerchip Plots](#makerchip-plots)
- [Netlists](#netlists)
- [NgSpice Plots](#ngspice-plots)
- [Steps to run generate NgVeri Model](#steps-to-run-generate-ngveri-model)
- [Steps to run this project](#steps-to-run-this-project)
- [Acknowlegdements](#acknowlegdements)
- [References](#references)

<small><i><a href='http://ecotrust-canada.github.io/markdown-toc/'>Table of contents generated with markdown-toc</a></i></small>


## Abstract
The MOD-10 synchronous counter has numerous applications such as digital clock, frequency divider, D2A, and so on. MOD-10 counters are also referred to as Decade counters or BCD counters. In this project, I used a JK flipflop as a counter and an astable multivibrator to generate the clock signal.

## Reference Circuit Diagram
![image](https://user-images.githubusercontent.com/58599984/152688334-fa3ad04d-e142-4dd1-a0cf-00fd13ca2d9e.png)
## Reference Waveform
![image](https://user-images.githubusercontent.com/58599984/152688402-29877a15-deb3-4dee-9bcc-2313851182de.png)

## Circuit Details
The MOD-10 synchronous counter has a count range of 0 to 9. Because the counter is synchronous, the clock signal is sent to all of the flip flops at the same time. The MOD-10 synchronous counter is built with both analogue and digital circuitry. The analogue circuitry consists of the astable multivibrator and the AND gate implemented in CMOS. The astable multivibrator is built by cascading three inverters and using a resistor and capacitor to generate a pulse signal for the clock. The inverters act as a buffer, and the direction of the capacitor's charging and discharging plays an important role in switching the inverter's inputs and outputs. The digital circuitry of MOD - 10 is made up of four JK flipflops with synchronous clear. The truth table is written and reduced using the K-map to obtain the boolean functions for the input and output to the flipflops. Using the Boolean function, the Verilog code for the digital circuit is written. Finally, the analog and digital circuits are integrated to form a mixed signal circuit.

## Truth Table

| Present State | Next State |J0 | K0 | J1 | K1 | J2 | K2 | J3 | K3 |
| ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- |
| q3 q2 q1 q0 | Q3 Q2 Q1 Q0 | ||||||||||

## Software Used
### eSim
It is an Open Source EDA developed by FOSSEE, IIT Bombay. It is used for electronic circuit simulation. It is made by the combination of two software namely NgSpice and KiCAD.
</br>
For more details refer:
</br>
https://esim.fossee.in/home
### NgSpice
It is an Open Source Software for Spice Simulations. For more details refer:
</br>
http://ngspice.sourceforge.net/docs.html
### Makerchip
It is an Online Web Browser IDE for Verilog/System-verilog/TL-Verilog Simulation. Refer
</br> https://www.makerchip.com/
### Verilator
It is a tool which converts Verilog code to C++ objects. Refer:
https://www.veripool.org/verilator/

## Circuit Diagram in eSim
The following is the schematic in eSim:
![image](https://user-images.githubusercontent.com/58599984/156439856-079de481-b68d-4955-b9c9-6ff310c5de58.png)
## Verilog Code
![image](https://user-images.githubusercontent.com/58599984/156445908-1af8255c-d17c-4275-8e24-ee65c96af66a.png)
## Makerchip
```
\TLV_version 1d: tl-x.org
\SV
/* verilator lint_off UNUSED*/  /* verilator lint_off DECLFILENAME*/  /* verilator lint_off BLKSEQ*/  /* verilator lint_off WIDTH*/  /* verilator lint_off SELRANGE*/  /* verilator lint_off PINCONNECTEMPTY*/  /* verilator lint_off DEFPARAM*/  /* verilator lint_off IMPLICIT*/  /* verilator lint_off COMBDLY*/  /* verilator lint_off SYNCASYNCNET*/  /* verilator lint_off UNOPTFLAT */  /* verilator lint_off UNSIGNED*/  /* verilator lint_off CASEINCOMPLETE*/  /* verilator lint_off UNDRIVEN*/  /* verilator lint_off VARHIDDEN*/  /* verilator lint_off CASEX*/  /* verilator lint_off CASEOVERLAP*/  /* verilator lint_off PINMISSING*/    /* verilator lint_off BLKANDNBLK*/  /* verilator lint_off MULTIDRIVEN*/     /* verilator lint_off WIDTHCONCAT*/  /* verilator lint_off ASSIGNDLY*/  /* verilator lint_off MODDUP*/  /* verilator lint_off STMTDLY*/  /* verilator lint_off LITENDIAN*/  /* verilator lint_off INITIALDLY*/    

//Your Verilog/System Verilog Code Starts Here:
module ixorxnor(output yXOR,output yXNOR, input a,input b);
  


  assign yXOR = a ^ b;
  assign yXNOR = ~(a ^ b);
  
endmodule 

//Top Module Code Starts here:
	module top(input logic clk, input logic reset, input logic [31:0] cyc_cnt, output logic passed, output logic failed);
		logic  yXOR;//output
		logic  yXNOR;//output
		logic  a;//input
		logic  b;//input
//The $random() can be replaced if user wants to assign values
      always @(posedge clk) 
         begin
         a = $random();
		   b = $random();
            end
		ixorxnor ixorxnor(.yXOR(yXOR), .yXNOR(yXNOR), .a(a), .b(b));
	
\TLV
//Add \TLV here if desired                                     
\SV
endmodule

```
## Makerchip Plots
![image](https://user-images.githubusercontent.com/58599984/156443516-6fdc4420-0bab-40a8-84f4-515966e4f569.png)

## Netlists
![image](https://user-images.githubusercontent.com/58599984/156440985-0a983124-b5ad-4b60-b83f-7adf0e7c36fb.png)
## NgSpice Plots
![image](https://user-images.githubusercontent.com/58599984/156440036-188911e0-9bb2-4d9f-b53d-878f5792d1c6.png)
![image](https://user-images.githubusercontent.com/58599984/156440082-c3f319ef-3224-4595-85e9-38bae135350f.png)

![image](https://user-images.githubusercontent.com/58599984/156439624-353c14ac-4216-4aa7-8207-64f4c287b2b7.png)
![image](https://user-images.githubusercontent.com/58599984/156439590-9371c62f-384b-42f8-9403-9704429d752d.png)
## GAW Plots
![image](https://user-images.githubusercontent.com/58599984/156439535-edb78fc7-a6e6-4178-864a-7cea5ea37e23.png)
## Steps to run generate NgVeri Model
1. Open eSim
2. Run NgVeri-Makerchip 
3. Add top level verilog file in Makerchip Tab
4. Click on NgVeri tab
5. Add dependency files
6. Click on Run Verilog to NgSpice Converter
7. Debug if any errors
8. Model created successfully
## Steps to run this project
1. Open a new terminal
2. Clone this project using the following command:</br>
```git clone https://github.com/Eyantra698Sumanto/XOR-XNOR-Gate.git ```</br>
3. Change directory:</br>
```cd eSim_project_files/xor_xnor```</br>
4. Run ngspice:</br>
```ngspice xor_xnor.cir.out```</br>
5. To run the project in eSim:

  - Run eSim</br>
  - Load the project</br>
  - Open eeSchema</br>
## Acknowlegdements
1. FOSSEE, IIT Bombay
2. Steve Hoover, Founder, Redwood EDA
3. Kunal Ghosh, Co-founder, VSD Corp. Pvt. Ltd. - kunalpghosh@gmail.com
4. Sumanto Kar, eSim Team, FOSSEE

## References
1. Ahmad, Nabihah & Hasan, Rezaul. (2011). A new design of XOR-XNOR gates for low power application. 10.1109/ICEDSA.2011.5959039. 
2. K. Ravali, N. R. Vijay, S. Jaggavarapu and R. Sakthivel, "Low power XOR gate design and its applications," 2017 Fourth International Conference on Signal Processing, Communication and Networking (ICSCN), 2017, pp. 1-4, doi: 10.1109/ICSCN.2017.8085699.
3. https://github.com/Eyantra698Sumanto/Two-in-One-Low-power-XOR-XNOR-Gate.git

