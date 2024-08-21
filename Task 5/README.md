# 🚀 RISC-V Pipelined Processor

In this assignment, we'll implement a RISC-V pipelined processor in Makerchip, a web-based IDE for designing and simulating digital circuits. We'll explore various aspects of the processor design, including:

- 🧮 Sequential and pipelined calculations
- ✅ Validity
- 📏 Total distance calculation

## 🔢 Sequential Calculator

The sequential calculator remembers the previous result and uses it for the next operation.

```verilog
\m5_TLV_version 1d: tl-x.org
\m5
   
   // =================================================
   // Welcome!  New to Makerchip? Try the "Learn" menu.
   // =================================================
   
   //use(m5-1.0)   /// uncomment to use M5 macro library.
\SV
   // Macro providing required top-level module definition, random
   // stimulus support, and Verilator config.
   m5_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV
   //$count[31:0] = 32'b0;
   
   // Sequential Clock
   
   |calc
      @1
         $clk_phan = *clk;
         $reset = *reset;
         $val1[31:0] = >>1$result[31:0];
         $val2[31:0] = $rand2[3:0];
         $result[31:0] = $reset ? 32'b0 : ($sel[1:0] == 2'b00)
                         ? ($val1[31:0] + $val2[31:0]) : ($sel[1:0] == 2'b01)
                         ? ($val1[31:0] - $val2[31:0]) : ($sel[1:0] == 2'b10)
                         ? ($val1[31:0] * $val2[31:0]) : ($sel[1:0] == 2'b11)
                         ? ($val2[31:0] != 0 ? ($val1[31:0] / $val2[31:0]) : 32'bx) :  32'b0;
         //$count[31:0] = $reset  ? 0 : (>>1$count + 1);
   
   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
\SV
	endmodule;
```

📊 Output waveform:

![1](https://github.com/user-attachments/assets/f21c1284-e140-49cf-bc51-787e229c35f3)

## 🔗 Pipelined Logic

Pipelining maximizes resource utilization and reduces delays in performing operations. We'll use a Pythagorean calculator as an example.

```verilog
\m5_TLV_version 1d: tl-x.org
\m5
   // =================================================
   // Welcome!  New to Makerchip? Try the "Learn" menu.
   // =================================================
   
   //use(m5-1.0)   /// uncomment to use M5 macro library.
\SV
	`include "sqrt32.v"
   // Macro providing required top-level module definition, random
   // stimulus support, and Verilator config.
   m5_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV
   |calc
      @1
         $reset = *reset;
         $clk_phan = *clk;
      ?$valid
         @1
            $aa_sq[31:0] = $aa[3:0] * $aa[3:0];
            $bb_sq[31:0] = $bb[3:0] * $bb[3:0];
         @2
            $cc_sq[31:0] = $aa_sq + $bb_sq;
         @3
            $cc[31:0] = sqrt($cc_sq);
            //@4
            //$tot_dist[63:0] = $reset ? 0 : $valid ? (>>1$tot_dist + $cc) : >>1$tot_dist;
            //@4
            //$adder[31:0] = $cc + >>1$tot_dist;
            //@5
            //$tot_dist[31:0] = $valid ? ( >>1$tot_dist + $adder ) : >>1$tot_dist

   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 16'd30;
   *failed = 1'b0;
\SV
   endmodule
```

📊 Output waveform:
![2](https://github.com/user-attachments/assets/514bccea-c080-4e82-b1fc-39906d016d4f)

## 🔄 Cycle Calculator

The cycle calculator receives input that is two cycles older than the current output.

```verilog
\m5_TLV_version 1d: tl-x.org
\m5
   // =================================================
   // Welcome!  New to Makerchip? Try the "Learn" menu.
   // =================================================
   
   //use(m5-1.0)   /// uncomment to use M5 macro library.
\SV
   // Macro providing required top-level module definition, random
   // stimulus support, and Verilator config.
   m5_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV
   //$count[31:0] = 32'b0;
   |calc
      @1
         $clk_phan = *clk;
         $reset = *reset;
         $valid = $reset ? 0 : (>>1$valid + 1);
         $valid_or_reset = $valid || $reset;
      ?$valid
         @1
            $val1[31:0] = >>2$result[31:0];
            $val2[31:0] = $rand2[3:0];
         @2
            $out[31:0] = $valid_or_reset ? 32'b0 : ($sel[1:0] == 2'b00) ? ($val1[31:0] + $val2[31:0]) : ($sel[1:0] == 2'b01) ? ($val1[31:0] - $val2[31:0]) : ($sel[1:0] == 2'b10) ? ($val1[31:0] * $val2[31:0]) : ($sel[1:0] == 2'b11) ? ($val2[31:0] != 0 ? ($val1[31:0] / $val2[31:0]) : 32'bx) :  32'b0;
   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
\SV
   endmodule
```

📊 Output waveform:
![3](https://github.com/user-attachments/assets/a4e6af81-ea3d-466e-b4b4-7ad8dab3c766)


## ✅ Validity

Validity ensures that the circuit only performs calculations when necessary, reducing power consumption.

```verilog
\m5_TLV_version 1d: tl-x.org
\m5
   // =================================================
   // Welcome!  New to Makerchip? Try the "Learn" menu.
   // =================================================
   
   //use(m5-1.0)   /// uncomment to use M5 macro library.
\SV
	`include "sqrt32.v"
   // Macro providing required top-level module definition, random
   // stimulus support, and Verilator config.
   m5_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV
   |calc
      @1
         $reset = *reset;
         $clk_phan = *clk;
      ?$valid
         @1
            $aa_sq[31:0] = $aa[3:0] * $aa[3:0];
            $bb_sq[31:0] = $bb[3:0] * $bb[3:0];
         @2
            $cc_sq[31:0] = $aa_sq + $bb_sq;
         @3
            $cc[31:0] = sqrt($cc_sq);
            //@4
            //$tot_dist[63:0] = $reset ? 0 : $valid ? (>>1$tot_dist + $cc) : >>1$tot_dist;
            //@4
            //$adder[31:0] = $cc + >>1$tot_dist;
            //@5
            //$tot_dist[31:0] = $valid ? ( >>1$tot_dist + $adder ) : >>1$tot_dist

   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 16'd30;
   *failed = 1'b0;
\SV
   endmodule
```

📊 Output waveform:
![4](https://github.com/user-attachments/assets/a984e17e-37db-4676-b4bf-d691e078a95a)

## 📏 Total Distance Calculator

The total distance calculator computes the cumulative distance traveled in a series of hops.

```verilog
\m5_TLV_version 1d: tl-x.org
\m5
   // =================================================
   // Welcome!  New to Makerchip? Try the "Learn" menu.
   // =================================================
   
   //use(m5-1.0)   /// uncomment to use M5 macro library.
\SV
	`include "sqrt32.v"
   // Macro providing required top-level module definition, random
   // stimulus support, and Verilator config.
   m5_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV
   |calc
      @1
         $reset = *reset;
         $clk_phan = *clk;
      ?$valid
         @1
            $aa_sq[31:0] = $aa[3:0] * $aa[3:0];
            $bb_sq[31:0] = $bb[3:0] * $bb[3:0];
         @2
            $cc_sq[31:0] = $aa_sq + $bb_sq;
         @3
            $cc[31:0] = sqrt($cc_sq);
         @4
            $tot_dist[63:0] = $reset ? 0 : $valid ? (>>1$tot_dist + $cc) : >>1$tot_dist;

   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 16'd30;
   *failed = 1'b0;
\SV
   endmodule
```

📊 Output waveform:
![5](https://github.com/user-attachments/assets/e5ecd844-c29f-4fc5-9d92-46fd86b88ae1)

## 🔄✅ Validity on Cycle Calculator

Implementing validity on the cycle calculator:

```verilog
\m5_TLV_version 1d: tl-x.org
\m5
   
   // =================================================
   // Welcome!  New to Makerchip? Try the "Learn" menu.
   // =================================================
   
   //use(m5-1.0)   /// uncomment to use M5 macro library.
\SV
   // Macro providing required top-level module definition, random
   // stimulus support, and Verilator config.
   m5_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV
   //$count[31:0] = 32'b0;
   |calc
      @1
         $clk_phan = *clk;
         $reset = *reset;
         $valid = $reset ? 0 : (>>1$valid + 1);
         $valid_or_reset = $valid || $reset;
      ?$valid
         @1
            $val1[31:0] = >>2$result[31:0];
            $val2[31:0] = $rand2[3:0];
         @2
            $out[31:0] = $valid_or_reset ? 32'b0 : ($sel[1:0] == 2'b00) ? ($val1[31:0] + $val2[31:0]) : ($sel[1:0] == 2'b01) ? ($val1[31:0] - $val2[31:0]) : ($sel[1:0] == 2'b10) ? ($val1[31:0] * $val2[31:0]) : ($sel[1:0] == 2'b11) ? ($val2[31:0] != 0 ? ($val1[31:0] / $val2[31:0]) : 32'bx) :  32'b0;
   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
\SV
   endmodule
```

📊 Output waveform:
![6](https://github.com/user-attachments/assets/dd25bf69-cf0f-4867-819e-286925c9beb6)

# 🖥️ RISC-V Processor Implementation Guide

## 🏗️ Basic RISC-V Architecture

The basic RISC-V architecture consists of the following components:

1. 🔢 **Program Counter**: Tracks the current instruction being executed
2. 💾 **Instruction Memory**: Stores program instructions
3. 🔍 **Instruction Decode**: Extracts instruction fields
4. 📁 **Register File**: Stores operands and results
5. ➕ **Arithmetic Logic Unit (ALU)**: Performs arithmetic and logical operations
6. ✍️ **Register File Write**: Writes results back to the register file
7. 🔀 **Branch Logic**: Handles branch instructions

📊 Implementation diagram:
![RISC-V Implementation](https://github.com/user-attachments/assets/05954d38-47b7-46e5-9ea8-42907c2c61b6)

## 1. Program Counter 🔢

The program counter (PC) is a crucial component that keeps track of the next instruction to be executed. It typically increments by 4 to fetch the next instruction from memory.

📊 Program Counter Behavior:
- Normal operation: PC += 4
- On reset: PC = 0

### Implementation:

```verilog
$pc[31:0] = >>1$reset ? 0 : (>>1$pc + 31'h4);
```

![7](https://github.com/user-attachments/assets/63637a9d-46a5-4992-a546-4ee51a25e461)

## 2. Instruction Memory 📚

The instruction memory holds the program instructions. The PC points to the address of the next instruction to be fetched.

### Fetching Instructions:

```verilog
$imem_rd_en = >>1$reset ? 0 : 1;
$imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
$instr[31:0] = $imem_rd_data[31:0];
```
![8](https://github.com/user-attachments/assets/42c2f863-d283-4fa1-8de5-9c960edfafbf)

## 3. Instruction Decoding 🧩

Decoding determines the type of instruction based on the opcode and other fields.

### Instruction Type Decoding:

```verilog
$is_i_instr = $instr[6:2] ==? 5'b0000x || /* ... */;
$is_r_instr = $instr[6:2] ==? 5'b01011 || /* ... */;
// ... (other instruction types)
```

![9](https://github.com/user-attachments/assets/f22017e6-912c-4433-887a-95dd9138268d)

## 4. Immediate Value Decoding 🔢

Immediate values are constants encoded within the instruction. The decoding process extracts and sign-extends these values.

### Immediate Decoding Logic:

```verilog
$imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
              $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
              // ... (other instruction types)
```

![10](https://github.com/user-attachments/assets/f71dda46-617c-445e-a357-90b0b5433dbb)

## 5. Other Field Decoding 🏷️

Decoding other instruction fields such as register addresses and function codes.

```verilog
$rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
?$rs2_valid
   $rs2[4:0] = $instr[24:20];
// ... (other fields)
```

![11](https://github.com/user-attachments/assets/5ead09bd-ada4-40d0-8914-5cee92c4a26f)

## 6. Individual Instruction Decoding 🔍

Identifying specific instructions based on their unique encoding.

```verilog
$dec_bits [10:0] = {$funct7[5], $funct3, $opcode};
$is_beq = $dec_bits ==? 11'bx_000_1100011;
$is_bne = $dec_bits ==? 11'bx_001_1100011;
// ... (other instructions)
```

![12](https://github.com/user-attachments/assets/febf67c3-d599-4971-b32b-a429477025f7)

## 7. Register File Operations 📂

### Reading from Registers:

```verilog
$rf_rd_en1 = $rs1_valid;
$rf_rd_index1[4:0] = $rs1;
// ... (similar for second read port)
```
![13](https://github.com/user-attachments/assets/449d3400-b0a9-4ba3-9eb8-62d29568fe8c)

### Writing to Registers:

```verilog
$rf_wr_en = $rd_valid && $rd != 5'b0;
$rf_wr_index[4:0] = $rd;
$rf_wr_data[31:0] = $result;
```

![14](https://github.com/user-attachments/assets/05a8e150-8415-46e5-bbd2-3817f84d240b)

## 8. Arithmetic Logic Unit (ALU) 🧮

Performs arithmetic and logical operations based on the instruction.

```verilog
$result[31:0] = $is_addi ? $src1_value + $imm :
                $is_add ? $src1_value + $src2_value :
                32'bx ;
```

![15](https://github.com/user-attachments/assets/0708a1fa-ded3-4355-8de5-69a5a11e8694)

## 9. Branch Instructions 🔀

Handling conditional jumps in the program flow.

```verilog
$taken_branch = $is_beq ? ($src1_value == $src2_value) :
                $is_bne ? ($src1_value != $src2_value) :
                // ... (other branch conditions)
$br_target_pc[31:0] = $pc + $imm;
```
![16](https://github.com/user-attachments/assets/12843dd8-72ed-44ec-94c9-7af93eaa49f9)

## 10. Testbench Verification ✅

Verifying the correctness of the implementation:

```verilog
*passed = |cpu/xreg[10]>>5$value == (1+2+3+4+5+6+7+8+9);
```

![Picture1](https://github.com/user-attachments/assets/e20dfb81-1e33-4f54-bf90-3c2894324349)


---

💡 Note: This guide provides a high-level overview of a RISC-V processor implementation. For a complete and functional design, additional components and more detailed logic would be required.


# Pipelining the CPU 🔗
The CPU core has now been pipelined, which allows for easy retiming and reduces functional bugs to a great extent. Pipelining enables faster computation. To implement pipelining, we simply need to add `@1`, `@2`, and so on. The snapshot of the pipelining is shown below. In TL Verilog, another advantage is that the systematic definition of the pipeline is not necessary.

## Lab on 3-Cycle Valid Signal 🔍
### Code
```c
$valid = $reset ? 1'b0 : ($start) ? 1'b1 : (>>3$valid);
$start_int = $reset ? 1'b0 : 1'b1;
$start = $reset ? 1'b0 : ($start_int && !>>1$start_int);
```

## Lab for Generating Valid Signals for Each Instruction 🔖
### Code
```c
//Generate valid signals for each instruction fields
$rs1_or_funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
$rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
$rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
$funct7_valid = $is_r_instr;
```

# Completing the RISC-V CPU 🚀
### Block Diagram
![CPU Block Diagram](https://github.com/user-attachments/assets/4c91e25b-79c3-43e7-bced-b3c11913e2e6)

## Code
```c
\m4_TLV_version 1d: tl-x.org
\SV
   // Template code can be found in: https://github.com/stevehoover/RISC-V_MYTH_Workshop
   
   m4_include_lib(['https://raw.githubusercontent.com/BalaDhinesh/RISC-V_MYTH_Workshop/master/tlv_lib/risc-v_shell_lib.tlv'])

\SV
   m4_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV

   // /====================\
   // | Sum 1 to 10 Program |
   // \====================/
   //
   // Add 1,2,3,...,10 (in that order).
   //
   // Regs:
   //  r10 (a0): In: 0, Out: final sum
   //  r12 (a2): 10
   //  r13 (a3): 1..10
   //  r14 (a4): Sum
   // 
   // External to function:
   m4_asm(ADD, r10, r0, r0)             // Initialize r10 (a0) to 0.
   // Function:
   m4_asm(ADD, r14, r10, r0)            // Initialize sum register a4 with 0x0
   m4_asm(ADDI, r12, r10, 1010)         // Store count of 10 in register a2.
   m4_asm(ADD, r13, r10, r0)            // Initialize intermediate sum register a3 with 0
   // Loop:
   m4_asm(ADD, r14, r13, r14)           // Incremental addition
   m4_asm(ADDI, r13, r13, 1)            // Increment intermediate register by 1
   m4_asm(BLT, r13, r12, 1111111111000) // If a3 is less than a2, branch to label named <loop>
   m4_asm(ADD, r10, r14, r0)            // Store final result to register a0 so that it can be read by main program
   m4_asm(SW, r0, r10, 10000)           // Store r10 result in dmem
   m4_asm(LW, r17, r0, 10000)           // Load contents of dmem to r17
   m4_asm(JAL, r7, 00000000000000000000) // Done. Jump to itself (infinite loop). (Up to 20-bit signed immediate plus implicit 0 bit (unlike JALR) provides byte address; last immediate bit should also be 0)
   m4_define_hier(['M4_IMEM'], M4_NUM_INSTRS)

   |cpu
      @0
         $reset = *reset;
         $clk_phan = *clk;
         
         //PC fetch - branch, jumps and loads introduce 2 cycle bubbles in this pipeline
         $pc[31:0] = >>1$reset ? '0 : (>>3$valid_taken_br ? >>3$br_tgt_pc :
                                       >>3$valid_load     ? >>3$inc_pc[31:0] :
                                       >>3$jal_valid      ? >>3$br_tgt_pc :
                                       >>3$jalr_valid     ? >>3$jalr_tgt_pc :
                                                     (>>1$inc_pc[31:0]));
         // Access instruction memory using PC
         $imem_rd_en = ~ $reset;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         
         
      @1
         //Getting instruction from IMem
         $instr[31:0] = $imem_rd_data[31:0];
         
         //Increment PC
         $inc_pc[31:0] = $pc[31:0] + 32'h4;
         
         //Decoding I,R,S,U,B,J type of instructions based on opcode [6:0]
         //Only [6:2] is used here because this implementation is for RV64I which does not use [1:0]
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                       $instr[6:2] ==? 5'b001x0 ||
                       $instr[6:2] == 5'b11001;
         
         $is_r_instr = $instr[6:2] == 5'b01011 ||
                       $instr[6:2] ==? 5'b011x0 ||
                       $instr[6:2] == 5'b10100;
         
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         
         $is_b_instr = $instr[6:2] == 5'b11000;
         
         $is_j_instr = $instr[6:2] == 5'b11011;
         
         //Immediate value decode
         $imm[31:0] = $is_i_instr ? { {21{$instr[31]}} , $instr[30:20]} :
                      $is_s_instr ? { {21{$instr[31]}} , $instr[30:25] , $instr[11:8] , $instr[7]} :
                      $is_b_instr ? { {20{$instr[31]}} , $instr[7] , $instr[30:25] , $instr[11:8] , 1'b0} :
                      $is_u_instr ? { $instr[31] , $instr[30:12] , { 12{1'b0}} } :
                      $is_j_instr ? { {12{$instr[31]}} , $instr[19:12] , $instr[20] , $instr[30:21] , 1'b0} :
                      >>1$imm[31:0];
         
         //Generate valid signals for each instruction fields
         $rs1_or_funct3_valid    = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $rs2_valid              = $is_r_instr || $is_s_instr || $is_b_instr;
         $rd_valid               = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct7_valid           = $is_r_instr;
         
         //Decode other fields of instruction - source and destination registers, funct, opcode
         ?$rs1_or_funct3_valid
            $rs1[4:0]    = $instr[19:15];
            $funct3[2:0] = $instr[14:12];
         
         ?$rs2_valid
            $rs2[4:0]    = $instr[24:20];
         
         ?$rd_valid
            $rd[4:0]     = $instr[11:7];
         
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         
         $opcode[6:0] = $instr[6:0];
         
         //Decode instruction in subset of base instruction set based on RISC-V 32I
         $dec_bits[10:0] = {$funct7[5],$funct3,$opcode};
         
         //Branch instructions
         $is_beq   = $dec_bits ==? 11'bx_000_1100011;
         $is_bne   = $dec_bits ==? 11'bx_001_1100011;
         $is_blt   = $dec_bits ==? 11'bx_100_1100011;
         $is_bge   = $dec_bits ==? 11'bx_101_1100011;
         $is_bltu  = $dec_bits ==? 11'bx_110_1100011;
         $is_bgeu  = $dec_bits ==? 11'bx_111_1100011;
         
         //Jump instructions
         $is_auipc = $dec_bits ==? 11'bx_xxx_0010111;
         $is_jal   = $dec_bits ==? 11'bx_xxx_1101111;
         $is_jalr  = $dec_bits ==? 11'bx_000_1100111;
         
         //Arithmetic instructions
         $is_addi  = $dec_bits ==? 11'bx_000_0010011;
         $is_add   = $dec_bits ==  11'b0_000_0110011;
         $is_lui   = $dec_bits ==? 11'bx_xxx_0110111;
         $is_slti  = $dec_bits ==? 11'bx_010_0010011;
         $is_sltiu = $dec_bits ==? 11'bx_011_0010011;
         $is_xori  = $dec_bits ==? 11'bx_100_0010011;
         $is_ori   = $dec_bits ==? 11'bx_110_0010011;
         $is_andi  = $dec_bits ==? 11'bx_111_0010011;
         $is_slli  = $dec_bits ==? 11'b0_001_0010011;
         $is_srli  = $dec_bits ==? 11'b0_101_0010011;
         $is_srai  = $dec_bits ==? 11'b1_101_0010011;
         $is_sub   = $dec_bits ==? 11'b1_000_0110011;
         $is_sll   = $dec_bits ==? 11'b0_001_0110011;
         $is_slt   = $dec_bits ==? 11'b0_010_0110011;
         $is_sltu  = $dec_bits ==? 11'b0_011_0110011;
         $is_xor   = $dec_bits ==? 11'b0_100_0110011;
         $is_srl   = $dec_bits ==? 11'b0_101_0110011;
         $is_sra   = $dec_bits ==? 11'b1_101_0110011;
         $is_or    = $dec_bits ==? 11'b0_110_0110011;
         $is_and   = $dec_bits ==? 11'b0_111_0110011;
         
         //Store instructions
         $is_sb    = $dec_bits ==? 11'bx_000_0100011;
         $is_sh    = $dec_bits ==? 11'bx_001_0100011;
         $is_sw    = $dec_bits ==? 11'bx_010_0100011;
         
         //Load instructions - support only 4 byte load
         $is_load  = $dec_bits ==? 11'bx_xxx_0000011;
         
         $is_jump = $is_jal || $is_jalr;
         
      @2
         //Get Source register values from reg file
         $rf_rd_en1 = $rs1_or_funct3_valid;
         $rf_rd_en2 = $rs2_valid;
         
         $rf_rd_index1[4:0] = $rs1[4:0];
         $rf_rd_index2[4:0] = $rs2[4:0];
         
         //Register file bypass logic - data forwarding from ALU to resolve RAW dependence
         $src1_value[31:0] = $rs1_bypass ? >>1$result[31:0] : $rf_rd_data1[31:0];
         $src2_value[31:0] = $rs2_bypass ? >>1$result[31:0] : $rf_rd_data2[31:0];
         
         //Branch target PC computation for branches and JAL
         $br_tgt_pc[31:0] = $imm[31:0] + $pc[31:0];
         
         //RAW dependence check for ALU data forwarding
         //If previous instruction was writing to reg file, and current instruction is reading from same register
         $rs1_bypass = >>1$rf_wr_en && (>>1$rd == $rs1);
         $rs2_bypass = >>1$rf_wr_en && (>>1$rd == $rs2);
         
      @3
         //ALU
         $result[31:0] = $is_addi  ? $src1_value +  $imm :
                         $is_add   ? $src1_value +  $src2_value :
                         $is_andi  ? $src1_value &  $imm :
                         $is_ori   ? $src1_value |  $imm :
                         $is_xori  ? $src1_value ^  $imm :
                         $is_slli  ? $src1_value << $imm[5:0]:
                         $is_srli  ? $src1_value >> $imm[5:0]:
                         $is_and   ? $src1_value &  $src2_value:
                         $is_or    ? $src1_value |  $src2_value:
                         $is_xor   ? $src1_value ^  $src2_value:
                         $is_sub   ? $src1_value -  $src2_value:
                         $is_sll   ? $src1_value << $src2_value:
                         $is_srl   ? $src1_value >> $src2_value:
                         $is_sltu  ? $sltu_rslt[31:0]:
                         $is_sltiu ? $sltiu_rslt[31:0]:
                         $is_lui   ? {$imm[31:12], 12'b0}:
                         $is_auipc ? $pc + $imm:
                         $is_jal   ? $pc + 4:
                         $is_jalr  ? $pc + 4:
                         $is_srai  ? ({ {32{$src1_value[31]}} , $src1_value} >> $imm[4:0]) :
                         $is_slt   ? (($src1_value[31] == $src2_value[31]) ? $sltu_rslt : {31'b0, $src1_value[31]}):
                         $is_slti  ? (($src1_value[31] == $imm[31]) ? $sltiu_rslt : {31'b0, $src1_value[31]}) :
                         $is_sra   ? ({ {32{$src1_value[31]}}, $src1_value} >> $src2_value[4:0]) :
                         $is_load  ? $src1_value +  $imm :
                         $is_s_instr ? $src1_value + $imm :
                                    32'bx;
         
         $sltu_rslt[31:0]  = $src1_value <  $src2_value;
         $sltiu_rslt[31:0] = $src1_value <  $imm;
         
         //Jump instruction target PC computation
         $jalr_tgt_pc[31:0] = $imm[31:0] + $src1_value[31:0]; 
         
         //Branch resolution
         $taken_br = $is_beq ? ($src1_value == $src2_value) :
                     $is_bne ? ($src1_value != $src2_value) :
                     $is_blt ? (($src1_value < $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                     $is_bge ? (($src1_value >= $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                     $is_bltu ? ($src1_value < $src2_value) :
                     $is_bgeu ? ($src1_value >= $src2_value) :
                     1'b0;
         
         //Current instruction is valid if one of the previous 2 instructions were not (taken_branch or load or jump)
         $valid = ~(>>1$valid_taken_br || >>2$valid_taken_br || >>1$is_load || >>2$is_load || >>2$jump_valid || >>1$jump_valid);
         
         //Current instruction is valid & is a taken branch
         $valid_taken_br = $valid && $taken_br;
         
         //Current instruction is valid & is a load
         $valid_load = $valid && $is_load;
         
         //Current instruction is valid & is jump
         $jump_valid = $valid && $is_jump;
         $jal_valid  = $valid && $is_jal;
         $jalr_valid = $valid && $is_jalr;
         
         //Destination register update - ALU result or load result depending on instruction
         $rf_wr_en = (($rd != '0) && $rd_valid && $valid) || >>2$valid_load;
         $rf_wr_index[4:0] = $valid ? $rd[4:0] : >>2$rd[4:0];
         $rf_wr_data[31:0] = $valid ? $result[31:0] : >>2$ld_data[31:0];
         
      @4
         //Data memory access for load, store
         $dmem_addr[3:0]     =  $result[5:2];
         $dmem_wr_en         =  $valid && $is_s_instr;
         $dmem_wr_data[31:0] =  $src2_value[31:0];
         $dmem_rd_en         =  $valid_load;
         
      
         //Write back data read from load instruction to register
         $ld_data[31:0]      =  $dmem_rd_data[31:0];
         
      
      

      // Note: Because of the magic we are using for visualisation, if visualisation is enabled below,
      //       be sure to avoid having unassigned signals (which you might be using for random inputs)
      //       other than those specifically expected in the labs. You'll get strange errors for these.

   
   // Assert these to end simulation (before Makerchip cycle limit).
   //Checks if sum of numbers from 1 to 9 is obtained in reg[17] and runs 10 cycles extra after this is met
   *passed = |cpu/xreg[17]>>10$value == (1+2+3+4+5+6+7+8+9);
   //Run for 200 cycles without any checks
   //*passed = *cyc_cnt > 200;
   *failed = 1'b0;
   
   // Macro instantiations for:
   //  o instruction memory
   //  o register file
   //  o data memory
   //  o CPU visualization
   |cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@2, @3)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+dmem(@4)    // Args: (read/write stage)
   
   m4+cpu_viz(@4)    // For visualisation, argument should be at least equal to the last stage of CPU logic
                       // @4 would work for all labs
\SV
   endmodule
```

## Simulation Passed ✅
![log](https://github.com/user-attachments/assets/ddc9cc82-6804-4ccb-8316-13cabd26f54b)

## Diagram �blueprint:
![block](https://github.com/user-attachments/assets/db10b6ad-afdb-4a0a-83cc-ded99836b3ba)

## Waveform 📊
![wave ](https://github.com/user-attachments/assets/8b2bbb4a-f75b-41bc-a501-667408b2b877)

## Visualization 🔍
![viz](https://github.com/user-attachments/assets/d541f8b7-bf46-493c-94da-bf724c64370d)
