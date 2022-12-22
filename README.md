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
