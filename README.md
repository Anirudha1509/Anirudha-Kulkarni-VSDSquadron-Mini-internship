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

Task 3:

Functional simulation experiment using RISC-V Core Verilog netlist and testbench.

- IVERILOG:-Icarus Verilog, commonly referred to as IVerilog, is an open-source Verilog simulation and synthesis tool. It supports a wide range of Verilog standards and is used for designing and testing digital circuits. IVerilog is popular for its flexibility, allowing users to simulate complex designs and generate netlists for various FPGA and ASIC platforms. It is widely used in both educational and professional settings for hardware design and verification.

- GTKWAVE:- GTKWave is an open-source waveform viewer used for visualizing simulation results from digital circuit designs. It is commonly used in conjunction with simulation tools like Icarus Verilog.It is a fully featured GTK+ based waveform viewer for Unix and Win32, capable of displaying signal waveforms dumped in a variety of formats.

to get the expected waveforms, the following commands were typed in the terminal:
    
    ```
    sudo apt-get update
    sudo apt install iverilog gtkwave
    ```


![Screenshot 2024-06-01 184122](https://github.com/Anirudha1509/VSDSquadron-Mini-internship/assets/126673141/580f391f-6879-46ec-aa82-64638fc63b0f)

- clone the github repositry:
  ```
  $ git clone https://github.com/Anirudha1509/VSDSquadron-Mini-internship
  ```
  ```
  $ cd VSDSquadron-Mini-internship
  ```

  ![Screenshot 2024-06-01 184613](https://github.com/Anirudha1509/VSDSquadron-Mini-internship/assets/126673141/8f7a8146-c25f-4523-ab24-2725fcdf6830)

- simulate and run the code
  ```
  $ iverilog -o rv32i rv32i.v rv32i_tb.v
  ```
  ```
  $ ./rv32i
  ```

  ![Screenshot 2024-06-01 184713](https://github.com/Anirudha1509/VSDSquadron-Mini-internship/assets/126673141/cb3def26-8c1f-4c36-849b-d7d72c91ea8d)

- to open the waveform in gtkwave
  ```
  $ gtkwave ani_rv32i.vcd&
  ```

- following instructions were analysed:
following instruction are:-

1.ADD r6, r2, r1

2.SUB r7, r1, r2

3.AND r8, r1, r3

4.OR r9, r2, r5

5.XOR r10, r1, r4

6.SLT r11, r2, r4

7.ADDI r12, r4, 5

8.SW r3, r1, 2

9.SRL r16, r14, r2

10.BEQ r0, r0, 15

```
1.ADD r6, r2, r1
```
<img width="464" alt="image" src="https://github.com/Anirudha1509/VSDSquadron-Mini-internship/assets/126673141/6a827e6f-dc26-4579-a6a8-1be40e3ed4f5">

```
2.SUB r7, r1, r2
```
<img width="734" alt="image" src="https://github.com/Anirudha1509/VSDSquadron-Mini-internship/assets/126673141/fa8d8895-86cd-49d9-81b8-65a2b9901e53">

```
3.AND r8, r1, r3
```
<img width="513" alt="image" src="https://github.com/Anirudha1509/VSDSquadron-Mini-internship/assets/126673141/2c971949-d5dc-481d-ba4a-c64befdd1b7a">

```
4.OR r9, r2, r5
```
<img width="578" alt="image" src="https://github.com/Anirudha1509/VSDSquadron-Mini-internship/assets/126673141/beedc549-eebe-4986-b26b-ce8f723656f4">

```
5.XOR r10, r1, r4
```
<img width="633" alt="image" src="https://github.com/Anirudha1509/VSDSquadron-Mini-internship/assets/126673141/65374207-0df1-4bed-a5db-7ce27ddc8087">

```
6.SLT r11, r2, r4
```
<img width="686" alt="image" src="https://github.com/Anirudha1509/VSDSquadron-Mini-internship/assets/126673141/31a89ce7-ac4f-4562-8736-532cc366c9f0">

```
7.ADDI r12, r4, 5
```
![Screenshot 2024-06-01 202012](https://github.com/Anirudha1509/VSDSquadron-Mini-internship/assets/126673141/a21603bd-f52d-454e-b329-efb9c25ef508)


```
8.SW r3, r1, 2
```
<img width="462" alt="image" src="https://github.com/Anirudha1509/VSDSquadron-Mini-internship/assets/126673141/a0a8c569-96fd-4bb3-b28d-fd62d3a38f48">

```
9.LW r13, r1, 2
```
<img width="332" alt="image" src="https://github.com/Anirudha1509/VSDSquadron-Mini-internship/assets/126673141/f3e7cccd-6415-4ab7-82a9-a1c02274658f">

```
10.BEQ r0, r0, 15
```
<img width="375" alt="image" src="https://github.com/Anirudha1509/VSDSquadron-Mini-internship/assets/126673141/077e792c-ce7a-456d-9005-31580bfa501e">



Task 4:

To update the project overview, components required, pinout diagram through powerpoint.

[Powerpoint link] (https://1drv.ms/p/s!AqLzFgI4vU8agtYK4l8yEv4oyh_s7g?e=ralosN)


**2 Bit Multiplier**

**Overview**

This project aims to design and implement a 2-bit multiplier using the VSDSquadron Mini board. A Binary Multiplier is a digital circuit used in digital electronics to multiply two binary numbers and provide the result as output. The two numbers A1A0 and B1B0 are multiplied together to produce a 4-bit output P3P2P1P0. (The maximum product term can be 3 * 3 = 9, which is 1001, a 4-bit number).


 **Components Required**
- VSDSquadron Mini Board : The main microcontroller board used for processing and logic implementation.
- Breadboard and Jumper Wires : For building and testing the circuit.
- LEDs : To display the product results. This project requires 4 LEDs.
- Resistors : To limit the current to the LEDs 2.2k Ohm, and 10k  resistors are used in this project.

**Circuit Diagram**

![Screenshot 2024-06-09 224948](https://github.com/Anirudha1509/VSDSquadron-Mini-internship/assets/126673141/1b9c3890-208b-437c-8839-76ea2bdf61fd)



**Truth table**

![image](https://github.com/Anirudha1509/VSDSquadron-Mini-internship/assets/126673141/a9766a99-fdc4-489d-8c48-2fd786ce46d5)


**Pin Diagram**

![Screenshot 2024-06-09 215230](https://github.com/Anirudha1509/VSDSquadron-Mini-internship/assets/126673141/1f8c6e85-0cd8-409c-bbb4-28a37b76ed1c)


**Code for the project**
```

#include <ch32v00x.h>
#include <debug.h>
#include <stdio.h>
/* Defining gate functions */
int and (int bit1, int bit2)
{
int and = bit1 & bit2;
return and;
}
int xor (int bit1, int bit2)
{
int xor = bit1 ^ bit2;
return xor;
}
void GPIO_Config(void)
{
GPIO_InitTypeDef GPIO_InitStructure = {0};
/* Switching ON port D and simultaneously defining pin functions */
RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOD, ENABLE);
GPIO_InitStructure.GPIO_Pin = GPIO_Pin_3 | GPIO_Pin_4;
GPIO_InitStructure.GPIO_Mode = GPIO_Mode_IPU;
GPIO_Init(GPIOD, &GPIO_InitStructure);
GPIO_InitStructure.GPIO_Pin = GPIO_Pin_2;
GPIO_InitStructure.GPIO_Mode = GPIO_Mode_Out_PP;
GPIO_InitStructure.GPIO_Speed = GPIO_Speed_2MHz;
GPIO_Init(GPIOD, &GPIO_InitStructure);
/* Switching ON port C and simultaneously defining pin functions */
RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOC, ENABLE);
GPIO_InitStructure.GPIO_Pin = GPIO_Pin_3 | GPIO_Pin_4;
GPIO_InitStructure.GPIO_Mode = GPIO_Mode_IPU;
GPIO_Init(GPIOC, &GPIO_InitStructure);
GPIO_InitStructure.GPIO_Pin = GPIO_Pin_5|GPIO_Pin_2|GPIO_Pin_1;
GPIO_InitStructure.GPIO_Mode = GPIO_Mode_Out_PP;
GPIO_InitStructure.GPIO_Speed = GPIO_Speed_2MHz;
GPIO_Init(GPIOC, &GPIO_InitStructure);
}
/* The main function responsible for execution of program */
int main(void)
{
uint8_t a, b0, b1, b, d, a0, a1, x, e,g ,f, v = 0; /* Declaring variables */
NVIC_PriorityGroupConfig(NVIC_PriorityGroup_2);
SystemCoreClockUpdate();
Delay_Init();
GPIO_Config();

while (1)
{
a0 = GPIO_ReadInputDataBit(GPIOD, GPIO_Pin_3); /* Reading input values for pin D3, D4, C3, C4 */
a1 = GPIO_ReadInputDataBit(GPIOD, GPIO_Pin_4);
b0 = GPIO_ReadInputDataBit(GPIOC, GPIO_Pin_3);
b1 = GPIO_ReadInputDataBit(GPIOC, GPIO_Pin_4);
a = and(a0,b0); /* P0 */
b = and(a0,b1);
d = and(a1,b0);
x = xor(b,d); /* P1 */
e = and(a1,b1);
g = and(b,d);
f = xor(e,g); /* P2 */
v = and(e,g); /* P3 */
/* P0 */
if(a==1)
{
GPIO_WriteBit(GPIOD,GPIO_Pin_2,SET);
}
else
{
GPIO_WriteBit(GPIOD,GPIO_Pin_2,RESET);
}
/* P1 */
if(x==1)
{
GPIO_WriteBit(GPIOC,GPIO_Pin_1,SET);
}
else
{
GPIO_WriteBit(GPIOC,GPIO_Pin_1,RESET);
}
/* P2 */
if(f==1)
{
GPIO_WriteBit(GPIOC,GPIO_Pin_2,SET);
}
else
{
GPIO_WriteBit(GPIOC,GPIO_Pin_2,RESET);
}
/* P3 */
if(v==1)
{
GPIO_WriteBit(GPIOC,GPIO_Pin_5,SET);
}
else
{
GPIO_WriteBit(GPIOC,GPIO_Pin_5,RESET);
}
}
}

```


![Screenshot 2024-06-09 220445](https://github.com/Anirudha1509/VSDSquadron-Mini-internship/assets/126673141/d88fbc9e-e970-493b-89ed-895415c54a15)




**Working Model**

![WhatsApp Image 2024-06-09 at 10 06 27 PM](https://github.com/Anirudha1509/VSDSquadron-Mini-internship/assets/126673141/c54aef58-9cc2-45d3-808d-be624ff474bd)




![WhatsApp Image 2024-06-09 at 10 06 28 PM](https://github.com/Anirudha1509/VSDSquadron-Mini-internship/assets/126673141/e8dae8c4-10e0-49d3-81a5-057857de21f6)


**Demonstration**

Drive link: 
```
https://drive.google.com/file/d/1N_kPnGqd-BCUeDQE7Ih2_IoaSFkL780I/view?usp=sharing

```





