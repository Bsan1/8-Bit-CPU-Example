# CNG331 Computer Organization

An 8-bit processor built in Logisim, starting from individual arithmetic circuits and ending with a single-cycle CPU.

## 8-bit ALU

The ALU is assembled from custom subcircuits instead of relying on ready-made arithmetic blocks. It supports addition, bitwise AND/OR, and bit rotation. Separate circuits handle two's-complement conversion, equality comparison, rotation, and full addition.

The output includes zero, sign, carry, overflow, and equality flags. Test vectors were used to verify the subcircuits and the complete ALU.

## Register file and memory

The processor uses eight 8-bit registers, ROM for instructions, and RAM for data. A control unit selects ALU operations, register write-back sources, memory reads and writes, and immediate operands. Instructions are encoded in a custom 21-bit format.

## Single-cycle CPU

The final processor adds branching, jumps, jump-and-link, jump-register, and set-less-than operations. Extra multiplexers select the next program-counter value and destination register. Each instruction completes in one clock cycle.

## Included circuits

```text
Part1/All_Circuits_FIXED.circ   ALU and supporting circuits
Part3/8bitCPU_FIXED.circ        Complete single-cycle processor
```

## Technology

- Logisim
- Digital logic design
- CPU datapath and control design

## Author

Barış Şan
