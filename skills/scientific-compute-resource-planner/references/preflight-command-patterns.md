# Preflight Command Patterns

Use these commands as inputs for resource-aware parameter choices. Prefer native commands on the target machine.

## Linux Server

```bash
date
hostname
nproc
free -h
df -h .
uptime
ps -eo pid,user,comm,%cpu,%mem,rss,vsz --sort=-rss | head -20
dmesg -T | tail -50 | grep -i -E "killed process|out of memory|oom" || true
```

For R:

```bash
Rscript -e 'sessionInfo()'
Rscript -e 'pkgs <- c("data.table","Matrix","future","future.apply","BiocParallel"); print(sapply(pkgs, requireNamespace, quietly=TRUE))'
```

## Windows PowerShell

```powershell
Get-Date
$env:COMPUTERNAME
Get-CimInstance Win32_Processor | Select-Object NumberOfCores,NumberOfLogicalProcessors,Name
Get-CimInstance Win32_OperatingSystem | Select-Object TotalVisibleMemorySize,FreePhysicalMemory
Get-PSDrive -PSProvider FileSystem
Get-Process | Sort-Object WorkingSet64 -Descending | Select-Object -First 20 Id,ProcessName,CPU,WorkingSet64
```

## Reporting Template

Record:

```text
Resource snapshot:
- CPU:
- Load:
- Memory available:
- Disk free:
- Largest competing processes:
- Packages:

Chosen parameters:
- workers:
- chunks:
- random/permutation count:
- cell/sample/FOV caps:
- seed:
- progress interval:

Rationale:
- What resource is limiting:
- What margin is left:
- What output confirms progress:
```
