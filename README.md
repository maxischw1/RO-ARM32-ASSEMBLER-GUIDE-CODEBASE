# RO-ARM32-ASSEMBLER-GUIDE_CODEBASE
short file containing all necessary code modules for RO


## LDR, STR LARGE VARIABLES:

## BITMANIPULATION:

## IF ELSE:

```bash
IF:

1   cmp r0, r1
2 bne IF
3   ... 
4 IF :
5   ... /* IF */

IF-ELSE:

1   cmp r0 , r1
2   bne IF
3   ...
4   b ELSE
5 IF :
6   ... /* IF */
7 ELSE :
8   ... /* ELSE */


```
## LOOP:

Both Loops act verymuch alike,
the only notebale difference is the inclusion of a counter

### WHILE:

```bash
1   ... /* necessary init steps */
2   ...
3 WHILE :
4   cmp r0, #x /* x being  */
5   beq DONE
6   ...
7   ...
8   b WHILE
9 DONE :

```

### FOR:

```bash
1   ... /* necessary init steps */
2   mov r0, #0 /* counter init */
3 FOR :
4   cmp r0, #x /* x being amount of for-calls */
5   beq DONE
6   ...
7   add r1, r1, #1 /* incrementing counter */
8   b FOR
9 DONE :

```

## ARRAY + SORTING:

Arrays are basically: 
a starting address and a varying amount of 4 Byte long Data.

Arrays with larger capacity for each element,
can be implemented by tweaking the jumps and writing arguments.

### ARRAY:

```bash
1   /* init */
2   mov r0, #adr /* move the adr of first element into r0 */
3   mov r1, #0 /* 0 to y , array pointer */
4   /* LOOP to fill Array */
5 LOOP :
6   cmp r1, #y /* Break for LOOP  y = (Length of Array * 4) */
7   bge DONE:
8   ...
9   add r1, r1, #4 /* moving array pointer */
10  str rX, [r0, r1] /* writing value of X-Register into array */
11  ...
12  b LOOP:
13 DONE :
```

### SORTING

```bash
1   /* init */
2   mov r0, #adr /* move the adr of first element into r0 */
3   ...
4   /* LOOP to iterate over Array */
5 LOOP :
6   cmp r1, #y /* Break for LOOP  y = (Length of Array * 4) */
7   bge DONE:
8   ...
9   add r1, r1, #4 /* moving array pointer */
10  ldr rX, [r0, r1] /* loading value of array into X-Register to compute */
11  ... /* the computation happening */
12  b LOOP:
13 DONE :
```

SUBPROGRAM:

SUBPROGRAM + STACK:

RECURSION:
