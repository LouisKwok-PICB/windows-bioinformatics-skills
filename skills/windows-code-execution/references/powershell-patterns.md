# PowerShell Filesystem And Pipeline Patterns

Use this reference for Windows filesystem reads, path handling, object construction, hash/QC checks, and fragile pipeline syntax.

## Filesystem Basics

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

Create directories with `New-Item -Path`; some hosts do not support `New-Item -LiteralPath`:

```powershell
New-Item -ItemType Directory -Force -Path 'results/figure4/tables' | Out-Null
```

Use `-LiteralPath` for existing paths when reading, copying, moving, removing, hashing, or opening files.

## Safe Object Construction

Count lines and read a header without fragile pipelines:

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

## Pipeline Rules

Piping cmdlet output into `ForEach-Object` is normal and acceptable:

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

Use the most general appropriate skill. Put PowerShell, path, encoding, quoting, and command-structure lessons in `windows-code-execution`. Put workflow-specific lessons, such as skill synchronization or publication packaging checks, in that workflow's skill.
