# 8-Bit CPU Example

A processor built in Logisim from custom arithmetic circuits, registers, memory, and control logic.

## ALU

The 8-bit ALU supports addition, AND, OR, and bit rotation. It also produces zero, sign, carry, overflow, and equality flags.

```text
Opcode  Operation
00      ADD
01      AND
10      OR
11      ROTATE
```

## Processor

The CPU has eight 8-bit registers, ROM instruction memory, RAM data memory, and a custom 21-bit instruction format. The final datapath supports arithmetic, load/store, immediate values, branches, jumps, jump-and-link, jump-register, and set-less-than.

```text
Instruction -> Control Unit -> Register File -> ALU -> Memory/Write-back
```

## Circuit files

```text
Part1/ALU-Circuits.circ   ALU and supporting circuits
Part3/8bitCPU.circ        Single-cycle processor
```

## Author

Barış Şan
