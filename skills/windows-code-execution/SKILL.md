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
- For validation manifests or inventories that intentionally contain wildcard patterns such as `panelS1_*.tiff` or `supplement_table_*.csv`, branch explicitly: use `Test-Path -LiteralPath` / `Get-Item -LiteralPath` for literal paths and `Get-ChildItem -Path` for wildcard rows. Do not validate wildcard rows with `-LiteralPath`, or you will create false missing-file failures.
- For Windows paths passed into R/Python code, prefer forward slashes: `C:/path/to/project/file.csv`.
- Avoid PowerShell here-strings piped into `Rscript -` unless encoding has been verified; BOM and `$` expansion can corrupt embedded code.
- In inline PowerShell commands, avoid R/Python code that contains unescaped `$`. Prefer R `df[['Gene']]` over `df$Gene`.
- Use `apply_patch` for manual file edits. Do not use shell redirection, `cat`, or here-string writes to create or edit project files.
- When generating a script or text artifact that would be too large or fragile to produce in one edit, split it into ordered small files or logical script modules first, then combine or source them through a deterministic assembly step. Create each part with normal edit tooling, keep part names ordered, add a short manifest when helpful, and validate the final artifact with parse checks, row/line counts, hashes, or a dry run. Do not emit one huge here-string or redirection write for a large script.
- Do not build destructive file operations with string-concatenated shell commands. Resolve paths and use native PowerShell cmdlets.
- Keep PowerShell object construction simple: compute conditional values first, then create `[pscustomobject]`.
- Do not pipe directly from a `foreach (...) { ... }` language statement. Assign loop output to `$rows`, then pipe `$rows`.
- Do not assume newer .NET APIs are present in Windows PowerShell. In particular, `[System.IO.Path]::GetRelativePath()` may be unavailable; for manifest/QC relative paths, compute a normalized root prefix and use `Substring()` after checking `StartsWith()`, or delegate path normalization to R/Python.
- Do not assume newer PowerShell cmdlet parameters are present. For example, some Windows PowerShell hosts do not support `Format-Hex -Count`; use `Format-Hex -LiteralPath <path> | Select-Object -First <n>` when only a short byte preview is needed.
- Keep R scripts as UTF-8 without BOM. Windows `Set-Content -Encoding UTF8` can write a BOM in older PowerShell, and some `Rscript` sessions may fail with `unexpected invalid token` at byte 1. Use `[System.IO.File]::WriteAllText($path, $text, (New-Object System.Text.UTF8Encoding($false)))` when converting a script that R must source.
- Before using `git diff`, `git status`, or path-limited Git comparisons as a QC shortcut, verify the current directory is inside a Git work tree with `git rev-parse --is-inside-work-tree`. If it is not a Git repository, do not treat the Git error as evidence about the files; use file inventories, hashes, timestamps, or targeted content searches instead.
- When combining one scalar path with an array of paths for `-LiteralPath`, do not write `@($src + $targets)`: Windows PowerShell may concatenate the scalar and array into one invalid path string. Use `$allPaths = @($src) + $targets`, then pass `-LiteralPath $allPaths`.
- Remember that PowerShell `-replace` uses regular expressions. For path separator normalization, do not write `-replace '\'`, which is an invalid regex; prefer `$rel = $rel.Replace('\','/')`, or use `-replace '\\','/'` only when regex escaping has been checked.
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
