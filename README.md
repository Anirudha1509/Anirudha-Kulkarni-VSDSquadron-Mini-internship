# Anirudha-Kulkarni-VSDSquadron-Mini-internship

Task 1
\t task: To install RISC-V toolchain 
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



