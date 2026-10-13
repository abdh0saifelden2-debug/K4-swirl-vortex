# Swirl vortex — the two clocks at a turbulent vortex (Goldshtik–Sorokin / Hurricane Otis)

The atmospheric *observation* of the two clocks (NEON, ASOS, reanalysis) is part
of the theory repository **`K1-two-clocks-theory`** (see Provenance below) — it
is the foundation the whole program rests on. This repository holds the
atmospheric **application**: does the K-theory blindness matter at a coherent
atmospheric vortex, where the global (elliptic) low-pressure core well is the
load-bearing structure?

## What was found so far

- **[VERIFIED a-priori]** At a sustained 128² turbulent swirl, the exact subgrid
  momentum force is compared against three closures
  ([`REPORT_SWIRL.md`](REPORT_SWIRL.md), Figs 40–43, `run_swirl.py`):
  - Smagorinsky (K-theory): transfer correlation **+0.19**, drains the resolved
    swirl ~**385×** faster than truth → suspension margin **0.36**, the levitated
    particle **falls**.
  - Spectrum-matched surrogate: right energy, but breaks ∇·m = 0 → injects
    spurious pressure into the very core well it must preserve.
  - Projected-FDT: correlation **+0.99**, solenoidal, tracks the truth's net
    drain → particle stays up.
- **[VERIFIED on real-storm geometry]** The result survives calibration to
  **Hurricane Otis** (NHC HURDAT2 best track, bundled in `swirl/data/`): with
  Otis's measured Holland-B vortex shape, K-theory still over-drains at ~**170×**
  truth (margin 0.69 < 1, falls); projected-FDT holds the core well (margin
  ≈ 1.00). [`REPORT_SWIRL_REAL.md`](REPORT_SWIRL_REAL.md), Figs 44–47.
- The mechanism chain — global elliptic core well ⇒ pressure-gradient levitation
  ⇒ any closure that kills backscatter kills the well — is exactly the Part-8b
  benchmark verdict transplanted to an atmospheric structure.

## What remains a HYP

- **Rapid-intensification relevance [HYP]** — the suggestive framing (Otis's
  missed Cat-5 jump as a fast-clock/backscatter failure of operational closures)
  is *motivation*, not a demonstrated result. Nothing here is a hurricane
  forecast.
- **3-D vortex dynamics [HYP]** — the demo is 2D, frozen-field, a-priori; no
  vortex stretching, no boundary-layer inflow, no moist physics.
- **Suspension proxy [HYP]** — levitation is scored by force balance, not an
  integrated Lagrangian trajectory; only the *relative* ordering of closures is
  meaningful.

## What is pending

- An **a-posteriori** swirl LES (run the closures inside the time integration,
  as the cavity 3-D runner does in **`K2-subglacial-cavity`**).
- A 3-D swirl extension with stretching, and a real radiosonde/dropsonde-based
  test of the two-clocks spectral fingerprint inside a tropical cyclone.
- Connecting the measured memory time `τ_c` to an operational eddy-viscosity
  correction for vortex-resolving models (RSM/EDMF/LES positioning is sketched
  in `K2-subglacial-cavity/subglacial/THEORY_CAVITY.md` §15 in the full
  snapshot).

## Contents

- `swirl/` — swirl DNS library (`flow.py`), Otis best-track loader + Holland
  calibration (`otis.py`, `data/otis_besttrack.csv`), levitation diagnostics
  (`levitation.py`).
- `run_swirl.py` — Part 10 runner (`--swirl idealized` or `--swirl otis`).
- `closure/`, `compressible/`, `subglacial/` — vendored solver dependencies
  (see `AUDIT.md`), so this repo is import-clean on its own.
- `figures/` — Figs 40–47. `tests/` — `test_swirl.py`, `test_swirl_otis.py`.

## Quick start

```bash
python3 -m venv .venv && . .venv/bin/activate
pip install -r requirements.txt
python run_swirl.py --swirl otis --out-dir figures
python -m pytest            # 20 passed
```

## Provenance

Split out of the **K** monorepo, partitioned by claim cluster:

| repository | claim cluster |
|---|---|
| `K1-two-clocks-theory` | observation, two-clocks theory, closure benchmarks |
| `K2-subglacial-cavity` | cavity DNS, real-bed validation, field-analysis validation |
| `K3-scallop-migration` | scallop instability family, channelisation |
| `K4-swirl-vortex` *(this repo)* | atmospheric vortex application |
| `K5-ocean-probes` | ice–ocean double diffusion |

The pristine monorepo was snapshotted **before** any edit:
`K-monorepo-archive.tar.gz`, SHA-256
`3c30c68b4d4287787af00539b2cbe75a47dc0536491ec0d1b17a0f61d80b5304`
(`K-monorepo-archive.sha256`). The cross-repo claim ledger (`FUTURE_WORK.md`)
and paper outline are deliberately **not** copied here — they live only in that
archive. `AUDIT.md` records the AST dependency audit that decided this split.
