# A Survey on RISC-V Based Machine Learning Ecosystem

## Overview

This paper presents a quantitative taxonomy of RISC-V SoCs and explores opportunities for future research in machine learning using open-source hardware architectures. It highlights how open-source hardware has increased the complexity and diversity of RISC-V processors alongside emerging ML frameworks.

---

## RISC-V SoC Implementations

### Hardware Cores

- **Rocket Core**
  - Scalar RISC-V core from UCB
  - Supports RV32G and RV64G
  - Renowned for its configurability and use in SoC designs

- **BOOM (SonicBOOM)**
  - Out-of-order processor from UCB
  - Designed for educational purposes with performance improvements

- **PicoRV32**
  - Size-optimized core for FPGA and ASIC
  - Supports RV32IMC with a minimal footprint

- **NEORV32**
  - Highly configurable core for microcontroller applications
  - Compatible with various peripherals and RTOS

- **NaxRiscv**
  - Supports out-of-order execution
  - Scalable for different ISA extensions and optimized for FPGA

- **NOEL-V**
  - Open-source core designed for embedded applications
  - Offers customizable configurations

- **ORCA**
  - Portable, FPGA-optimized core with vector extension support
  - Known for its performance

- **SERV**
  - Bit-serial CPU core; one of the smallest RISC-V implementations
  - Compatible with a variety of FPGA boards

- **VROOM**
  - A high-end core under development
  - Features simultaneous multithreading and advanced ISA extensions

- **Ibex**
  - Microcontroller-class CPU supporting RV32IMC
  - Part of the PULP platform and optimized for multiple FPGA implementations

---

## Software Frameworks

- **TVM**
  - An Apache open-source ML framework
  - Optimizes and runs ML models on various hardware (CPUs, GPUs, FPGAs)
  - Provides a hardware-agnostic, performance-efficient infrastructure for ML model development

- **CFU Playground**
  - Full-stack open-source framework for rapid prototyping of ML accelerators on FPGA systems
  - Simplifies the development of hardware accelerators for ML tasks

- **Chipyard**
  - Unified SoC design, simulation, and implementation environment developed at UC Berkeley
  - Offers a comprehensive set of tools for RTL design, system validation, and chip physical design

- **Open ESP**
  - Open-source research platform for heterogeneous SoC design by Columbia University
  - Integrates software and hardware design flows to enable flexible and scalable accelerator development

- **NVDLA**
  - NVIDIA Deep Learning Accelerator: an open-source platform for accelerating deep learning network inference
  - Modular and scalable design for efficient neural network operation execution on various devices

---

## Future Opportunities

- **Power Efficiency & Reliability:**  
  Develop more power-efficient and reliable hardware designs tailored for machine learning applications.

- **Custom Accelerators:**  
  Leverage the flexibility of RISC-V to create customized accelerators targeting specific ML tasks.

- **Enhanced Integration:**  
  Improve integration between RISC-V hardware and existing ML software frameworks to boost performance and scalability.

- **New Architectural Configurations:**  
  Explore innovative architectural configurations that can better meet the computational demands of advanced AI algorithms.
