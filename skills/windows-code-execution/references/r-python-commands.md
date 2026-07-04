# R And Python Commands From PowerShell

Use this reference when invoking Rscript or Python from PowerShell, especially with paths containing spaces, inline code, CSV/RDS reads, document text extraction, non-ASCII filenames, or stdin.

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

## Non-ASCII Filenames And DOCX Text

When reading document content or paths that may contain Chinese or other non-ASCII text, make UTF-8 handling explicit before printing from Python:

```powershell
$env:PYTHONIOENCODING = 'utf-8'
[Console]::OutputEncoding = [System.Text.UTF8Encoding]::new()
```

Prefer discovering paths inside Python instead of embedding non-ASCII filenames in the PowerShell command. This avoids command transport or console-codepage corruption:

```powershell
python -c "from pathlib import Path; docs=list(Path('docs').glob('*.docx')); print(len(docs)); print(docs[0].as_posix())"
```

For a lightweight DOCX text sanity check without relying on Word automation or PowerShell display, read `word/document.xml` directly from the OOXML package:

```powershell
python -c "from pathlib import Path; import zipfile, xml.etree.ElementTree as ET; p=list(Path('docs').glob('*.docx'))[0]; root=ET.fromstring(zipfile.ZipFile(p).read('word/document.xml')); ns='{http://schemas.openxmlformats.org/wordprocessingml/2006/main}'; paras=[]; [paras.append(''.join(t.text or '' for t in para.iter(ns+'t')).strip()) for para in root.iter(ns+'p')]; paras=[x for x in paras if x]; print(p.as_posix()); print(len(paras)); print(paras[0][:120])"
```

Use a real Python script for chapter-scale extraction, tables, comments, equations, or repeated workflows. Direct OOXML paragraph counts can differ from `python-docx` or custom extractors because runs, empty paragraphs, tables, text boxes, comments, and fields may be handled differently; treat count differences as extraction-rule differences until specific content is missing.

Do not treat mojibake in `Get-Content` or the PowerShell console as proof that the file is damaged. Verify Markdown/text files with Python `Path(...).read_text(encoding='utf-8')`, and check for replacement characters when corruption is suspected.

## Validation Checklist

Before concluding a command failed because of data or code:

- Check whether PowerShell expanded `$` inside embedded R/Python code.
- Check path quoting, especially `C:/Program Files/...`.
- Check whether stdin or here-string encoding introduced a BOM.
- Check whether console display, rather than file bytes, caused non-ASCII mojibake; re-read with Python UTF-8 before repairing files.
- Re-run as a shorter command or as a real script file.
- Confirm the working directory with `Get-Location` when relative paths fail.

## R Script Encoding Repair

If `Rscript` fails at byte 1 with `unexpected invalid token`, suspect a BOM or encoding rewrite before blaming the script logic. Validate with:

```powershell
& 'C:/Program Files/R/R-x.y.z/bin/Rscript.exe' --vanilla -e "tryCatch({parse(file='C:/path/to/script.R'); cat('parse_ok\n')}, error=function(e){cat(conditionMessage(e), '\n'); quit(status=1)})"
```

Do not repair a project R script that contains non-ASCII or mojibake text by doing ad hoc line replacement with `Set-Content -Encoding UTF8`; it can preserve or introduce invalid string tokens. Prefer `apply_patch` to rewrite the affected block or, when the text block is already corrupted, rewrite the script section in ASCII and then rerun the parse check above.
