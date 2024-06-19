# RO-ARM32-ASSEMBLER-GUIDE_CODEBASE
short file containing all necessary code modules for RO


## LDR, STR LARGE VARIABLES:

## BITMANIPULATION:

## IF ELSE:

```bash
IF:

1 cmp r0, r1
2 bne L1
3 ... 
4 L1:
5 ... /* IF */

IF-ELSE:

1 cmp r0 , r1
2 bne L1
3 ...
4 b L2
5 L1:
6 ... /* IF */
7 L2:
8 ... /* ELSE */


```
## LOOP:

Both Loops act verymuch alike,
the only notebale difference is the inclusion of a counter

### WHILE:

```bash
1 ... /* necessary init steps */
2 ...
3 WHILE :
4 cmp r0, #x /* x being  */
5 beq DONE
6 ...
7 ...
8 b WHILE
9 DONE:

```

### FOR:

```bash
1 ... /* necessary init steps */
2 mov r0, #0 /* counter init */
3 FOR :
4 cmp r0, #x /* x being amount of for-calls */
5 beq DONE
6 ...
7 add r1, r1, #1 /* incrementing counter */
8 b FOR
9 DONE:

```

ARRAY + SORTING:

SUBPROGRAM:

SUBPROGRAM + STACK:

RECURSION:
