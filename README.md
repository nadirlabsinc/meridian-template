# Meridian-0.5U Reference Module (RM-1)

![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)
![Standard: Meridian--4U](https://img.shields.io/badge/Standard-Meridian--4U-blue)
![Hardware: KiCad](https://img.shields.io/badge/Hardware-KiCad-green)
![Status: Alpha](https://img.shields.io/badge/Status-Alpha-orange)

The **Meridian-0.5U Reference Module (RM-1)** is the standardized "blank" blade for the Meridian-4U ecosystem. It provides a structural and electrical bridge between custom hardware experiments and the **Voyager64** compute node.

---

## Overview

The RM-1 is designed for researchers, students, and aerospace engineers to rapidly deploy custom payloads—ranging from GaN-based power stages to SDR arrays—into a high-density 4U satellite backplane. 

By following this reference design, your hardware gains instant compatibility with the **Meridian Wildcard** serial routing system and the **Nadir Meridian** power/data fabric.

## Technical Specifications

| Feature | Specification |
| :--- | :--- |
| **Form Factor** | 95mm x 90mm Meridian Blade |
| **Connector** | 200-pin Samtec SEARAY™ (High-Density) |
| **Data Fabric** | PCIe Gen 3, SATA 3.0, Gigabit Ethernet |
| **Control Bus** | Dual UART, I2C, SPI, CAN-FD |
| **Power Rails** | 5V DC, 3.3V DC (Backplane Sourced) |
| **Mounting** | Meridian L-Frame Compatible |

## System Architecture

### 1. High-Speed Interface
The module utilizes the **Samtec SEARAY** interconnect to maintain signal integrity over the 40cm Meridian backplane. It exposes differential pairs optimized for 100Ω impedance.

### 2. The Wildcard Forwarder
Each reference module includes dedicated UART lines routed through the backplane's **TMUX1208** array. This allows the Voyager64 master node to address this module's console via the `meridian-cli` without needing dedicated hardware for every slot.

### 3. Developer Sandbox
* **0.1" Proto-Grid:** A 15x20 through-hole grid for mounting discrete components or sensors.
* **Bus Breakouts:** All primary signals are broken out to easy-to-probe surface mount test points.
* **Logic ID:** On-board DIP switches for hardware-level addressing in the rack.

## Repository Structure

* `/hardware`: KiCad project files, schematic, and 4-layer PCB templates.
* `/mechanical`: STEP models and DXF files for the L-Frame and thermal spacers.
* `/docs`: Detailed Interface Control Document (ICD) and pin-mapping.

## Getting Started

1. **Clone the Repo:**
   ```bash
   git clone https://github.com/nadirlabs/meridian-template

2. Open in CAD software of choice (default KiCAD)
