# Anirudha-Kulkarni-VSDSquadron-Mini-internship

Task 1:

To install RISC-V toolchain 
status: done

then a c program to calculate sum of 1 to n numbers is compiled and the snapshot of the output of the code is atteched.
![Screenshot 2024-05-23 231321](https://github.com/Anirudha1509/VSDSquadron-Mini-internship/assets/126673141/38907db2-fd65-4740-a7f8-a409b0284c57)

then same code is compiled using RISC-V compiler
<img width="809" alt="image" src="https://github.com/Anirudha1509/VSDSquadron-Mini-internship/assets/126673141/5d8fb90a-7325-4a43-b0e3-d7cf151bd8f8">
to open assembly level instructions of the desired C code we use the command:
riscv64-unknown-elf-objdump -d sum_1_to_n.o
from the huge set of instructions we then search for main
![Screenshot 2024-05-23 234129](https://github.com/Anirudha1509/VSDSquadron-Mini-internship/assets/126673141/8cabf1a1-29a4-49d0-a253-c710b4ea57a6)
total no. of inst. under main are 15.




Task 2:

RISC V INSTRUCTION TYPES 
RISC V Instructions format:
There are 6 insrtuction types
R-Register type
I-Immediate type
S-Store type
B-Branch type
U-Upper Immediate type
J-Jump type
1. R type- has 3 registers; 2 source and 1 destination register. Hence the name R type. rs1 and rs2 are operands. Result is stored in destination register.We need min. of 5 bits to address 32 registers.
2. I type- similar to R type except that instead of rs2 we perform opn between rs1 and constant defined by 12 bits. for the constant, we need to sign extend the immediate value.
the sign bit will aslways be bit 31.
3. S type- we use this primarily to write the values in the registers. The value is defined and stored in rs2. Address is calculated by rs1 and immediate value.
Address = sum of rs1 and immediate value. The immediate value is sign extended.
4. B type- It will always check the condition using rs1 and rs2 as operands. ie less than, greater than. If the conditon is true, It will jump dowm to the immediate value which will be sign extended.
5. U type- the const defined by immediate value will be stored in the destination register. We basically load the upper immediate. I.e., we need to keep the const in msb and append 0's in lsb.
6. J type- It jumps to a particular location and address is defined by the immediate value.
General rule:
we keep the source(rs1 and rs2) and destination(rd) registers in the same position.
Immediates are always sign extended- ie packed towards left most available bits in the instruction. Sign bit is always 31.

A pictorial representation of the same is shown in the image below-

![image](https://github.com/Anirudha1509/VSDSquadron-Mini-internship/assets/126673141/7e535966-3086-4e3d-886d-3132679c3bac)


![image](https://github.com/Anirudha1509/VSDSquadron-Mini-internship/assets/126673141/92545954-7995-407b-a12e-239cd26ab2af)


Some instructions and their opcodes is as follows:
(opcode is the portion of a machine language instruction that specifies the operation to be performed.)

R type:

R-type instructions follow the format:

| funct7 (7 bits) | rs2 (5 bits) | rs1 (5 bits) | funct3 (3 bits) | rd (5 bits) | opcode (7 bits) |

1.ADD r6, r2, r1
funct7 = 0000000

rs2    = 00001

rs1    = 00010

funct3 = 000

rd     = 00110

opcode = 0110011

32 bit: 0000000 00001 00010 000 00110 0110011

2.SUB r7, r1, r2

funct7 = 0100000
rs2    = 00010
rs1    = 00001
funct3 = 000
rd     = 00111
opcode = 0110011
32-bit: 0100000 00010 00001 000 00111 0110011

3.AND r8, r1, r3

funct7 = 0000000
rs2    = 00011
rs1    = 00001
funct3 = 111
rd     = 01000
opcode = 0110011
32-bit: 0000000 00011 00001 111 01000 0110011

4.OR r9, r2, r5

funct7 = 0000000
rs2    = 00101
rs1    = 00010
funct3 = 110
rd     = 01001
opcode = 0110011
32-bit: 0000000 00101 00010 110 01001 0110011

5.XOR r10, r1, r4

funct7 = 0000000
rs2    = 00100
rs1    = 00001
funct3 = 100
rd     = 01010
opcode = 0110011
32-bit: 0000000 00100 00001 100 01010 0110011

6.SLT r11, r2, r4

funct7 = 0000000
rs2    = 00100
rs1    = 00010
funct3 = 010
rd     = 01011
opcode = 0110011
32-bit: 0000000 00100 00010 010 01011 0110011

7.SRL r16, r14, r2

funct7 = 0000000
rs2    = 00010
rs1    = 01110
funct3 = 101
rd     = 10000
opcode = 0110011
32-bit: 0000000 00010 01110 101 10000 0110011

8.SLL r15, r1, r2

funct7 = 0000000
rs2    = 00010
rs1    = 00001
funct3 = 001
rd     = 01111
opcode = 0110011
32-bit: 0000000 00010 00001 001 01111 0110011

I-type Instructions

I-type instructions have the format:

| imm[11:0] (12 bits) | rs1 (5 bits) | funct3 (3 bits) | rd (5 bits) | opcode (7 bits) |


1.ADDI r12, r4, 5

imm    = 000000000101
rs1    = 00100
funct3 = 000
rd     = 01100
opcode = 0010011
32-bit: 000000000101 00100 000 01100 0010011

2.LW r13, r1, 2

imm    = 000000000010
rs1    = 00001
funct3 = 010
rd     = 01101
opcode = 0000011
32-bit: 000000000010 00001 010 01101 0000011

S-type Instructions

S-type instructions have the format: 

| imm[11:5] (7 bits) | rs2 (5 bits) | rs1 (5 bits) | funct3 (3 bits) | imm[4:0] (5 bits) | opcode (7 bits) |

1.SW r3, r1, 2

imm[11:5] = 0000000
rs2       = 00011
rs1       = 00001
funct3    = 010
imm[4:0]  = 00010
opcode    = 0100011
32-bit: 0000000 00011 00001 010 00010 0100011

B-type Instructions

B-type instructions have the format:

| imm[12] (1 bit) | imm[10:5] (6 bits) | rs2 (5 bits) | rs1 (5 bits) | funct3 (3 bits) | imm[4:1] (4 bits) | imm[11] (1 bit) | opcode (7 bits) |


1.BNE r0, r1, 20

imm[12]    = 0
imm[10:5]  = 001010
rs2        = 00001
rs1        = 00000
funct3     = 001
imm[4:1]   = 0100
imm[11]    = 0
opcode     = 1100011
32-bit: 000000 00001 00000 001 0100 0 1100011

2.BEQ r0, r0, 15

imm[12]    = 0
imm[10:5]  = 000001
rs2        = 00000
rs1        = 00000
funct3     = 000
imm[4:1]   = 1111
imm[11]    = 0
opcode     = 1100011
32-bit: 000001 00000 00000 000 1111 0 1100011








