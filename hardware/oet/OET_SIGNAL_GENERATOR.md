# OET Signal Generator — ARGUS-OS4

**Part of ARGUS-OS4.** Provides the AC bias across the OET cell: top ITO electrode ↔ bottom ITO electrode (through the photoconductor and channel).

## Electrical drive parameters

| Parameter | Value | Reference |
|---|---|---|
| Waveform | Sinusoidal (or square for sharper field) | Chiou 2005; Zhang PNAS 2019 |
| Voltage (peak–peak) | 10–20 Vpp (up to 25 Vpp in micro-robot demos) | Chiou 2005 (typical); Zhang 2019 (25 Vpp @ 20 kHz) |
| Frequency | 10–100 kHz | Chiou 2005; Zhang 2019 (20 kHz) |
| Output | Single AC channel + common ground; floating, isolated | — |
| Load | Capacitive (cell ~ tens of pF–nF across channel) | — |

## Implementation options

### 1. Function generator + amplifier (recommended, low cost)
- Signal source: low-cost DDS function generator (e.g. Siglent SDG1032X, JDS6600, or DIY AD9833/AD9834 board).
- Amplifier: wideband op-amp stage (e.g. OPA541 / LM7171) or a 1:10 step-up transformer; output 10–25 Vpp, 10–100 kHz.
- Isolation: small 1:1 isolation transformer or floating supply to avoid ground loops through the microscope.

### 2. Dedicated OET driver board (integrated, reproducible)
- DDS (AD9834) → 2–4 stage op-amp → output 0–25 Vpp, 1–200 kHz.
- Digital control (SPI/UART) via Raspberry Pi Pico / Jetson GPIO; frequency & amplitude programmable.
- Expose as a device in `software/oet/signal_gen.py` (AIS-compatible).

## Wiring to the OET cell
- Connect output to top ITO and bottom ITO contact pads (silver epoxy / conductive tape).
- Keep leads short, shielded; ground the microscope frame.
- Verify waveform at cell with an oscilloscope before running live cells.

## Safety
- Max 25 Vpp at ≤200 kHz — low energy, but **isolate** from operator and from Jetson/camera grounds.
- Interlock: disable output when microscope lid open (AIS Body Law).
