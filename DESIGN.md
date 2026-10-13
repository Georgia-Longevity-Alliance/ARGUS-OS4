# DESIGN — ARGUS-OS4

**Version:** 1.0
**Date:** 2026-10-13

## Architecture

ARGUS-OS4 = inverted OpenFlexure frame + OET micromanipulation cell + high-NA WI/oil imaging + Jetson edge-AI.

```
┌─────────────────────────────────────────────────────────┐
│  PROJECTOR MODULE (DMD, e.g. Mightex Polygon1000)        │
│  - DMD-based, pattern frames at 1–60 fps (up to 6.6 kHz  │
│    pattern switching in Polygon1000)                     │
│  - Wavelength 530–650 nm (a-Si:H photoconductor peak)    │
│  - Coupled to microscope via an adaptor (epi port)       │
└──────────────────────────┬──────────────────────────────┘
                           │ light pattern
                           ▼
┌─────────────────────────────────────────────────────────┐
│  OET CELL (the core new device)                         │
│  ┌───────────────────────────────────────────────────┐  │
│  │ Top: ITO-coated glass (bias return electrode)      │  │
│  │ Channel: spacer ~100 µm, cell/embryo medium        │  │
│  │ Photoconductor: a-Si:H (~1 µm) on bottom ITO       │  │
│  │ Bottom substrate: ITO on No.1.5 coverslip (170 µm) │  │
│  └───────────────────────────────────────────────────┘  │
└──────────────────────────┬──────────────────────────────┘
                           ▲   AC bias 10–20 Vpp, 10–100 kHz
                           │   (function generator + amp)
                           ▼
┌─────────────────────────────────────────────────────────┐
│  IMAGING: Objective (WI 60×/1.2 or oil 100×/1.35) below │
│  → tube lens → sCMOS → Jetson AGX Orin (AI)             │
└─────────────────────────────────────────────────────────┘
```

## Key Design Decisions

### 1. Inverted geometry (objective below)
- Objective approaches the thin (170 µm) coverslip → short-WD high-NA objectives work.
- OET light pattern comes from above → **no conflict** with the imaging objective below.
- Sample sits on coverslip → live adherent cells/embryos in contact with the substrate.

### 2. Photoconductive substrate on a coverslip
- Standard OET: ITO + hydrogenated amorphous silicon (a-Si:H) as photoconductor.
- **OS4 change:** deposit a-Si:H on a No. 1.5 coverslip (170 µm), not on 1.1 mm glass → enables NA 1.2–1.4.
- Alternative photoconductors (evaluated): TiOPc (spin-coat, cheap, lower performance), c-Si wafer (higher conductivity, but opaque and thick).

### 3. Projector = consumer-grade DMD or Mightex Polygon1000
- Wheeler/Zhang group used a **consumer-grade optical projector** → low cost, widely accessible.
- Mightex Polygon1000: DMD, 350–1000 nm, subcellular resolution, PolyScan software, TTL sync, pattern rates up to 6.6 kHz → high-end option.
- Both options keep OET "massively parallel" (15,000 traps demonstrated).

### 4. AC bias generation
- OET needs AC bias across the cell: typically **10–20 Vpp at 10–100 kHz**.
- Function generator (e.g. Keysight 33500B) + wideband amplifier; or dedicated low-cost DDS (AD9833/AD9834) + op-amp stage.
- Bias applied between top ITO and bottom ITO.

### 5. Microfluidic sample delivery
- Channel formed by spacer (double-sided tape or SU-8) between coverslip and top ITO glass.
- Cells/embryos loaded via tubing + syringe pump (µL/min); OET then steers cells to target.
- Enables closed-system (sterile, no evaporation) manipulation.

### 6. Local edge-AI (no cloud)
- Jetson AGX Orin runs segmentation (Cellpose/StarDist), tracking, lineage building — same as OS1.
- Real-time steering loop: AI detects target → projector pattern moves → OET transports cell.

## Closed-loop control (limited-FOV principle)
From Li/Cheah/Yan/Sun: when the OET/optical pattern or target leaves the FOV, use Cartesian-space (stage) feedback to return it — Lyapunov-stable region feedback. OS4 software implements:
- Visual feedback (image space) inside FOV
- Cartesian-space (stage encoder) feedback outside FOV
- Smooth transition between the two (weighted potential functions)

## AIS/DAIS integration
Same AIS layer as OS1 (passport, body law, flight recorder, trace network). OET adds new "body law" items:
- Max light power on cells (phototoxicity ceiling) — from OS1 phototoxicity data.
- AC bias limits (electroporation threshold for the cell type).
- No pattern on cells during imaging (avoid photobleaching) — temporal multiplexing.

## Module map
| Module | Location |
|---|---|
| OET substrate | `hardware/oet/OET_SUBSTRATE.md` |
| Projector | `hardware/oet/OET_PROJECTOR.md` |
| Signal generator | `hardware/oet/OET_SIGNAL_GENERATOR.md` |
| Microfluidics | `hardware/oet/OET_MICROFLUIDICS.md` |
| BOM | `hardware/oet/OET_BOM.csv` |
| Full technical description (grant) | `docs/INVERTED_ARGUS_DESIGN.md` |
