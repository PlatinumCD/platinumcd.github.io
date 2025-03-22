# The Rocket Chip Generator Notes

## Overview

**Rocket Chip** is an open-source System-on-Chip (SoC) generator that produces design instances ranging from RTL to silicon prototypes. Its configurations support a wide range of applications—from small embedded microcontrollers to large multi-core server chips.

---

## Rocket Core

Rocket is a **5-stage in-order scalar core generator** with the following key features:
- **MMU:** Implements page-based virtual memory.
- **Non-blocking Data Cache:** Helps maintain performance by reducing memory wait times.
- **Frontend with Branch Prediction:** Uses branch prediction (configurable with branch target buffer, branch history table, and return address stack) to improve execution flow.
- **Configurable Options:** Various parameters (ISA extensions like M, A, F, D, floating-point pipeline stages, cache sizes, and TLB sizes) are exposed for customization.

Additionally, Rocket can be considered as a library of processor components.

---

## Rocket Custom Coprocessor Interface (RoCC)

The **RoCC interface** allows the Rocket processor to communicate in a decoupled manner with attached coprocessors (e.g., crypto units, vector processing units). The interface is designed to:
- **Exchange Commands:** Pass commands from the core to the coprocessor.
- **Share Resources:** Allow the coprocessor to use the core’s data cache and page table walker.
- **Handle Interrupts:** Enable the coprocessor to interrupt the core when necessary.
- **Direct Memory Connection:** Facilitate high-bandwidth coherent connections to the outer memory system via the TileLink interconnect.

### RoCC Command Flow Diagram

   +---------------------+
   |   Rocket Core       |
   |  (Issues Command)   |
   +---------------------+
            |
            | Command:
            | - Instruction Word
            | - Integer Reg 1 (operand)
            | - Integer Reg 2 (operand)
            v
   +---------------------+
   |   RoCC Interface    |
   | (Coprocessor Link)  |
   +---------------------+
            |
            | Process Command
            v
   +---------------------+
   |   Coprocessor Unit  |
   |  (Performs Action)  |
   +---------------------+
            |
            | (Optional Response)
            | - Write to Integer Reg
            v
   +---------------------+
   |   Rocket Core       |
   |  (Receives Result)  |
   +---------------------+

---

## Boom Core (Out-of-Order Superscalar)

**Boom** is an out-of-order superscalar core generator aimed at serving as a baseline for research and exploring out-of-order microarchitecture designs.

### In-Order Pipeline

In an in-order design, instructions progress sequentially through the following stages:

+---------+    +--------+    +---------+    +--------+    +-----------+
| Fetch   | -> | Decode | -> | Execute | -> | Memory | -> | Writeback |
+---------+    +--------+    +---------+    +--------+    +-----------+


### Out-of-Order Pipeline

Out-of-order cores fetch and decode instructions sequentially, but they allow instructions to be issued and executed as soon as their operands are ready. A reorder buffer ensures that the results are committed in the original program order.

     +---------+    +--------+
     | Fetch   | -> | Decode |
     +---------+    +--------+
                       |
                       v
              +-----------------+
              |  Issue/Dispatch |   <-- Instructions queued
              +-----------------+
                  /     |     \
                 /      |      \
   +---------+   +---------+   +---------+
   | Execute |   | Execute |   | Execute |
   +---------+   +---------+   +---------+
                 \      |      /
                  \     |     /
              +-----------------+
              | Reorder Buffer  | <-- Maintains program order
              +-----------------+
                       |
                       v
                  +-----------+
                  | Writeback |
                  +-----------+

---

## Z-Scale Core

**Z-Scale Core** is a 32-bit core generator tailored for embedded systems and microcontrollers. It is designed for efficiency and low power in smaller-scale applications.

---

## Summary

- **Rocket Chip** is a versatile open-source SoC generator.
- **Rocket Core** utilizes a 5-stage in-order pipeline with configurable features.
- **RoCC Interface** enables offloading tasks to specialized coprocessors while sharing resources.
- **Boom Core** represents an advanced out-of-order design that leverages a reorder buffer for high performance.
- **Z-Scale Core** targets low-power, embedded applications.

This collection of core generators supports a wide range of designs, making them valuable for both research and practical applications in processor design.
