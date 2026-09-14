# CMOS Digital Circuit Design & VLSI Layout

A transistor-level CMOS digital circuit design project using **TSMC 180 nm CMOS models**, **LTspice**, and the **Electric VLSI Design System**.

The project covers MOSFET characterization, CMOS logic-gate design and simulation, transistor sizing, physical layout, DRC, RC extraction, and post-layout timing analysis.

## Overview

This project was developed as part of VLSI design coursework to study CMOS circuits from the transistor level through physical layout.

The main workflow is:

**MOSFET characterization → CMOS schematic → LTspice simulation → transistor sizing → Electric VLSI layout → DRC → RC extraction → post-layout timing analysis**

### Circuits / analyses

- NMOS and PMOS `I_D-V_DS` characteristics
- CMOS inverter
- 2-input CMOS NAND
- 2-input CMOS NOR
- 3-input CMOS NAND
- 3-input CMOS NOR
- CMOS half-adder
- CMOS inverter physical layout
- Capacitive-load analysis
- RC/parasitic extraction and timing analysis

## Technology

- **Technology:** TSMC 180 nm CMOS
- **Minimum channel length used:** 0.18 µm
- **Supply voltage:** 3 V for the main inverter characterization
- **SPICE model:** `tsmc018.lib`

The repository contains the TSMC 180 nm model/library files used by the LTspice simulations.

## Tools Used

| Tool | Purpose |
|---|---|
| **LTspice** | Transistor-level CMOS simulation, DC sweeps and transient analysis |
| **Electric VLSI Design System** | CMOS schematic and physical layout design |
| **TSMC 180 nm SPICE model** | NMOS/PMOS device modeling |
| **SPICE netlists / `.asc` files** | Simulation setups and circuit definitions |

## Project Structure

```text
CMOS/
├── Figs/                    # Figures and project visuals
├── Id vs Vds/               # MOSFET I_D-V_DS analysis material
├── Inverter/                # CMOS inverter design/layout material
├── TSMC_180mn/              # TSMC 180 nm related project files
├── nand-gate/               # NAND gate design material
├── nor-gate/                # NOR gate design material
│
├── CMOS.jelib               # Electric VLSI project/library file
├── TSMC_180mn.zip           # Archived TSMC 180 nm project files
├── tsmc018.lib              # TSMC 180 nm SPICE model
│
├── CMOS_inverter.asc        # CMOS inverter LTspice schematic
├── NAND.asc                 # CMOS NAND LTspice schematic
├── NOR.asc                  # CMOS NOR LTspice schematic
├── 3ip_NAND.asc             # 3-input NAND LTspice schematic
├── q3.asc                   # Additional circuit/simulation setup
├── Draft1.asc               # Intermediate LTspice design
├── Draft2.asc               # Intermediate LTspice design
│
├── cmos_sizing.pdf          # CMOS transistor-sizing calculations
├── Report.pdf               # Detailed project report
└── README.md
```

## 1. MOSFET Characterization

The project begins with NMOS and PMOS characterization using the TSMC 180 nm device models.

The simulations examine the drain-current characteristics for different gate-to-source voltages and demonstrate the transition between the linear and saturation regions.

## 2. CMOS Inverter

A CMOS inverter was designed and analyzed using LTspice.

The inverter was evaluated using:

- Transient/PULSE simulation
- DC sweep
- Rise time
- Fall time
- Low-to-high propagation delay
- High-to-low propagation delay
- Average propagation delay
- Capacitive loading

For the main 3 V inverter simulation, the transistor dimensions were:

```text
NMOS: W = 1 µm,   L = 0.18 µm
PMOS: W = 1.9 µm, L = 0.18 µm
VDD:  3 V
```

The sizing was selected to obtain approximately symmetric rise and fall times.

### Capacitive loading

A **10 pF load capacitor** was also introduced to study the effect of capacitive loading on switching speed.

The simulation shows the expected increase in rise/fall time and propagation delay when the output capacitance is increased.

## 3. CMOS NAND and NOR Gates

CMOS NAND and NOR gates were implemented at the transistor level.

### 2-input NAND

The NAND uses:

- PMOS devices in parallel in the pull-up network
- NMOS devices in series in the pull-down network

The LTspice implementation includes transient stimulus and timing measurements.

### 2-input NOR

The NOR uses:

- PMOS devices in series in the pull-up network
- NMOS devices in parallel in the pull-down network

The transistor sizing was adjusted to account for the higher effective resistance of the series PMOS pull-up network.

### 3-input NAND and NOR

3-input versions were also analyzed to study the effect of additional series/parallel devices on switching behavior and timing.

## 4. CMOS Half-Adder

A CMOS half-adder was designed at the transistor level using CMOS logic structures.

The design extends the individual CMOS logic-gate concepts toward a larger combinational digital circuit.

## 5. Physical VLSI Layout

The CMOS circuits were implemented in the **Electric VLSI Design System**.

The CMOS inverter was taken through the physical-layout flow:

```text
Schematic
   ↓
Layout
   ↓
Design Rule Check (DRC)
   ↓
RC Extraction
   ↓
Post-layout simulation
   ↓
Timing analysis
```

The Electric VLSI project/library is provided as:

```text
CMOS.jelib
```

## 6. DRC and RC Extraction

The CMOS inverter layout was checked using Electric VLSI's design-rule checking flow.

After layout verification, RC extraction was used to capture parasitic effects introduced by the physical implementation.

The extracted circuit was then analyzed to compare switching performance against the ideal/pre-layout behavior.

## 7. Results

For the CMOS inverter physical-layout analysis, the report gives the following results:

| Parameter | Without Capacitor | With Capacitor |
|---|---:|---:|
| Rise time | 20.8773 ns | 21.3761 ns |
| Fall time | 24.9272 ns | 25.5079 ns |
| `t_phl` | 13.5094 ns | 13.8276 ns |
| `t_plh` | 9.62857 ns | 9.84209 ns |
| Propagation delay | 11.5690 ns | 11.8348 ns |
| Maximum frequency | ~86.4 MHz | ~84.5 MHz |

The extracted parasitic capacitance increases the rise/fall times and propagation delay, resulting in a reduction in the maximum operating frequency.

## Key Concepts Demonstrated

- CMOS inverter operation
- NMOS/PMOS device characteristics
- Pull-up and pull-down networks
- CMOS NAND/NOR topology
- Transistor sizing
- Rise/fall time
- Propagation delay
- Capacitive loading
- SPICE simulation
- CMOS physical layout
- Design Rule Checking (DRC)
- RC/parasitic extraction
- Post-layout timing analysis
- 180 nm CMOS technology

## Files of Interest

### LTspice

- `CMOS_inverter.asc` — CMOS inverter simulation
- `NAND.asc` — NAND gate simulation
- `NOR.asc` — NOR gate simulation
- `3ip_NAND.asc` — 3-input NAND simulation
- `tsmc018.lib` — TSMC 180 nm transistor model

### Electric VLSI

- `CMOS.jelib` — Electric VLSI project/library containing the CMOS designs and layout work

### Documentation

- `Report.pdf` — complete project report
- `cmos_sizing.pdf` — transistor-sizing calculations

## How to Explore the Project

### LTspice

1. Install LTspice.
2. Keep `tsmc018.lib` available in the same project directory.
3. Open the relevant `.asc` schematic.
4. Run the DC or transient simulation.
5. Inspect the output waveform and timing measurements.

The LTspice schematics contain `.include tsmc018.lib` statements so that the TSMC 180 nm device models are used during simulation.

### Electric VLSI

Open `CMOS.jelib` using the Electric VLSI Design System to inspect the available schematic/layout cells.

The physical-layout portion of the project is centered around the CMOS inverter, including DRC and RC-extraction analysis.

## Repository Notes

Some `.asc` files such as `Draft1.asc` and `Draft2.asc` are intermediate simulation/design files retained from the development process.

The detailed methodology, circuit diagrams, simulations, layout screenshots, DRC results, RC extraction and timing results are documented in `Report.pdf`.

## Author

**Harshil Rathan Y**  
B.Tech Electrical Engineering  
Indian Institute of Technology Hyderabad

GitHub: [Harshil095](https://github.com/Harshil095)
