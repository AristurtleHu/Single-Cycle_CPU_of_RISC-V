# Project 2.1: Single-Cycle CPU Implementation

## Task Description

Implement a single-cycle CPU capable of processing the instructions specified in the Instruction Set section below.

## The Instruction Set

The instructions you need to implement are shown in the table below:

| Format | Instruction | Implementation                                     |
| :----- | :---------- | :------------------------------------------------- |
| R      | `add`       | `x[rd] = x[rs1] + x[rs2]`                          |
| R      | `sra`       | `x[rd] = x[rs1] >>s x[rs2]`                        |
| R      | `slt`       | `x[rd] = (x[rs1] <s x[rs2]) ? 1 : 0`               |
| I      | `srli`      | `x[rd] = x[rs1] >>u shamt`                         |
| I      | `sltiu`     | `x[rd] = (x[rs1] <u sext(immediate)) ? 1 : 0`      |
| I      | `andi`      | `x[rd] = x[rs1] & sext(immediate)`                 |
| I      | `addi`      | `x[rd] = x[rs1] + sext(immediate)`                 |
| I      | `lw`        | `x[rd] = sext(M[x[rs1] + sext(offset)][31:0])`     |
| I      | `lh`        | `x[rd] = sext(M[x[rs1] + sext(offset)][15:0])`     |
| I      | `jalr`      | `t =pc+4; pc=(x[rs1]+sext(offset))&~1; x[rd]=t`    |
| U      | `auipc`     | `x[rd] = pc + sext(immediate[31:12] << 12)`        |
| U      | `lui`       | `x[rd] = sext(immediate[31:12] << 12)`             |
| S      | `sw`        | `M[x[rs1] + sext(offset)] = x[rs2][31:0]`          |
| S      | `sh`        | `M[x[rs1] + sext(offset)] = x[rs2][15:0]`          |
| J      | `jal`       | `x[rd] = pc+4; pc += sext(offset)`                 |
| B      | `beq`       | `if (x[rs1] == x[rs2]) pc += sext(offset)`         |

**Notes:**

*   `x[n]` refers to register `n`.
*   `pc` is the program counter.
*   `M[addr]` refers to memory at address `addr`.
*   `sext()` denotes sign extension.
*   `>>s` denotes arithmetic right shift.
*   `>>u` denotes logical right shift.
*   `<s` denotes signed comparison.
*   `<u` denotes unsigned comparison.
*   `shamt` is the 5-bit shift amount from the I-type instruction.
*   `offset` refers to the immediate value used in load, store, branch, and jump instructions, appropriately sign-extended.
*   `immediate` refers to the immediate value from the instruction format.
*   `&~1` ensures the target address for `jalr` is 2-byte aligned.
