**SIMULATION AND IMPLEMENTATION OF SEQUENTIAL LOGIC CIRCUITS**

AIM : To simulate and synthesis SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using Vivado 2023.2.

APPARATUS REQUIRED : Vivado™ ML 2023.2

PROCEDURE:

1.Open Vivado: Launch Xilinx Vivado software on your computer.

2.Create a New Project: Click on "Create Project" from the welcome page or navigate through "File" > "Project" > "New".

3.Project Settings: Follow the prompts to set up your project. Specify the project name, location, and select RTL project type.

4.Add Design Files: Add your Verilog design files to the project. You can do this by right-clicking on "Design Sources" in the Sources window, then selecting "Add Sources". Choose your Verilog files from the file browser.

5.Specify Simulation Settings: Go to "Simulation" > "Simulation Settings". Choose your simulation language (Verilog in this case) and simulation tool (Vivado Simulator).

6.Run Simulation: Go to "Flow" > "Run Simulation" > "Run Behavioral Simulation". This will launch the Vivado Simulator and compile your design for simulation.

7.Set Simulation Time: In the Vivado Simulator window, set the simulation time if it's not set automatically. This determines how long the simulation will run.

8.Run Simulation: Start the simulation by clicking on the "Run" button in the simulation window.

9.View Results: After the simulation completes, you can view waveforms, debug signals, and analyze the behavior of your design.


**LOGIC DIAGRAM**

SR FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/77fb7f38-5649-4778-a987-8468df9ea3c3)


JK FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/1510e030-4ddc-42b1-88ce-d00f6f0dc7e6)

T FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/7a020379-efb1-4104-85ee-439d660baa08)


D FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/dda843c5-f0a0-4b51-93a2-eaa4b7fa8aa0)


COUNTER

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/a1fc5f68-aafb-49a1-93d2-779529f525fa)

EXPERIMENTS :

#1

D FLIP FLOP :-

Code:
```
module dff(d,clk,rst,q);
input d,clk,rst;
output reg q;
always @(posedge clk)
begin
if (rst==1)
q=1'b0;
else
q=d;
end
endmodule
```
OUTPUT:-

Simulation :

![image](https://github.com/Hariharan177/VLSI-LAB-EXP-4/assets/164841000/25a7bfd6-a8ec-4641-a33b-871d7d2c84e1)

Elaborated Design :

![image](https://github.com/Hariharan177/VLSI-LAB-EXP-4/assets/164841000/57477f37-bb46-48b1-8586-abd01afabe9f)

#2

JK FLIP FLOP:-

Code:
```
module JK_flipflop (q, q_bar, j,k, clk, reset);
  input j,k,clk, reset;
  output reg q;
  output q_bar;
  always@(posedge clk) begin
    if(!reset)        q <= 0;
    else 
  begin
      case({j,k})
        2'b00: q <= q;  
        2'b01: q <= 1'b0; 
        2'b10: q <= 1'b1;
        2'b11: q <= ~q; 
      endcase
    end
  end
  assign q_bar = ~q;
endmodule
```
OUTPUT:-

Simulation Output:

![image](https://github.com/Hariharan177/VLSI-LAB-EXP-4/assets/164841000/85c592fe-8829-42e5-8db6-f36749cd1af9)

Elaborated Design:

![image](https://github.com/Hariharan177/VLSI-LAB-EXP-4/assets/164841000/6292539f-8dad-4576-89d5-a99adbf985ab)

#3

MOD 10 COUNTER :-

Code :
```
module counter(
input clk,rst,enable,
output reg [3:0]counter_output
);
always@ (posedge clk)
begin 
if( rst | counter_output==4'b1001)
counter_output <= 4'b0000;
else if(enable)
counter_output <= counter_output + 1;
else
counter_output <= 0;
end
endmodule
```
OUTPUT:-

Simulation :

![image](https://github.com/Hariharan177/VLSI-LAB-EXP-4/assets/164841000/078b2f9b-20fc-4291-89f6-41411c5a2966)

Elaborated Design :

![image](https://github.com/Hariharan177/VLSI-LAB-EXP-4/assets/164841000/07f7abcd-8e48-4c1d-a172-19d30bcf74af)

#4

Ripple Counter:-

Code :
```
module D_FF(q, d, clk, reset);
output q;
input d, clk, reset;
reg q;
always @(posedge reset or negedge clk)
if (reset)
q = 1'b0;
else
q = d;
endmodule
module T_FF(q, clk, reset);
output q;
input clk, reset;
wire d;
D_FF dff0(q, d, clk, reset);
not n1(d, q); 
endmodule
module ripple_carry_counter(q, clk, reset);
output [3:0] q;
input clk, reset;
T_FF tffo(q[0], clk, reset);
T_FF tff1(q[1], q[0], reset);
T_FF tff2(q[2], q[1], reset);
T_FF tff3(q[3], q[2], reset);
endmodule
```
OUTPUT:-

Simulation:

![image](https://github.com/Hariharan177/VLSI-LAB-EXP-4/assets/164841000/c7480be3-e7bf-4d46-bd07-56c30f281fb9)

Elaborated Design :

![image](https://github.com/Hariharan177/VLSI-LAB-EXP-4/assets/164841000/5c7965c8-cfa3-4f75-be35-9bbdc7656f78)

#5

SR FLIPFLOP :-

Code :
```
module SR_flipflop (q, q_bar, s,r, clk, reset);
  input s,r,clk, reset;
  output reg q;
  output q_bar;
  always@(posedge clk) begin 
    if(!reset)�        q <= 0;
    else 
  begin
      case({s,r})
        2'b00: q <= q;    
        2'b01: q <= 1'b0; 
        2'b10: q <= 1'b1; 
        2'b11: q <= 1'bx; 
      endcase
    end
  end
  assign q_bar = ~q;
endmodule
```
OUTPUT:-

Simulation :

![image](https://github.com/Hariharan177/VLSI-LAB-EXP-4/assets/164841000/e25f7008-3727-4af0-9185-7631cf9ceead)

Elaborated Design :

![image](https://github.com/Hariharan177/VLSI-LAB-EXP-4/assets/164841000/797dfabd-cfae-4f60-a3ac-ceef832777d4)

#6

T FLIP FLOP :-

Code :
```
module tff (t,clk, rstn,q);  
 input t,clk, rstn;
 output reg q;
  always @ (posedge clk) begin  
    if (!rstn)  
      q <= 0;  
    else  
        if (t)  
            q <= ~q;  
        else  
            q <= q;  
  end  
endmodule
```
OUTPUT:-

Simulation :

![image](https://github.com/Hariharan177/VLSI-LAB-EXP-4/assets/164841000/32379154-79d1-463f-8c1f-bf879f967a72)

Elaborated Design :

![image](https://github.com/Hariharan177/VLSI-LAB-EXP-4/assets/164841000/c1678daa-2dfc-4496-924d-6cfd238fc71a)

#7

UP DOWN COUNTER :-

Code:
```
module updown_counter(clk,rst,updown,out);
input clk,rst,updown;
output reg [3:0]out;
always@(posedge clk)
begin
if (rst==1)
out=4'b0000;
else if(updown==1)
out=out+1;
else
out=out-1;
end
endmodule
```
OUTPUT:-

Simulation:-

![image](https://github.com/Hariharan177/VLSI-LAB-EXP-4/assets/164841000/e80a92e6-736e-4a5d-a4df-61af58c6d1df)

Elaborated Design:-

![image](https://github.com/Hariharan177/VLSI-LAB-EXP-4/assets/164841000/a4672fd9-bdef-49f8-9410-d29c3ed54ec6)

RESULT :

Simulate And Synthesis SR, JK, T, D - FLIPFLOP, COUNTER DESIGN is Successfully Verified using Vivado Software.





