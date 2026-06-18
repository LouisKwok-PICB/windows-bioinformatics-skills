# Plot Style Rules

Use these rules when the task involves single-panel plotting or standalone figure panels.

## General

- All plot text must be English.
- Keep project-specific biological claims, dataset names, and module IDs out of reusable style rules.
- Prefer sentence case for titles and axis labels.
- Use concise, literal legend titles.
- Use reader-facing terms in the image. Replace internal workflow labels such as `endpoint`, `gate`, `manifest`, `QC`, `source table`, `blocked`, `pass/fail`, `bridge`, or project shorthand with biological/statistical labels that a manuscript reader can understand. Keep technical definitions, matching rules, thresholds, and p-value details in the legend, Methods, or source data.
- Every visible element must earn its space: remove redundant titles in assembled figures, reduce unused margins, and move detailed explanations to the caption when the graphic is already dense.
- In main figures, a plot should answer a specific question in the evidence chain. If two plots answer the same question, merge them, move one to supplementary material, or replace one with a source table.
- The figure should make the statistical or biological contrast readable at first glance; style choices serve evidence clarity, not decoration.
- Before final styling, write a compact figure contract: core conclusion, evidence role, plotted quantity, controls or nulls, source data, statistics needed, final size, and likely reviewer misreadings.
- Choose the display grammar from the evidence role, not from the easiest table to plot:
  - spatial observable: tissue-coordinate map, ROI/context map, or spatial score map;
  - biological anchor: marker/pathway/gene-set heatmap, dotplot, or expression/score map;
  - matched statistical support: observed-vs-null interval, calibrated distribution, or compact benchmark axis;
  - comparator boundary: paired same-endpoint display, decomposition/resolution view, or same-scale statistic;
  - robustness: ablation, sensitivity, subset, or marker-removal axis;
  - context-only modality: clearly labeled context map/heatmap/dotplot with limitations left to the legend;
  - blocked, QC, coverage, manifest, file availability, or source-data status: source table or Methods text, not a result figure.
- Avoid decorative backgrounds, shadows, excessive gridlines, and rainbow palettes.
- Use color-blind-safe palettes and avoid red-green as the only distinction.
- Prefer white backgrounds and near-black text.
- Use standard sans-serif fonts; Arial/Helvetica when available, otherwise `sans`.
- For journals with explicit minimum text-size rules, the journal rule overrides compact-style defaults. For PLOS Computational Biology, keep every retained figure label, axis/tick label, colorbar label, legend/key label, and embedded statistic label within 8-12 pt at final size.

## Manuscript-Result Eligibility

Do not create or preserve a manuscript-facing single panel when the only information shown is:

- a source table rendered as a plot;
- gene set size, file count, row count, or coverage count without a biological/statistical behavior;
- pipeline status, pass/fail gate, manifest completeness, or input/output availability;
- a blocked endpoint or missing-data audit;
- an unexplained internal statistic that cannot be interpreted from axis labels plus the figure legend;
- a plot whose conclusion is only "we ran this analysis" rather than an observed biological or matched statistical result.

If such information is needed for reproducibility, route it to source data, Methods, package QC, or project records. If it is needed scientifically, redesign the panel so it displays the biological behavior or calibrated statistic directly.

## PLOS Computational Biology Figures

- Official source to verify before exact submission export: `https://journals.plos.org/ploscompbiol/s/figures` (checked for these rules on 2026-06-05).
- Use only Arial, Times, or Symbol fonts in manuscript figures. Prefer Arial for scientific plots unless a project style guide says otherwise.
- Keep all text that remains inside the submitted figure at 8-12 pt at the final physical/export size. In R/ggplot, remember that `theme(element_text(size = ...))` uses points, while `geom_text(size = ...)` uses millimeters; use roughly `2.8 mm` for 8 pt geom text.
- Keep figure captions out of the image. Let the manuscript legend carry detailed interpretation, definitions, and nonessential source-data notes.
- For main article figures, stay within the PLOS figure box unless the target journal page says otherwise: about `190.5 mm` wide by `222.3 mm` high, equivalent to `2250 x 2625 px` at 300 dpi.
- Submit TIFF or EPS for final article figures; keep PDF/PNG review copies when useful. Use 300-600 dpi and white backgrounds.
- If 8 pt text does not fit, redesign before shrinking: shorten visible labels, use titled compact legends, place legends outside dense data, split a panel, move detail to supplementary/source tables, or demote low-priority content.
- Check the final-size PNG/PDF visually. Do not judge PLOS text compliance from a zoomed viewer or from standalone panels alone.

## Dimensions

- For PLOS journals, design final figures within the official maximum box: `190.5 mm` wide by `222.3 mm` high (`7.5 x 8.75 in`; `2250 x 2625 px` at 300 dpi). If an assembled figure is taller than this, redesign the layout or move secondary evidence to supplementary material; do not rely on publisher down-scaling.
- PLOS manuscript-facing figure text should remain readable at final size, typically `8-12 pt` for required labels. Internal labels below this range need explicit visual QC at final physical dimensions.
- Judge readability from the final assembled PNG/PDF at the journal physical size, not from a zoomed viewer. If labels are only readable when zoomed, redesign the panel or move detail to supplements/source tables.
- For panels that contain subplots, adjust the internal layout before accepting a cramped assembled figure. Valid adjustments include changing from one row to two rows, sharing legends, moving legends below paired plots, removing redundant axes, wrapping labels, reducing displayed categories, or replacing the main-panel version with a compact summary while keeping full detail in supplementary material.
- Single-column target: about 89 mm.
- Double-column target: about 183 mm.
- Choose width/height from data geometry:
  - more x categories -> wider panel;
  - more y categories -> taller panel;
  - many long labels -> wider margin or shorter visible labels with expanded definitions in caption.
- Avoid very tall/narrow or empty square plots unless data shape requires it.
- If a plot looks sparse, shrink the plotting body or move it into a smaller panel. If it looks cramped, increase panel size or reduce displayed categories before increasing font size.

## ggplot

- Use `publication_theme()`.
- Place legends on the right by default.
- Center titles and subtitles for standalone panels.
- Remove panel titles before final multi-panel assembly unless the title is scientific content.
- When a plot has multiple legends and the panel is wide enough, consider bottom legends arranged as compact rows. Center each legend title above its own keys; do not place a legend title inline with keys unless the target design deliberately uses inline labels.
- For point-size legends, keep symbols large enough to read at final size and make the size title explicit, such as `Expressing cells (%)`, `Cells in state (%)`, or `Median score`.
- For paired or repeated subplots, enforce matching point sizes, stroke widths, alpha, coordinate body size, and legend scales when the visual comparison assumes equality.
- Use axis lines and ticks for statistical plots.
- Keep categorical x tick labels centered (`hjust = 0.5`) when not rotated.
- If a plot is short and wide because of unused x-range or few categories, shrink the panel width, swap axes, or tighten discrete scale expansion. Do not let a low-density statistic occupy a large empty canvas.
- For compact condition/state panels, limit x-axis to data positions and put condition annotations below the axis as a separate lower matrix with short `+/-` encodings.
- Compact repeated legends with `legend.key.height`, `legend.key.width`, `legend.spacing.y`, and explicit `guide_legend(keyheight=..., keywidth=...)`; avoid large default size legends that waste panel area.

## Heatmaps

- Prefer `ComplexHeatmap`.
- Use restrained diverging palettes for signed statistics and sequential palettes for magnitude-only metrics.
- Use palettes whose hue and direction match the manuscript's visual language when a project has one. Do not mix unrelated blue-green, purple, rainbow, and red scales across panels unless each scale encodes a genuinely different data type and the legend makes that clear.
- Use thin white/light borders only if they improve readability.
- Order rows and columns by biological/statistical logic.
- Use short visible labels; define expanded meanings in legends/captions when needed.
- Set `column_names_centered = TRUE` when labels must align with cells.
- Related heatmaps in a figure should have comparable body sizes/cell sizes.
- For small matrix heatmaps, keep heatmap cells square. In `ComplexHeatmap`, set heatmap body `width = ncol(mat) * cell_size` and `height = nrow(mat) * cell_size`; in `ggplot2::geom_tile()`, add `coord_fixed(ratio = 1)` or `theme(aspect.ratio = nrow / ncol)` and choose export dimensions so labels and legends do not distort the tile body. Do not stretch the heatmap body to make long labels fit; shorten or rotate labels and define expanded meanings in the legend or caption.
- Rotate or shorten annotation names when they steal heatmap body height, but keep expanded meanings in legends/captions.
- Barplot annotations should be named by the quantity shown, e.g. `Gene count`; if transformed, state the transform in legend or caption.

## Dotplots

- Keep dot size legends visible and consistent across related dotplots.
- Use explicit titles such as `Expressing cells (%)`, `Module-high cells (%)`, or `Mean module score (z)`.
- Center the dot-size legend title over the size keys. Avoid cramped legends where the largest and smallest dots are visually indistinguishable.
- If color shows a signed difference, use a diverging palette centered at 0 and explain negative values.
- Use a compact dot-size guide. Large vertical gaps between legend circles make journal panels look unfinished.
- If multiple dotplots in the same manuscript encode the same size statistic, use matching size scales, guide titles, and guide spacing.
- If a dotplot uses fill color and point size simultaneously, use filled point shapes such as 21 and keep the outline thin enough that small dots remain visible.
- For enrichment dotplots, choose displayed terms by inferential role, not only by smallest FDR. In main panels, one representative term per module/category is usually enough; in supplementary panels, two terms per module/category can be shown when the panel has enough vertical space and the two terms explain distinct biology.
- When showing multiple terms per module/category, write the displayed-term selection table to the source tables so the figure is traceable and not perceived as hand-picked.

## Bar Charts

- Use horizontal bars for long labels or gene rankings.
- Avoid 3D bars and heavy outlines.
- Annotate key values only if it does not make the plot crowded.

## UMAP / Dense Scatter

- Use small points with moderate alpha for large single-cell plots.
- Use `ggrepel::geom_text_repel()` for cell-type labels.
- Do not use filled label boxes on expression UMAPs.
- Starting label parameters: `size = 2.0-2.3`, `color = "#30343B"`, `fontface = "bold"` when needed, `max.overlaps = Inf`, `segment.size = 0.10-0.16`, fixed `seed`.
- If labels obscure expression signal, reduce label count or size before adding backgrounds.
- For multi-UMAP panels, force identical plot-body sizes. If multiple UMAP coordinate systems are shown side by side, keep axis names visible unless the caption makes the coordinate semantics obvious. Remove numeric ticks when coordinates are not directly interpretable.
- For paired spatial or embedding subplots that compare highlighted subsets, keep the base point size identical unless the difference is itself the encoded variable. Use larger outlines, rings, or local annotations only when they mark an ROI or subset relationship without changing the perceived abundance of the underlying cells/spots.
- Harmonize coordinate limits only among panels that share the same embedding. Do not force unrelated UMAP embeddings into one common coordinate range; it implies a false shared coordinate system.
- Use an axis-line-only style for formal UMAP panels when axes matter: show `UMAP 1` and `UMAP 2`, hide numeric tick labels and tick marks, and avoid full grey square panel borders unless the border encodes grouping.
- Separate continuous score colorbars from binary highlight legends. Use a different marker shape or hue for highlighted cells so the highlight cannot be mistaken for a continuous color scale.
- When legends are shared by a pair of panels, place compact horizontal colorbars under the relevant panels and center the legend title over the encoding.

## Sankey / Alluvial

- Use when the key message is module splitting/convergence.
- Keep side labels short and categorical.
- Aggregate tiny groups when labels collide.
- Hide x-axis ticks/axis lines in publication-facing alluvial panels.
- Put long module labels or shared-count details outside the Sankey body as a compact legend.

## Submission Export

- For journal upload copies, prefer TIFF with white background, RGB or grayscale, LZW compression, and embedded dpi.
- Maintain a manifest recording width, height, dpi, physical size, file size, and whether the file fits the target journal box.
- Generate upload copies from the reproducible figure outputs; avoid manual file copying that can desynchronize manuscript figures and submission files.

## Statistics And Source-Data Minimum

For quantitative manuscript panels, ensure the plot, legend, Methods, or source table records:

- sample size or cell count definition;
- biological versus technical replicate definition when applicable;
- center statistic and spread or interval;
- statistical test and whether it is one-sided or two-sided;
- multiple-comparison correction;
- threshold or quantile definition;
- source-data file and analysis script.

Do not force all of this text into the graphic when it makes the panel unreadable. Use concise legends and source tables, but make the information traceable.

## Single-Panel Visual QC

Before promoting a standalone panel to assembly:

- Confirm the visible title, subtitle, axis labels, legend titles, and facet labels use manuscript-facing terms.
- Confirm no internal workflow labels remain unless explicitly accepted as domain terms.
- Confirm the panel displays biological behavior or matched statistical behavior, not only QC/source/status metadata.
- Confirm legend titles are centered over keys when the legend is not intentionally inline.
- Confirm colorbars use an interpretable direction and a palette consistent with related panels.
- Confirm every color, size, shape, alpha, or outline encoding has a visible legend or is explained by direct labeling.
- Confirm paired subplots have equal data-body dimensions and equal symbol sizes when visual comparison requires that.
- Confirm heatmap cells are square when the matrix is small enough for square cells to be meaningful.
- Confirm x/y scale expansion does not create large unused spaces; swap axes, shrink canvas, or adjust panel width when needed.
- Confirm details that belong in the figure legend or Methods have not been embedded as dense in-image paragraphs.
