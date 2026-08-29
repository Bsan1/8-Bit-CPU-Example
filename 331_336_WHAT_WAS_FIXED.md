# What was fixed — 331 & 336

350 (Term Project) is **not included** — see the note at the bottom.

---

## 331 Computer Organization (Logisim)

### Part 1 — 8-bit ALU (`All_Circuits_FIXED.circ`)
**Bug:** the `SF` (sign) flag was wired from the `twosComplement` sub-circuit instead of from the actual result's sign bit, so `SF` computed "positive & nonzero" instead of "negative."
**Fix:** removed the stray `twosComplement` tap feeding the sign-bit splitter and wired the splitter directly from the real ALU result.
**Verified:** real headless Logisim run, `Alu8TestVector_CorrectSF.txt` — 7/7 pass. All other Part 1 sub-circuit vectors (twosComplement, rotr, FULLADDER8, customComparator) still pass 7/7 each — no regressions.

### Part 3 — Single-Cycle CPU, ControlUnit (`8bitCPU_FIXED.circ`)
Three bugs found and fixed, all in the `ControlUnit` sub-circuit:

1. **Mux1** was wired so a gate meant only for opcode `1110` was instead forcing `Mux1=11` for several unrelated opcodes too, corrupting the ALU-vs-PC+1 write-back selection for `AND`/`ROTL`/`SLT`. Added the correct minterm logic for `1110` and rewired the offending gate to source from it.
2. **WE** (register write-enable) used `NOT(op2 AND op3)` where the design needed `NOT(op2) AND NOT(op3)` — De Morgan's law was applied backwards, so `WE` was wrongly `1` for opcodes `0010`, `0111`, `1011` (store/branch/jump instructions that must not write a register). This also explains the student's own self-reported `jr $ra` infinite-loop bug (opcode `1101`/JR is one of the affected opcodes) — the fixes below very likely resolve that too. Added a dedicated OR-gate-then-NOT path (`NOT(op2 OR op3)`) rather than touching the shared AND-gate signal that other logic still correctly depends on.
3. **Branch** (BNE): the term for opcode `0111` tapped `EQ` directly instead of `NOT(EQ)`, so BNE branched when the compared values were *equal* instead of *unequal*. Added a NOT gate on that one tap.

**Verified:** real headless Logisim run against the authoritative spec vector (`ControlUnitTestVector.txt`, from the spec's Table 2.8 including "don't care" cells) — went from 10 failures (before any fix) to **15/15 passing** after all three fixes.

---

## 336 Microprocessors (AVR)

### HW1 (`hw1q2_FIXED.asm`)
- Boundary bug: `cpi R25, 100` / `brlo` implemented "< 100"; spec wants "≤ 100". Changed the compare value to 101 so the same `brlo` now means "≤ 100".
- Added the missing Normal-mode timer variant (`DELAY_025s_NORMAL`) alongside the existing CTC-mode one — the spec asks for both. This part is written fresh since only the CTC version existed; double-check it against your report's exact expected format.

### HW2 (`hw2_FIXED.asm`)
- The ISR toggles the LED pin once per timer compare match, so the compare interval is a *half*-period, not the full period. The original value (`0x1E85` = 7813 ticks ≈ 0.5s) made the toggle interval 0.5s, giving a 1.0s square-wave period — 2x the 0.5s spec target. Halved it to `0x0F42` (3906 ticks ≈ 0.25s toggle interval → 0.5s period).

### Lab 3, Task 5 / Module 1, Scenario 1 (`task5_FIXED.asm`, `module1_scenario1_fixed.asm`)
Both submissions share the same vote-counter code, so the same fix applies to both. **Bug:** all 8 `SBIC PINA,n` checks called `C1INC`, so only candidate 1 was ever counted. **Fix:** added `C2INC`...`C8INC`, each mirroring `C1INC`'s structure with its own register (R22–R28), its own memory address (0x101–0x107), and its own overflow-error handler, and wired each `PINA` bit to call its matching routine.

### Lab 4, Task 3 (`task3_FIXED.c`)
**Bug:** `PORTD &= !(1<<n)` uses logical-NOT instead of bitwise-NOT, so `!(1<<n)` is always `0` for every `n`, and each of those four lines clears the *entire* port instead of one bit. **Fix:** changed `!` to `~`.
**Verified at the compiled machine-code level** (avr-gcc + objdump): the original compiles those lines to `in r24,PORTD` / `out PORTD,r1` (r1 is the AVR zero register — an unconditional full-port clear); the fixed version compiles to `cbi PORTD,n` (a precise single-bit clear) for each of the four bits. Confirmed by diffing the disassembly of both builds.

### Module 1
- **Task 2** (`module1_task2_fixed.asm`): the divide-by-repeated-subtraction loop started its counter at `0x01` instead of `0xFF` (-1), giving quotient `10` instead of the correct `8` for 80/10 (off-by-two). Fixed the initial value to match the same, already-correct pattern the student used in Task 5's own loop. Hand-traced both before and after: before = 10, after = 8.
- **Task 4** (`module1_task4_fixed.asm`): the report's "Code Part" for this task was left completely blank (only the flowchart was submitted), so there was no existing code to fix — this is written fresh from the spec (sum three input-port values, show the sum on 8 LEDs, or light an error LED and blank the display if the sum overflows 8 bits). Port assignment (PINA/B/C in, PORTD out, PE0 error LED) is an assumption since the spec doesn't name exact ports — adjust to match your actual wiring/report diagram.
- **Scenario 1**: same vote-counter fix as Lab 3 Task 5 above (identical bug, identical fix).

All AVR files reassembled clean with `avra`/`avr-gcc` (no syntax/build errors).

---

## 350 — not included

Blocked: the Term Project source `.docx` files (SRS + SDD) aren't cached anywhere in this session — this fix only needs template cleanup (removing leftover "[Keep this sentence in the report]" text, filling title-page placeholders, writing the Glossary/References), but I need the actual files to do it. Once your computer is back online I can pull them directly, or you can attach the two `.docx` files here and I'll fix them right away.
