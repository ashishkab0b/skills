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
   - Inputs tested, hypothesis or substantive question, metrics, notable logs, failures, output artifacts, and next steps.
4. Append a new entry unless the user asks to edit an existing entry. If the existing log is newest-first, add the entry near the top; if oldest-first, add it at the bottom.
5. Keep the entry useful but compact. Favor specific filenames, commands, artifact paths, metric names, and observations over generic prose.
6. If a run is still in progress, label it as `in progress` and record the current checkpoint, last observed output, and what remains to be checked.

## Recommended Checks

Use local commands when available and relevant:

```bash
date "+%Y-%m-%d %H:%M:%S %Z"
git rev-parse --show-toplevel
git branch --show-current
git rev-parse HEAD
git log -1 --pretty=%s
git status --short
git diff --stat
```

For training artifacts, inspect likely output directories without making assumptions. Common names include `runs/`, `outputs/`, `artifacts/`, `checkpoints/`, `logs/`, `wandb/`, `mlruns/`, `tensorboard/`, `results/`, and `models/`.

## Entry Content

When no established format exists, create `RUNS.md` with a short title and entries like this:

```markdown
# Runs

## 2026-04-17 14:32:10 PDT - Short run name

- Status: completed | in progress | failed
- Git: branch `main`, commit `abc1234` (`commit subject`), dirty: yes/no
- Command: `python train.py --config configs/experiment.yaml`
- Purpose: What substantive question, hypothesis, regression, or model behavior this run tested.
- Inputs: Dataset, split, config, prompts, model weights, seed, notable hyperparameters.
- Outputs: Checkpoints, logs, reports, tables, plots, model files, eval artifacts, or external run IDs.
- Results: Metrics, qualitative observations, failures, warnings, timing, and resource notes.
- Next: Follow-up run, cleanup, investigation, or decision.
```

Include only fields that are meaningful for the current run. Add fields such as `Hardware`, `Duration`, `Environment`, `Baseline`, `Comparison`, `Run ID`, or `Owner` when the available context supports them.

## Quality Rules

- Do not fabricate metrics, artifact paths, commits, or outcomes. Write `unknown`, `not captured`, or `not yet available` when needed.
- Prefer links or paths to durable artifacts over pasted logs. Quote only the few log lines needed to explain the outcome.
- Mention uncommitted changes when present because they affect reproducibility.
- Record enough detail for a future rerun: command, config, data version, code version, model/checkpoint, and seed when available.
- Separate observation from interpretation. Results say what happened; next steps say what to do about it.
- Avoid rewriting old entries except to correct factual mistakes or add a clearly labeled update.
