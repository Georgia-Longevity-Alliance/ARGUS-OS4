# PARAMETERS — ARGUS-OS4

**Version:** 1.0
**Date:** 2026-10-13

## OS4 Inverted OET Platform

| Parameter | Value |
|-----------|-------|
| Geometry | **Inverted (objective below sample)** — OS4 = ИНВЕРТИРОВАННАЯ версия ARGUS (OS1/OS2/OS3 — вертикальные, upright). Инвертированная геометрия — для иммерсионных объективов (WI/oil) и образцов на покровных стёклах (клеточные культуры) |
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

| Item | Cost | Market check (2026) |
|------|:---:|------|
| OET cell (substrate kit + a-Si:H) | ~$3K | ITO/a-Si:H substrate kit |
| DMD projector (Polygon1000) | ~$18K | Mightex Polygon1000, list ~$15–20K |
| Function generator + amp | ~$1.5K | e.g. Keysight 33500B ~$1.5–2.5K |
| Microfluidics (pumps, tubing) | ~$1.5K | 2× syringe pumps, PTFE/PEEK |
| Objective (60×/1.2 WI or 100×/1.35) | ~$12K | Nikon CFI Apo 60×/1.2 W ~$10–13K |
| sCMOS + Jetson (reused from OS2) | ~$30K | ORCA-Fusion BT list ~$50–60K (marginal cost if reused) |
| **Machined aluminium inverted chassis + thermal mgmt (in-incubator, 37°C)** | **~$12K** | CNC aluminium frame + heat sinks; **NOT 3D-printed polymer** |
| **Total** | **~$78K** | |

> **📌 Геометрия платформы (варианты):** OS1/OS2/OS3 — вертикальные (upright, OpenFlexure-база); **OS4 — инвертированная версия** (объектив снизу, для WI/oil-иммерсии и культур на покровных стёклах). **Опция:** инвертированный вариант может быть собран и для OS1/OS2/OS3 по архитектуре OS4 — т.е. геометрия это вариант сборки, а не отдельная платформа.
>
> **🔧 Корпус (опция, не обязательство):** OS4 в инкубаторном боксе (37°C, влажность, тепло от DMD ~18W и Jetson ~20–40W) требует металлический (CNC-алюминий) корпус вместо 3D-печатного полимера — полимер деформируется при 37°C+ (тепловой дрейф оптики) и не отводит тепло. При не-инкубаторном использовании допустим облегчённый вариант. В бюджете учтён металлический каркас (~$12K).

## Status
🟡 Concept & design (2026-10-13). Next: prototype substrate + projector test — see TODO.
