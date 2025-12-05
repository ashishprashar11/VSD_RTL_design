x xxxxxxxxxxxxxxxxx**If, Case statements**
If --> Used to creat the priority logic
Syntax 

<img width="218" height="176" alt="image" src="https://github.com/user-attachments/assets/4f255f8d-372c-475c-a23a-ab5553a7c8e6" />
<img width="264" height="322" alt="image" src="https://github.com/user-attachments/assets/667091ec-e65f-496b-8880-e1d7e716fbce" />
__________________________

**if** will get highest priority. Only if not met, so to second if else, againn if not then next otherwise else
In hardware it will be like the MUXES as show in PIC
<img width="911" height="520" alt="image" src="https://github.com/user-attachments/assets/f62823b4-3a12-4a4b-ab00-54ff0e0e38a3" />
**Cautions with IF statements: Infered Latches**
Due to bad style of coding, latch will get infered. If comes with incomplete if statement

<img width="212" height="110" alt="image" src="https://github.com/user-attachments/assets/6ed99cce-86c1-406e-8cd4-54e2059833ca" />

No "else", we stated if condn 1 and 2  waht will be happening. However if none meet, it will an issue. So tool will infer a latch and connect as shown in pic to retain the value. The enable of Latch will be OR of cond1 and cond2. So when none condn meets, enable will go low and latch stored value will be driven here.
This is coming due to incomplete If statement
<img width="942" height="534" alt="image" src="https://github.com/user-attachments/assets/92e031eb-99e6-4a25-b3d9-e74f803cbdb7" />

COUNTERS:
<img width="315" height="184" alt="image" src="https://github.com/user-attachments/assets/bbc6a0b3-9efb-4884-911c-17e16c0de31d" />

Here aslo no else but its fine here.
Always while coding, think for Hardware. See Attached pic.If en is there, count is count+1 i.e. incrementer. If no enable it should latch to prvc value. So here no en count should latch to prvc value. i.e if 4 will be 4. So intended behavior.
However in combi ckts we should not have inferred latches
Incomplete IF else is ok or not Ok is piurely based on what we are trying to do.
<img width="892" height="504" alt="image" src="https://github.com/user-attachments/assets/56fb6be3-8409-4b30-9c18-083d04eb23d2" />

Now will see CASE statement 
**if, case are ised nside always block 
The variable assigned in if or case should be a register variable
<img width="158" height="338" alt="image" src="https://github.com/user-attachments/assets/57ab7006-a6cf-474c-bc8c-1441ae303354" />
It will be 4 input mux. See pic
<img width="908" height="507" alt="image" src="https://github.com/user-attachments/assets/8327bcb3-7d21-4179-b0de-2f720c49bdb4" />
**Issues with CASE assignments.**
Like incomplete if, incomplete case also infer latch.
--> Incomplet case:
Sel is 2Bit, 4 combinations are possible so 4x1 mux. we mentioned what will happen when c1 and c2 occur but not for c3 and c4 so it will infer latch for these 2
To avoid this, code case should be with "default".
<img width="930" height="530" alt="image" src="https://github.com/user-attachments/assets/d4ba9a2b-aac6-4bef-b326-1b9be276faaa" />
There are more things to be taken care in case 
--> Partial assignments in case
Lets say we are trying to control 2 outputs in case.
in second case when 2'b01, both x and y are not defined.
Here 2 muxes will get infered as 2 outputs x and y. It looks like if default is there all done. But see pic 
when sel = 00, x=a, y =b
when sel = 01, x=c, y = Not defined __partil assignemnt... this will lead to infered latch
for default, told to follwe d 
<img width="905" height="505" alt="image" src="https://github.com/user-attachments/assets/652003b7-a66f-499d-a354-0bdc5813d930" />
So, assign all he outputs in all the segments of the case. 
In case of if stmts, if "if " is executed, no else thing can be executed. But in "case" things are different. And it will give unpredictable outputs like as shown in pic with 2'b1? i.e. in bad case like if 2'b10, 2 matches will be there. If in "If", condition meets, it will comeout after match but not in "case", it will check every case even if it matches.
So no overlapping case should be there

<img width="898" height="511" alt="image" src="https://github.com/user-attachments/assets/5ef4be1d-b1c1-4e79-9b39-46b402e72568" />

_____________
Will start with in complee If
<img width="1061" height="79" alt="image" src="https://github.com/user-attachments/assets/13ac4ea6-47c6-42b4-b59c-9ca5577276e0" />
<img width="878" height="496" alt="image" src="https://github.com/user-attachments/assets/10005b49-14f2-4857-9c15-0e2e53dba4c0" />
<img width="1366" height="842" alt="image" src="https://github.com/user-attachments/assets/56aa88fd-4359-45c4-a6a2-34e6b406bf64" />
No we will simulate and synthesise this
Whenever i0 (sel line) high, y is following i1. If low, its following prvc value. Momement i0 going low taking the I1 value.
<img width="1900" height="897" alt="image" src="https://github.com/user-attachments/assets/9de5ed67-e852-47b1-9b3e-ff30db9f4586" />
Now will synthesis
Our goal is to  code a mux but tool infered latch
I2 not used, i0 enable pin i1 is the d, q is to Y 
<img width="1302" height="930" alt="image" src="https://github.com/user-attachments/assets/16fcc441-974e-4aa8-9cd6-ce7c140f0e6f" />
i.e. the infered latch comming out of incomplete IF statement

**Now lets see incomplete_if2
<img width="870" height="930" alt="image" src="https://github.com/user-attachments/assets/b7676f9c-bb38-4e73-bd95-d587d654eaa1" />
Here what will happen if i0 and i2 both are false is not mentioned. So they will latch
So we will get latch
SO we will get such that i0 i1 ored are the enable of the latch as shown in pic. we wil aso have a combo ligic of these at input of latch 
<img width="1217" height="555" alt="image" src="https://github.com/user-attachments/assets/d989a835-f773-4564-9b5f-89879ec23ee4" />
Now we will simulate and synthesise
<img width="1908" height="930" alt="image" src="https://github.com/user-attachments/assets/28597ab0-18a2-48ab-9749-8ea99e44ebcf" />
When i0 high, o/p is following i1
When i0 low, o/p looks toward i2. So in window when i0 , i2 both low, o/p is constanst. When I2 goes high, it starts following i3
<img width="1908" height="948" alt="image" src="https://github.com/user-attachments/assets/fea23e5f-8bbe-44ec-b848-f8a14a7c6cf3" />
so we got combo logic fxn of i0, i1, i3 and i2 i.e. we expected and enables of latch io ored with i2. If both i0, i2 0, it will latch 

**Now lets see incomplete CASE statements**
<img width="1076" height="948" alt="image" src="https://github.com/user-attachments/assets/ca168ee9-8dd2-41d0-80cf-98538192a428" />
for sel 00, 01 its defined but nothing defined for 10 and 11 also default is not coded so it will be going to latch.
Whenever select of 1 is 1 we have latching action as shown in truth table when 0
<img width="925" height="468" alt="image" src="https://github.com/user-attachments/assets/5b746437-46e7-4682-b541-d0f2a1951dc5" />
Now lets simulater and synthesise
Its latching for 10 and 11
<img width="1908" height="948" alt="image" src="https://github.com/user-attachments/assets/4870ae0d-21e1-4fc2-927b-c349116cec86" />
<img width="2594" height="840" alt="image" src="https://github.com/user-attachments/assets/8ad46e9c-e424-4257-818e-1fd4baa8c019" />
So we get latch with enable condition of same as expected. Its negative latch so sel is buffered only 

**Now lets see a complete case**
Here no latch expected
<img width="1662" height="884" alt="image" src="https://github.com/user-attachments/assets/5e8d8ef0-b890-4cff-9e65-fac930e08f24" />
<img width="1896" height="884" alt="image" src="https://github.com/user-attachments/assets/4089d5ec-aeb9-4c04-a599-07907b6df87a" />
as expected results, now we will synthesis
No latch will be infered here 
<img width="1912" height="1054" alt="image" src="https://github.com/user-attachments/assets/70be8836-feda-4c02-96be-4406176e2b74" />
**Now lets see a Partial case**
<img width="1129" height="371" alt="image" src="https://github.com/user-attachments/assets/384c1764-e6b2-49c4-b1d1-15e9a50b59d2" />
<img width="937" height="520" alt="image" src="https://github.com/user-attachments/assets/b2432533-f542-4650-8f87-82f297b553c5" />
It follows redundancy theorem **a+a'b=a+b**
<img width="2446" height="928" alt="image" src="https://github.com/user-attachments/assets/d04d8978-1c01-4832-9b8e-fac53d7f4577" />
I.e. what we expected 
In case, overlapping condition is also problem. Allcase statements are not mutually exclusive
We will see file maned bad_case where where sel 2'b1? is included 
<img width="1246" height="384" alt="image" src="https://github.com/user-attachments/assets/580d8726-caff-4c00-a89f-dc53e0c1a833" />
Here we will get sim and synth mismatch 
11 and 10 both conditions matching, tool is confused 
<img width="2446" height="928" alt="image" src="https://github.com/user-attachments/assets/4f0f289c-2ec9-4db4-aa35-5e4761094c6c" />
If we synthesise this, here no inferred latch as its a full case so no latches. Bt problem is there with overlapping case
<img width="2464" height="948" alt="image" src="https://github.com/user-attachments/assets/7f730cf3-e021-4c9c-8398-79ca7a6b3b69" />
Lets try GLS on this 
<img width="1880" height="1512" alt="image" src="https://github.com/user-attachments/assets/ba0e14d7-d3b2-412c-93cf-da418d41a8ee" />
Here its clean ie 00--> i0
01 -->i1 
10 -->i2
11 -->i3
No confussion here unlike RTL simulation 
SUCH CODING PRACTICES SHOULD BE AVOIDED

**Will see ow to use looping construct to generate the hardware, simplified the hardware**
**LOOPING CONSTRUCTS**
In verilog, there is a **for** loop and a **generate** followed bu a for loopp
FOR loop is used in always
GENERATE and not be used in for loop. It should not and cannot be used inside always loop
GENERATE is used to instantiating the hardware
eg, if need to instantiatethe & gate 100 time, in such case nned to use generate with for loop, whereas plane for loop is used to evaluating the expressions. For loop is not for generating(Instantiating) the hardware.
Eg, need & gate 100 times but can not be done by for loop. If want to evalute the expression multiople times, need to use the FOR Loop
32:1 mux will become more comlex if follow the approach as below
<img width="1334" height="603" alt="image" src="https://github.com/user-attachments/assets/36326d0a-452a-42ce-b731-78d4d75e1511" />
Instead, can use below approach
<img width="938" height="515" alt="image" src="https://github.com/user-attachments/assets/47a5b1af-1359-4a2d-8249-0012057e6675" />
Same is the case with demultiplexer,
Eg 1x8 demux
<img width="897" height="520" alt="image" src="https://github.com/user-attachments/assets/e9540a77-ad2a-438d-927d-6b1675fe9928" />
**FOR GENERATE**
Lets say we need t instantiate 500 time say 500 instances of & gate.
For generate is for replicating the hardware
Its used outside always block 
<img width="916" height="515" alt="image" src="https://github.com/user-attachments/assets/216317e1-7f81-4b95-a68c-376da0cc7601" />
This will instantiate & gate 8 times. SO each will have a, b anf y pin. It is replication of hardware.
eg ripple carry adder(RCA), where we need to add 2 binary numbers
if carry is there need to card forward. Carry ripple till the last.
It will have multiple full adders like shown below
<img width="886" height="502" alt="image" src="https://github.com/user-attachments/assets/439bd988-42cf-43cf-9b9f-06561a10e195" />
So here instantiating 3 times the full adder. If say we have 500 bit then it will be issue. In such cases need this approach
Similarly can use the if generate approach also but same outside the Always block
QUICK COMPARISON SUMMARY 
<img width="880" height="302" alt="image" src="https://github.com/user-attachments/assets/3747f309-9bee-4e27-9822-955b403d079c" />
_________________________________________________________________________
No wwill see looping constructs in LAB
First lets see MUX
file used is mux_generate.v
<img width="1013" height="420" alt="image" src="https://github.com/user-attachments/assets/c1cc4705-2a9d-4b12-9dc2-129871455907" />
Modile has input i0,i1,i2,i3, 2 bit select line and output (1bit)
Internally we are making bus i_int
Declared integer K
FOR loop is used here so is in always block.
Select will take only 4 values. If K and select are matching, y will be assingned he value of i_int[0][
I.e. 2x1 mux fxnality 
Lets simulate and see
<img width="1908" height="890" alt="image" src="https://github.com/user-attachments/assets/f1199eb3-dd7c-44c4-87bd-12dcfa2a7a5e" />
If do same using case statements, complexity increase like below snapshot 
<img width="905" height="481" alt="image" src="https://github.com/user-attachments/assets/12613947-28be-4ada-8293-93d32aa0cbfe" />
But in this just need to change k
<img width="1908" height="830" alt="image" src="https://github.com/user-attachments/assets/f9dce788-bfc7-4bbd-a484-d3470bd32436" />
Nest example we will see is demux
Here we will have y_int instead of i_int of mux 
<img width="704" height="395" alt="image" src="https://github.com/user-attachments/assets/96b8f2be-8681-46bf-b353-de757996685a" />
<img width="1318" height="459" alt="image" src="https://github.com/user-attachments/assets/5e664978-b22d-494e-ba28-2850b2024b92" />
Its good for small but not for bigger one say 256
see another approach where generate is used , 
<img width="1414" height="307" alt="image" src="https://github.com/user-attachments/assets/0ec683d1-189b-4d02-9a42-2e710fc7aae8" />
lets simulate and see first for case stmt
<img width="1908" height="896" alt="image" src="https://github.com/user-attachments/assets/126f2197-70d5-48c0-a946-5169bcf31ed3" />
Will see its synth also 
<img width="1458" height="884" alt="image" src="https://github.com/user-attachments/assets/b5e4c4e0-2dfa-42cf-9db5-72d475ed8b25" />

Lets see same for for generate case, both wil be same 
<img width="1908" height="858" alt="image" src="https://github.com/user-attachments/assets/64a150f6-6458-4f93-b76d-3e2c3890e7b2" />
When synthesised will lead to below
<img width="1458" height="884" alt="image" src="https://github.com/user-attachments/assets/88361978-70fb-4536-97a6-5466c1dcfe0c" />
**Now lets see example of for generate**
Lets see Ripple carry adder as discussed before in this file
<img width="656" height="336" alt="image" src="https://github.com/user-attachments/assets/ac52e891-6fc5-4bb5-b6e7-d2e01e9822ed" />

Can do in 2 ways
1 --> instantiate FA four times and conect.
It ooks simpl but its only 4. What if 32 bit no. so second way
2 --> For generate- > It will replicate the hardware
One full edder replicated based on for generate for replication 
File used are below
<img width="827" height="40" alt="image" src="https://github.com/user-attachments/assets/6c1041e8-dc83-4f8f-a7f7-b0b8c971c7da" />
<img width="1066" height="709" alt="image" src="https://github.com/user-attachments/assets/cfb5d529-8008-41a1-bd8e-fb39ff6e592d" />
Full adder: Summiong the 3 one bit binary numbers.
Ripple Adder:RULE FOR ADDITION
Add N bit and N bit no. the result will be N+1 Bits
Add N bit and M bit no. the result will be max(N,M) +1 Bits
So for 8 bit 2 no. it will be 9 bits
First adders carry should be 0 so wrote differently for the fa u_fa_0
VAriable used is genvar. It can not be declared as a integer. 
<img width="946" height="735" alt="image" src="https://github.com/user-attachments/assets/cce19914-3878-4b51-a6ff-ed42e5863456" />
Now lets simulate this
<img width="947" height="250" alt="image" src="https://github.com/user-attachments/assets/e85abff3-d196-486d-9eb4-ee9a16b4ba88" />
Error as FA is instantiated in rca so need to call this as well, need to tell tool where is the defination of this FA
<img width="1899" height="840" alt="image" src="https://github.com/user-attachments/assets/b2219798-4aa8-479d-8d4f-890570df08b4" />
<img width="1894" height="351" alt="image" src="https://github.com/user-attachments/assets/b8ac924b-0110-4641-bd2f-ff2651aed85e" />
Lets synthesise this now
<img width="974" height="1544" alt="image" src="https://github.com/user-attachments/assets/a2c77692-fb19-4f42-b13d-207e90da6e9c" />
<img width="983" height="841" alt="image" src="https://github.com/user-attachments/assets/28b301b1-edf4-4d2c-a3ab-374e53d96dc1" />
similarly can also view for FA 
<img width="992" height="830" alt="image" src="https://github.com/user-attachments/assets/72b396e1-6ee0-4cde-842e-768d732a161f" />
Now wil do GLS, 
<img width="1920" height="837" alt="image" src="https://github.com/user-attachments/assets/7855ebcd-5f1c-42bc-920e-85a71bf4202c" />
This is the GLS simulation for this RCA. 
