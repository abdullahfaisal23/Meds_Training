# Lecture 6: Timing and Verification

## 1. Combinational Timing
Real-world signals face physical delays due to transistor switching and capacitance.
* **Propagation Delay ($t_{pd}$):** Max time for output to settle (stable state).
* **Contamination Delay ($t_{cd}$):** Min time before output starts changing.
* **Critical Path:** The longest path (determines max speed).
* **Short Path:** The shortest path (determines min delay).

## 2. Glitches
* **Definition:** Temporary incorrect output values caused by path delay imbalances.
* **Fix:** Can be resolved using consensus terms in K-maps, though often ignored in synchronous systems if they settle before the next clock edge.

## 3. Sequential Timing
Flip-flops require stable data around the clock edge to avoid **Metastability**.
* **Setup Time ($t_{setup}$):** Time data must be stable *before* the clock edge.
* **Hold Time ($t_{hold}$):** Time data must remain stable *after* the clock edge.

### System Constraints
1.  **Setup Constraint:** $T_c \geq t_{pcq} + t_{pd} + t_{setup}$ (Limits max frequency).
2.  **Hold Constraint:** $t_{ccq} + t_{cd} > t_{hold}$ (Prevents "race" conditions).
* **Clock Skew:** Differences in clock arrival times; it penalizes both setup and hold margins.

## 4. Verification
Ensures the design is functionally and physically correct.
* **Functional Verification:** Uses **Testbenches** to simulate inputs and check outputs against "Golden Models."
* **Timing Verification:** Uses tools to generate **Timing Reports**; setup violations are fixed by splitting logic, hold violations by adding buffers.

---

### Key Timing Summary
| Term | Meaning | Impact |
| :--- | :--- | :--- |
| **$t_{pd}$** | Propagation Delay | Slowest path; limits speed |
| **$t_{cd}$** | Contamination Delay | Shortest path; protects hold time |
| **$t_{setup}$** | Setup Time | Must be met for data to be captured |
| **$t_{hold}$** | Hold Time | Must be met to keep data stable |