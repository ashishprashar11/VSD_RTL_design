**.lib**
.lib contains the slow fast and medium speed cells
Open Sky130 library
<img width="1409" height="915" alt="image" src="https://github.com/user-attachments/assets/1d8a7f54-66a8-403c-b3f9-e518e7aebf3d" />

130--> 130nm library
tt--> typical
025c--> temprature
PVT: Process Voltag Temprature; these are important for design to work
Process variation are due to fabrication i.e. variations due to fab machines. Variations are also in voltage and temprature. These PVT defines how the Silicon works
eg, a product used in different conditions so need it to work in all conditions.
You can see operating conditions, voltage, process, time units, resistance unit used in the same file
<img width="554" height="699" alt="image" src="https://github.com/user-attachments/assets/26963ae2-ce21-4efd-a092-a58ab718902e" />

.lib is a bucket of all std cells as shown below, CELL marks the begining of cell defination
eg cell is and 2 or gate a2lll0_1
<img width="1721" height="855" alt="image" src="https://github.com/user-attachments/assets/312d9fc3-8bcd-4b4d-95d2-bea010fdcdfb" />

we can open its behavioral model
withoutr PP we will open , PP->> Power port 
!A --> A is off
D1--> D is on
Power associated with this is mentioned 

**Hierarchical vs Flat synthesis**
Open multiple_modules.v file located in verilog files directore
<img width="772" height="364" alt="image" src="https://github.com/user-attachments/assets/b6d4db09-5e98-46a5-83ed-c5a0544ec88c" />

Now, first launch yosys and read the lib file 
<img width="972" height="478" alt="image" src="https://github.com/user-attachments/assets/313cb750-7990-42d8-8b77-c0f930eeacc8" />


read verilog file multiple module.v
<img width="688" height="183" alt="image" src="https://github.com/user-attachments/assets/5276d377-22e2-4799-98ff-b7910ccf52cb" />


synthesise, you can see the deails as below
After this use abc -liberty and SHow, it will show hierarchial design
<img width="7064" height="2352" alt="image" src="https://github.com/user-attachments/assets/3bec41d5-e9e5-4b08-ba80-8f2e9d88954c" />

Now will see how netlist looks like 
can use no attr switch, hierarchies will be preserved
<img width="2516" height="1140" alt="image" src="https://github.com/user-attachments/assets/e53a6d2c-5e3b-4e8b-89ab-08ffa7ea4fd6" />



**Stacked Nmos is better thhan Stacked PMOPS

Now will see *FLATTEN*
<img width="2516" height="1140" alt="image" src="https://github.com/user-attachments/assets/0c86c64c-8fcb-48ce-943f-1756c1b0e483" />

Flatten and show, you wil not see U1 and U2 unlike before
<img width="2516" height="1140" alt="image" src="https://github.com/user-attachments/assets/6c86a5c8-ad02-4e75-8359-0fbddb595e0d" />

**Submodule level Synthesis**
<img width="2516" height="1140" alt="image" src="https://github.com/user-attachments/assets/b300c56b-bec1-4907-9471-b30ee0bf6523" />

it infered only gate.
now will link the design using abc - liberty
<img width="2516" height="1140" alt="image" src="https://github.com/user-attachments/assets/34b7f135-9f42-4492-9da6-873b29f4ba2c" />

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
**OPTIMIZATION**
Lest look at rtl code
All required files are in verilog file folder
Will see mult2.v and mult8.v files
 <img width="666" height="851" alt="image" src="https://github.com/user-attachments/assets/86fce2f8-7cab-4114-98f6-b8b53f9b07f2" />
So accepting 3 bit input, 4 bit output y and y=2*a
 a    y
000 0000
001 0010
010 0100
011 0110
100 1000
101 1010
110 1100
111 1110
only last bit is getting appended
so a[0], no HW required to do so
if say x4 is there then its append 2 0s ie 5x4 = 20, 0101 * 4 = 10100
X8 appends 3 0s
In code we have y=a*2
lets see what it is synthesise to 
<img width="756" height="174" alt="image" src="https://github.com/user-attachments/assets/8f42513d-c9ba-4c40-9c31-14ed5d04c3d8" />
<img width="594" height="156" alt="image" src="https://github.com/user-attachments/assets/e3b95619-b8ce-4b3c-8cfe-b5f9f284e7c6" />
<img width="389" height="275" alt="image" src="https://github.com/user-attachments/assets/0ccb644a-e01b-41dc-a199-7567ab32ec72" />
No cells infered,
<img width="555" height="339" alt="image" src="https://github.com/user-attachments/assets/e494aab6-d873-4c4d-85d5-efe0a9d89636" />
No need to call abc as no cell to infer 
<img width="843" height="334" alt="image" src="https://github.com/user-attachments/assets/4508dfec-8a74-4599-8896-81180b2460dc" />
Show
<img width="1261" height="925" alt="image" src="https://github.com/user-attachments/assets/6ec7bdb1-1399-4180-8c63-1bb7a37b3583" />
i.e. a appended with 1'b0. I.e we expected. Now lets see its netlist,
<img width="466" height="306" alt="image" src="https://github.com/user-attachments/assets/098dd2d5-20a6-430f-a075-054f40fc9b66" />
<img width="984" height="327" alt="image" src="https://github.com/user-attachments/assets/1eec6369-aa47-4027-a9f4-d4485abe36d6" />
Now lets see 1 more secial case
a--> 3Bit No.
y--> 6Bit No.
a*9=y, a*[8+1] = a*8 + a*1 
<img width="857" height="491" alt="image" src="https://github.com/user-attachments/assets/05d91fa3-7a44-4405-b4db-50ea311db037" />
<img width="755" height="473" alt="image" src="https://github.com/user-attachments/assets/16df779a-6f85-49be-9340-69d61a196a6c" />

lets see mult8
here we have multiplication with 9
<img width="509" height="359" alt="image" src="https://github.com/user-attachments/assets/e4eaaf24-4bb5-41ac-9803-c201a9e1bbd4" />
<img width="618" height="375" alt="image" src="https://github.com/user-attachments/assets/83c2c221-e9a7-4f16-a9c0-c172c3230338" />
<img width="884" height="221" alt="image" src="https://github.com/user-attachments/assets/d530f28b-34fc-4390-8eed-092a4c767dab" />
show
<img width="1920" height="676" alt="image" src="https://github.com/user-attachments/assets/fc4bc79d-46b0-456e-9325-740402674ba0" />
to see netlist 
<img width="544" height="318" alt="image" src="https://github.com/user-attachments/assets/f1391e44-eb5f-44f0-a522-dcaf391c5349" />
<img width="431" height="346" alt="image" src="https://github.com/user-attachments/assets/3cca050f-56b6-4c45-948c-fd35a1986c6a" />









