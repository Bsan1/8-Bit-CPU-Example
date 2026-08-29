# CNG331 Computer Organization

Logisim projects developed across a three-part processor design assignment. The work starts with an 8-bit ALU and builds toward a single-cycle 8-bit CPU.

## Project parts

### Part 1 - 8-bit ALU

The first part implements the main combinational building blocks of the processor:

- 2's-complement converter
- rotate-left and rotate-right circuits
- 8-bit full adder
- custom equality comparator
- 8-bit ALU with ADD, OR, AND, and rotate operations
- zero, sign, carry, overflow, and equality flags

The circuits were designed and tested in Logisim using the input/output names and test-vector format required by the assignment.

### Part 2 - Memory and register file

The second stage of the assignment introduced an eight-register file, ROM-based instruction memory, RAM-based data memory, a control unit, and a 21-bit instruction format. The supported instruction set included arithmetic, logical, load/store, and immediate operations.

### Part 3 - Single-cycle processor

The final stage extended the CPU with branching, jumps, jump-and-link, jump-register, and set-less-than operations. This required an expanded ALU, a new control unit, and additional multiplexers for program-counter and destination-register selection.

## Included files

```text
Part1/All_Circuits_FIXED.circ   Corrected Part 1 circuit collection
Part3/8bitCPU_FIXED.circ        Corrected single-cycle CPU
331_336_WHAT_WAS_FIXED.md       Verification and correction notes
```

The corrected control unit was checked against the assignment's control table, and the Part 1 subcircuits were verified with Logisim test vectors.

## Author

Barış Şan
