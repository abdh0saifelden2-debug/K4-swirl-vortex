# Split audit — K4-swirl-vortex

How this repository was carved out of the pristine **K** monorepo. Regenerate the classification with [`K-audit` v1.0](https://github.com/abdh0saifelden2-debug/K-audit/tree/v1.0) — `python3 classify.py --mono K K4-swirl-vortex` — and re-check the import graph with `python3 verify_repo.py --mono K K4-swirl-vortex` (both run from a clone of `K-audit` against a clone of the monorepo).

## Claim cluster

the atmospheric-vortex application (Goldshtik–Sorokin / Otis).

Source: `atmosphere/**` + `general_two_clocks/{closure,compressible}/**` + `subglacial/{__init__,diag}.py` (the diagnostics the swirl runner imports).

## Composition

| | files |
|---|---|
| traced to a monorepo file | 33 |
| byte-identical copies | 30 |
| modified (see *Edits*) | 3 |
| new (not in the monorepo) | 1 |

Source directories, by file count:

- `atmosphere/figures/` — 8
- `general_two_clocks/closure/` — 7
- `atmosphere/swirl/` — 4
- `(monorepo root)`/ — 3
- `atmosphere/` — 3
- `general_two_clocks/compressible/` — 3
- `glaciers/subglacial/` — 2
- `atmosphere/tests/` — 2
- …plus 1 file(s) that sit alone in their source directory (top-level scripts, one-off reports)

## Vendored files

Copied byte-for-byte from the monorepo paths below (this is what makes the repo import-clean on its own):

- `REPORT_SWIRL.md`
- `REPORT_SWIRL_REAL.md`
- `run_swirl.py`
- `closure/*` (7 files)
- `compressible/__init__.py`
- `compressible/ns.py`
- `compressible/solver.py`
- `figures/*` (8 files)
- `subglacial/__init__.py`
- `subglacial/diag.py`
- `swirl/__init__.py`
- `swirl/flow.py`
- `swirl/levitation.py`
- `swirl/otis.py`
- `swirl/data/otis_besttrack.csv`
- `tests/test_swirl.py`
- `tests/test_swirl_otis.py`

## Edits

- `README.md` — rewritten to stand alone: no `../` links into sibling monorepo folders, run commands given from the repo root, and a Provenance section pointing at the archive.
- `pyproject.toml` — rewritten for this repo: `testpaths`/`pythonpath` scoped to this repo instead of all five monorepo domains, and the dependency list trimmed to the libraries this claim cluster imports.
- `requirements.txt` — rewritten for this repo: `testpaths`/`pythonpath` scoped to this repo instead of all five monorepo domains, and the dependency list trimmed to the libraries this claim cluster imports.

## Excluded files

- none: every monorepo file belonging to this claim cluster was carried over.

## Test-suite accounting

`tests/` carries **2 test files** (atmosphere/tests (2)); the whole monorepo has 136 test files across the five repos (78+39+15+2+2 = 136; the NR33–NR35 modules relocated from K1 now count under K2).

## Verification

[`K-audit`](https://github.com/abdh0saifelden2-debug/K-audit/tree/v1.0) `verify_repo.py` walks the **AST import graph** of every Python file in this repo, expands each unqualified import against every `sys.path` root the file would actually see, and reports any import that resolves only outside the repository. Result:

```
OK K4-swirl-vortex: no external edges
```

## Provenance

Pristine snapshot taken **before** any edit: `K-monorepo-archive.tar.gz` (SHA-256 `ef637ff55f912a5d1404f677429f9429eccc8102a8cab23cee79cf055bbf1220`). `FUTURE_WORK.md` / `PAPER_OUTLINE.md` were deliberately left in the archive.
