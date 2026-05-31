# Windows Bioinformatics Skills / Windows 生信分析 Skills

Reusable Codex skills for Windows-based bioinformatics and computational biology workflows, including research planning, manuscript writing, publication figures, figure-package organization, PDF handling, and reliable PowerShell/Rscript/Python execution.

这是一组面向 Windows 生信分析与计算生物学工作流的可复用 Codex skills，覆盖科研分析规划、论文写作、发表级图片制作、论文图表材料整理、PDF 处理，以及更可靠的 PowerShell/Rscript/Python 命令执行。

This repository intentionally contains only general-purpose workflow skills. It does not include project-specific skills, unpublished method details, private datasets, local project paths, or manuscript-specific conclusions.

本仓库只包含通用工作流 skills，不包含任何项目特异 skill、未公开方法细节、私有数据、本地项目路径或特定论文结论。

## Included Skills / 包含的 Skills

| Skill | Purpose | 用途 |
|---|---|---|
| `scientific-research-evidence-planner` | Plan and document bioinformatics or computational biology analyses around explicit hypotheses, evidence chains, file inventories, experiment attempts, reviewer risks, and conservative conclusions. | 围绕明确假设和证据链规划生信或计算生物学分析，记录文件清单、实验尝试、审稿风险和保守结论边界。 |
| `scientific-manuscript-writer` | Draft, restructure, or audit evidence-first manuscript text, including Results, Methods, Discussion, legends, and reviewer-risk-aware wording. | 撰写、重组或审查以证据为核心的论文文本，包括 Results、Methods、Discussion、图注和审稿风险导向的表述。 |
| `publication-plot-styler` | Create or repair publication-ready plots from R/ggplot2/ComplexHeatmap-style outputs, including legends, labels, heatmaps, dotplots, UMAPs, and export rules. | 优化发表级科研图，包括 R/ggplot2/ComplexHeatmap 风格输出、图例、标签、热图、点图、UMAP 和导出规则。 |
| `paper-figure-assembler` | Assemble publication-ready multi-panel scientific figures from live R objects rather than cropped raster panels. | 基于 R 中的 live objects 组装发表级多 panel 图片，避免使用裁剪后的 raster 图片拼图。 |
| `publication-content-packager` | Organize manuscript-facing figure publication packages with figures, source tables, supplementary tables, scripts, submission-ready files, and closeout QC. | 整理论文发表材料包，包括主图、附图、source tables、补充表格、脚本、投稿文件和最终 QC。 |
| `windows-code-execution` | Run Windows PowerShell, Rscript, and Python commands more reliably, with path quoting and encoding safeguards. | 提供 Windows PowerShell、Rscript 和 Python 命令执行规则，减少路径、引号和编码问题。 |
| `pdf` | Read, create, and visually review PDFs where layout matters. | 读取、创建和检查 PDF，尤其适用于需要确认排版和视觉布局的任务。 |

## What These Skills Are For / 这些 Skills 适合做什么

These skills are designed to help an AI coding assistant:

这些 skills 用于帮助 AI coding assistant：

- treat each analysis as a test of a named scientific claim;
- 把每个分析都视为对明确科学论点的检验；
- document bioinformatics inputs, scripts, source tables, outputs, and interpretation boundaries;
- 记录生信分析输入、脚本、source tables、输出和解释边界；
- separate observation, statistical support, biological or technical interpretation, and claim boundary;
- 区分数据观察、统计支持、生物学或技术解释，以及结论边界；
- keep manuscript claims traceable to figures, source tables, scripts, and statistics;
- 让论文中的论点可以追溯到图片、source tables、脚本和统计量；
- avoid overclaiming results, novelty, mechanisms, comparator failures, or proxy labels;
- 避免过度宣称结果、创新性、机制、对照方法失败或 proxy label 的含义；
- generate readable publication figures and supplementary figures;
- 生成清晰可读的主图和补充图；
- organize manuscript-facing outputs into reproducible figure packages;
- 将面向论文的输出整理成可复现的图表发表包；
- reduce Windows command quoting and Rscript/Python execution errors.
- 减少 Windows 命令、Rscript 和 Python 执行中的路径、引号和编码错误。

They do not replace scientific judgment, target-journal policy checks, statistical review, ethics review, or author responsibility for the manuscript.

这些 skills 不能替代研究者的科学判断、目标期刊政策核查、统计审查、伦理审查，也不能替代作者对论文内容的最终责任。

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

Each skill is self-contained and includes its own `SKILL.md`. Some skills include `references/`, `agents/`, or `assets/`; copy the full skill directory, not only `SKILL.md`.

每个 skill 都是独立目录，并包含自己的 `SKILL.md`。部分 skill 还包含 `references/`、`agents/` 或 `assets/`；安装或复制时应复制完整 skill 目录，而不是只复制 `SKILL.md`。

## Installation / 安装

See [INSTALL.md](INSTALL.md).

安装方式见 [INSTALL.md](INSTALL.md)。

## Scope And Safety / 范围与安全

See [SECURITY_AND_SCOPE.md](SECURITY_AND_SCOPE.md). In short:

详细说明见 [SECURITY_AND_SCOPE.md](SECURITY_AND_SCOPE.md)。简要来说：

- no private project data are included;
- 不包含私有项目数据；
- no unpublished algorithm-specific or project-specific rules are included;
- 不包含未公开算法细节或项目特异规则；
- no local absolute project paths are included;
- 不包含本地绝对项目路径；
- users should verify target-journal instructions before final submission.
- 用户在最终投稿前仍需核查目标期刊的最新要求。

## License / 许可证

See [LICENSE](LICENSE).

许可证见 [LICENSE](LICENSE)。
