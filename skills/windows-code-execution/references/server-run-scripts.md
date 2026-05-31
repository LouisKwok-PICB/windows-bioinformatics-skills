# Portable Server-Run Scripts

Use this reference when local Windows hardware or environment limits prevent a full analysis from running, but the analysis is still scientifically required.

Do not silently downsample, reduce model scope, change thresholds, or switch to a weaker endpoint just to make the task finish locally unless the user explicitly asks for that exploratory shortcut.

## Required Properties

- Put user-editable paths and major parameters at the top of the script.
- Use generic placeholders such as `/path/to/input` and `/path/to/output`, not local private paths.
- Define `input_dir`, `output_dir`, key input file names, thread counts, memory-sensitive parameters, seeds, and overwrite behavior in one configuration block.
- Create output directories recursively.
- Validate required input files before heavy computation starts.
- Write logs, session information, package versions, parameters, and expected output paths.
- Keep the script runnable by a single command such as `Rscript script_name.R` or `python script_name.py`.
- Avoid interactive prompts, GUI dependencies, and machine-specific absolute paths.
- Include comments telling the user which variables should be edited and which should usually remain unchanged.

## R Template

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
