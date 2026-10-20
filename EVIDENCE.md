# EVIDENCE — ARGUS-OS4

**Updated:** 2026-10-13 · **Status:** OET/inverted platform evidence inventory. All PMID verified via PubMed E-utilities 2026-10-13.

## OET (optoelectronic tweezers) — core evidence

| Ref | Finding | Role in OS4 |
|:----:|---------|-------------|
| Chiou, Ohta & Wu 2005 *Nature* 436:370–372 (DOI 10.1038/nature03831) | OET principle: light pattern → a-Si:H photoconductor → virtual electrodes → DEP. ~10⁵× lower light than optical tweezers; 15,000 traps on 1.3×1.0 mm² | **Core mechanism** of the OS4 manipulation layer |
| Zhang S, et al. 2019 *PNAS* 116(30):14823–14828 (PMID **31289234**) | Optoelectronic micro-robot: SU-8 cogwheel/box/spaceship robots, "load–transport–deliver"; single-cell isolation, clonal expansion, RNA-seq, enclosed systems, cell–cell interaction; consumer-grade projector | Micro-robot layer; single-cell protocols |
| Zhang S, et al. MicroTAS 2019 (Scopus 85094947366) | First light-driven micro-robot on OET; multi-axis programmed ops | Historical/parallel evidence |
| Iványi GT, Kelemen L, et al. 2024 *Adv Mater* (DOI 10.1002/adma.202401115, PMID **38814436**) | Two-photon-polymerized soft micro-robot family: grip / rotate / "kiss" single cells with optical tweezers; non-destructive | Complementary contact-level manipulation ("kiss" experiments) |
| Islam MA, Park S-Y. 2024 *Micromachines* 15(1):119 (PMID **38258238**) | FEOET/ODEP: position & size optimization (x_opt=Lc+r, r_opt=5Lc); photoconductor (TiOPc+plasmonic) characterization; low-light (4.08 µW/mm²) droplet manipulation | Substrate/force optimization; alternative photoconductor (TiOPc) |

## High-resolution imaging through thin coverslip (inverted geometry)

| Ref | Finding | Role in OS4 |
|:----:|---------|-------------|
| Mightex Bio application note (Polygon1000) | DMD-based pattern illuminator; 350–1000 nm; integrates into infinity path of upright **and inverted** microscopes; used for OET cell & micro-robot manipulation | Projector integration (both geometries); OET with APRE-19/MCF-7 cells and 200 µm micro-robot |
| Li X, Cheah CC, Yan X, Sun D. (A*STAR / CityU) | Robotic cell manipulation with optical tweezers & **limited FOV**: vision-based control (in FOV) + Cartesian-space feedback (out of FOV); Lyapunov-stable | Closed-loop control robustness for OS4 steering |
| Zhang et al. 2019 *PNAS* (same as above) | 200+ µm micro-robots manipulated by OET — larger than OT-capable objects | Size range: OS4 handles embryos/cells |
| Kaneshiro et al. 2022 (DOI **10.1017/qpb.2022.24**) | Fully automated IR-laser cell disruption on an **inverted** microscope (Nikon Ti2-E), laser delivered **through a 20×/0.75 objective** (epi-illumination path); detect→classify→mask→irradiate→verify loop | ⭐ Independent validation of OS4's **inverted geometry + through-objective laser port**; confirms an automated laser-ablation port is a natural OS4 add-on (OET positions cells → laser ablates/disrupts) |

## Core centriole biology (inherited from OS1/OS2/OS3)

| PMID | Finding | Role in OS4 |
|:----:|---------|-------------|
| 6684600 | Sulston et al. 1983 — invariant lineage | Sister-pair design |
| 37256957 | Kalbfuss & Gönczy 2023 — 88% centriole elimination | H₀ baseline |
| 37414202 | Kalbfuss, Berger & Gönczy 2023 — cell fate determines centriole fate | Null model |
| 39764850 | Barandun et al. 2025 — mother centrosome inheritance → CD8+ T-cell fate (mammals) | OS2 principle |
| 36988082 | Rostami et al. 2023 — sperm centrioles segregate stochastically | Natural variation |
| 37987153 | Pierron et al. 2023 — SAS-1 loss first; UPS localizes to centrioles | Early elimination marker |

## Weak points / limitations (meta-analysis)

1. **OET channel vs high NA:** OET needs a channel (~100 µm) with medium; high-NA objectives need the specimen within ~0.3 mm. The 170 µm coverslip solves this, but channel height + coverslip + immersion still consume WD — 100×/1.35 oil (WD 0.13 mm) may not reach cells inside a 100 µm channel on a 170 µm coverslip; **60×/1.2 WI (WD 0.28 mm) is the safe choice**; verify by WD budget (0.17 coverslip + ~0.1 channel ≈ 0.27 mm ≈ WD).
2. **a-Si:H requires PECVD clean-room** — not accessible everywhere; alternative TiOPc (spin-coat) has ~10³ lower σ_photo/σ_dark ratio → weaker force (Islam & Park 2024). Mitigation: foundry a-Si:H deposition (one-time cost) or plasmonic-enhanced TiOPc.
3. **Light-induced heating / phototoxicity:** even at 10⁵× lower light than OT, cells in OET channels see light + electric field; AC electroporation threshold must be measured per cell type (OS1 pilot P2 style).
4. **DEP force scale:** OET forces are pN–nN range; sufficient for cells/embryos but not for strong anchoring; combine with micro-robots (SU-8) for mechanical holding.
5. **Projector cost:** Polygon1000 ~$18K; consumer DLP ~$300 but lower pattern speed/resolution — acceptable for most biological OET (Wheeler group used consumer projector).
6. **Wet/open chamber:** microfluidics + OET need sealed channel to prevent evaporation during long (hours) imaging; gravity/open-chamber FEOET style is simpler but less stable.

## Verified vs predicted

| Claim | Status |
|-------|:---:|
| OET traps single cells with ~10⁵× lower light than OT | ✅ Confirmed (Chiou 2005, Zhang 2019) |
| Optoelectronic micro-robots do load–transport–deliver, clonal expansion | ✅ Confirmed (Zhang 2019 PNAS) |
| Soft two-photon micro-robots grip/rotate/kiss cells | ✅ Confirmed (Iványi & Kelemen 2024) |
| Inverted + 170 µm coverslip enables NA 1.2–1.35 | ✅ Engineering standard (inverted microscopes) — verify WD budget empirically for OS4 |
| Through-objective laser ablation on inverted geometry | ✅ Confirmed (Kaneshiro 2022, DOI 10.1017/qpb.2022.24 — IR laser through 20×/0.75 on inverted Ti2-E) |
| 100×/1.35 oil reaches cells in 100 µm channel on coverslip | ⚠ Predicted (WD marginal) — test needed |
| OET + AI steering loop works autonomously | ⚠ Predicted — to prototype |

## Update procedure
Follow OS1 EVIDENCE §6: verify PMID/DOI, add row, mark superseded with strikethrough.
