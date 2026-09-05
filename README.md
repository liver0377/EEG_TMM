# EEG_TMM

Code and reproducibility assets for the major revision of the Cognition-Injected Diffusion paper.

This repository contains code, portable configurations, dataset manifests, split definitions, tests, and small summary results. Raw datasets, model checkpoints, embeddings, generated images, and run logs live outside Git.

## Repository layout

```text
configs/          Portable experiment configurations
docs/             Human-facing collaboration and experiment documentation
manifests/        Versioned descriptions of external datasets and preprocessing
results/summary/  Small, reviewed CSV/JSON summaries used by the paper
scripts/          Thin command-line entry points
splits/           Versioned train/validation/test sample lists
src/eeg_tmm/      Reusable Python package code
tests/            Fast tests and smoke tests
```

## Local paths

Copy `.env.example` to `.env` in each personal clone and adjust it for that instance. Never commit `.env`.

```bash
cp .env.example .env
```

Expected variables:

```text
CID_DATA_ROOT      Read-only source datasets
CID_ARTIFACT_ROOT  Unique run outputs and checkpoints
CID_CACHE_ROOT     Downloaded model and framework caches
```

The current shared source is `/root/fsas/dataset_eeg/unpacked/datasets`. New experiments should use `/root/fnvme/cid_revision/artifacts/<owner>/...` for outputs.

## Development status

The repository currently contains only the collaboration and reproducibility scaffold. Historical scripts are intentionally not copied yet because they contain user-specific absolute paths and need to be audited before migration.

Read `AGENTS.md` and `docs/协作与同步指南.md` before changing paths, importing historical code, or launching experiments.

The current legacy-asset audit and the execution order for Wu Dawei's experiments are documented in `docs/吴大伟实验审计与执行计划.md`.
