---
name: project-log
description: Use when the user asks to log, record, summarize, or maintain project progress at logical milestones in a repository or project. This skill updates a project-local PROGRESS.md with concise notes about what has been done, current status, decisions, blockers, and next steps.
---

# Project Log

Use this skill to maintain a project-local `PROGRESS.md` that captures meaningful progress at logical points during work.

## When To Log

Update `PROGRESS.md` when one of these is true:

- A task, feature slice, investigation, or bug fix reaches a clear stopping point.
- A significant decision, tradeoff, blocker, or scope change appears.
- The user asks for progress to be logged, checkpointed, recorded, or summarized.
- Work pauses or hands off with important context that should survive conversation history.

Do not log every tiny command, failed attempt, or routine edit. Prefer useful checkpoints over a transcript.

## Location

- Save the log as `PROGRESS.md` in the project root unless the user specifies another root.
- If the current working directory is a subdirectory, infer the project root from repository markers such as `.git`, package manifests, or the user’s stated project path.
- Create `PROGRESS.md` if it does not exist. Preserve existing content and append a new entry.

## Entry Format

Append entries in reverse chronological order when the file already uses that style; otherwise append to the end. Keep the existing style if one is present.

For a new file, use:

```markdown
# Progress

## YYYY-MM-DD HH:MM TZ

### Done
- ...

### Decisions
- ...

### Blockers
- ...

### Next
- ...
```

Omit empty sections. Use the local date and timezone when available.

## Content Rules

- Be concise and factual. Write for a future agent or developer resuming the work.
- Include file paths, commands, test results, and important outputs only when they help explain state.
- Note unresolved risks, skipped validation, and assumptions explicitly.
- Distinguish completed work from planned next steps.
- Do not include secrets, private credentials, or long pasted logs.
- Do not claim tests passed unless they were actually run.

## Workflow

1. Inspect any existing `PROGRESS.md` to match its structure and avoid duplicate entries.
2. Summarize only the meaningful progress since the last relevant entry.
3. Update `PROGRESS.md` using the project’s root and existing style.
4. Mention the log update in the final response, including any validation status that matters.
