# R And Python Commands From PowerShell

Use this reference when invoking Rscript or Python from PowerShell, especially with paths containing spaces, inline code, CSV/RDS reads, or stdin.

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

Use a real `.R` script, not an inline command, when the R code contains any of:

- `data.table` filters with `&` or `|`;
- `$` column access, formula terms, or nested list access that may be expanded by PowerShell;
- multi-line functions, loops, or grouped summaries;
- code long enough that command-line quote escaping becomes hard to inspect.

Safe scratch-check pattern:

```powershell
# 1. Create or update tmp_check.R with apply_patch, keeping it UTF-8 without BOM.
# 2. Run the script directly.
& 'C:/Program Files/R/R-x.y.z/bin/Rscript.exe' --vanilla .\tmp_check.R
# 3. Remove the scratch script with apply_patch when finished.
```

Do not switch to `cmd /c Rscript -e "..."` as a generic escape hatch for complex R snippets. `cmd.exe` treats characters such as `&` as command separators, so expressions like `dt[x == 1 & y == 2]` can be split before R sees them.

Avoid this fragile pattern:

```powershell
@'
df <- read.csv("file.csv")
cat(df$Gene[1])
'@ | Rscript -
```

It may fail from BOM/encoding or `$`/quote interactions depending on how the command is constructed.

## Python Patterns

Use Python for parsing when it avoids shell quoting problems:

```powershell
python -c "import pandas as pd; df=pd.read_csv(r'data/example.csv'); print(df.shape)"
```

For longer Python code, prefer a script file edited with `apply_patch`, or a carefully quoted one-liner. Avoid large here-doc style snippets unless encoding is known to be safe.

## Validation Checklist

Before concluding a command failed because of data or code:

- Check whether PowerShell expanded `$` inside embedded R/Python code.
- Check path quoting, especially `C:/Program Files/...`.
- Check whether stdin or here-string encoding introduced a BOM.
- Re-run as a shorter command or as a real script file.
- Confirm the working directory with `Get-Location` when relative paths fail.
