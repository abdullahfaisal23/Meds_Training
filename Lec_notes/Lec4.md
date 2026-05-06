# Lecture 4c: Hardware Description Languages & Verilog

## 🔹 Introduction to HDL
- Hardware Description Languages (HDLs) are used to:
  - Describe hardware systems
  - Simulate behavior
  - Synthesize circuits
- Popular HDLs:
  - Verilog (IEEE 1364)
  - VHDL (IEEE 1076)

## 🔹 Why HDL?
- Handles complex digital systems
- Supports:
  - Parallelism
  - Combinational & Sequential logic
- Enables simulation + synthesis

## 🔹 Design Methodologies

### Top-Down
- Start from top module → divide into submodules

### Bottom-Up
- Start from basic gates → build larger modules

##  Verilog Basics

### Module Structure

module example(
input [31:0] a;
output [7:0] b;
);

endmodule

assign y = ~a & ~b & ~c |
           a & ~b & ~c |
           a & ~b &  c;
