<!---

This file is used to generate your project datasheet. Please fill in the information below and delete any unused
sections.

You can also include images in this folder and reference them in the markdown. Each image must be less than
512 kb in size, and the combined size of all images must be less than 1 MB.
-->

## How it works

The design contains four identical 2:1 multiplexer slices built entirely from
NAND gates, all sharing a common select line SEL (`ui[7]`). Each slice picks
one of its two data inputs (A when SEL is high, B when SEL is low) using the
classic NAND-based mux structure `Y = NAND(NAND(A, S), NAND(S', B))`.

Every mux result is brought out as a differential (complementary) pair: an
XNOR output stage produces both the true output (Y) and the inverted output
(Y_N) for each slice, so the result is available in both polarities at the
same time.

Muxes 1–3 take their data inputs from the dedicated inputs `ui[0]`–`ui[5]`,
while mux 4 takes its data from the bidirectional pins `uio[0]` and `uio[1]`
(configured as inputs). `uio[2]` and `uio[3]` are polarity controls for the
XNOR input/output stages.

## How to test

In the Wokwi simulation, set the data inputs with the DIP switch and toggle
SEL (`ui[7]`); the four output pairs drive the segments of the 7-segment
display, so you can watch each Y/Y_N pair change complementarily.

On the demo board: apply logic levels to A/B data inputs (`ui[0]`–`ui[5]`),
choose the select value on `ui[7]`, and observe the outputs on `uo[0]`–`uo[7]`.
Each even/odd output pair must always carry complementary values, and which
input (A or B) appears on the outputs must follow SEL.

## External hardware

No external hardware is required. The Wokwi simulation uses DIP switches for
the inputs and a 7-segment display for the outputs; on the demo board the
on-board switches and LEDs are sufficient.
