# ARGUS-OS4 Inverted Platform — Technical Description (grant-ready)

**Version:** 1.0 · **Date:** 2026-10-13 · **Author:** Jaba Tqemaladze, MD — Georgia Longevity Alliance

> This document is the technical description of the ARGUS-OS4 inverted platform with an optoelectronic-tweezers (OET) micromanipulation cell. It is written to be dropped into a grant application (Background, Technical Approach, or Methods).

---

## 1. Summary

ARGUS-OS4 is an **open-source, inverted-geometry autonomous microscope** that combines:
1. **Inverted optical layout** (objective below the sample) — enabling water-immersion/oil-immersion objectives with numerical aperture up to 1.35–1.4 on a thin (170 µm) No. 1.5 coverslip;
2. **Optoelectronic tweezers (OET)** — a light-patterned, contact-free dielectrophoretic micromanipulation layer for trapping, transporting, rotating and delivering single cells, embryos, and micro-particles;
3. **Full ARGUS AI pipeline** (edge inference on NVIDIA Jetson AGX Orin: segmentation, tracking, lineage construction) inherited from ARGUS-OS1/OS2/OS3;
4. **Microfluidic sample delivery** for loading, media exchange, and closed-system manipulation.

The platform is 100% open hardware/software (Apache 2.0 / MIT / CERN-OHL), built as a fork/extension of the OpenFlexure microscope, and targets longevity-relevant single-cell biology: centriole/age inheritance, clonal expansion, and cell–cell interaction experiments.

---

## 2. Scientific & technical background

### 2.1 Why inverted geometry with a thin coverslip
High-resolution optical trapping, imaging, and optoelectronic manipulation all benefit from high numerical aperture (NA). Immersion objectives (water: NA up to ~1.2; oil: NA up to ~1.4) require the specimen to lie within a short working distance (WD) of the objective (e.g., 60×/1.2 WI WD ≈ 0.28 mm; 100×/1.35 oil WD ≈ 0.13 mm). Standard glass slides are 1.1 mm thick — too thick for these objectives.

**The key design decision:** the OET photoconductive substrate is fabricated directly on a **No. 1.5 coverslip (170 µm)**, placing the microfluidic/OET channel within the objective's working distance. This single change unlocks diffraction-limited high-NA imaging **and** OET in the same device — the same solution used by inverted microscopes in optoelectronic and microfluidic systems.

### 2.2 Optoelectronic tweezers (OET) — mechanism
OET (Chiou, Ohta & Wu, *Nature* 436:370, 2005) uses projected light patterns to switch the local conductivity of a photoconductive layer (hydrogenated amorphous silicon, a-Si:H), creating "virtual electrodes" that produce non-uniform electric fields → **dielectrophoretic (DEP)** forces on objects in the adjacent channel. Key advantages:

| Advantage | Value |
|---|---|
| Light intensity vs optical tweezers | ~10⁵× lower (gentle on cells) |
| Parallel manipulation | up to 15,000 traps on 1.3×1.0 mm² |
| Force | DEP force scales with ∇E²; sufficient to move cells |
| Programmable | dynamic light patterns (DMD) — arbitrary trap geometry |
| Cost | consumer-grade DLP projector sufficient |

**Optoelectronic micro-robots** (Zhang et al., *PNAS* 116:14823, 2019) extend OET to "load–transport–deliver" programs: SU-8 micro-robots (cogwheel/box/spaceship) carry cells for single-cell isolation, clonal expansion, and RNA-seq — demonstrated to be gentler on fragile mammalian cells than direct OET.

**Soft optically-actuated micro-robots** (Iványi & Kelemen et al., *Adv Mater* 2024, DOI 10.1002/adma.202401115) add two-photon-polymerized grippers for grip / rotate / "kiss" (cell–cell contact) operations, complementing OET for contact-level tasks.

### 2.3 Robotic control with limited field of view
OET/optical manipulation must remain robust when the trap or target leaves the microscope's field of view (FOV). We adopt the control framework of Li, Cheah, Yan & Sun (A*STAR / CityU): a vision-based controller inside the FOV plus a Cartesian-space (stage encoder) controller outside it, with smooth transitions guaranteed by Lyapunov-based region feedback. This gives stable closed-loop manipulation over the full sample area.

---

## 3. System architecture

```
┌──────────────────────────────────────────────────────────────┐
│ PROJECTION MODULE (from above)                               │
│   DMD projector (Mightex Polygon1000 or consumer DLP)         │
│   530–650 nm, dynamic patterns, 1–60 fps (up to 6.6 kHz)      │
└──────────────────────────┬───────────────────────────────────┘
                           │ light pattern
                           ▼
┌──────────────────────────────────────────────────────────────┐
│ OET CELL                                                    │
│  Top ITO glass (bias return)                                │
│  Channel ~100 µm (cells/embryos in low-conductivity buffer) │
│  a-Si:H photoconductor (~1 µm) on ITO                       │
│  No.1.5 coverslip 170 µm (thin optical window)              │
└──────────────────────────┬──────────────────────────────────┘
                           ▲ AC bias 10–20 Vpp @ 10–100 kHz
                           │
┌──────────────────────────┴──────────────────────────────────┐
│ IMAGING (from below)                                        │
│  Objective WI 60×/1.2 or oil 100×/1.35                     │
│  sCMOS camera + Jetson AGX Orin (edge AI)                  │
└─────────────────────────────────────────────────────────────┘
```

### 3.1 Modules
| Module | Description |
|---|---|
| OET substrate | ITO + a-Si:H on 170 µm coverslip (see `hardware/oet/OET_SUBSTRATE.md`) |
| Projector | DMD pattern projection from above (see `OET_PROJECTOR.md`) |
| Signal generator | AC bias 10–20 Vpp, 10–100 kHz (see `OET_SIGNAL_GENERATOR.md`) |
| Microfluidics | syringe-pump sample delivery & media exchange (see `OET_MICROFLUIDICS.md`) |
| Imaging/AI | WI/oil objective + sCMOS + Jetson edge-AI (from OS1/OS2) |
| Control | closed-loop OET steering + limited-FOV controller (Li/Cheah) |
| AIS layer | passport, body law (phototoxicity/AC limits), flight recorder (from OS1) |

### 3.2 Key specifications
| Parameter | Value |
|---|---|
| Objective | 60×/1.2 WI or 100×/1.35 oil (through 170 µm coverslip) |
| Photoconductor | a-Si:H ~1 µm (PECVD); alt. TiOPc spin-coat |
| OET bias | 10–20 Vpp, 10–100 kHz (square or sine) |
| Projector | 530–650 nm, DMD; consumer DLP acceptable |
| Manipulation | trap / transport / rotate / deliver / "kiss" (cell–cell) |
| Parallel traps | up to 15,000 (Chiou 2005) |
| Sample | Developing embryos (from zygote), mammalian cells, organoids |
| AI | Jetson AGX Orin 64GB (segmentation, tracking, lineage) |
| Openness | Apache 2.0 / MIT / CERN-OHL; GitHub `Georgia-Longevity-Alliance/ARGUS-OS4` |

---

## 4. Applications in longevity research

1. **Centriole-age inheritance with manipulation** (OS1+OS4): force-controlled cell–cell contacts / spatial re-arrangement while tracking centriole inheritance across 5 generations.
2. **Causality without contact artifacts** (OS3+OS4): OET pick-and-deliver of a "known-pedigree" centriole/cell into a host chamber — mechanical-free transfer.
3. **High-throughput single-cell aging assays:** isolate → clonal-expand → image across generations; OET delivers founder cells to dedicated microwells.
4. **Cell–cell interaction ("kiss") experiments:** hold two cells in contact, image outcome — relevant to fate-determination and intercellular signaling.

---

## 5. Openness & reproducibility
- Full hardware design, CAD, BOM, and control software in the public repository.
- Substrate fabrication procedure (a-Si:H on coverslip) is standard clean-room/PECVD and can be outsourced to a foundry; low-cost TiOPc alternative enables assembly in any lab.
- Projector can be a consumer-grade DLP (~$300) → dramatically lowers the barrier (as demonstrated by the Wheeler/Zhang group).

---

## 6. Safety & ethics
- Cell phototoxicity ceiling: light intensity kept at the lower bound (OET uses ~10⁵× less light than optical tweezers); imaging interval constrained per OS1 pilot P2.
- AC bias limited to non-electroporating range for the target cell type.
- Human cell lines: ethics/data-availability statements per OS1 standard.
- Laser/oil safety: interlocked enclosure (inherited OS1 Body Law).

---

## 7. References (verified)
1. Chiou PY, Ohta AT, Wu MC. *Nature* 2005;436:370–372. DOI 10.1038/nature03831 (OET).
2. Zhang S, et al. *PNAS* 2019;116(30):14823–14828. PMID 31289234 (optoelectronic micro-robot).
3. Zhang S, et al. MicroTAS 2019;160–161 (light-driven micro-robot).
4. Iványi GT, Kelemen L, et al. *Adv Mater* 2024. DOI 10.1002/adma.202401115. PMID 38814436 (soft micro-robot family).
5. Islam MA, Park S-Y. *Micromachines* 2024;15(1):119. PMID 38258238 (ODEP/FEOET optimization).
6. Li X, Cheah CC, Yan X, Sun D. Robotic cell manipulation with optical tweezers and limited FOV (A*STAR/CityU). DOI (see repo).
7. Mightex Bio. Optoelectronic tweezers application note (Polygon1000 integration).
8. OpenFlexure Microscope (Collins et al. 2020, *Biomed Opt Express* 11:2447) — base frame.
