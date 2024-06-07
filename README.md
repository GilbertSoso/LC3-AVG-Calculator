# LC3-AVG-Calculator
An LC3 Program that takes 5 numbers between 0 and 100, and displays the biggest number, smallest number, and average








CIS-11 Project Documentation Template

Team Push N Pop
Tawny Hoemke, Gilbert Sosa
Test Score Calculator
5/19/2024

Advisor: Kasey Nguyen, PhD





Part I – Application Overview 
Objectives 
Create an LC-3 program that displays the minimum, maximum and average grade of 5 test scores and display the letter grade associated with the test scores. 
		Input: User is prompted to input the test scores.
Output: Display maximum, minimum, average scores and letter grade equivalent (0 – 50 = F, 60 – 69 = D, 70 – 79 = C, 80 – 89 = B, 90 – 100 = A) on the console.

Why are we doing this?	

What business objectives of the company will this project help achieve? This project will help simplify the workflow of teachers, professors, and any personnel that is required to enter a grade.
Why are we doing this project now? What will happen if we do it later? What if we do not do it at all? We are doing this project to build our skills in assembly/ LC3.If we do this later or not at all, our grade would be negatively affected.

Who will benefit from this project? Do the people who will benefit from it consider it the most important improvement that can possibly be made at this time? Should we be doing a different project instead? Professors and teachers will benefit from this project. This is an important improvement because it minimizes their workload by automating the processes for calculating the average,  minimum, and maximum test scores.


Business Process

Previously, professors would have to manually calculate averages for lecture halls filled with hundreds of students, after having to grade each of their tests.
With this program, professors will no longer have to worry about crunching those numbers. By simply inputting numbers into this calculator, an average will immediately be produced.

User Roles and Responsibilities

Professors must first grade their class' test. After having them all graded, they are to input their values into this calculator.

Terminology

LC3: Little Computer 3
		Assembly: A low level program
		Array: A collection of values
		ASCII: American Standard Code for Information Interchange
		Binary: A decimal value
		Register: A storage location
		Pointer: Stores memory address location
		


Part II – Functional Requirements 








	
	

Statement of Functionality 

Prompt the user to input five grades. Each 3-digit grade will be inputted one digit at a time. 
The program converts each digit from the ASCII character value to its appropriate binary value.
Once converted, the first digit of the grade is multiplied by 100, and the second digit is multiplied by 10.
After this multiplication, all three digits are added together and stored into a register.
The grade is then placed into an array. Each time a grade is placed into the array, a pointer is used to move to the next location of the array.
The program finds the maximum, minimum, average and its associated letter grade.
Maximum, minimum, average and associated grades are displayed.


Scope
PROMPT1: Gives direction on how to input digits
PROMPT2: Prompts input of each digit of grade
TSCORES: Array
\MULT: performs appropriate multiplication on first two digits.
CHECKMIN: Determines minimum grade 
CHECKMAX: Determines maximum grade
AVGSUM: Determines average grade
DISPLAYALL: Outputs minimum, maximum, average, and letter grades 
Technical Requirements
Contain appropriate addresses
Display minimum, maximum, average, and associated letter grades on console
Use appropriate comments and labels
Contain appropriate instructions for arithmetic, data movement and conditional operations
Comprise of two or more subroutines, and implement subroutine calls
Use branching for control: conditional and iterative
Manage overflow and storage allocation
Manage stack
Include save-restore operations
Include pointer
Implement ASCII conversion operations
Use appropriate system call directives
Test program


Documenting Requests for Enhancements
There does come a time when the requirements for the initial release of your application are frozen. Usually, it happens after the system acceptance test which is the last chance for the users to lobby for some changes to be introduced in the upcoming release.
Currently, you need to begin maintaining the list of requested enhancements. Below is a template for tracking requests for enhancements.
Date
Enhancement
Requested by
Notes
Priority
Release No/ Status



Part III – Appendices

Flow chart or pseudo-code.

Include branching, iteration, subroutines/functions in flowchart or pseudocode. 


Code is to implement:
Array with each digit; every 3 elements is one test score
Pointer pointing to array elements
Stack may be used in place of array; appropriate PUSH POP subroutines will be made

Input/ Output

LEA R0, IN_PROMPT		;Output prompt to enter in test score
PUTS					;Display PROMPT
LEA R1 TSCORES 			;R1 Pointer for test scores array
AND R5, R5, #0			;R5 is loop counter

PROMT LOOP {
PROMPTING USER

;//////////////////////////////////////////////////////////////////
;//	Getting Digits		//
;/////////////////////////////////////////////////////////////////

;//Let R0 be used for prompting user and accepting input
;//Let R1, R2, and R3 be used for multiplication
;//R2 will be used to multiply digits 1 and 2 by 100 and 10, respectively
;//Get digit1, multiply by 100
LEA R0, PROMPT1
GETC		;//Get ASCII Value (Character)
ST R0, DIGIT1		;//R0 = ASCII for DIGIT1 

R0 -= 48		;//Convert to Binary
ADD R1, R0, #0	;//R1 = Digit 1

R2 = 100		;//Multiple ADD lines
JSR MULT		;//R1 * R2 = R3
R4 += R3

AND R0, R0, #0	;//Clear R0
AND R2, R2, #0	;//Clear R2

;//Get digit2, multiply by 10, add to R3
LEA R0, PROMT2
GETC
ST R0, DIGIT2	
R0 -= 48
ADD R1, R0, #0

R2 = 10
JSR MULT
R4 += R3

AND R0, R0, #0
AND R2, R2, #0
	
;//Get digit3

LEA R0, PROMT3
GETC
ST R0, DIGIT3		;//Store
R0 -= 48		;//Convert to Binary
ADD R1, R0, #0	;R1 = Digit3

R3 += R1		;//R3 = Test Score


;//////////////////////////////////////////////////////////////////
;//	Checking MIN MAX	//
;//////////////////////////////////////////////////////////////////

LEA R1,  MIN
JSR CHECKMIN
LEA R1, MAX
JSR CHECKMAX

R5--
if (R5 = 0)
     BRz EXITLOOP	;//May have different name
}

TSCORES[R5] = R3

R5++
if (R5 = 5)
 BR EXITLOOP	;//May have different name
}

;/////////////////////////////////////////////////////////////////////////////
;//	Average Summing Loop		//
;/////////////////////////////////////////////////////////////////////////////

R1 = &TSCORES1	;//Pointer points at address of first array element
R2 = 0		;//R2 is a counter
AVGSUM{

R3+= *R1		;// R3 = Sum

R1 += (Element size)
R2++
if (R2 != 5)
      BR AVGSUM	;//Continue loop

}

JSR DIV	;//R4 = R3 / R2 = SUM/5
ST R4, AVG

;//////////////////////////////////////////////////////////////////
;//	Display values		//
;//////////////////////////////////////////////////////////////////

DISPLAYALL{

LEA R0, DISPLAYMIN
PUTS
LEA R0, TSCORES[Min element]
PUTS
R3 = MIN
JSR GIVELETTER

LEA R0, DISPLAYMAX
PUTS
LEA R0, TSCORES[Max element]
PUTS
R3 = MAX
JSR GIVELETTER

LEA R0, DISPLAYAVG
PUTS

AVGTOASCII
LEA R0, AVGASCII
PUTS
R3 = AVG
JSR GIVELETTER
}





AVGTOASCII{
First Digit:
99 / 100
However many times 100 goes into 99:
DIGIT1 = 0 + 48

Second Digit: 
99/10
Digit2 = 9 + 48

Digit 3 = Remainder + 48 

RET
}



IN_PROMPT		.STRINGZ “Enter test score 1 digit at a time. If score is not 100, enter 0 
for first the digit.”
PROMPT1		.STRINGZ “1st digit: “
PROMPT2		.STRINGZ “2nd digit: “
PROMPT3		.STRINGZ “3rd digit: “




























SubRoutines


;//Let R3 have your inputted grade
;//Let R1 be pointer to current minimum MIN
CHECKMIN
	;//Save OG values of R2, R1
	ST R3, SAVER3
	ST R1, SAVER1		
	
	if (R3 < *R1)
	   ST R3, MIN
	   
	;///Restore values of R3, R4
	LD R3, SAVER3
	LD R1, SAVER1
	
	RET

	
;//Let R3 have your inputted grade
;//Let R1 be current maximum MAX
CHECKMAX
	;//Save OG values of R3, R1
	ST R3, SAVER3
	ST R1, SAVER4		
	
	if (R3 > *R4)
	   ST R3, MAX
	   
	;///Restore values of R3, R4
	LD R3, SAVERR3
	LD R4, SAVERR4

	RET


DIV	;R4 = R3/R2, R5 = R3%R2
	ST R2, SAVE1	
	ST R3, SAVE2
	AND R4, R4, x0
	NOT R2, R2
	ADD R2, R2, #1
	
	DLOOP
	AND R5, R5, x0
	ADD R4, R4, #1
	ADD R5, R3, x0
	ADD R3, R3, R2
	BRzp DLOOP
	ADD R4, R4, #-1
	RET









;//Let R3 contain grade
;//Let R0 contain appropriate letter grade
GIVELETTER
	ST R0, SAVER0
	ST R3, SAVER3
	

	if (R3 - 59 <= 0)
    		R0 = ASCII for 'F'
    		Display R0	
  	else if (R3 - 69 <= 0)
    		R0 = ASCII for 'D'
    		Display R0
  	else if (R3 - 79 <= 0)
    		R0 = ASCII for 'C'
    		Display R0
	  else if (R3 - 89 <= 0)
	    	R0 = ASCII for 'B'
	    	Display R0
	  else
	    	R0 = ASCII for 'A'
	    	Display R0
	
	LD R0, SAVER0
	ST R3, SAVER	
	RET

;//R1 * R2 = R3
MULT	
	;//Save register values
	ST R1, SAVER1
	ST R2, SAVER2
	ST R3, SAVER3

	AND R3, R3, #0
	MLOOP
	ADD R3, R3, R1
	ADD R2, R2, #-1
	BRp MLOOP

	LD R1, SAVER1
	LD R2, SAVER2
	LD R3, SAVER3
	RE





;/////////////////////////////////////////////////////////
;//							//
;//		 Input a 3 digit number			//
;//	 Converts to Decimal, and back to ASCII		//
;//							//
;//	      Requires MULT, DIV Subroutine		//
;//							//
;/////////////////////////////////////////////////////////




.ORIG X3000

;/////////////////////////////////////////////////////////////////////////
;//	Prompt user for 3 digits. If first digit is 1, assume 100	//
;/////////////////////////////////////////////////////////////////////////

;//Get Digit 1; If it is 1, assume 100
LEA R0, PROMPT
PUTS
LEA R0, PROMPT1
PUTS
GETC
;//Convert ASCII to Decimal
ADD R1, R0, X0		;//R1 = Digit 1 (ASCII)
ADD R1, R1, #-16
ADD R1, R1, #-16
ADD R1, R1, #-16	;//R1 = Digit 1 (Decimal)

;//Verify; if digit1 - 1 is positive, then digit1 > 1
ADD R2, R0, #-1		;//R2 = digit1 - 1.
BRp ERROR
;//If digit 1 was 1 (that is, if R2 = 1 - 1 = 0), assume input will be 100
BRz SKIP

;//Get Digit 2
LEA R0, PROMPT2
PUTS
GETC
;//Convert ASCII to Decimal
ADD R1, R0, X0		;//R1 = Digit 2 (ASCII)
ADD R1, R1, #-16
ADD R1, R1, #-16
ADD R1, R1, #-16	;//R1 = Digit 2 (Decimal)

;//Multiply by 10, since Digit 2 is in ten's place
AND R2, R2, #0
ADD R2, R2, #10
JSR MULT			;//R1 * R2 = R3
ADD R4, R3, #0		;//R4 = Digit2 * 10


;//Get Digit 3
LEA R0, PROMPT3
PUTS
GETC
;//Convert ASCII to Decimal
ADD R1, R0, X0		;//R1 = Digit 3 (ASCII)
ADD R1, R1, #-16
ADD R1, R1, #-16
ADD R1, R1, #-16	;//R1 = Digit 3 (Decimal)

;//Get full number by adding digit3 to R4
ADD R4, R4, R1

BR DECTOASCII

SKIP			
;//Tell user program is assuming 100
LEA R0, HUNDRED
PUTS

;//Multiply R1 by 100
AND R2, R2, #0		
ADD R2, R2, #15
ADD R2, R2, #15
ADD R2, R2, #15
ADD R2, R2, #15
ADD R2, R2, #15
ADD R2, R2, #15
ADD R2, R2, #10
JSR MULT			;//R1 * R2 = R3, R3 is full number
AND R4, R4, #0		;//Ensure R4 is 0 for next conversion





;/////////////////////////////////////////////////////////////////////////
;//			Convert our number to ASCII			//
;/////////////////////////////////////////////////////////////////////////

DECTOASCII
;//Convert Digit 1. If 1, assume other digits are 0
;//ADD R5, R4, #0		;//R5 holds full number for future use
ADD R3, R4, #0		;//R3 = Full Number
AND R2, R2, #0		
ADD R2, R2, #15
ADD R2, R2, #15
ADD R2, R2, #15
ADD R2, R2, #15
ADD R2, R2, #15
ADD R2, R2, #15
ADD R2, R2, #10		;//R2 = 100

JSR DIV 			;//R3 / R2 = R4, R3 saved into SAVE2
LD R3, SAVE2		
ST R4, DIGIT1		;//Digit1 now holds first digit

;//Check if first digit is 100
ADD R4, R4, #-1		
BRz SKIP1

;//Convert Digit 2

;//ADD R3, R5, #0		;//R3 = Full Number
AND R2, R2, #0		
ADD R2, R2, #10		;//R2 = 10

JSR DIV			;//R3 / R2 = R4. R5 holds remainder
LD R3, SAVE2
ST R4, DIGIT2		;//DIGIT2 now holds second digit
ST R5, DIGIT3		;//DIGIT3 now holds third digit
BR RESULT


SKIP1
AND R5, R5, #0
ST R5, DIGIT2
ST R5, DIGIT3
BR RESULT

RESULT
LEA R0, RESMSG
PUTS
LEA R0, DIGIT1
PUTS
ADD R0, R0, x1
PUTS
ADD R0, R0, x1
PUTS
HALT





;//	Strings & Labels	//
PROMPT	.STRINGZ "Enter a 3 digit number (0-100). Entering a 1 assumes 100.\n"
PROMPT1	.STRINGZ "Digit 1: "
PROMPT2 .STRINGZ "Digit 2: "
PROMPT3 .STRINGZ "Digit 3: "
HUNDRED	.STRINGZ "Assuming 100... "
ERROR	.STRINGZ "Error! Invalid Input."
RESMSG	.STRINGZ "Your number is: "

DIGIT1	.FILL X3100
DIGIT2	.FILL X3101
DIGIT3	.FILL X3102




;//R1 * R2 = R3
MULT	
	;//Save register values
	;ST R1, SAVER1
	;ST R2, SAVER2
	;ST R3, SAVER3

	AND R3, R3, #0
	MLOOP
	ADD R3, R3, R1
	ADD R2, R2, #-1
	BRp MLOOP

	;LD R1, SAVER1
	;LD R2, SAVER2
	;LD R3, SAVER3
	RET

;// R3 / R2 = R4, R3 % R2 = R5
DIV	
	ST R2, SAVE1	
	ST R3, SAVE2
	AND R4, R4, x0
	NOT R2, R2
	ADD R2, R2, #1
	
	DLOOP
	AND R5, R5, x0
	ADD R4, R4, #1
	ADD R5, R3, x0
	ADD R3, R3, R2
	BRzp DLOOP
	ADD R4, R4, #-1
	RET
	
SAVE1	.FILL x0
SAVE2	.FILL x0

.END
