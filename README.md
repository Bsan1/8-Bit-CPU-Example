# 8-Bit Processor Design

A set of Logisim circuits developed to understand how a processor grows from small arithmetic components into a complete single-cycle datapath.

## ALU design

The 8-bit arithmetic logic unit supports addition, AND, OR, and bit rotation. It also produces zero, sign, carry, overflow, and equality flags. Building these operations from smaller circuits provides practical experience with binary representation, adders, multiplexers, comparators, and processor status flags.

```text
Opcode  Operation
00      ADD
01      AND
10      OR
11      ROTATE
```

## Processor core

The processor core combines eight 8-bit registers with instruction memory, data memory, and a control unit. Its custom 21-bit instruction format supports arithmetic, load and store operations, immediate values, conditional branches, jumps, jump-and-link, jump-register, and set-less-than.

This stage focuses on instruction encoding, register addressing, control-signal generation, memory access, and write-back behavior.

## Single-cycle processor

The final circuit connects the datapath and control logic so that each instruction completes in one clock cycle. It demonstrates how the program counter, register file, ALU, memory, and control unit cooperate during instruction execution.

```text
Instruction -> Control Unit -> Register File -> ALU -> Memory -> Write-back
```

## Project files

```text
ALU-Design/ALU-Circuits.circ
Processor-Core/Processor-Core.circ
Single-Cycle-Processor/Single-Cycle-Processor.circ
```

## Contributor

Barış Şan
