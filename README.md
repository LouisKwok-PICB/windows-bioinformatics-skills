# Windows Bioinformatics Skills

This repository contains a small set of Codex skills that I use for Windows-based bioinformatics and computational biology work. They are written to help an AI assistant behave less like a command runner and more like a careful research assistant: check whether the data fit the scientific purpose, keep analyses tied to explicit evidence, make readable publication figures, organize manuscript-facing files, and avoid common Windows command pitfalls.

这个仓库整理了一组我在 Windows 生信分析和计算生物学工作中使用的 Codex skills。它们的目的不是替代科研判断，而是让 AI assistant 在协助分析时更稳健：先判断数据是否适合当前科学问题，再围绕明确证据链推进分析，生成可读的论文图片，整理投稿相关文件，并减少 Windows 下常见的命令、路径和编码问题。

## Who This Is For

You may find this useful if you:

- run R, Python, PowerShell, ggplot2, ComplexHeatmap, or mixed bioinformatics scripts on Windows;
- want analysis plans to start from a concrete claim and a fit-for-purpose data audit;
- need publication figures that remain readable after journal-size export;
- want source tables, scripts, figures, and manuscript text to stay synchronized;
- want reusable rules for safer Windows command execution.

如果你有下面这些需求，这个仓库可能会有帮助：

- 在 Windows 上运行 R、Python、PowerShell、ggplot2、ComplexHeatmap 或混合生信脚本；
- 希望分析计划从明确科学结论和“数据是否适合该目的”的审查开始；
- 需要制作在期刊版面大小下仍然清晰可读的论文图片；
- 希望 source tables、脚本、图片和 manuscript 文本保持一致；
- 希望有一套更安全的 Windows 命令执行规则。

## Included Skills

| Skill | What it helps with |
|---|---|
| `scientific-research-evidence-planner` | Plan analyses around named claims, evidence chains, file inventories, fit-for-purpose data audits, experiment records, reviewer risks, and conservative conclusions. |
| `scientific-manuscript-writer` | Draft or audit Results, Methods, Discussion, figure legends, and reviewer-aware scientific prose from actual evidence. |
| `publication-plot-styler` | Improve ggplot2, ComplexHeatmap, heatmaps, dotplots, UMAPs, labels, legends, spacing, and journal-style exports. |
| `paper-figure-assembler` | Assemble multi-panel figures from live R objects instead of cropped screenshots or stretched raster panels. |
| `publication-content-packager` | Organize manuscript-facing outputs, including figures, source tables, supplementary tables, scripts, upload copies, and closeout QC records. |
| `windows-code-execution` | Use safer PowerShell, Rscript, and Python patterns for paths, quoting, UTF-8, `$` expansion, and file operations on Windows. |
| `pdf` | Read, create, and visually check PDFs when layout, pagination, or rendered appearance matters. |

| Skill | 主要用途 |
|---|---|
| `scientific-research-evidence-planner` | 围绕明确科学结论制定分析计划，维护证据链、文件清单、数据适配性审查、实验记录、审稿风险和保守结论边界。 |
| `scientific-manuscript-writer` | 基于真实结果撰写或审查 Results、Methods、Discussion、图注，以及面向审稿风险的科学表述。 |
| `publication-plot-styler` | 优化 ggplot2、ComplexHeatmap、热图、点图、UMAP、标签、图例、间距和期刊风格导出。 |
| `paper-figure-assembler` | 基于 R 中的 live objects 组装多 panel 图片，避免截图拼图、裁剪变形和栅格拉伸。 |
| `publication-content-packager` | 整理论文发表相关输出，包括图片、source tables、补充表、脚本、投稿副本和最终 QC 记录。 |
| `windows-code-execution` | 提供 Windows 下更稳健的 PowerShell、Rscript、Python 执行规则，处理路径、引号、UTF-8、`$` 展开和文件操作。 |
| `pdf` | 在需要关注排版、页码或渲染效果时，读取、生成和检查 PDF。 |

## Typical Workflow

These skills are meant to work together. A common sequence is:

```text
scientific-research-evidence-planner
-> publication-plot-styler
-> paper-figure-assembler
-> publication-content-packager
-> scientific-manuscript-writer
```

In practice, this means the assistant should first clarify what a figure or analysis is supposed to prove, check whether the available data can actually answer that question, generate or repair the relevant panels, assemble the final figure without distorting plots, package the supporting files, and only then write manuscript text that matches the evidence.

这些 skills 适合组合使用。实际工作中，assistant 应该先明确某个分析或图片想证明什么，再判断现有数据是否真的能回答这个问题；随后生成或修复子图，基于原始绘图对象组装总图，整理支撑文件，最后再根据已经确认的证据撰写 manuscript 文本。

## What This Repository Does Not Do

This repository does not provide private project data, unpublished method details, journal acceptance guarantees, or automatic biological validation. The skills help structure the work, but the user still needs to verify data provenance, statistical design, software versions, ethics requirements, journal instructions, and final scientific claims.

这个仓库不包含私有项目数据、未公开的方法细节，也不保证投稿成功或自动完成生物学验证。它提供的是工作流程和检查规则；用户仍然需要自行确认数据来源、统计设计、软件版本、伦理要求、期刊要求和最终科学结论。

## Repository Layout

```text
windows-bioinformatics-skills/
  README.md
  INSTALL.md
  SKILL_INDEX.md
  SECURITY_AND_SCOPE.md
  LICENSE
  .gitignore
  skills/
    scientific-research-evidence-planner/
    scientific-manuscript-writer/
    publication-plot-styler/
    paper-figure-assembler/
    publication-content-packager/
    windows-code-execution/
    pdf/
```

Each skill is a complete directory. When installing or copying a skill, copy the whole folder, not only `SKILL.md`, because some skills include `references/`, `agents/`, or `assets/`.

每个 skill 都是一个完整目录。安装或复制时应复制整个文件夹，而不是只复制 `SKILL.md`，因为部分 skills 会依赖 `references/`、`agents/` 或 `assets/`。

## Installation

See [INSTALL.md](INSTALL.md).

安装方式见 [INSTALL.md](INSTALL.md)。

## Scope And Safety

See [SECURITY_AND_SCOPE.md](SECURITY_AND_SCOPE.md) for what should and should not be included in this public bundle.

关于这个公开 skill 包应该包含什么、不应该包含什么，见 [SECURITY_AND_SCOPE.md](SECURITY_AND_SCOPE.md)。

## License

See [LICENSE](LICENSE).

许可证见 [LICENSE](LICENSE)。
