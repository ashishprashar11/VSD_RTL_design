**Introduction to Gae level synthesis GLS & Simulation synyhesis mismatches**
GLS: We validate RTL by testing it with TB, giving stimulus and check the O/P as per spec, RTL code was DUT.
-->Here we run the TB with netlist as DUT. Netlist is logically same as RTL code and will seamless fit in TB
? Why to run GLS??
--> to verify design correctness after synthesis
--> simulation of RTL not have notion of timing, But when design need to work, set up and hold must meet, so various flavours of cell (Slow, med and fast). So need to make sure timing is met. For GLS, design should be run with delay annotation (Out of course scope)
*GLS Setup with iverilog*
Design + Testbench -> iverilog (Traditional flow)
Design +Gate level verilog models+  Testbench -> iverilog --> VCSfile->GTKWave (Only Gate lvl verilog models are new here)
$ if Gate level verilog models are dellay annotated(Timing aware), can use GLS for timing smulation
See, cell named and can not be actually and gate, this necesary info is there in gate level verilog models. Such models are either timing aware or functional
<img width="1262" height="651" alt="image" src="https://github.com/user-attachments/assets/56fc23a2-b326-448c-bc90-f1c57ce367f7" />

? why to do fxnl val of netlist if its true rep of rtl?
Reason is synth and simu mismatch

**Simulation synyhesis mismatches**
It can happen due to 
--> Missing sensitivityt list
Simulator work on principle that if input changes then only output will change. So simu will look for activity. If no activity, no changes,
In below code, always block is getting evaluated only when sel is changing otherwise not
If sel is 0, activity is there on i0 and if sel is 1, activi is on i1. Always block is not sensitive to the i0, i1 activity due to which y will not be evaluated for them.
So it will make MUX look like latch in simulation.
The RHS way is the correct way of coding this
<img width="1306" height="707" alt="image" src="https://github.com/user-attachments/assets/aff16ca0-68a0-4e2d-90f6-46418f6836c7" />
RHS means always is evaluated when any signal changes. 
Simulation will simulate like a doube edge flop

--> Blocking and Non Blocking stmts
 Blocking and Non Blocking stmts come to picture in always block
Blocking is using "=". It execute stmnts as in order within and first stmt evaluated b4 second
Non Blocking is using "<=". Moment it enters always block, if multple assignments, it will avaluate RHS assignments first and then these wl be assigned. Order not matters. It looks like parallel evaluation. Due to this also we sees mismatches
Eg code, where creating shift register. i.e. 2 flops, upon rest (async) its 0
D go to q0 and q0 to q
if use blocking
q=q0; --> first gets executed
q0=d; --> executeed secondly
2 storages happening, 
If wrote code like RHS, i.e q0= d first and q=q0 second (MESS). q0 wil alreday have value of d  even before q assigned gets to q0. So only one flop 
<img width="1262" height="682" alt="image" src="https://github.com/user-attachments/assets/85986a42-44d1-4209-aa53-776a908b079a" />
If written in non blocking way say, q0<=d, q<=q0.Here order doesnot matter as al RHS evaluated first  then will get asssigned to LHS
--> ALWAYS USE NON BLOCKING STMTS WHEN USING SEQUENTIAL STMTS
<img width="1198" height="678" alt="image" src="https://github.com/user-attachments/assets/aacecea0-889d-447b-ac7e-931cfbb427e3" />
SECOND ISSUE With BLOCKING STMT: It will lead ti sim synt mismatch
AIM: To creat a ckt as shown
TO create we had reg q0, no issue with sensitivity list
1st is y= q0 &c then q0 = a|b
But q0 wil be executed only when second is executed and taken value is old value which is &ed with c. It will mimic a flop as when prvl value comes its flop but when synthesise will get no flop. If we change the order, 2nd is y= q0 &c first is q0 = a|b i.e. RHS code, 
I.e latest value of q0 is used here in simulation and both codes will yield same circuit in synthesis
<img width="1313" height="661" alt="image" src="https://github.com/user-attachments/assets/7e7ece52-70bb-49cf-948b-8766f71864eb" />

To makle sure no mismatch in sim and synth, we use GLS











