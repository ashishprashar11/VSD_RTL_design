**Introduction:** 
Simulator : Tool used to check a design. RTL is implentation of spec and adherence to spec is checked using the tool Iwave (SIMULATOR)
Testbench: To ensure design adhere to specified specification, need to apply stimulus to design to check functionality For ever change in input, output is evaluated. If no change inm input, no evaluation happens
eg: AND gate, 2 inputs one output. for boh 2 inputs need to applly input and check the output. We need both stimulus generator and observer.
Iverilog simulation flow:
Design >> write TB >>>iVerilog >>> output be VCD file (VALUE CHANGE DUMP) -> USe GTK wave tool to see waveform 
Now will see how to work with iverilog and GTWAVE
Load design in i verilog
Use command iverilog <File_name.v> <TB_for_File_name.v>

Use gtkwave to see the waveform 
<img width="1667" height="699" alt="image" src="https://github.com/user-attachments/assets/56ba8721-09f7-4f90-a8a8-7080e347233f" />

**YOSIS and LOGIC SYNTHESIS**
Synthesizer is used o convert the RTL to netlist --> yosys is used here
Design>>.lib-->YOSYS-> Netlist (rep of standard cells)
Commands:
read_liberty--> read the .lib file
read_verilog--> read the design
write_verilog--> execution gives the netlist and shol be rep of the design in form of cells present in the .lib
? How to verify that systesize is done correctly??
To verify synthesis output, 
Netlist + Testbench --> iverilog --> VCD file -> GTKWAVE and waveform output, stimulus should be same as the output obseved during RTL simulation.
Netlist is the true form of design 
Testbench will be same as a RTL testbench. We dont need new testbench

**LOGIC SYNTHESIS:**
RTL design is the behavioral rep of required specification. 
RTL to gate level transition is called synthesis
Design is converted to gates and gates are connected. THis is given as a file called netlist

RTL+Front ENd Lib --> SYnthesis --> NETLIST
.lib: Its a collection of logic modules i.e different varients of gate (slow medium fast, as combinatonal delay in logic path determine the max speed of operation)
FAST CELLS--> setup 
tclk>Tcq_a+Tcombi+tsetup_b
tclk, clock period 
Tcq_a, clock propogation delay of A flop
Tcombi, is combinational circuit propogatrion delay
tsetup_b, is a time before the clock edge, need to supply data to B flop
so, Fclk (max)=1/Tclk(min)
High Fclk, need cells to work very fast.

Faster cells come ih penaly of area and power. The load in digital ckt is in form of capacitance, faster charging/dischagring i.e. small capacitance, lesser the delay. It needs the transistor capable of sourcing more current i.e. wide transistors 
Wide transistor -> Low delay --> More area and Power

SLOW CELLS--> hold
Thold(b)< Tcq_a+Tcombi
Thold(b)< Tcq_a+Tcombi
What A flop launch in first cycle, should be captured by B at next cycle, so delay from a to b should be greater then hold time, 
To make sure no hold issues at capture flop (b) , need slow cells

Slower cells. The load in digital ckt is in form of capacitance, slower charging/dischagring i.e. large capacitance, more the delay. i.e. narrow transistors.
Narrow transistor0-> Hign delay --> Less area and Power

So need to guide the sysnthsizer to select the flavour of cells
To guide synthesizer, we use Constraints

**Synthesizer:**
1. Do Syntax check
2. MAp design (Module to top level design)
RTL converted in the form of Standard cells and givenm in the form of netlist
**LAB3: Intro to YOSYS**
Invoke Yosys 
<img width="1100" height="743" alt="image" src="https://github.com/user-attachments/assets/d13b68e9-9a3f-4e0d-8d3d-36547d59981b" />

Read the library now 

<img width="761" height="467" alt="image" src="https://github.com/user-attachments/assets/49742272-5841-470c-aaf6-27c61985b799" />

Library has special name. 
Now we will read design 
<img width="1059" height="521" alt="image" src="https://github.com/user-attachments/assets/9fbc6b8a-edd1-43a5-831b-161fa5c7eb55" />

If more hen 1 file, we will read all files.
Now use synth -top <module to be synthesise>
we will use good_mux module here
<img width="801" height="759" alt="image" src="https://github.com/user-attachments/assets/a34069d3-39bd-42ee-a955-3916eae8f8b8" />


Now will see its code 
<img width="811" height="278" alt="image" src="https://github.com/user-attachments/assets/9c530ee8-3915-40d5-a200-e49c6797397f" />

Its pure combi circuit
Now will generate netlist
use abc -liberty <path>
<img width="601" height="129" alt="abccommand" src="https://github.com/user-attachments/assets/05f0013f-09a9-4730-97d9-ae522a5154cd" />


It will convert RTL to gate level netlist
In message it will print the info of input , outputs and cells used i.e mux here
<img width="601" height="430" alt="signals" src="https://github.com/user-attachments/assets/43312e47-b908-4fd4-a937-2cab8a5efadc" />


Use *show* to see reqized logic 
<img width="1486" height="887" alt="image" src="https://github.com/user-attachments/assets/7043daab-97d7-44d9-99c2-03a037af790c" />


Now will see how Netlist looks
use __write_verilog <name>__ and to open use __!gvim <name>__
<img width="1236" height="705" alt="image" src="https://github.com/user-attachments/assets/8c48a74a-d1a0-4a53-869a-647ca7df4b38" />

It have lot of info now will use one swich to ge more shorted netlist
use **write_verilog -noattr <name>**
<img width="1236" height="707" alt="image" src="https://github.com/user-attachments/assets/189b8069-afe3-478f-9942-fe8d191db1bc" />
