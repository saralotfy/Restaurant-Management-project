# Restaurant Management System

This is a Restaurant Management System which is capable of taking order from customer. Firstly it shows a menu that we can choose the type of food from it (breakfast, dinner, appetizers or drinks), then a list of the types available in either of them appears with prices . we can select the meal we want with quantity then it will calculate the price and displays it. It allows us to choose more than one order from the same list and calculate the total price.

## Explanation of the code
 Firstly the code start with :

~~~
org 100h
~~~
The command ORG is the ORiGinate command which sets the start of the assembled code. ORG 100h means originate this block of
assembled code at the location 100 hexidecmal.
~~~
.model small
~~~
This command tells the assembler that you intend to use the small memory model - one code segment, one data segment and one stack segment - and the values of the segment registers are never changed.
~~~
.stack 1000h
~~~
This command reserves 1000h bytes for stack.
~~~
.DATA
~~~
The data section is used for declaring initialized data or constants. This data does not change at runtime.
### Variables Definition
Syntax for a variable declaration:
~~~
name DB value
(or)
name DW value
~~~
DB - stays for Define Byte.

DW - stays for Define Word.

For examble:
~~~
M1 DB 10,13,10,13,9,9,9,32,'>>>>Welcome to Our Restaurant<<<<$',10,13
~~~
The variable name is :M1

Data type : Byte

The value : the string '>>>>Welcome to Our Restaurant<<<<'
~~~
'10' is the ASCII control code for line feed while '13' is the code for carriage return.
The line feed control code moves the cursor to the next line, the carriage return code moves the cursor to the start of line. 
Together the two control codes move the cursor to the start of the next line.
'9' is the ASCII control code for Horizontal Tab
'32' is the ASCII control code for Space
~~~

All variables in the program are defined by the same way.

~~~
SN1 DB ?    
SN2 DB ?
PRC DW ? 
~~~
The "?" symbol is used  for variables that are not initialized. 
~~~
.CODE
MAIN PROC
    MOV AX,@DATA
    MOV DS,AX
~~~
 "MOV AX,@DATA" is the first line of code that gets run. @DATA is a variable that holds the value of the location in memory where the data segment is. 
 It moves the memory location of @DATA into the AX register."MOV DS,AX" will then set that memory location in the data segment register DS .
 
### To print string :
-Create a string , the string must be terminated by ‘$’ sign.

-Load the effective address of the string in dx using LEA command.

-Print the string by calling the interrupt with 9H in AH.

 ~~~ 
  TOP:
  
    LEA DX,M1
    MOV AH,9h
    INT 21H
    
    LEA DX,NEWLINE 
    MOV AH,9h
    INT 21H
    
    LEA DX,MF1
    MOV AH,9h
    INT 21H
       
    LEA DX,MF1
    MOV AH,9h
    INT 21H  
        
    LEA DX,M3
    MOV AH,9h
    INT 21H
    
    LEA DX,M4
    MOV AH,9h
    INT 21H
    
    LEA DX,M5
    MOV AH,9h
    INT 21H
    
    LEA DX,M6
    MOV AH,9h
    INT 21H
       
    LEA DX,MF1
    MOV AH,9h
    INT 21H
    
    LEA DX,MF1
    MOV AH,9h
    INT 21H
    
     LEA DX,NEWLINE
     MOV AH,9h
     INT 21H
     
     LEA DX,M2
     MOV AH,9h
     INT 21H    
 ~~~
   
   This label will print the menu that will first appear when the program is run as follows :
   
   <img src="https://user-images.githubusercontent.com/66350581/209178345-8f4e7fff-79fc-4aea-afcc-69aabae7cdff.png" width="50%">
   
To get an input from the user we use this instructions:  
 ~~~
    MOV AH,1h
    INT 21H
    MOV BH,AL
    SUB BH,48
 ~~~ 
 
 ~~~
  CMP BH,1
  JE BREATFAST
  CMP BH,2
  JE DINNER
  CMP BH,3
  JE APPETIZER
  CMP BH,4
  JE DRINKS
  LEA DX,M36
  MOV AH,9
  INT 21H      
  LEA DX,M37 
  MOV AH,9
  INT 21H
~~~
If the user enters "1" the program will jump to the BREATFAST label and show its menu , in case of "2" it will jump to the DINNER label,
in case of "3" it will jump to the APPETIZER label and show its menu, in case of "4" it will jump to the DRINKS label and show its menu. 
IF the user enters any character except these characters ,the program will show this until he enters a right character :

<img src ="https://user-images.githubusercontent.com/66350581/209186062-d3ffdbae-0393-496b-88be-a3f310a13093.png" width="50%">

This is implemented using loop :

~~~
 EE1:
 
 loop EE1
~~~


 
