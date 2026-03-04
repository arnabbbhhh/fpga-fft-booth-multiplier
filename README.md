# 8-Point FFT Using Booth Multiplier-Based MAC Unit

> **Published in IEEE Embedded Systems Letters, September 2025**  
> **Authors: Arnab Harsh, B. C. Nagar**  
> **Research Internship — National Institute of Technology, Patna**

---

## Publication

> Arnab Harsh and B. C. Nagar, "Compact and Energy Efficient 8-Point FFT using Booth Multiplier-based MAC Unit," *IEEE Embedded Systems Letters*, Sept. 2025. [Communicated]

---

## Overview

This project presents a **compact and energy-efficient 8-point FFT (Fast Fourier Transform)** implemented on FPGA using a custom **Booth Multiplier-based MAC (Multiply-Accumulate) Unit**. The design targets reduced hardware resource utilization and improved energy efficiency compared to conventional FFT implementations that use standard multipliers.

The FFT is a fundamental algorithm in digital signal processing, used extensively in communications, audio processing, spectrum analysis, and embedded systems. This implementation demonstrates how architectural optimization at the arithmetic unit level (Booth multiplier) directly improves FPGA resource usage and power consumption.

---

## Architecture

```
Input Samples (8 points)
        │
        ▼
┌───────────────────┐
│   Booth Multiplier │  ← Efficient signed multiplication using Booth encoding
│   (Radix-2 / 4)   │
└────────┬──────────┘
         │
         ▼
┌───────────────────┐
│    MAC Unit        │  ← Multiply-Accumulate built on Booth Multiplier
│  (Multiply + Add)  │
└────────┬──────────┘
         │
         ▼
┌───────────────────┐
│  8-Point FFT Core  │  ← DIT (Decimation-In-Time) Butterfly Structure
│  (Butterfly Stages)│
└────────┬──────────┘
         │
         ▼
  FFT Output (8 frequency bins)
```

### Key Design Modules

| Module | Description |
|---|---|
| `booth_multiplier.vhd` | Radix-2 Booth encoder for efficient signed multiplication |
| `mac_unit.vhd` | MAC unit using Booth multiplier as arithmetic core |
| `butterfly.vhd` | DIT butterfly computation unit |
| `fft_8point.vhd` | 8-point FFT top-level using 3 butterfly stages |
| `top_module.vhd` | Top-level wrapper with I/O ports |

---

## Why Booth Multiplier?

Standard binary multipliers generate many partial products, leading to higher area and power usage. The **Booth encoding algorithm** reduces the number of partial products by up to 50% in Radix-2 and up to 75% in Radix-4, directly translating to:

- ✅ Fewer LUTs on FPGA
- ✅ Lower dynamic power consumption
- ✅ Comparable or better timing performance
- ✅ Compact implementation suitable for embedded/IoT applications

---

## FPGA Resource Utilization

*(Results from Xilinx Vivado — update with your actual values)*

| Resource | Used | Available | Utilization |
|---|---|---|---|
| LUTs | XX | XXXXX | XX% |
| Flip-Flops | XX | XXXXX | XX% |
| DSP Blocks | XX | XX | XX% |
| Max Frequency | XX MHz | — | — |
| Power (Dynamic) | XX mW | — | — |

---

## Tools Used

- **Xilinx Vivado** — RTL design, synthesis, implementation
- **VHDL** — Hardware description language
- **Target FPGA** — *(add your board, e.g., Artix-7 / Basys-3)*
- **Testbench simulation** — Behavioral and timing verification

---

## How to Run

### Simulation
1. Open **Xilinx Vivado**
2. Create new project, add all `.vhd` files from `src/`
3. Set `top_module.vhd` as the top module
4. Add testbench from `tb/tb_fft_8point.vhd`
5. Run **Behavioral Simulation**
6. Verify output FFT bins in waveform viewer

### Synthesis & Implementation
1. Run **Synthesis** → check resource report in `docs/`
2. Run **Implementation** → check timing report
3. Generate bitstream and program to FPGA board

---

## Repository Structure

```
fpga-fft-booth-multiplier/
├── src/
│   ├── booth_multiplier.vhd
│   ├── mac_unit.vhd
│   ├── butterfly.vhd
│   ├── fft_8point.vhd
│   └── top_module.vhd
├── tb/
│   ├── tb_booth_multiplier.vhd
│   └── tb_fft_8point.vhd
├── docs/
│   ├── resource_utilization.png
│   └── timing_report.png
├── sim/
│   └── waveform_screenshot.png
└── README.md
```

---

## Applications

- Digital Signal Processing (DSP) on resource-constrained FPGAs
- Embedded spectrum analyzers
- Wireless communication front-ends
- Audio processing on edge devices
- IoT sensor data frequency analysis

---

## Related Work

This design is part of a research internship at NIT Patna under the guidance of B. C. Nagar, focusing on compact FPGA arithmetic architectures for embedded signal processing applications.
