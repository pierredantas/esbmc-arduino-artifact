# ESBMC-Arduino — Reproducibility CI

[![Reproducibility Check](../../actions/workflows/reproduce.yml/badge.svg)](../../actions/workflows/reproduce.yml)

This repository hosts the **GitHub Actions CI** that validates the reproducibility of the artifact published at:

> **Zenodo DOI:** [10.5281/zenodo.21014210](https://doi.org/10.5281/zenodo.21014210)

The workflow runs on a **clean Ubuntu 22.04 runner** — no pre-installed ESBMC, CBMC, or Frama-C — and mirrors exactly what a reviewer would do following the artifact's instructions.

## What the workflow does

| Step | Description |
|------|-------------|
| Download | Fetches `esbmc-arduino-artifact.tar.gz` directly from Zenodo |
| Verify | Checks SHA-256 against the published `SHA256SUMS` |
| Setup | Runs `setup.sh` (installs CBMC 6.10.0, Frama-C 32.1, MATIEC; builds patched ESBMC) |
| Reproduce | Runs `reproduce.sh` and captures full log |
| Upload | Publishes `results/` + `reproduce.log` as a GitHub Actions artifact (90-day retention) |

## How to trigger a run

- **Automatic:** runs on every push to `main` and on the 1st of each month
- **Manual:** go to *Actions → Reproducibility Check → Run workflow*

## Results

Each successful run produces a downloadable archive under *Actions → [run] → Artifacts*.  
The job summary tab shows the last 30 lines of `reproduce.log` inline.

## Citing

If you use this CI setup as evidence of reproducibility, cite the Zenodo record:

```
@software{esbmc_arduino_artifact,
  author    = {Anonymous Author(s)},
  title     = {ESBMC-Arduino: Reproduction Artifact},
  year      = {2026},
  doi       = {10.5281/zenodo.21014210},
  publisher = {Zenodo}
}
```
