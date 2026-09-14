# CMOS Circuit Design & VLSI Layout

A transistor-level CMOS digital circuit design project using **TSMC 180 nm CMOS models**, **LTspice**, and the **Electric VLSI Design System**.

The project covers MOSFET characterization, CMOS logic-gate design and simulation, transistor sizing, physical layout, DRC, RC extraction, and post-layout timing analysis.

## Overview

The main workflow is:

**MOSFET characterization → CMOS schematic → LTspice simulation → transistor sizing → Electric VLSI layout → DRC → RC extraction → post-layout timing analysis**

### Circuits / analyses

- NMOS and PMOS `I_D-V_DS` characteristics
- CMOS inverter
- 2-input CMOS NAND
- 2-input CMOS NOR
- 3-input CMOS NAND
- 3-input CMOS NOR
- Schematic & Layout

## Tools Used

| Tool | Purpose |
|---|---|
| **LTspice** | Transistor-level CMOS simulation, DC sweeps and transient analysis |
| **Electric VLSI Design Tool* | CMOS schematic and physical layout design |


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

## 6. Results

| Parameter | Without Capacitor | With Capacitor |
|---|---:|---:|
| Rise time | 20.8773 ns | 21.3761 ns |
| Fall time | 24.9272 ns | 25.5079 ns |
| `t_phl` | 13.5094 ns | 13.8276 ns |
| `t_plh` | 9.62857 ns | 9.84209 ns |
| Propagation delay | 11.5690 ns | 11.8348 ns |
| Maximum frequency | ~86.4 MHz | ~84.5 MHz |

The extracted parasitic capacitance increases the rise/fall times and propagation delay, resulting in a reduction in the maximum operating frequency.

**Harshil Rathan Y**  

