# MEMORY — ARGUS-OS4

**Date:** 2026-10-13 · **Status:** 🟡 Concept/design

## Key decisions
1. **Inverted geometry** chosen over upright for OS4 — enables high-NA WI/oil on 170 µm coverslip and separates OET projection (above) from imaging objective (below).
2. **Substrate on No.1.5 coverslip (170 µm)** — the single change that unlocks both high NA and OET in one device (mirrors how inverted microscopes achieve WI/high resolution).
3. **a-Si:H as primary photoconductor** (foundry PECVD); TiOPc spin-coat as low-cost fallback (Islam & Park 2024).
4. **Consumer DLP projector acceptable** (Wheeler/Zhang approach); Polygon1000 as high-end option.
5. **60×/1.2 WI primary objective** (WD 0.28 mm ≥ 0.17 coverslip + ~0.1 channel); 100×/1.35 oil marginal (WD 0.13 mm) — flagged as open question.

## Lessons learned (from 6-source analysis)
- OET is the only technique combining high throughput + high resolution + contact-free + low photodamage at once.
- Micro-robots (SU-8 OET-driven; two-photon soft grippers) extend OET to "gripping" tasks.
- Limited-FOV control (Li/Cheah) is the engineering backbone for autonomous steering.

## Blockers
- a-Si:H deposition needs a clean-room/foundry (or TiOPc fallback).
- WD budget for 100×/1.35 oil through coverslip+channel needs empirical validation.
- No prototype built yet.

## Links
- Full design: `docs/INVERTED_ARGUS_DESIGN.md`
- Evidence: `EVIDENCE.md`
