# Meridian Process Design Kit (PDK)
**Version:** 1.0.0  
**Process:** JLC06161H-3313 (6-Layer)  
**Finish:** ENIG (Electroless Nickel Immersion Gold)  
**Application:** Nadir Labs Meridian Architecture  

This PDK defines the manufacturing constraints for the **Meridian** ecosystem. Adherence to these rules is mandatory to ensure signal integrity across the 40cm backplane and mechanical compatibility with the L-Frame chassis.

---

## 1. Manufacturing Specifications (JLC Prototype Class)

| Parameter | Specification | Note |
|:---|:---|:---|
| **Layer Count** | 6 Layers | Standard stackup |
| **Material** | FR4 High-Tg 155°C | Thermal stability for vacuum |
| **Board Thickness** | 1.6mm (±0.1mm) | Required for SEARAY mating |
| **Outer Copper** | 1.0 oz (35µm) | Power density requirement |
| **Inner Copper** | 0.5 oz (17.5µm) | Signal integrity balance |
| **Surface Finish** | **ENIG** | **Mandatory** for 1.27mm pitch |
| **Min Trace/Space** | 0.1mm / 0.1mm | 4mil / 4mil |
| **Min Via Hole/Dia** | 0.2mm / 0.4mm | 8mil / 16mil |
| **Solder Mask** | Matte Black / Green | User preference |

---

## 2. Layer Stackup & Impedance Control
*Calculated for JLC06161H-3313 Prepreg/Core heights.*

| Layer | Type | Usage | Impedance |
|:---|:---|:---|:---|
| **L1 (Top)** | Signal | High-Speed Diff Pairs | 85Ω / 100Ω |
| **L2** | Plane | **GND (Solid Reference)** | N/A |
| **L3** | Signal | Low-Speed Data (SPI/UART) | 50Ω Single |
| **L4** | Plane | **VCC (5V / 3.3V Split)** | N/A |
| **L5** | Plane | **GND (Solid Reference)** | N/A |
| **L6 (Bot)** | Signal | GPIO / Low-Speed | 50Ω Single |

### 2.1 Controlled Impedance Trace Widths
| Interface | Target | Trace Width | Gap | Layer |
|:---|:---|:---|:---|:---|
| **PCIe Gen 3** | 85Ω Diff | 0.127mm (5.0mil) | 0.152mm (6.0mil) | L1 |
| **SATA / USB** | 100Ω Diff | 0.102mm (4.0mil) | 0.178mm (7.0mil) | L1 |
| **Single-Ended**| 50Ω | 0.203mm (8.0mil) | N/A | L1 / L3 |

---

## 3. Design Rules (DRC) Constraints

### 3.1 Via-In-Pad (VIPPO)
* **Allowed:** Yes.
* **Requirement:** Vias under BGA (i.MX8) or high-density SMT (SEARAY) must be **Epoxy Filled and Capped** (JLC "Plugged" process) to prevent solder wicking.

### 3.2 Mechanical Clearances
* **Edge Keepout:** No copper within **2.0mm** of the PCB edge to prevent shorting against the Aluminum L-Frame.
* **Component Height:** * Top Side Max: 20.0mm
    * Bottom Side Max: 3.5mm (to clear chassis floor)

---

## 4. Footprint Requirements

### 4.1 SEARAY (SEAF-RA)
* **Solder Mask Expansion:** 0.05mm (2mil).
* **Paste Mask:** 1:1 ratio.
* **Alignment:** Ensure **GP (Guide Post)** holes are non-plated and sized correctly per Samtec spec (±0.05mm tolerance).

### 4.2 Thermal Interface
* High-thermal components (SoC/PMIC) must include a **Thermal Via Array** (minimum 4x4, 0.3mm holes) tied to the L5/L6 Ground planes for conduction cooling.

---

## 5. Ordering Checklist
When submitting to JLCPCB or similar fab:
1. **Layer Stackup:** Select "JLC06161H-3313".
2. **Impedance Control:** Select "Yes" and attach the Meridian Stackup table.
3. **Surface Finish:** Must be **ENIG**.
4. **Via Process:** Select "Plugged via" for designs using Via-in-Pad.

---
**Nadir Labs** | *Steward of the Meridian Standard*
