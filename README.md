
# RO-ARM32-Assembler-Guide

This repository contains code modules for basic operations in ARM32 assembly, including handling large variables, bit manipulation, control flow (if-else, loops), array manipulation, sorting, subprograms, recursion, and file operations using SWI.

## Table of Contents

- [LDR, STR Large Variables](#ldr-str-large-variables)
- [Bit Manipulation](#bit-manipulation)
- [If-Else](#if-else)
- [Loop](#loop)
  - [While Loop](#while-loop)
  - [For Loop](#for-loop)
- [Array and Sorting](#array-and-sorting)
  - [Array](#array)
  - [Sorting](#sorting)
- [Subprograms](#subprograms)
  - [Simple Recursion](#simple-recursion)
- [File Operations Using SWI](#file-operations-using-swi)

## LDR, STR Large Variables

*(Section to be completed as needed)*

## Bit Manipulation

*(Section to be completed as needed)*

## If-Else

```assembly
@ IF statement
cmp r0, r1        @ Compare r0 with r1
bne IF            @ Branch to IF if they are not equal
...               @ Code if r0 == r1
IF:
...               @ Code if r0 != r1

@ IF-ELSE statement
cmp r0, r1        @ Compare r0 with r1
bne IF            @ Branch to IF if they are not equal
...               @ Code if r0 == r1
b ELSE            @ Branch to ELSE
IF:
...               @ Code if r0 != r1
ELSE:
...               @ Code for else condition
```

## Loop

### While Loop

```assembly
@ WHILE loop
@ Initial setup code
...

WHILE:
cmp r0, #x        @ Compare r0 with x
beq DONE          @ Break loop if r0 == x
...               @ Loop body
b WHILE           @ Jump back to start of WHILE loop

DONE:
```

### For Loop

```assembly
@ FOR loop
@ Initial setup code
...
mov r0, #0        @ Initialize counter to 0

FOR:
cmp r0, #x        @ Compare counter with x (number of iterations)
beq DONE          @ Break loop if counter == x
...               @ Loop body
add r0, r0, #1    @ Increment counter
b FOR             @ Jump back to start of FOR loop

DONE:
```

## Array and Sorting

### Array

```assembly
@ Array initialization and filling loop
@ Initial setup code
mov r0, #adr      @ Load address of the first element into r0
mov r1, #0        @ Initialize array pointer to 0

LOOP:
cmp r1, #(y * 4)  @ Compare array pointer with length of array in bytes
bge DONE          @ Break loop if r1 >= length of array
...               @ Code to fill array
add r1, r1, #4    @ Move array pointer to next element (4 bytes per element)
str rX, [r0, r1]  @ Store value of rX into the array
b LOOP            @ Jump back to start of LOOP

DONE:
```

### Sorting

```assembly
@ Sorting algorithm loop
@ Initial setup code
mov r0, #adr      @ Load address of the first element into r0
...

LOOP:
cmp r1, #(y * 4)  @ Compare array pointer with length of array in bytes
bge DONE          @ Break loop if r1 >= length of array
...               @ Sorting computation
add r1, r1, #4    @ Move array pointer to next element (4 bytes per element)
ldr rX, [r0, r1]  @ Load value from array into rX for computation
b LOOP            @ Jump back to start of LOOP

DONE:
```

## Subprograms

### Simple Recursion

```assembly
@ Simple recursion example
main:
mov rX, #X        @ Move initial value into rX
...
bl RECURSION      @ Branch with link to RECURSION subroutine

RECURSION:
sub sp, sp, #(X+4)@ Allocate space on stack
str rX, [sp, #X]  @ Push rX onto stack
...
str lr, [sp, #(X+4)] @ Save link register on stack
...
cmp rX, #0        @ Check for recursive break condition
beq BREAK         @ Break recursion if condition is met
bl RECURSION      @ Recursive call

END:
ldr rX, [sp, #X]  @ Pop rX from stack
ldr lr, [sp, #(X+4)] @ Restore link register
add sp, sp, #(X+4)@ Deallocate stack space
bx lr             @ Return from subroutine

BREAK:
...               @ Code to execute when recursion ends
b END             @ Branch to end
```

## File Operations Using SWI

### File Handling with SWI

In ARM assembly, file operations can be implemented using software interrupts (SWI). The `SWI{cond} <immediate_24_bit>` instruction invokes a software interrupt, which can be used to perform various system calls, including file handling. Below are examples of how to use SWI for basic file operations.

#### Opening a File

```assembly
@ Open a file
mov r0, #filename     @ Load the address of the filename into r0
mov r1, #mode         @ Load the mode (e.g., read, write) into r1
swi 0x66              @ Software interrupt to open file
                      @ File descriptor returned in r0
```

#### Reading from a File

```assembly
@ Read from a file
mov r0, #file_desc    @ Load the file descriptor into r0
mov r1, #buffer       @ Load the address of the buffer into r1
mov r2, #size         @ Load the number of bytes to read into r2
swi 0x67              @ Software interrupt to read from file
                      @ Number of bytes read returned in r0
```

#### Writing to a File

```assembly
@ Write to a file
mov r0, #file_desc    @ Load the file descriptor into r0
mov r1, #buffer       @ Load the address of the buffer into r1
mov r2, #size         @ Load the number of bytes to write into r2
swi 0x68              @ Software interrupt to write to file
                      @ Number of bytes written returned in r0
```

#### Closing a File

```assembly
@ Close a file
mov r0, #file_desc    @ Load the file descriptor into r0
swi 0x69              @ Software interrupt to close file
                      @ Returns 0 on success, or an error code
```

### Example: Reading from a File

Here's a complete example demonstrating how to open a file, read from it, and then close it.

```assembly
@ Example of reading from a file

.data
filename: .asciz "example.txt"   @ File name
buffer: .space 256               @ Buffer to hold file contents

.text
.global _start

_start:
    @ Open the file
    ldr r0, =filename            @ Load the address of the filename
    mov r1, #0                   @ Mode: read (0)
    swi 0x66                     @ Open file
    mov r4, r0                   @ Save file descriptor

    @ Read from the file
    ldr r0, [r4]                 @ Load file descriptor
    ldr r1, =buffer              @ Load buffer address
    mov r2, #256                 @ Number of bytes to read
    swi 0x67                     @ Read from file

    @ Close the file
    mov r0, r4                   @ Load file descriptor
    swi 0x69                     @ Close file

    @ Exit (assuming a Linux system call to exit)
    mov r7, #1                   @ sys_exit
    swi 0x0                      @ Call kernel
```

---

Feel free to contribute by adding more sections or improving existing ones. Happy coding!

```

