# CLAUDE.md — SIGGRAPH Conference Track LaTeX 项目规范

本文件供 Claude Code 在辅助撰写和编辑本项目 LaTeX 论文时参考，确保每次对话都遵循一致的规范。

## 项目基本信息

- 投稿目标：SIGGRAPH Technical Papers Conference Track
- 文档类：`\documentclass[acmtog, anonymous, review]{acmart}`
- 文献管理：BibTeX（`ACM-Reference-Format.bst` + `main.bib`）
- 引用格式：作者-年份（`\citestyle{acmauthoryear}`）
- 图片目录：`figs/`
- 编译方式：`pdflatex → bibtex → pdflatex → pdflatex`
- 编译缓存目录：`tmp/`（已被 `.gitignore` 忽略）

## 文件结构

```
main.tex                  # 主论文文件，唯一需要编辑的 tex 文件
main.bib                  # 参考文献库
figs/                     # 所有图片放这里
```

> 注：`acmart.cls`（文档类）和 `ACM-Reference-Format.bst`（BibTeX 样式）是 `acmart` 宏包的一部分，由 TeX 发行版（TeX Live / MiKTeX）自带，不在本仓库内，也不要试图创建或修改它们。

## LaTeX 编写规范

### 文档结构

- 正文章节顺序：Introduction → Related Work → Method → Experiments → Conclusion
- 使用 `\section`、`\subsection`、`\subsubsection`，不要用加粗段落模拟标题
- 致谢使用 `\begin{acks}...\end{acks}`，不要用 `\section{Acknowledgments}`
- 附录放在 `\end{document}` 之前，用 `\appendix` 开头

### 图片

- 所有图片文件放在 `figs/` 目录下
- 引用时使用相对路径：`\includegraphics{figs/filename}`，不要带扩展名（LaTeX 自动匹配）
- 每个 figure 必须有 `\caption{}` 和 `\Description{}`（无障碍要求，ACM 强制）
- 图注放在图片**下方**（`\caption` 在 `\includegraphics` 之后）
- 表格标题放在表格**上方**（`\caption` 在 `\begin{tabular}` 之前）
- 宽图使用 `figure*` 环境（跨双栏）

### 引用

- 引用格式为作者-年份，例如 `\cite{Smith2023}`
- 行内引用用 `\citet{}`，括号引用用 `\citep{}`
- 新参考文献条目添加到 `main.bib`
- BibTeX key 命名规范：`作者姓+年份`，例如 `Smith2023` 或 `SmithJones2023`
- 作者姓名写全名，不要缩写（ACM 要求）

### 数学公式

- 行内公式用 `$...$`
- 独立编号公式用 `equation` 环境
- 不编号的独立公式用 `displaymath` 或 `equation*`

### 匿名审稿注意事项

当前配置为匿名双盲审稿（`anonymous, review`）：

- 不要在正文中出现作者姓名、机构名称
- 不要引用自己未公开的工作
- `\begin{acks}...\end{acks}` 中的致谢内容在 `anonymous` 模式下会自动隐藏，可以正常填写
- `\acmSubmissionID{...}` 替换为 Linklings 系统给你的真实投稿 ID

### 禁止修改的内容

- 不要调整页边距、字号、行距、段落间距
- 不要使用 `\vspace`、`\hspace` 手动调整间距
- 不要替换字体（不要加载 `lmodern`、`ltimes` 等包）
- 不要修改 `acmart.cls` 和 `ACM-Reference-Format.bst`（它们由 TeX 发行版自带，不在仓库内，也不要把它们复制进仓库）

## 参考文献管理

- 所有参考文献写入 `main.bib`
- 常用条目类型：
  - 期刊论文：`@article`
  - 会议论文：`@inproceedings`
  - 技术报告/预印本：`@misc` 或 `@techreport`
  - 书籍：`@book`
- DOI 字段尽量填写
- 会议/期刊名称写全称，不要自行缩写

## Git 规范

- 只维持一个 commit history（amend + force push）
- 不要提交编译产物（`.aux`、`.pdf`、`.log` 等，已被 `.gitignore` 忽略）
- 不要提交 `tmp/` 目录内容

## camera-ready 时需要做的事

1. 将文档类改为：`\documentclass[acmtog]{acmart}`
2. 填写 ACM 录用邮件提供的版权信息（`\setcopyright`、`\acmDOI`、`\acmConference` 等）
3. 填写真实作者信息
4. 按 ACM TAPS 系统要求提交源文件
