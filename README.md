# Anirudha-Kulkarni-VSDSquadron-Mini-internship

Task 1
task: To install RISC-V toolchain 
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


Task 2
RISC V INSTRUCTION TYPES 
RISC V Instructions format:
There are 6 insrtuction types
R-Register type
I-Immediate type
S-Store type
B-Branch type
U-Upper Immediate type
J-Jump type
1. R type- has 3 registers; 2 source and 1 destination register. Hence the name R type. rs1 and rs2 are operands. Result stored in destination register.We need min. of 5 bits to address 32 registers.
2. I type- similar to R type except that instead of rs2 we perform opn between rs1 and constant defined by 12 bits. for the constant, we need to sign extend the immidiate value.
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
![riscv instruction types](https://github.com/Anirudha1509/VSDSquadron-Mini-internship/assets/126673141/89dae892-a069-4b9c-b319-ccaad99aef95)



