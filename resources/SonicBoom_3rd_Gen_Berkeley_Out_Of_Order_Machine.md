# Sonic BOOM: Berkeley Out-of-Order Machine (v3) Notes

## Overview
- Third generation Berkeley Out-of-Order Machine (BOOM) named **Sonic BOOM**.
- Open-source RISC-V superscalar out-of-order core, state-of-the-art performance.
- Achieves highest IPC among open-source cores at publication (6.2 CoreMark/MHz).

## Key Improvements Over BOOMv2
- Execution path optimizations.
- Redesigned instruction fetch with new TAGE branch predictor.
- First open-source load-store unit supporting multiple loads per cycle.
- 2x IPC improvement on SPEC CPU benchmarks compared to prior open cores.

## Major Features
### Instruction Fetch
- New frontend supports compressed RISC-V (RVC) instructions.
- Pipelined, hierarchical TAGE-based branch predictor:
  - Single-cycle next-line predictor (uBTB).
  - Superscalar global-history vector, improved accuracy and reduced aliasing.
  - Snapshotted Return Address Stack (RAS) reduces mispredicts by 10x.
  - Superscalar branch resolution units for higher throughput.

### Execution Pipeline Enhancements
- RoCC interface support for tightly-integrated custom accelerators.
- Short-forward branch optimization converts unpredictable branches to internal predicated micro-ops, significantly boosting IPC (up to 1.7x improvement observed).

### Load-Store Unit & Data Cache
- Redesigned dual-ported L1 data cache, supports dual-issue loads/stores.
- Speculative refills via line-fill buffers to reduce cache pollution and latency.
- Non-blocking, parallel state machines for improved cache management.
- Simple next-line prefetcher and resilience to Spectre-like attacks.

### System Integration
- Fully integrates within Chipyard SoC ecosystem for broad compatibility.
- Continuous VLSI and FPGA-accelerated simulation via FireSim and Hammer.

### Operating System & Validation
- Supports RV64GC Linux (Fedora, Buildroot).
- Discovered critical kernel bugs due to aggressive speculation.
- Utilizes unit testing (TraceGen, memtrace) and co-simulation (Dromajo) to detect and resolve corner-case bugs efficiently.

## Evaluation Results
- Synthesized at 1 GHz (FinFET process).
- Competitive IPC with AWS Graviton, comparable to Intel Skylake on certain benchmarks.
- Almost 2x IPC improvement in CoreMark vs. BOOMv2.

## Future Work
- Integration of RISC-V Vector extensions.
- Enhanced instruction/data prefetching to better handle memory latency.
