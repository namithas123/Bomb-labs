# Bomb-labs
**RE-challenge**
*PHASE_1*
 Open in radar ,You can find password to first phase
*Public speaking is very easy.*

*PHASE_2*
break phase_2
```
   0x08048b59 <+17>:	push   eax
   0x08048b5a <+18>:	push   edx
   0x08048b5b <+19>:	call   0x8048fd8 <read_six_numbers>   //showing that input is 6 numbers
   0x08048b60 <+24>:	add    esp,0x10
```
"password.txt of phase1"

//type random 6 integers
disass phase_2

find break points   ---1
```
  0x08048b63 <+27>:	cmp    DWORD PTR [ebp-0x18],0x1   //cmpare 1st element as 1
   0x08048b67 <+31>:	je     0x8048b6e <phase_2+38>
   0x08048b69 <+33>:	call   0x80494fc <explode_bomb>
   0x08048b6e <+38>:	mov    ebx,0x1                //ebx=1
   0x08048b73 <+43>:	lea    esi,[ebp-0x18]         //esi has first inputed number
   0x08048b76 <+46>:	lea    eax,[ebx+0x1]          //eax=2
   0x08048b79 <+49>:	imul   eax,DWORD PTR [esi+ebx*4-0x4]//cmp second input as eax(2)
   0x08048b7e <+54>:	cmp    DWORD PTR [esi+ebx*4],eax    
   0x08048b81 <+57>:	je     0x8048b88 <phase_2+64>
   0x08048b83 <+59>:	call   0x80494fc <explode_bomb>
   0x08048b88 <+64>:	inc    ebx                    //inc ebx
   0x08048b89 <+65>:	cmp    ebx,0x5                
   0x08048b8c <+68>:	jle    0x8048b76 <phase_2+46>
```
loop:
eax=1,ebx=1 initially
eax=ebx+1
eax=eax*ebx
ebx++
1
2 
6
.
.
24 
120                  //ebx<=5
720
Password:
*1 2 6 24 120 720*

*PHASE_3*


run ...
```
|           0x08048bb1      68de970408     push str.d__c__d  ; 0x80497de ; "%d %c %d"  // int char int is password
```
1st--[ebp-0xc]
2nd--[ebp-0x5]
3rd--[ebp-0x4]

   0x08048bc9 <+49>:	cmp    DWORD PTR [ebp-0xc],0x7  //consist of 1st integer
    uses any number fron 0 to 7



Combinations are used in this phase
when 1st is 0
0x08048bd6 <+62>:	jmp    DWORD PTR [eax*4+0x80497e8] // shows to where the pointer moves
   according to how we run the program

EG: if run pass.txt
       1 t 4
       (gdb) until *0x08048bd6
       gdb) x/x $eax*4+0x80497e8
          0x80497ec:	0x08048c00 //directs to the address to disply other charecters
```
   0x08048c00 <+104>:	mov    bl,0x62              //bl gets b
=> 0x08048c02 <+106>:	cmp    DWORD PTR [ebp-0x4],0xd6 //cmp if 214
   0x08048c09 <+113>:	je     0x8048c8f <phase_3+247>
```
PASSWORD
hence one combination is 
*1 b 214*





*PHASE_4*

0x8049808:	"%d"
then we went furthur to func4
```
   0x08048ca8 <+8>:	mov    ebx,DWORD PTR [ebp+0x8]  //input into ebx  
 0x08048cab <+11>:	cmp    ebx,0x1 //inp<=1-- return 1
```
else
```
0x08048cb3 <+19>:	lea    eax,[ebx-0x1]   //eax=ebx-1
0x08048cbc <+28>:	mov    esi,eax         //moving to esi
0x08048cc1 <+33>:	lea    eax,[ebx-0x2]   //eax=ebx-2
0x08048cca <+42>:	add    eax,esi         func4(n)+func4(n-1)
```
1 1 2 3 5 8 13 21 34 55
input=4
if (n=3)
  eax=5-----5
 soo
 if eax=55 
  that means n=9

*9*
the program is basically fibonacci series


*PHASE_5*
```
 0x08048d3b <+15>:	call   0x8049018 <string_length>
   0x08048d40 <+20>:	add    esp,0x10
   0x08048d43 <+23>:	cmp    eax,0x6                         //sHOWING string length to be 6
````


esi=isrveawhobpnutfg

eax=ef
````
   0x08048d72 <+70>:	push   0x804980b            //shows'giants'
   0x08048d77 <+75>:	lea    eax,[ebp-0x8]
   0x08048d7a <+78>:	push   eax                  //shows 	"srveaw" //when input is "abcdef"
````




```
ebx == abcdef
esi == srveaw
edi == giants
edx == srveaw
ecx == giants
```

Our first letter of the password is ‘g’. It lies on the 15-th index of the string in esi.
So, we must find a character whose ASCII representation when AND-ed with 0xf returns 15.


a & 0xf gives 01 ---s 
so for g---- position in esi is 15
 so find a char which anded with 0xf forms binary of 15--o

15-o
0-p
5-e
11-k
13-m
1-a


*PHASE_6*

edx=23456

DWORD PTR [ebp-0x34]:0xfd:253


eax=123456
// numbers are inputted by 4 byte
```
 0x08048fe4 <+12>:	lea    eax,[edx+0x14]
   0x08048fe7 <+15>:	push   eax
   0x08048fe8 <+16>:	lea    eax,[edx+0x10]
   0x08048feb <+19>:	push   eax
   0x08048fec <+20>:	lea    eax,[edx+0xc]
   0x08048fef <+23>:	push   eax
   0x08048ff0 <+24>:	lea    eax,[edx+0x8]
   0x08048ff3 <+27>:	push   eax
   0x08048ff4 <+28>:	lea    eax,[edx+0x4]
   0x08048ff7 <+31>:	push   eax
```

Dump of assembler code for function phase_6:
````
   0x08048d98 <+0>:	push   ebp
   0x08048d99 <+1>:	mov    ebp,esp
   0x08048d9b <+3>:	sub    esp,0x4c
   0x08048d9e <+6>:	push   edi
   0x08048d9f <+7>:	push   esi
   0x08048da0 <+8>:	push   ebx
=> 0x08048da1 <+9>:	mov    edx,DWORD PTR [ebp+0x8]                  //123456
   0x08048da4 <+12>:	mov    DWORD PTR [ebp-0x34],0x804b26c  
   0x08048dab <+19>:	add    esp,0xfffffff8
   0x08048dae <+22>:	lea    eax,[ebp-0x18]
   0x08048db1 <+25>:	push   eax                                      //i
   0x08048db2 <+26>:	push   edx                                          
   0x08048db3 <+27>:	call   0x8048fd8 <read_six_numbers>
   0x08048db8 <+32>:	xor    edi,edi                                  //j
   0x08048dba <+34>:	add    esp,0x10
   0x08048dbd <+37>:	lea    esi,[esi+0x0]	
   0x08048dc0 <+40>:	lea    eax,[ebp-0x18]
   0x08048dc3 <+43>:	mov    eax,DWORD PTR [eax+edi*4]                 eax=eax+j*4
   0x08048dc6 <+46>:	dec    eax                                       eax-- 
   0x08048dc7 <+47>:	cmp    eax,0x5                                  eax>5?    
   0x08048dca <+50>:	jbe    0x8048dd1 <phase_6+57>
   0x08048dcc <+52>:	call   0x80494fc <explode_bomb>
   0x08048dd1 <+57>:	lea    ebx,[edi+0x1]                             k=i+1   
   0x08048dd4 <+60>:	cmp    ebx,0x5                                   k>5--100
   0x08048dd7 <+63>:	jg     0x8048dfc <phase_6+100>
   0x08048dd9 <+65>:	lea    eax,[edi*4+0x0]
   0x08048de0 <+72>:	mov    DWORD PTR [ebp-0x38],eax
   0x08048de3 <+75>:	lea    esi,[ebp-0x18]
   0x08048de6 <+78>:	mov    edx,DWORD PTR [ebp-0x38]
   0x08048de9 <+81>:	mov    eax,DWORD PTR [edx+esi*1]
   0x08048dec <+84>:	cmp    eax,DWORD PTR [esi+ebx*4]
   0x08048def <+87>:	jne    0x8048df6 <phase_6+94>
   0x08048df1 <+89>:	call   0x80494fc <explode_bomb>
   0x08048df6 <+94>:	inc    ebx
   0x08048df7 <+95>:	cmp    ebx,0x5
   0x08048dfa <+98>:	jle    0x8048de6 <phase_6+78>
   0x08048dfc <+100>:	inc    edi                                      j++
   0x08048dfd <+101>:	cmp    edi,0x5                                  j<=5?move to 40:continue
   0x08048e00 <+104>:	jle    0x8048dc0 <phase_6+40>
   0x08048e02 <+106>:	xor    edi,edi
   0x08048e04 <+108>:	lea    ecx,[ebp-0x18]                           ecx=a[j]
   0x08048e07 <+111>:	lea    eax,[ebp-0x30]                           eax=
   0x08048e0a <+114>:	mov    DWORD PTR [ebp-0x3c],eax
---Type <return> to continue, or q <return> to quit---
   0x08048e0d <+117>:	lea    esi,[esi+0x0]
   0x08048e10 <+120>:	mov    esi,DWORD PTR [ebp-0x34]                 
   0x08048e13 <+123>:	mov    ebx,0x1                                 k=1
   0x08048e18 <+128>:	lea    eax,[edi*4+0x0]                         i=j*4
   0x08048e1f <+135>:	mov    edx,eax
   0x08048e21 <+137>:	cmp    ebx,DWORD PTR [eax+ecx*1]              if(k>=edx+ecx)?<160> 
   0x08048e24 <+140>:	jge    0x8048e38 <phase_6+160>
   0x08048e26 <+142>:	mov    eax,DWORD PTR [edx+ecx*1]               eax=i+ecx
   0x08048e29 <+145>:	lea    esi,[esi+eiz*1+0x0]         
   0x08048e30 <+152>:	mov    esi,DWORD PTR [esi+0x8]
   0x08048e33 <+155>:	inc    ebx                                     k++ 
   0x08048e34 <+156>:	cmp    ebx,eax                                 
   0x08048e36 <+158>:	jl     0x8048e30 <phase_6+152>
   0x08048e38 <+160>:	mov    edx,DWORD PTR [ebp-0x3c]
   0x08048e3b <+163>:	mov    DWORD PTR [edx+edi*4],esi
   0x08048e3e <+166>:	inc    edi
   0x08048e3f <+167>:	cmp    edi,0x5
   0x08048e42 <+170>:	jle    0x8048e10 <phase_6+120>
   0x08048e44 <+172>:	mov    esi,DWORD PTR [ebp-0x30]
   0x08048e47 <+175>:	mov    DWORD PTR [ebp-0x34],esi
   0x08048e4a <+178>:	mov    edi,0x1
   0x08048e4f <+183>:	lea    edx,[ebp-0x30]
   0x08048e52 <+186>:	mov    eax,DWORD PTR [edx+edi*4]
   0x08048e55 <+189>:	mov    DWORD PTR [esi+0x8],eax
   0x08048e58 <+192>:	mov    esi,eax
   0x08048e5a <+194>:	inc    edi
   0x08048e5b <+195>:	cmp    edi,0x5
   0x08048e5e <+198>:	jle    0x8048e52 <phase_6+186>
   0x08048e60 <+200>:	mov    DWORD PTR [esi+0x8],0x0
   0x08048e67 <+207>:	mov    esi,DWORD PTR [ebp-0x34]
   0x08048e6a <+210>:	xor    edi,edi
   0x08048e6c <+212>:	lea    esi,[esi+eiz*1+0x0]
   0x08048e70 <+216>:	mov    edx,DWORD PTR [esi+0x8]
   0x08048e73 <+219>:	mov    eax,DWORD PTR [esi]
   0x08048e75 <+221>:	cmp    eax,DWORD PTR [edx]
   0x08048e77 <+223>:	jge    0x8048e7e <phase_6+230>
   0x08048e79 <+225>:	call   0x80494fc <explode_bomb>
   0x08048e7e <+230>:	mov    esi,DWORD PTR [esi+0x8]
   0x08048e81 <+233>:	inc    edi
   0x08048e82 <+234>:	cmp    edi,0x4
   0x08048e85 <+237>:	jle    0x8048e70 <phase_6+216>
   0x08048e87 <+239>:	lea    esp,[ebp-0x58]
   0x08048e8a <+242>:	pop    ebx
   0x08048e8b <+243>:	pop    esi
---Type <return> to continue, or q <return> to quit---
   0x08048e8c <+244>:	pop    edi
   0x08048e8d <+245>:	mov    esp,ebp
   0x08048e8f <+247>:	pop    ebp
   0x08048e90 <+248>:	ret    
End of assembler dump.
`````
(gdb) 

 node1--   0xfd     //check if node1<node2
 node2--   0x2d5       
 ````
0x804b26c <node1>:	0x000000fd	0x00000001	0x0804b260  253
0x804b260 <node2>:	0x000002d5	0x00000002	0x0804b254  725
0x804b254 <node3>:	0x0000012d	0x00000003	0x0804b248  301
0x804b248 <node4>:	0x000003e5	0x00000004	0x0804b23c  997
0x804b23c <node5>:	0x000000d4	0x00000005	0x0804b230  212
0x804b230 <node6>:	0x000001b0	0x00000006	0x00000000  432
  0x8048e75 <phase_6+221>:	cmp    eax,DWORD PTR [edx]
   0x8048e77 <phase_6+223>:	jge    0x8048e7e <phase_6+230>

`````
writting in order:::
--------------------
*4 2 6 3 1 5 * ------password
Here the value of next node is compared with present node and writte
n in decending order


