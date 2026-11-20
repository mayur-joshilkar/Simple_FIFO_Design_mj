# Parameterized Synchronous FIFO -- Verilog RTL

A basic parameterized synchronous FIFO (First-In, First-Out) implemented
in Verilog HDL, with a separate testbench for functional simulation.

## Project Overview

This project contains: - A FIFO RTL module with configurable data width
and FIFO depth. - Write (push) and read (pop) control signals. - `full`
and `empty` status flags. - A Verilog testbench that generates a clock,
applies reset, writes two data values, and reads them back.

## Default Configuration

  Parameter        Default value Description
  -------------- --------------- ----------------------------------
  `data_width`                 8 Number of bits in each data word
  `fifo_width`                32 Number of memory locations

Both parameters can be overridden when the `FIFO` module is
instantiated.

## Interface

  -----------------------------------------------------------------------
  Signal                  Direction               Description
  ----------------------- ----------------------- -----------------------
  `clk`                   Input                   Clock signal

  `reset`                 Input                   Synchronous active-high
                                                  reset

  `wr_en`                 Input                   Enables a write when
                                                  the FIFO is not full

  `rd_en`                 Input                   Enables a read when the
                                                  FIFO is not empty

  `data_in`               Input                   Data word to be written

  `data_out`              Output                  Data word read from the
                                                  FIFO

  `full`                  Output                  Asserted when the
                                                  internal count equals
                                                  the configured depth

  `empty`                 Output                  Asserted when the
                                                  internal count is zero
  -----------------------------------------------------------------------

## Repository Contents

``` text
Parameterized-Synchronous-FIFO/
├── FIFO.v
├── fifo_testbench.v
└── README.md
```

## How It Works

1.  Apply the active-high reset to initialize the read pointer, write
    pointer, and occupancy counter.
2.  Set `wr_en` to write `data_in` when `full` is low.
3.  Set `rd_en` to read data when `empty` is low.
4.  The `full` and `empty` outputs indicate the FIFO status.

The RTL uses a clocked process for write control, read control, and
occupancy counting.

## Testbench

The supplied testbench: - Generates a clock with a 10 ns period. -
Applies reset. - Writes `8'h10` and `8'h20`. - Performs two read
operations. - Prints signal activity using `$monitor` and ends the
simulation using `$finish`.

## Run a Simulation

You can simulate the RTL and testbench using a Verilog simulator such as
Xilinx Vivado Simulator or ModelSim.

For Icarus Verilog, if installed, run:

``` bash
iverilog -o fifo_sim FIFO.v fifo_testbench.v
vvp fifo_sim
```

## Current Scope and Future Improvements

This repository contains a basic FIFO implementation and a simple
read/write test sequence. Further development and verification can
include: - Circular pointer wrap-around. - Simultaneous read and write
operation handling. - Boundary-condition tests for full and empty
states. - Parameter-range and pointer-width checks. - Assertions and
broader self-checking testbench coverage.

## Author

**Mayur Joshilkar**\
B.Tech -- Electronics Engineering (VLSI Design and Technology)\
Dr. Babasaheb Ambedkar Technological University (DBATU)

------------------------------------------------------------------------

*This project is intended for learning and demonstrating basic Verilog
RTL design and simulation.*
