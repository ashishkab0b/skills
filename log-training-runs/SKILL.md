---
name: log-training-runs
description: Maintain a project-local RUNS.md training run log for ML, deep learning, data processing, benchmark, evaluation, experiment, fine-tuning, or model training work. Use when the user asks to log, record, append, summarize, or maintain information about a model run, experiment run, training job, evaluation run, benchmark run, dataset run, hyperparameter test, or output artifact.
---

# Log Training Runs

## Overview

Create or update `RUNS.md` in the active project with a concise, audit-friendly record of training and evaluation runs. Capture concrete facts from the repo, command output, user notes, and available artifacts; mark unknowns explicitly instead of inventing them.

## Workflow

1. Locate the project root. Prefer the Git root from `git rev-parse --show-toplevel`; otherwise use the current working directory.
2. Read any existing `RUNS.md`. Preserve its structure, ordering, heading levels, tone, and field names when it already has a clear convention.
3. Gather run context before editing:
   - Timestamp with timezone.
   - Git branch, commit SHA, commit subject, and dirty status.
   - Run command, config files, scripts, notebooks, model names, datasets, checkpoints, seeds, hyperparameters, and environment details available in the conversation or workspace.
   - When the user provides a CLI command, inspect the referenced training script and config files to identify defaults from `argparse`, `click`, `typer`, dataclasses, config loaders, YAML/JSON/TOML files, shell wrappers, or framework launchers. Combine explicit CLI overrides with script/config defaults into a `Training Parameters` segment.
   - Resolve specific input and output paths from both the CLI command and script defaults. Prefer project-relative paths when clear, include absolute paths when the command uses them, and mark dynamic or unresolved paths as `unknown` or `computed at runtime`.
   - Inputs tested, hypothesis or substantive question, metrics, notable logs, failures, output artifacts, and next steps.
4. Append a new entry unless the user asks to edit an existing entry. If the existing log is newest-first, add the entry near the top; if oldest-first, add it at the bottom.
5. Keep the entry useful but compact. Favor specific filenames, commands, artifact paths, metric names, and observations over generic prose.
6. If a run is still in progress, label it as `in progress` and record the current checkpoint, last observed output, and what remains to be checked.

## Entry Content

When no established format exists, create `RUNS.md` with a short title and entries like this:

```markdown
# Runs

## 2026-04-17 14:32:10 PDT

- Description: What substantive question, recent script change, hypothesis, or model behavior this run tested.
- Status: completed | in progress | failed
- Git: branch `main`, commit `abc1234` (`commit subject`), dirty: yes/no
- Command: `python train.py --config configs/experiment.yaml`
- Training Parameters: Batch size, learning rate, epochs/steps, optimizer, scheduler, precision, device/distributed settings, seed, model/checkpoint, config values, and other script arguments. Note whether values came from CLI overrides, config files, or script defaults.
- Inputs: Specific dataset, split, config, prompt, model weight, checkpoint, cache, or manifest paths from the CLI and script defaults.
- Outputs: Specific checkpoint, log, report, table, plot, model file, eval artifact, cache, external run ID, or output directory paths from the CLI and script defaults.
- Results: Metrics, qualitative observations, failures, warnings, timing, and resource notes.
```

Include additional fields that are meaningful for the current run when the available context supports them.

## Quality Rules

- Do not fabricate metrics, artifact paths, commits, or outcomes. Write `unknown`, `not captured`, or `not yet available` when needed.
- Record enough detail for a future rerun: command, resolved training parameters, config, data version, code version, model/checkpoint, and seed when available.
- Avoid rewriting old entries.
