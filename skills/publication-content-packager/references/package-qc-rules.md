# Publication Package QC Rules

Use this reference when auditing figure files, source data, scripts, upload copies, and completion status for a manuscript-facing figure package.

## Figure And Table Rules

- Export manuscript-facing plots as `PDF`, `PNG`, and `TIFF` by default unless the user or journal specifies otherwise.
- For PLOS-style packages, prepare flattened RGB or grayscale TIFFs at 300-600 dpi, keep figures within the journal box, and record file size/dimension checks. For other journals, verify the target journal's current figure specifications before final upload copies.
- Verify upload TIFFs are single-frame, RGB or grayscale, have no alpha channel, use lossless compression when available, and meet journal DPI/size limits. Record these checks in a manifest.
- Assemble final multi-panel figures from source plot objects or source tables when possible. Do not assemble a final manuscript figure from low-resolution screenshots or compressed raster previews.
- Keep standalone panels alongside the assembled figure so visual problems can be diagnosed panel by panel.
- Keep source tables separate from formal supplementary tables. Source tables support traceability; formal supplementary tables are manuscript-numbered upload files.
- Add a manifest when there are many figures or tables. Include output path, evidence role, source input, allowed claim, claim boundary, and status.
- Keep formal supplementary figure numbering consistent across manuscript citations, legends, upload filenames, manifests, content maps, and closeout reports. If a conceptual figure is split for upload, use explicit labels such as `S4C1` and `S4C2` everywhere rather than mixing them with `S4C`.
- Ensure figure captions and article titles are not embedded inside figure image files unless the journal explicitly asks for that layout.

## Data Availability And Source Data

Inventory the data behind every figure:

- newly generated raw data;
- processed matrices or objects;
- figure source tables;
- statistical output tables;
- images or segmentation masks;
- reused public datasets and accessions;
- restricted or third-party data;
- scripts and software needed to regenerate the outputs.

Classify each item as `public repository`, `controlled access`, `within paper/supplement`, `reused public source`, `third-party restricted`, `available on justified request`, or `not applicable`. Do not invent repository identifiers, DOIs, licenses, embargo dates, or access committees. Flag weak `available upon request` wording unless a specific legal, ethical, commercial, or third-party restriction exists.

## Script And Environment Rules

- Follow the analysis language already used by the project. If the workflow is R-first, keep new analysis and figure scripts in R unless a specific file format or library makes another language necessary.
- Use established packages for specialized tasks when available. Install missing routine packages when the environment allows it, and record package use in Methods, session info, or logs.
- Keep scripts ordered and named by workflow stage. Avoid unnumbered one-off scripts in the active publication path.
- Include session information or environment metadata for computational reproducibility.
- If a manuscript-facing output depends on a script that could not run locally because of hardware or environment limits, include a portable server-run script with editable input/output paths and major parameters at the top.
- Mark server-run outputs as pending until returned files exist, match expected paths, and pass source-table or figure regeneration checks. Do not package locally downsampled substitutes as final results unless explicitly part of the manuscript design.

## Closeout QC

Before calling a package complete, check:

- all main and supplementary figure files exist in expected formats;
- upload copies exist in `submission_ready/` with journal-compliant names;
- source tables and supplementary tables are traceable to scripts and figures;
- manuscript text, legends, and Methods match final panels and table numbering;
- claims in README, content map, Results, legends, and closeout report are consistent;
- unsupported or failed exploratory claims are documented as limitations or diagnostics, not promoted as results;
- latest generated images, upload copies, and manifests have matching timestamps or documented reasons for differences;
- file-level QC includes dimensions, DPI, file size, color mode, compression, alpha-channel status when relevant, and journal box limits;
- supporting figures named in text have corresponding upload files and source tables;
- figure-specific manuscript packages do not imply whole-paper completion when article-level declarations remain pending;
- every plotted claim has a source-data path and every reused dataset has an accession, DOI, citation, or explicit unresolved field.

## Status Labels

- `draft`: content exists but is not yet reviewed.
- `candidate`: evidence is generated, but panel selection or visual QC remains.
- `publication-facing`: content is organized for manuscript review, but final upload files may still be pending.
- `submission-ready`: final files exist, journal QC has passed, and upload copies are in place.
- `closed`: no required figure-specific work remains except broader manuscript integration or explicit new analysis.
