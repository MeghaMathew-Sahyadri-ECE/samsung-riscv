# RISC-V Internship program powered by SAMSUNG and VSD
The program is based on the RISC-V architecture and uses open-source tools to teach people about VLSI chip design and RISC-V. The instructor for this internship is Kunal Ghosh Sir.
# Basic Details
Name: Megha Akku Mathew

College: Sahyadri College of Engineering and Management

Email ID: meghaakkumathew@gmail.com

GitHub Profile: https://github.com/MeghaMathew-Sahyadri-ECE

LinkedIN Profile: https://www.linkedin.com/in/megha-akku-mathew-1545b2257/


# Task 1: 
Task is to refer to C based and RISCV based lab videos and execute the task of compiling the C code using gcc and riscv compiler.

# Task 2: 
Performing SPIKE Simulation and Debugging the C code with Interactive Debugging Mode using Spike.

# Task 3: 
Task is to identify instruction type of all the given instructions with its exact 32 bits instruction code in the desired instruction type format.

**Instruction 1: lui a0, 0x2b**

![Screenshot 2025-01-16 183517](https://github.com/user-attachments/assets/88e483b3-8f7f-4345-b1d9-3de21147da54)

Operation: Load the upper 20 bits of an immediate (0x2b) into register a0.

Opcode: 0110111 (for lui).

Destination Register (rd): a0 is register x10 (binary: 01010).

Immediate (imm[31:12]): 0x2b = 0000000000101011 in binary.

Encoding into Machine Code:

imm[31:12]         | rd      | opcode --->0000000000101011  | 01010   | 0110111

Binary: 0000000000101011010100110111

Hexadecimal: 0x002b537



**Instruction 2: addi sp, sp, -32**

![Screenshot 2025-01-16 184848](https://github.com/user-attachments/assets/129cff5e-fb51-4c4a-b84d-9873402b46e3)

Operation: Add -32 to sp (stack pointer).

Opcode: 0010011 (for immediate arithmetic operations like addi).

Function (funct3): 000 (for addition).

Source Register (rs1): sp is register x2 (binary: 00010).

Destination Register (rd): sp is x2 (binary: 00010).

Immediate (imm[11:0]): -32 = 1111111111100000 (12-bit two’s complement).

Encoding into Machine Code:

imm[11:0]        | rs1    | funct3 | rd      | opcode -----> 111111111110     | 00010  | 000    | 00010   | 0010011

Binary: 11111111111000010000100110011

Hexadecimal: 0xfe010113

**Instruction 3: sd ra, 24(sp)**

![Screenshot 2025-01-16 184929](https://github.com/user-attachments/assets/a965e099-9b5b-488a-bcae-841197513dfd)

Operation: Store the value in ra into memory at offset 24 from sp.

Opcode: 0100011 (for store instructions).

Function (funct3): 011 (for sd, store double-word).

Source Register 1 (rs1): sp is x2 (binary: 00010).

Source Register 2 (rs2): ra is x1 (binary: 00001).

Immediate (imm[11:0]): Offset 24 is split into:

imm[11:5]: 0000011

imm[4:0]: 11000

Encoding into Machine Code:

imm[11:5] | rs2   | rs1    | funct3 | imm[4:0] | opcode ------> 0000011   | 00001 | 00010  | 011    | 11000    | 0100011

Binary: 000001100001000100110000100011

Hexadecimal: 0x01801323

**Instruction 4: jal ra, 10438**

![Screenshot 2025-01-16 184953](https://github.com/user-attachments/assets/78558d34-6ddc-42cf-9de2-e81884d96629)

Operation: Jump to the address 10438 and store the return address in ra.

Opcode: 1101111 (for jal).

Destination Register (rd): ra is x1 (binary: 00001).

Immediate (imm[20|10:1|11|19:12]):

Immediate 10438 in binary: 001010001001110 (split into fields):

imm[20]: 0

imm[10:1]: 0100010011

imm[11]: 0

imm[19:12]: 00101000

Encoding into Machine Code:

imm[20|10:1|11|19:12] | rd      | opcode -------> 0|0100010011|0|00101000| 00001  | 1101111

Binary: 0000000100100011000101110111

Hexadecimal: 0x370001e7

