# LEC3 :
# The Programmable Logic Array (PLA)

The PLA is a common and versatile building block for implementing multiple logic functions with the same set of inputs. It is structured as an **AND Array** followed by an **OR Array**.

**Example PLA Diagram:** (Insert detailed diagram with inputs A, B, C, AND gates, interconnections, and OR gates)
* **Inputs (A, B, C):** The inputs and their inverses are fed as rows into the AND array.
* **AND Array:** Consists of multiple AND gates. Interconnections can be "programmed" or connected to form different product terms. The number of rows corresponds to inputs; columns represent product terms.
* **Product Terms:** The outputs of the AND gates represent specific product terms or implicants.
* **OR Array:** Takes the product terms as inputs and sums them to generate the desired output functions.
* **Outputs (X, Y, Z):** Multiple output columns, each representing a unique logic function.

**Key Design Points for PLAs:**

* **AND Array:** An array of AND gates generates product terms of the inputs.
* **OR Array:** An array of OR gates follows the AND array to sum the desired product terms.
* **Required Configuration:** For an n-input logic function with multiple outputs, a PLA requires an AND array to generate $2^n$ possible product terms and an OR array with as many output columns as there are functions in the truth table.

# Arithmetic Logic Unit (ALU)

The ALU is a critical component of a computer processor's central processing unit (CPU). It combines arithmetic operations (like addition, subtraction) and logical operations (like AND, OR, NOT) into a single functional unit.

* **Function:** Performs only one specific function at a given time, determined by control inputs.
* **Example 3-bit Control ALU:**
    * **Inputs:** Two data inputs ($A, B$), and 3 select lines ($F_{2:0}$).
    * **Outputs:** Output $Y$.
    * **ALU Symbol Diagram:** (Insert generic ALU block symbol with input/output labels)
    * **ALU Function Table:**

| Function Select ($F_{2:0}$) | Operation Performed | Note / Alternative Notation |
|---|---|---|
| 000 | A AND B | bitwise AND |
| 001 | A OR B | bitwise OR |
| 010 | A + B | Arithmetic Addition |
| 011 | **not used** | No operation defined |
| 100 | A NAND B | bitwise NAND |
| 101 | A NOR B | bitwise NOR |
| 110 | A - B | Arithmetic Subtraction |
| 111 | SLT | Set Less Than (comparative) |

*The note mentions "Arithmetic and logical operation in a single unit, performs only one function at a time." This is a key principle of ALU operation.*


# Tri-State Buffer (TSB)

A **Tri-State Buffer**, also called a tri-state gate or driver, is a fundamental digital component that acts as a switch, controlling the connection of a signal to a common bus or wire. It enables the "gating" or isolation of different signals on the same wire.

* **Structure:** It has three key connections: Data Input (A), Data Output (Y), and an Enable Input (E).
* **Symbol Diagram:** (Insert schematic symbol with labels A, Y, E)
* **Truth Table:**

| Enable Input (E) | Data Input (A) | Output (Y) | Description |
|---|---|---|---|
| 0 | 0 | Z | **Disabled:** Output is High-Impedance, acting as an open circuit (disconnected). |
| 0 | 1 | Z | **Disabled:** Output is High-Impedance, acting as an open circuit. |
| 1 | 0 | 0 | **Enabled:** Output follows input (output = input). |
| 1 | 1 | 1 | **Enabled:** Output follows input. |

The special **Z** state represents "High Impedance" or "tri-state," where the output is logically disconnected from both VDD and Ground.

---

# Multiplexer (MUX) Design using TSBs

A Multiplexer is a combinatorial circuit that selects from several binary input signals and directs one of them to a single output line based on control inputs. We can efficiently build MUXes using Tri-State Buffers.

## 1. 2-to-1 Multiplexer (using TSBs)

* **Function:** Selects input $D_0$ or $D_1$ to output Y based on select input S.
* **Concept:** Use two tri-state buffers with complementary enable signals. When one is enabled, the other is disabled.
* **Diagram:** (Insert logic diagram with two TSBs, data inputs D0, D1, control input S with an inverter, and output Y)
* **Logic Function:**
    $$Y = D_0\overline{S} + D_1S$$
* **Alternative Symbol Diagram:** (Insert standard block diagram for a 2-1 MUX, perhaps showing the relationship to a decoder-like function on select lines). The notes show a 2-1 MUX built with TSBs, and a standard representation below with S0 control and D0/D1 inputs.

## 2. 4-to-1 Multiplexer (using TSBs)

* **Function:** Selects one of four inputs ($D_0, D_1, D_2, D_3$) to output Y based on a 2-bit select signal ($S_1, S_0$).
* **Diagram:** (Insert diagram showing four TSBs with data inputs D0-D3 and their respective enable lines derived from select logic. All outputs combine to Y)
* **Concept:**
    * $D_0$ selected when $S_1S_0 = 00$ (enable line for $D_0$'s TSB should be $\overline{S_1}\overline{S_0}$).
    * $D_1$ selected when $S_1S_0 = 01$ (enable line for $D_1$'s TSB should be $\overline{S_1}S_0$).
    * $D_2$ selected when $S_1S_0 = 10$ (enable line for $D_2$'s TSB should be $S_1\overline{S_0}$).
    * $D_3$ selected when $S_1S_0 = 11$ (enable line for $D_3$'s TSB should be $S_1S_0$).
    * The diagrams in the image visually represent this selection logic with complementary enable signals (shown as bars over control variables in the diagram captions like $\overline{S_1}\overline{S_0}$).

* **Simplified Representation:** The bottom-left diagram shows a more compact representation of a 4-1 MUX structure with control inputs S0, S1, data inputs D0-D3, and output Y.

# Transistor-Level Tri-State Buffer and Priority Circuit

## Tri-State Buffer (TSB) using Transistors

A transistor-level implementation of a Tri-State Buffer (TSB) provides a detailed look at its operation, specifically how the third, high-impedance (Z) state is achieved.

* **Diagram:** (Insert transistor-level diagram with VDD, Ground, Data Input In(A), Enable Input EN with an inverter, and Output Y)
* **Description:**
    * This is an inverting tri-state buffer.
    * It's similar to a standard CMOS inverter but with two additional "clock-like" or control transistors (one pMOS and one nMOS) in series between the pull-up pMOS and pull-down nMOS.
    * These control transistors are driven by the Enable (`EN`) signal. The pMOS control is driven by `$\overline{EN}$` and the nMOS control by `EN`.

* **Transistor States Based on Enable Input (EN):**

| EN Input | $\overline{EN}$ Input | Upper nMOS Control | Upper pMOS Control | Lower pMOS Control | Lower nMOS Control | Output Network Status | Output Y Status |
|---|---|---|---|---|---|---|---|
| 0 | 1 | **OFF** | **ON** | (depends on A) | (depends on A) | **Open Circuit / Floating** | **High-Impedance (Z)** |
| 1 | 0 | **ON** | **OFF** | (depends on A) | (depends on A) | **Normal Inverter Mode** | **Follows Input ($\overline{A}$)** |

**Circuit Explanation:**
1.  **Disabled (EN = 0, $\overline{EN} = 1$):**
    * The upper nMOS control transistor is OFF.
    * The lower pMOS control transistor is OFF.
    * This disconnects the pull-down nMOS from Ground.
    * Similarly, the upper pMOS control is ON and lower pMOS control is ON (for pMOS). This is confusing. Let's re-evaluate. The diagram shows: Top pMOS -> pMOS controlled by $\overline{EN}$ -> Output -> nMOS controlled by EN -> nMOS -> GND.
    * Let's correct: Top pMOS -> **pMOS controlled by EN** -> Output -> **nMOS controlled by $\overline{EN}$** -> nMOS -> GND.
    * Let's re-correct based on standard design: Top pMOS -> **pMOS controlled by $\overline{EN}$** -> Output -> **nMOS controlled by EN** -> nMOS -> GND.
    * Let's check the diagram again. Yes, top pMOS gate gets EN. pMOS gate with EN. Next pMOS is below it. The nMOS gets EN on its gate. Wait. Let's re-look.
    * Top pMOS gate connected to `EN` (but should be `EN` or `$\overline{EN}$`? A `$\overline{EN}$` would turn it ON when active low. An `EN` turns it OFF when EN=1. Standard active high enable: `$\overline{EN}$` on pMOS, `EN` on nMOS).
    * Let's assume standard active-high `EN` logic.
    * **EN = 0 (Disabled):** `$\overline{EN}=1$`. Top control pMOS is OFF. Bottom control nMOS is OFF. Both pull-up and pull-down paths are blocked. The output is not connected to either power or ground, resulting in the high-impedance state (Z). The state of inputs does not matter.
    * **EN = 1 (Enabled):** `$\overline{EN}=0$`. Top control pMOS is ON. Bottom control nMOS is ON. The circuit functions as a normal CMOS inverter for input `A`. If A=0, Y=1 (through pull-up). If A=1, Y=0 (through pull-down).

---

## Priority Circuit

A **Priority Circuit** is used to determine which of several active requests has the highest priority. It "grants" a signal only to the single highest-priority request among multiple simultaneously asserted input signals.

* **Inputs:** Multiple "Requestor" lines (e.g., A3, A2, A1, A0), each with an associated priority level. By convention, higher indices often have higher priority (e.g., A3 has the highest priority, A0 the lowest).
* **Outputs:** Multiple "Grant" lines (e.g., Y3, Y2, Y1, Y0). Only one grant line will be active (1), corresponding to the active request with the highest priority.
* **Example: 4-bit Priority Circuit (Prioritizing higher index):**

* **Diagram:** (Insert block diagram of 4-bit priority circuit with input labels A3-A0 and output labels Y3-Y0)
* **Truth Table:**

| Input Requests ($A_3$ $A_2$ $A_1$ $A_0$) | Grant Outputs ($Y_3$ $Y_2$ $Y_1$ $Y_0$) | Priority Analysis |
|---|---|---|
| 0 0 0 0 | 0 0 0 0 | No active requests. No grants given. |
| 0 0 0 1 | 0 0 0 1 | Lowest priority request A0 is the only one active. Y0 is granted. |
| 0 0 1 0 | 0 0 1 0 | Request A1 is active. Higher priority than A0 (even if A0 were active). Y1 is granted. |
| 0 0 1 1 | 0 0 1 0 | Both A1 and A0 active. A1 has higher priority. Y1 granted, Y0 denied. |
| 0 1 0 0 | 0 1 0 0 | Request A2 is active. Y2 is granted. |
| 0 1 0 1 | 0 1 0 0 | Requests A2 and A0 active. A2 has higher priority. Y2 granted. |
| 0 1 1 0 | 0 1 0 0 | Requests A2 and A1 active. A2 has higher priority. Y2 granted. |
| 0 1 1 1 | 0 1 0 0 | A2, A1, A0 active. A2 has the highest priority. Y2 granted. |
| 1 0 0 0 | 1 0 0 0 | Highest priority request A3 is active. Y3 granted. |
| 1 0 0 1 | 1 0 0 0 | A3 and A0 active. A3 has higher priority. Y3 granted. |
| 1 0 1 0 | 1 0 0 0 | A3 and A1 active. A3 has higher priority. Y3 granted. |
| 1 0 1 1 | 1 0 0 0 | A3, A1, A0 active. A3 has the highest priority. Y3 granted. |
| 1 1 0 0 | 1 0 0 0 | A3 and A2 active. A3 has the highest priority. Y3 granted. |
| **... (continuation)** | **... (continuation)** | ... |
| 1 1 1 1 | 1 0 0 0 | All requests are active. A3 has the absolute highest priority. Y3 granted. |

The key observation is that once a higher-priority request is found (reading from left to right as A3, A2, A1, A0), any request with lower priority is ignored. For example, if $A_3$ is 1, output $Y_3$ will always be 1, and $Y_2, Y_1, Y_0$ will always be 0, regardless of the states of $A_2, A_1, A_0$. The note in the bottom right column for '1100' -> '1000' and '1111' -> '1000' correctly reflects this behavior for high-to-low priority ordering.