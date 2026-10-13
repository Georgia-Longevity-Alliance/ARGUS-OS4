# OET Projection Module (DMD / pattern projector) — ARGUS-OS4

**Part of ARGUS-OS4.** Light source that paints the OET cell with addressable patterns. Pattern → photoconductor → virtual electrodes → cell manipulation.

## Requirements for the OS4 OET cell

| Parameter | Requirement | Why |
|---|---|---|
| Wavelength | 530–650 nm (visible), a-Si:H peak ~600 nm | Matches photoconductor; avoids UV photodamage of cells |
| Pattern type | Arbitrary, dynamically switchable | Trap / transport / deliver / rotate programs |
| Spatial resolution | ≤ 1 µm (per mirror → cell size 5–30 µm) | Cell-level precision; trap several cells in parallel |
| Frame rate | ≥ 1–10 Hz (up to 6.6 kHz mirror switching) | Real-time steering of moving cells |
| Coupling | Must integrate with inverted microscope (infinity path) | Both projector and objective on same optical axis |
| Output power | ~0.1–10 mW/cm² on cell plane | ~10⁵× lower than optical tweezers; gentle on cells |

## Options

### 1. Mightex Polygon1000 (DMD-based pattern illuminator) — recommended
- Digital Micromirror Device (DMD): 1024×768 micromirrors, per-mirror ON/OFF, subcellular resolution.
- Wavelength range: 350–1000 nm (LED/laser fiber-coupled input); 400–700 nm VIS version for OET.
- Integrates into infinity path of any microscope (both upright and inverted via dedicated adapters).
- Software: PolyScan — calibration maps camera pixels to DMD mirrors; TTL triggering; pattern sequences stored on-board (up to 2000 patterns, switching up to 6.6 kHz).
- Application: exactly OET patterned illumination for cell and micro-robot manipulation (Mightex application note).

### 2. Consumer-grade DLP projector (Wheeler/Zhang approach)
- A consumer optical projector (e.g. Optoma/Epson 1080p) projected through a reduction lens onto the OET cell.
- Pros: very low cost (~$100–300), parallel manipulation (Zhang PNAS 2019 uses exactly this).
- Cons: bulkier, must add coupling optics, less precise per-mirror calibration; green/red channels best for a-Si:H.

### 3. OpenFlexure Optical Tweezers extension (laser-based)
- Reference open-hardware: `aliazadbakht/OpenFlexure_OpticalTweezers` (CERN-OHL-S-2.0) — 635 nm, ~1 mW laser diode, NA≥0.8 objective, dichroic cube, RMS-threaded optics module, 3D-printed STL + OpenSCAD. Useful as an **optical-tweezers** companion to OET (different force regime: OET is dielectrophoretic, this is photonic momentum). OET is the OS4 core; this is an optional extra module for single-beam trapping.

## Recommended OS4 configuration

- **Primary (OET):** Mightex Polygon1000 (DMD) → infinity-path adapter → illuminates OET cell from above.
- **Secondary (optional, soft-robot micro-grippers):** two-photon-polymerized micro-robots (Iványi & Kelemen 2024) actuated by the same or a dedicated laser path.

## Integration into the inverted microscope (top module)

```
Polygon1000 DMD ──infinity-path adapter──▶  tube lens
        │                                   │
        │ (pattern light)                    │
        ▼                                   ▼
   beam-splitter  ◄──►  Objective (from below)
        │
        └──▶  to OET cell (from above)
```

Practical mounting: the DMD projector occupies the epi/tube port above the sample; the objective + sCMOS is below. The two paths are separated by the thin coverslip geometry — no conflict.

## Driving software
- **PolyScan** (Mightex) — pattern generation, calibration, TTL sync with camera.
- **Custom Python driver** (OS4 `software/oet/projector.py`) — loads trap patterns, positions, sequences; exposes REST/JSON to the ARGUS orchestrator (AIS layer).

## Light safety
- Keep cell-plane intensity ≤ phototoxicity ceiling (see OS1 phototoxicity pilot P2).
- Laser modules (635 nm) — eye-safe enclosure, interlock, alignment caps (from OpenFlexure OT BOM).
