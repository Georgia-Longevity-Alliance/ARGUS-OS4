# CONCEPT — ARGUS-OS4

**Version:** 1.0
**Date:** 2026-10-13
**Author:** Jaba Tqemaladze, MD — Georgia Longevity Alliance
**License:** MIT

---

## 0. What is ARGUS-OS4

ARGUS-OS4 is the **inverted-geometry** instantiation of the ARGUS longevity-imaging platform. It keeps every capability already built for OS1 (autonomous fluorescence microscopy + AI lineage tracking), OS2 (centriole pedigree → fate prediction), and OS3 (centriole causality / entropy reset), but reorganizes the optical layout **inverted** (objective below the sample) and adds a **light-driven micromanipulation layer — optoelectronic tweezers (OET)** — that is impossible in the upright OS1 frame.

### The one-line problem it solves
> How do inverted microscopes achieve water-immersion (WI) objectives and diffraction-limited resolution in microfluidic / optoelectronic systems? — **By using a thin (170 µm) bottom coverslip as the substrate**, so the OET channel sits within the working distance of a high-NA objective. OS4 adopts exactly this solution.

---

## 1. Why inverted is the right geometry for OET + high resolution

| Need | Upright (OS1) | Inverted (OS4) |
|---|---|---|
| High NA (WI/oil) | WD ≤ ~0.3 mm, but substrate ≥1.1 mm → NA limited to ~0.75 | **170 µm coverslip → NA 1.35–1.4 achievable** |
| OET light pattern | must be projected onto photoconductor; awkward with objective above | **projector from above, objective from below — optical paths separate** |
| Sample loading (microfluidics) | gravity + air bubbles | **open/inverted chamber, gravity-stable, easy loading** |
| Live-cell / organoid culture | adherent cells on bottom — viewed from above through medium | **adherent cells on coverslip — objective sees them directly** |
| OET manipulation of cells | contact from above competes with objective | **cells sit on the photoconductor; pattern steers them from above** |

**Key structural decision:** the OET photoconductive substrate (ITO + a-Si:H) is fabricated **directly on a No. 1.5 (170 µm) coverslip**. The objective approaches from below (water/oil immersion), the DMD projector illuminates from above. This single change unlocks both high NA and OET in one device.

---

## 2. OET principle (basis)

- **Optoelectronic tweezers (OET):** Chiou, Ohta & Wu 2005 *Nature* 436:370–372. Light pattern → photoconductive a-Si:H layer switches local conductivity → virtual electrodes → dielectrophoretic (DEP) force on cells. **~10⁵× lower light intensity than optical tweezers; up to 15,000 traps on 1.3×1.0 mm².**
- **Optoelectronic micro-robots:** Zhang et al. 2019 *PNAS* 116:14823–14828. SU-8 micro-robots (cogwheel/box/spaceship) driven by OET; "load–transport–deliver"; single-cell isolation, clonal expansion, RNA-seq, enclosed-system manipulation, cell–cell interaction control; built with a consumer-grade projector.
- **Soft optically-actuated micro-robot family:** Iványi, Kelemen et al. 2024 *Adv Mater* (DOI 10.1002/adma.202401115). Two-photon-polymerized grippers (grip / rotate / kiss cells) — complements OET for contact operations.
- **Robotic control with limited FOV:** Li, Cheah, Yan & Sun (A*STAR/CityU) — Lyapunov-based visual feedback keeps trapped cells controlled even when the laser leaves the field of view — control-engineering reference for the OS4 closed-loop.

---

## 3. Capabilities inherited from OS1/OS2/OS3

| # | Capability | Source |
|---|---|---|
| C1 | Autonomous fluorescence microscope (OpenFlexure fork, Jetson edge-AI) | OS1 |
| C2 | Centriole + lineage tracking, 5-generation pedigree | OS1/OS2 |
| C3 | Pedigree-score → cell-fate prediction (statistics, BIC, mixed models) | OS2 |
| C4 | Causality / centriole-transplantation / entropy-reset protocol | OS3 |
| C5 | AI: segmentation (Cellpose/StarDist), division detection, lineage trees | OS1 |
| C6 | AIS/DAIS protocol layer (passport, trace, flight recorder) | OS1 |
| C7 | **NEW (OS4):** OET micromanipulation (trap, transport, deliver, rotate) | OS4 |
| C8 | **NEW (OS4):** high-NA WI/oil imaging on 170 µm coverslip | OS4 |

---

## 4. New capabilities unlocked by OS4

1. **OET trap & transport** — move a single cell/embryo to a target position without contact, no pipette.
2. **OET single-cell isolation + clonal expansion** — "load–transport–deliver" program.
3. **Cell–cell interaction ("kiss") experiments** — pair two cells, hold in contact, image.
4. **Microfluidic sample delivery** — cells/embryos loaded into the OET chamber; OET positions them.
5. **High-resolution (NA 1.35–1.4) imaging** of the same specimen through the thin coverslip.
6. **Combine with OS3 causality:** OET pick-and-deliver of a "known-pedigree" centriole/cell into a host chamber — mechanical-free transfer, fewer artifacts.

---

## 5. The OS4 stack (top → bottom)

```
Projector (DMD, e.g. Mightex Polygon1000) — from above
    │  light pattern (visible, ~530–650 nm)
    ▼
┌─────────────────────────────┐
│ Top ITO electrode (glass)   │  ─ AC bias return
│   ────────────────────────  │
│ OET channel (~100 µm) + cells│
│   ────────────────────────  │
│ Photoconductive layer a-Si:H│  ← virtual electrodes here
│ Bottom ITO electrode        │
│ No.1.5 coverslip (170 µm)   │  ← thin window
└─────────────────────────────┘
    ▲
Objective (WI 60×/1.2 or 100×/1.35) — from below
    │
sCMOS + Jetson AI
```

---

## 6. Hypothesis-driven use in longevity science

- Track centriole inheritance **while manipulating** cells (OS1+OS4): do forced cell–cell contacts change centriole fate?
- OS3 causality with **contact-free** transfer: transplant a "young/old centriole" cell via OET — does recipient fate follow the transplanted centriole?
- High-throughput single-cell aging assays: isolate → clonal-expand → image across generations (OET delivers each founder cell to a dedicated microwell).

---

## 7. Budget & status

| Item | Budget (indicative) |
|---|---|
| Inverted OpenFlexure frame + WI/oil objective (60×/1.2 or 100×/1.35) | $12–20K |
| OET cell (ITO/a-Si:H substrate kit) | $1–3K |
| DMD projector (Mightex Polygon1000 or equivalent) | $15–25K |
| Signal generator (AC 10–20 Vpp, 10–100 kHz) | $0.5–2K |
| Microfluidics (pumps, cassette) | $3–5K |
| sCMOS + Jetson AI (from OS2) | $30K |
| **Total** | **~$60–85K** |

**Status:** 🟡 Concept/design (2026-10-13). Prototype path — see `TODO.md`.

---

## References
- Chiou, Ohta & Wu 2005 *Nature* 436:370–372 (OET).
- Zhang et al. 2019 *PNAS* 116:14823–14828 (optoelectronic micro-robot).
- Zhang et al. 2019 *MicroTAS* (light-driven micro-robot).
- Iványi & Kelemen 2024 *Adv Mater* (soft micro-robot family).
- Li, Cheah, Yan & Sun — optical manipulation with limited FOV (control).
- Mightex — OET application note (Polygon1000 integration).
