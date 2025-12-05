**If, Case statements**
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





