# Mixed Signal SoC design Marathon using eSim & SKY130
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
![ref_ckt](https://user-images.githubusercontent.com/88330171/194209930-82e07232-5b18-433f-8963-aee1c5e36fad.jpg)

## Reference Waveform
The waveform is simulated using EDA playground (https://www.edaplayground.com/)
![ref_wave](https://user-images.githubusercontent.com/88330171/194209938-b496d5ce-928c-48a9-9696-70dc3244f8db.png)

## Circuit Details
The MOD-10 synchronous counter has a count range of 0 to 9. Because the counter is synchronous, the clock signal is sent to all of the flip flops at the same time. The MOD-10 synchronous counter is built with both analogue and digital circuitry. The analogue circuitry consists of the astable multivibrator and the AND gate implemented in CMOS. The astable multivibrator is built by cascading three inverters and using a resistor and capacitor to generate a pulse signal for the clock. The inverters act as a buffer, and the direction of the capacitor's charging and discharging plays an important role in switching the inverter's inputs and outputs. The digital circuitry of MOD - 10 is made up of four JK flipflops with synchronous clear. The truth table is written and reduced using the K-map to obtain the boolean functions for the input and output to the flipflops. Using the Boolean function, the Verilog code for the digital circuit is written. Finally, the analog and digital circuits are integrated to form a mixed signal circuit.

## Truth Table
The truth table along with the excitation table for each flipflop is shown below:

| Present State | Next State |J3 | K3 | J2 | K2 | J1 | K1 | J0 | K0 |
| ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------ | 
| **q3 q2 q1 q0** | **Q3 Q2 Q1 Q0** | | | | | | | | |
| 0 0 0 0 | 0 0 0 1 |  0 | x | 0 | x | 0 | x | 1 | x |
| 0 0 0 1 | 0 0 1 0 |  0 | x | 0 | x | 1 | x | x | 1 |
| 0 0 1 0 | 0 0 1 1 |  0 | x | 0 | x | x | 0 | 1 | x |
| 0 0 1 1 | 0 1 0 0 |  0 | x | 1 | x | x | 1 | x | 1 |
| 0 1 0 0 | 0 1 0 1 |  0 | x | x | 0 | 0 | x | 1 | x |
| 0 1 0 1 | 0 1 1 0 |  0 | x | x | 0 | 1 | x | x | 1 |
| 0 1 1 0 | 0 1 1 1 |  0 | x | x | 0 | x | 0 | 1 | x |
| 0 1 1 1 | 1 0 0 0 |  1 | x | x | 1 | x | 1 | x | 1 |
| 1 0 0 0 | 1 0 0 1 |  x | 0 | 0 | x | 0 | x | 1 | x |
| 1 0 0 1 | 0 0 0 0 |  x | 1 | 0 | x | 0 | x | x | 1 |
| 1 0 1 0 | x x x x |  x | x | x | x | x | x | x | x |
| 1 0 1 1 | x x x x |  x | x | x | x | x | x | x | x |
| 1 1 0 0 | x x x x |  x | x | x | x | x | x | x | x |
| 1 1 0 1 | x x x x |  x | x | x | x | x | x | x | x |
| 1 1 1 0 | x x x x |  x | x | x | x | x | x | x | x |
| 1 1 1 1 | x x x x |  x | x | x | x | x | x | x | x |

J0 = K0 = 1 </br>

J1 = q3'q0  ;  K1 = q0 </br>

J2 = K2 = q0q1 </br>

J3 = q0q1q2  ;  K3 = q0 </br>

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
The following is the schematic in drawn in eSim:

**Power Supply**</br>
![pwr](https://user-images.githubusercontent.com/88330171/194203839-5ac37993-82b3-467f-a961-c55915a366cb.png)

**Astable Multivibrator Circuit**
![astable_multivibrator](https://user-images.githubusercontent.com/88330171/194203820-905691fb-ee55-44bd-af03-8cb9e864f110.png)

**Mixed Signal MOD-10 Synchronous Counter using JK Flipflop with Synchronous Clear** 

![MOD_10_Counter](https://user-images.githubusercontent.com/88330171/194207207-d79991c6-5b7d-4ee9-bd3d-20a79540cb37.png)

## Verilog Code
```
module jk_ff_sky130(j,k,clk,clr,q,qb);
	input clk,clr,j,k;
	output reg q;
	output qb;
	
	always @(posedge clk) begin
		if (~clr)
			q<=0;
		else begin
			case({j,k})
				2'b00 : q<=q;
				2'b01 : q<=0;
				2'b10 : q<=1;
				2'b11 : q<=~q;
			endcase
		end
	end
	assign qb = ~q;
endmodule


```


## Makerchip
```
\TLV_version 1d: tl-x.org
\SV
/* verilator lint_off UNUSED*/  /* verilator lint_off DECLFILENAME*/  /* verilator lint_off BLKSEQ*/  /* verilator lint_off WIDTH*/  /* verilator lint_off SELRANGE*/  /* verilator lint_off PINCONNECTEMPTY*/  /* verilator lint_off DEFPARAM*/  /* verilator lint_off IMPLICIT*/  /* verilator lint_off COMBDLY*/  /* verilator lint_off SYNCASYNCNET*/  /* verilator lint_off UNOPTFLAT */  /* verilator lint_off UNSIGNED*/  /* verilator lint_off CASEINCOMPLETE*/  /* verilator lint_off UNDRIVEN*/  /* verilator lint_off VARHIDDEN*/  /* verilator lint_off CASEX*/  /* verilator lint_off CASEOVERLAP*/  /* verilator lint_off PINMISSING*/    /* verilator lint_off BLKANDNBLK*/  /* verilator lint_off MULTIDRIVEN*/    /* verilator lint_off WIDTHCONCAT*/  /* verilator lint_off ASSIGNDLY*/  /* verilator lint_off MODDUP*/  /* verilator lint_off STMTDLY*/  /* verilator lint_off LITENDIAN*/  /* verilator lint_off INITIALDLY*/    

//Your Verilog/System Verilog Code Starts Here:
module jk_ff_sky130(j,k,clk,clr,q,qb);
	input clk,clr,j,k;
	output reg q;
	output qb;
	
	always @(posedge clk) begin
		if (~clr)
			q<=0;
		else begin
			case({j,k})
				2'b00 : q<=q;
				2'b01 : q<=0;
				2'b10 : q<=1;
				2'b11 : q<=~q;
			endcase
		end
	end
	assign qb = ~q;
endmodule



//Top Module Code Starts here:
	module top(input logic clk, input logic reset, input logic [31:0] cyc_cnt, output logic passed, output logic failed);
		logic  clr;//input
		logic  j;//input
		logic  k;//input
		logic  q;//output
		logic  qb;//output
//The $random() can be replaced if user wants to assign values
		assign clr = 1;
		assign j = $random();
		assign k = $random();
		jk_ff_sky130 jk_ff_sky130(.clk(clk), .clr(clr), .j(j), .k(k), .q(q), .qb(qb));
	
\TLV
//Add \TLV here if desired                                     
\SV
endmodule

```
## Makerchip Plots

**JK Flipflop Output**
![makerchip plot](https://user-images.githubusercontent.com/88330171/194207229-9dff4bce-01be-42b8-bd1a-a8a29998302d.png)

The plot here depicts the functionality of the positive edge triggered JK flipflop with synchronous clear for the inputs J = 1 and K = 1.


## Netlists
The following figures show the contents in the counter_jk_2.cir.out : 

![netlist_1](https://user-images.githubusercontent.com/88330171/194203821-86b8b6b9-7eb3-4bab-aab8-5f27deedf52c.png)</br>

![netlist_2](https://user-images.githubusercontent.com/88330171/194203826-79b94e11-d0e3-4eae-a166-4bbf140df64e.png)</br>

![netlist_3](https://user-images.githubusercontent.com/88330171/194203830-b852a7cd-acb3-48c8-9e50-8fed9f70f322.png)</br>


## NgSpice Plots
The following waveforms are the ngspice plots for the designed circuit :

**Clear Signal**
![Clear](https://user-images.githubusercontent.com/88330171/194203790-6e82ce67-1202-489e-a659-63502bcd9b68.png)
**Clock Signal**
![Clock](https://user-images.githubusercontent.com/88330171/194203796-50213481-34fe-473f-a712-0240bf60a490.png)
**Q0 Output**
![V0](https://user-images.githubusercontent.com/88330171/194203807-6f3ac675-b99d-447c-8597-1fd9fcf45c29.png)
**Q1 Output**
![V1](https://user-images.githubusercontent.com/88330171/194203811-6249d4cb-b238-4acc-89f3-1cb4de743a11.png)
**Q2 Output**
![V2](https://user-images.githubusercontent.com/88330171/194203816-00e7ffdb-318b-4244-b0ea-174159930ed0.png)
**Q3 Output**
![V3](https://user-images.githubusercontent.com/88330171/194203817-c58e6c1f-f3aa-403e-b111-c932141442c3.png)
**Combined Waveform** </br>
![ng_spice](https://user-images.githubusercontent.com/88330171/194203837-6d4b0ee1-72b1-4728-b616-96b97f78b0a8.png)

## Steps to run generate NgVeri Model
1. Open eSim
2. Run NgVeri-Makerchip to create a digital block 
3. Add top level verilog file in Makerchip Tab
4. Click on NgVeri tab and add dependency files
5. Click on Run Verilog to NgSpice Converter
6. Debug if any errors
7. Model created successfully

## Steps to run this project
1. Open a new terminal
2. Clone this project using the following command:</br>
```git clone https://github.com/KanishR1/MOD_10_Sync_Counter_Mixed_sig_SoC.git ```</br>
3. Change directory:</br>
```cd eSim_project_files/counter_jk_2 ```</br>
4. Run ngspice:</br>
```ngspice counter_jk_2.cir.out```</br>
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
1. Morris Mano & Michael D Ciletti, “Digital Design: With an Introduction to Verilog HDL, 5th Edition, Pearson Education, 2013
2. Neil H.E. Weste, David Money Harris ―CMOS VLSI Design: A Circuits and Systems Perspective.
3. https://skywater-pdk.readthedocs.io/en/main/
4. https://www.homemade-circuits.com/cmos-astable-bistable-monostable-circuits-explained/
5. https://www.youtube.com/watch?v=M8EqkE4G9IE&ab_channel=SimplyPut
6. https://github.com/Eyantra698Sumanto/Two-in-One-Low-power-XOR-XNOR-Gate.git

