---
name: scientific-compute-resource-planner
description: Plan safe execution for computationally intensive scientific analyses by checking CPU, memory, disk, packages, OS, server constraints, parallel workers, chunking, progress logging, and portable server-run scripts. Use before long R/Python jobs, large spatial/single-cell/omics matrices, image processing, permutations/null simulations, bootstraps, model training, package installation decisions, or when the user asks how many threads, permutations, cells, chunks, or resources to use.
---

# Scientific Compute Resource Planner

## Core Rule

Do not weaken the scientific endpoint because a local machine is slow. First assess resources and choose a safe execution strategy. If the local environment is inadequate, write a portable server-run script with editable input/output directories, parameters, package checks, progress logs, and restart-safe outputs.

Respect the project language. For R-first projects, write R scripts by default and install mature R packages when available instead of hand-rolling specialized computation.

## Preflight Checklist

Before running long analyses, record:

- OS and shell;
- CPU logical cores and current load;
- total and available memory;
- disk free space in input, output, and temp locations;
- expected input size and matrix dimensions;
- package availability and versions;
- expected intermediate files;
- user/shared-server constraints;
- proposed workers, chunks, permutations, max cells per group/FOV, and seed;
- progress logging interval and estimated runtime checkpoints.

Use `references/preflight-command-patterns.md` for command patterns.

## Parameter Rules

- Leave at least 2 CPU cores free on shared machines, more when load is high.
- Do not set workers from `nproc` alone; use current load and memory per worker.
- For permutation/null simulations, prefer enough iterations for stable tails, but report Monte Carlo uncertainty when relevant.
- For spatial/single-cell data, cap cells per FOV/sample only when the cap is part of a documented approximation or sensitivity analysis.
- Use chunking or streaming when estimated peak memory exceeds 50-70% of available memory.
- Use reproducible seeds for randomized sampling, permutations, and null distributions.
- Print progress with elapsed time, completed units, total units, current memory-sensitive step, and output paths.

## Server-Run Script Contract

When preparing a server script:

- put editable `INPUT_DIR` and `OUTPUT_DIR` at the top;
- place user-tuned parameters immediately below them;
- create output directories if missing;
- fail early on missing files, missing columns, missing packages, or invalid parameters;
- write a run manifest with timestamp, parameters, package versions, input files, and output files;
- save intermediate result tables before expensive plotting;
- write `PDF`, `PNG`, and `TIFF` outputs for manuscript-facing figures unless the project says otherwise;
- include progress messages frequent enough to estimate remaining runtime.

Do not leave users with only an interactive notebook or hidden local path when the job is expected to run on a server.
