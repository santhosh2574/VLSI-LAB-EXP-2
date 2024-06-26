# SIMULATION AND IMPLEMENTATION OF  COMBINATIONAL LOGIC CIRCUITS

# AIM: 
  To simulate ENCODER, DECODER, MULTIPLEXER, DEMULTIPLEXER, MAGNITUDE COMPARATOR using VIVADO 2023.1.

# APPARATUS REQUIRED:
              VIVADO 2023.1

# PROCEDURE:
1. Open Vivado: Launch Xilinx Vivado software on your computer.

2. Create a New Project: Click on "Create Project" from the welcome page or navigate through "File" > "Project" > "New".

3. Project Settings: Follow the prompts to set up your project. Specify the project name, location, and select RTL project type.

4. Add Design Files: Add your Verilog design files to the project. You can do this by right-clicking on "Design Sources" in the Sources window, then selecting "Add Sources". Choose your Verilog files from the file browser.

5. Specify Simulation Settings: Go to "Simulation" > "Simulation Settings". Choose your simulation language (Verilog in this case) and simulation tool (Vivado Simulator).

6. Run Simulation: Go to "Flow" > "Run Simulation" > "Run Behavioral Simulation". This will launch the Vivado Simulator and compile your design for simulation.

7. Set Simulation Time: In the Vivado Simulator window, set the simulation time if it's not set automatically. This determines how long the simulation will run.

8. Run Simulation: Start the simulation by clicking on the "Run" button in the simulation window.

9. View Results: After the simulation completes, you can view waveforms, debug signals, and analyze the behavior of your design.

# LOGIC DIAGRAM

# ENCODER
![320416625-e0686f04-ab98-4b23-b0f7-7bfd04004b32](https://github.com/santhosh2574/VLSI-LAB-EXP-2/assets/167754920/84530796-0baa-44b5-89f3-1b141189ac4d)


# verilog code
```
module encoder_8_to_3(a0,a1,a2,d7,d6,d5,d4,d3,d2,d1,d0);
input d7,d6,d5,d4,d3,d2,d1,d0;
output a0,a1,a2;
or g1(a0,d1,d3,d5,d7);
or g2(a1,d2,d3,d6,d7);
or g3(a2,d4,d5,d6,d7);
endmodule
```
# output
![320416709-b2cb2f7d-c92a-47ec-a900-19bd3b3b0da3](https://github.com/santhosh2574/VLSI-LAB-EXP-2/assets/167754920/d5dd3a24-2022-4ab0-a26e-864be1f1b845)



# RTL DESIGN
<img width="764" alt="324467775-8105fc33-fd84-4d77-a7fa-7ccadf2a6964" src="https://github.com/santhosh2574/VLSI-LAB-EXP-2/assets/167754920/7acaa741-75da-4523-977b-3263e0f41cab">

# DECODER
![320416791-4a43503a-8dd4-4968-a06c-359e67030439](https://github.com/santhosh2574/VLSI-LAB-EXP-2/assets/167754920/522750f7-5b9f-4445-a0ee-68fef95e4a91)


# verilog code
```
module decoder(input [2:0] a,output [7:0] d );
assign d[0]=(~a[2])&(~a[1])&(~a[0]);
assign d[1]=(~a[2])&(~a[1])&(a[0]);
assign d[2]=(~a[2])&(a[1])&(~a[0]);
assign d[3]=(~a[2])&(a[1])&(a[0]);
assign d[4]=(a[2])&(~a[1])&(~a[0]);
assign d[5]=(a[2])&(~a[1])&(a[0]);
assign d[6]=(a[2])&(a[1])&(~a[0]);
assign d[7]=(a[2])&(a[1])&(a[0]);
endmodule
```

# output
![320416856-6e158ab1-eca6-450b-b59e-a212e33a3e43](https://github.com/santhosh2574/VLSI-LAB-EXP-2/assets/167754920/a6ec2855-a9c2-46e6-9a4a-11e8d85e6c84)



# RTL DESIGN
<img width="766" alt="324468386-11b97cf8-ef31-4812-85c7-5aace6ba14d0" src="https://github.com/santhosh2574/VLSI-LAB-EXP-2/assets/167754920/d4f9331b-9c01-48ca-84e7-01be93f6da74">


# MULTIPLEXER
![320417096-f2b7c963-4b8a-4ae6-918e-81248613eec5](https://github.com/santhosh2574/VLSI-LAB-EXP-2/assets/167754920/3288dbfd-5604-466d-b48a-a203ff8bb07a)


# verilog code
```
module mux(a,s,y);
input [7:0]a;
input [2:0]s;
output y;
reg y;
always@({s ,a})
   begin
      case(s)
         3'b000: y=a[0];
         3'b001: y=a[1];
         3'b010: y=a[2];
         3'b011: y=a[3];
         3'b100: y=a[4];
         3'b101: y=a[5];
         3'b110: y=a[6];
         3'b111: y=a[7];
      endcase
   end
endmodule
```

# output
![320417225-766970e9-975e-478f-8ab1-8c5df2c24ad9](https://github.com/santhosh2574/VLSI-LAB-EXP-2/assets/167754920/950f19ba-b9b9-461d-9f73-45fdb92363b9)



# RTL DESIGN
<img width="761" alt="324468711-2537a600-f8be-48cf-8998-f3fe0b1d6f11" src="https://github.com/santhosh2574/VLSI-LAB-EXP-2/assets/167754920/3869c66f-173f-4956-b645-21ec50fccb38">



# DEMULTIPLEXER
![320417283-6dcb6ced-2602-4d6d-951e-3a8c22a279f7](https://github.com/santhosh2574/VLSI-LAB-EXP-2/assets/167754920/68e551a4-38ff-464a-8fba-fde214c72707)



# verilog code
```
module demux(din,s,d);
input din;
input[2:0]s;
output [7:0]d;
assign d[0]=(din&~s [2]&~s[1]&~s[0]);
assign d[1]=(din&~s[2]&~s[1]&s[0]);
assign d[2]=(din&~s[2]&s[1]&~s[0]);
assign d[3]=(din&~s[2]&s[1]&s[0]);
assign d[4]=(din&s[2]&~s[1]&~s[0]);
assign d[5]=(din&s[2]&~s[1]&s[0]);
assign d[6]=(din&s[2]&s[1]&~s[0]);
assign d[7]=(din&s[2]&s[1]&s[0]);
endmodule
```

# output
![320417434-be30677f-15b5-4fc7-b9ec-3ec305974ccc](https://github.com/santhosh2574/VLSI-LAB-EXP-2/assets/167754920/bfb2fac7-5685-4b96-8791-0123ae1ca2a5)



# RTL DESIGN
<img width="767" alt="324469337-529c0ec3-d323-4b32-9bec-40d369cbae5c" src="https://github.com/santhosh2574/VLSI-LAB-EXP-2/assets/167754920/f27e3420-2a9c-4279-afdb-9f13f605dfa2">



# MAGNITUDE COMPARATOR
![320417851-ca9b5ed3-9b51-480a-889e-9474be9e35a1](https://github.com/santhosh2574/VLSI-LAB-EXP-2/assets/167754920/ab45c54f-1360-441f-8af0-da3234d0e45b)


**verilog code**
```
module comparator(a,b,eq,lt,gt);
input [3:0] a,b;
output reg eq,lt,gt;
always @(a,b)
begin
 if (a==b)
 begin
  eq = 1'b1;
  lt = 1'b0;
  gt = 1'b0;
 end
 else if (a>b)
 begin
  eq = 1'b0;
  lt = 1'b0;
  gt = 1'b1;
 end
 else
 begin
  eq = 1'b0;
  lt = 1'b1;
  gt = 1'b0;
 end
end 
endmodule
```

# output
![320417984-3b0a314f-3c1d-4e68-8284-020d02ebb8ef](https://github.com/santhosh2574/VLSI-LAB-EXP-2/assets/167754920/1ab3f640-9852-47fd-8926-debbe4cfeaa3)



# RTL DESIGN
<img width="761" alt="324469568-7e9455c7-f0a6-46cd-b86f-96a7b30bcef0" src="https://github.com/santhosh2574/VLSI-LAB-EXP-2/assets/167754920/d609b957-ad66-4725-9ad1-55bfb9be32de">



# RESULT
Simulation and synthesis ENCODER, DECODER, MULTIPLEXER, DEMULTIPLEXER, MAGNITUDE COMPARATOR using Xilinx ISE is verified.
