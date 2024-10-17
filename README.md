# Ex-3-RECOGNITION-OF-A-VALID-ARITHMETIC-EXPRESSION-THAT-USES-OPERATOR-AND-USING-YACC
# Date: 18-0-10-2024
# AIM
To write a yacc program to recognize a valid arithmetic expression that uses operator +,- ,* and /.
# ALGORITHM
1.	Start the program.
2.	Write a program in the vi editor and save it with .l extension.
3.	In the lex program, write the translation rules for the operators =,+,-,*,/ and for the identifier.
4.	Write a program in the vi editor and save it with .y extension.
5.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l
6.	Compile the yacc program with yacc compiler to produce output file as y.tab.c. eg $ yacc –d arith_id.y
7.	Compile these with the C compiler as gcc lex.yy.c y.tab.c
8.	Enter an arithmetic expression as input and the tokens are identified as output.
# PROGRAM
## arth.l
```
%{ 
/* This LEX program returns the tokens for the expression */ 
#include "y.tab.h" 
%} 
%% 
"=" {printf("\n Operator is EQUAL");} 
"+" {printf("\n Operator is PLUS");} 
"-" {printf("\n Operator is MINUS");} 
"/" {printf("\n Operator is DIVISION");} 
"*" {printf("\n Operator is MULTIPLICATION");} 
[a-zA-Z]*[0-9]* { 
printf("\n Identifier is %s",yytext); 
return ID; } 
. return yytext[0]; 
\n return 0; 
%% 
int yywrap() 
{ 
return 1; 
} 
```
## arth.y
```
%{ 
#include <stdio.h> 
/* This YACC program is for recognizing the Expression */ 
%} 
%token A ID 
%% 
statement: A'='E 
| E { 
printf("\n Valid arithmetic expression"); 
$$=$1; 
} 
; 
  E: E'+'ID 
| E'-'ID 
| E'*'ID 
| E'/'ID 
| ID 
; 
%% 
extern FILE*yyin; 
int main() { 
do { 
yyparse(); 
}while(!feof(yyin)); } 
yyerror(char*s) 
{ fprintf(stderr, "Error: %s\n",s);
}
```
# OUTPUT
![alt text](Output.png)
# RESULT
A YACC program to recognize a valid arithmetic expression that uses operator +,-,* and / is executed successfully and the output is verified.
