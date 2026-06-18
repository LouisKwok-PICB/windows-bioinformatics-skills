# Windows Bioinformatics Skills

This repository contains a small set of Codex skills that I use for Windows-based bioinformatics and computational biology work. They are written to help an AI assistant behave less like a command runner and more like a careful research assistant: check whether the data fit the scientific purpose, keep analyses tied to explicit evidence, plan source-backed database/literature lookups, audit enrichment analyses, preflight compute-heavy jobs, keep task Markdown and recovery records focused, make readable publication figures, organize manuscript-facing files, avoid common Windows command pitfalls, and prepare portable server-run scripts when local hardware is not enough.

这个仓库整理了一组我在 Windows 生信分析和计算生物学工作中使用的 Codex skills。它们的目的不是替代科研判断，而是让 AI assistant 在协助分析时更稳健：先判断数据是否适合当前科学问题，再围绕明确证据链推进分析，让任务 Markdown 和恢复记录保持聚焦，生成可读的论文图片，整理投稿相关文件，减少 Windows 下常见的命令、路径和编码问题，并在本机硬件不足时生成可迁移到服务器运行的脚本。

## Who This Is For

You may find this useful if you:

- run R, Python, PowerShell, ggplot2, ComplexHeatmap, or mixed bioinformatics scripts on Windows;
- want analysis plans to start from a concrete claim and a fit-for-purpose data audit;
- want each planned project to leave lightweight recovery notes so another agent can resume after interruption;
- want new planning requests to reuse and update existing related Markdown plan records before creating duplicate plan files;
- want multi-step plans to record the current active step, outcome, and next checkpoint instead of relying on chat history;
- want Markdown task memory, recovery notes, package records, and skill docs kept compact without losing provenance;
- need publication figures that remain readable after journal-size export;
- want source tables, scripts, figures, and manuscript text to stay synchronized;
- need compute-heavy analyses to be moved from a local Windows machine to a server without changing the scientific endpoint;
- want reusable rules for safer Windows command execution.

如果你有下面这些需求，这个仓库可能会有帮助：

- 在 Windows 上运行 R、Python、PowerShell、ggplot2、ComplexHeatmap 或混合生信脚本；
- 希望分析计划从明确科学结论和“数据是否适合该目的”的审查开始；
- 希望每个有计划的项目都留下轻量级恢复记录，方便任务中断后由其他 assistant 接续；
- 希望 Markdown 任务记忆、恢复记录、package 记录和 skill 文档保持精简，同时不丢失来源和历史索引；
- 需要制作在期刊版面大小下仍然清晰可读的论文图片；
- 希望 source tables、脚本、图片和 manuscript 文本保持一致；
- 需要在本地 Windows 机器跑不动时，把计算量大的分析迁移到服务器，而不是降低原始科学目标；
- 希望有一套更安全的 Windows 命令执行规则。

## Included Skills

| Skill | What it helps with |
|---|---|
| `scientific-research-evidence-planner` | Plan analyses and literature reviews around named scientific questions, data-fit audits, endpoint-native analysis designs, evidence chains, external-paper summaries, reusable Markdown plan records, active-step recovery records, execution-environment feasibility, experiment records, figure-promotion gates, reviewer risks, and conservative conclusions. |
| `scientific-manuscript-writer` | Draft or audit Results, Methods, Discussion, figure legends, and reviewer-aware scientific prose from actual evidence. |
| `bioinformatics-enrichment-analysis-guardrails` | Design, audit, interpret, and report defensible ORA, GSEA, GSVA, GO, KEGG, Reactome, MSigDB, and module-enrichment workflows with explicit background universes and panel-coverage limits. |
| `scientific-compute-resource-planner` | Preflight CPU, memory, disk, packages, workers, chunking, progress logging, and server-run strategy for compute-heavy scientific analyses. |
| `scientific-database-literature-lookup` | Plan source-backed paper, gene, protein, pathway, dataset, accession, and public database lookups with reproducible provenance. |
| `publication-plot-styler` | Convert supported evidence-chain results into reader-facing single-panel plots, improving terminology, display grammar, legends, color scales, whitespace, heatmaps, dotplots, UMAPs, and journal-style exports. |
| `paper-figure-assembler` | Assemble multi-panel figures from live R objects with panel order, area, and whitespace driven by evidence hierarchy, information density, natural aspect ratio, and journal readability. |
| `publication-content-packager` | Organize manuscript-facing outputs, including figures, source tables, supplementary tables, scripts, upload copies, and closeout QC records. |
| `windows-code-execution` | Use safer PowerShell, Rscript, and Python patterns for paths, quoting, UTF-8, `$` expansion, file operations on Windows, and portable server-run scripts. |
| `markdown-context-curator` | Keep Markdown/YAML task memory, recovery notes, package records, archives, and skill docs concise while preserving information through indexes and archives. |
| `pdf` | Read, create, and visually check PDFs when layout, pagination, or rendered appearance matters. |

| Skill | 主要用途 |
|---|---|
| `scientific-research-evidence-planner` | 围绕明确科学问题制定分析和文献审阅计划，维护数据适配性审查、endpoint-native 分析设计、证据链、外部论文摘要、可复用 Markdown 计划、主动步骤恢复记录、运行环境可行性、实验记录、图件提升门控、审稿风险和保守结论边界。 |
| `scientific-manuscript-writer` | 基于真实结果撰写或审查 Results、Methods、Discussion、图注，以及面向审稿风险的科学表述。 |
| `bioinformatics-enrichment-analysis-guardrails` | 设计、审查、解释和报告 ORA、GSEA、GSVA、GO、KEGG、Reactome、MSigDB 及模块富集分析，强调背景基因集和 panel 覆盖限制。 |
| `scientific-compute-resource-planner` | 在计算量大的科学分析前预检 CPU、内存、磁盘、软件包、线程、分块、进度日志和服务器运行策略。 |
| `scientific-database-literature-lookup` | 规划有来源依据的论文、基因、蛋白、通路、数据集、accession 和公共数据库查询，并记录可复现来源。 |
| `publication-plot-styler` | 将已通过证据链判断的结果转化为读者可理解的单图，优化术语、展示语法、图例、色阶、空白、热图、点图、UMAP 和期刊风格导出。 |
| `paper-figure-assembler` | 基于 R 中的 live objects 组装多 panel 图片，按照证据层级、信息密度、自然比例和期刊可读性决定 panel 顺序、面积和空白。 |
| `publication-content-packager` | 整理论文发表相关输出，包括图片、source tables、补充表、脚本、投稿副本和最终 QC 记录。 |
| `windows-code-execution` | 提供 Windows 下更稳健的 PowerShell、Rscript、Python 执行规则，处理路径、引号、UTF-8、`$` 展开、文件操作和服务器运行脚本。 |
| `markdown-context-curator` | 整理 Markdown/YAML 任务记忆、恢复记录、package 记录、归档和 skill 文档，在保留信息索引的同时减少上下文负担。 |
| `pdf` | 在需要关注排版、页码或渲染效果时，读取、生成和检查 PDF。 |

## Typical Workflow

These skills are meant to work together. A common sequence is:

```text
scientific-research-evidence-planner
-> scientific-database-literature-lookup
-> bioinformatics-enrichment-analysis-guardrails
-> publication-plot-styler
-> paper-figure-assembler
-> publication-content-packager
-> scientific-manuscript-writer
```

In practice, this means the assistant should first state the biological or methodological question, define the required data, judge whether the available data are fit for that purpose, choose endpoint-native analyses, assign each result to a non-redundant evidence-chain role, search for and update an existing related Markdown plan when one exists, create or update `AGENT_MEMORY.yaml` and `docs/CURRENT_TASK.md` for recovery, record the current active step before executing a multi-step plan, summarize external papers before using their figures as evidence or design references, record panel-level evidence gates before any manuscript-facing figure assembly or publication package, decide whether the current machine can run the required analysis, prepare a server-run script when needed, generate or repair only justified panels, assemble the final figure without distorting plots, package the supporting files, update the step outcome and next checkpoint, and only then write manuscript text that matches the evidence.

这些 skills 适合组合使用。实际工作中，assistant 应该先明确某个分析或图片想证明什么，并创建或更新 `AGENT_MEMORY.yaml` 和 `docs/CURRENT_TASK.md` 作为恢复记录；如果使用外部论文作为证据或图片设计参考，先整理论文核心摘要和来源状态，再逐图分析；随后判断现有数据是否真的能回答这个问题；在任何面向 manuscript 的最终组图或 publication package 之前，记录并通过 panel-level evidence gate；随后判断当前机器是否能运行所需分析，必要时生成服务器运行脚本；之后再生成或修复子图，基于原始绘图对象组装总图，整理支撑文件，最后根据已经确认的证据撰写 manuscript 文本。

## Server-Run Scripts

Some bioinformatics analyses are too large for a local Windows machine. In that case, these skills instruct the assistant to treat the problem as an execution-environment limit, not as a reason to weaken the analysis. The expected output is a portable R or Python script with input paths, output paths, thread counts, seeds, and major parameters placed at the top so the user can edit them and run the script directly on a server.

有些生信分析不适合在本地 Windows 机器上完成。遇到这种情况时，这些 skills 要求 assistant 将问题视为运行环境限制，而不是降低分析目标。更合适的输出是一个可迁移的 R 或 Python 脚本，把输入路径、输出路径、线程数、seed 和关键参数集中放在脚本顶部，用户修改后即可在服务器上直接运行。

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
    bioinformatics-enrichment-analysis-guardrails/
    scientific-compute-resource-planner/
    scientific-database-literature-lookup/
    publication-plot-styler/
    paper-figure-assembler/
    publication-content-packager/
    windows-code-execution/
    markdown-context-curator/
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
