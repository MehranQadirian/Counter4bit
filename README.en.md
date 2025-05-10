[نسخه فارسی](README.md)

# 4-Bit Counter Verilog Module

![Counter4Bit Header Image](log.png)

## Overview

This repository contains a Verilog implementation of a 4-bit counter module (`Counter4Bit`). The module is designed to increment a 4-bit binary count on each positive clock edge, with a synchronous reset functionality to initialize the counter to a specific state. The design is suitable for educational purposes and can be used as a foundational component in digital system design courses or projects.

## Module Description

The `Counter4Bit` module is a synchronous 4-bit counter that operates on the positive edge of the clock signal (`clk`). It includes a reset input (`reset`) to initialize the counter and outputs a 4-bit count value (`q`). The counter employs a feedback mechanism to generate the next state, ensuring a sequential count from 0 to 15 (in binary).

### Inputs and Outputs
- **Inputs**:
  - `clk`: Clock signal (active on positive edge).
  - `reset`: Synchronous reset signal (active high).
- **Outputs**:
  - `q[3:0]`: 4-bit output representing the current count value.

### Functionality
- On each positive clock edge, the counter updates its state based on the feedback logic.
- When the `reset` signal is high, the counter initializes to the state `q = 4'b1000` (binary 8).
- Otherwise, the counter shifts the bits in a circular manner, effectively implementing a counting sequence.

## Design Details

The module uses four flip-flops (`q0`, `q1`, `q2`, `q3`) to store the state of the counter. The next state logic is implemented using combinational assignments (`d0`, `d1`, `d2`, `d3`), where:
- `d0 = ~q3`
- `d1 = q0`
- `d2 = q1`
- `d3 = q2`

The output `q` is formed by concatenating the flip-flop states `{q3, q2, q1, q0}`. The counter operates with a time scale of 1 ns / 1 ps, as specified by the Verilog timescale directive.

## Usage

To use this module in a Verilog project:
1. Include the `Counter4Bit.v` file in your project directory.
2. Instantiate the module in your top-level design, connecting the `clk`, `reset`, and `q` ports appropriately.
3. Ensure the clock signal is properly driven and the reset signal is controlled to initialize the counter as needed.

### Example Instantiation
```verilog
Counter4Bit counter (
    .clk(clk),
    .reset(reset),
    .q(count)
);
```

## Simulation and Testing

To verify the functionality of the counter, a testbench should be developed to:
- Drive the `clk` signal with a fixed period (e.g., 10 ns).
- Assert the `reset` signal for one clock cycle to initialize the counter.
- Observe the `q` output over multiple clock cycles to confirm the counting sequence.
