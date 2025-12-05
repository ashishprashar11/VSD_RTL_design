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

