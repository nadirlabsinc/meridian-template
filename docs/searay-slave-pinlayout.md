# Meridian Slave Interface Control Document (ICD)
**Standard Version:** 1.0.0  
**Connector Spec:** Samtec SEAF Series (20 Rows x 10 Columns)  
**Pitch:** 1.27mm (0.050")  
**Application:** Nadir Labs Meridian Backplane Ecosystem

---

## 1. Pin Mapping Table
*Note: Pin numbering follows the Samtec standard grid (A1 through T10). This table defines the interface for a **Peripheral Module** (Slave).*

| Pin Range | Name | Purpose | Signal Type | Constraints / Requirements |
|:---|:---|:---|:---|:---|
| **A1 - A10** | **VCC_5V** | Main System Power | Power (IN) | Max 2A per pin. Tie all pins to a 2oz copper pour. |
| **B1 - B10** | **VCC_3V3** | Logic Power | Power (IN) | Max 1.5A per pin. Local decoupling required. |
| **C1 - C20** | **GND** | Signal Ground | Ground | Primary reference for high-speed signals. |
| **D1** | **UART_TX** | Primary Console TX | 3.3V CMOS | Routed to Wildcard Mux. |
| **D2** | **UART_RX** | Primary Console RX | 3.3V CMOS | Routed to Wildcard Mux. |
| **D3** | **GND** | Signal isolation | Ground |  |
| **D4** | **I2C1_SDA** | Management Bus | Open-Drain | 3.3V Logic. Pull-ups located on Backplane. |
| **D5** | **I2C1_SCL** | Management Bus | Open-Drain | 3.3V Logic. Pull-ups located on Backplane. |
| **D6** | **I2C1_INT** | Bus Control | 3.3V CMOS | Active Low. |
| **D7** | **I2C1_RST** | Bus Control | 3.3V CMOS | Active Low. |
| **D11** | **GND** |  Signal isolation | Ground |  |
| **D12** | **I2C1_SDA** | Management Bus | Open-Drain | Signal redundancy |
| **D13** | **I2C1_SCL** | Management Bus | Open-Drain | Signal redundancy |
| **D14** | **I2C1_INT** | Bus Control | 3.3V CMOS | Signal redundancy |
| **D15** | **I2C1_RST** | Bus Control | 3.3V CMOS | Signal redundancy |
| **D16** | **GND** | Signal isolation | Ground |  |
| **E1** | **SPI1_MOSI** | Data Bus | 3.3V CMOS | 50MHz Max Clock. |
| **E2** | **GND** | Signal isolation | Ground |  |
| **E3** | **SPI1_MISO** | Data Bus | 3.3V CMOS | 50MHz Max Clock. |
| **E4** | **GND** | Signal isolation | Ground | 5 |
| **E5** | **SPI1_SCK** | Bus Control | 3.3V CMOS | Dedicated CS per slot. |
| **E6** | **GND** | Signal isolation | Ground | 5 |
| **E7** | **SPI1_CS** | Bus Control | 3.3V CMOS | Dedicated CS per slot. |
| **E8** | **GND** | Signal isolation | Ground | 5 |
| **E13** | **SPI1_MOSI** | Data Bus | 3.3V CMOS | 50MHz Max Clock. |
| **E14** | **GND** | Signal isolation | Ground |  |
| **E15** | **SPI1_MISO** | Data Bus | 3.3V CMOS | 50MHz Max Clock. |
| **E16** | **GND** | Signal isolation | Ground | 5 |
| **E17** | **SPI1_SCK** | Bus Control | 3.3V CMOS | Dedicated CS per slot. |
| **E18** | **GND** | Signal isolation | Ground | 5 |
| **E19** | **SPI1_CS** | Bus Control | 3.3V CMOS | Dedicated CS per slot. |
| **E205** | **GND** | Signal isolation | Ground | 5 |
| **F1 - F4** | **CAN_H/L** | Control Bus | Differential | 120Ω termination required on end-nodes. |
| **G1 - G4** | **PCIE0_TX+/TX-** | PCIe Lane 0 Out | Diff Pair | 85Ω Diff. AC Coupling caps on Source. |
| **G5 - G8** | **PCIE0_RX+/RX-** | PCIe Lane 0 In | Diff Pair | 85Ω Diff. |
| **H1 - H4** | **PCIE1_TX+/TX-** | PCIe Lane 1 Out | Diff Pair | 85Ω Diff. AC Coupling caps on Source. |
| **H5 - H8** | **PCIE1_RX+/RX-** | PCIe Lane 1 In | Diff Pair | 85Ω Diff. |
| **J1 - J4** | **USB_D+/D-** | USB 2.0 Interface | Diff Pair | 90Ω Diff. Length match < 50mil. |
| **K1 - K4** | **ETH_TRX0+/-** | Ethernet Pair 0 | Diff Pair | 100Ω Diff. Magnetics on Module. |
| **K5 - K8** | **ETH_TRX1+/-** | Ethernet Pair 1 | Diff Pair | 100Ω Diff. Magnetics on Module. |
| **L1 - L4** | **SATA_TX+/TX-** | Storage Data Out | Diff Pair | 100Ω Diff. (Reserved for Voyager CM). |
| **L5 - L8** | **SATA_RX+/RX-** | Storage Data In | Diff Pair | 100Ω Diff. (Reserved for Voyager CM). |
| **M1 - M20** | **GPIO_0..19** | User Defined I/O | 3.3V CMOS | 10mA max drive strength per pin. |
| **N1** | **SYS_RESET** | Global Reset | Active Low | Pulled high (10k) on Backplane. |
| **N2** | **SYS_WAKE** | Power Management | Active Low | Open-drain capable. |
| **P1 - P10** | **GND_PWR** | Power Return | Ground | High-current return path. |

---

## 2. Electrical Specifications

### 2.1 Power Distribution
* **Total Slot Power:** Designed for a maximum thermal envelope of 25W per 1U slot.
* **Filtering:** Every module must include a bulk capacitance of at least 22µF on both `VCC_5V` and `VCC_3V3` rails to suppress transients caused by the 40cm backplane inductance.

### 2.2 Signal Integrity (SI)
* **Impedance Targets:**
  * PCIe: 85Ω Differential
  * USB/SATA/Ethernet: 90-100Ω Differential
  * Single-Ended: 50Ω
* **Stackup:** Modules are recommended to use a minimum 4-layer stackup (Signal-GND-VCC-Signal) to maintain a consistent reference plane for the SEARAY interface.

---

## 3. Mechanical Constraints

* **PCB Thickness:** **1.6mm (±0.1mm)**. Thinner boards may flex excessively during mating, risking solder joint failure on high-density pins.
* **Component Height:** Maximum component height on the "Top" side of the module is **20mm**. 
* **Thermal Interface:** Components requiring high heat dissipation (e.g., SoCs, FPGAs) should be positioned to interface with the Aluminum L-Frame via a thermal gap pad.

---

## 4. Usage Instructions
To start a new design, clone the `meridian-starter-kit` repository. 
1. Use the provided **KiCad Board Template**.
2. **DO NOT** move the SEARAY footprint; its position is fixed relative to the L-Frame mounting holes.
3. Assign your module IDs via the `GPIO` bank if running multiple identical modules on the same backplane.

---
