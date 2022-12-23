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
   
   <img src="https://user-images.githubusercontent.com/65913853/209343475-a8be985d-9295-49ce-8f1b-d1ffca671e05.png" width="50%">
   
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

<img src ="https://user-images.githubusercontent.com/65913853/209344186-b1cd27df-2a5c-46e6-82f3-4f03e7480a9d.png" width="50%">

This is implemented using loop :

~~~
 EE1:
 
 loop EE1
~~~
when the user enters "1" the menu of the breakfast will appear .

this menu  was written as below :
~~~
BREAKFAST:
   
        MOV PRC,0 
        LEA DX,M7    
        MOV AH,9h
        INT 21H
        
        LEA DX,NEWLINE 
        MOV AH,9h
        INT 21H
        
        LEA DX,MF2
        MOV AH,9h
        INT 21H
               
        LEA DX,MF2
        MOV AH,9h
        INT 21H
              
        LEA DX,M8    
        MOV AH,9h
        INT 21H 
                
        LEA DX,M9  
        MOV AH,9h
        INT 21H
        
        LEA DX,M10
        MOV AH,9h          
        INT 21H 
        
        LEA DX,M11
        MOV AH,9h           
        INT 21H
                
        LEA DX,M12         
        MOV AH,9h
        INT 21H
               
        LEA DX,M13     
        MOV AH,9h
        INT 21H 
                        
        LEA DX,M14
        MOV AH,9h           
        INT 21H
                                
        LEA DX,M15        
        MOV AH,9h
        INT 21H 
        
        LEA DX,M16         
        MOV AH,9h
        INT 21H
               
        LEA DX,MF2
        MOV AH,9h
        INT 21H
        
        LEA DX,MF2
        MOV AH,9h
        INT 21H
   ~~~
        
this label will print the menu of the breakfast:

<img src="https://user-images.githubusercontent.com/65913853/209344373-f6b04685-5868-45a6-acb1-ec167c87aadb.png" width="50%">

~~~
 EE2:
        
            LEA DX,M38              
            MOV AH,9h
            INT 21H 
            MOV AH,1h
            INT 21H
            MOV BL,AL
            SUB BL,48 
            
            CMP BL,1
            JE TEN-B
            
            CMP BL,2
            JE FIFTEEN-B
            
            CMP BL,3
            JE TWINTY-B 
            
            CMP BL,4
            JE TWINTY-B
            
            CMP BL,5
            JE THIRTY-B
            
            CMP BL,6
            JE FOURTY-B
            
            CMP BL,7
            JE FIFTEEN-B
            
            CMP BL,8
            JE FIFTY-B 
            
            CMP BL,9
            JE SIXTY-B
             

~~~
 


If the user enters any character from "1" to "9", the program will jump to the price label of this order 

~~~
          TEN-B:
            
         mov BL,0Ah
                
         call Calculate             
         
         JMP REPEAT_BR
~~~                        

- mov BL,0Ah   " the price of the order is put in BL register"
- then the program will call the function "calculate" to ask for the quantity 
- label  REPEAT_BR  "to ask for another order from the user"
~~~
      Calculate: 
     
        LEA DX,M39              
        MOV AH,9
        INT 21H 
           
        MOV AH,1
        INT 21H
        SUB AL,48
        mov ah,00          
        
        MUL BL
        
        ADD PRC,AX
        
        ret
~~~

- first the program ask for the quantity 

- then calculate the price and store it in PRC variable 

- then return to  REPEAT_BR label 

~~~
 REPEAT_BR:
        
            LEA DX,M44
            MOV AH,9h
            INT 21H
            
            MOV AH,1h
            INT 21H
            
            CMP AL,'n'
            JE PRINTE
           
            CMP AL,'N'
            JE PRINTE
            
            CMP AL,'y'
            JE EE2
           
            CMP AL,'Y'
            JE EE2
            
            LEA DX,M36
            MOV AH,9
            INT 21H 
                    
                    
            LEA DX,M37 
            MOV AH,9
            INT 21H
            
            loop REPEAT_BR    
 ~~~
- the program ask the user if he need another order 
- if the user enter "n" or "N" then the total price will be print
- if the user enter "y" or "Y" then label IEE will be repeated TO take the order from the user
 

- the output for this function will be as follow :

<img src="https://user-images.githubusercontent.com/65913853/209344745-e3eefb3e-294a-421b-a371-783277791446.png" width="50%">


IF the user enters any character except these characters ,the program will show this until he enters a right character :


<img src="https://user-images.githubusercontent.com/65913853/209345031-c711edb3-68f4-4a19-b9ef-0bd28ef485aa.png" width="50%">

### NOTE

- the steps of code in breakfast is applied also in dinner,drinks and Appetizer



