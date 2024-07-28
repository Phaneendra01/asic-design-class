# 🖥️ RISC-V Instruction Analysis

## 🎯 Task 2: Instruction Type Identification and 32-Bit Code Generation

Dive into the world of RISC-V as we explore instruction types and generate 32-bit instruction codes!

### 🧠 RISC-V Overview

RISC-V is an open-source instruction set architecture (ISA) that empowers developers to create custom processors. It's built on RISC principles and represents the fifth generation of this innovative concept.

### 📊 RISC-V Instruction Formats

RISC-V features six powerful instruction formats:

1. R-format 🔴
2. I-format 🟠
3. S-format 🟡
4. B-format 🟢
5. U-format 🔵
6. J-format 🟣

<p align="center">
  <img src="https://github.com/maazm007/vsdsquadron-mini-internship/assets/83294849/f8e6fd22-79c5-4f6c-b59f-2b38fdb62c0e" alt="RISCV Instruction Types" width="600"/>
</p>

### 🔍 Detailed Instruction Format Breakdown

<details>
<summary><b>🔴 R-type Instruction</b></summary>

<p align="center">
  <img src="https://github.com/maazm007/vsdsquadron-mini-internship/assets/83294849/4a17f03e-ae74-4809-a8d9-79924fb8b421" alt="R-type" width="500"/>
</p>

- 🔹 Used for: Register-to-register operations
- 🔹 Fields: opcode (7 bits), rd (5 bits), func3 (3 bits), rs1 (5 bits), rs2 (5 bits), func7 (7 bits)
</details>

<details>
<summary><b>🟠 I-type Instruction</b></summary>

<p align="center">
  <img src="https://github.com/maazm007/vsdsquadron-mini-internship/assets/83294849/4a53f5fa-d55a-4308-8f93-a0f2f9aedba0" alt="I-type" width="500"/>
</p>

- 🔹 Used for: Immediate and load operations
- 🔹 Fields: opcode (7 bits), rd (5 bits), func3 (3 bits), rs1 (5 bits), imm[11:0] (12 bits)
</details>

<details>
<summary><b>🟡 S-type Instruction</b></summary>

<p align="center">
  <img src="https://github.com/maazm007/vsdsquadron-mini-internship/assets/83294849/fc9ddedc-4c99-4b6f-9765-c2e8c8e29302" alt="S-type" width="500"/>
</p>

- 🔹 Used for: Store operations
- 🔹 Fields: opcode (7 bits), imm[4:0] (5 bits), func3 (3 bits), rs1 (5 bits), rs2 (5 bits), imm[11:5] (7 bits)
</details>

<details>
<summary><b>🟢 B-type Instruction</b></summary>

<p align="center">
  <img src="https://github.com/maazm007/vsdsquadron-mini-internship/assets/83294849/14486f41-f3e4-4c4a-85b0-9acc56be3f46" alt="B-type" width="500"/>
</p>

- 🔹 Used for: Branching operations
- 🔹 Fields: opcode (7 bits), imm[11] (1 bit), imm[4:1] (4 bits), func3 (3 bits), rs1 (5 bits), rs2 (5 bits), imm[10:5] (6 bits), imm[12] (1 bit)
</details>

<details>
<summary><b>🔵 U-type Instruction</b></summary>

<p align="center">
  <img src="https://github.com/maazm007/vsdsquadron-mini-internship/assets/83294849/4f3df58b-8c0c-45c6-ba39-a196547dd38f" alt="U-type" width="500"/>
</p>

- 🔹 Used for: Upper immediate instructions
- 🔹 Fields: opcode (7 bits), rd (5 bits), imm[31:12] (20 bits)
</details>

<details>
<summary><b>🟣 J-type Instruction</b></summary>

<p align="center">
  <img src="https://github.com/maazm007/vsdsquadron-mini-internship/assets/83294849/5dc9a9be-4048-4a35-a99e-7b4a0075caa0" alt="J-type" width="500"/>
</p>

- 🔹 Used for: Jump operations
- 🔹 Fields: opcode (7 bits), rd (5 bits), imm[20|10:1|11|19:12] (20 bits)
</details>

### 🧪 Instruction Analysis

<details>
<summary><b>📝 ADD r5, r4, r5</b></summary>

- Type: R-type 🔵
- Opcode: `0110011`
- funct7: `0000000`
- rs2: `00101`
- rs1: `00100`
- funct3: `000`
- rd: `00101`
- 32-bit instruction: `0000000 00101 00100 000 00101 0110011`
</details>

<details>
<summary><b>📝 SUB r5, r5, r4</b></summary>

- Type: R-type 🟢
- Opcode: `0110011`
- funct7: `0100000`
- rs2: `00100`
- rs1: `00101`
- funct3: `000`
- rd: `00101`
- 32-bit instruction: `0100000 00100 00101 000 00101 0110011`
</details>

<details>
<summary><b>📝 AND r4, r5, r5</b></summary>

- Type: R-type 🔴
- Opcode: `0110011`
- funct7: `0000000`
- rs2: `00101`
- rs1: `00101`
- funct3: `111`
- rd: `00100`
- 32-bit instruction: `0000000 00101 00101 111 00100 0110011`
</details>

<details>
<summary><b>📝 OR r8, r4, r5</b></summary>

- Type: R-type 🟡
- Opcode: `0110011`
- funct7: `0000000`
- rs2: `00101`
- rs1: `00100`
- funct3: `110`
- rd: `01000`
- 32-bit instruction: `0000000 00101 00100 110 01000 0110011`
</details>

<details>
<summary><b>📝 XOR r8, r5, r4</b></summary>

- Type: R-type 🟠
- Opcode: `0110011`
- funct7: `0000000`
- rs2: `00100`
- rs1: `00101`
- funct3: `100`
- rd: `01000`
- 32-bit instruction: `0000000 00100 00101 100 01000 0110011`
</details>

<details>
<summary><b>📝 SLT r10, r2, r4</b></summary>

- Type: R-type 🟣
- Opcode: `0110011`
- funct7: `0000000`
- rs2: `00100`
- rs1: `00010`
- funct3: `010`
- rd: `01010`
- 32-bit instruction: `0000000 00100 00010 010 01010 0110011`
</details>

<details>
<summary><b>📝 ADDI r12, r3, 5</b></summary>

- Type: I-type 🟤
- Opcode: `0010011`
- imm: `000000000101`
- rs1: `00011`
- funct3: `000`
- rd: `01100`
- 32-bit instruction: `000000000101 00011 000 01100 0010011`
</details>

<details>
<summary><b>📝 SW r3, r1, 4</b></summary>

- Type: S-type 🔵
- Opcode: `0100011`
- imm[11:5]: `0000000`
- rs2: `00011`
- rs1: `00001`
- funct3: `010`
- imm[4:0]: `00100`
- 32-bit instruction: `0000000 00011 00001 010 00100 0100011`
</details>

<details>
<summary><b>📝 SRL r16, r11, r2</b></summary>

- Type: R-type 🟡
- Opcode: `0110011`
- funct7: `0000000`
- rs2: `00010`
- rs1: `01011`
- funct3: `101`
- rd: `10000`
- 32-bit instruction: `0000000 00010 01011 101 10000 0110011`
</details>

<details>
<summary><b>📝 BNE r0, r1, 20</b></summary>

- Type: B-type 🔴
- Opcode: `1100011`
- imm[12|10:5]: `000000`
- rs2: `00001`
- rs1: `00000`
- funct3: `001`
- imm[4:1|11]: `10100`
- 32-bit instruction: `000000 00001 00000 001 0100 1100011`
</details>

<details>
<summary><b>📝 BEQ r0, r0, 15</b></summary>

- Type: B-type 🟢
- Opcode: `1100011`
- imm[12|10:5]: `000000`
- rs2: `00000`
- rs1: `00000`
- funct3: `000`
- imm[4:1|11]: `01110`
- 32-bit instruction: `000000 00000 00000 000 1110 1100011`
</details>

<details>
<summary><b>📝 LW r13, r11, 2</b></summary>

- Type: I-type 🟣
- Opcode: `0000011`
- imm: `000000000010`
- rs1: `01011`
- funct3: `010`
- rd: `01101`
- 32-bit instruction: `000000000010 01011 010 01101 0000011`
</details>

<details>
<summary><b>📝 SLL r15, r11, r2</b></summary>

- Type: R-type 🟤
- Opcode: `0110011`
- funct7: `0000000`
- rs2: `00010`
- rs1: `01011`
- funct3: `001`
- rd: `01111`
- 32-bit instruction: `0000000 00010 01011 001 01111 0110011`
</details>

<h1 style="font-size: 36px; text-align: center;">👨‍🎓 Basic Details</h1>

<h1 style="font-size: 36px; text-align: center; width: 100%;">👨‍🎓 Basic Details</h1>

<p align="center">
  <h1>
  👨‍🎓 Basic Details
  </h1>
</p>

<h1 align="center">👨‍🎓 Basic Details</h1>

<p align="center">
  Name: Phaneendra M V
</p>

<p align="center">
  College: IIIT Banglore
</p>

<p align="center">
  Email: Phaneendra.MV@iiitb.ac.in
</p>

<p align="center">
  GitHub: (https://github.com/Phaneendra01/asic-design-class.git)
</p>

<p align="center">
  LinkedIn: (www.linkedin.com/in/phaneendra-mv)
</p>
