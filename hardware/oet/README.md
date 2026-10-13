# OET Cell Module — ARGUS-OS4

Optoelectronic-tweezers micromanipulation cell for the inverted ARGUS platform.

| File | Content |
|------|---------|
| `OET_SUBSTRATE.md` | Photoconductive substrate: ITO + a-Si:H on No.1.5 (170 µm) coverslip |
| `OET_PROJECTOR.md` | DMD projector parameters (Mightex Polygon1000 / consumer DLP) |
| `OET_SIGNAL_GENERATOR.md` | AC bias 10–20 Vpp @ 10–100 kHz |
| `OET_MICROFLUIDICS.md` | Sample delivery & media exchange |
| `OET_BOM.csv` | Bill of materials (~$3K core, ~$34K with objective) |

## Core principle
Light pattern → a-Si:H photoconductor → virtual electrodes → DEP forces on cells (Chiou 2005 Nature; Zhang 2019 PNAS).

## Key design decision
Substrate on **170 µm coverslip** → objective below can use WI/oil high NA (0.28 mm WD budget); projector illuminates from above.
