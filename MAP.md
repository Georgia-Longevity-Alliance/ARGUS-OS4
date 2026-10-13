# MAP — ARGUS-OS4

```
ARGUS-OS4/  (inverted + OET)
├── README.md              # overview
├── _pi.md                 # parent/deps
├── CONCEPT.md             # why inverted + OET, hypothesis, budget
├── DESIGN.md              # architecture (projector/OET cell/objective/AI)
├── PARAMETERS.md          # OS4 parameters + budget
├── EVIDENCE.md            # OET + centriole evidence (verified PMID/DOI)
├── TODO.md                # Phase 0 (OET PoC) / Phase 1 (build) / Phase 2 (biology)
├── LICENSE                # MIT
├── hardware/
│   └── oet/               # OET cell module
│       ├── OET_SUBSTRATE.md        # ITO/a-Si:H on 170 µm coverslip
│       ├── OET_PROJECTOR.md        # DMD projector parameters
│       ├── OET_SIGNAL_GENERATOR.md # AC bias 10-20 Vpp @ 10-100 kHz
│       ├── OET_MICROFLUIDICS.md    # sample delivery / media exchange
│       └── OET_BOM.csv             # bill of materials
└── docs/
    └── INVERTED_ARGUS_DESIGN.md    # grant-ready technical description
```

## Dependencies
- ARGUS-OS1 — OpenFlexure base, Jetson AI, AIS layer
- ARGUS-OS2 — pedigree → fate analysis
- ARGUS-OS3 — causality / entropy reset

## References to sister repos
- GitHub: `Georgia-Longevity-Alliance/ARGUS-OS1`, `ARGUS-OS2`, `ARGUS-OS3`, `ARGUS-OS4`
- djabbat mirror (private)
