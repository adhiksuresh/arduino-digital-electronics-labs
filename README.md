# Arduino Digital Electronics Labs: Seven-Segment Display & BCD Counters

Lab exercises in combinational and sequential logic, implemented on an **Arduino Uno** and shown on a **seven-segment display**.
Each sketch writes the logic as Boolean equations (AND, OR, NOT) instead of using lookup tables or arithmetic, so the code follows the truth tables and Karnaugh-map (K-map) simplification directly.

> Coursework, 2022. Kept as a record of foundational digital-design work.

## What is covered

- Driving a seven-segment display through a **7447 BCD-to-seven-segment decoder**
- Driving a seven-segment display **directly** from Arduino pins, without a decoder
- **Decade (0–9) up and down counters** built from next-state Boolean equations
- **K-map minimisation**: the same counter and decoder written first in full (sum of minterms), then simplified using the unused states 10–15 as "don't care" terms

## Hardware

| Part | Purpose |
|---|---|
| Arduino Uno | Runs the logic |
| 7447 IC | BCD-to-seven-segment decoder (active-low outputs) |
| Common-anode seven-segment display | Shows the digit |
| 4 switches or jumper wires | 4-bit input, for the sketches that read input |
| 220 Ω resistors | Current limiting for each segment |

### Pin map

| Arduino pin | Used for |
|---|---|
| 2, 3, 4, 5 | 7447 inputs A (LSB), B, C, D (MSB). For direct-drive sketches: segments a–g on pins 2–8 |
| 6, 7, 8, 9 | 4-bit input W (LSB), X, Y, Z (MSB) |
| 13 | On-board LED, blinks as a clock indicator in the counter sketches |

## Files

| File | What it does | Display method |
|---|---|---|
| `3.1` | Shows a fixed digit (5) by sending BCD `0101` | 7447 |
| `3.2` | Decade up counter 0→9, using full next-state equations | 7447 |
| `3.3` | Reads a 4-bit input from pins 6–9 and displays it | 7447 |
| `3.4` | Same as `3.3` (without the `Arduino.h` include) | 7447 |
| `3.5` | Reads a 4-bit input and displays input + 1 (mod 10) | 7447 |
| `3.7` | Decade counter, with segment equations written in full | Direct drive |
| `3.8` | Decade counter, with simplified next-state equations | 7447 |
| `3.9` | Decade counter, with partly simplified segment equations | Direct drive |
| `4.6` | Decade counter, fully simplified using don't-care states | 7447 |
| `4.8` | Decade counter, fully simplified segment equations (a lookup-table version is kept as a comment for comparison) | Direct drive |
| `up counter` | Reads the current state from pins 6–9 and outputs the next count (+1) | 7447 |
| `down counter` | Reads the current state from pins 6–9 and outputs the previous count (−1, 0→9) | 7447 |

The sketches move from **full equations** (`3.2`, `3.7`) to **simplified equations** (`3.8`, `3.9`, `4.6`, `4.8`), so you can compare them side by side.

## Notation used in the code

| Symbol | Meaning |
|---|---|
| `W X Y Z` | Present state / input bits (W = LSB) |
| `A B C D` | Next state / output bits (A = LSB) |
| `H I J K L M N` | Seven-segment outputs a–g (active low: `0` = segment ON) |
| `&&` `\|\|` `!` | AND, OR, NOT |

## How to run

1. Install the [Arduino IDE](https://www.arduino.cc/en/software).
2. Copy the code from a file into a new sketch. The files here have no `.ino` extension, so they can't be opened directly.
3. Wire the circuit using the pin map above.
4. Choose **Tools → Board → Arduino Uno**, then click **Upload**.

## License

The code comments state that it is released under the GNU GPL. See `LICENSE`.
