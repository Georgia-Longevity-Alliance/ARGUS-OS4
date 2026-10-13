# OET Substrate — Photoconductive Cell (ITO / a-Si:H on 170 µm coverslip)

**Part of ARGUS-OS4.** The OET cell is the core new device: light patterns → virtual electrodes → DEP forces on cells.

## Device structure (bottom → top)

```
 ┌───────────────────────────────────────────────────────────┐
 │ Top ITO-coated glass (bias return electrode)              │   glass ~1.1 mm
 │   ITO ~100–200 nm                                         │
 ├───────────────────────────────────────────────────────────┤
 │ Microfluidic channel (spacer ~100 µm) — cells + medium    │
 │   spacer: double-sided tape or SU-8 ~100 µm               │
 ├───────────────────────────────────────────────────────────┤
 │ Photoconductive layer: a-Si:H (~1 µm)                     │   ← light-addressable
 │ Bottom ITO (~100–200 nm)                                  │
 │ **No.1.5 coverslip (170 µm)**                             │   ← thin optical window
 └───────────────────────────────────────────────────────────┘
        ▲  objective (WI/oil) from below
```

## Materials & thicknesses

| Layer | Material | Thickness | Notes |
|---|---|---|---|
| Top substrate | Glass (soda-lime / borosilicate) | 1.1 mm | Optional ITO for bias return |
| Top electrode | ITO (indium tin oxide) | 100–200 nm | Transparent conductor |
| Spacer | SU-8 3050 / double-sided tape | 100 µm (50–150 µm) | Defines channel height |
| Photoconductor | **a-Si:H (hydrogenated amorphous silicon)** | ~1 µm (0.5–2 µm) | PECVD-deposited; light-addressable |
| Bottom electrode | ITO | 100–200 nm | On coverslip |
| Bottom substrate | **No.1.5 coverslip** | **170 µm** | Thin window → high NA |

## Photoconductor options

| Material | Deposition | σ photo/dark ratio | Cost | Suitability |
|---|---|---|---|---|
| **a-Si:H (PECVD)** | PECVD (clean-room) | ~10³–10⁵ | $$ | **Best performance (standard OET)** |
| TiOPc (polymer) | spin-coat + cure | ~10³ (with plasmonic NP) | $ | Cheap, lower performance; FEOET/ODEP studies |
| c-Si (crystalline) | standard Si wafer | high | $$ | Opaque & thick — not for imaging; use for non-imaging OET |

**Recommendation:** a-Si:H via PECVD on an ITO-coated No.1.5 coverslip. This is the geometry used in high-performance OET (Chiou 2005; Wheeler group).

## Electrical drive

| Parameter | Value | Source |
|---|---|---|
| AC bias (across cell) | **10–20 Vpp** | Chiou 2005; Zhang PNAS 2019 (25 Vpp @ 20 kHz in some demos) |
| Frequency | **10–100 kHz** | Chiou 2005; typical OET |
| Waveform | sinusoidal / square | Square gives sharper field gradients |
| Max parallel traps | ~15,000 on 1.3×1.0 mm² | Chiou 2005 *Nature* |

## Light requirements

| Parameter | Value | Notes |
|---|---|---|
| Wavelength | 530–650 nm (green–red) | a-Si:H photoconductor peak; 633 nm (HeNe) common; 530–590 nm (LED) works |
| Intensity | ~10⁴× lower than optical tweezers; **0.1–10 mW/cm² typical** | OET "light-addressable" |
| Pattern source | DMD projector / LED projector | See OET_PROJECTOR.md |

## Fabrication steps (coverslip OET cell)

1. **Substrate:** No.1.5 coverslip (170 µm), pre-cleaned (piranha / UV-ozone).
2. **Bottom ITO:** sputter ~150 nm ITO (or purchase ITO-coated coverslips).
3. **a-Si:H:** PECVD ~1 µm hydrogenated amorphous silicon (SiH₄+H₂, ~200–250 °C).
4. **Channel spacer:** spin SU-8 (~100 µm) or laminate double-sided tape with a cut-out.
5. **Top ITO glass:** ITO-coated glass coverslip bonded over the channel (adhesive / UV-cure).
6. **Contacts:** silver epoxy / conductive tape to both ITO layers → function generator.

## Performance references
- Chiou, Ohta & Wu 2005 *Nature* 436:370–372 — OET principle, 15,000 traps, ~10⁵× lower light.
- Zhang et al. 2019 *PNAS* 116:14823 — optoelectronic micro-robots; SU-8 robots ≥200 µm; 25 Vpp @ 20 kHz; max velocity 1.1 mm/s, 9.7 rad/s.
- Islam & Park 2024 *Micromachines* 15:119 (PMC10818536) — FEOET/ODEP optimization; characteristic length Lc governs force; droplet opt r≈5·Lc; 4.08 µW/mm² low-intensity manipulation.
- Mightex OET application note — Polygon1000-patterned OET for cell + micro-robot manipulation.
