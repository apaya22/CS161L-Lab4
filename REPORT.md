Section 1: the only issues given to me for this lab was laying out the wires. The digital program is a little frustrating to use and manipulate compared to other kinds of layout/wiring programs. I had a few issues with getting bugs in my wiring with getting the wrong number of bits. This was because of a typo, where I would put 5 bits as constant value for the ALU instead of 

Section 2: Assembly and Hand Tracing



asm
ill assemble these instructions 
and $t0 $t1 $t2
addi $t3 $t4 123
lw $t5, 135($t1)
sw $t3, 136($t1)
beq $t3, $zero, -10


1: and $t0 $t1 $t2 
Opcode: 0, rs: 9, rt: 10, rd: 8, shamt: 0, funct: 36
Binary: 000000 01001 01010 01000 00000 100100
Hex: 0x01284024

2: addi $t3 $t4 123
Opcode: 8, rs: 12, rt: 11, immediate: 123
binary:  001000 01100 01011 0000000001111011
Hex: 0x218B007B

3: lw $t5, 135 
Opcode: 35, rs: 9, rt: 13, immediate: 135
binary: 100011 01001 01101 0000000010000111
Hex: 0x8D2D0087

4: sw $t3, 136
Opcode: 43, rs: 9, rt: 11, immediate: 136
binary: 101011 01001 01011 0000000010001000
Hex: 0xAC2B0088

5: beq $t3, $zero, -10
Opcode: 4, rs: 11, rt: 0, immediate: -10
binary: 000100 01011 00000 1111111111110110
Hex: 0x11607FF6


Hand traces: 
so this is before anything is executed 
Registers
|Reg. Name|Reg. Addr.|Value |
|---------|---------:|------|
| `$zero` | 0        | 0    |
| `$at`   | 1        | 0    |
| `$v0`   | 2        | 0x56 |
| `$v1`   | 3        | 0    |
| `$a0`   | 4        | 0    |
| `$a1`   | 5        | 0    |
| `$a2`   | 6        | 0    |
| `$a3`   | 7        | 0    |
Ram
|Address|Value       |
|------:|------------|
|31    | 0x00000056 |
|132    | 0x00000000 |


Instruction 1: 
lw $v0, 31($zero)

$v0 = Memory[31] = 0x56

instruction 2: 
add $v1, $v0, $v0

$v1 = 0x56 + 0x56 = 0xAC

Instruction 3
sw $v1, 132($zero)

Memory[132] = 0xAC

Instruction 4
sub $a0, $v1, $v0

$a0 = 0xAC 0x56 = 0x56

Instruction 5
addi $a1, $v1, 12

$a1 = 0xAC + 0x0C = 0xB8

Instruction 6
and $a2, $a1, $v1

0xB8 AND 0xAC = 0xA8


$a2 = 0xA8

Instruction 7
or $a3, $a2, $v0

0xA8 OR 0x56 = 0xFE


$a3 = 0xFE

Instruction 8
nor $t0, $a2, $v0

$a2 OR $v0 = 0xA8 OR 0x56 = 0xFE
NOR = ~0xFE = 0xFFFFFF01
$t0 = 0xFFFFFF01

Instruction 9
slt $a2, $a1, $a0

$a1 = 0xB8
$a0 = 0x56 
a1 < a2 = F
this makes $a2 = 0

Instruction 10
beq $a2, $zero, -8

$a2 = 0
$zero = 0

jumps -8 

Instruction 11 
lw $t0, 132($zero)

Memory[132] = 0xAC
$t0 = 0xAC

so after hand tracing all the instructions we see 
Registers
|Reg. Name|Reg. Addr.|Value |
|---------|---------:|------|
| `$zero` | 0        | 0    |
| `$at`   | 1        | 0    |
| `$v0`   | 2        | 0x56 |
| `$v1`   | 3        | 0xAC    |
| `$a0`   | 4        | 0x56    |
| `$a1`   | 5        | 0xB8    |
| `$a2`   | 6        | 0    |
| `$a3`   | 7        | 0xFE    |

$t0 wasnt included in the given chart but it is used and its final val is 0xAC

Ram
|Address|Value       |
|------:|------------|
|31    | 0x00000056 |
|132    | 0x000000AC |