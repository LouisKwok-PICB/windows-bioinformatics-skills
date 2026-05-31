# Multi-Panel Layout Design

Use this reference when designing a manuscript main figure or supplementary figure. The goal is to maximize readable evidence per page without making panels cramped or visually sparse.

## Quick Navigation

- Start with figure logic: `Design Principles`
- Choose physical dimensions: `Canvas Size Heuristics`, `PLOS Readability Gate`
- Allocate panel area: `Area Allocation Rules`, `Layout Skeleton`
- Handle repeated embeddings: `Equal-Viewport Multi-UMAP Panel`
- Final visual checks: `Whitespace QC Checklist`

## Design Principles

- Start from the evidence chain, not from a grid. Panel order should match the reader's reasoning path.
- Write a one-line role for each panel before assigning space. If a panel has no unique inferential role, merge it, move it to supplementary material, or remove it.
- Allocate area by information density:
  - heatmaps: enough body height for cells plus label/legend room;
  - UMAP/dense scatter: square or nearly square bodies;
  - dotplots: width for x-scale, height for categories;
  - text or bar summaries: smaller unless they carry the main claim.
- Remove redundant standalone titles inside assembled figures; use panel letters and a figure legend.
- Legends must be close enough to their panels to be unambiguous, but outside the data body.
- Prefer fewer panels with readable details over many tiny panels.
- Store dataset-specific panel choices in the project repository, not in this reusable layout reference.

## Canvas Size Heuristics

Use millimeters in R scripts.

- PLOS journal maximum figure size:
  - maximum width `190.5 mm` (`7.5 in`);
  - maximum height `222.3 mm` (`8.75 in`);
  - at 300 dpi this corresponds to `2250 x 2625 px`.
  Design PLOS main figures to fit within this box before manuscript review; do not export an oversized tall figure and assume down-scaling will remain readable.
- Single-column figure: `width_mm = 89`.
- 1.5-column figure: `width_mm = 140-160`.
- Double-column figure: `width_mm = 183`.
- Extended multi-panel main figure: `width_mm = 210-240` only when journal format permits or when the output is a non-PLOS supplementary/diagnostic draft. For PLOS, split or redesign instead of exceeding `190.5 x 222.3 mm`.
- Typical row gaps: `1.5-4 mm`.
- Outer margins: `3-6 mm`.
- Panel label reserve: `4.5-6 mm`.
- Panel internal padding: `0.6-1.2 mm`.

If final PNG preview looks sparse, shrink the canvas or panel. If details are readable only when zoomed in, increase canvas height/width or reduce displayed categories.

## PLOS Readability Gate

Before declaring a PLOS figure ready:

1. Confirm the assembled canvas is no larger than `190.5 mm x 222.3 mm`.
2. Confirm manuscript-facing text remains effectively `8-12 pt` after final placement or publisher scaling. If using smaller internal labels for dense panels, verify the PNG/PDF at final physical size rather than judging a zoomed preview.
3. If a figure exceeds the PLOS height limit, do not simply downscale it. Reallocate panels into a wider two-column layout, simplify panel content, move secondary evidence to supplementary figures, or split the figure.
4. Audit every nested multi-subplot panel at the same final size. A figure can pass the outer canvas check while still failing because one nested panel has tiny axes, overlapped labels, or unequal subplot bodies.
5. Record the final width, height, dpi, panel map, and any nested-panel compaction decisions in a manifest.
6. Confirm supplementary figures follow the same readability rules; do not let supplements become a dumping ground for unreadable dense panels.

## Area Allocation Rules

1. Estimate each panel's natural aspect ratio.
   - UMAP: 1:1 body, plus legend/title space.
   - Heatmap: `width/height ~= n_columns/n_rows` after label constraints, but do not let one-cell dimensions become too large.
   - Dotplot with many y labels: taller; with many x categories: wider.
   - Bar chart with long y labels: wider left text margin.

2. Decide whether legends are shared or panel-local.
   - Shared legends save space when encodings are identical.
   - Panel-local legends avoid ambiguity when scales differ.
   - For paired UMAPs, use bottom horizontal colorbars and a separate binary highlight key when the right side would make plot bodies unequal.
   - If a panel contains two different embeddings or coordinate systems, do not share axes or global coordinate limits across them. Share limits only within views of the same embedding, and state this in the figure legend when needed.

3. Set deterministic panel rectangles.
   - Define `x`, `y`, `w`, and `h` in millimeters.
   - Avoid relying on patchwork to infer a dense journal layout.

4. Check visual density.
   - Too sparse: large empty margins, tiny data body, oversized legend, or panel with few marks occupying a large row.
   - Too crowded: labels overlap, legends clip, heatmap cells too small, or subplot titles consume body area.

5. Redesign nested panels before shrinking the whole figure.
   - If a panel contains internal subplots, do not treat it as an immutable image-sized box.
   - Change the panel's internal row/column arrangement, shared legends, axis removal, label wrapping, or summary granularity so each subplot remains readable at the final journal page size.
   - For multi-UMAP or multi-dotplot panels, equalize the data-body viewport sizes inside the panel; do not let a legend-bearing subplot become smaller than its neighbors.
   - For multi-UMAP panels, preserve the semantics of axes. If subplots are from separate embeddings, keep axis names on each subplot and use embedding-specific limits; hiding y-axis labels in later columns can be misleading even when it looks cleaner.
   - For supplementary multi-UMAP atlases, use axis-line-only plots with visible axis names and no numeric tick labels when coordinates are qualitative. Avoid grey square borders unless they encode a grouping structure.
   - If an internal subplot cannot remain readable inside the PLOS page limit, replace the main-panel version with a compact summary and move the full detailed display to supplementary figures.

## Layout Skeleton

```r
figure_layout_dimensions <- function() {
  width_mm <- 230
  margin <- 4
  gap <- 2
  inner_w <- width_mm - 2 * margin

  left_w <- 112
  right_w <- inner_w - left_w - gap

  hA <- 84   # wide heatmap or opening landscape
  hB <- 82   # dense UMAP row with bottom legends
  hCD <- 86  # two-column analytical row
  hE <- 70   # full-width comparator row
  hF <- 68   # organization/summary row

  height_mm <- 2 * margin + hA + hB + hCD + hE + hF + 4 * gap

  yF <- margin
  yE <- yF + hF + gap
  yCD <- yE + hE + gap
  yB <- yCD + hCD + gap
  yA <- yB + hB + gap

  list(
    canvas = c(width_mm = width_mm, height_mm = height_mm),
    panels = list(
      A = c(x = margin, y = yA, w = inner_w, h = hA),
      B = c(x = margin, y = yB, w = inner_w, h = hB),
      C = c(x = margin, y = yCD, w = left_w, h = hCD),
      D = c(x = margin + left_w + gap, y = yCD, w = right_w, h = hCD),
      E = c(x = margin, y = yE, w = inner_w, h = hE),
      F = c(x = margin, y = yF, w = inner_w, h = hF)
    )
  )
}
```

Adjust the example dimensions to the actual panel count and journal limit. Keep dimensions documented in a manifest.

## Equal-Viewport Multi-UMAP Panel

Use a custom grid draw function when patchwork creates unequal plot bodies because some subplots have legends.

```r
umap_limits_from_plots <- function(plots) {
  x <- unlist(lapply(plots, function(p) p$data$umap_1), use.names = FALSE)
  y <- unlist(lapply(plots, function(p) p$data$umap_2), use.names = FALSE)
  lim <- range(c(x, y), na.rm = TRUE)
  pad <- diff(lim) * 0.035
  c(lim[1] - pad, lim[2] + pad)
}

harmonize_umap <- function(p, lim) {
  p +
    coord_equal(xlim = lim, ylim = lim, expand = FALSE, clip = "off") +
    theme(axis.text = element_blank(), axis.ticks = element_blank(), legend.position = "none")
}

draw_horizontal_colorbar <- function(title, limits, x, y, w, h, high = "#B24A3A") {
  n <- 96
  ramp <- grDevices::colorRampPalette(c("#F2F0EA", high))(n)
  bar_x0 <- 0.14
  bar_w <- 0.72
  pushViewport(viewport(x = unit(x, "npc"), y = unit(y, "npc"),
                        width = unit(w, "npc"), height = unit(h, "npc"),
                        just = c("left", "bottom"), clip = "off"))
  grid.text(title, x = unit(bar_x0 + bar_w / 2, "npc"), y = unit(0.96, "npc"),
            just = c("center", "top"), gp = gpar(fontsize = 7, col = "#30343B"))
  for (i in seq_len(n)) {
    grid.rect(x = unit(bar_x0 + (i - 0.5) * bar_w / n, "npc"),
              y = unit(0.42, "npc"), width = unit(bar_w / n, "npc"),
              height = unit(0.24, "npc"), gp = gpar(fill = ramp[i], col = NA))
  }
  tick_vals <- c(limits[1], mean(limits), limits[2])
  tick_x <- bar_x0 + c(0, 0.5, 1) * bar_w
  grid.text(sprintf("%.1f", tick_vals), x = unit(tick_x, "npc"), y = unit(0.04, "npc"),
            just = c("center", "bottom"), gp = gpar(fontsize = 5.8, col = "#30343B"))
  popViewport()
}

draw_highlight_key <- function(title = "High-tail cells", x, y, w, h) {
  pushViewport(viewport(x = unit(x, "npc"), y = unit(y, "npc"),
                        width = unit(w, "npc"), height = unit(h, "npc"),
                        just = c("left", "bottom"), clip = "off"))
  grid.text(title, x = unit(0.5, "npc"), y = unit(0.96, "npc"),
            just = c("center", "top"), gp = gpar(fontsize = 7, col = "#30343B"))
  grid.points(x = unit(c(0.13, 0.13), "npc"), y = unit(c(0.46, 0.21), "npc"),
              pch = c(17, 16), size = unit(c(1.55, 1.15), "mm"),
              gp = gpar(col = c("#2C6DB2", "#D3D7DB")))
  grid.text(c("Global top 5%", "Other cells"), x = unit(0.27, "npc"),
            y = unit(c(0.46, 0.21), "npc"), just = c("left", "center"),
            gp = gpar(fontsize = 6.2, col = "#30343B"))
  popViewport()
}

make_equal_umap_panel <- function(plots, score_limits_left, score_limits_right) {
  lim <- umap_limits_from_plots(plots)
  plots <- lapply(plots, harmonize_umap, lim = lim)
  function() {
    pushViewport(viewport(layout = grid.layout(
      nrow = 2, ncol = 4,
      heights = unit.c(unit(1, "null"), unit(13, "mm")),
      widths = unit(rep(1, 4), "null")
    )))
    for (i in seq_along(plots)) {
      pushViewport(viewport(layout.pos.row = 1, layout.pos.col = i, clip = "off"))
      print(plots[[i]], newpage = FALSE)
      popViewport()
    }
    pushViewport(viewport(layout.pos.row = 2, layout.pos.col = 1:2, clip = "off"))
    draw_horizontal_colorbar("Left score", score_limits_left, 0.02, 0.07, 0.56, 0.86)
    draw_highlight_key(x = 0.63, y = 0.08, w = 0.34, h = 0.82)
    popViewport()
    pushViewport(viewport(layout.pos.row = 2, layout.pos.col = 3:4, clip = "off"))
    draw_horizontal_colorbar("Right score", score_limits_right, 0.02, 0.07, 0.56, 0.86)
    draw_highlight_key(x = 0.63, y = 0.08, w = 0.34, h = 0.82)
    popViewport(2)
  }
}
```

If the left and right plot pairs are different embeddings, compute `lim` separately for each pair:

```r
make_equal_umap_panel_two_embeddings <- function(left_plots, right_plots,
                                                 score_limits_left, score_limits_right) {
  left_lim <- umap_limits_from_plots(left_plots)
  right_lim <- umap_limits_from_plots(right_plots)
  plots <- c(
    lapply(left_plots, harmonize_umap, lim = left_lim),
    lapply(right_plots, harmonize_umap, lim = right_lim)
  )
  # Draw each plot in equal viewports, keeping axis titles visible on every
  # subplot because the two embedding pairs do not share one coordinate system.
}
```

## Whitespace QC Checklist

- Does each panel's data body occupy most of its allocated area?
- Are legends smaller than the data body but still readable?
- Are paired panels aligned by plot-body size, not just outer panel size?
- Are titles removed when the figure legend already explains the panel?
- Are heatmap cells or UMAP points distorted by forced raster resizing? If yes, switch back to live object drawing.
- Does the assembled PNG remain readable without zooming beyond normal manuscript review size?
- Do standalone panels exported from the same objects match the assembled panel content and numbering?
