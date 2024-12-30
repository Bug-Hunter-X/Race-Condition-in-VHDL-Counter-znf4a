# VHDL Counter Race Condition

This repository demonstrates a potential race condition in a simple VHDL counter.  The code implements a counter that increments on each rising clock edge, resetting to 0 when a reset signal is high. However, if the `reset` signal changes at exactly the same time as the `clk`'s rising edge, the behavior becomes unpredictable.

## Bug Description
The problem lies in the sensitivity list of the process.  Both `clk` and `reset` are included.  If a simultaneous change occurs, the order of execution is not guaranteed, potentially leading to unexpected values in the `internal_count` signal.

## Solution
The solution involves careful handling of signal changes to prevent simultaneous events from affecting each other. This requires introducing a synchronous reset that is only sampled after the clock's rising edge.