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
