# LEC2 : Designing Complex Logic Gates(LEC 1 EXTENSION)

## AND Gate using NAND and NOT Gates

A standard AND gate can be created by following a NAND gate with an Inverter (NOT gate). This effectively implements the logic $\overline{\text{NAND}(A, B)} = \text{AND}(A, B)$.

* **Symbol Diagram:** (Insert diagram with NAND gate followed by an Inverter)
* **Truth Table:**

| Input A | Input B | Intermediate Output (A NAND B) | Final Output Y (A AND B) |
|---|---|---|---|
| 0 | 0 | 1 | 0 |
| 0 | 1 | 1 | 0 |
| 1 | 0 | 1 | 0 |
| 1 | 1 | 0 | 1 |

* **Transistor Diagram:** (Insert diagram showing CMOS NAND gate linked to CMOS Inverter)
    * The output of the CMOS NAND gate (using inputs A and B) becomes the single input for the CMOS Inverter.
    * The final output is taken from the output of the inverter.

**General Rule for Constructing Any Inverting Logic Gate:**

* **Diagram of General Form:** (Insert Block Diagram)
    * **Inputs:** Connected to both the pMOS and nMOS networks.
    * **pMOS pull-up network:** Consists of parallel combinations of pMOS transistors. This network "pulls up" the output to VDD (logic 1).
    * **nMOS pull-down network:** Consists of series combinations of nMOS transistors. This network "pulls down" the output to Ground (logic 0).
    * **Output:** The point between the pMOS and nMOS networks.

**Rules for CMOS Circuit Design:**

* **Network Composition:** A network can consist of transistors in series or in parallel.
* **Rule 1 - Parallel Network:** A parallel network is ON (closed circuit) if **at least one** of its transistors is ON.
* **Rule 2 - Series Network:** A series network is ON (closed circuit) **only if all** its transistors are ON.
* **Rule 3 - Single Path:** For any given input combination, **exactly one** of the two networks (pMOS or nMOS) must be ON, and the other must be OFF.
    * There should always be a single path from the output to either VDD or Ground, never to both or neither.


# Advanced Digital Design Topics

## Circuit Design Considerations and Limitations

When designing logic circuits with transistor networks, two undesirable conditions must be carefully avoided:

1.  **Short Circuit:** Occurs when both the pMOS (pull-up) and nMOS (pull-down) networks are ON simultaneously. This creates a direct path from VDD to Ground, causing excessive current flow and likely incorrect logic operation or damage to the circuit.
2.  **Floating Output:** Happens when both the pMOS and nMOS networks are OFF at the same time. In this state, the output is not connected to either VDD or Ground, resulting in an undefined voltage level. This condition is also known as a **high-impedance** state (Z).

## Boolean Algebra Canonical Forms: SOP and POS

Standard notation for Sum-of-Products (SOP) and Product-of-Sums (POS) forms:

* **Min-terms (m):** Represent logical AND combinations. A minterm is true only for one specific input combination.
* **Max-terms (M):** Represent logical OR combinations. A maxterm is false only for one specific input combination.

**Truth Table Example with 3 Inputs (A, B, C):**

| Input A | Input B | Input C | Output F | Minterms (SOP) | Maxterms (POS) |
|---|---|---|---|---|---|
| 0 | 0 | 0 | 0 | m0 | M0 |
| 0 | 0 | 1 | 0 | m1 | M1 |
| 0 | 1 | 0 | 0 | m2 | M2 |
| 0 | 1 | 1 | 1 | m3 | M3 |
| 1 | 0 | 0 | 1 | m4 | M4 |
| 1 | 0 | 1 | 1 | m5 | M5 |
| 1 | 1 | 0 | 1 | m6 | M6 |
| 1 | 1 | 1 | 1 | m7 | M7 |

**Sum-of-Products (SOP) Expression:** F is the sum of minterms where the output is 1.
$$F = \sum m(3, 4, 5, 6, 7) = m3 + m4 + m5 + m6 + m7$$
This form focuses on rows where the output is '1'.

**Product-of-Sums (POS) Expression:** F is the product of maxterms where the output is 0.
$$F = \prod M(0, 1, 2)$$
This form focuses on rows where the output is '0'.

## Decoder

A decoder is a fundamental digital component that detects a specific input pattern.

* **Function:** It takes an n-bit binary input and activates one of $2^n$ unique outputs.
* **Key Characteristic:** For any given input combination, **exactly one** output line is active (HIGH or 1), while all other output lines are inactive (LOW or 0). The active output line corresponds directly to the numerical value of the binary input.
* **Example: 2-to-4 Decoder:**
    * **Inputs:** 2 ($A, B$)
    * **Outputs:** 4 ($Y_0, Y_1, Y_2, Y_3$)
    * If input AB = 00, output $Y_0$ is 1.
    * If input AB = 01, output $Y_1$ is 1.
    * If input AB = 10, output $Y_2$ is 1.
    * If input AB = 11, output $Y_3$ is 1.