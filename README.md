# ARGUS-OS4 — Inverted Geometry + OET Micromanipulation

**Inverted ARGUS:** every capability of OS1/OS2/OS3 in an **inverted-microscope geometry** (objective below the sample), extended with an **optoelectronic-tweezers (OET)** light-patterned micro-manipulation cell and water-immersion high-resolution imaging through a thin 170 µm bottom coverslip.

| Feature | OS1/OS2/OS3 (upright) | **OS4 (inverted + OET)** |
|---|---|---|
| Geometry | Objective above sample | **Objective below sample** (inverted) |
| Immersion / resolution | 60×/1.2 WI (long WD, thick substrate) | **60×/1.2 WI or 100×/1.35** on 170 µm coverslip — diffraction-limited |
| Micromanipulation | FOSH mechanical arms (contact) | **+ OET: contact-free, light-patterned, parallel** |
| Loading | manual / microfluidic | **microfluidic sample delivery + OET trap/transport** |
| Pedigree / centriole tracking | ARGUS AI pipeline (Jetson) | retained, **+ real-time OET steering** |
| Causality (OS3) | mechanical transplantation | **OET-based contact-free cell pick-up & delivery** |

## Key modules
- `hardware/oet/` — OET cell design: photoconductive substrate (ITO/a-Si:H), projection module, signal generator, microfluidics, BOM
- `docs/INVERTED_ARGUS_DESIGN.md` — full inverted-platform technical description (grant-ready)
- Core biology, statistics, AI pipeline — inherited from OS1/OS2/OS3.

## Why inverted + OET
1. **High NA / high resolution:** WI and oil-immersion objectives need the specimen within a short working distance; a thin 170 µm (No. 1.5) bottom coverslip places the OET channel right at the objective — enabling NA up to 1.35–1.4, impossible through a 1.1 mm substrate.
2. **Contact-free manipulation:** OET (Chiou/Ohta/Wu 2005 *Nature* 436:370) patterns DEP forces with light — up to 15,000 parallel traps, ~10⁵× lower light intensity than optical tweezers.
3. **Gentle on cells:** optoelectronic micro-robots (Zhang et al. 2019 *PNAS* 116:14823) "scoop", transport, and deliver mammalian cells/clonal expansion without the photodamage of direct optical trapping.
4. **Soft micro-robot family** (Iványi & Kelemen 2024 *Adv Mater*, DOI 10.1002/adma.202401115): two-photon-polymerized grippers for rotate/kiss/press single cells.

## Quick start
```
See docs/INVERTED_ARGUS_DESIGN.md  (architecture & integration)
See hardware/oet/OET_SUBSTRATE.md  (ITO/a-Si:H substrate)
See hardware/oet/OET_PROJECTOR.md  (DMD projector parameters)
See hardware/oet/OET_SIGNAL_GENERATOR.md
See hardware/oet/OET_MICROFLUIDICS.md
```
