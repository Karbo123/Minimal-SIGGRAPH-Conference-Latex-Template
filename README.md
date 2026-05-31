# SIGGRAPH Conference Track LaTeX 模板

本仓库基于官方 ACM `acmart` 包，为 **SIGGRAPH Technical Papers Conference Track** 初次投稿配置，开箱即用。

## 当前配置

- 投稿类型：SIGGRAPH Technical Papers **Conference Track**
- 状态：**匿名双盲审稿**（`anonymous, review`）
- 文献管理：**BibTeX**
- 图片目录：[figs/](figs/)

```latex
\documentclass[acmtog, anonymous, review]{acmart}
\citestyle{acmauthoryear}
```

## 官方原始资源与来源说明

本仓库的 `main.tex` 源自官方 ACM `acmart` 宏包 **v2.16（2025-08-27）** 的样例文件 `sample-acmtog-conf.tex`（改名而来）。

> **关于版本**：上面的 v2.16 指的是「`main.tex` 取自哪个版本的 acmart 样例」。**实际排版所用的 `acmart.cls` 由本机 TeX 发行版（TeX Live / MiKTeX）提供**（见下文「关于 `acmart.cls` 和 `ACM-Reference-Format.bst`」），其版本以发行版为准，可能随 `tlmgr update` 高于 v2.16。本仓库不锁定 acmart 版本——这是有意为之，以便始终用到发行版维护的最新修订。编写本仓库时，发行版自带的 acmart 恰好也是 v2.16，两者一致。

官方 `acmart` 包有两个等价的下载入口，**装的是同一个包、同一份样例**：

```
# CTAN（权威发行版）
https://mirrors.ctan.org/macros/latex/contrib/acmart.zip

# ACM 官网（同一个包的镜像）
https://portalparts.acm.org/hippo/latex_templates/acmart-primary.zip
```

> **关于来源的澄清**：本仓库 `main.tex` 的源文件 `sample-acmtog-conf.tex` 经逐字节哈希核对，CTAN 版与 ACM 官网版**完全相同**（sha256 `6d669bee…`），保留的 `sample-base.bib`、`sample-franklin.png`、`sampleteaser.pdf` 也两边一致。两者唯一区别是打包方式：CTAN 的 `acmart.zip` 只附带 `samples.dtx`，需要运行 `pdflatex samples.ins`（docstrip）才能生成出 `.tex` 样例；ACM 官网的 `acmart-primary.zip` 则**直接附带已生成好的 `.tex`**。下文「删除的文件」表中列出的 `sample-*.tex`，指的就是这一步生成（或 ACM 官网版直接自带）的 18 个样例文件。
>
> **为什么不用 SIGGRAPH 投稿说明页里的那个 zip**：`https://www.siggraph.org/.../author-instructions/` 早年提供的 `sample-SIGGRAPH-techpaper-submission.zip` 是 **2018 年的旧包**（用 `\input{samplebody-journals}` 拆分正文、bib 名为 `sample-bibliography.bib`），结构已过时，并非当前的 `acmart`。SIGGRAPH 官方现已改为指引使用当前版 `acmart`，因此本仓库直接基于官方 `acmart` 包，而非那个旧 zip。

官方 SIGGRAPH 作者投稿说明：

```
https://www.siggraph.org/preparing-your-content/author-instructions/
```

### 为什么是 `sample-acmtog-conf.tex` 这个样例

`acmart` 包里有十多个样例，本仓库选 `sample-acmtog-conf.tex`，依据是它的 docstrip 头部声明：

```
%% samples.dtx  (with options: `all,journal,proceedings,bibtex,acmtog-conf')
```

`journal,proceedings` + `acmtog-conf` 这组选项对应的正是 **SIGGRAPH Technical Papers Conference Track**（详见下方「为什么选」表）。

<details>
<summary><strong>本仓库文件说明与改动详情</strong>（点击展开）</summary>

### 保留的文件

| 文件 | 来源（官方 zip 中的路径） | 保留理由 |
|------|--------------------------|---------|
| [main.tex](main.tex) | `acmart/samples/sample-acmtog-conf.tex` | Conference Track 对应的官方样例，改名后作为主文件 |
| [main.bib](main.bib) | `acmart/samples/sample-base.bib` | `main.tex` 中 `\bibliography{main}` 依赖它；已从官方原名 `sample-base.bib` 改名为 `main.bib` |
| [figs/sample-franklin.png](figs/sample-franklin.png) | `acmart/samples/sample-franklin.png` | `main.tex` 正文 figure 示例引用 |
| [figs/sampleteaser.pdf](figs/sampleteaser.pdf) | `acmart/samples/sampleteaser.pdf` | 用作正文头图（teaser figure）的占位图；正式投稿前替换为自己的头图 |

> **关于 `acmart.cls` 和 `ACM-Reference-Format.bst`**：这两个文件是 `acmart` 宏包的一部分，**TeX Live / MiKTeX 安装后会自带**（本机位于 `texmf-dist/tex/latex/acmart/` 和 `texmf-dist/bibtex/bst/acmart/`），编译时 LaTeX 会自动找到它们。因此本仓库**不再单独保存**这两个文件，也已在 `.gitignore` 中忽略，避免把发行版自带、且会随 `tlmgr update` 更新的文件锁死在某个旧版本。如果你的环境没有安装 acmart，运行 `tlmgr install acmart` 即可。

### 删除的文件及理由

**`acmart/`（zip 根目录）**

| 文件 | 删除理由 |
|------|---------|
| `acmart.dtx` | 用于生成 `acmart.cls` 的源码；`acmart.cls` 由 TeX 发行版自带（见上方说明），无需自行生成 |
| `acmart.ins` | 配合 `acmart.dtx` 生成 `.cls` 的安装脚本，同上 |
| `acmart.pdf` | acmart 完整使用文档（200+ 页），参考文档，不是投稿所需文件 |
| `acmguide.pdf` | acmart 快速指南，参考文档，不是投稿所需文件 |
| `acmart.bib` | 只用于生成 `acmart.pdf`，与投稿无关 |
| `README` | acmart 包维护者说明，本仓库有自己的 `README.md` |
| `Makefile` | 只对 acmart 包开发者有用 |
| `acmauthoryear.bbx` | BibLaTeX 样式，本仓库使用 BibTeX，不用 BibLaTeX |
| `acmauthoryear.cbx` | 同上 |
| `acmnumeric.bbx` | 同上 |
| `acmnumeric.cbx` | 同上 |
| `acmdatamodel.dbx` | 同上 |
| `acm-jdslogo.png` | 只用于生成 `acmart.pdf` 文档内部，与投稿无关 |

**`acmart/samples/`（样例目录）**

> 说明：下表的 `sample-*.tex` 共 18 个，是运行 `samples.ins`（docstrip）由 `samples.dtx` **生成**的（ACM 官网版 `acmart-primary.zip` 则直接自带这 18 个 `.tex`）；本仓库只保留 `sample-acmtog-conf.tex`（即 `main.tex`），其余删除。除 `.tex` 外，原样例目录还含 **16 个 `.pdf` 预览图**（每个样例的渲染结果，如 `sample-acmtog-conf.pdf`）、`acmengage.dtx`（ACM Engage 课程材料样例源码）、以及 `sample-acmsmall-tagged-luamml-mathml.html`（无障碍标记示例的 HTML 输出）——这些都是参考/演示文件，与本仓库投稿无关，一并删除。

| 文件 | 删除理由 |
|------|---------|
| `abbrev.bib` | 期刊/会议名称缩写定义，`main.bib`（即官方 `sample-base.bib`）单独编译不依赖它 |
| `software.bib` | 软件类引用示例，不是投稿必须的 |
| `sample-acmtog.tex` | SIGGRAPH **journal track** 样例，你投的是 conference track |
| `sample-sigconf.tex` | 其他 SIGGRAPH 项目（Posters 等）样例，不是你的投稿类型 |
| `sample-acmsmall.tex` | PACMCGIT 期刊样例，不是你的投稿类型 |
| `sample-acmsmall-conf.tex` | acmsmall conference 样例，不是你的投稿类型 |
| `sample-acmsmall-biblatex.tex` | 使用 BibLaTeX，且不是你的投稿类型 |
| `sample-acmsmall-submission.tex` | 不是你的投稿类型 |
| `sample-acmsmall-tagged.tex` | 无障碍标记样例，不是你的投稿类型 |
| `sample-acmlarge.tex` | JOCCH/TAP 期刊样例，不是你的投稿类型 |
| `sample-acmcp.tex` | ACM Computing Practices 样例，不是你的投稿类型 |
| `sample-manuscript.tex` | 初稿单栏样例，你要的是完整排版的 conference 版本 |
| `sample-sigconf-authordraft.tex` | 不是你的投稿类型 |
| `sample-sigconf-biblatex.tex` | 使用 BibLaTeX，且不是你的投稿类型 |
| `sample-sigconf-i13n.tex` | 多语言样例，不是你的投稿类型 |
| `sample-sigconf-lualatex.tex` | 使用 LuaLaTeX，且不是你的投稿类型 |
| `sample-sigconf-xelatex.tex` | 使用 XeLaTeX，且不是你的投稿类型 |
| `sample-sigplan.tex` | SIGPLAN 样例，不是你的投稿类型 |
| `sample-acmengage.tex` | ACM Engage 课程材料样例，不是你的投稿类型 |
| `samples.dtx` | 生成所有样例 `.tex` 的源码（docstrip） |
| `samples.ins` | 配合 `samples.dtx` 生成样例 `.tex` 的安装脚本 |
| `acmengage.dtx` | 生成 `sample-acmengage.tex` 的源码 |
| `sample-*.pdf`（16 个） | 各样例的渲染预览（如 `sample-acmtog-conf.pdf`），参考用，非投稿文件 |
| `sample-acmsmall-tagged-luamml-mathml.html` | 无障碍标记示例的 HTML 输出，参考用 |

### 本仓库新增的文件

| 文件 | 说明 |
|------|------|
| [.gitignore](.gitignore) | 忽略编译产物（`*.aux`、`*.pdf` 等）和 `tmp/` 目录 |
| [README.md](README.md) | 本文件 |
| [CLAUDE.md](CLAUDE.md) | 供 Claude Code 使用的项目规范文件 |

### `main.tex` 相比官方样例的改动

相比官方 `sample-acmtog-conf.tex`，`main.tex` 共有 **6 组改动**：

| 位置 | 官方原文 | 改动后 | 说明 |
|------|---------|--------|------|
| 第 46 行 | `%%`（空注释行） | `%% SIGGRAPH Conference Track submission uses the review configuration below.` | 加一行说明性注释，紧接在 `\documentclass` 上方 |
| 第 47 行 | `\documentclass[acmtog]{acmart}` | `\documentclass[acmtog, anonymous, review]{acmart}` | 启用匿名双盲审稿模式和行号 |
| 第 88 行 | `%%\acmSubmissionID{123-A56-BU3}` | `\acmSubmissionID{123-A56-BU3}` | 去掉注释符，让投稿 ID 在每页显示（review 模式要求） |
| 第 260–269 行 | （无，官方样例此处直接 `\maketitle`） | 在 `\maketitle` 前新增真实 `teaserfigure` 环境（含 `\caption` 与 `\Description`） | 让头图真正显示在标题/作者块之后、正文之前；官方样例仅在正文用 `verbatim` 演示该写法，并未真正插图 |
| 第 621 行 | `{sample-franklin}` | `{figs/sample-franklin}` | 图片移入 `figs/` 子目录 |
| 第 661 行 | `{sampleteaser}` | `{figs/sampleteaser}` | 同上（正文 `verbatim` 示例代码里的路径） |
| 第 812 行 | `\bibliography{sample-base}` | `\bibliography{main}` | 参考文献库从官方原名 `sample-base.bib` 改名为 `main.bib` |

> 其中第 46–47 行是**同一处改动**（替换 `\documentclass` 配置时顺带加了上方的说明注释），其余 5 处各独立，故称「6 组改动」。

### 为什么选 `sample-acmtog-conf.tex`

官方 zip 里有多个样例文件，选择依据如下：

| 样例文件 | 对应投稿类型 |
|---------|------------|
| `sample-acmtog-conf.tex` | SIGGRAPH Technical Papers **Conference Track** ← 本仓库使用 |
| `sample-acmtog.tex` | SIGGRAPH Technical Papers Journal Track |
| `sample-sigconf.tex` | SIGGRAPH Posters、Talks 等其他项目 |
| `sample-acmsmall.tex` | PACMCGIT 期刊 |
| `sample-manuscript.tex` | 初稿单栏格式（任何类型的初始草稿） |

</details>

## 编译方法

推荐用 `latexmk` 一条命令编译，产物直接写入 `tmp/` 缓存目录（自动处理 bibtex 和多次编译）：

```bash
latexmk -pdf -outdir=tmp main.tex
```

也可以按官方四步流程手动编译。注意：以下命令把产物生成在**当前目录**（不是 `tmp/`），这些产物已被 `.gitignore` 忽略：

```bash
pdflatex main
bibtex main
pdflatex main
pdflatex main
```

编译产物（`*.aux`、`*.pdf` 等）和 `tmp/` 目录都已被 `.gitignore` 忽略。`figs/` 下的图片（含 PDF 矢量图）不受忽略影响，可正常提交。

## 正式投稿前需要修改的地方

- `\title{...}` — 替换为你的论文标题
- `\author{...}` 等作者信息 — 匿名投稿时保持占位符即可，camera-ready 时填写真实信息
- `\acmSubmissionID{...}` — 替换为 Linklings 系统给你的真实投稿 ID
- abstract、CCS concepts、keywords、正文内容

camera-ready 时将文档类改回：

```latex
\documentclass[acmtog]{acmart}
```

并填入 ACM 录用后提供的版权、DOI、会议信息。

## 推荐工具链

| 工具 | 说明 |
|------|------|
| [latex-vscode-config](https://github.com/shinyypig/latex-vscode-config) | VS Code 本地 LaTeX 开发环境配置教程 |
| [SIGGRAPH 作者投稿说明](https://www.siggraph.org/preparing-your-content/author-instructions/) | 官方投稿规范 |
| [Claude Code](https://code.claude.com/docs/en/quickstart#step-1-install-claude-code) | AI 辅助 LaTeX 代码编写 |
| [ccswitch](https://ccswitch.io/zh/) | 切换大模型供应商 |
