# Thermal Analysis & Design of Semiconductor Chip Packaging using ANSYS

[![ANSYS AEDT](https://img.shields.io/badge/ANSYS-AEDT%20%7C%20Icepak-red.svg?style=for-the-badge&logo=ansys)](https://www.ansys.com/)
[![Packaging Technology](https://img.shields.io/badge/Packaging-Wirebond%20%7C%20FlipChip%20%7C%202.5D%2F3D-blue.svg?style=for-the-badge)](https://en.wikipedia.org/wiki/Semiconductor_package)
[![Thermal Reliability](https://img.shields.io/badge/Reliability-JEDEC%20%7C%20HAST%20%7C%20Burn--In-green.svg?style=for-the-badge)](https://www.jedec.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](LICENSE)

A comprehensive theoretical and practical guide to **Semiconductor Packaging Architectures**, **Cleanroom Assembly Processes**, **Reliability & Environmental Stress Testing**, and **Finite Element Thermal Simulation** using **ANSYS Electronics Desktop (AEDT / Icepak)** and **Q3D Extractor**.

---

## Table of Contents
1. [Executive Overview & The Role of Packaging](#1-executive-overview--the-role-of-packaging)
2. [Module 1: Packaging Evolution — From Basics to 3D Integration](#2-module-1-packaging-evolution--from-basics-to-3d-integration)
   - [L1: Introduction to Semiconductor Packaging & Industry Ecosystem](#l1-introduction-to-semiconductor-packaging--industry-ecosystem)
   - [L2: Package Requirements & Foundational Architectures](#l2-package-requirements--foundational-architectures)
   - [L3: Evolving Architectures — Monolithic Limits, MCMs, and SiP](#l3-evolving-architectures--monolithic-limits-mcms-and-sip)
   - [L4: Interposers, Redistribution Layers (RDL), and 2.5D/3D Integration](#l4-interposers-redistribution-layers-rdl-and-25d3d-integration)
   - [L5: Comparative Analysis & Package Selection Matrix](#l5-comparative-analysis--package-selection-matrix)
3. [Module 2: From Wafer to Package — Assembly & Manufacturing Essentials](#3-module-2-from-wafer-to-package--assembly--manufacturing-essentials)
   - [L1: Manufacturing Supply Chain, Cleanrooms & Facilities](#l1-manufacturing-supply-chain-cleanrooms--facilities)
   - [L2: Wafer Pre-Preparation — Backgrinding, Stress Relief & Dicing](#l2-wafer-pre-preparation--backgrinding-stress-relief--dicing)
   - [L3: Wire Bond Packaging — Die Attach to Transfer Molding](#l3-wire-bond-packaging--die-attach-to-transfer-molding)
   - [L4: Flip-Chip Assembly — Solder Bump Formation & Underfill Mechanics](#l4-flip-chip-assembly--solder-bump-formation--underfill-mechanics)
   - [L5: Wafer-Level Packaging (WLP) & Fan-Out Reconstitution](#l5-wafer-level-packaging-wlp--fan-out-reconstitution)
4. [Module 3: Labs — Thermal Simulation of Semiconductor Packages with ANSYS](#4-module-3-labs--thermal-simulation-of-semiconductor-packages-with-ansys)
   - [L1: Getting Started with ANSYS Electronics Desktop (AEDT) Icepak](#l1-getting-started-with-ansys-electronics-desktop-aedt-icepak)
   - [L2: Setting Up a Flip-Chip BGA Package Model](#l2-setting-up-a-flip-chip-bga-package-model)
   - [L3: Material Definitions & Volumetric Thermal Power Sources](#l3-material-definitions--volumetric-thermal-power-sources)
   - [L4: Finite Element Mesh Generation & Refinement Strategy](#l4-finite-element-mesh-generation--refinement-strategy)
   - [L5: Thermal Field Analysis, Temperature Contours & Results](#l5-thermal-field-analysis-temperature-contours--results)
5. [Module 4: Ensuring Package Reliability — Testing & Performance Validation](#5-module-4-ensuring-package-reliability--testing--performance-validation)
   - [L1: Multi-Stage Testing Pipeline & Electrical Functionality Checks](#l1-multi-stage-testing-pipeline--electrical-functionality-checks)
   - [L2: Assembly Open/Short Test (AOST) & Failure Mechanisms](#l2-assembly-openshort-test-aost--failure-mechanisms)
   - [L3: Burn-In Screening, Accelerated Aging & The Bathtub Curve](#l3-burn-in-screening-accelerated-aging--the-bathtub-curve)
   - [L4: Environmental Qualification & Automated Test Equipment (ATE)](#l4-environmental-qualification--automated-test-equipment-ate)
6. [Module 5: Package Design & Modeling — Building a Package from Scratch in AEDT](#6-module-5-package-design--modeling--building-a-package-from-scratch-in-aedt)
   - [L1: Virtual Package Cross-Section Modeling Principles](#l1-virtual-package-cross-section-modeling-principles)
   - [L2: 2D Planar Geometry Sketching in 3D Modeler](#l2-2d-planar-geometry-sketching-in-3d-modeler)
   - [L3: Solid Thickening & Multi-Layer Stackup Construction](#l3-solid-thickening--multi-layer-stackup-construction)
   - [L4: Material Assignment from AEDT SysLibrary](#l4-material-assignment-from-aedt-syslibrary)
   - [L5: Complete Package Assembly & Validation](#l5-complete-package-assembly--validation)
7. [Repository Structure](#7-repository-structure)
8. [References & Acknowledgements](#8-references--acknowledgements)

---

## 1. Executive Overview & The Role of Packaging

In modern microelectronics, **Semiconductor Packaging** is no longer just a passive protective shell; it is an active enabler of chip performance, power delivery, and system scaling. As traditional **Dennard scaling** and **Moore's Law** face physical and economic barriers (reticle size limits, exploding mask costs, dielectric breakdown), performance scaling has transitioned toward **Heterogeneous Integration (HI)**, **Chiplets**, and advanced **2.5D/3D Packaging**.

<p align="center">
  <img src="images/Screenshot%202026-10-19%20232739.png" width="850" alt="Typical Package Structure">
  <br>
  <em>Figure 1.1: Typical semiconductor package structure showcasing carrier types, interconnection styles, through-hole mountings (DIP, TO, PGA), surface-mount technology (QFN, QFP, CSP, PBGA, LGA, PoP), and multi-chip modules (Intel Broadwell, NVIDIA H100 CoWoS).</em>
</p>

### Fundamental Functions of a Package:
1. **Mechanical Protection:** Shields fragile semiconductor silicon dies ($\sim 50\text{--}750\,\mu\text{m}$ thick) against external handling, mechanical shock, vibration, moisture ingress, and particulate contamination.
2. **Electrical Routing & Power Delivery:** Routes power, ground, and high-frequency signals between sub-micron die bond pads and macroscopic printed circuit boards (PCBs) while controlling parasitic inductance ($L$), capacitance ($C$), and resistance ($R$).
3. **Thermal Dissipation:** Dissipates concentrated volumetric heat generated within active transistors ($\sim 50\text{--}150\,\text{W/cm}^2$) to the ambient environment to keep junction temperatures ($T_j$) below safe limits (typically $85\text{--}105^\circ\text{C}$).
4. **Physical Bridge & Space Transformation:** Fans out fine-pitch die interconnects ($\sim 20\text{--}100\,\mu\text{m}$ pitch) to board-compatible printed circuit board pitches ($0.4\text{--}1.0\,\text{mm}$ pitch).

---

## 2. Module 1: Packaging Evolution — From Basics to 3D Integration

### L1: Introduction to Semiconductor Packaging & Industry Ecosystem
- **Evolving Industry Dynamics:** The semiconductor value chain is bifurcated into:
  - **Front-End Foundries (Pure-play fabs):** Dedicated to wafer fabrication, lithography, etching, and chemical vapor deposition (e.g., TSMC, Intel Foundry, Samsung).
  - **Back-End Assembly & Test (OSAT / ATMP):** Dedicated to wafer thinning, dicing, assembly, die attach, wire bonding / flip-chip reflow, encapsulation, burn-in, and final testing (e.g., ASE, Amkor, JCET).
- **Heterogeneous Integration Paradigm:** With monolithic System-on-Chip (SoC) dies exceeding $800\,\text{mm}^2$, manufacturing yield drops precipitously according to Murphy's and Poisson's yield models:
  $$Y = \left( \frac{1 - e^{-A \cdot D}}{A \cdot D} \right)^2 \quad \text{or} \quad Y = e^{-A \cdot D}$$
  where $A$ is the die area and $D$ is defect density. Breaking large monolithic chips into smaller, modular **chiplets** connected across high-density packaging substrates dramatically elevates effective yields and reduces development costs.

---

### L2: Package Requirements & Foundational Architectures

Semiconductor packages must simultaneously satisfy three coupled physical domains:

```
                      ┌──────────────────────────────────────────────┐
                      │    Semiconductor Packaging Requirements      │
                      └──────────────────────┬───────────────────────┘
                                             │
         ┌───────────────────────────────────┼───────────────────────────────────┐
         ▼                                   ▼                                   ▼
┌──────────────────┐               ┌──────────────────┐                ┌──────────────────┐
│    Electrical    │               │     Thermal      │                │    Mechanical    │
├──────────────────┤               ├──────────────────┤                ├──────────────────┤
│• Low parasitic R │               │• Heat flux mgmt  │                │• CTE match mgmt  │
│• Controlled Z0   │               │• Low θ_ja, θ_jc  │                │• Warpage control │
│• High bandwidth  │               │• Uniform spread  │                │• Joint integrity │
│• Low crosstalk   │               │• Safe Tj limit   │                │• Shock/vibe drop │
└──────────────────┘               └──────────────────┘                └──────────────────┘
```

#### 1. Electrical Performance
High signal switching speeds ($>10\text{--}112\,\text{Gbps}$ PAM4) require strictly controlled characteristic impedances ($Z_0 \approx 50\,\Omega$) and minimal parasitic lead inductance:
$$V_{\text{noise}} = L \frac{di}{dt}$$
Lowering interconnect length reduces simultaneous switching noise (SSN) and ground bounce.

#### 2. Thermal Management
Heat generated in the active junction ($T_j$) must conduct through internal Thermal Interface Materials (TIMs) to the package lid/spreader and heat sink:
$$T_j = T_a + P \cdot \theta_{ja} = T_a + P \cdot (\theta_{jc} + \theta_{cs} + \theta_{sa})$$
where $\theta_{ja}$ is the junction-to-ambient thermal resistance, $\theta_{jc}$ is junction-to-case, $\theta_{cs}$ is case-to-sink, and $\theta_{sa}$ is sink-to-ambient.

#### 3. Mechanical & Thermo-Mechanical Integrity
Because silicon ($2.6\text{--}3.2 \times 10^{-6}/\text{K}$), copper ($16.5 \times 10^{-6}/\text{K}$), FR4 substrate ($14\text{--}18 \times 10^{-6}/\text{K}$), and epoxy molding compound ($10\text{--}25 \times 10^{-6}/\text{K}$) have mismatched **Coefficients of Thermal Expansion (CTE)**, thermal excursions generate severe cyclic shear strain ($\gamma$) in interconnect joints:
$$\Delta \gamma = \frac{L_{\text{DNP}} \cdot \Delta \alpha \cdot \Delta T}{h_{\text{joint}}}$$
where $L_{\text{DNP}}$ is Distance to Neutral Point, $\Delta \alpha$ is the CTE mismatch, $\Delta T$ is the thermal cycle amplitude, and $h_{\text{joint}}$ is joint standoff height.

<p align="center">
  <img src="images/Screenshot%202026-10-19%20234942.png" width="850" alt="Anatomy of Packages">
  <br>
  <em>Figure 1.2: Anatomy of packages: Leadframe (DIP, QFN, Leadframe-CSP, Leadframe-QFP), Laminate Substrates (Wire bond PBGA, Flip-Chip PBGA, LGA, FC-CSP), and Advanced Package Substrates (2D, 2.1D RDL, 2.3D Organic Interposer, 2.5D Silicon Interposer / CoWoS).</em>
</p>

---

### L3: Evolving Architectures — Monolithic Limits, MCMs, and SiP
- **Single Chip Packaging:** Encapsulates a solitary silicon die. As I/O counts grew beyond leadframe limits ($>200\text{ pins}$), area-array Ball Grid Array (BGA) and Chip-Scale Packages (CSP) emerged.
- **Multi-Chip Modules (MCM):** Integrates multiple distinct silicon dies placed side-by-side on a shared multilayer ceramic or organic laminate substrate (e.g., CPU + cache or multichip compute blocks).
- **System-in-Package (SiP):** Unifies multiple integrated circuits (processors, DRAM, flash, RF front-ends, and passive passives) into a single functional package, acting as a complete miniaturized electronic system.

---

### L4: Interposers, Redistribution Layers (RDL), and 2.5D/3D Integration

<p align="center">
  <img src="images/Screenshot%202026-10-19%20235453.png" width="850" alt="Summary Nomenclature of Packages">
  <br>
  <em>Figure 1.3: Classification and hierarchy of advanced semiconductor packaging architectures (Source: John H. Lau, Semiconductor Advanced Packaging), detailing single-chip (PBGA, fcCSP) and multi-chip spectrums (2D, 2.1D thin-film, 2.3D organic interposer, 2.5D passive TSV interposer, and 3D active TSV integration).</em>
</p>

#### Dimensional Categorization:
- **2D Packaging:** Multiple dies placed horizontally on an organic laminate substrate (e.g., standard FCBGA). Die-to-die communication is limited by package substrate trace width and spacing ($L/S \approx 10\text{--}15\,\mu\text{m}$).
- **2.1D Packaging:** High-density thin-film **Redistribution Layers (RDL)** fabricated on the substrate surface ($L/S \approx 2\text{--}5\,\mu\text{m}$) without requiring silicon interposers.
- **2.3D Packaging:** Organic interposers with fine-pitch metal routing lines, offering an intermediate cost-performance trade-off between standard laminates and silicon interposers.
- **2.5D Packaging:** Dies (such as SoC/GPU compute engines and High Bandwidth Memory stacks, HBM3/HBM3e) attached face-down via micro-bumps onto a **passive Silicon Interposer** containing **Through-Silicon Vias (TSVs)** and sub-micron RDL routing ($L/S \le 1\,\mu\text{m}$). Prominent example: **TSMC CoWoS (Chip-on-Wafer-on-Substrate)** used in NVIDIA A100/H100/B200 GPUs.
- **3D Packaging:** Silicon dies stacked directly atop one another, interconnected vertically using through-silicon vias (TSVs) or bumpless **Copper-to-Copper Direct Hybrid Bonding** (e.g., AMD 3D V-Cache, Intel Foveros Direct), reducing interconnect lengths to $<10\,\mu\text{m}$.

---

### L5: Comparative Analysis & Package Selection Matrix

<p align="center">
  <img src="images/Screenshot%202026-10-19%20235733.png" width="850" alt="Package Comparison Matrix">
  <br>
  <em>Figure 1.4: Comprehensive comparison of semiconductor packaging solutions highlighting trade-offs between cost, assembly complexity, thermal dissipation, form factor, and industrial use cases.</em>
</p>

| IC Package Type | Key Advantages (Pros) | Limitations & Trade-Offs (Cons) | Primary Application Domains |
| :--- | :--- | :--- | :--- |
| **DIP** (Dual In-line) | Ultra-low cost, easy manual/socket assembly, high mechanical ruggedness | Bulky form factor, strictly through-hole, low pin count ($<64$), high parasitic $L$ | Consumer electronics, industrial controllers, legacy avionics |
| **QFN** (Quad Flat No-Lead) | Compact footprint, exposed thermal paddle provides excellent heat dissipation, low inductance | Edge solder joints difficult to inspect, limited reworkability, lower I/O count than QFP | Smartphones, tablets, automotive ECUs, power management ICs |
| **QFP** (Quad Flat Package) | Higher pin density ($>200\text{ pins}$), perimeter leads ease visual & automated optical inspection (AOI) | Fragile gull-wing leads prone to bending/damage, difficult lead co-planarity control | Microcontrollers, automotive microprocessors, ASICs |
| **PBGA** (Plastic BGA) | High I/O density ($>1000\text{ balls}$), area-array layout, excellent thermal and electrical routing | Hidden solder joints require X-ray inspection, difficult rework, susceptible to moisture warpage | High-performance computing, networking switch ASICs |
| **CSP** (Chip Scale Package) | Package size $\le 1.2\times$ die size, ultra-short trace paths, minimal parasitic capacitance | Stringent PCB routing rules, solder fatigue reliability risks under aggressive thermal cycling | Mobile application processors, wearable sensors, IoT nodes |
| **2D Multi-Chip** | Higher integration density, heterogeneous silicon combination without monolithic yield penalty | Longer die-to-die trace latency, limited routing pitch on standard organic laminates | Data center server modules, wireless RF baseband modules, space avionics |
| **2.1D (Polymer RDL)** | High I/O density and routing resolution ($2\text{--}5\,\mu\text{m}$) at lower cost than silicon interposers | Thermo-mechanical warpage risks from polymer-copper CTE mismatch, lower wire density than 2.5D | High-performance client computing, AI inference accelerators |
| **2.5D (Si Interposer / CoWoS)** | Massive interconnect throughput ($>1024\text{ bits/interface}$), ultra-low latency, heterogeneous integration (SoC + HBM) | Significant silicon substrate cost, multi-step assembly yield risk, complex thermal co-design | Flagship AI/ML training accelerators (NVIDIA H100/B200), supercomputers |

---

## 3. Module 2: From Wafer to Package — Assembly & Manufacturing Essentials

### L1: Manufacturing Supply Chain, Cleanrooms & Facilities
- **Foundry-to-OSAT Transition:** Following front-end fabrication, complete wafers undergo **Wafer Probe (Chip Probing, CP)** using automated probe cards to identify non-functional dies. Defective dies are electronically mapped (wafer map) or marked with ink.
- **Cleanroom Protocol:** Assembly occurs inside certified cleanroom environments (ISO Class 5 to Class 7; Federal Standard 209E Class 100 to 10,000) to prevent airborne particulate contamination on exposed die bond pads:

$$\text{Particles per } m^3 \le 10^N \times \left( \frac{0.1}{\text{Size in } \mu\text{m}} \right)^{2.08}$$

Strict Electrostatic Discharge (ESD) shielding protocols prevent gate dielectric puncture.

---

### L2: Wafer Pre-Preparation — Backgrinding, Stress Relief & Dicing
1. **Backgrinding (Wafer Thinning):** Incoming raw wafers ($\sim 775\,\mu\text{m}$ for $300\,\text{mm}$ wafers) are mounted on UV-curable grinding tape and mechanically ground using diamond-impregnated grinding wheels down to $50\text{--}100\,\mu\text{m}$.
2. **Stress Relief:** Mechanical grinding introduces subsurface micro-cracks and residual stresses. Chemical etching (wet acid or dry chemical spin-etching) or Chemical-Mechanical Polishing (CMP) is applied to restore silicon fracture strength.
3. **Wafer Dicing Techniques:**
   - **Mechanical Saw Dicing:** High-speed air-bearing spindles ($30,000\text{--}60,000\,\text{RPM}$) with nickel-plated diamond blades accompanied by continuous DI water jet cooling.
   - **Stealth Laser Dicing:** A semi-transparent infrared laser creates internal micro-cracks within the silicon bulk without surface ablation, followed by tape expansion to singulate dies with zero kerf loss.
   - **Plasma Dicing (DRIE):** Deep Reactive-Ion Etching with Bosch process chemistry ($SF_6 / C_4F_8$) etching all scribe lines simultaneously with zero mechanical chipping and high die fracture strength.

---

### L3: Wire Bond Packaging — Die Attach to Transfer Molding

<p align="center">
  <img src="images/Screenshot%202026-10-22%20002822.png" width="850" alt="Activities inside Cleanroom Wire Bond Packaging">
  <br>
  <em>Figure 2.1: End-to-end cleanroom assembly sequence for wire-bonded packages: Epoxy dispensing on leadframe / substrate &rarr; Chip pick-and-place &rarr; Thermal oven curing &rarr; Thermosonic wire bonding &rarr; Transfer molding encapsulation &rarr; Laser marking &rarr; Singulation.</em>
</p>

#### Step-by-Step Cleanroom Flow:
1. **Die Attach:** Silver-filled conductive epoxy or Die Attach Film (DAF) is dispensed onto the carrier flag. A high-speed robotic pick-and-place head transfers the singulated die onto the adhesive layer.
2. **Thermal Curing:** The assembly is baked in an inert atmosphere ($N_2$) convection oven at $150\text{--}175^\circ\text{C}$ to cross-link the polymer resin and establish a void-free interface.
3. **Wire Bonding:**

<p align="center">
  <img src="images/Screenshot%202026-10-22%20002349.png" width="700" alt="Thermosonic Wire Bonding Cycle">
  <br>
  <em>Figure 2.2: Micro-kinetics of the thermosonic wire bonding cycle: Ceramic capillary &rarr; Electronic Flame-Off (EFO) spark producing Free Air Ball (FAB) &rarr; Ultrasound + normal compressive force forming the first ball bond &rarr; Looping trajectory &rarr; Crescent (wedge) second bond on substrate &rarr; Wire clamp tear.</em>
</p>

- **Electronic Flame-Off (EFO):** A high-voltage electric arc melts the exposed wire tail, forming a spherical Free Air Ball (FAB) governed by surface tension.
- **First Bond (Ball Bond):** The ceramic capillary presses the FAB onto the aluminum die pad while applying ultrasonic acoustic energy ($60\text{--}120\,\text{kHz}$) and heat ($150\text{--}220^\circ\text{C}$), generating an intermetallic bond ($Au\text{-}Al$ or $Cu\text{-}Al$).
- **Loop Profile Formation:** The capillary maneuvers through a precisely programmed 3D trajectory to control loop height, wire span, and clearance.
- **Second Bond (Crescent / Wedge Bond):** The capillary tip deforms the wire against the leadframe finger, ultrasonic energy bonds the wire, and the wire clamp closes to shear the wire at the heel.

<p align="center">
  <img src="images/Screenshot%202026-10-22%20002706.png" width="700" alt="HB100 Automatic Wire Bonder">
  <br>
  <em>Figure 2.3: Industrial automatic wire bonding equipment (TPT HB100) featuring multi-axis motorized stages, optical pattern recognition, and ultrasonic transducer heads.</em>
</p>

4. **Encapsulation (Transfer Molding):** The leadframe strips are placed into heated mold cavities ($170\text{--}180^\circ\text{C}$). Thermosetting Epoxy Molding Compound (EMC pellets) is hydraulically injected under pressure to encapsulate the delicate wire bonds and dies without wire sweep.
5. **Post-Mold Cure (PMC) & Laser Marking:** Cured at $175^\circ\text{C}$ for $4\text{--}8\,\text{hours}$ to maximize polymer cross-linking density, followed by UV or fiber laser marking of device part numbers.
6. **Singulation / Trim & Form:** High-precision punch tools or diamond saws separate individual packaged units from leadframe strips.

---

### L4: Flip-Chip Assembly — Solder Bump Formation & Underfill Mechanics

<p align="center">
  <img src="images/Screenshot%202026-10-22%20160614.png" width="850" alt="Flip Chip Packaging Assembly Flow">
  <br>
  <em>Figure 2.4: Flip-chip packaging manufacturing line: Solder bump formation on wafer &rarr; Flipping die face-down &rarr; Flux dispensing on substrate pads &rarr; High-accuracy die placement &rarr; Mass solder reflow / thermo-compression &rarr; Solvent flux cleaning &rarr; Capillary underfill (CUF) dispensing & thermal curing &rarr; Overmolding &rarr; BGA ball mounting and reflow.</em>
</p>

#### Physical Mechanisms:
1. **Under Bump Metallization (UBM) & Bump Formation:** On-chip aluminum/copper pads are covered with thin-film barrier layers ($Ti/Cu/Ni$) to prevent solder intermetallic dissolution. Lead-free solder micro-bumps ($Sn\text{-}Ag\text{-}Cu$, SAC305) or copper pillars with solder caps are electroplated onto the pads.
2. **Chip Inversion & Alignment:** The die is flipped face-down. Solder bumps are aligned with matching substrate pads using split-beam optical vision systems.
3. **Reflow & Metallurgical Interdiffusion:**
   - **Mass Reflow:** Driven through a multi-zone convection furnace under $N_2$ atmosphere following a precise temperature profile ($T_{\text{peak}} \approx 245\text{--}260^\circ\text{C}$ for SAC solders). Solder melts and self-aligns the die through surface tension.
   - **Thermo-Compression Bonding (TCB):** A heated bond head applies force and heat directly to individual dies, utilized for ultra-fine-pitch micro-bumps ($<40\,\mu\text{m}$).
4. **Capillary Underfill (CUF):** A specialized low-viscosity epoxy resin filled with silica particles ($SiO_2$) is dispensed along the edge of the die. Capillary force draws the underfill into the $20\text{--}80\,\mu\text{m}$ standoff gap between die and substrate:

$$v_{\text{flow}} = \frac{\gamma \cdot \cos(\theta) \cdot h}{6 \mu \cdot x}$$

where $\gamma$ is surface tension, $\theta$ is contact angle, $h$ is gap height, $\mu$ is dynamic viscosity, and $x$ is penetration distance.
- **Thermal Significance of Underfill:** Without underfill, thermal cycling causes solder fatigue cracks at the corner bumps due to the large CTE mismatch between silicon ($2.8 \times 10^{-6}/\text{K}$) and organic substrate ($15 \times 10^{-6}/\text{K}$). Underfill redistributes the shear strain across the entire die area, increasing solder joint fatigue life by $>10\times$.

<p align="center">
  <img src="images/Screenshot%202026-10-22%20161958.png" width="700" alt="Amkor Solder Ball Attach Equipment">
  <br>
  <em>Figure 2.5: Automated solder ball attach and inspection cell inside an OSAT manufacturing facility (Amkor Technology).</em>
</p>

---

### L5: Wafer-Level Packaging (WLP) & Fan-Out Reconstitution

<p align="center">
  <img src="images/Screenshot%202026-10-22%20161931.png" width="850" alt="Wafer Level Packaging and Reconstitution Process">
  <br>
  <em>Figure 2.6: Fan-Out Wafer-Level Packaging (FOWLP) reconstitution line: Dicing wafer &rarr; Pick-and-place Known Good Dies (KGD) onto temporary carrier &rarr; Epoxy overmolding into artificial reconstituted wafer &rarr; Carrier release &rarr; Multi-layer RDL dielectric coating and copper electroplating &rarr; Solder ball drop &rarr; Singulation.</em>
</p>

- **Fan-In WLP (Standard WLCSP):** All package solder balls are placed directly over the active silicon footprint. Final package size equals die size. Pin count is limited by die surface area.
- **Fan-Out WLP (FOWLP):** Solves the area constraint by embedding Known Good Dies (KGD) inside an artificial epoxy mold wafer. **Redistribution Layers (RDL)** fan out connections beyond the silicon perimeter onto the mold compound zone, enabling high I/O counts with thin profiles and excellent thermal performance.

---

## 4. Module 3: Labs — Thermal Simulation of Semiconductor Packages with ANSYS

Thermal management of high-power packages requires numerical simulation of 3D conjugate heat transfer and fluid dynamics. ANSYS Electronics Desktop (AEDT) integrates **ANSYS Icepak**, a computational fluid dynamics (CFD) and thermal solver based on the finite volume/element formulation.

```
                  ┌──────────────────────────────────────────────┐
                  │          ANSYS Icepak Lab Workflow           │
                  └──────────────────────┬───────────────────────┘
                                         │
 ┌───────────────────────────────────────┼───────────────────────────────────────┐
 │                                       │                                       │
 ▼                                       ▼                                       ▼
┌────────────────────────┐     ┌────────────────────────┐      ┌────────────────────────┐
│   Geometric Setup      │     │  Physics & Boundaries  │      │ Meshing & Solution     │
├────────────────────────┤     ├────────────────────────┤      ├────────────────────────┤
│• Icepak SteadyState    │     │• Material conductivities│     │• Hexahedral/tet mesh   │
│• Toolkit BGA macro     │     │• Volumetric die heat P │      │• Local mesh refinement │
│• 8.56x8.56 mm Die      │     │• Ambient conv (h, T∞)  │      │• 32,042 elements       │
│• 14x14 Solder ball net │     │• Radiation boundaries  │      │• Convergence criteria  │
└────────────────────────┘     └────────────────────────┘      └───────────┬────────────┘
                                                                           │
                                                                           ▼
                                                               ┌────────────────────────┐
                                                               │  Post-Processing (Tj)  │
                                                               ├────────────────────────┤
                                                               │• Max Tj = 137.640 °C   │
                                                               │• Thermal gradient field│
                                                               │• Bottleneck evaluation │
                                                               └────────────────────────┘
```

### Governing Heat Transfer Equations:
1. **Fourier Heat Conduction in 3D Solid Domains:**
   $$\nabla \cdot (k \nabla T) + \dot{q}_{\text{gen}} = \rho C_p \frac{\partial T}{\partial t}$$
   In steady state ($\frac{\partial T}{\partial t} = 0$):
   $$\frac{\partial}{\partial x}\left(k_x \frac{\partial T}{\partial x}\right) + \frac{\partial}{\partial y}\left(k_y \frac{\partial T}{\partial y}\right) + \frac{\partial}{\partial z}\left(k_z \frac{\partial T}{\partial z}\right) + \dot{q}_{\text{gen}} = 0$$

2. **Convective Boundary Conditions (Newton's Law of Cooling):**
   $$-k \left. \frac{\partial T}{\partial n} \right|_{\text{surface}} = h (T_{\text{surface}} - T_\infty)$$

3. **Radiative Heat Transfer (Stefan-Boltzmann Formulation):**
   $$q_{\text{rad}} = \epsilon \sigma (T_{\text{surface}}^4 - T_{\text{ambient}}^4)$$

---

### L1: Getting Started with ANSYS Electronics Desktop (AEDT) Icepak

<p align="center">
  <img src="images/Screenshot%202026-10-25%20111815.png" width="850" alt="AEDT Icepak Interface">
  <br>
  <em>Figure 3.1: ANSYS Electronics Desktop (AEDT) Student 2024 R2 workspace initialized with an Icepak SteadyState design environment, displaying the 3D modeler tree, global boundary domain, and analysis managers.</em>
</p>

- **Design Environment Setup:** Launch AEDT &rarr; Select `Project` &rarr; `Insert Icepak Design`.
- **Solution Type:** Selected as `SteadyState` thermal conduction and natural convection mode.

---

### L2: Setting Up a Flip-Chip BGA Package Model

<p align="center">
  <img src="images/Screenshot%202026-10-25%20112421.png" width="850" alt="AEDT Toolkit Menu">
  <br>
  <em>Figure 3.2: Accessing parametric packaging macros in AEDT: Icepak &rarr; Toolkit &rarr; Packages &rarr; Flipchip_BGA.</em>
</p>

Using the built-in parametric package toolkit, complex multi-layer geometries are generated with exact parametric dimensions:

<p align="center">
  <img src="images/Screenshot%202026-10-25%20115139.png" width="750" alt="Create Flipchip BGA Package Die Setup">
  <br>
  <em>Figure 3.3: Flip-Chip BGA parametric generator dialog: Die length ($X = 8.56\,\text{mm}$, $Y = 8.56\,\text{mm}$), Active Power ($P = 1.0\,\text{W}$), Material selection (Si-Typical), and Underfill gap thickness ($0.01\,\text{mm}$).</em>
</p>

<p align="center">
  <img src="images/Screenshot%202026-10-25%20121445.png" width="750" alt="Solder Ball Array Configuration">
  <br>
  <em>Figure 3.4: Solder ball array configuration: $14 \times 14$ Full Array (196 solder joints), Ball Pitch ($1.0\,\text{mm}$), Ball Diameter ($0.5\,\text{mm}$), Ball Height ($0.5\,\text{mm}$), and Ball Material (Solder-pb50_sn50).</em>
</p>

<p align="center">
  <img src="images/Screenshot%202026-10-25%20121558.png" width="850" alt="3D Flip-Chip BGA Geometry Render">
  <br>
  <em>Figure 3.5: 3D CAD visualization of the generated Flip-Chip BGA package inside the computational thermal bounding box.</em>
</p>

---

### L3: Material Definitions & Volumetric Thermal Power Sources

<p align="center">
  <img src="images/Screenshot%202026-10-25%20122733.png" width="750" alt="Assign Source Thermal Model">
  <br>
  <em>Figure 3.6: Thermal source specification: Defining a 1.0 W active uniform heat load on Flipchip_BGA1_die_source representing core transistor power dissipation.</em>
</p>

<p align="center">
  <img src="images/Screenshot%202026-10-25%20125103.png" width="850" alt="Solids and Material Tree">
  <br>
  <em>Figure 3.7: AEDT Model Tree displaying structural components and material assignments: Silicon Die (Si-Typical), Underfill, Substrate (FR4_epoxy), Vias, Copper Traces, and Solder Bumps (Pb50_Sn50).</em>
</p>

#### Thermo-Physical Properties Assigned in Simulation:

| Component | Assigned Material | Thermal Conductivity $k$ ($\text{W/m}\cdot\text{K}$) | Density $\rho$ ($\text{kg/m}^3$) | Specific Heat $C_p$ ($\text{J/kg}\cdot\text{K}$) | CTE $\alpha$ ($10^{-6}/\text{K}$) |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Silicon Die** | `Si-Typical` | $148.0$ (isotropic) | $2330$ | $712$ | $2.6$ |
| **Substrate Core** | `FR4_epoxy` | $k_{xy} = 0.81$, $k_z = 0.35$ (anisotropic) | $1900$ | $1200$ | $14.0$ ($xy$), $65.0$ ($z$) |
| **Die Underfill** | `Flipchip_underfill` | $0.85$ | $1650$ | $950$ | $28.0$ |
| **Solder Bumps** | `Solder-pb50_sn50` | $48.0$ | $8900$ | $167$ | $24.0$ |
| **Metal Traces** | `Copper` | $400.0$ | $8933$ | $385$ | $16.5$ |
| **Ambient Air** | `Air` | $0.026$ | $1.161$ | $1007$ | — |

---

### L4: Finite Element Mesh Generation & Refinement Strategy

<p align="center">
  <img src="images/Screenshot%202026-10-25%20152435.png" width="850" alt="Icepak Mesh Visualization">
  <br>
  <em>Figure 3.8: Finite element mesh visualization on a horizontal cut plane ($P_z = 0.75\,\text{mm}$): Total design mesh count of 32,042 elements, highlighting dense element sizing across the micro-bump and active die domain to capture steep thermal gradients.</em>
</p>

- **Mesh Control Strategy:** Due to the aspect ratio disparity between the thin die underfill ($10\,\mu\text{m}$) and macroscopic substrate ($>10\,\text{mm}$), non-conformal mesh subdomains are defined to optimize solve time without losing boundary-layer gradient accuracy.
- **Mesh Elements:** $32,042$ cells with refinement around high heat-flux contact interfaces.

---

### L5: Thermal Field Analysis, Temperature Contours & Results

<p align="center">
  <img src="images/Screenshot%202026-10-25%20154227.png" width="850" alt="Thermal Contour Solved Results">
  <br>
  <em>Figure 3.9: Solved steady-state temperature field distribution for the Flip-Chip BGA package under 1.0 W power dissipation: Peak junction temperature reaches $T_{j,\max} = 137.640^\circ\text{C}$ (localized at the active die core, red contour) decaying through underfill and substrate down to $20^\circ\text{C}$ ambient.</em>
</p>

<p align="center">
  <img src="images/Screenshot%202026-10-25%20154842.png" width="850" alt="Isometric Thermal Plot">
  <br>
  <em>Figure 3.10: Isometric view of temperature distribution across the die and laminate substrate, illustrating lateral heat spreading through the package substrate.</em>
</p>

#### Key Thermal Findings:
1. **Hotspot Localization:** The peak junction temperature reaches **$137.640^\circ\text{C}$** at the central core of the active silicon surface.
2. **Thermal Resistance Breakdown:** In the absence of an attached top lid/heat sink, heat is forced to conduct downward through the underfill ($k = 0.85\,\text{W/m}\cdot\text{K}$) and $14 \times 14$ solder ball array into the laminate substrate.
3. **Design Recommendations:**
   - Attach a copper integrated heat spreader (IHS) with high thermal conductivity TIM-1 ($k \ge 5\text{--}8\,\text{W/m}\cdot\text{K}$) over the die backside.
   - Introduce thermal vias in the substrate directly under the die footprint to lower vertical thermal resistance $\theta_{jc}$.

---

## 5. Module 4: Ensuring Package Reliability — Testing & Performance Validation

### L1: Multi-Stage Testing Pipeline & Electrical Functionality Checks

<p align="center">
  <img src="images/Screenshot%202026-10-22%20162125.png" width="850" alt="Testing at Different Stages">
  <br>
  <em>Figure 4.1: Industrial test roadmap across Foundry and OSAT facilities: Front-end fabrication &rarr; Wafer probe test &rarr; Wafer sorting (defect binning) &rarr; Package manufacturing &rarr; Package testing &rarr; System-Level Test (SLT) accompanied by continuous root-cause failure analysis.</em>
</p>

Testing is performed in graduated phases to prevent packaging defective silicon:
1. **Wafer Probe Test (Chip Probing / CP):** Performed on full wafers using probe cards. Checks DC parametric baselines (contact opens, leakage currents, supply voltages).
2. **Wafer Sorting (KGD Verification):** Categorizes dies into Known Good Dies (KGD) using wafer bin maps. Only KGDs are released to packaging.

<p align="center">
  <img src="images/Screenshot%202026-10-22%20164425.png" width="850" alt="Package Testing Hierarchy">
  <br>
  <em>Figure 4.2: Package test flow inside ISO Class 6/7 environments: Singulated parts loaded into test sockets on package boards &rarr; Assembly Open and Short Test (AOST) &rarr; Burn-In thermal/voltage stress &rarr; Final Test across cold/hot temperature extremes.</em>
</p>

---

### L2: Assembly Open/Short Test (AOST) & Failure Mechanisms

<p align="center">
  <img src="images/Screenshot%202026-10-22%20164631.png" width="850" alt="AOST Functionality and Failure Modes">
  <br>
  <em>Figure 4.3: Assembly Open and Short Test (AOST) principles and common physical failure modes: Head-on-Pillow (HoP), Solder Bridging, Non-Wet Open (NWO) driven by package/board warpage, and silicon die cracking.</em>
</p>

#### Common Interconnect Defect Modes:
- **Head-on-Pillow (HoP):** A solder paste deposit on the PCB melts and contacts the component sphere, but surface oxides prevent coalescent metallurgical wetting. Under electrical test, it forms an intermittent open.
- **Solder Bridging (Electrical Short):** Excessive solder volume, misalignment, or severe local warpage causes neighboring solder balls to bridge, creating low-impedance short circuits.
- **Non-Wet Open (NWO):** During reflow, differential thermal expansion induces **concave package warpage** and **convex board warpage**, pulling the corner balls away from contact pads before solder solidifies.
- **Die Cracking:** High thermo-mechanical shear stress induced by high-force pick-and-place or sharp temperature gradients during reflow initiates silicon cleaving along crystallographic planes.
- **Product Grade Sorting (PGSRT):** Parts are classified based on AOST test vectors into:
  - **Grade 1 (Best):** Full specification margin for mission-critical/aerospace use.
  - **Grade 2 (Better):** Standard commercial temperature grade.
  - **Grade 3 (Good):** Low-power/consumer grade.
  - **Grade 4 (Scrap):** Irreparable functional failures.

---

### L3: Burn-In Screening, Accelerated Aging & The Bathtub Curve

<p align="center">
  <img src="images/Screenshot%202026-10-22%20164706.png" width="850" alt="Burn In Test and Bathtub Curve">
  <br>
  <em>Figure 4.4: The reliability Bathtub Curve: Accelerating Infant Mortality failures via High-Temperature Operating Life (HTOL) and voltage stressing inside dedicated Burn-In ovens to ensure delivered chips enter their low, constant-failure Useful Life regime.</em>
</p>

The **Bathtub Curve** divides device failure probability over time into three zones:
1. **Infant Mortality Period:** Early failures caused by latent manufacturing defects (gate oxide micro-voids, metallization step-coverage thinning, weak wire-bond heels, contaminated interfaces).
2. **Useful Life Period:** Low, constant, random failure rate ($\lambda$) governed by external electrical/environmental surges.
3. **Wear-Out Period:** Increasing failure rate caused by intrinsic aging mechanisms (electromigration, dielectric breakdown TDDB, hot-carrier injection, solder joint fatigue).

#### Accelerated Life Testing (Arrhenius Model):
Burn-in accelerates thermal defect kinetics using elevated temperatures ($125\text{--}150^\circ\text{C}$) and over-voltage conditions ($1.2\text{--}1.4\times V_{\text{nom}}$). The Acceleration Factor ($AF$) is governed by:
$$AF = \exp\left[ \frac{E_a}{k_B} \left( \frac{1}{T_{\text{use}}} - \frac{1}{T_{\text{stress}}} \right) \right] \times \left( \frac{V_{\text{stress}}}{V_{\text{use}}} \right)^\gamma$$
where $E_a$ is the activation energy of the defect mode ($0.3\text{--}1.1\,\text{eV}$), $k_B$ is the Boltzmann constant ($8.617 \times 10^{-5}\,\text{eV/K}$), and $\gamma$ is the voltage acceleration exponent.

---

### L4: Environmental Qualification & Automated Test Equipment (ATE)

<p align="center">
  <img src="images/Screenshot%202026-10-22%20170754.png" width="850" alt="Summary ATE and Test Categories">
  <br>
  <em>Figure 4.5: Automated Test Equipment (ATE) architecture: High-speed digital testers (Teradyne test stations), collaborative robotic arms (COBOTs), and automated handlers performing parametric, functional, and speed-binning screening.</em>
</p>

#### JEDEC Standard Reliability Tests:
- **Temperature Cycling (TC) — JEDEC JESD22-A104:** Packages undergo $-40^\circ\text{C}$ to $+125^\circ\text{C}$ air-to-air cycling ($1000\text{--}2000\,\text{cycles}$) to evaluate solder fatigue via the **Coffin-Manson relation**:
  $$N_f = C \cdot (\Delta \gamma_{\text{plastic}})^{-m}$$
- **Highly Accelerated Stress Test (HAST) — JEDEC JESD22-A110:** Tests moisture-induced corrosion under severe bias ($130^\circ\text{C}$, $85\%\,\text{RH}$, $33.3\,\text{psia}$).
- **Pressure Cooker Test (PCT / Autoclave) — JEDEC JESD22-A102:** Non-biased moisture test ($121^\circ\text{C}$, $100\%\,\text{RH}$, $15\,\text{psig}$) screening mold compound delamination.
- **High Temperature Storage (HTS) — JEDEC JESD22-A103:** Bakes packages at $150^\circ\text{C}$ for $1000\,\text{hours}$ without electrical bias to evaluate Intermetallic Compound (IMC) embrittlement ($Cu_6Sn_5, Cu_3Sn$).

---

## 6. Module 5: Package Design & Modeling — Building a Package from Scratch in AEDT

<p align="center">
  <img src="images/Screenshot%202026-10-25%20154913.png" width="850" alt="Lab 2 Cross Section Modeling Flow">
  <br>
  <em>Figure 5.1: Lab 2 Workflow: Virtual CAD reconstruction of a semiconductor package cross-section in ANSYS Electronics Desktop matching physical fabrication stages.</em>
</p>

### L1: Virtual Package Cross-Section Modeling Principles
To analyze parasitic RLC extractions and thermal-mechanical stress, engineers construct 3D geometric cross-sections from scratch within AEDT (Q3D Extractor / Icepak Modeler). The virtual model represents:
1. Multi-layer organic/ceramic substrate.
2. Die attach adhesive (DAF/epoxy).
3. Active silicon die.
4. Top bond pads and substrate bond fingers.
5. 3D wire bond arcs or flip-chip solder bumps.
6. Encapsulating mold compound.

---

### L2: 2D Planar Geometry Sketching in 3D Modeler

<p align="center">
  <img src="images/Screenshot%202026-10-25%20185331.png" width="850" alt="AEDT 2D Rectangle Sketch">
  <br>
  <em>Figure 5.2: Sketching base 2D planar geometries on the XY coordinate plane using CreateRectangle within AEDT Modeler.</em>
</p>

- Establish a global Cartesian coordinate system ($X, Y, Z$).
- Draw planar rectangular sheets for the substrate base and silicon die footprints using parametric coordinates (`Sub_X`, `Sub_Y`, `Die_X`, `Die_Y`).

---

### L3: Solid Thickening & Multi-Layer Stackup Construction

<p align="center">
  <img src="images/Screenshot%202026-10-25%20185404.png" width="850" alt="Thicken Sheet Command in AEDT">
  <br>
  <em>Figure 5.3: Converting 2D planar boundary sheets into 3D solid volumes using Modeler &rarr; Surface &rarr; Thicken Sheet.</em>
</p>

<p align="center">
  <img src="images/Screenshot%202026-10-25%20194423.png" width="850" alt="Multi-layer Solid Stackup in Q3D Modeler">
  <br>
  <em>Figure 5.4: 3D multi-layer stackup created by thickening planar sheets: Base copper lead layer and upper silicon die layer.</em>
</p>

<p align="center">
  <img src="images/Screenshot%202026-10-25%20194431.png" width="850" alt="Solid Stackup Isometric View">
  <br>
  <em>Figure 5.5: Isometric perspective of the thickened 3D package geometry showing spatial layer alignment.</em>
</p>

- **Operation:** Select 2D sheet &rarr; `Modeler` &rarr; `Surface` &rarr; `Thicken Sheet`.
- Assign physical thickness:
  - Substrate thickness: $t = 0.5\text{--}1.0\,\text{mm}$.
  - Die attach thickness: $t = 25\,\mu\text{m}$.
  - Silicon die thickness: $t = 150\text{--}300\,\mu\text{m}$.

---

### L4: Material Assignment from AEDT SysLibrary

<p align="center">
  <img src="images/Screenshot%202026-10-25%20195143.png" width="850" alt="Assigning FR4 Epoxy Material">
  <br>
  <em>Figure 5.6: Assigning dielectric material properties from the AEDT SysLibrary: Selecting FR4_epoxy ($\epsilon_r = 4.4$, $\tan\delta = 0.02$).</em>
</p>

- Right-click solid volume &rarr; `Assign Material`.
- Select materials from the verified system database:
  - Substrate: `FR4_epoxy` ($\epsilon_r = 4.4$, $\mu_r = 1$, $\sigma = 0\,\text{S/m}$).
  - Die: `silicon` ($\epsilon_r = 11.9$, $k = 148\,\text{W/m}\cdot\text{K}$).
  - Interconnects: `copper` ($\sigma = 5.8 \times 10^7\,\text{S/m}$, $k = 400\,\text{W/m}\cdot\text{K}$).

---

### L5: Complete Package Assembly & Validation

<p align="center">
  <img src="images/Screenshot%202026-10-25%20195528.png" width="850" alt="Completed Package Cross Section Geometry">
  <br>
  <em>Figure 5.7: Verified multi-layer semiconductor package cross-section model ready for electromagnetic parasitic extraction (Q3D) and thermal analysis (Icepak).</em>
</p>

- **Geometric Intersect Validation:** Execute `Modeler` &rarr; `Validation Check` to confirm zero geometric self-intersections or duplicate boundary overlaps.
- **Simulation Handoff:** The model is parameterized for parametric sweeps (`Optimetrics`), electro-thermal co-simulation, and stress modeling.

---

## 7. Repository Structure

```
Chip_Packaging_Thermal_Analysis_using_Ansys/
│
├── images/                                # High-resolution lecture & simulation screenshots
│   ├── Screenshot 2026-10-19 232739.png   # Package structures & hierarchy
│   ├── Screenshot 2026-10-19 234942.png   # Anatomy of packages (Leadframe to 2.5D)
│   ├── Screenshot 2026-10-19 235453.png   # Nomenclature of advanced packages (John H. Lau)
│   ├── Screenshot 2026-10-19 235733.png   # Package trade-off comparison matrix
│   ├── Screenshot 2026-10-22 002349.png   # Thermosonic wire bonding cycle
│   ├── Screenshot 2026-10-22 002706.png   # HB100 automatic wire bonder
│   ├── Screenshot 2026-10-22 002822.png   # Cleanroom wire bond packaging flow
│   ├── Screenshot 2026-10-22 003059.png   # Wire bond flow with singulation
│   ├── Screenshot 2026-10-22 160614.png   # Cleanroom flip-chip packaging flow
│   ├── Screenshot 2026-10-22 161931.png   # Wafer-level packaging & reconstitution
│   ├── Screenshot 2026-10-22 161958.png   # Solder ball attach machine
│   ├── Screenshot 2026-10-22 162125.png   # Testing stages across foundry and OSAT
│   ├── Screenshot 2026-10-22 164425.png   # Package test flow (AOST, Burn-in, FT)
│   ├── Screenshot 2026-10-22 164631.png   # AOST test modes & physical defect types
│   ├── Screenshot 2026-10-22 164706.png   # Burn-in testing & Bathtub failure curve
│   ├── Screenshot 2026-10-22 170754.png   # Automatic test equipment (ATE) categories
│   ├── Screenshot 2026-10-25 111815.png   # ANSYS Electronics Desktop Icepak setup
│   ├── Screenshot 2026-10-25 112421.png   # AEDT Icepak toolkit package menu
│   ├── Screenshot 2026-10-25 115139.png   # Flipchip BGA die & power input dialog
│   ├── Screenshot 2026-10-25 121445.png   # Solder ball array configuration dialog
│   ├── Screenshot 2026-10-25 121558.png   # 3D Flip-chip BGA model visualization
│   ├── Screenshot 2026-10-25 122733.png   # Source thermal model power setup (1W)
│   ├── Screenshot 2026-10-25 125103.png   # AEDT model tree & solid entities
│   ├── Screenshot 2026-10-25 152435.png   # Finite element design mesh (32,042 elements)
│   ├── Screenshot 2026-10-25 154227.png   # Solved temperature contours (Tj_max = 137.64 °C)
│   ├── Screenshot 2026-10-25 154842.png   # Isometric temperature field contour plot
│   ├── Screenshot 2026-10-25 154913.png   # Package cross-section modeling lifecycle
│   ├── Screenshot 2026-10-25 185331.png   # 2D layer rectangle sketch in AEDT
│   ├── Screenshot 2026-10-25 185404.png   # Thicken Sheet tool command
│   ├── Screenshot 2026-10-25 194423.png   # 3D thickened multi-layer package stackup
│   ├── Screenshot 2026-10-25 194431.png   # Isometric stackup view in AEDT
│   ├── Screenshot 2026-10-25 195143.png   # FR4 epoxy material selection from library
│   └── Screenshot 2026-10-25 195528.png   # Final assembled package cross-section
│
└── README.md                              # Complete course theory, formulas & simulation guide
```

---

## 8. References & Acknowledgements

1. **Course & Material Reference:** VLSI System Design (VSD) Workshop on *Chip Packaging & Thermal Analysis using ANSYS*, instructed by **Tarun Agrawal**.
2. **Textbook & Theoretical Foundations:**
   - John H. Lau, *Semiconductor Advanced Packaging*, Springer.
   - R.R. Tummala, *Fundamentals of Microsystems Packaging*, McGraw-Hill.
   - C.P. Wong et al., *Materials for Advanced Packaging*, Springer.
3. **Simulation Software:** ANSYS Electronics Desktop (AEDT) Student 2024 R2 / 2025 R2 (Icepak, Q3D Extractor, Maxwell).
4. **Standards & Specifications:** JEDEC Solid State Technology Association (JESD22 Reliability Test Methods: A104, A110, A102, A103).
