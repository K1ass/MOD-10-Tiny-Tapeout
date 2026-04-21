<!---

This file is used to generate your project datasheet. Please fill in the information below and delete any unused
sections.

You can also include images in this folder and reference them in the markdown. Each image must be less than
512 kb in size, and the combined size of all images must be less than 1 MB.
-->

## How it works

This design implements a MOD-10 (decade) counter using four D flip-flops.

Each flip-flop represents one bit of the current state:
Q3 (MSB), Q2, Q1, Q0 (LSB)

The counter follows a sequence from decimal 0 (0000) to 9 (1001), then resets.

---

### State Transition Table

| Decimal | Q3 | Q2 | Q1 | Q0 | D3 | D2 | D1 | D0 |
|--------|----|----|----|----|----|----|----|----|
|   0    | 0  | 0  | 0  | 0  | 0  | 0  | 0  | 1  |
|   1    | 0  | 0  | 0  | 1  | 0  | 0  | 1  | 0  |
|   2    | 0  | 0  | 1  | 0  | 0  | 0  | 1  | 1  |
|   3    | 0  | 0  | 1  | 1  | 0  | 1  | 0  | 0  |
|   4    | 0  | 1  | 0  | 0  | 0  | 1  | 0  | 1  |
|   5    | 0  | 1  | 0  | 1  | 0  | 1  | 1  | 0  |
|   6    | 0  | 1  | 1  | 0  | 0  | 1  | 1  | 1  |
|   7    | 0  | 1  | 1  | 1  | 1  | 0  | 0  | 0  |
|   8    | 1  | 0  | 0  | 0  | 1  | 0  | 0  | 1  |
|   9    | 1  | 0  | 0  | 1  | 0  | 0  | 0  | 0  |

Note:
- The D inputs represent the next state.
- Since D flip-flops follow: Q(next) = D, this table directly drives the design.

---

### Logic Behavior

- D0 toggles every clock cycle
- D1 toggles when Q0 = 1
- D2 toggles when Q1 AND Q0 = 1
- D3 toggles when Q2 AND Q1 AND Q0 = 1

---

### Reset Logic (MOD-10)

To prevent counting beyond 9:

RESET = Q3 AND Q1

When the counter reaches an invalid state (1010):
- RESET is triggered
- All flip-flops are cleared to 0000

---

### Final Sequence

0000 → 0001 → 0010 → 0011 → 0100 → 0101 → 0110 → 0111 → 1000 → 1001 → 0000


## How to test

1. Apply Clock Signal
- Connect a clock to all D flip-flops

2. Initialize Circuit
- Reset outputs to 0000

3. Observe Outputs
- Monitor Q3 Q2 Q1 Q0 using LEDs or waveform viewer

4. Verify Counting

Expected sequence:

0000
0001
0010
0011
0100
0101
0110
0111
1000
1001
0000

5. Verify Reset
- Ensure the counter does NOT go to 1010
- It should reset immediately after 1001

---

## Debug Tips

- Counts beyond 1001 → reset logic incorrect
- Incorrect transitions → check D input connections
- No counting → check clock signal

