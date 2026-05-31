---
name: windows-code-execution
description: Use when running or writing commands on Windows, especially PowerShell, Rscript, Python, paths with spaces, quoting, here-strings, CSV/RDS reads, or avoiding failures from shell variable expansion, BOM/encoding, and unsafe file operations.
---

# Windows Code Execution

Use this skill before running non-trivial shell commands in a Windows workspace, especially when invoking R or Python from PowerShell.

## Core Rules

- Prefer short, single-purpose commands. Avoid long one-line programs when a small script file or `Rscript -e` fragments are safer.
- Use `-LiteralPath` for PowerShell filesystem paths when paths may contain spaces, brackets, parentheses, or special characters.
- For Windows paths passed into R/Python code, prefer forward slashes: `C:/path/to/project/file.csv`.
- Do not pipe UTF-8 here-strings into `Rscript -` unless necessary. PowerShell can inject a BOM or encoding that R reads as an invalid token.
- In PowerShell double-quoted strings, `$Gene`, `$x`, `$env`, etc. are expanded before reaching R. Avoid R `$` column access in inline commands; use `df[['Gene']]` instead.
- For inline `Rscript -e`, the most robust pattern in this Codex Windows toolchain is: PowerShell outer double quotes, R string literals in single quotes, and R column access with `[[...]]`.
- Do not use shell redirection or `cat` to create/edit project files when manual edits are needed. Use `apply_patch`.
- Do not build destructive file operations by string concatenation. Use native PowerShell cmdlets with resolved paths and `-LiteralPath`.
- Keep PowerShell object construction simple. Do not embed complex `if/else`, loops, or multi-statement logic directly inside `[pscustomobject]@{...}` or hashtable literals; compute values in variables first, then construct the object. This avoids parser errors such as `An empty pipe element is not allowed`.
- Do not confuse the PowerShell `foreach (...) { ... }` language statement with the `ForEach-Object` pipeline cmdlet. Piping cmdlet output to `ForEach-Object` is valid. The fragile pattern is piping directly from a completed `foreach (...) { ... }` statement or other multi-line script block into another command. Assign the loop output to a variable first, then pipe the variable. This avoids parser behavior such as `An empty pipe element is not allowed`.
- When a command fails because of quoting, parsing, path, encoding, shell expansion, or pipeline structure, do not only patch the immediate command. Record the failed pattern, error symptom, safe replacement, and verification step in the relevant skill so the same failure is not repeated.
- If a script cannot reasonably run on the current Windows machine because of memory, CPU, disk, wall-time, package, or local-environment limits, treat it as an execution-environment constraint, not as evidence against the analysis. Create a portable server-run script instead of weakening the scientific endpoint.

## Rscript Patterns

Find and call the local R explicitly when known:

```powershell
& 'C:/Program Files/R/R-x.y.z/bin/Rscript.exe' --version
```

Safe short R command from PowerShell:

```powershell
& 'C:/Program Files/R/R-x.y.z/bin/Rscript.exe' -e "df <- read.csv('data/example.csv', check.names=FALSE); cat(nrow(df), length(unique(df[['Gene']])), '\n')"
```

If a command host preserves PowerShell single quotes exactly, this can also work, but verify before relying on it:

```powershell
& 'C:/Program Files/R/R-x.y.z/bin/Rscript.exe' -e 'df <- read.csv("file.csv", check.names=FALSE); print(df[["Gene"]][1:5])'
```

For longer R code, prefer creating or updating an `.R` script with `apply_patch`, then run:

```powershell
& 'C:/Program Files/R/R-x.y.z/bin/Rscript.exe' .\path\to\script.R
```

Avoid this fragile pattern:

```powershell
@'
df <- read.csv("file.csv")
cat(df$Gene[1])
'@ | Rscript -
```

It may fail from BOM/encoding or `$`/quote interactions depending on how the command is constructed.

## Server-Run Script Pattern

When local Windows hardware or environment limits prevent a full analysis from running, prepare a server-run script that the user can edit and run directly on a larger machine. Do this when the analysis is still scientifically needed and the blocker is compute, memory, disk, wall-time, package availability, or operating-system limits.

Do not silently downsample, reduce model scope, change thresholds, or switch to a weaker endpoint just to make the task finish locally unless the user explicitly asks for that exploratory shortcut.

For server-run scripts:

- put all user-editable paths and major parameters at the top of the script;
- use generic placeholders such as `/path/to/input` and `/path/to/output`, not local private paths;
- define `input_dir`, `output_dir`, key input file names, thread counts, memory-sensitive parameters, seeds, and overwrite behavior in one configuration block;
- create output directories with recursive creation;
- validate required input files before heavy computation starts;
- write logs, session information, package versions, parameters, and expected output paths;
- keep the script runnable by a single command such as `Rscript script_name.R` or `python script_name.py`;
- avoid interactive prompts, GUI dependencies, and machine-specific absolute paths;
- include comments telling the user which variables should be edited and which should usually remain unchanged.

R template:

```r
## ---- User-editable paths and parameters ----
input_dir <- "/path/to/input"
output_dir <- "/path/to/output"
input_rds <- file.path(input_dir, "analysis_input.rds")
threads <- 8
seed <- 1
overwrite <- FALSE

## ---- Setup ----
dir.create(output_dir, recursive = TRUE, showWarnings = FALSE)
stopifnot(file.exists(input_rds))
set.seed(seed)

log_file <- file.path(output_dir, "run_log.txt")
sink(log_file, split = TRUE)
cat("Started:", format(Sys.time()), "\n")
cat("Input:", input_rds, "\n")
cat("Output:", output_dir, "\n")

## ---- Analysis ----
obj <- readRDS(input_rds)
## Run the heavy analysis here.

## ---- Save outputs and environment ----
saveRDS(obj, file.path(output_dir, "analysis_result.rds"))
writeLines(capture.output(sessionInfo()), file.path(output_dir, "sessionInfo.txt"))
cat("Finished:", format(Sys.time()), "\n")
sink()
```

If generating a script for Linux/HPC from a Windows workspace, use POSIX-style placeholders inside the server script and provide a separate Windows command only for local syntax checking when needed.

## PowerShell Reading Patterns

List files:

```powershell
Get-ChildItem -LiteralPath data\module_resources -Recurse -File
```

Read first lines:

```powershell
Get-Content -LiteralPath data\module_resources\README.md -TotalCount 80
```

Search files:

```powershell
rg -n "pattern|Gene" data\example_dir
```

Count lines and read header without fragile pipelines:

```powershell
$f = 'data\example.csv'
$header = Get-Content -LiteralPath $f -TotalCount 1
$lines = (Get-Content -LiteralPath $f | Measure-Object -Line).Lines
[pscustomobject]@{ File = $f; Lines = $lines; Header = $header }
```

Build objects after computing conditional fields:

```powershell
foreach ($p in @('data', 'results')) {
  $exists = Test-Path -LiteralPath $p
  if ($exists) {
    $item = Get-Item -LiteralPath $p
    $kind = if ($item.PSIsContainer) { 'Directory' } else { 'File' }
  } else {
    $kind = 'Missing'
  }

  [pscustomobject]@{
    Path = $p
    Exists = $exists
    Kind = $kind
  }
}
```

Piping cmdlet output into `ForEach-Object` is a normal PowerShell pipeline and is acceptable:

```powershell
Select-String -LiteralPath $files -Pattern 'fit-for-purpose' |
  ForEach-Object {
    "{0}:{1}: {2}" -f $_.Path, $_.LineNumber, $_.Line
  }
```

Avoid piping directly from a `foreach` language statement:

```powershell
# Fragile: parser behavior differs across hosts and often fails.
foreach ($f in $files) {
  [pscustomobject]@{ File = $f; Exists = Test-Path -LiteralPath $f }
} | Format-Table -AutoSize
```

Use a collected variable, then pipe the variable:

```powershell
$rows = foreach ($f in $files) {
  $exists = Test-Path -LiteralPath $f
  [pscustomobject]@{
    File = $f
    Exists = $exists
  }
}

$rows | Format-Table -AutoSize
```

For hash or QC checks, keep validation separate from display:

```powershell
$rows = foreach ($f in $files) {
  $path = Join-Path $root $f
  if (!(Test-Path -LiteralPath $path)) {
    throw "Missing file: $path"
  }

  $hash = (Get-FileHash -Algorithm SHA256 -LiteralPath $path).Hash
  [pscustomobject]@{
    File = $f
    Hash = $hash
  }
}

$rows | Sort-Object File | Format-Table -AutoSize
```

## Failure-To-Rule Update Pattern

When a Windows command fails and is repaired during a task, update the relevant skill if the failure is reusable. Record:

- the fragile pattern, such as `foreach (...) { ... } | Format-Table`, and distinguish it from valid cmdlet pipelines such as `Select-String ... | ForEach-Object { ... }`;
- the observed symptom or error message, such as `An empty pipe element is not allowed`;
- the safe replacement pattern;
- the validation command that proves the replacement works.

Use the most general appropriate skill. Put PowerShell, path, encoding, quoting, and command-structure lessons here. Put workflow-specific lessons, such as skill synchronization or publication packaging checks, in that workflow's skill.

## Python Patterns

Use Python for parsing when it avoids shell quoting problems:

```powershell
python -c "import pandas as pd; df=pd.read_csv(r'data/example.csv'); print(df.shape)"
```

For longer Python code, prefer a script file edited with `apply_patch`, or a carefully quoted one-liner. Avoid large here-doc style snippets unless encoding is known to be safe.

## Validation Checklist

Before concluding a command failed because of data/code:

- Check whether PowerShell expanded `$` inside the embedded R/Python code.
- Check path quoting, especially `C:/Program Files/...`.
- Check whether stdin or here-string encoding introduced a BOM.
- Re-run as a shorter command or as a real script file.
- Confirm the working directory with `Get-Location` when relative paths fail.
