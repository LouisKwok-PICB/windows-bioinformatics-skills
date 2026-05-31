# Installation

## Manual Install

Copy the desired skill directories into your Codex skills folder.

On Windows PowerShell:

```powershell
$repo = "I:/github/windows-bioinformatics-skills"
$codexSkills = "$env:USERPROFILE/.codex/skills"
New-Item -ItemType Directory -Force -Path $codexSkills | Out-Null

Copy-Item -Recurse -Force "$repo/skills/scientific-research-evidence-planner" "$codexSkills/"
Copy-Item -Recurse -Force "$repo/skills/scientific-manuscript-writer" "$codexSkills/"
Copy-Item -Recurse -Force "$repo/skills/publication-plot-styler" "$codexSkills/"
Copy-Item -Recurse -Force "$repo/skills/paper-figure-assembler" "$codexSkills/"
Copy-Item -Recurse -Force "$repo/skills/publication-content-packager" "$codexSkills/"
Copy-Item -Recurse -Force "$repo/skills/windows-code-execution" "$codexSkills/"
Copy-Item -Recurse -Force "$repo/skills/pdf" "$codexSkills/"
```

After copying, restart Codex or reload the environment so the skill metadata are discovered.

## Install Selected Skills

You can install only the skills you need. For example, to install only manuscript-writing and evidence-planning skills:

```powershell
$repo = "I:/github/windows-bioinformatics-skills"
$codexSkills = "$env:USERPROFILE/.codex/skills"
New-Item -ItemType Directory -Force -Path $codexSkills | Out-Null

Copy-Item -Recurse -Force "$repo/skills/scientific-research-evidence-planner" "$codexSkills/"
Copy-Item -Recurse -Force "$repo/skills/scientific-manuscript-writer" "$codexSkills/"
```

## Important Copy Rule

Copy the whole skill folder. Do not copy only `SKILL.md`.

Several skills include `references/`, `agents/`, or `assets/` files that are loaded only when needed. Omitting them will make the skill less useful or incomplete.

## Expected Directory Shape

After install, a skill should look like:

```text
~/.codex/skills/publication-plot-styler/
  SKILL.md
  agents/openai.yaml
  references/
```

## Dependencies

The skills themselves are Markdown instructions. Some workflows may ask the assistant to use external software when appropriate:

- R and R packages such as `ggplot2`, `ComplexHeatmap`, `grid`, `ragg`, or `svglite` for publication figures.
- Python packages such as `reportlab`, `pdfplumber`, or `pypdf` for PDF workflows.
- Poppler tools for PDF rendering when layout review is needed.

The skills do not install dependencies automatically. Users should decide whether package installation is appropriate for their environment.
