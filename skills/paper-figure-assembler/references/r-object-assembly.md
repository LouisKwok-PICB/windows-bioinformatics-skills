# R Object-Based Publication Figure Assembly

Use this reference when writing or repairing an R script that assembles a manuscript figure from live objects.

## Quick Navigation

- Start a new assembly script: `Minimal Template`, `Required Structure`
- Draw heatmaps safely: `ComplexHeatmap Rules`
- Avoid nested tag problems: `Patchwork Rules`
- Record outputs: `Figure Manifest`
- Check final exports: `Visual Checklist`, `Synchronization Checklist`

## Minimal Template

```r
suppressPackageStartupMessages({
  library(ComplexHeatmap)
  library(ggplot2)
  library(grid)
})

mm_to_in <- function(mm) mm / 25.4

draw_object <- function(obj) {
  if (inherits(obj, "Heatmap") || inherits(obj, "HeatmapList")) {
    ComplexHeatmap::draw(
      obj,
      newpage = FALSE,
      heatmap_legend_side = "right",
      annotation_legend_side = "right",
      padding = unit(c(0.8, 0.8, 0.8, 0.8), "mm")
    )
  } else if (inherits(obj, "gtable") || inherits(obj, "grob") || inherits(obj, "gTree")) {
    grid.draw(obj)
  } else if (inherits(obj, "ggplot")) {
    print(obj, newpage = FALSE)
  } else if (is.function(obj)) {
    obj()
  } else {
    stop("Unsupported object type: ", paste(class(obj), collapse = ", "))
  }
}

draw_panel_box <- function(obj, label, x_mm, y_mm, w_mm, h_mm,
                           label_h_mm = 5.2, pad_mm = 0.8) {
  pushViewport(viewport(
    x = unit(x_mm, "mm"),
    y = unit(y_mm, "mm"),
    width = unit(w_mm, "mm"),
    height = unit(h_mm, "mm"),
    just = c("left", "bottom"),
    clip = "off"
  ))
  grid.rect(gp = gpar(fill = "white", col = NA))
  grid.text(
    label,
    x = unit(0.2, "mm"),
    y = unit(h_mm - 0.3, "mm"),
    just = c("left", "top"),
    gp = gpar(fontsize = 11, fontface = "bold", fontfamily = "sans", col = "#30343B")
  )
  pushViewport(viewport(
    x = unit(pad_mm, "mm"),
    y = unit(pad_mm, "mm"),
    width = unit(w_mm - 2 * pad_mm, "mm"),
    height = unit(h_mm - label_h_mm - 2 * pad_mm, "mm"),
    just = c("left", "bottom"),
    clip = "on"
  ))
  draw_object(obj)
  popViewport(2)
}

save_layout <- function(draw_fun, out_dir, stub, width_mm, height_mm, dpi = 600) {
  dir.create(out_dir, showWarnings = FALSE, recursive = TRUE)

  cairo_pdf(file.path(out_dir, paste0(stub, ".pdf")),
            width = mm_to_in(width_mm), height = mm_to_in(height_mm), bg = "white")
  draw_fun()
  dev.off()

  png(file.path(out_dir, paste0(stub, ".png")),
      width = width_mm, height = height_mm, units = "mm", res = dpi,
      bg = "white", type = "cairo")
  draw_fun()
  dev.off()

  tiff(file.path(out_dir, paste0(stub, ".tiff")),
       width = width_mm, height = height_mm, units = "mm", res = dpi,
       bg = "white", compression = "lzw", type = "cairo")
  draw_fun()
  dev.off()
}
```

## Required Structure

Use this skeleton:

```r
build_objects <- function() {
  # Source panel scripts in isolated environments when needed.
  # Return live objects, not file paths.
  list(
    A = pA,
    B = pB,
    C = htC,
    D = function() { ... draw composite panel ... }
  )
}

figure_layout_dimensions <- function() {
  list(
    A = c(x = 4, y = 180, w = 90, h = 50),
    B = c(x = 98, y = 180, w = 90, h = 50)
  )
}

draw_final_figure <- function() {
  objs <- build_objects()  # Rebuild per device when objects contain ComplexHeatmap/grid state.
  grid.newpage()
  grid.rect(gp = gpar(fill = "white", col = NA))
  dims <- figure_layout_dimensions()
  draw_panel_box(objs$A, "A", dims$A["x"], dims$A["y"], dims$A["w"], dims$A["h"])
  draw_panel_box(objs$B, "B", dims$B["x"], dims$B["y"], dims$B["w"], dims$B["h"])
}
```

If object construction is expensive, build pure ggplots once, but rebuild ComplexHeatmap or captured grid objects inside the device draw function when viewport errors appear.

## ComplexHeatmap Rules

- Prefer passing raw `Heatmap` or `HeatmapList` objects into `draw_object()`.
- Do not store `grid.grabExpr(draw(ht))` and reuse it for PDF, PNG, and TIFF.
- Keep `newpage = FALSE` inside a panel viewport.
- Set `width`, `height`, `row_names_gp`, `column_names_gp`, and legend parameters in the Heatmap object.
- Use `column_names_centered = TRUE` when heatmap column labels must align with cells.
- Keep legends close to the heatmap but outside the cell body.

## Patchwork Rules

- Patchwork is acceptable inside source plots only when it is stable.
- Avoid `plot_annotation(tag_levels = "A")` in nested layouts.
- Add panel letters with `draw_panel_box()` at the final assembly level.
- If a panel is itself a multi-part composite, draw it as a function using `grid.layout`.

## Figure Manifest

Always write a manifest with:

- Figure stub and output directory.
- Width and height in millimeters.
- Panel letter.
- Source object or source function.
- Role/question.
- Promotion route: `main`, `supplement`, `source-only`, `diagnostic-only`, or `remove`.
- Area rationale: why the allocated width/height matches the panel's evidence weight and natural aspect ratio.
- Source table or script output supporting the plotted values.
- Interpretation boundary if relevant.
- Statistics, threshold, or sample-size definition needed to interpret the panel when applicable.

Do not list a source-only or diagnostic-only record in a final manuscript assembly manifest as if it were a displayed panel. Keep those records in source-data or package QC manifests unless the panel has been redesigned into an interpretable result display.

## Visual Checklist

Before finalizing manuscript text:

- Panel labels appear exactly once and in correct order.
- No title from a standalone panel remains inside the assembled figure unless intended.
- No source-table-like, QC-only, manifest, coverage, status, blocked-endpoint, or gene-set-size-only panel appears as a manuscript result panel.
- Visible labels use reader-facing scientific/statistical terms rather than internal workflow terms.
- Text is readable at final export size.
- Heatmap x/y labels are centered on cells.
- Colorbars and legends exist for every encoded variable.
- No legends overlap or clip.
- Legend titles are centered above keys or otherwise clearly direct-labeled.
- Shared legends are used only when scales and coordinate semantics are truly shared.
- Multi-subplot panels preserve axis meaning. Do not remove axis titles from later subplots when those subplots use different embeddings, scales, or coordinate systems.
- Paired subplots that invite direct comparison have equal data-body sizes and matching symbol sizes unless the difference encodes data.
- Panel sizes follow evidence hierarchy and information density; low-density statistics are not stretched to visually compete with primary observables.
- No panel has been raster-cropped, stretched, or compressed.
- Assembled output and standalone panels are generated from the same live objects.

## Synchronization Checklist

After changing a publication figure:

- Regenerate the source panel and the assembled figure from live R objects.
- Copy regenerated outputs into the publication-facing directory.
- Regenerate journal upload copies and the figure manifest.
- Update figure legends if visual encodings, axes, displayed categories, or displayed enrichment terms changed.
- Update any project memory or content-map files that describe the figure state.
