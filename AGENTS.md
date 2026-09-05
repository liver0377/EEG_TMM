# AGENTS.md

## Scope

These instructions apply to this code repository. It is a personal Git clone used for the Cognition-Injected Diffusion paper revision. Read `docs/协作与同步指南.md` before changing data paths, importing historical scripts, or launching experiments.

## Sources of truth

- The remote Git repository is the source of truth for code, configurations, manifests, splits, tests, and reviewed summary metrics.
- `CID_DATA_ROOT` points to shared source data. Treat all content there as read-only.
- `CID_ARTIFACT_ROOT` stores checkpoints, embeddings, generated images, logs, and raw metrics. These are not Git content.
- Historical source material under `/root/fsas/dataset_eeg/unpacked/datasets` must not be modified from this repository.

## Git and collaboration

- Every person and every cloud instance uses a separate clone.
- Work on a task branch and merge through review.
- Preserve unrelated user changes; never reset, clean, checkout, or discard them without explicit authorization.
- Do not use `git add .` or `git add -A`. Stage explicit files after reviewing `git status`.
- Never commit datasets, weights, embeddings, generated images, raw logs, caches, secrets, or virtual environments.
- Do not copy `.git` or synchronize working trees with `rsync`.

## Paths and configuration

- Do not hardcode user-specific or instance-specific absolute paths in Python code.
- Obtain storage locations from `CID_DATA_ROOT`, `CID_ARTIFACT_ROOT`, and `CID_CACHE_ROOT`, or from explicit configuration fields.
- Committed configurations must be portable. Machine-local overrides belong in ignored `.env` or `config.local.yaml` files.
- Resolve paths once at the application boundary and pass them explicitly to reusable functions.

## Data safety

- Raw data is immutable.
- Changed preprocessing creates a new versioned directory and manifest.
- Never silently change a split, channel order, EEG-image mapping, band definition, time window, or normalization rule.
- Before any destructive action, resolve and show the exact target and obtain explicit user authorization.
- Avoid broad recursive scans of NFS storage when a targeted query is sufficient.

## Experiment requirements

Each formal run must have a unique directory:

```text
<artifact-root>/<owner>/<experiment>/<timestamp>_<instance>_<git-sha>_seed<seed>/
```

Each run must record:

- resolved configuration;
- launch command and Git commit;
- random seed;
- dataset split and preprocessing manifest versions;
- Python, PyTorch, CUDA, dependency, and GPU information;
- logs and machine-readable metrics;
- checkpoints or generated samples when applicable.

Write incomplete artifacts to a temporary filename inside the run directory and rename only after completion. Never reuse another run directory.

## Implementation workflow

1. Inspect repository status and relevant configuration.
2. Identify the exact external inputs and new output directory.
3. Add or update a fast test when practical.
4. Run a small smoke test before a long experiment.
5. Make scoped changes and report the files changed, validation performed, and artifact location.

Do not install or upgrade CUDA, NVIDIA drivers, PyTorch, or core ML packages without first inspecting compatibility and obtaining user approval.
