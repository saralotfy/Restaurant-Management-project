# Restaurant Management System

This is a Restaurant Management System which is capable of taking order from customer. Firstly it shows a menu that we can choose the type of food from it (breakfast, dinner, appetizers or drinks), then a list of the types available in either of them appears with prices . we can select the meal we want with quantity then it will calculate the price and displays it. It allows us to choose more than one order from the same list and calculate the total price.


<div align="center">
<video  src="https://user-images.githubusercontent.com/65913853/209354993-e1b7a432-5c6d-4d13-bdb2-abf2f268c2d4.mp4" width="400" height="400" controls></video>
</div>

## Explanation of the code
 Firstly the code starts with :

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
DB - stands for Define Byte.

DW - stands for Define Word.

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

### Coloring
~~~
    MOV AH, 06h    
    XOR AL, AL     
    XOR CX, CX     
    MOV DX, 184fH  
    MOV BH, 01110000b    
    INT 10H
    
    MOV AH, 06h    
    XOR AL, AL     
    mov cx,0219h    
    MOV DX, 0239H  
    MOV BH, 11110000b
    INT 10H
~~~



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
If the user enters "1" the program will jump to the BREATFAST label and shows its menu , in case of "2" it will jump to the DINNER label,
in case of "3" it will jump to the APPETIZER label and shows its menu, in case of "4" it will jump to the DRINKS label and shows its menu. 
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
- then the program will call the function "calculate" to ask for the quantity and calculate the cost 
- label  REPEAT_BR  " isto ask for an another order from the user"
~~~
     Calculate: 
     
        EE7:
            LEA DX,M39              
            MOV AH,9
            INT 21H 
               
            MOV AH,1
            INT 21H
        
            CMP AL,48
            JA EE8
            
            
            LEA DX,M36
            MOV AH,9
            INT 21H 
                
                
            LEA DX,M37 
            MOV AH,9
            INT 21H
            
            loop EE7
            
         EE8:  
         
            CMP AL,58
            JB Break
            
            LEA DX,M36
            MOV AH,9
            INT 21H 
                
                
            LEA DX,M37 
            MOV AH,9
            INT 21H
            
            loop EE7
        
        Break:
          
            SUB AL,48
            mov ah,00          
            
            MUL BL
            
            ADD PRC,AX
            
            ret
~~~

- firstly the program asks for the quantity 

- then check if the value that user entered is a number and higher than '0' by comparing the input ascii with the ascii codes lower than that for '1' and higher than that for '9'. if this condition isn't satisfied, it will ask for the quantity again as shown

<img src="https://user-images.githubusercontent.com/66569142/209399753-2ee3700d-059e-4750-add1-f2ada9bc605f.png" width="50%">
 
 
 
- then calculate the total price and store it in 'PRC' variable to add to it the total price of the next choice  

- then return to the price label and jump to REPEAT_BR label 

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
- the user must enter 'y' or 'n' only, otherwise the program will repeat the question as shown before.  
- if the user enter "y" or "Y", the label EE2 will be repeated to take the order from the user

the output will be as follow :

<img src="https://user-images.githubusercontent.com/66569142/209400248-1d8d8679-5449-47fa-af04-9d40570eac73.png" width="50%">



- if the user enter "n" or "N", the program jumps to the print function 'PRINTE' and the total price will be printed
~~~
    PRINTE:    
        
        mov bx,64h
        
        MOV AX,PRC
        
        div bl
        
        mov SN1,ah
        mov SN2,al
        
        LEA DX,M40              
        MOV AH,9
        INT 21H
        
        mov al,SN2
        
        mov bh,0ah
        
        mov cx,2h

        print:     
        
            mov bh,0ah
            
            mov ah,0
            div bh
            
            
            
            MOV DL,al
            mov dh,ah
            
            
            
            MOV AH,2
            add dl,48
            INT 21H
             
            
            MOV AH,2
            MOV DL,dh
            mov dh,0
            
            add dl,48
            
            INT 21H
             
            mov al,SN1
            
            
            loop print 
        
        ;FOR LE PRINT
        
        LEA DX,MU
        MOV AH,9
        INT 21H 
         
        EE6:
          
            ;GO BACK TO the MAIN MENU 
            
            LEA DX,M41
            MOV AH,9
            INT 21H 
              
            ;EXIT 
            
            LEA DX,M42
            MOV AH,9
            INT 21H
            
            LEA DX,M2
            MOV AH,9
            INT 21H 
            
            MOV AH,1
            INT 21H          
            SUB AL,48
            
            
            
            CMP AL,1
            JE TOP
            
            CMP AL,2
            JE EXIT 
            
            
            LEA DX,M36
            MOV AH,9
            INT 21H 
                    
                    
            LEA DX,M37 
            MOV AH,9
            INT 21H 
            loop EE6

~~~

- the way this function works is dividing the value to isolate each digit and print it by dividing the number by 100 and then by 10 assuming that the value contains up to 4 digits
- the value of PRC is put in AX regester to do the operations on it. the value at AX is divided by 100 and as default, the result is stored at AL and the reminder at AH, then these values are stored in two variables and return them back again to work on each one alone as explained and ensure that they won't be affected when printing the string "total price:".
- firstly, we will work on the result of the previous division and divide it by 10, then add 48 to the result to be the ascii code of the desired number and do that also to the reminder.
- secondly, the reminder of the first division is returned back to AL and repeat the loop "print".
- After that the user is asked if he want to return to the main menu or exit. if he entered '2', it jumps to the exit label to end the program   

the output will be as follow :

<img src="https://user-images.githubusercontent.com/66569142/209398815-c42ee795-14ee-42c8-8aa4-b445a308c948.png" width="50%">



#### NOTE:
- the steps of code in breakfast is applied also in dinner,drinks and Appetizer

### link of the project :    

[GITHUB CODE](https://github.com/saralotfy/Restaurant-Management-project/blob/main/Restaurant%20Management%20system) - Restaurant management project

