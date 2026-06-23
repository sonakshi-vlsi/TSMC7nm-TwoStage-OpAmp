# Two-Stage Miller-Compensated OTA — Cadence Virtuoso (Spectre)

> Fully characterized two-stage OTA designed and simulated in Cadence Virtuoso using Spectre. All analyses were run at the schematic level.
> Desgined to function as an error amplifier for LDO.
---

## Overview

This project implements a classic two-stage Miller-compensated OTA topology and performs a comprehensive characterization suite covering gain, stability, bandwidth, noise, CMRR, PSRR, slew rate, and power consumption. The design targets general-purpose amplifier applications where phase margin, UGB, and low-frequency gain are the primary constraints.

The OTA uses a differential input pair (M1/M2) driving a current mirror active load, followed by a common-source second stage with Miller capacitor compensation to split the dominant and non-dominant poles and achieve adequate phase margin.

---

## Simulation Results Summary

| Parameter | Value | Analysis Type |
|---|---|---|
| Open-Loop Gain (AOL) | 47.38 dB | AC |
| Phase Margin | 54.41° – 60.78° | AC / STB |
| Gain Margin | 6.20 dB | STB |
| Unity-Gain Bandwidth (UGB) | 494.2 MHz | AC |
| −3 dB Bandwidth | 1.707 MHz | AC |
| Slew Rate | ~1 V/μs (998.4 kV/s) | Transient |
| DC CMRR | ~51 dB | AC (differential) |
| PSRR (at 216.5 kHz) | −52.57 dB | XF |
| Input-Referred Noise (1 kHz) | 8.19×10⁻¹² V²/Hz | Noise |
| Quiescent Power | 67.74 μW | DC |


## Tools & Environment

| Tool | Version/Details |
|---|---|
| EDA Tool | Cadence Virtuoso (Analog Design Environment) |
| Simulator | Spectre |
| Analysis Environment | Maestro (ADE XL) |
| Waveform Viewer | Virtuoso Visualization & Analysis XL (VIVA) |

---

## Key Design Decisions

- **Miller compensation** was chosen for its pole-splitting effect: it pushes the dominant pole to low frequency while moving the non-dominant pole to well beyond UGB, ensuring adequate PM without excessive power overhead.
- **Flicker noise** is the bottleneck at low frequencies. To reduce it, PMOS input pair devices can be used (PMOS has lower KF), or larger gate area devices can be selected.
- **Phase margin of ~54–60°** (two methods give slightly different values due to loop-gain vs. open-loop phase measurement conventions) provides adequate stability with reasonable transient overshoot.
- **PSRR and CMRR** are both limited at high frequency — typical for a two-stage topology without explicit PSRR enhancement circuitry.

---

## Potential Improvements

- Add a right-half-plane (RHP) zero cancellation resistor in series with Cc to push the zero to infinity or the LHP
- Use PMOS input pair to reduce flicker noise by ~10×
- Increase Miller cap or tail current to push UGB / improve GM if needed
- Add output buffer stage for driving low-impedance loads

---

## Author

**Sonakshi**  
B.Tech ECE (VLSI Design & Technology), VIT Chennai  
Analog IC Design Intern

---

*Simulations performed in Cadence Virtuoso / Spectre. Results shown are from schematic-level simulation.*
