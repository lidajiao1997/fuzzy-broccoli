# Lecture Notes Template（单文件通用讲义模板）

一个**开箱即用、全自包含**的 XeLaTeX 课程讲义模板。所有内容——排版机制、参数接口、正文、参考文献——都在**一个 `.tex` 文件**里，不依赖任何外部配置或数据文件。换一门课只需改文件顶部的接口区和正文章节，无需在多文件之间来回切换、也不必担心漏改或找不到错误位置。

仓库中的示例正文是一套**完整可用的示例讲义（图论基础 + 初等数论）**，并非空洞的占位文字——它用真实的知识结构（定义、定理、证明、习题、图表）充分展示模板在匀称、清秀方面的排版能力，可整段替换为你的课程内容。示例主题、封面署名与文献条目均与真实课程无关，仅作演示。

## 特性

- **单文件自包含**：机制 + 接口 + 正文 + 文献一体，拷贝一个文件即可编译。
- **文献沿用 `filecontents*` 内嵌**：编译时自动生成 `.bib`，无需外部文献文件。
- **集中接口区**：文档类、封面信息、主题色、页边距、章节称谓、定理名称、解答开关全部集中在文件顶部，带 `【接口N】` 编号与说明。
- **习题解答一键切换**：`\showanswertrue` / `\showanswerfalse` 控制答案显示，`solution*` 环境恒显示。
- **完整学术排版**：book 文档类、篇/章/节层级、定理族环境、GB/T 7714 参考文献、术语索引、TikZ 绘图、fancy 页眉页脚、自定义篇页。
- **强制 XeLaTeX 检测**：误用其他编译器会给出明确报错。

## 文件结构

```
.
├── lecture-template.tex   # 唯一的源文件：模板机制 + 接口 + 示例正文 + 内嵌文献
├── lecture-template.pdf   # 编译生成的示例产物
├── README.md
├── LICENSE                # MIT
└── .gitignore
```

编译后自动产生（已被 `.gitignore` 忽略）：`refs.bib`、`*.aux`、`*.bbl`、`*.blg`、`*.idx`、`*.ilg`、`*.ind`、`*.log`、`*.out`、`*.toc`。

## 快速开始

需要 TeX Live / MiKTeX，且需 `biber`、中文宏包 `ctex` 与 `gb7714-2015` 样式。

```bash
xelatex lecture-template.tex
biber lecture-template
xelatex lecture-template.tex
xelatex lecture-template.tex
```

> Windows 用户可在 TeXworks / TeXstudio 中选择 XeLaTeX 编译，并按上述顺序运行 biber。

## 接口一览

所有接口都在 `lecture-template.tex` 顶部「用户接口区」，搜索 `【接口` 即可定位。

| 编号 | 接口 | 作用 |
|------|------|------|
| 1 | `\LectureClass` / `\LectureClassOptions` | 文档类与选项（book / report / article） |
| 2 | `\CourseTitle` 等 4 项 | 封面标题、副标题、作者、日期 |
| 3 | `\ThemeRed/Green/Blue` | 主题色 RGB |
| 4 | `\MarginLeft` 等 4 项 | 页面边距 |
| 5 | `\ChapterWord` | 章节称谓（章 / Chapter） |
| 6 | `\NameDefinition` 等 | 定理环境显示名 |
| 7 | `\showanswertrue/false` | 习题解答开关 |
| 8 | `\BibTitle` / `\IndexTitle` | 参考文献与索引标题 |

文献条目在文件开头 `filecontents*` 块内，直接增删即可，无需另建 `.bib`。

## 正文写作约定

正文写在「正文区」（搜索 `正文区` 定位）。可用环境：

- `definition` / `example` / `exercise` / `theorem` / `lemma` / `corollary` / `proposition`
- `proof`
- `solution`（受接口 7 控制） / `solution*`（始终显示）
- 命令 `\mypart{篇名}{篇导言}`

正文中**不要**写 `\documentclass`、`\usepackage`、`\begin{document}`、`\printbibliography`、`\printindex`——这些由模板机制统一处理。

## 自定义建议

- 换教材：整段替换「正文区」，其余不动。
- 换配色：改接口 3 的 RGB 值，全局主题色自动同步。
- 出练习版：把接口 7 切到 `\showanswerfalse` 重编译。隐藏态下 `solution` 内的 `\label` 不会定义，正文若需 `\ref` 请改用 `solution*` 或把标签移出。
- 换字体：改 `ctex` 宏包调用；若触发字体警告，在 `silence` 的 `WarningFilter` 处追加即可。

## 许可

MIT，详见 [LICENSE](LICENSE)。
