# PARAMETERS — ARGUS-OS4

**Version:** 1.0
**Date:** 2026-10-13

## OS4 Inverted OET Platform

| Parameter | Value |
|-----------|-------|
| Geometry | Inverted (objective below sample) |
| Objective | 60×/1.2 WI or 100×/1.35 oil, through 170 µm coverslip |
| Camera | sCMOS (Hamamatsu ORCA-Fusion BT) |
| AI | Jetson AGX Orin 64GB (edge inference) |
| Substrate | No.1.5 coverslip (170 µm) + ITO + a-Si:H ~1 µm |
| OET bias | 10–20 Vpp AC @ 10–100 kHz |
| Projector | DMD (Mightex Polygon1000) or consumer DLP, 530–650 nm |
| Manipulation | trap / transport / rotate / deliver / kiss |
| Microfluidics | 2× syringe pumps, PTFE/PEEK tubing |
| Sample | C. elegans embryos, mammalian cells, organoids |

## Inherited (from OS1/OS2/OS3)

| Parameter | Value |
|-----------|-------|
| Pedigree Score | PCA of 5 division-orientation metrics (fraction ∥, mean angle, variance, switches, cum. path) |
| Primary outcome | SAS-4 retention / SAS-1 (earlier decision) |
| Statistics | Bootstrap mixed model, BIC, sister-pair sensitivity, BF |
| Power target | N=100 embryos (~6,800 centrioles) |
| AIS | passport / body law / flight recorder / trace network |

## Budget

| Item | Cost |
|------|:---:|
| OET cell (substrate kit + a-Si:H) | ~$3K |
| DMD projector (Polygon1000) | ~$18K |
| Function generator + amp | ~$1.5K |
| Microfluidics (pumps, tubing) | ~$1.5K |
| Objective (60×/1.2 WI or 100×/1.35) | ~$12K |
| sCMOS + Jetson (from OS2) | ~$30K |
| Frame / inverted OpenFlexure build | ~$5K |
| **Total** | **~$71K** |

## Status
🟡 Concept & design (2026-10-13). Next: prototype substrate + projector test — see TODO.
