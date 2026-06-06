---
name: paper-figure-assembler
description: Assemble publication-ready multi-panel scientific figures from R panel objects. Use when Codex needs to create, repair, or refactor a manuscript main figure or supplementary figure layout from ggplot, ComplexHeatmap, grob, gtable, or draw-function objects, especially after author layout critique or when designing canvas size, panel ratios, whitespace, legend titles, axis text, panel body alignment, avoiding raster cropping, patchwork tag errors, viewport reuse errors, distorted panels, or unreadable journal-style assembled figures.
---

# Paper Figure Assembler

## Core Rule

Assemble manuscript figures from live objects, not from cropped PNG/PDF panel images. Use fixed `grid` viewports and redraw every panel on each output device. Treat panel letters as external labels added by the assembler, not as titles inside source panels.

For the full R template and validation checklist, read `references/r-object-assembly.md`.
For canvas sizing, panel ratios, whitespace control, and multi-panel layout heuristics, read `references/layout-design.md`.

This skill handles figure assembly geometry and export. For single-panel styling, use `publication-plot-styler`. For manuscript wording and domain-specific claims, use the relevant manuscript or domain guardrail skill if one exists.

Keep current-project panel logic and biological conclusions out of this general skill. Store project-specific final layouts, script chains, and evidence maps in a project navigator skill or repository docs.

Use `publication-content-packager` after assembly when the task is to organize final figures, standalone panels, source tables, manuscript text, submission-ready copies, and closeout QC. This assembler should not decide whether a scientific claim is supported; it should enforce that every assembled panel has a clear role and traceable source.

Before assembling, require a panel map. Each panel must have a letter, source object, evidence role, one-sentence takeaway, source table, and claim boundary. Do not assemble panels whose role in the figure argument is unclear; return them to standalone review first.

For manuscript-facing figures or candidate figures under author review, make the panel map and layout repair plan a **user-visible checkpoint**. If the user gives visual critique, questions the figure's rigor, or project recovery docs require author confirmation, first state the affected panels, object-level fixes, validation steps, and unchanged scientific quantities; wait for explicit confirmation before editing scripts, rerendering, or updating outputs. Treat critique as diagnosis rather than permission to proceed unless the user explicitly says to proceed immediately.

For dense multi-panel manuscript figures, rank panel evidence before assigning area: primary evidence gets the largest or clearest body; validation, comparator, robustness, and limitation panels get space according to information density. Do not default to equal-sized panels when the inferential weight and visual density differ.

Rows do not need to be filled edge-to-edge. A low-density context, summary, limitation, or source-breadth panel may sit in a partial-width bottom row with deliberate whitespace. Do not stretch a sparse bar chart, table, or metric summary across the full figure width just because it is alone on a row; full-width rows are for panels whose evidence role and natural aspect ratio justify that space.

## Workflow

1. Build source panel objects in a function such as `build_objects()`.
   - Return a named list: `A`, `B`, `C`, etc.
   - Allow each element to be a `ggplot`, `ComplexHeatmap::Heatmap`, `HeatmapList`, `grob`, `gtable`, or draw function.
   - Strip source panel titles before assembly unless the title is scientific content.
   - Keep panel-specific captions and interpretation out of the image unless the journal or figure design requires embedded labels.

2. Define figure dimensions in millimeters.
   - Use a larger canvas when details are dense; do not squeeze a paper figure into a small preview page.
   - Define `figure_layout_dimensions()` returning `x`, `y`, `w`, `h` for each panel.
   - Use deterministic row heights, column widths, margins, and gaps.
   - Assign space by information density: heatmaps and dense UMAPs need body area; legends need enough width to be readable but should not dominate.
   - Allow partial-width rows when a subordinate panel is clearer at a smaller natural width; intentional whitespace is acceptable when it preserves evidence hierarchy.
   - When a panel contains subplots, redesign the internal subplot layout before shrinking the whole panel.

3. Draw with `grid`, not raster recomposition.
   - Open `cairo_pdf`, `png(type = "cairo")`, and `tiff(type = "cairo", compression = "lzw")`.
   - Call a `draw_final_figure()` function separately for each device.
   - Inside each panel viewport, call `draw_object(obj)`.
   - For ComplexHeatmap, call `ComplexHeatmap::draw(..., newpage = FALSE)`.

4. Export standalone panels from the same live objects.
   - Use the same `draw_panel_box()` routine and panel dimensions as the assembled figure.
   - Write a manifest mapping panel letter, file stub, source object, width, height, and interpretation.

5. Validate visually before editing manuscript text.
   - Open the assembled PNG.
   - Check panel tags A-G exactly once, no A-H leak from nested patchwork.
   - Check no raster distortion/cropping, no heatmap label misalignment, and all colorbars/legends are present.
   - Check every panel can be understood from figure legend plus labels.
   - Check the figure still works at the target journal's final physical dimensions, not only when zoomed on screen.
   - Check the visual hierarchy matches the evidence hierarchy: the main validation or conclusion panel should not be visually weaker than a diagnostic panel.
   - Check no subordinate, low-density panel appears visually promoted because it was stretched to fill an otherwise empty row.
   - Check standalone panels and assembled panels encode the same values, scales, legends, and thresholds.

## Do Not

- Do not assemble by reading panel PNGs and placing them as rasters unless explicitly making a quick diagnostic draft.
- Do not reuse a `grid.grabExpr(draw(ht))` grob across multiple output devices; it can cause viewport errors.
- Do not rely on nested `patchwork::plot_annotation(tag_levels = "A")` when panels contain subplots; it can create extra letters.
- Do not put panel letters in each source panel and then add letters again in the assembler.
- Do not let assembled dimensions force text below publication readability.

## General Pattern

Use object-based assembly as the default reusable pattern: build live objects, draw them into fixed `grid` viewports, save each device by redrawing the complete layout, and export standalone panels from the same objects and panel dimensions.
