# LEC1 : INTRODUCTION,FUNDMANETALS,TRANSISTOR,GATES
## INTRODUCTION:
### SAFARI RESERCH GROUP:
To enable fundamentally better computers in many aspects:
* Performance
* Effeciency
* Security
* Relaibility
* Safety


### Transformation Hirerachy:
* Problem
* Algorithm
* Language
* System Software
* Logic 
* Device


##  Introduction to Transistors :
**MOS Transistors (Metal-Oxide-Semiconductor Field-Effect Transistor):**

There are two primary types of MOS transistors:

| Type | Diagram | Terminal Descriptions |
|---|---|---|
| **n-type** (nMOS) |  (Insert Diagram) |  **Drain:** (Top), **Gate:** (Middle), **Source:** (Bottom) |
| **p-type** (pMOS) |  (Insert Diagram) |  **Source:** (Top), **Gate:** (Middle), **Drain:** (Bottom) |

* **n-type (nMOS):** The circuit is **closed** (on) when $V_G = 3V$ (logic 1, high voltage). It is open when $V_G = 0V$.
* **p-type (pMOS):** The circuit is **closed** (on) when $V_G = 0V$ (logic 0, low voltage). It is open when $V_G = 3V$.

**1. The Inverter (NOT Gate)**

* **Logic Symbol:** (Insert NOT Gate Symbol)
* **Truth Table:**

| Input A | Output Y |
|---|---|
| 0 | 1 |
| 1 | 0 |

* **Transistor-Level Diagram (CMOS):** (Insert CMOS Inverter Diagram)
    * **P-type (P):** Connected to VDD (3V). The input `In(A)` is connected to its gate.
    * **N-type (N):** Connected to Ground (0V). The same input `In(A)` is connected to its gate.
    * **Output (Y):** Taken from the common connection point between the P and N transistors.

**2. The NAND Gate**

* **Logic Symbol:** (Insert NAND Gate Symbol with inputs A, B)
* **Truth Table:**

| Input A | Input B | Output Y |
|---|---|---|
| 0 | 0 | 1 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

* **Transistor-Level Diagram (CMOS):** (Insert CMOS NAND Gate Diagram)
    * **P-type Network (P1, P2):** Two pMOS transistors in parallel, connected to VDD (3V). Inputs `In(A)` and `In(B)` are connected to their respective gates.
    * **N-type Network (N1, N2):** Two nMOS transistors in series, connected to Ground (0V). Inputs `In(A)` and `In(B)` are connected to their respective gates.
    * **Output (Y):** Connected to the output point between the parallel pMOS network and the series nMOS network.

**Circuit Operation Note for 13V entry in Truth Table:** The note mentions that a value of "13V" in the `In(B)` column results in an output of "0". This is likely a typographical error, and the intention is likely "1V" or just "1" for a logical High input on B, consistent with CMOS logic. In general, for a NAND gate, both inputs must be high (1) for the output to be low (0).


