# Hardware Description Languages and Verilog II

## Overview
Hardware Description Languages (HDLs) are specialized languages used to describe hardware structures like wires, gates, and registers[cite: 5]. They are designed to handle the **parallelism** inherent in hardware, where all logic operates concurrently[cite: 5].

---

## Design Methodologies
*   **Hierarchical Design**: Complexity is managed by building a hierarchy of modules[cite: 5].
*   **Top-Down**: Start with the top-level module and subdivide into sub-modules until reaching **leaf cells** (primitive gates)[cite: 5].
*   **Bottom-Up**: Identify available building blocks first and combine them into increasingly complex modules[cite: 5].

---

## Verilog Module Basics
A module is the fundamental building block in Verilog[cite: 5].
*   **Declaration**: Includes the module name, port directions (input/output), and port names[cite: 5].
*   **Multi-bit Signals (Bus)**: Defined using range syntax, typically `[31:0]` for a 32-bit value[cite: 5].
*   **Bit Manipulation**: Supports bit slicing (`longbus[12:5]`), concatenation (`{a, b}`), and duplication (`{4{a[0]}}`)[cite: 5].

### Implementation Styles
1.  **Structural (Gate-Level)**: Describes the physical interconnection of gates and sub-modules[cite: 5].
2.  **Behavioral**: Describes the functional logic using mathematical and logical operators at a higher abstraction level[cite: 5].

---

## Combinational Logic Constructs
*   **Continuous Assignment**: Uses the `assign` keyword to model simple combinational logic[cite: 5].
*   **Operators**: Supports bitwise (`&`, `|`, `^`), reduction (`&a` for an 8-input AND), and conditional/ternary operators (`s ? d1 : d0`)[cite: 5].
*   **Numbers**: Expressed as `N'Bxx` (e.g., `8'b0000_0001` for 8-bit binary)[cite: 5].
*   **Tri-state Buffers**: Use `z` to represent high impedance/floating signals[cite: 5].

---

## Sequential Logic Constructs
Sequential logic requires memory elements (Flip-Flops/Latches) triggered by a clock[cite: 5].



### The `always` Block
*   **Sensitivity List**: Statements inside execute only when an event in the list occurs (e.g., `always @ (posedge clk)`)[cite: 5].
*   **Assignments**:
    *   **Non-blocking (`<=`)**: Assignments occur in parallel at the end of the block; used for **sequential logic**[cite: 5].
    *   **Blocking (`=`)**: Assignments occur immediately in order; used for **combinational logic**[cite: 5].
*   **Variable Type**: Any signal assigned inside an `always` block must be declared as a `reg`[cite: 5].

### Resets
*   **Asynchronous**: Sampled independently of the clock; higher priority but sensitive to glitches[cite: 5].
*   **Synchronous**: Sampled only at the clock edge, resulting in a fully synchronous circuit[cite: 5].

---

## Finite State Machines (FSMs)
FSMs are implemented in three distinct parts[cite: 5]:



1.  **State Register**: A sequential `always` block to update the current state on the clock edge[cite: 5].
2.  **Next State Logic**: A combinational block (usually a `case` statement) to determine the next state based on the current state and inputs[cite: 5].
3.  **Output Logic**: Logic that generates outputs based on the state (**Moore**) or state and inputs (**Mealy**)[cite: 5].