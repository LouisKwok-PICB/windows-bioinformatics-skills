---
name: windows-code-execution
description: Use when running or writing commands on Windows, especially PowerShell, Rscript, Python, paths with spaces, quoting, here-strings, CSV/RDS reads, or avoiding failures from shell variable expansion, BOM/encoding, and unsafe file operations.
---

# Windows Code Execution

Use this skill before running non-trivial shell commands in a Windows workspace, especially when invoking R or Python from PowerShell.

## Core Rules

- Prefer short, single-purpose commands. Use real script files for complex R/Python logic.
- Use `-LiteralPath` for existing filesystem paths. For `New-Item` directory creation, use `-Path`; not every PowerShell host exposes `New-Item -LiteralPath`.
- `-LiteralPath` treats wildcard characters such as `*` literally. Do not pass wildcard paths like `C:\dir\*.R` to `Select-String -LiteralPath`; expand files first with `Get-ChildItem` and pass `.FullName`, or use `Select-String -Path` when wildcard expansion is intended.
- For Windows paths passed into R/Python code, prefer forward slashes: `C:/path/to/project/file.csv`.
- Avoid PowerShell here-strings piped into `Rscript -` unless encoding has been verified; BOM and `$` expansion can corrupt embedded code.
- In inline PowerShell commands, avoid R/Python code that contains unescaped `$`. Prefer R `df[['Gene']]` over `df$Gene`.
- Use `apply_patch` for manual file edits. Do not use shell redirection, `cat`, or here-string writes to create or edit project files.
- Do not build destructive file operations with string-concatenated shell commands. Resolve paths and use native PowerShell cmdlets.
- Keep PowerShell object construction simple: compute conditional values first, then create `[pscustomobject]`.
- Do not pipe directly from a `foreach (...) { ... }` language statement. Assign loop output to `$rows`, then pipe `$rows`.
- Do not assume newer .NET APIs are present in Windows PowerShell. In particular, `[System.IO.Path]::GetRelativePath()` may be unavailable; for manifest/QC relative paths, compute a normalized root prefix and use `Substring()` after checking `StartsWith()`, or delegate path normalization to R/Python.
- Treat memory, CPU, disk, wall-time, package, or OS limits as execution-environment constraints. Create a portable server-run script rather than weakening the scientific endpoint.
- When a reusable Windows command failure is fixed, update the relevant skill or reference with the failed pattern, symptom, safe replacement, and validation.

## Reference Routing

Load only the reference needed for the current command:

- Rscript, Python, `$` expansion, and stdin/here-string problems: `references/r-python-commands.md`.
- PowerShell filesystem reads, path creation, object construction, pipelines, and hash/QC checks: `references/powershell-patterns.md`.
- Portable server-run scripts for work that cannot run locally: `references/server-run-scripts.md`.

## Minimal Workflow

1. Identify whether the command is filesystem, R, Python, sync/QC, or server-run work.
2. Load the matching reference only if the core rules above are not enough.
3. Run the smallest command that proves the next step.
4. If a command fails, diagnose quoting, path, encoding, `$` expansion, and pipeline structure before blaming the data or code.
5. For reusable failures, update the relevant skill/reference before finishing.
