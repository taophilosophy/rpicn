# AGENTS.md

本文件为 AI 编码代理（Claude Code、ZCode 等）在本仓库工作时提供指导。

## 仓库概览

这是树莓派官方文档（Raspberry Pi Documentation）的简体中文翻译项目。基于 GitBook 格式，由 GitBook 平台自动构建和部署，无需本地构建步骤。

- 本项目开源地址：<https://github.com/taophilosophy/rpicn>（由 FreeBSD 中文社区发起）
- 英文原版存储库：<https://github.com/raspberrypi/documentation>
- 翻译对照的官方文档页面：<https://www.raspberrypi.com/documentation/>
- 授权协议：CC BY-SA 4.0（与上游一致，详见 `README.md`"版权说明"）

本仓库配有完整的 GitHub Actions 自动化（`.github/workflows/`）：`sync-headers.yml` 自动把各页面 H1 同步为 `SUMMARY.md` 中的条目文字；`Markdown-lint2-pr.yml` 在 PR 时检查变更的 `.md` 文件；`check-images.yml` 检查图片引用；`file-name-check.yml` 检查 `SUMMARY.md` 目录；另有链接检查、AutoCorrect、md-padding、PDF 导出、issue/PR 自动分配等工作流（部分为手动触发）。术语规则和格式惯例与 FreeBSD 手册翻译项目（handbook.bsdcn.org）在多处相反（如路径包裹方式），勿跨项目套用。

## 版本与流程

当前翻译同步基线（英文原版 commit）：
<https://github.com/raspberrypi/documentation/commit/1b7709fea907aed7af8950f936ccfd1b82a29edd>（官方文档 2024.9.8 版本）

同步历史（详见 `CHANGELOG.md`）：

- 2024.6.5 同步至 f0511a225236d2defc8c12010c315827cb3baf7d
- 2024.7.11 同步至 b68a629c7212e668fdfba94d227cc9ec32d9bfbb
- 2024.9.8 同步至 1b7709fea907aed7af8950f936ccfd1b82a29edd（当前基线）

截至当前基线，英文原版位于上游仓库 `documentation/asciidoc/` 下，按板块分为 `computers/`、`accessories/`、`microcontrollers/`、`services/` 四个目录；每个页面被上游拆分为多个 `.adoc` 子文件（如 `computers/os/using-gpio.adoc`）。

### 原文获取（重要）

- **以官方文档网页为权威源**：<https://www.raspberrypi.com/documentation/>。官方页面由上游 `master` 分支生成；GitHub 默认分支 `develop` 包含未发布改动，不要对着 `develop` 分支或 GitHub 上的 adoc 散文件翻译。
- 本项目维护的英文 Markdown 原文存档：<https://github.com/taophilosophy/rpi-documentation-diff/>。同步上游时，用官方网页生成新的 Markdown 存档，与旧存档对比得到实际内容差异（GitHub 会自动生成对比视图）。
- 网页转 Markdown 推荐使用思源笔记，少数页面需用 Marktext 兜底；Typora、Obsidian 效果不佳（详见 `CONTRIBUTING.md`）。
- **禁止使用 DeepL 进行任何英中翻译**：DeepL 会吞字、吞句，甚至把整句意思翻译反，对技术文档是致命错误（详见 `CONTRIBUTING.md`）。
- 树莓派官方文档平时变动很小（只在每个版本发布后的半年内较活跃，且大量提交只是调整文件顺序、每次只改几个字）。同步前先确认实际内容差异，避免无效劳动。

### 相关上游项目

本项目同时维护树莓派启动盘制作工具（Raspberry Pi Imager）的简体中文翻译，通过 PR 提交至 <https://github.com/raspberrypi/rpi-imager>（历史记录见 `CHANGELOG.md`）。发现官方文档本身的错误（命令错误、排版问题等）时，应向上游提交 PR 或 issue，并在 `CHANGELOG.md` 记录。

## 内容架构

### 核心文件

- **`SUMMARY.md`** — 全书唯一数据源，定义完整目录结构和导航树，GitBook 用它生成侧边栏。**第一行 `# Table of contents` 绝对不能变更**，否则 GitBook 同步失效。
- **`mu-lu.md`** — 手工维护的可视化目录页（卡片式表格，含配图和简介）。**它不是由 `SUMMARY.md` 自动生成的**，`SUMMARY.md` 新增、删除或改标题时必须手工同步对应卡片（链接、图片、说明文字）。`mu-lu.md` 是本仓库唯一大量使用 HTML（`<a>`、`<img>`、`<br>`）的文件。
- **`qian-yan/ci-hui-biao.md`** — 术语翻译对照表（词汇表），所有术语翻译以此为准。新出现的人名、专有名词必须登记进词汇表。
- **`CHANGELOG.md`** — 编辑日志。每完成一次上游同步或整页校对，追加一条记录（日期、同步的 commit、完成内容、向上游反馈的 PR）。
- **`CONTRIBUTING.md`** — 贡献指南，是原文获取方式、工具选择、DeepL 禁令等约定的权威来源。
- **`README.md`** — 项目说明。上游同步后需更新其中"版本说明"一节的指向。

### 目录结构

| 目录 | 对应上游板块 | 页数 | 内容 |
| ---- | ------------ | ---- | ---- |
| `qian-yan/` | （项目自有页面） | 3 | 词汇表、关于我们、版权说明 |
| `shu-mei-pai/` | `documentation/asciidoc/computers/` | 11 | 入门至处理器 |
| `pei-jian/` | `documentation/asciidoc/accessories/` | 9 | 摄像头至音频扩展板 |
| `wei-kong-zhi-qi/` | `documentation/asciidoc/microcontrollers/` | 5 | 芯片至 C/C++ SDK |
| `fu-wu/` | `documentation/asciidoc/services/` | 2 | Raspberry Pi ID、Connect |

- 每页为独立 `.md` 文件，与上游 27 个顶级页面 1:1 对应。上游拆分的子页面在中文版合并为单页：上游子页 `.adoc` → 中文 H2（`##`），子页内 `===` → H3（`###`），`====` → H4（`####`）。
- 文件命名使用拼音 slug，不得包含空格、中文字符或英文冒号 `:`，必须兼容 Windows 对文件名的要求。
- `.gitbook/assets/` — 本地化图片（约 70 张），正文插图使用相对路径引用（如 `.gitbook/assets/xxx.png`）。新增图片优先本地化到此目录；仍指向 www.raspberrypi.com 的历史遗留图片，在修订对应页面时逐步本地化。
- 中文页面与上游子页的层级对应关系用临时脚本核对，脚本与日志放在 `script/` 目录（该目录当前不存在，需要时创建）。

### 标题管理（关键约束）

- 各 `.md` 文件的 H1 由 `sync-headers.yml` CI 自动与 `SUMMARY.md` 中对应条目的文字保持一致；修改章节标题时，需同时更新 `SUMMARY.md` 条目与 `mu-lu.md` 卡片文字（文件 H1 由 CI 自动同步）。

## 编写规范

### 格式

- **代码块：** 与上游原文保持一致，禁止篡改命令、配置内容、软件版本号。代码块内的英文注释翻译为中文（如 `# This is a comment` → `# 这是一个注释`），代码结构和格式不变。shell 命令用 `bash` 或 `sh` 围栏标记，其余按内容选语言（`json`、`c`、`python`、`cpp`、`csharp`、`php` 等）；无法判断时用无语言标注的 ` ``` ` 兜底，禁止使用 `text` 作为代码块标记。上游使用 `sudo` 的命令原样保留（树莓派文档惯例，与 FreeBSD 手册项目"禁用 sudo"的规则相反）。
- **命令行前缀：** `#` 表示 root 权限，`$` 表示普通用户。
- **提示块：** 使用 `>` 缩进引用，关键词加粗，`>` 后不留空格，与既有文件风格一致：`>**技巧**`、`>**注意**`、`>**重要**`、`>**警告**`（对应上游 tip/note/important/warning）。
- **命令、选项、参数、文件路径：** 一律用反引号包裹（如 `/boot/firmware`、`config.txt`、`raspi-config`）。不带选项和参数的裸命令（如 mv、cp）一般不加反引号。**注意：本项目路径用反引号而非加粗，与 FreeBSD 手册项目的规则相反，勿跨项目套用。**
- **表格：** 风格与所在文件既有表格保持一致（内容列一般左对齐，短枚举列居中）；`mu-lu.md` 的卡片表格一律居中。表头声明几列，所有数据行就必须有几列，缺的补空单元格，不得让单元格超出表头列数（超出部分在 GFM 渲染中被丢弃）。
- **HTML：** 正文页面禁止成段的 HTML（div、table 等）；`<br>` 换行是既有用法，可保留；`mu-lu.md` 是唯一例外。
- **禁止「」引号：** 正文中不允许出现「」，一律使用""（中文双引号）。逐个手动修改，禁止机械替换。
- **禁止 AsciiDoc 语法残留：** 不允许出现 `xref:file[文本]`、`link:file[文本]` 等双冒号链接语法和行尾 `+` 软换行；所有段落必须在同一行内完成，不得跨行拼接。链接一律使用标准 markdown `[文本](路径或URL)`。
- **禁止篡改：** 软件版本号、用户名、邮箱、URL、IP 地址、带圈数字（如 ①②③）必须与英文原文保持一致，其位置和数量不得变动。
- **避免滥用"已"字：** 如"XX 已新增"应改为"新增 XX"；"已修复"应改为"修复完成"。禁止机械替换。
- **避免章节交叉引用：** 正文不要出现"参见第 X 节"式的硬编码引用。站内引用用相对 markdown 链接指向对应中文页面；指向尚未翻译的内容时，可直接使用官方英文文档 URL（含锚点，如 `https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#gpio`）。
- **图片：** 正文插图使用 markdown 格式（`![说明](路径)`）。
- **第二人称：** 一律使用"你"而非"您"。

### 术语

- 所有术语以 `qian-yan/ci-hui-biao.md` 词汇表为准，常用译法：Raspberry Pi OS → 树莓派系统；HAT → 扩展板；Compute Module → 计算模块；Camera Module → 摄像头模块；Raspberry Pi Imager → 树莓派启动盘制作工具；microSD → 存储卡；Legacy → 旧版；boot partition → 启动分区。
- 产品名、型号、软件名保持英文原样：Raspberry Pi、Pico、RP2040、RP2350、RP1、MicroPython、Thonny、rpicam-apps（不翻译，是 GitHub 存储库名）等。
- "拷贝" → "复制"；"壳/外壳" → "shell"。禁止机械替换。
- 新术语先查词汇表；词汇表没有的，确定译法后先补录进词汇表，再在正文使用。

### CJK 空格

中英文、中文与数字之间必须加半角空格。文件和命令名用反引号括起来。可使用 AutoCorrect 工具检查（见"本地工具"）。

## 翻译校对工作流程（AI 代理）

对已翻译页面进行质量审校时，参考以下步骤：

1. **获取原文**：以官方文档网页（`https://www.raspberrypi.com/documentation/<板块>/<页面>.html`，板块为 computers/accessories/microcontrollers/services）为唯一权威源，或使用 `rpi-documentation-diff` 存档；需要核查细节时才参考上游 GitHub 仓库对应 `.adoc`（`master` 分支）。**禁止以中文版已有翻译作为修改依据**，避免错误沿袭。

2. **逐句对照**：将中文翻译与英文原文逐句比对，重点检查以下问题类别：

   | 问题类型 | 示例 |
   | -------- | ---- |
   | 事实性错误 | "large parts" 误译为"三个文件" |
   | 漏译 | 英文原版有但中文缺失的句子或小节 |
   | 机翻腔/表达生硬 | "将被自动安装" → "会自动安装" |
   | 用词不当 | "独家优势"应为"主要优势"（原文 "particular strengths"） |
   | 版本过时 | 软件版本号、型号未同步至英文原版当前版本 |
   | 语法/文字错误 | 重复字词、"非常地"应为"非常" |
   | 欧化汉语、倒装句、后置句、偷换主语、不必要的被动句 | 自行联网制定标准，避免语法错误和非地道汉语表述 |

3. **提交修改**：
   - 基于 `main` 创建分支（如 `fix/<拼音页面名>`）
   - 仅提交修改的 `.md` 文件，不要包含无关文件
   - 提交信息用中文简述变更（现有历史风格如"更新 raspberry-pi-os.md"）
   - PR 目标分支为 `main`，描述中列出每处修改及原因

4. **注意事项**：
   - 比较必须基于 diff：先用 diff 确定相对上一版的实际改动范围，再逐句对照，禁止凭印象或抽样判断
   - 英文原文可能比翻译版本新，版本号等差异以英文原版为准
   - 禁止篡改代码块（包括 shell 命令、配置文件内容等），仅翻译注释
   - 保持术语一致性，参考 `qian-yan/ci-hui-biao.md`
   - 修改标题需同步 `SUMMARY.md` 与 `mu-lu.md`
   - 添加新内容（如英文原版新增的段落）时，确保翻译风格与上下文一致

5. **逐句校对递归工作流**（核心约束）：
   - **逐行逐句子**遍历内容，检查逻辑一致性，联网复核后修改
   - **三轮 + 一轮复查**：完整执行三轮逐句校对，然后严格、完整地复查一轮；若仍有问题，继续执行三轮，递归直至无问题
   - **逐个修改**：修改时禁止机械修改、禁止批量；必须逐个手动修改，禁止使用软件工具批量替换或批量逐个复核
   - **修改前后复核**：每次修改前确认问题真实存在、修改后确认改动准确且未引入新错误
   - **不复查旧错**：不得复查以前已经完成三轮的错误；每轮查询内容必须是新的（若与之前的复查重复则跳过、不改，只看是否有新增内容）
   - **联网复查**：对于不存在的实际访问查询（如失效链接、版本号、API 端点），需联网复查三次后修改
   - **禁止绕过审查**：不得以任何方式搜索、批量、绕过逐句子审查流程

## 同步上游工作流

英文原版更新时的操作流程：

1. 确定目标 commit（官方网页当日的 `master` 分支 commit），记录到 `CHANGELOG.md`。
2. 用思源笔记（或 Marktext）将官方网页逐页另存为 Markdown，更新 `rpi-documentation-diff` 存档库。
3. 用 diff 逐行对比新旧存档（如 `git diff`、GitHub 对比视图、思源笔记/Marktext 的文档对比功能），得到实际内容差异；**比较必须基于 diff，禁止凭印象、抽样或仅统计数量**。
4. 将差异逐句翻译并合并进对应中文 `.md` 文件；禁止使用 DeepL。
5. 上游结构变化处理：
   - **新增页面**：在对应目录新建拼音 slug 的 `.md` 文件，在 `SUMMARY.md` 对应位置插入条目，在 `mu-lu.md` 添加卡片（可选用上游 `documentation/images/full-sized/` 下的官方配图），新术语登记进词汇表。
   - **删除页面**：反向操作，并清理 `mu-lu.md` 卡片与失效图片。
   - **新增子节**：在对应中文页添加 H2/H3，层级按"上游子页 `.adoc` → H2、`===` → H3"对应。
6. 更新 `README.md`"版本说明"指向，在 `CHANGELOG.md` 追加记录。
7. 校验：核对上游每个子页面在中文页中都有对应的 H2/H3 小节（可用临时脚本生成两侧标题清单的 diff 再逐项核对，脚本放 `script/` 目录）。

## 本地工具

- **AutoCorrect**（`.github/.autocorrectrc`，根目录另有一份 `.autocorrectrc`）：仅启用 `space-word`（CJK 与英文/数字间空格，error 级）；标点、括号、反引号、全半角转换、拼写检查等其余规则全部关闭。`AutoCorrect.yml` 与 `md-padding.yml` 为手动触发，运行后必须逐文件核对 diff 再提交，禁止盲目批量应用。
- **markdownlint**（`.github/.markdownlint.json`）：PR 时由 `Markdown-lint2-pr.yml` 自动检查变更的 `.md` 文件；**lychee**（`.github/lychee.toml`）由 `links.yml` 定期检查链接；textlint 未配置。
- PDF 导出：`create-pdf.yml` 工作流，或使用 `README.md` 提到的 [gitbook-pdf-export](https://github.com/FreeBSD-Ask/gitbook-pdf-export) 脚本。
