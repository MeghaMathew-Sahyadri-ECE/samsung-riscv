# RISC-V Internship Program **Powered by SAMSUNG and VSD**

This internship focuses on the RISC-V architecture and uses open-source tools to teach participants about VLSI chip design and RISC-V.

Instructor: **Kunal Ghosh Sir**

---

## Basic Details

**Name**: Megha Akku Mathew  
**College**: Sahyadri College of Engineering and Management  
**Email**: [meghaakkumathew@gmail.com](mailto:meghaakkumathew@gmail.com)  
**GitHub Profile**: [MeghaMathew-Sahyadri-ECE](https://github.com/MeghaMathew-Sahyadri-ECE)  
**LinkedIn Profile**: [Megha Akku Mathew](https://www.linkedin.com/in/megha-akku-mathew-1545b2257/)

---

## Tasks Overview

<details>
<summary>Task 1: Compile C Code</summary>

The task involved referring to C-based and RISC-V-based lab videos and executing the process of compiling C code using GCC and the RISC-V compiler.

</details>

<details>
<summary>Task 2: SPIKE Simulation</summary>

- Performing SPIKE simulation.
- Debugging the C code in Interactive Debugging Mode using Spike.

</details>

<details>
<summary>Task 3: Instruction Encoding</summary>

The goal is to identify the instruction type, decode the given instructions, and represent the exact 32-bit machine code in the desired format.


### Instruction 1: `lui a0, 0x2b`  
![Screenshot 2025-01-16 183517](https://github.com/user-attachments/assets/88e483b3-8f7f-4345-b1d9-3de21147da54)  
**Operation**: Load the upper 20 bits of an immediate (`0x2b`) into register `a0`.  
- **Opcode**: `0110111` (for `lui`)  
- **Destination Register (rd)**: `a0` → `x10` (binary: `01010`)  
- **Immediate (imm[31:12])**: `0x2b` → `0000000000101011` (binary)  
**Encoding into Machine Code**:  
imm[31:12]         | rd      | opcode --->0000000000101011  | 01010   | 0110111  
- **Binary**: `0000000000101011010100110111`  
- **Hexadecimal**: `0x002b537`  

---

### Instruction 2: `addi sp, sp, -32`  
![Screenshot 2025-01-16 184848](https://github.com/user-attachments/assets/129cff5e-fb51-4c4a-b84d-9873402b46e3)  
**Operation**: Add `-32` to the stack pointer (`sp`).  
- **Opcode**: `0010011` (for immediate arithmetic operations like `addi`)  
- **Function (funct3)**: `000` (for addition)  
- **Source Register (rs1)**: `sp` → `x2` (binary: `00010`)  
- **Destination Register (rd)**: `sp` → `x2` (binary: `00010`)  
- **Immediate (imm[11:0])**: `-32` → `1111111111100000` (12-bit two’s complement)  
**Encoding into Machine Code**:  
imm[11:0]        | rs1    | funct3 | rd      | opcode -----> 111111111110     | 00010  | 000    | 00010   | 0010011  
- **Binary**: `11111111111000010000100110011`  
- **Hexadecimal**: `0xfe010113`

---

### Instruction 3: `sd ra, 24(sp)`  
![Screenshot 2025-01-16 184929](https://github.com/user-attachments/assets/a965e099-9b5b-488a-bcae-841197513dfd)  
**Operation**: Store the value in `ra` into memory at offset `24` from `sp`.  
- **Opcode**: `0100011` (for store instructions)  
- **Function (funct3)**: `011` (for `sd`, store double-word)  
- **Source Register 1 (rs1)**: `sp` → `x2` (binary: `00010`)  
- **Source Register 2 (rs2)**: `ra` → `x1` (binary: `00001`)  
- **Immediate (imm[11:0])**:  
  - **imm[11:5]**: `0000011`  
  - **imm[4:0]**: `11000`  
**Encoding into Machine Code**:  
imm[11:5] | rs2   | rs1    | funct3 | imm[4:0] | opcode ------> 0000011   | 00001 | 00010  | 011    | 11000    | 0100011  
- **Binary**: `000001100001000100110000100011`  
- **Hexadecimal**: `0x01801323`

---

### Instruction 4: `jal ra, 10438`  
![Screenshot 2025-01-16 184953](https://github.com/user-attachments/assets/78558d34-6ddc-42cf-9de2-e81884d96629)  
**Operation**: Jump to the address 10438 and store the return address in ra.  
- **Opcode**: `1101111` (for `jal`).  
- **Destination Register (rd)**: ra is x1 (binary: `00001`).  
- **Immediate (imm[20|10:1|11|19:12])**: Immediate 10438 in binary: 001010001001110 (split into fields):  
  - imm[20]: `0`  
  - imm[10:1]: `0100010011`  
  - imm[11]: `0`  
  - imm[19:12]: `00101000`  
**Encoding into Machine Code**:  
imm[20|10:1|11|19:12] | rd      | opcode -------> 0|0100010011|0|00101000| 00001  | 1101111  
- **Binary**: `0000000100100011000101110111`  
- **Hexadecimal**: `0x370001e7`

---

### Instruction 5: `ret`  
![Screenshot 2025-01-17 135951](https://github.com/user-attachments/assets/0be2f752-044f-4a0f-a480-f889f182a3fb)  
**Operation**: Return to the calling function. This is equivalent to `jalr x0, ra, 0` in RISC-V assembly.  
- **Opcode**: `1100111` (for `jalr`)  
- **Source Register (rs1)**: `ra` → `x1` (binary: `00001`)  
- **Destination Register (rd)**: `x0` → `x0` (binary: `00000`)  
- **Immediate**: `0`  
**Encoding into Machine Code**:  
imm[11:0] | rs1    | funct3 | rd    | opcode -----> 000000000000     | 00001  | 000    | 00000  | 1100111  
- **Binary**: `00000000000000010000000001110011`  
- **Hexadecimal**: `0x00000067`

---

### Instruction 6: `bnez a5, offset`  
![Screenshot 2025-01-17 130933](https://github.com/user-attachments/assets/56cd7a16-2dd8-4367-aeb7-e27033de646f)  
**Operation**: Branch to the specified offset if the value in register `a5` is not zero.  
- **Opcode**: `1100011` (for `branch` instructions)  
- **Source Register (rs1)**: `a5` → `x15` (binary: `01111`)  
- **Function (funct3)**: `001` (for `bnez`, branch if not zero)  
- **Immediate (offset)**: Branch target address relative to PC.  
**Encoding into Machine Code**:  
imm[12|10:5] | rs2   | rs1    | funct3 | imm[4:1|11] | opcode -----> 000000000000   | 01111  | 01111 | 001    | 00000   | 1100011  
- **Binary**: `000000000000011110001000000011`  
- **Hexadecimal**: `0x000f0043`

---

### Instruction 7: `andi a5, a5, 1`  
![Screenshot 2025-01-17 130917](https://github.com/user-attachments/assets/339ebf12-6cd5-4951-b800-06262c2af782)  
**Operation**: Performs a bitwise AND on register `a5` and the immediate value `1`, storing the result back in `a5`.  
- **Opcode**: `0010011` (for immediate arithmetic operations like `andi`)  
- **Function (funct3)**: `111` (for `andi`)  
- **Immediate (imm[11:0])**: `1`  
**Encoding into Machine Code**:  
imm[11:0] | rs1   | funct3 | rd    | opcode ------> 000000000001   | 01111  | 111    | 01111  | 0010011  
- **Binary**: `0000000000010111100010000110011`  
- **Hexadecimal**: `0x001f0763`

---

### Instruction 8: `lw a5, 12(sp)`  

![Screenshot 2025-01-17 130856](https://github.com/user-attachments/assets/0fe14acc-845a-4fb3-ac0f-3ff4783099b4)

**Operation**: Load a word from memory at offset `12` from the stack pointer (`sp`) into register `a5`.  
- **Opcode**: `0000011` (for load instructions)  
- **Function (funct3)**: `010` (for `lw`, load word)  
- **Source Register (rs1)**: `sp` → `x2` (binary: `00010`)  
- **Destination Register (rd)**: `a5` → `x15` (binary: `01111`)  
- **Immediate (imm[11:0])**: `12` → `00000000001100` (binary)

**Encoding into Machine Code:**

imm[11:0] | rs1    | funct3 | rd    | opcode -----> 000000000011     | 00010  | 010    | 01111  | 0000011

- **Binary**: `00000000001100010000101110000011`  
- **Hexadecimal**: `0x0002c783`

---

### Instruction 9: `li a0, 0`  

![Screenshot 2025-01-17 131023](https://github.com/user-attachments/assets/67bb7026-1faf-4a62-b771-b5a024925cdd)

**Operation**: Load the immediate value `0` into register `a0`.  
- **Opcode**: `0010011` (for immediate arithmetic operations like `li`)  
- **Function (funct3)**: `000` (for `addi` operation)  
- **Source Register (rs1)**: `x0` (binary: `00000`)  
- **Destination Register (rd)**: `a0` → `x10` (binary: `01010`)  
- **Immediate (imm[11:0])**: `0` → `000000000000` (binary)

**Encoding into Machine Code:**

imm[11:0] | rs1    | funct3 | rd    | opcode -----> 000000000000   | 00000  | 000    | 01010  | 0010011

- **Binary**: `00000000000000000000101000010011`  
- **Hexadecimal**: `0x00000293`

---
---

### Instruction 10: `j 100ec <main+0x3c>`  

![Screenshot 2025-01-17 131055](https://github.com/user-attachments/assets/023753a6-f6d9-46dd-9d22-b87df64483b5)

**Operation**: Perform an unconditional jump to the target address `100ec`, which is `main+0x3c`.  
- **Opcode**: `1101111` (for `j` jump instructions)  
- **Immediate (imm[20|10:1|11|19:12])**:  
  - Immediate `100ec` in binary: `000001001110110100000000000000` (split into fields)  
  - imm[20]: `0`  
  - imm[10:1]: `0011101101`  
  - imm[11]: `0`  
  - imm[19:12]: `00000000`  

**Encoding into Machine Code:**

imm[20|10:1|11|19:12] | rd    | opcode -----> 0|0011101101|0|00000000| 00000  | 1101111

- **Binary**: `00000000001110110101000000001111`  
- **Hexadecimal**: `0xfe5ff06f`

---

### Instruction 11: `ld ra, 24(sp)`  

![Screenshot 2025-01-17 130958](https://github.com/user-attachments/assets/509dbb03-7570-48db-a1cc-24f15b6a4e35)

**Operation**: Load a double-word from memory at offset `24` from the stack pointer (`sp`) into register `ra`.  
- **Opcode**: `0000011` (for load instructions)  
- **Function (funct3)**: `011` (for `ld`, load double-word)  
- **Source Register (rs1)**: `sp` → `x2` (binary: `00010`)  
- **Destination Register (rd)**: `ra` → `x1` (binary: `00001`)  
- **Immediate (imm[11:0])**: `24` → `00000000011000` (binary)

**Encoding into Machine Code:**

imm[11:0] | rs1    | funct3 | rd   | opcode -----> 000000000110     | 00010  | 011    | 00001  | 0000011

- **Binary**: `00000000011000010001000110000011`  
- **Hexadecimal**: `0x01813083`

---

### Instruction 12: `auipc ra, 0x0`  

![Screenshot 2025-01-17 142008](https://github.com/user-attachments/assets/40ccf672-c70c-4142-b7f3-47f179925618)

**Operation**: Adds the program counter (`PC`) value and an immediate value `0x0`, and stores the result in `ra`.  
- **Opcode**: `0010111` (for `auipc`, add upper immediate to program counter)  
- **Destination Register (rd)**: `ra` → `x1` (binary: `00001`)  
- **Immediate (imm[31:12])**: `0x0` → `000000000000` (binary)

**Encoding into Machine Code:**

imm[31:12] | rd    | opcode -----> 000000000000   | 00001  | 0010111

- **Binary**: `00000000000000000000000101110111`  
- **Hexadecimal**: `0x00000097`

---

### Instruction 13: `jalr zero, 0x0(main-0x100b0)`  

![Screenshot 2025-01-17 142109](https://github.com/user-attachments/assets/d6a1f9eb-2671-4783-a63c-a62a69e5d490)

**Operation**: Perform a jump and link register to the address `main-0x100b0` and write the return address to `zero`.  
- **Opcode**: `1100111` (for `jalr` jump and link register)  
- **Function (funct3)**: `000` (for `jalr` with `x0` as destination)  
- **Source Register (rs1)**: `main` → `x1` (binary: `00001`)  
- **Immediate (imm[11:0])**: `0x0` → `000000000000` (binary)  

**Encoding into Machine Code:**

imm[11:0] | rs1    | funct3 | rd    | opcode -----> 000000000000   | 00001  | 000    | 00000  | 1100111

- **Binary**: `00000000000000001000000000001111`  
- **Hexadecimal**: `0x000000e7`
---

---

### Instruction 14: `jr zero # 0 <main-0x100b0>`  

![Screenshot 2025-01-17 142817](https://github.com/user-attachments/assets/7138fff3-cdcf-4d6b-a974-ffc370dd1bb0)

**Operation**: Perform a jump register to the address `main-0x100b0` and write the return address to register `zero`.  
- **Opcode**: `1100011` (for `jr` jump register)  
- **Function (funct3)**: `000` (for `jr` with `x0` as destination)  
- **Source Register (rs1)**: `main` → `x1` (binary: `00001`)  
- **Immediate (imm[11:0])**: `0x0` → `000000000000` (binary)

**Encoding into Machine Code:**

imm[11:0] | rs1    | funct3 | rd    | opcode -----> 000000000000   | 00001  | 000    | 00000  | 1100011

- **Binary**: `00000000000000001000000000000011`  
- **Hexadecimal**: `0x00000067`

---

### Instruction 15: `mv a1, a0`  

![Screenshot 2025-01-17 142801](https://github.com/user-attachments/assets/b0770975-a71a-4bd0-9552-0bb349004d35)

**Operation**: Move the value in register `a0` to register `a1`.  
- **Opcode**: `0110011` (for R-type register operations like `mv`)  
- **Function (funct3)**: `000` (for `mv` operation)  
- **Source Register (rs1)**: `a0` → `x10` (binary: `01010`)  
- **Source Register (rs2)**: `a0` → `x10` (binary: `01010`)  
- **Destination Register (rd)**: `a1` → `x11` (binary: `01011`)  
- **Function (funct7)**: `0000000` (for `mv` operation)

**Encoding into Machine Code:**

funct7 | rs2    | rs1    | funct3 | rd    | opcode -----> 0000000   | 01010  | 01010  | 000    | 01011  | 0110011

- **Binary**: `00000000010101001010100000000011`  
- **Hexadecimal**: `0x00050593`

---


</details>

<details>
<summary>Task 4: Run Code and Verify Outputs</summary>

# Task 4: RISCV Functional Simulation

This task contains the Verilog code for a simple RISCV core (`megha_rv32i.v`) and its corresponding testbench (`megha_rv32i_tb.v`). The simulation is executed using Icarus Verilog, and the waveform output is visualized in GTKWave.

## Task Objective

We will simulate the RISCV core and analyze the output waveforms for different RISCV instructions that have been hardcoded in the Verilog code. The instructions are based on the reference RISCV ISA but differ in the instruction bit patterns.

### Hardcoded Instructions:
Below are the instructions used in the reference repository compared to the standard RISCV ISA bit patterns:

![Instructions](https://github.com/user-attachments/assets/f1fc4e22-cbb4-44b8-aa57-e15a76f79145)


###To to perform functional simulation of RISCV
1. Create a new directory with your name mkdir <your_name>

2. Create two files by using touch command as megha_rv32i.v and megha_rv32i_tb.v

3. Copy the code from the reference github repo and paste it in your verilog and testbench files

![Generation n adding of code](https://github.com/user-attachments/assets/53ca8a64-c7c5-439b-8651-da1144d007ec)

![Compilation of code](https://github.com/user-attachments/assets/7d88c714-c416-4f61-b375-c61d4a915690)


Following are the differences between standard RISCV ISA and the Instruction Set given in the reference repository:

- **ADD R6, R2, R1**  
  - Standard RISCV ISA: `32'h00110333`  
  - Hardcoded ISA: `32'h02208300`
  
  ![ADD](https://github.com/user-attachments/assets/9351ac4d-832d-43fc-8f63-805ac7c8b04d)

- **SUB R7, R1, R2**  
  - Standard RISCV ISA: `32'h402083b3`  
  - Hardcoded ISA: `32'h02209380`
 
    ![SUB](https://github.com/user-attachments/assets/8d719c4f-a938-4550-bda9-bd4932c7337c)


- **AND R8, R1, R3**  
  - Standard RISCV ISA: `32'h0030f433`  
  - Hardcoded ISA: `32'h0230a400`
 
![bitwise AND](https://github.com/user-attachments/assets/c9b0135f-36f0-4c3b-b45b-12f234be4e4a)


- **OR R9, R2, R5**  
  - Standard RISCV ISA: `32'h005164b3`  
  - Hardcoded ISA: `32'h02513480`
 
![Bitwise OR](https://github.com/user-attachments/assets/6db85b83-8411-4eea-a194-e9d4ddcfa092)


- **XOR R10, R1, R4**  
  - Standard RISCV ISA: `32'h0040c533`  
  - Hardcoded ISA: `32'h0240c500`
 
![BITWISE XOR](https://github.com/user-attachments/assets/1ef0bf3e-a550-4c3d-8d19-8ac4da60ccfe)


- **SLT R1, R2, R4**  
  - Standard RISCV ISA: `32'h0045a0b3`  
  - Hardcoded ISA: `32'h02415580`

![SLT operator](https://github.com/user-attachments/assets/118a62ab-b5ab-4530-a0b9-da1b58ab61c6)


- **ADDI R12, R4, 5**  
  - Standard RISCV ISA: `32'h004120b3`  
  - Hardcoded ISA: `32'h00520600`
 
![ADDI](https://github.com/user-attachments/assets/51f27d12-990d-4829-91b5-d53fde104d34)


- **BEQ R0, R0, 15**  
  - Standard RISCV ISA: `32'h00000f63`  
  - Hardcoded ISA: `32'h00f00002`
 
![BEQ](https://github.com/user-attachments/assets/69efa0bb-832d-4c29-b357-50d7133d8b9f)


- **BNE R0, R1, 20**  
  - Standard RISCV ISA: `32'h00000163`  
  - Hardcoded ISA: `32'h02005063`
 
![BNE](https://github.com/user-attachments/assets/d10a7fbb-ac7b-4e7f-b17a-89e207fb880a)



### Simulation Output

![GTK simulation 1](https://github.com/user-attachments/assets/69f3f232-202a-4738-b1ba-71331cafbe79)

![simulation 3](https://github.com/user-attachments/assets/83af30f4-6891-4fd7-9231-edfadc65fa37)


</details>



