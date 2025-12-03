**.lib**
.lib contains the slow fast and medium speed cells
Open Sky130 library
![image](libraryfile.png)
130--> 130nm library
tt--> typical
025c--> temprature
PVT: Process Voltag Temprature; these are important for design to work
Process variation are due to fabrication i.e. variations due to fab machines. Variations are also in voltage and temprature. These PVT defines how the Silicon works
eg, a product used in different conditions so need it to work in all conditions.
You can see operating conditions, voltage, process, time units, resistance unit used in the same file
![image](operatingcnd.png)
.lib is a bucket of all std cells as shown below, CELL marks the begining of cell defination
eg cell is and 2 or gate a2lll0_1
![image](and2or.png)
we can open its behavioral model
withoutr PP we will open , PP->> Power port 
!A --> A is off
D1--> D is on
Power associated with this is mentioned 

**Hierarchical vs Flat synthesis**
Open multiple_modules.v file located in verilog files directore
![image](mmodule.png)
Now, first launch yosys and read the lib file 
![image](liberty.png)
read verilog file multiple module.v
![image](readmodules.png)
synthesise, you can see the deails as below
After this use abc -liberty and SHow, it will show hierarchial design
![image](showy.png)
Now will see how netlist looks like 
can use no attr switch, hierarchies will be preserved
![image](attrsw.png)


**Stacked Nmos is better thhan Stacked PMOPS

Now will see *FLATTEN*
![image](flat.png)
Flatten and show, you wil not see U1 and U2 unlike before
![image](flatten.png)
**Submodule level Synthesis**
![image](submo.png)
it infered only gate.
now will link the design using abc - liberty
![image](submo1.png)
and then show 
So only submodule 1. we did controlled the module which we was synthesising becoz say if we have a same module instantiated multiple times, so instead synthesisng the same module say 4 times, we synthesise he modules once and replicate the netlist maany times in top level
So Modulelevel systhesis is prefered when have multiple instances of same module
Also second reasom is if say design in massive and if design is given to the tool, it will not werk properly so will prefer giving portion by portion to get good optimized netlist, stiched at the top level.
synth -top <module name >is used in yosys to control which module to sysnthesise


**FLOPS AND FLOP CODING STYLE**
All files reqired are in verilog files directory
Flop: Combi ckts have propogation delay so glitches are exopected, 
![image](flop.png)
So we need element to store a value called flop. Flops are storage elements
If put flop between Comb clks, even though input is unstable, output will be stable and glitch will not be propogating throughout and output of combi ckt will be stable
There is a initial stage of flop. To initialize we have reset and set which can be asyn or sync

*Flop with asynch Reset*
Thsi is a posedge flop, whenever the clock and rest changes, if reset happens, If is have high priority then else. If any changes in CLK or reset, always block is executed
Under async reset, q will go low upon this asyn_rest. Else, only at posedge, q is getting d. If negedge, always block will not be executed. Its async rest as it does  not wait for any clock 
![image](asyncreset.png)
Synchronous, will turn to D pin of the flop
![image](asynset.png)
**flop with both sync and asyn set reset**
![image](syasy.png)

**Lets now simulate the flops**
![image](asyncrst.png)
It shows that when reset commes, immediately the q comes down
Now will see for async set
Set is 1, q is 1 irespective of d unless set is 1. Its async set behaviours
![image](asyncset.png)
Now will see sync reset
Reset is  priority here
![image](syncrst.png)

**Now lets synthesise these ckts and see what happens**
Will now go to YOSYS. lets synthesise async reset flop
1. Read liberty files
2. Read design by read_verilog
3. Set synth -top
4. as using flop, need to use dfflibmap -liberty as in flow, seprate flop library is there in std cell library, so need to mention this for tool to aware of where to pick this from here no such thing, we have same library so will point to same library
![image](sync_asyncrst.png)
5. So we wrote flop with active high reset but flop have active low rst so tool inserted invertor.

Similarly can synthesise other codes
Now will see flop with sync reset
<img width="1904" height="1170" alt="image" src="https://github.com/user-attachments/assets/e7d6e62e-ca2c-427a-b7b9-795e2c7df79d" />
Here, no set pin no reset pin, it only have sync reset
We can see A_N i.e. inverted input.
<img width="1234" height="517" alt="image" src="https://github.com/user-attachments/assets/7142d199-4896-472d-b38a-f610f14b3976" />



