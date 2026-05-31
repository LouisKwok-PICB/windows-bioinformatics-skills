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
