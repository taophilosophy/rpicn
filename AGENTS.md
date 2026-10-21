# AGENTS.md

本文件为 AI 编码代理（Claude Code、ZCode 等）在本仓库工作时提供指导。

> **当前进度快照（2026-10-21 13:30）：**
>
> - 全部 52 页已于 2026-10-20 同步至上游 `master`（上一基线 1b7709f / 2024.9.8）；CP-0 至 CP-4 全部通过。
> - **三轮逐句校对 + 复查：52/52 完成（100%）**——树莓派 17/17、配件 20/20、微控制器 6/6、服务 4/4、安全 5/5。本阶段已结束，逐页任务书 `TASKS.md` 已于 2026-10-21 删除，进度以本快照与 `CHANGELOG.md` 为准。
> - 全仓工程项已清零：CRLF、图片引用 `../` 前缀（368 处）、提示块空格（80 处）、正文直引号（29 处）、失效锚点（系统配置页 59 处等）、日式引号（2026-10-20 新规：禁止「」『』）。

## 下次同步上游时怎么做（按需 diff 增量增补）

本仓库**不保存上游 AsciiDoc 副本**（原 `script/upstream-*/` 基准目录已删除）。每次同步时临时拉取上游仓库，用 `git diff` 找出旧基线以来的改动，**只增补受影响的中文页**，不做全量重译。

### 第 1 步：确定旧基线

读 `CHANGELOG.md` 末尾最近一条「同步至 `<commit>`」记录，记为 `BASE`。日志中没有 commit 时，用 `README.md`「版本说明」里的基线链接。

### 第 2 步：拉取上游（只在临时目录，严禁写进仓库）

```bash
cd /tmp                                    # 或任一系统临时目录
git clone --filter=blob:none --no-checkout --depth 300 \
  https://github.com/raspberrypi/documentation.git up-doc
cd up-doc
git sparse-checkout set documentation/asciidoc
git checkout master
```

- 只认 `master`（对应官方已发布页面）；`develop` 含未发布内容，不得作为同步基准。
- 官方文档网页（raspberrypi.com/documentation）受 Cloudflare 挑战，`curl` 抓不动；单文件核对可用 `raw.githubusercontent.com`（已验证 52 个上游文件全部可达）。
- 若 `BASE` 过老被 shallow 克隆裁掉：`git fetch --deepen=300`，必要时 `git fetch --unshallow`。

### 第 3 步：生成差异清单

```bash
git diff --stat BASE..HEAD -- documentation/asciidoc
git diff --name-status BASE..HEAD -- documentation/asciidoc
```

抄下所有改动的 `.adoc` 路径（A=新增、M=修改、D=删除、R=重命名）。上游平时变动很小；若输出只有文件顺序调整（重命名到同内容），可跳过。

### 第 4 步：用映射表定位中文页

上游路径规则：`documentation/asciidoc/<板块>/<页面>.adoc`，该页拆分的子文件在**同名子目录**下（`<页面>/*.adoc`），由主文件 `include::` 引用。逐句比对时须把子文件按 include 顺序拼接后对照中文页。

| 中文页 | 上游 `asciidoc/` 下路径 |
| --- | --- |
| `shu-mei-pai/ru-men.md` | `computers/getting-started.adoc` |
| `shu-mei-pai/raspberry-pi-os.md` | `computers/os.adoc` |
| `shu-mei-pai/xi-tong-pei-zhi.md` | `computers/configuration.adoc` |
| `shu-mei-pai/config.txt.md` | `computers/config_txt.adoc` |
| `shu-mei-pai/linux-nei-he.md` | `computers/linux_kernel.adoc` |
| `shu-mei-pai/yuan-cheng-fang-wen.md` | `computers/remote-access.adoc` |
| `shu-mei-pai/she-xiang-tou-ruan-jian.md` | `computers/camera_software.adoc` |
| `shu-mei-pai/ren-gong-zhi-neng-ruan-jian.md` | `computers/ai.adoc` |
| `shu-mei-pai/shu-mei-pai-ying-jian.md` | `computers/raspberry-pi.adoc` |
| `shu-mei-pai/ling-dian-xing-hao.md` | `computers/zero.adoc` |
| `shu-mei-pai/ji-suan-mo-kuai-ying-jian.md` | `computers/compute-module.adoc` |
| `shu-mei-pai/chu-li-qi.md` | `computers/processors.adoc` |
| `shu-mei-pai/io-kong-zhi-qi.md` | `computers/io-controllers.adoc` |
| `shu-mei-pai/ruan-jian-lai-yuan.md` | `computers/software-sources.adoc` |
| `shu-mei-pai/jiu-ban-config.txt-can-shu.md` | `computers/legacy_config_txt.adoc` |
| `shu-mei-pai/jing-dian-dan-ban-ji-suan-ji.md` | `computers/sbcs.adoc` |
| `shu-mei-pai/jian-pan-ji-suan-ji.md` | `computers/keyboard-computers.adoc` |
| `pei-jian/sd-ka.md` | `accessories/sd-cards.adoc` |
| `pei-jian/ssd.md` | `accessories/ssds.adoc` |
| `pei-jian/ssd-tao-jian.md` | `accessories/ssd-kit.adoc` |
| `pei-jian/m.2-hat+.md` | `accessories/m2-hat-plus.adoc` |
| `pei-jian/xian-shi-qi.md` | `accessories/display.adoc` |
| `pei-jian/chu-mo-xian-shi-ping-2.md` | `accessories/touch-display-2.adoc` |
| `pei-jian/raspberry-pi-monitor.md` | `accessories/monitor.adoc` |
| `pei-jian/she-xiang-tou.md` | `accessories/camera.adoc` |
| `pei-jian/ai-she-xiang-tou.md` | `accessories/ai-camera.adoc` |
| `pei-jian/jian-pan-he-shu-biao.md` | `accessories/keyboard-and-mouse.adoc` |
| `pei-jian/usb-pei-jian.md` | `accessories/usb.adoc` |
| `pei-jian/build-hat.md` | `accessories/build-hat.adoc` |
| `pei-jian/chuan-gan-qi-kuo-zhan-ban-sense-hat.md` | `accessories/sense-hat.adoc` |
| `pei-jian/ren-gong-zhi-neng-tao-jian-ai-kit.md` | `accessories/ai-kit.adoc` |
| `pei-jian/ai-hat.md` | `accessories/ai-hat-plus.adoc` |
| `pei-jian/shu-mei-pai-yin-pin-kuo-zhan-ban-raspberry-pi-audio-board.md` | `accessories/audio.adoc` |
| `pei-jian/dian-shi-kuo-zhan-ban-tv-hat.md` | `accessories/tv-hat.adoc` |
| `pei-jian/cm5-bian-cheng-zhi-ju.md` | `accessories/cm5-programming-jig.adoc` |
| `pei-jian/zhi-neng-xian-shi-mo-kuai.md` | `accessories/smart-display-module.adoc` |
| `pei-jian/bao-hu-ke.md` | `accessories/bumper.adoc` |
| `wei-kong-zhi-qi/wu-xian-dian-mo-kuai.md` | `microcontrollers/radio-modules.adoc` |
| `wei-kong-zhi-qi/rp2040.md` | `microcontrollers/microcontroller-chips.adoc` |
| `wei-kong-zhi-qi/shu-mei-pai-pico-he-pico-w.md` | `microcontrollers/pico-series.adoc` |
| `wei-kong-zhi-qi/shu-mei-pai-tiao-shi-tao-jian-raspberry-pi-debug-probe.md` | `microcontrollers/debug-probe.adoc` |
| `wei-kong-zhi-qi/micropython.md` | `microcontrollers/micropython.adoc` |
| `wei-kong-zhi-qi/c-c++-sdk.md` | `microcontrollers/c_sdk.adoc` |
| `fu-wu/shu-mei-pai-zhang-hao-raspberry-pi-id.md` | `services/id.adoc` |
| `fu-wu/shu-mei-pai-yuan-cheng-fang-wen-raspberry-pi-connect.md` | `services/connect.adoc` |
| `fu-wu/shu-mei-pai-connect-qi-ye-ban.md` | `services/connect-for-organisations.adoc` |
| `fu-wu/shu-mei-pai-shu-jia.md` | `services/bookshelf.adoc` |
| `an-quan/an-quan-gai-shu.md` | `security/security.adoc` |
| `an-quan/an-quan-jia-gou.md` | `security/security-architecture.adoc` |
| `an-quan/an-quan-qi-dong-pei-zhi-qi.md` | `security/secure-boot-provisioner.adoc` |
| `an-quan/yun-ying-an-quan.md` | `security/operational-security.adoc` |
| `an-quan/ufw-fang-huo-qiang.md` | `security/ufw.adoc` |

diff 里出现上表没有的路径（上游新增/重命名页面）时：先读主文件确认内容归属，再决定映射到哪一页，**并把新映射补进本表**。

### 第 5 步：增量增补（只处理 diff 命中的页）

对每个受影响的中文页：

1. 读上游新版全文（主文件 + 按 `include::` 顺序拼接子文件），与中文页逐句比对，**只改有差异的部分**，不做无关重构。
2. 上游笔误（拼写错误、自相矛盾的参数、错位的表格）按正确含义译出，记入异常清单；照录的丝印/截图文法除外（如 `WiFI/BT`）。
3. 遵守本文件「编写规范」全部条款（提示块、反引号、禁日式引号、禁 AsciiDoc 残留、表格列数等）。
4. 上游**新增**页面 → 新增中文页（拼音命名，不得含空格/中文/冒号）+ `SUMMARY.md` 条目 + `mu-lu.md` 卡片（板块内顺序与 `SUMMARY.md` 逐位一致，卡片图用上游 `images/full-sized/` 线上地址并验证 200）；上游**删除**页面 → 三处同步移除。
5. 上游改动涉及图片时：下载到 `.gitbook/assets/`，正文用 `](../.gitbook/assets/xxx.png)` 引用（子目录页面必须带 `../`）。

### 第 6 步：质量门禁（原 `script/lint_all.py` 已随 `script/` 删除，改用内联检查）

```bash
python - <<'EOF'
import re, glob, os
files = [f for d in ['shu-mei-pai','pei-jian','wei-kong-zhi-qi','fu-wu','an-quan','qian-yan'] for f in glob.glob(d+'/*.md')]
def strip_code(s):
    out, infence = [], False
    for l in s.split('\n'):
        if l.lstrip('> \t').startswith('```'): infence = not infence; continue
        if not infence: out.append(l)
    return '\n'.join(out)
bad = 0
for f in files:
    raw = open(f,'rb').read(); s = raw.decode('utf-8'); body = strip_code(s)
    probs = []
    if any(c in s for c in '「」『』'): probs.append('日式引号')
    if re.findall(r'xref:|link::|image::', body): probs.append('asciidoc残留')
    if len(re.findall(r'^```', s, re.M)) % 2: probs.append('围栏奇数')
    if body.count('“') != body.count('”'): probs.append('弯引号不配对')
    if [l for l in body.split('\n') if l.startswith('> ')]: probs.append('提示块空格')
    if [l for l in body.split('\n') if re.match(r'^#+ .*[。.]$', l)]: probs.append('标题句号')
    if raw.count(b'\n') != raw.count(b'\r\n'): probs.append('换行混合')
    for m in re.finditer(r'\]\((\.{0,2}\.gitbook/assets/[^)]+)\)', s):
        if not os.path.exists(os.path.normpath(os.path.join(os.path.dirname(f), m.group(1)))): probs.append('图片缺失:'+m.group(1)[:40])
    if probs: print(f, probs); bad += 1
print('交付页 %d 个，问题文件 %d 个' % (len(files), bad))
EOF
```

要求输出 `问题文件 0 个`。此外按需补查：表格列数一致性、页内锚点命中标题（slug 规则：标题去反引号/星号、保留英文下划线、空格转 `-`、全小写）、内部链接目标存在。

### 第 7 步：收尾登记

1. `CHANGELOG.md` 追加一条：日期、新基线 commit、改动页清单（每页修正数）、上游异常清单。
2. `README.md` 更新「版本说明」的基线链接；若为全量完成，更新「翻译校对进度」表。
3. 提交（本仓库要求 GPG 签名，Git 自带 gpg 无密钥库，须用系统 GnuPG）：
   ```bash
   git -c gpg.program="C:\Program Files\GnuPG\bin\gpg.exe" commit -m "同步上游至 <新commit>：<改动概述>"
   ```
4. 清理临时目录：`rm -rf /tmp/up-doc`。比对脚本与日志可留存于 `script/` 目录，但**不得把上游 adoc 副本（`upstream-*`）提交进仓库**——它们可由 `git diff` 随时重新定位，入库只会造成重复维护。

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
- 网页转 Markdown 推荐使用思源笔记，少数页面需用 Marktext 兜底；Typora、Obsidian 效果不佳。
- **禁止使用 DeepL 进行任何英中翻译**：DeepL 会吞字、吞句，甚至把整句意思翻译反，对技术文档是致命错误。
- 树莓派官方文档平时变动很小（只在每个版本发布后的半年内较活跃，且大量提交只是调整文件顺序、每次只改几个字）。同步前先确认实际内容差异，避免无效劳动。
- **GitHub 提交数严重虚高**：上游每篇文档被拆成数百个 adoc 子文件，大量提交只是调整文件顺序，一个字也没改。不得把「提交数很多」判断为「有实质改动」，也不得逐个对照散装 adoc 子文件人工通读——那是多余劳动。
- **git diff 只是定位工具**：本文档「下次同步上游」七步流程用 `git diff BASE..HEAD` 从上游 GitHub 仓库快速定位真实改动的文件；定位之后，仍要以官方网页生成的内容为权威依据完成翻译，**不得直接对着 `develop` 分支或散装 adoc 做译文**。
- **翻译工具禁令**：严禁使用 DeepL 进行任何英中翻译——它会吞字、吞句（长文本会跳过整句），且常把整句意思译反，对技术文档是致命错误（0 和 1 没有辩证法）。人工翻译或使用可信的大模型辅助后必须逐句对照原文复核。

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
| `shu-mei-pai/` | `documentation/asciidoc/computers/` | 17 | 入门、系统、远程访问、硬件、AI 软件、Zero、SBC、键盘计算机、计算模块、处理器、I/O 控制器、软件来源 |
| `pei-jian/` | `documentation/asciidoc/accessories/` | 20 | SD 卡、SSD、显示屏、摄像头、AI 摄像头、键盘鼠标、USB、各类 HAT、编程治具、Bumper |
| `wei-kong-zhi-qi/` | `documentation/asciidoc/microcontrollers/` | 5 | 芯片、Pico、调试套件、MicroPython、C/C++ SDK |
| `fu-wu/` | `documentation/asciidoc/services/` | 4 | Raspberry Pi ID、Connect、Connect 企业版、书架 |
| `an-quan/` | `documentation/asciidoc/security/` | 5 | 安全概述、安全架构、安全启动配置器、运营安全、UFW |

- 每页为独立 `.md` 文件，与上游顶级页面 1:1 对应。上游拆分的子页面在中文版合并为单页：上游子页 `.adoc` → 中文 H2（`##`），子页内 `===` → H3（`###`），`====` → H4（`####`）。
- 文件命名使用拼音 slug，不得包含空格、中文字符或英文冒号 `:`，必须兼容 Windows 对文件名的要求。
- `.gitbook/assets/` — 本地化图片（约 70 张），正文插图使用相对路径引用（如 `.gitbook/assets/xxx.png`）。新增图片优先本地化到此目录；仍指向 www.raspberrypi.com 的历史遗留图片，在修订对应页面时逐步本地化。
- 中文页面与上游子页的层级对应关系用临时脚本核对，脚本与日志放在 `script/` 目录（该目录当前不存在，需要时创建）。

### 标题管理（关键约束）

- 各 `.md` 文件的 H1 由 `sync-headers.yml` CI 自动与 `SUMMARY.md` 中对应条目的文字保持一致；修改章节标题时，需同时更新 `SUMMARY.md` 条目与 `mu-lu.md` 卡片文字（文件 H1 由 CI 自动同步）。

## 编写规范

### 格式

- **代码块：** 与上游原文保持一致，禁止篡改命令、配置内容、软件版本号。代码块内的英文注释翻译为中文（如 `# This is a comment` → `# 这是一个注释`），代码结构和格式不变。shell 命令用 `bash` 或 `sh` 围栏标记，其余按内容选语言（`json`、`c`、`python`、`cpp`、`csharp`、`php` 等）；无法判断时用不带语言标注的围栏，禁止使用 `text` 作为代码块标记。上游使用 `sudo` 的命令原样保留（树莓派文档惯例，与 FreeBSD 手册项目"禁用 sudo"的规则相反）。
- **命令行前缀：** `#` 表示 root 权限，`$` 表示普通用户。
- **提示块：** 使用 `>` 缩进引用，关键词加粗，`>` 后不留空格，与既有文件风格一致：`>**技巧**`、`>**注意**`、`>**重要**`、`>**警告**`（对应上游 tip/note/important/warning）。
- **命令、选项、参数、文件路径：** 一律用反引号包裹（如 `/boot/firmware`、`config.txt`、`raspi-config`）。不带选项和参数的裸命令（如 mv、cp）一般不加反引号。**注意：本项目路径用反引号而非加粗，与 FreeBSD 手册项目的规则相反，勿跨项目套用。**
- **表格：** 风格与所在文件既有表格保持一致（内容列一般左对齐，短枚举列居中）；`mu-lu.md` 的卡片表格一律居中。表头声明几列，所有数据行就必须有几列，缺的补空单元格，不得让单元格超出表头列数（超出部分在 GFM 渲染中被丢弃）。
- **HTML：** 正文页面禁止成段的 HTML（div、table 等）；`<br>` 换行是既有用法，可保留；`mu-lu.md` 是唯一例外。
- **禁止日式引号（2026-10-20 新增，用户明令）：** 正文中不允许出现任何日式/直角引号——「」（单层）与『』（双层）一律禁止，统一使用""（中文双引号）或''（中文单引号）。此规则适用于全部交付页面与工作记录文件（CHANGELOG.md 等自本规则生效起的新增内容）。逐个手动修改，禁止机械替换。
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
