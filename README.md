# Ex-5-RECOGNITION-OF-THE-GRAMMAR-anb-where-n-10-USING-YACC
RECOGNITION OF THE GRAMMAR(anb where n>=10) USING YACC
# Date:12/03/26
# Reg no : 212224040365
# Aim:
To write a YACC program to recognize the grammar anb where n>=10.
# ALGORITHM
1.	Start the program.
2.	Write a program in the vi editor and save it with .l extension.
3.	In the lex program, write the translation rules for the variables a and b.
4.	Write a program in the vi editor and save it with .y extension.
5.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l
6.	Compile the yacc program with yacc compiler to produce output file as y.tab.c. eg $ yacc –d arith_id.y
7.	Compile these with the C compiler as gcc lex.yy.c y.tab.c
8.	Enter a string as input and it is identified as valid or invalid.
# PROGRAM:
### l file
```
%{
#include "y.tab.h"
%}

%%
a   { return A; }
b   { return B; }
\n  { return '\n'; }
.   { return yytext[0]; }
%%

int yywrap() {
    return 1;
}
```
### y file
```
%{
#include <stdio.h>
#include <stdlib.h>
int count = 0;  // to count number of a's
%}

%token A B

%%
start:
    sequence B '\n' {
        if (count >= 10) {
            printf("Valid string: %d a's followed by b\n", count);
        } else {
            printf("Invalid: Less than 10 a's\n");
        }
        count = 0; // reset for next input
    }
    ;

sequence:
    A { count++; }
  | sequence A { count++; }
  ;
%%

int main() {
    printf("Enter a string (aⁿb where n >= 10):\n");
    return yyparse();
}

void yyerror(const char *msg) {
    printf("Syntax error: %s\n", msg);
}
```
# OUTPUT
<img width="510" height="459" alt="Screenshot 2026-03-12 204214" src="https://github.com/user-attachments/assets/ab09f7dd-d170-41d9-b2bb-c1ab1dd7f493" />


# RESULT
The YACC program to recognize the grammar anb where n>=10 is executed successfully and the output is verified.
