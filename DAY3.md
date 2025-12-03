**COMBINATIONAL AND SEQUENTIAL OPTIMIZATION**
COMBINATIONAL logic OPTIMIZATION: Squeezing the logc to get most optimized design in terms of area and power savings
Techniquest used are :
a. Constant Propogation i.e. Direct Optimization
b. Boolean Logic Optimization i.e K maps or Q-MCkl algos
eg, <img width="1235" height="622" alt="image" src="https://github.com/user-attachments/assets/dfeae421-313a-487c-a40c-5d90ac89ac43" />
<img width="1166" height="604" alt="image" src="https://github.com/user-attachments/assets/92881e61-5551-4aea-9f1e-7978d041a237" />

Synthesis tools do these things to get moist simple logic

SequentialL logic OPTIMIZATION:
Again 2 types,
1. Basic - Sequential constant Propogation
2. Advanced(Not covered in this course) - 1. State Optimization, 2. Retiming, 3. Sequential Logic Cloning (Floor Plan Aware Synthesis)
   If reset, q=0, and if d=0 irrespective of rst, q=0
   It will propogate and gives (A.0)'
   In second case , set applied, q=1,
   if no set, and clk is thesre q = 0, i.e taking both values of 0 and 1
   q is not equal to set
   So this can not be optimized and needs to be retained as such.
  Every D flop is not sequential constant
<img width="1292" height="668" alt="image" src="https://github.com/user-attachments/assets/e9f3717f-d620-4a55-9f89-3c5d9e71f923" />
*State Optimization: Optimizaton of unused state, gives condensed use of states*
*Cloning, followed while doing Physical aware synthesis*
*If in floor plan flop sitting distance apart, long routing delay ill be there, If say large positive slack at A, soi instead of a be 1 fop we have 2 flops and logic a1 goes to 2 flops
Now have 2 copis of A and also no issue ad large +ve slack at A*
*Retiming: If combo ligoc is say 5ns and of 2 ns, Clk to  delay and stup time =0,and ave limitation of 200 and 500Mhz fo clocking. So we wil shift the logic such that both elays are say 4ns and 3 ns leading to logic to work at 250 and 333Mhz*
<img width="1286" height="664" alt="image" src="https://github.com/user-attachments/assets/d1ebb2d1-2724-4d63-aa4c-42fabc610c37" />

***COMBINATIONAL LOGIC OPTIMIZATION**
We will use opt files
<img width="1730" height="44" alt="image" src="https://github.com/user-attachments/assets/16009055-eda2-43d2-bc81-cb08192a9d31" />
opt_check.v looks like below
<img width="507" height="175" alt="image" src="https://github.com/user-attachments/assets/c7eba3ce-dd24-4f58-927e-7fd824ebff78" />
i.e. assigning y based aon a
i.e. 2x1 mus
Expected to be optimized as 2x1 mus
Now opt_check2
<img width="524" height="222" alt="image" src="https://github.com/user-attachments/assets/36067a8f-2caf-47a2-a298-69e5e8e0a4c1" />
<img width="951" height="436" alt="image" src="https://github.com/user-attachments/assets/db00f15c-e5ce-40d0-bcf7-5f35bb4dcd5a" />
Now we will invoke Yosys
<img width="931" height="375" alt="image" src="https://github.com/user-attachments/assets/b3338271-f8d4-4a13-a9d9-f6b5ac8edb20" />
<img width="764" height="198" alt="image" src="https://github.com/user-attachments/assets/fa30eaf9-7e3b-45eb-a4af-a79fbd224b33" />
Command to do optimization is opt_clean -purge
<img width="680" height="552" alt="image" src="https://github.com/user-attachments/assets/7a88e15e-be93-42e9-b7ff-0666af989b46" />
All optimizations are dome now will link it to abd -liberty and show. We will get the and gate as expected
<img width="1904" height="1170" alt="image" src="https://github.com/user-attachments/assets/9ce96de2-7ec5-40a8-89ee-480d2991f06a" />

opt_check2 will be aslo have or gate
<img width="1904" height="1170" alt="image" src="https://github.com/user-attachments/assets/c845a69b-4180-4a07-b040-c8e012a6754c" />

Now will see opt_Check3, will get 3 input and gate
<img width="566" height="88" alt="image" src="https://github.com/user-attachments/assets/674e9bc8-f60b-4c2b-b8ff-142bd643bd8b" />
<img width="1692" height="824" alt="image" src="https://github.com/user-attachments/assets/adca9602-e924-429c-acbd-be21becb15af" />

***SEQUENTIAL LOGIC OPTIMIZATION**
We will use file named with dff_const
lets see for dff_const1 and dff_const2
<img width="589" height="769" alt="image" src="https://github.com/user-attachments/assets/40e51b66-3ea0-4d4a-9045-b243e671b12a" />
dff_const1: if reset q=0 else q=1 , Dis always 1'b1
Rsest cn be deasserted anywhere but q will change only at clock edge
dff_const2: if reset, i.e set here , d is tied to 1, if reset removed q=1 and is tied to 1 
<img width="852" height="513" alt="image" src="https://github.com/user-attachments/assets/355ab722-25c6-42ca-bafd-d110c46e0196" />
lets simulate first
Q wil wait for edge of clock in first
<img width="1232" height="292" alt="image" src="https://github.com/user-attachments/assets/b86bd933-7a36-4141-b255-1721c70b3337" />
but in second case it will be 1
<img width="1920" height="182" alt="image" src="https://github.com/user-attachments/assets/37bb228c-388d-4ae5-9c55-2a255bfe6883" />
Now will synthesise
<img width="1873" height="943" alt="image" src="https://github.com/user-attachments/assets/5e882dfe-7d4d-4e52-97ac-c51a6c349418" />
So, dff we got i.e. has everthinmg as expected. STD cell lib expecting the reset to be active low, but we coded as active high so tool infering invertor here
IF !reset it would not have infered the invertor
Now will see another one
<img width="965" height="411" alt="image" src="https://github.com/user-attachments/assets/7f0f9fa2-1ddc-4daa-88bc-c894cbc4cb98" />
No flop infered in second case 
Q is always 1 so no flop 
<img width="1586" height="874" alt="image" src="https://github.com/user-attachments/assets/f0a680c2-55f6-4c5e-8a23-91094a72e48e" />
Now const 3
<img width="696" height="489" alt="image" src="https://github.com/user-attachments/assets/2348cce9-42f8-402a-8b33-5eadc37a5bef" />
<img width="1083" height="194" alt="image" src="https://github.com/user-attachments/assets/81892db3-9695-4b06-9843-9a893ba7b140" />
<img width="1626" height="318" alt="image" src="https://github.com/user-attachments/assets/31acd0e1-18b3-4d42-b139-9d21cf57dd94" />
<img width="784" height="385" alt="image" src="https://github.com/user-attachments/assets/4743b417-3521-4de0-9c37-30873f71da19" />
lets synthesise
this will infer 2 flops
<img width="1920" height="1118" alt="image" src="https://github.com/user-attachments/assets/815e48a6-ca0a-4458-9084-777cffe3f3ce" />
std cells are infered here. First is reset flop, second is set



















 
