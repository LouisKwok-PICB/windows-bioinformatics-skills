# Windows Bioinformatics Skills / Windows 生信分析 Skills

This repository collects a small set of Codex skills that I use to make Windows-based bioinformatics work less fragile: planning analyses around explicit evidence, writing manuscript text from actual results, making readable publication figures, packaging source tables and figure files, and avoiding common PowerShell/Rscript/Python execution mistakes.

这个仓库整理了一组我在 Windows 生信分析中使用的 Codex skills。它们的目标不是替代科研判断，而是帮助 AI assistant 更稳定地完成几类重复但容易出错的工作：围绕证据链规划分析、基于真实结果组织论文内容、生成可发表的图、整理 source tables 和投稿文件，以及减少 PowerShell/Rscript/Python 执行中的路径和编码问题。

## Who This Is For / 适合谁用

This repository may be useful if you:

如果你有下面这些需求，这个仓库可能会有帮助：

- run bioinformatics or computational biology projects on Windows;
- 在 Windows 上进行生信分析或计算生物学分析；
- use R, ggplot2, ComplexHeatmap, Python, PowerShell, or mixed scripts;
- 经常使用 R、ggplot2、ComplexHeatmap、Python、PowerShell 或混合脚本；
- need manuscript figures that remain readable after journal-size export;
- 需要制作在期刊版面大小下仍然清晰可读的论文图片；
- want the assistant to keep analyses tied to explicit claims, source tables, and limitations;
- 希望 AI assistant 把分析结果和明确论点、source tables、局限性对应起来；
- want safer Windows command patterns for Rscript/Python and file operations.
- 希望减少 Windows 下运行 Rscript/Python 和文件操作时的命令错误。

## What Is Included / 包含内容

| Skill | What it helps with | 主要用途 |
|---|---|---|
| `scientific-research-evidence-planner` | Turning a research question into an evidence-chain analysis plan, with data inventory, experiment records, reviewer-risk checks, and conservative interpretation. | 将研究问题整理为证据链分析计划，记录数据清单、分析尝试、审稿风险和保守解释边界。 |
| `scientific-manuscript-writer` | Drafting and auditing Results, Methods, Discussion, figure legends, and reviewer-risk-aware manuscript text. | 撰写和审查 Results、Methods、Discussion、图注，以及注意审稿风险的论文表述。 |
| `publication-plot-styler` | Improving ggplot2/ComplexHeatmap-style panels, legends, heatmaps, dotplots, UMAPs, labels, and export settings. | 优化 ggplot2/ComplexHeatmap 风格图片，包括图例、热图、点图、UMAP、标签和导出设置。 |
| `paper-figure-assembler` | Assembling multi-panel figures from live R objects instead of cropped screenshots or stretched raster panels. | 基于 R 中的 live objects 组装多 panel 图片，避免截图拼图、裁剪变形和低分辨率问题。 |
| `publication-content-packager` | Organizing manuscript-facing outputs: figures, source tables, supplementary tables, scripts, upload copies, and closeout QC. | 整理论文发表材料：主图、附图、source tables、补充表格、脚本、投稿文件和最终 QC。 |
| `windows-code-execution` | PowerShell, Rscript, and Python execution patterns for paths, quoting, UTF-8, `$` expansion, and safer file operations. | Windows 命令执行规则，处理路径、引号、UTF-8、`$` 展开和文件操作安全问题。 |
| `pdf` | Reading, creating, and visually checking PDFs when layout matters. | 处理需要关注排版和视觉效果的 PDF 读取、生成和检查任务。 |

## How The Skills Work Together / 如何组合使用

A common workflow is:

一个常见使用流程是：

```text
scientific-research-evidence-planner
-> publication-plot-styler
-> paper-figure-assembler
-> publication-content-packager
-> scientific-manuscript-writer
```

For example, the assistant can first define what a figure is supposed to prove, then generate or repair the source panels, assemble the final figure from R objects, package source tables and upload files, and only then draft manuscript text that matches the final evidence.

例如，assistant 可以先明确某张图要支持什么结论，再生成或修复源 panel，随后用 R object 组装总图，整理 source tables 和投稿文件，最后再根据已经确定的证据撰写 manuscript 内容。

## What This Repository Does Not Include / 不包含什么

This repository does not include:

本仓库不包含：

- private project data or project-specific conclusions;
- 私有项目数据或项目特异结论；
- unpublished algorithm details;
- 未公开算法细节；
- local absolute project paths;
- 本地绝对项目路径；
- journal-specific guarantees;
- 对特定期刊投稿成功的保证；
- statistical, ethical, or biological validation by itself.
- 对统计、伦理或生物学结论本身的验证。

These skills help structure the work, but users still need to verify data, statistics, ethics, software versions, journal instructions, and final manuscript claims.

这些 skills 只是帮助规范工作流程。用户仍然需要自行核查数据、统计方法、伦理要求、软件版本、目标期刊要求和最终论文结论。

## Repository Layout / 仓库结构

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

Each skill is self-contained. Copy the whole skill directory, not only `SKILL.md`, because some skills include `references/`, `agents/`, or `assets/`.

每个 skill 都是独立目录。复制或安装时应复制完整目录，而不是只复制 `SKILL.md`，因为部分 skill 依赖 `references/`、`agents/` 或 `assets/`。

## Installation / 安装

See [INSTALL.md](INSTALL.md).

安装方式见 [INSTALL.md](INSTALL.md)。

## License / 许可证

See [LICENSE](LICENSE).

许可证见 [LICENSE](LICENSE)。
