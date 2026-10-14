# OET Microfluidics (Sample Delivery) — ARGUS-OS4

**Part of ARGUS-OS4.** Delivers cells/embryos into the OET channel and enables media exchange, washing, and collection after manipulation.

## Requirements

| Need | Specification |
|---|---|
| Load cells/embryos into OET channel | gentle, no shear damage (embryos ~30–50 µm, cells 5–30 µm) |
| Medium exchange | laminar flow, low shear |
| In-situ imaging | transparent channel, compatible with 170 µm coverslip |
| Collect manipulated cell | removable / dedicated outlet well |

## Design

### Channel
- OET channel defined by spacer (SU-8 or double-sided tape, ~100 µm) between top ITO glass and bottom coverslip+ITO+a-Si:H.
- Inlet & outlet ports: 0.5–1 mm holes drilled in the **top** glass (avoids compromising the thin coverslip bottom window).
- Dead volume minimal; connect PTFE/FEP tubing (0.5 mm ID).

### Pumping
- **Syringe pumps** (2×, e.g. NE-1000 / Aladdin) — one for sample, one for medium; flow 0.1–10 µL/min.
- **Gravity-driven** optional for very gentle delivery.
- **Peristaltic** for medium circulation during long imaging (OS1 overnight runs).

### Chamber modes
| Mode | Flow | Use |
|---|---|---|
| Load | 1–5 µL/min, sample syringe | Introduce cells/embryos |
| Trap | 0 | OET manipulates (no flow) |
| Wash | 5–20 µL/min buffer | Remove debris, exchange medium |
| Deliver/collect | forward + reverse | Move target to outlet for downstream analysis (RNA-seq, clonal expansion) |

## Integration with OET manipulation
- Cells loaded → flow stopped → OET traps selected cells → transport within channel.
- Media refresh between imaging intervals (2-min cycle) — pilot P2 phototoxicity compatible.

## Sterility / materials
- Autoclave-compatible: glass, PTFE/PEEK tubing, stainless fittings.
- PDMS/SU-8 parts — EO or UV-C sterilization (see OS1 STERILIZATION_TRANSFER SOP).
- Single-use coverslip+ITO assemblies — batch fabricate.

## Open/hybrid option
- For open-chamber / droplet work (FEOET/ODEP style, Islam & Park 2024 Micromachines 15:119): PDMS open chamber on the photoconductive surface; micropipette/manual loading. Enables droplet microfluidics if needed later.
