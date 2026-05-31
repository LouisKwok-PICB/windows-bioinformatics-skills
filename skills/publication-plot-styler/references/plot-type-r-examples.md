# R Plot Type Examples

Use these generic examples as starting points for manuscript-facing plots. Adapt variable names, labels, and palettes to the dataset. Do not copy project-specific module names or biological claims into reusable scripts.

## Quick Navigation

- Shared theme: `Shared ggplot Theme`
- Summary encodings: `Dotplot`, `Lollipop / High-Tail Fraction Plot`, `Horizontal Bar Chart`
- Heatmaps: `ComplexHeatmap`
- Embeddings: `UMAP / Dense Scatter With Transparent Labels`, `UMAP Axis-Line-Only Style`, `Binary Highlight UMAP`
- Enrichment and flows: `Enrichment Dotplot With Two Representative Terms`, `Alluvial / Sankey`
- Export checks: `Submission TIFF Manifest`

## Shared ggplot Theme

```r
publication_theme <- function(base_size = 7, base_family = "sans") {
  ggplot2::theme_classic(base_size = base_size, base_family = base_family) +
    ggplot2::theme(
      text = ggplot2::element_text(color = "#30343B"),
      plot.title = ggplot2::element_text(hjust = 0.5, face = "bold", size = base_size + 1.5),
      axis.title = ggplot2::element_text(size = base_size),
      axis.text = ggplot2::element_text(size = base_size - 0.5),
      axis.title.x = ggplot2::element_text(margin = ggplot2::margin(t = 4)),
      axis.title.y = ggplot2::element_text(margin = ggplot2::margin(r = 4)),
      legend.title = ggplot2::element_text(size = base_size, face = "bold"),
      legend.text = ggplot2::element_text(size = base_size - 0.5),
      legend.position = "right",
      legend.key.height = grid::unit(4, "mm"),
      legend.key.width = grid::unit(4, "mm"),
      legend.spacing.y = grid::unit(0.2, "mm"),
      legend.box.spacing = grid::unit(1, "mm"),
      plot.margin = ggplot2::margin(4, 5, 5, 4)
    )
}
```

## Dotplot

Use when size and color encode two different summaries. Keep size legends compact.

```r
p <- ggplot(df, aes(x = group, y = label)) +
  geom_point(
    aes(size = percent, fill = value),
    shape = 21,
    color = "#2F353A",
    stroke = 0.35,
    alpha = 0.95
  ) +
  scale_size_area(
    max_size = 6,
    breaks = c(5, 25, 50, 75),
    limits = c(0, 100),
    name = "Cells (%)"
  ) +
  scale_fill_gradientn(
    colors = c("#F4EFE7", "#E7B985", "#CF705C", "#8E2F2F"),
    name = "Mean score"
  ) +
  labs(x = "Group", y = "Label") +
  publication_theme(7) +
  guides(
    fill = guide_colorbar(order = 1, barheight = unit(22, "mm"), barwidth = unit(3, "mm")),
    size = guide_legend(
      order = 2,
      keyheight = unit(4.8, "mm"),
      keywidth = unit(5.0, "mm"),
      override.aes = list(fill = "#CF705C")
    )
  )
```

## Lollipop / High-Tail Fraction Plot

Use when comparing per-label percentages across conditions. Keep the endpoint descriptive.

```r
p <- ggplot(df, aes(x = percent, y = label)) +
  geom_vline(xintercept = reference, linetype = "dotted", linewidth = 0.3, color = "#6E7781") +
  geom_line(aes(group = label), color = "#C9CED3", linewidth = 0.35, na.rm = TRUE) +
  geom_point(aes(fill = condition), shape = 21, size = 2.4, stroke = 0.25, color = "#2F353A") +
  scale_fill_manual(values = c(A = "#5F9E89", B = "#D8B35B", C = "#C45A46"), name = "Condition") +
  scale_x_continuous(labels = function(x) paste0(x, "%"), expand = expansion(mult = c(0, 0.03))) +
  labs(x = "Cells in high-score tail (%)", y = NULL) +
  publication_theme(7) +
  guides(fill = guide_legend(keyheight = unit(3.8, "mm"), keywidth = unit(4.5, "mm"))) +
  theme(panel.grid.major.x = element_line(color = "#ECEFF2", linewidth = 0.25))
```

## ComplexHeatmap

Use for formal heatmaps. Size the heatmap body explicitly and keep annotation labels short.

```r
library(ComplexHeatmap)
library(circlize)

col_fun <- colorRamp2(c(0, 0.5, 1), c("#FFFFFF", "#E7B985", "#8E2F2F"))

left_anno <- rowAnnotation(
  Class = class_factor,
  `Gene count` = anno_barplot(
    log10(gene_count + 1),
    border = FALSE,
    gp = gpar(fill = "#6E7781", col = NA),
    axis = FALSE,
    width = unit(14, "mm")
  ),
  annotation_name_rot = 45,
  annotation_name_gp = gpar(fontsize = 7, fontface = "bold")
)

ht <- Heatmap(
  mat,
  name = "Mean value",
  col = col_fun,
  cluster_rows = FALSE,
  cluster_columns = TRUE,
  show_row_names = FALSE,
  column_names_rot = 45,
  column_names_centered = TRUE,
  column_names_gp = gpar(fontsize = 6),
  left_annotation = left_anno,
  heatmap_legend_param = list(
    title_gp = gpar(fontsize = 7, fontface = "bold"),
    labels_gp = gpar(fontsize = 6),
    legend_height = unit(24, "mm")
  ),
  use_raster = TRUE,
  raster_quality = 3
)
```

## UMAP / Dense Scatter With Transparent Labels

Use text-only `ggrepel`; do not add filled label boxes over expression or score signal.

```r
p <- ggplot(plot_df, aes(umap_1, umap_2)) +
  geom_point(aes(color = score), size = 0.12, alpha = 0.7, stroke = 0) +
  ggrepel::geom_text_repel(
    data = label_df,
    aes(x = umap_1, y = umap_2, label = label),
    inherit.aes = FALSE,
    seed = 1,
    size = 2.2,
    color = "#30343B",
    fontface = "bold",
    max.overlaps = Inf,
    min.segment.length = 0,
    segment.size = 0.12,
    segment.color = "#6F7780",
    box.padding = 0.22,
    point.padding = 0.08
  ) +
  scale_color_gradient(low = "#F2F0EA", high = "#B24A3A", name = "Score") +
  coord_equal() +
  labs(x = "UMAP 1", y = "UMAP 2") +
  publication_theme(7) +
  theme(axis.text = element_blank(), axis.ticks = element_blank())
```

## UMAP Axis-Line-Only Style

Use for formal multi-UMAP figures when different rows or module-specific embeddings have distinct coordinate systems. Keep axis names but remove numeric ticks; avoid a full grey panel border.

```r
umap_axis_theme <- function(base_size = 6.5) {
  publication_theme(base_size) +
    theme(
      axis.text = element_blank(),
      axis.ticks = element_blank(),
      axis.title = element_text(size = base_size, color = "#30343B"),
      axis.title.x = element_text(margin = margin(t = 2.4)),
      axis.title.y = element_text(margin = margin(r = 2.4)),
      axis.line = element_line(color = "#30343B", linewidth = 0.28),
      panel.border = element_blank(),
      panel.grid = element_blank(),
      plot.margin = margin(2, 2, 3.2, 3.2)
    )
}
```

## Binary Highlight UMAP

Use a distinct marker shape or hue that cannot be confused with the continuous score color scale.

```r
p <- ggplot(plot_df, aes(umap_1, umap_2)) +
  geom_point(data = subset(plot_df, !highlight), color = "#D3D7DB", size = 0.10, alpha = 0.35, stroke = 0) +
  geom_point(data = subset(plot_df, highlight), color = "#2C6DB2", shape = 17, size = 0.24, alpha = 0.90, stroke = 0) +
  coord_equal() +
  labs(x = "UMAP 1", y = "UMAP 2") +
  publication_theme(7) +
  theme(axis.text = element_blank(), axis.ticks = element_blank(), legend.position = "none")
```

## Enrichment Dotplot With Two Representative Terms

Use in supplementary panels when one term is too thin but all terms would be crowded. Select terms by biological/statistical role and export the displayed table.

```r
preferred_terms <- list(
  A = c("Response to stimulus", "Cytokine signaling"),
  B = c("Cell adhesion", "Extracellular matrix organization")
)

display_terms <- do.call(rbind, lapply(split(enrich_df, enrich_df$module), function(df) {
  module <- df$module[1]
  selected <- list()
  for (term in preferred_terms[[module]] %||% character(0)) {
    hit <- grep(term, df$term, fixed = TRUE)
    if (length(hit)) selected[[length(selected) + 1]] <- df[hit[1], , drop = FALSE]
    if (length(selected) >= 2) break
  }
  selected <- if (length(selected)) do.call(rbind, selected) else df[FALSE, , drop = FALSE]
  df <- df[order(df$fdr, -df$overlap_genes), , drop = FALSE]
  if (nrow(selected) < 2) {
    selected <- rbind(selected, head(df[!df$term %in% selected$term, , drop = FALSE], 2 - nrow(selected)))
  }
  head(selected, 2)
}))
write.csv(display_terms, "displayed_enrichment_terms.csv", row.names = FALSE)

p <- ggplot(display_terms, aes(module_label, wrapped_term)) +
  geom_point(aes(size = overlap_genes, fill = pmin(-log10(fdr), 8)),
             shape = 21, color = "#2F353A", stroke = 0.28) +
  scale_fill_gradientn(colors = c("#F7F7F3", "#E7B985", "#CF705C", "#8E2F2F"),
                       limits = c(0, 8), name = "-log10 FDR\n(capped)") +
  scale_size_area(max_size = 4.7, name = "Overlap\ngenes") +
  labs(x = "Module", y = "Representative term") +
  publication_theme(6.4)
```

## Horizontal Bar Chart

Use for module sizes, ranks, or long labels.

```r
p <- ggplot(df, aes(x = value, y = reorder(label, value))) +
  geom_col(width = 0.65, fill = "#6E7781") +
  geom_text(aes(label = value_label), hjust = -0.08, size = 2.0, color = "#30343B") +
  scale_x_continuous(expand = expansion(mult = c(0, 0.10))) +
  labs(x = "Value", y = NULL) +
  publication_theme(7) +
  theme(panel.grid.major.x = element_line(color = "#ECEFF2", linewidth = 0.25))
```

## Alluvial / Sankey

Use for splitting/convergence. Keep long definitions outside the alluvial body.

```r
p <- ggplot(flow_df, aes(axis1 = left_group, axis2 = right_group, y = weight)) +
  ggalluvial::geom_alluvium(aes(fill = class), width = 0.18, alpha = 0.78, color = NA) +
  ggalluvial::geom_stratum(width = 0.18, fill = "#F4F5F6", color = "#6E7781", linewidth = 0.25) +
  ggalluvial::geom_text(stat = "stratum", aes(label = after_stat(stratum)), size = 2.0) +
  scale_x_discrete(limits = c("Source", "Target"), expand = c(0.04, 0.04)) +
  labs(x = NULL, y = "Shared items") +
  publication_theme(7) +
  theme(axis.text.x = element_blank(), axis.ticks.x = element_blank(), axis.line.x = element_blank())
```

## Submission TIFF Manifest

Use after producing journal upload copies. This generic pattern records file size and physical dimensions from pixel size and embedded dpi. Adapt paths and journal limits.

```r
copy_submission_tiff <- function(from, to, density = "600x600") {
  dir.create(dirname(to), showWarnings = FALSE, recursive = TRUE)
  magick::image_read(from) |>
    magick::image_background("white", flatten = TRUE) |>
    magick::image_convert(type = "truecolor") |>
    magick::image_write(path = to, format = "tiff", density = density, compression = "lzw")
}

parse_density_number <- function(x) {
  as.numeric(strsplit(as.character(x), "x", fixed = TRUE)[[1]][1])
}

make_figure_manifest <- function(files, max_width_in = 7.5, max_height_in = 8.75, max_size_mb = 10) {
  do.call(rbind, lapply(files, function(path) {
    info <- magick::image_info(magick::image_read(path))
    dpi_x <- if ("density" %in% names(info) && nzchar(info$density)) parse_density_number(info$density) else 300
    data.frame(
      File = basename(path),
      WidthPx = info$width,
      HeightPx = info$height,
      Dpi = dpi_x,
      WidthIn = info$width / dpi_x,
      HeightIn = info$height / dpi_x,
      SizeMB = file.info(path)$size / 1024^2,
      WithinBox = (info$width / dpi_x <= max_width_in) && (info$height / dpi_x <= max_height_in),
      UnderLimit = file.info(path)$size / 1024^2 <= max_size_mb,
      stringsAsFactors = FALSE
    )
  }))
}
```
