---
name: publication-plot-styler
description: Create or repair publication-ready scientific plots from R/ggplot2/ComplexHeatmap/pheatmap outputs. Use when Codex needs to generate manuscript figures, improve plot aesthetics, fix legends, labels, axis alignment, heatmap cell sizing, UMAP labels, dotplots, barplots, Sankey/alluvial plots, compact whitespace, or export PDF/PNG/TIFF figures for a journal-style manuscript.
---

# Publication Plot Styler

## Core Rules

Use English text in manuscript-facing figures. Make labels readable at final size, keep legends outside dense data, and choose dimensions from the data structure rather than fixed defaults.

For detailed plot-type rules, read `references/plot-style-rules.md`.
For reusable R examples by plot type, read only the relevant section of `references/plot-type-r-examples.md`.

Separate project-specific biological choices from reusable styling rules. Do not copy dataset names, module IDs, or manuscript conclusions into this skill; keep them in project docs or a project navigator skill.

Use this skill for single-panel or standalone panel styling. Use `paper-figure-assembler` when the task is final multi-panel layout, object-based assembly, canvas geometry, or export of an assembled figure. Use manuscript or domain guardrail skills for claims, captions, and biological interpretation.

Before styling or rewriting plotting code, define the figure contract:

- core conclusion the plot must support;
- evidence role: discovery, validation, comparator, mechanism, robustness, or limitation;
- plotted quantity and its biological or statistical meaning;
- required controls, nulls, or baselines;
- source data needed and whether the plotted values are traceable to a table or script output;
- statistics needed: sample size or cell count definition, center/spread or interval, test, correction, threshold, and source-data file when applicable;
- final export formats and physical size;
- likely reviewer misreadings that labels, legends, or captions must prevent.

If the plot cannot support the stated conclusion, say so before polishing aesthetics.

## R Plotting Defaults

- Source the project style file when available: `src/00_publication_plot_style.R`.
- Use `publication_theme()` for ggplot outputs unless the script documents a better local reason.
- Export manuscript-facing plots as PDF, PNG, and TIFF by default unless the project explicitly uses a different submission standard. Use PDF for vector review, PNG for quick inspection, and TIFF for journal/submission workflows.
- Use lossless TIFF compression such as LZW when available. For final assembled figures, prefer 600 dpi TIFF; for source/candidate panels, 300-450 dpi is usually acceptable unless the project specifies otherwise.
- Use right-side legends by default for ggplot and heatmaps unless the assembled layout requires a different placement.
- Keep ggplot titles centered, but remove titles when a panel is assembled into a multi-panel figure and the caption carries the interpretation.
- Keep x-axis labels centered on ticks. If labels rotate, set `hjust` and margins deliberately.
- Keep axis titles outside the plotting area with enough margin.
- Keep R as the exclusive plotting backend when the project is R-first or the user chose R. Use Python only for non-visual inspection or file conversion unless the user explicitly changes the plotting backend.
- Install routine plotting dependencies when the environment allows it rather than reimplementing mature plotting, image, spatial, or statistical functionality from scratch.

## Heatmap Rules

- Use `ComplexHeatmap` for formal manuscript heatmaps; use `pheatmap` only for simpler internal views.
- Use diverging palettes only for signed statistics, centered at the meaningful null.
- Label signed percentage differences as percentage-point differences.
- If negative values are possible, state what negative/blue means in the legend or caption.
- Set `column_names_centered = TRUE` when available.
- Related heatmaps in the same figure should have comparable cell/body sizes.
- For small matrix heatmaps, keep heatmap cells square by explicitly setting equal body cell width and height; do not let the export canvas stretch cells into wide or tall rectangles.

## Dense Labels

For UMAP or dense scatter labels, use `ggrepel::geom_text_repel()` with text-only labels. Do not use `geom_label_repel()` or any filled label box over expression signal.

## Output Check

Before declaring a figure ready:

- Open the PNG preview.
- Check that text is readable, legends are not clipped, and labels do not overlap data.
- Confirm x/y labels do not intrude into the panel.
- Confirm heatmap labels sit over cell centers.
- Confirm all legends and colorbars correspond to visible encodings.
- Confirm legends are compact enough to avoid wasting panel area but not so tight that symbols and labels overlap.
- Confirm the plot is not sparse, cramped, or dominated by empty margins; revise dimensions or legend placement before final export.
- Confirm any problem observed in a final assembled figure is fixed at the source panel or internal subplot layout level, not by raster stretching or manual cropping.
- Confirm the legend explains whether a color scale is sequential, diverging, signed, normalized, percentile-based, clipped, or raw.
- Confirm high-overlap comparator visuals make the intended contrast explicit, such as compact feature use, decomposition, resolution, or matched localization, rather than leaving readers to infer the added value.
- Confirm quantitative panels have enough information in the plot, legend, or paired source table to recover the sample size/cell count definition, statistic, threshold, test, and multiple-comparison correction when relevant.
