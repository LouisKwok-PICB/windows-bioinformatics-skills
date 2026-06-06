---
name: markdown-context-curator
description: Keep Markdown, YAML recovery records, and Codex skill docs concise and context-efficient. Use when Codex needs to create, update, audit, slim, archive, or reorganize `.md`, `.yaml`, `.yml`, or `SKILL.md` files; when active tasks are buried under completed history; when documentation bloat slows recovery; or when the user asks to keep task memory, plans, progress logs, or skills focused.
---

# Markdown Context Curator

Use this skill to keep documentation useful for the next agent, not merely short.

## Core Rule

When a Markdown, YAML, or skill file becomes bloated enough to hide the active task or slow context recovery, curate it immediately as part of the current work. Do not leave cleanup as a vague future task.

Compaction must be no-loss. Move, index, and summarize information so it can be loaded on demand; do not silently discard unique content.

## Document Roles

Assign each file one primary role before editing:

- `active`: current objective, next actions, guardrails, and source-of-truth links.
- `index`: compact map to files, scripts, outputs, and archives.
- `archive`: completed history, retired plans, old route comparisons, and provenance.
- `reference`: stable method rules, terminology, or reusable background.
- `package`: publication or handoff manifest, QC, content map, or submission record.

Do not let one file serve all roles. Split or move content when roles are mixed.

## Active-File Standard

For files such as `docs/CURRENT_TASK.md`, active project memory, or a current plan:

- Put the active task in the first screen.
- Keep only the current objective, target files, plan, next checkpoint, and guardrails.
- Link to archives instead of embedding long completed logs.
- Keep completed results to one-line summaries unless they directly affect the next action.
- Prefer "current source of truth" and "do not use" notes over long narrative history.
- Include an archive/index pointer for any substantial content moved out.

## Recovery Record Density Rule

For paired recovery records such as `AGENT_MEMORY.yaml` and `docs/CURRENT_TASK.md`, optimize for the next agent's first five minutes:

- `AGENT_MEMORY.yaml` should be a compact machine-readable index: current status, active objective, source-of-truth files, current output paths, latest decisions, next action, and hard guardrails.
- `docs/CURRENT_TASK.md` should be a human-readable active handoff: current task, why it matters, what has just changed, expected next checkpoint, and concise recovery notes.
- Detailed paper reviews, audit narratives, route histories, figure candidate comparisons, command logs, source-table inventories, and completed plans should live in task-specific docs, package docs, or archives, with one-line pointers in the active records.
- Each completed checkpoint in active records should usually be one bullet with date/status/result/path. Put the full reasoning in the linked source-of-truth document.
- Do not duplicate the same long conclusion in both recovery files. Put machine-oriented path/status in memory and human-oriented narrative in current task.

Start curation when any of these are true:

- the active task is not visible in the first screen;
- the file has become mostly completed history rather than next action;
- a reader must scan many old routes to find the current source of truth;
- repeated recovery updates are copying multi-paragraph summaries;
- active files approach several hundred lines or feel costly to load during resume;
- the same content is duplicated across memory, current task, plan, package, and archive records.

Use no-loss compaction. Move details into a stable source file or archive, then add an index row with: date/route, status, when to read, path, one-line result, and reason it is no longer active. Prefer query tables or "read first / read only if" lists over narrative history when many records exist.

## Archive Standard

Move completed work into `docs/archive/`, `archive/`, a package archive, or another clearly named archive location.

Use two archive patterns:

- full-history archive: original long text moved intact when exact provenance may matter;
- compact archive index: short route/date/status summaries that point to full history, outputs, manifests, or source tables.

Compact archive entries should include:

- date or route;
- status;
- key output paths;
- one-sentence result;
- reason it is no longer active.

Do not copy huge chat-style logs into default active files. If exact provenance is required, move the full text into an archive and add an index entry so it can be read only when needed.

## Skill-File Standard

For `SKILL.md` files:

- Keep `SKILL.md` focused on trigger, decision rules, workflow, and validation.
- Move detailed examples or long references into `references/` only when they are genuinely reusable.
- Do not add README, changelog, or auxiliary explanation files inside a skill.
- If the bloat lesson is reusable across projects, update or create a general skill rather than burying the rule in one project-specific skill.
- Preserve detailed skill knowledge by moving it to a named reference file and linking it from `SKILL.md`; do not delete reusable instructions just to reduce line count.
- Validate changed skills with the available skill validation script when practical.

## Cleanup Workflow

1. Measure the problem quickly with line counts, top sections, and search hits.
2. Identify the active task and the few records needed to recover it.
3. Choose no-loss handling: move full text intact, summarize with exact links, or split detailed reusable material into references.
4. Create or update an index that says when to read each moved file.
5. Rewrite the active file so the next agent can resume without reading history.
6. Update cross-links in memory, plan, registry, or package docs.
7. Re-read the edited top sections and verify the active task is visible immediately.
8. If a skill was changed, run validation when available.

## Safety

- Preserve unique scientific, legal, financial, or reproducibility evidence by moving or summarizing with source links; do not silently discard it.
- Do not change scientific claims, outputs, or code behavior while doing documentation cleanup unless the user requested that too.
- Do not archive material that is still needed for the next immediate action.
