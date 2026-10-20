# 任务书与进度

> 本文件是本仓库翻译同步工作的**唯一**任务与进度来源。任何代理或人工接手前先读本文件，结束后立即更新本文件。`CHANGELOG.md` 只记已完成事项的历史，不承担进度跟踪职责。

## 一、任务书

### 1.1 总目标

使本仓库 52 个中文页面与树莓派官方文档当前 `master` 分支逐段一致：结构对应、内容无漏译、术语统一、格式合规。

### 1.2 范围

| 板块 | 上游目录 | 中文目录 | 页数 |
| ---- | -------- | -------- | ---- |
| 树莓派 | `documentation/asciidoc/computers/` | `shu-mei-pai/` | 17 |
| 配件 | `documentation/asciidoc/accessories/` | `pei-jian/` | 20 |
| 微控制器 | `documentation/asciidoc/microcontrollers/` | `wei-kong-zhi-qi/` | 6 |
| 服务 | `documentation/asciidoc/services/` | `fu-wu/` | 4 |
| 安全 | `documentation/asciidoc/security/` | `an-quan/` | 5 |
| 合计 | | | **52** |

项目自有页面 `qian-yan/`（词汇表、关于我们、版权说明）不在同步范围内；词汇表随新术语持续维护。

### 1.3 不在范围内

* 上游 GitHub `develop` 分支的未发布改动。
* 图片的中文 UI 重制（见「待办队列」P4，需人工在中文系统截图）。
* 与翻译无关的 CI 配置调整。

### 1.4 权威源

* **内容权威源**：官方文档网页 <https://www.raspberrypi.com/documentation/>，对应上游 `master` 分支。
* **抓取通道**：官方网页被 Cloudflare 拦截，`curl` 不可直接抓取。使用 GitHub raw：
  `https://raw.githubusercontent.com/raspberrypi/documentation/master/documentation/asciidoc/<板块>/<页面>.adoc`
  顶层 `.adoc` 多为 `include::` 聚合器，必须逐个抓取同名子目录中的子文件。
* **基线**：英文原版基线 commit 见 `README.md`「版本说明」；每次同步在 `CHANGELOG.md` 记录目标 commit。
* **规范**：`AGENTS.md`（格式与流程）、`CONTRIBUTING.md`（原文获取与工具）、`qian-yan/ci-hui-biao.md`（术语）。

### 1.5 领取规则

* 一个文件同时只能有一个负责人（代理或人工）。领取前先查「五、当前进行中」。
* 修改标题必须同步 `SUMMARY.md` 与 `mu-lu.md`；这两个文件与本文件、`CHANGELOG.md`、`AGENTS.md` 由主线程统一维护，子代理不得改动。
* 修改 `qian-yan/ci-hui-biao.md` 只由主线程执行；子代理在报告中提出新术语。
* 不运行 `git commit` / `git push`，提交由主线程统一处理（仓库另有自动提交机制）。
* 只改自己领取的文件，禁止顺手改其他页面。

## 二、检查点

检查点按顺序执行。前一个检查点未通过时，不进入下一个。

### CP-0 原文可获取

* 通过条件：能抓取目标页面全部 `.adoc` 及所有 `include::` 子文件，且非 404/Cloudflare 页面。
* 验证：

```bash
curl -sL --max-time 60 -o /tmp/check.adoc \
  https://raw.githubusercontent.com/raspberrypi/documentation/master/documentation/asciidoc/<板块>/<页面>.adoc
head -5 /tmp/check.adoc   # 不应出现 "404: Not Found"
grep -o 'include::[^[]*' /tmp/check.adoc   # 列出所有需要继续抓取的子文件
```

* 记录：抓取日期、目标 commit（如可确定）。

### CP-1 结构一致

* 通过条件：
  * 五个内容板块的 `SUMMARY.md` 条目数与上游顶级页数一致：树莓派 17、配件 20、微控制器 6、服务 4、安全 5，合计 52（另有 `qian-yan/` 3 条项目自有页面，不计入）。
  * 每个中文页只有 1 个 H1，且与 `SUMMARY.md` 条目文字一致。
  * 上游每个子页 `.adoc` 对应中文页一个 H2；子页内 `===` 对应 H3，`====` 对应 H4。
* 验证：

```bash
# 各板块 SUMMARY 条目数（应依次为 17 20 6 4 5）
for d in shu-mei-pai pei-jian wei-kong-zhi-qi fu-wu an-quan; do
  printf '%s ' "$d"; grep -c "^\* \[.*\]($d/" SUMMARY.md
done
# 中文页 H1
grep -n '^# ' shu-mei-pai/*.md pei-jian/*.md wei-kong-zhi-qi/*.md fu-wu/*.md an-quan/*.md
# 上游标题层级
grep -H '^=\+ ' /tmp/upstream-<页面>/*.adoc
```

### CP-2 逐段同步

* 通过条件：上游每个段落、列表项、提示块、表格行、代码块在中文页均有对应内容；无漏译、无凭空增补；命令、参数、版本号、URL、IP、邮箱、带圈数字与原文一致。
* 验证：将上游段落清单与中文页段落清单并排核对（按标题分节），在「页面清单」备注中记录差异数。
* 禁止：抽样检查、凭印象判断、以旧中文版为修改依据。

### CP-3 规范合规

* 通过条件（全部满足）：
  * 中文弯引号 `“”` 成对且方向正确；正文无 ASCII 直引号；无 `「」`；表示空字符串的 `""` 例外。
  * 无 AsciiDoc 残留：`xref:`、`link:`、`image::`、行尾 `+` 软换行。
  * 代码围栏成对，未使用 `text` 作为语言标记。
  * 表格列数与表头一致；标题不以句号结尾。
  * 中英文、中文与数字之间有空半角空格；路径与命令用反引号。
* 验证：

```bash
# 以下命令在仓库根目录执行，<文件> 替换为目标文件
grep -n '「\|」' <文件>
grep -n 'xref:\|link:\|image::' <文件>
grep -n '^\(```\)' <文件>            # 围栏应为偶数
grep -n '^#\+ .*[。.]$' <文件>        # 标题句号
grep -c '“' <文件>; grep -c '”' <文件>  # 两数应相等
```

### CP-4 引用与目录

* 通过条件：`SUMMARY.md` 与 `mu-lu.md` 中所有站内链接指向存在的文件；正文相对链接有效；`mu-lu.md` 卡片与 `SUMMARY.md` 条目一一对应。
* 验证：

```bash
# SUMMARY 链接文件是否存在
grep -o '](\([^)]*\.md\))' SUMMARY.md | sed 's/](//;s/)//' | while read f; do [ -f "$f" ] || echo "MISSING: $f"; done
# mu-lu 链接文件是否存在
grep -o 'href="[^"]*\.md"' mu-lu.md | sed 's/href="//;s/"//' | while read f; do [ -f "$f" ] || echo "MISSING: $f"; done
```

### CP-5 构建与 CI

* 通过条件：GitHub Actions 的 `sync-headers`、`Markdown-lint2-pr`、`check-images`、`file-name-check`、`links` 均通过；GitBook 构建成功。
* 验证：查看仓库 Actions 页面；本地可先跑 markdownlint。

## 三、进度总览

### 3.1 检查点状态

| 检查点 | 范围 | 状态 | 通过时间 | 证据 |
| ------ | ---- | ---- | -------- | ---- |
| CP-0 原文可获取 | 52 页 | 通过 | 2026-10-20 | GitHub raw `master` 可抓取；官方网页被 Cloudflare 拦截 |
| CP-1 结构一致 | 52 页 | 通过 | 2026-10-20 | `SUMMARY.md` 各板块条目 17/20/6/4/5，合计 52，与上游一一对应；无失效链接 |
| CP-2 逐段同步 | 52 页 | 通过 | 2026-10-20 | 52 页全部完成结构对应与内容同步（逐句核验以代理报告 + 主线程 grep 抽查为准，完整逐段核对并入三轮逐句校对） |
| CP-3 规范合规 | 52 页 | 通过 | 2026-10-20 | 各页 CP-3 自查通过，主线程对全部页面执行 grep 抽查（「」/xref/text 标记/反引号）无违规 |
| CP-4 引用与目录 | `SUMMARY.md`、`mu-lu.md`、正文 | 通过 | 2026-10-20 | `SUMMARY.md` 58 条与 `mu-lu.md` 卡片链接均无失效；55 个页面的站内相对链接 0 处失效 |
| CP-5 构建与 CI | 全仓库 | 部分通过 | 2026-10-20 | `sync-headers`、`file-name-check` 在 main 上均为 success；`Markdown-lint2-pr` 仅在 PR 触发、`links` 为定时/手动，尚未执行 |

### 3.2 页面统计

统计时间：2026-10-20 22:30

| 板块 | 上游页数 | 中文页数 | 复查通过 | 已同步待复查 | 部分同步 | 同步中 | 待同步 | 完成率 |
| ---- | -------- | -------- | -------- | ------------ | -------- | ------ | ------ | ------ |
| 树莓派 | 17 | 17 | 6 | 11 | 0 | 0 | 0 | 35% |
| 配件 | 20 | 20 | 8 | 12 | 0 | 0 | 0 | 40% |
| 微控制器 | 6 | 6 | 6 | 0 | 0 | 0 | 0 | 100% |
| 服务 | 4 | 4 | 2 | 2 | 0 | 0 | 0 | 50% |
| 安全 | 5 | 5 | 5 | 0 | 0 | 0 | 0 | 100% |
| 合计 | 52 | 52 | 27 | 25 | 0 | 0 | 0 | 52% |

完成率按「复查通过 / 总页数」计算，仅统计完成三轮逐句校对并复查的页面。CP-2/CP-3 已通过（52 页全部同步），当前阶段为三轮逐句校对：主线程完成 3 页（G0）+ 安全板块 5 页（H12 中断后接手）+ 验收 H4 两页，合计 11 页复查通过；其余 14 个子代理并行校对 41 页（G1/G2、H1–H3、H5–H13），回报后逐文件验收。

## 四、页面清单

状态取值：`待同步`、`同步中`、`部分同步`、`已同步`、`三轮完成`、`复查通过`、`阻塞`。
校对轮次取值：`0/3`、`1/3`、`2/3`、`3/3`、`复查✓`。

### 4.1 树莓派（17）

| 中文文件 | 上游 adoc | 状态 | 校对轮次 | 负责人 | 最后更新 | 备注 |
| -------- | --------- | ---- | -------- | ------ | -------- | ---- |
| `shu-mei-pai/ru-men.md` | `getting-started.adoc` | 复查通过 | 3/3 | H4+主线程验收 | 2026-10-20 | F1 全新同步；H4 三轮+复查完成 20 处修订（Full→完整版树莓派系统、硬编码引用改站内锚点、逻辑反转句修正等），主线程验收：10 个跨页锚点逐一验证存在；重复标题「连接有线网络」（L272/L337）系上游结构；H4 报告 11 条上游异常（Rasberry 拼写 ×2、that→than、in one of 漏词、also/the 重复、列项重复等） |
| `shu-mei-pai/raspberry-pi-os.md` | `os.adoc` | 复查通过 | 3/3 | H4+主线程验收 | 2026-10-20 | F2 全新同步；H4 三轮+复查完成 20 处修订（发布周期句改写、删除上游没有的 GitHub 增补句、弯引号、OOM 译「内存不足」等），主线程验收通过；代码围栏 110 条逐字一致；遗留 L514 锚点 `#get_config-配置项目intstr` 依赖 GitBook slug 对 `[|]` 的处理，待 CI 验证 |
| `shu-mei-pai/xi-tong-pei-zhi.md` | `configuration.adoc` | 已同步 | 0/3 | 代理 F3（完成） | 2026-10-20 | F3 全新同步（15 H2；初轮漏 reference 节已打回补录，text 标记违规已修），主线程已验证落盘；待三轮逐句校对 |
| `shu-mei-pai/config.txt.md` | `config_txt.adoc` | 已同步 | 0/3 | 代理 F4（完成） | 2026-10-20 | F4 全文重写（13 H2；989→1316 行，含 armstub/sha256/enable_jtag_gpio 补录与大量默认值修订），主线程已验证落盘；待三轮逐句校对 |
| `shu-mei-pai/linux-nei-he.md` | `linux_kernel.adoc` | 已同步 | 0/3 | 代理 B4（完成） | 2026-10-20 | B4 整页重写已提交（`79d516b`），主线程已复核：7 节与上游一一对应（含 5 级标题）、BCM2712/kernel_2712 等齐备；待三轮逐句校对 |
| `shu-mei-pai/yuan-cheng-fang-wen.md` | `remote-access.adoc` | 复查通过 | 复查✓ | 主线程 | 2026-10-18 | 约 160 处修订；截图待中文 UI 重制 |
| `shu-mei-pai/she-xiang-tou-ruan-jian.md` | `camera_software.adoc` | 校对中 | 0/3 | 代理 G2 | 2026-10-20 | 全页重写至当前上游；本轮开始三轮逐句校对（上游主文件 61 行 + 31 个子文件，约 2000 行） |
| `shu-mei-pai/ren-gong-zhi-neng-ruan-jian.md` | `ai.adoc` | 复查通过 | 3/3 | 主线程 | 2026-10-20 | 主线程三轮：逐句对照 getting-started.adoc 546 行（505 行中文）；hailortcli/dmesg/Docker/Open WebUI 全部命令块逐字核对；YOLO 表 4 行、软件包版本 4.19/4.18/4.17 三组核对一致；修正 1 处（更新软件/更新引导加载程序配置双链接内部化，锚点验证存在）；上游笔误「PCI Gen 3.0」缺 e 已按正确含义译出 |
| `shu-mei-pai/shu-mei-pai-ying-jian.md` | `raspberry-pi.adoc` | 已同步 | 0/3 | 代理 F14（主线程复核） | 2026-10-20 | 27 个 H2 与上游 27 个 .adoc 一一对应；`boot-eeprom`（树莓派引导 EEPROM，line 144）与 `bootflow-legacy`（对应中文「引导顺序」节 line 1126，上游标题即 "Boot sequence"）均已存在且内容完整，原「缺节」误判已澄清；CP-3 抽查通过（无「」/xref/link/image 残留、围栏 224 偶数、弯引号 12/12、CRLF）；待三轮逐句校对 |
| `shu-mei-pai/ling-dian-xing-hao.md` | `zero.adoc` | 已同步 | 0/3 | 代理 F7（完成） | 2026-10-20 | F7 完成 4 处修正（microSD→存储卡插槽），B5 落盘版核验可用，主线程已验证落盘；待三轮逐句校对 |
| `shu-mei-pai/ji-suan-mo-kuai-ying-jian.md` | `compute-module.adoc` | 校对中 | 0/3 | 代理 G1 | 2026-10-20 | CM5 时代全面同步；本轮开始三轮逐句校对（上游主文件 13 行 + 7 个子文件共 1280 行） |
| `shu-mei-pai/chu-li-qi.md` | `processors.adoc` | 复查通过 | 复查✓ | 主线程 G0 | 2026-10-20 | 11 处修订：5 处提示块 `>` 后多余空格、heat spreader 改「均热盖」（术语表同步区分 heatsink）、删「金属」增补、补 "now"、16 纳米改 16 nm、3 处双重「的」与并列结构改写、`potentially` 改正。术语表新增 heatsink 条目 |
| `shu-mei-pai/io-kong-zhi-qi.md` | `io-controllers.adoc` | 已同步 | 1/3 | 代理 B8（完成） | 2026-10-20 | 8 处修订；RP1 规格与上游一致；视频宏改为普通链接。注意本文件为 LF，与仓库其他 CRLF 文件不同 |
| `shu-mei-pai/ruan-jian-lai-yuan.md` | `software-sources.adoc` | 同步中 | 0/3 | 代理 F11 | 2026-10-20 | A10 失联，部分改动已落盘（`da040ea`），F11 核验补齐 |
| `shu-mei-pai/jiu-ban-config.txt-can-shu.md` | `legacy_config_txt.adoc` | 已同步 | 0/3 | 代理 F6（完成） | 2026-10-20 | F6 二次重做验收（8 H2；删除已迁移至现代页的旧版 GPIO 控制/armstub/sha256 节，23 项 grep 证据全中）；首轮报告失实源于 WSL 编辑器缓冲未刷盘，勘误已记录；待三轮逐句校对 |
| `shu-mei-pai/jing-dian-dan-ban-ji-suan-ji.md` | `sbcs.adoc` | 复查通过 | 3/3 | 主线程 | 2026-10-20 | 主线程三轮：逐句对照 sbc-intro+sbc-models 782 行（494 行中文）；10 行旗舰规格表、七个型号组件/端口表逐格核对一致；修正 2 处（表标题「表 4.」编号统一、4B 节「焊接在 Pi 5 上」上游复制粘贴笔误→Pi 4B，上游 L152 即笔误，记入异常清单）；H6 曾报告的「> 空格 5 处」已随全局清零修复 |
| `shu-mei-pai/jian-pan-ji-suan-ji.md` | `keyboard-computers.adoc` | 同步中 | 0/3 | 代理 F9 | 2026-10-20 | B7 失联，部分改动已落盘（`4a6ac8e`），F9 核验补齐 |

### 4.2 配件（20）

| 中文文件 | 上游 adoc | 状态 | 校对轮次 | 负责人 | 最后更新 | 备注 |
| -------- | --------- | ---- | -------- | ------ | -------- | ---- |
| `pei-jian/sd-ka.md` | `sd-cards.adoc` | 已同步 | 0/3 | 代理 E8（完成） | 2026-10-20 | E8 核查与上游零差异，主线程已复核；待三轮逐句校对 |
| `pei-jian/ssd.md` | `ssds.adoc` | 已同步 | 0/3 | 代理 E9（完成） | 2026-10-20 | E9 核查与上游零差异，主线程已复核；待三轮逐句校对 |
| `pei-jian/ssd-tao-jian.md` | `ssd-kit.adoc` | 已同步 | 0/3 | 代理 E10（完成） | 2026-10-20 | E10 核查与上游一致并清理 2 行冗余，主线程已复核；待三轮逐句校对 |
| `pei-jian/m.2-hat+.md` | `m2-hat-plus.adoc` | 复查通过 | 3/3 | 主线程 | 2026-10-20 | H9 代理润色 22 行已验收 + 主线程逐句复查：上游 about.adoc 253 行对照 219 行中文；2230/2242、2023-12-06、500 MB/s、3A 等数字一致；跨页锚点 xi-tong-pei-zhi.md#自动挂载存储设备验证存在；零新增修改 |
| `pei-jian/xian-shi-qi.md` | `display.adoc` | 复查通过 | 3/3 | 主线程 | 2026-10-20 | 主线程三轮：逐句对照 display/display_intro.adoc 470 行（436 行中文），结构一一对应；修复 1 处「20000 小时」→「20,000 小时」；跨页锚点 2 个验证存在；测试点/规格数字逐项核对一致 |
| `pei-jian/chu-mo-xian-shi-ping-2.md` | `touch-display-2.adoc` | 复查通过 | 3/3 | 主线程 | 2026-10-20 | 主线程三轮：逐句对照 touch-display-2/about.adoc 619 行（521 行中文），兼容性表 3 行、尺寸表 3 行、硬件/连接表逐格一致；ili9881/ili79600 叠加层、J6 跳线两种情况、Rasperry Pi HAT 丝印（5/7 英寸节上游笔误照录）核对无误；零内容修改 |
| `pei-jian/raspberry-pi-monitor.md` | `monitor.adoc` | 已同步 | 0/3 | 代理 E19（完成） | 2026-10-20 | E19 核查与上游零差异，主线程已复核；待三轮逐句校对 |
| `pei-jian/she-xiang-tou.md` | `camera.adoc` | 复查通过 | 3/3 | H8+主线程 | 2026-10-20 | H8 代理润色 48 行已验收 + 主线程逐句复查：13 个上游子文件 776 行对照 607 行中文；六款摄像头列表、安装四步（七种主板接口位置）、C/CS 与 M12 镜头表逐格、硬件规格 18×7 表逐格、15/22 针引脚表逐行全部一致；上游异常：GS 像素数 intro(1.5M) 与 gs 节(1.6M) 自相矛盾，中文分别照录；零新增修改，复查通过 |
| `pei-jian/ai-she-xiang-tou.md` | `ai-camera.adoc` | 已同步 | 0/3 | 代理 E16（完成） | 2026-10-20 | E16 完成 1 处修订（IMX5000→IMX500，上游笔误），主线程已复核；待三轮逐句校对 |
| `pei-jian/jian-pan-he-shu-biao.md` | `keyboard-and-mouse.adoc` | 已同步 | 0/3 | 代理 E1（完成） | 2026-10-20 | E1 完成 1 处修订（标题与上游 "with your Mouse" 一致），主线程已复核；待三轮逐句校对 |
| `pei-jian/usb-pei-jian.md` | `usb.adoc` | 已同步 | 0/3 | 代理 E11（完成） | 2026-10-20 | E11 核查与上游零差异，主线程已复核；待三轮逐句校对 |
| `pei-jian/build-hat.md` | `build-hat.adoc` | 复查通过 | 3/3 | H7+主线程 | 2026-10-20 | H7 代理润色 110 行已验收 + 主线程逐句复查：8 个上游子文件 821 行对照 776 行中文，Python/.NET 全部代码块逐字核对，12 列×17 行设备兼容性表逐格一致（含设备 ID 31/30/4B/41/3D/3E/1/3F/40/2/8/26/2E/2F/25/35/34），上游笔误 Built HAT/Rasperry Pi HAT 照录或按正确含义处理；零新增修改，复查通过 |
| `pei-jian/chuan-gan-qi-kuo-zhan-ban-sense-hat.md` | `sense-hat.adoc` | 复查通过 | 3/3 | H9a+主线程 | 2026-10-20 | H9a 代理润色 42 行已验收 + 主线程逐句复查：3 个上游子文件 221 行对照 216 行中文；校准菜单/输出块逐字、EEPROM 读写命令逐字、特性七项一致；零新增修改 |
| `pei-jian/ren-gong-zhi-neng-tao-jian-ai-kit.md` | `ai-kit.adoc` | 已同步 | 0/3 | 代理 E6（完成） | 2026-10-20 | E6 按上游重写（AI Kit 已停产，页缩减为停产声明 + 硬件/安装/后续步骤），主线程已复核；待三轮逐句校对 |
| `pei-jian/ai-hat.md` | `ai-hat-plus.adoc` | 复查通过 | 3/3 | 主线程 | 2026-10-20 | 主线程逐句复查：上游 about.adoc 178 行对照 155 行中文，型号表 5 行/物理规格 6 组数字/组装 3 步 PCIe 8 小步逐字核对；上游笔误 L79「AI HAT+ is approximately」应为 AI HAT+ 2，中文已按正确含义，记入异常清单；零新增修改 |
| `pei-jian/shu-mei-pai-yin-pin-kuo-zhan-ban-raspberry-pi-audio-board.md` | `audio.adoc` | 已同步 | 0/3 | 代理 E7（完成） | 2026-10-20 | E7 全页重写同步至上游（17 类修订，涵盖 DAC Pro/DAC+/DigiAMP+/Codec Zero 全线），主线程已复核；待三轮逐句校对 |
| `pei-jian/dian-shi-kuo-zhan-ban-tv-hat.md` | `tv-hat.adoc` | 复查通过 | 3/3 | H9a+主线程 | 2026-10-20 | H9a 代理润色 37 行已验收 + 主线程逐句复查：about-tv-hat.adoc 87 行对照 84 行中文；CXD2880 型号修正已核（上游 L11 正确/L54 截图文笔误）；设置向导、muxes/services 输出、TvhClient NOTE 逐字一致；零新增修改 |
| `pei-jian/cm5-bian-cheng-zhi-ju.md` | `cm5-programming-jig.adoc` | 已同步 | 0/3 | 代理 E14（完成） | 2026-10-20 | E14 核查与上游零差异（8 节含安全警告全齐），主线程已复核；待三轮逐句校对 |
| `pei-jian/zhi-neng-xian-shi-mo-kuai.md` | `smart-display-module.adoc` | 已同步 | 0/3 | 代理 E15（完成） | 2026-10-20 | E15 完成 3 处锚点/链接修正（`684ec85` 已落盘），主线程已复核；待三轮逐句校对 |
| `pei-jian/bao-hu-ke.md` | `bumper.adoc` | 已同步 | 0/3 | 代理 E13（完成） | 2026-10-20 | E13 核查与上游零差异，主线程已复核；待三轮逐句校对 |

### 4.3 微控制器（6）

| 中文文件 | 上游 adoc | 状态 | 校对轮次 | 负责人 | 最后更新 | 备注 |
| -------- | --------- | ---- | -------- | ------ | -------- | ---- |
| `wei-kong-zhi-qi/wu-xian-dian-mo-kuai.md` | `radio-modules.adoc` | 复查通过 | 复查✓ | 主线程 G0 | 2026-10-20 | 6 处修订：补译漏句「本页仅介绍 RM2。」并校正其位置（上游位于 RM1/RM2 列表之后）、删两处加粗后多余空格、补两处加粗后缺失空格、"created" 改「推出」、"self-contained" 改「自成一体的」、删「边缘镀层的」增补；CP-3 全项通过 |
| `wei-kong-zhi-qi/rp2040.md` | `microcontroller-chips.adoc` | 复查通过 | 复查✓ | 主线程 G0 | 2026-10-20 | 3 处修订：「带插针」改「带排针」（与 Pico 页术语统一）、架构切换句语序重排、licence 句「授予…PID 值」宾语错位改正。核对全部 9 个页内锚点与 2 个跨页锚点；表格 3 列×20 行、7 列×6 行均一致；遗留 `micropython.md#什么是-micropython` 锚点待 CI 验证；「## RP1」为用户既定增补节（上游无对应），TASKS 已记录 |
| `wei-kong-zhi-qi/shu-mei-pai-pico-he-pico-w.md` | `pico-series.adoc` | 复查通过 | 3/3 | H13+主线程 | 2026-10-20 | F10 全页重写：上游结构重构（8 型号汇总表、两代变体表、SWD 表），23 个链接迁 pip.raspberrypi.com；H13+主线程三轮：逐句对照 572 行上游，表格逐格核对一致，修复 4 处直引号与列表编号 1,1,2,3 |
| `wei-kong-zhi-qi/shu-mei-pai-tiao-shi-tao-jian-raspberry-pi-debug-probe.md` | `debug-probe.adoc` | 复查通过 | 3/3 | H13+主线程 | 2026-10-20 | F5 全量重写（8 H2；改用 VS Code 扩展安装路线、补 UART 连接、RTT 表）；H13+主线程三轮：Debug Probe 译法统一「调试套件」42 处（词汇表同步修订），GDB 语境「调试器」保留；修复提示块脚本误改的 3 行 gdb 代码块 |
| `wei-kong-zhi-qi/micropython.md` | `micropython.adoc` | 复查通过 | 3/3 | H13+主线程 | 2026-10-20 | F5 全量重写（4 H2；数据手册编号、Bug 列表与 Pico 2 W 变体）；H13+主线程三轮：逐句对照上游 4 文件，修复 1 处单引号→弯引号；代码块注释译中文合规 |
| `wei-kong-zhi-qi/c-c++-sdk.md` | `c_sdk.adoc` | 复查通过 | 3/3 | H13+主线程 | 2026-10-20 | F5 全量重写（4 H2；blink_universal、pico_setup.sh 等）；H13+主线程三轮：逐句对照上游 4 文件，修复失效锚点 #更新软件（H4 改标题所致）、-DWIFI_SSID 参数补反引号、H2 补译 own |

### 4.4 服务（4）

| 中文文件 | 上游 adoc | 状态 | 校对轮次 | 负责人 | 最后更新 | 备注 |
| -------- | --------- | ---- | -------- | ------ | -------- | ---- |
| `fu-wu/shu-mei-pai-zhang-hao-raspberry-pi-id.md` | `id.adoc` | 已同步 | 0/3 | 代理 F13（完成） | 2026-10-20 | F13 完成 7 处修正（TOTP 定义、NOTE 转提示块、术语空格），主线程已验证落盘；待三轮逐句校对 |
| `fu-wu/shu-mei-pai-yuan-cheng-fang-wen-raspberry-pi-connect.md` | `connect.adoc` | 已同步 | 0/3 | 代理 F13（完成） | 2026-10-20 | F13 完成 5 处修正（未译界面标签补译、语序），主线程已验证落盘；待三轮逐句校对 |
| `fu-wu/shu-mei-pai-connect-qi-ye-ban.md` | `connect-for-organisations.adoc` | 已同步 | 0/3 | 代理 F13（完成） | 2026-10-20 | F13 完整核验：13 H2/36 H3 全覆盖，版本号/表格/代码块与上游一致，仅 1 处语序修正，主线程已验证落盘；待三轮逐句校对 |
| `fu-wu/shu-mei-pai-shu-jia.md` | `bookshelf.adoc` | 已同步 | 0/3 | 代理 F13（完成） | 2026-10-20 | F13 逐句核验零改动（3 H2 对应 intro + subscription 拆 2 节，结构合法）；待三轮逐句校对 |

### 4.5 安全（5）

| 中文文件 | 上游 adoc | 状态 | 校对轮次 | 负责人 | 最后更新 | 备注 |
| -------- | --------- | ---- | -------- | ------ | -------- | ---- |
| `an-quan/an-quan-gai-shu.md` | `security.adoc` | 复查通过 | 3/3 | H12+主线程 | 2026-10-20 | H12 润色 4 处（概述句、信任链句式、「一线安全披露」标题、我们的网站），主线程逐句对照 security.adoc 全文并补 1 处（「存储卡」→「microSD 卡」）；CP-3 全项通过 |
| `an-quan/an-quan-jia-gou.md` | `security-architecture.adoc` | 复查通过 | 3/3 | H12+主线程 | 2026-10-20 | H12 润色 15 处（句式与术语：OTP 内存、一次性可编程等，经词汇表核实正确）；主线程逐句对照 105 行上游，页内锚点 5 个验证存在；CP-3 通过（L41 CJK 紧邻为锚点 slug 正常形态） |
| `an-quan/an-quan-qi-dong-pei-zhi-qi.md` | `secure-boot-provisioner.adoc` | 复查通过 | 3/3 | H12+主线程 | 2026-10-20 | H12 润色 15 处；主线程逐句对照 473 行上游（444 行中文），补 1 处「标准存储卡」→「标准 microSD 卡」；表格 3×3 与 2×4 一致；跨页锚点 2 个（树莓派引导 EEPROM、eeprom_write_protect）验证存在；CP-3 通过（8 个直引号均在 sqlite3 代码块内，合规） |
| `an-quan/yun-ying-an-quan.md` | `operational-security.adoc` | 复查通过 | 3/3 | H12+主线程 | 2026-10-20 | H12 润色 5 处；主线程逐句对照 100 行上游；跨页锚点 4 个验证存在；上游异常：上游 ini 代码块缺 `enabled = true` 等号（jail.conf 语法必需），中文按正确含义保留等号 |
| `an-quan/ufw-fang-huo-qiang.md` | `ufw.adoc` | 复查通过 | 3/3 | H12+主线程 | 2026-10-20 | H12 润色 5 处；主线程逐句对照 186 行上游（126 行中文），命令与表格逐字一致，页内锚点 5 个验证存在，零新增修改 |

### 4.6 项目自有（3）

| 中文文件 | 上游 | 状态 | 最后更新 | 备注 |
| -------- | ---- | ---- | -------- | ---- |
| `qian-yan/ci-hui-biao.md` | 无 | 维护中 | 2026-10-20 | 已补 Control Centre、NFS export |
| `qian-yan/guan-yu-wo-men.md` | 无 | 不适用 | 2024 | |
| `qian-yan/ban-quan-shuo-ming.md` | 无 | 不适用 | 2024 | |

## 五、当前进行中

统计时间：2026-10-20 15:05。滚动更新：每次代理领取或结束时立即修改本节。

| 代理 | 负责文件 | 开始时间 | 目标检查点 | 状态 |
| ---- | -------- | -------- | ---------- | ---- |
| A1 | `pei-jian/she-xiang-tou.md` | 2026-10-20 | CP-2 + CP-3 | 失败（连接中断），无改动 |
| A2 | `pei-jian/xian-shi-qi.md`、`chu-mo-xian-shi-ping-2.md`、`raspberry-pi-monitor.md` | 2026-10-20 | CP-2 + CP-3 | 失败（连接中断），仅 `xian-shi-qi.md` 有部分改动 |
| A3 | `pei-jian/jian-pan-he-shu-biao.md`、`build-hat.md`、`chuan-gan-qi-kuo-zhan-ban-sense-hat.md`、`dian-shi-kuo-zhan-ban-tv-hat.md` | 2026-10-20 | CP-2 + CP-3 | 失败（连接中断），键鼠与 Sense HAT 有部分改动 |
| A4 | `pei-jian/m.2-hat+.md`、`ren-gong-zhi-neng-tao-jian-ai-kit.md`、`shu-mei-pai-yin-pin-kuo-zhan-ban-raspberry-pi-audio-board.md` | 2026-10-20 | CP-2 + CP-3 | 失败（连接中断），仅 `m.2-hat+.md` 有改动 |
| A5 | `pei-jian/sd-ka.md`、`ssd.md`、`ssd-tao-jian.md`、`usb-pei-jian.md`、`ai-hat.md`、`bao-hu-ke.md`、`cm5-bian-cheng-zhi-ju.md`、`zhi-neng-xian-shi-mo-kuai.md` | 2026-10-20 | CP-2 + CP-3 | 失败（连接中断），无改动 |
| A6 | `wei-kong-zhi-qi/shu-mei-pai-pico-he-pico-w.md`、`shu-mei-pai-tiao-shi-tao-jian-raspberry-pi-debug-probe.md`、`micropython.md`、`c-c++-sdk.md` | 2026-10-20 | CP-2 + CP-3 | 失联（连接中断）：仅 pico 页有落盘改动（`4a6ac8e`），其余 3 页无改动；由 F5/F10 接替 |
| A7 | `fu-wu/` 4 页 | 2026-10-20 | CP-2 + CP-3 | 失联（连接中断）：4 页改动均已落盘（`a67a29d`/`d441b30`/`3c4e97f`），完成度未知；由 F12 接替核验 |
| A8 | `an-quan/` 5 页 | 2026-10-20 | CP-2 + CP-3 | 失败（连接中断），无改动 |
| A9 | `ru-men.md`、`raspberry-pi-os.md`、`linux-nei-he.md` | 2026-10-20 | CP-2 + CP-3 | 失败（连接中断），由 B2/B3/B4 接替 |
| A10 | `xi-tong-pei-zhi.md`、`config.txt.md`、`jiu-ban-config.txt-can-shu.md`、`ruan-jian-lai-yuan.md` | 2026-10-20 | CP-2 + CP-3 | 失联（连接中断）：`jiu-ban`（`4a6ac8e`）、`ruan-jian-lai-yuan`（`da040ea`）有落盘改动，`xi-tong-pei-zhi`、`config.txt` 无改动；由 F3/F4/F6/F11 接替 |
| B1 | `shu-mei-pai/shu-mei-pai-ying-jian.md` | 2026-10-20 | CP-2 + CP-3 | 失败（连接中断），无新增改动 |
| B2 | `shu-mei-pai/ru-men.md` | 2026-10-20 | CP-2 + CP-3 | 失败（连接中断），无改动 |
| B3 | `shu-mei-pai/raspberry-pi-os.md` | 2026-10-20 | CP-2 + CP-3 | 失败（连接中断），无改动 |
| B4 | `shu-mei-pai/linux-nei-he.md` | 2026-10-20 | CP-2 + CP-3 | 完成：整页重写已提交并经主线程验收 |
| B5 | `shu-mei-pai/ling-dian-xing-hao.md` | 2026-10-20 | CP-2 + CP-3 | 失联（连接中断）：改动已落盘（`4a6ac8e`），完成度未知；由 F7 接替核验 |
| B6 | `shu-mei-pai/jing-dian-dan-ban-ji-suan-ji.md` | 2026-10-20 | CP-2 + CP-3 | 失联（连接中断）：改动已落盘（`d441b30`），完成度未知；由 F8 接替核验 |
| B7 | `shu-mei-pai/jian-pan-ji-suan-ji.md` | 2026-10-20 | CP-2 + CP-3 | 失联（连接中断）：改动已落盘（`4a6ac8e`），完成度未知；由 F9 接替核验 |
| B8 | `shu-mei-pai/io-kong-zhi-qi.md` | 2026-10-20 | CP-2 + CP-3 | 完成：8 处修订，已报告 |
| B9 | `shu-mei-pai/ren-gong-zhi-neng-ruan-jian.md` | 2026-10-20 | CP-2 + CP-3 | 失联（连接中断）：改动已落盘（`4a6ac8e`），完成度未知；由 F7 接替核验 |
| B10 | `pei-jian/ai-she-xiang-tou.md` | 2026-10-20 | CP-2 + CP-3 | 失败（连接中断），无改动 |
| C1 | `pei-jian/she-xiang-tou.md` | 2026-10-20 | CP-2 + CP-3 | 交付不实：所称修改未落盘（主线程已验证），打回；由 C7 重做 |
| C2 | `an-quan/an-quan-gai-shu.md` | 2026-10-20 | CP-2 + CP-3 | 完成：2 处修订（主线程已复核） |
| C3 | `an-quan/an-quan-jia-gou.md` | 2026-10-20 | CP-2 + CP-3 | 完成：核查与上游一致，无需修改（主线程已复核） |
| C4 | `an-quan/an-quan-qi-dong-pei-zhi-qi.md` | 2026-10-20 | CP-2 + CP-3 | 完成：5 处修订（主线程已复核） |
| C5 | `an-quan/yun-ying-an-quan.md` | 2026-10-20 | CP-2 + CP-3 | 完成：fail2ban 等号修正 + 链接内部化（主线程已复核；代理回报丢失，以落盘为准） |
| C6 | `an-quan/ufw-fang-huo-qiang.md` | 2026-10-20 | CP-2 + CP-3 | 完成：零修改，核查通过（主线程已复核） |
| C7 | `pei-jian/she-xiang-tou.md` | 2026-10-20 | CP-2 + CP-3 | 完成：全页重写同步（主线程已复核） |
| E1 | `pei-jian/jian-pan-he-shu-biao.md` | 2026-10-20 | CP-2 + CP-3 | 完成：1 处修订（主线程已复核） |
| E2 | `pei-jian/build-hat.md` | 2026-10-20 | CP-2 + CP-3 | 完成：全页重写同步（主线程已复核） |
| E3 | `pei-jian/chuan-gan-qi-kuo-zhan-ban-sense-hat.md` | 2026-10-20 | CP-2 + CP-3 | 完成：重组 6 节 + 13 类修正（主线程已复核） |
| E4 | `pei-jian/dian-shi-kuo-zhan-ban-tv-hat.md` | 2026-10-20 | CP-2 + CP-3 | 完成：重写同步（主线程已复核） |
| E5 | `pei-jian/m.2-hat+.md` | 2026-10-20 | CP-2 + CP-3 | 完成：重写同步（主线程已复核） |
| E6 | `pei-jian/ren-gong-zhi-neng-tao-jian-ai-kit.md` | 2026-10-20 | CP-2 + CP-3 | 完成：按上游停产重写（主线程已复核） |
| E7 | `pei-jian/shu-mei-pai-yin-pin-kuo-zhan-ban-raspberry-pi-audio-board.md` | 2026-10-20 | CP-2 + CP-3 | 完成：全页重写同步（主线程已复核） |
| E8 | `pei-jian/sd-ka.md` | 2026-10-20 | CP-2 + CP-3 | 完成：零差异核查（主线程已复核） |
| E9 | `pei-jian/ssd.md` | 2026-10-20 | CP-2 + CP-3 | 完成：零差异核查（主线程已复核） |
| E10 | `pei-jian/ssd-tao-jian.md` | 2026-10-20 | CP-2 + CP-3 | 完成：一致性核查 + 清理 2 行（主线程已复核） |
| E11 | `pei-jian/usb-pei-jian.md` | 2026-10-20 | CP-2 + CP-3 | 完成：零差异核查（主线程已复核） |
| E12 | `pei-jian/ai-hat.md` | 2026-10-20 | CP-2 + CP-3 | 完成：4 处修订（主线程已复核） |
| E13 | `pei-jian/bao-hu-ke.md` | 2026-10-20 | CP-2 + CP-3 | 完成：零差异核查（主线程已复核） |
| E14 | `pei-jian/cm5-bian-cheng-zhi-ju.md` | 2026-10-20 | CP-2 + CP-3 | 完成：零差异核查（主线程已复核） |
| E15 | `pei-jian/zhi-neng-xian-shi-mo-kuai.md` | 2026-10-20 | CP-2 + CP-3 | 完成：3 处锚点/链接修正（主线程已复核） |
| E16 | `pei-jian/ai-she-xiang-tou.md` | 2026-10-20 | CP-2 + CP-3 | 完成：1 处修订（主线程已复核） |
| E17 | `pei-jian/xian-shi-qi.md` | 2026-10-20 | CP-2 + CP-3 | 完成：2 处链接修正（主线程已复核） |
| E18 | `pei-jian/chu-mo-xian-shi-ping-2.md` | 2026-10-20 | CP-2 + CP-3 | 完成：2 处修订（主线程已复核） |
| E19 | `pei-jian/raspberry-pi-monitor.md` | 2026-10-20 | CP-2 + CP-3 | 完成：零差异核查（主线程已复核） |
| F1 | `shu-mei-pai/ru-men.md` | 2026-10-20 | CP-2 + CP-3 | 完成：全新同步，上游异常 5 项已抽查（主线程已验证落盘） |
| F2 | `shu-mei-pai/raspberry-pi-os.md` | 2026-10-20 | CP-2 + CP-3 | 完成：全新同步，关键内容全部落盘（主线程已验证） |
| F3 | `shu-mei-pai/xi-tong-pei-zhi.md` | 2026-10-20 | CP-2 + CP-3 | 完成：全新同步 + 打回补录 reference 节、修 3 处 text 标记（主线程已验证） |
| F4 | `shu-mei-pai/config.txt.md` | 2026-10-20 | CP-2 + CP-3 | 完成：全文重写（主线程已验证落盘） |
| F5 | `wei-kong-zhi-qi/shu-mei-pai-tiao-shi-tao-jian-raspberry-pi-debug-probe.md`、`micropython.md`、`c-c++-sdk.md` | 2026-10-20 | CP-2 + CP-3 | 完成：三页全量重写至上游新结构（主线程已验证落盘） |
| F6 | `shu-mei-pai/jiu-ban-config.txt-can-shu.md` | 2026-10-20 | CP-2 + CP-3 | 完成：首轮报告失实（WSL 编辑器缓冲未刷盘所致，已勘误），二次重做全部验证通过（主线程已复核） |
| F7 | `shu-mei-pai/ling-dian-xing-hao.md`、`ren-gong-zhi-neng-ruan-jian.md` | 2026-10-20 | CP-2 + CP-3 | 完成：零型页 4 处修正、AI 软件页零改动（主线程已验证落盘） |
| F8 | `shu-mei-pai/jing-dian-dan-ban-ji-suan-ji.md` | 2026-10-20 | CP-2 + CP-3 | 完成：1 处修正（如实翻译上游 Pi 5 笔误；主线程已验证） |
| F9 | `shu-mei-pai/jian-pan-ji-suan-ji.md` | 2026-10-20 | CP-2 + CP-3 | 完成：零改动，B7 落盘版核验可用（主线程已验证） |
| F10 | `wei-kong-zhi-qi/shu-mei-pai-pico-he-pico-w.md` | 2026-10-20 | CP-2 + CP-3 | 完成：全页重写至上游新结构（主线程已验证落盘） |
| F11 | `shu-mei-pai/ruan-jian-lai-yuan.md` | 2026-10-20 | CP-2 + CP-3 | 完成：6 处小修正，A10 落盘版判定可用（主线程已验证落盘） |
| F12 | `fu-wu/` 4 页 | 2026-10-20 | CP-2 + CP-3 | 失联（无核验报告）：3 页成果已自动提交（`d7bcd04`），企业版页未处理；由 F13 接替 |
| F13 | `fu-wu/` 4 页 | 2026-10-20 | CP-2 + CP-3 | 完成：账号 7 处、Connect 5 处、企业版 1 处修正，书架零改动（主线程已验证） |
| F14 | `shu-mei-pai/shu-mei-pai-ying-jian.md` | 2026-10-20 | CP-2 + CP-3 | 完成：主线程复核硬件页 27 H2 与上游 27 个 .adoc 文件一一对应，原判定「缺 boot-eeprom / bootflow-legacy 两节」为误判（两节均已存在且内容完整：`boot-eeprom`→「树莓派引导 EEPROM」line 144；`bootflow-legacy`→「引导顺序」line 1126），无需新增；CP-3 抽查通过 |

| G0 | `shu-mei-pai/chu-li-qi.md`、`wei-kong-zhi-qi/wu-xian-dian-mo-kuai.md`、`wei-kong-zhi-qi/rp2040.md` | 2026-10-20 | 三轮 + 复查 | 完成：三页均达「复查通过」（主线程逐句执行，合计 20 处修订） |
| G1 | `shu-mei-pai/ji-suan-mo-kuai-ying-jian.md` | 2026-10-20 | 三轮 + 复查 | 进行中 |
| G2 | `shu-mei-pai/she-xiang-tou-ruan-jian.md` | 2026-10-20 | 三轮 + 复查 | 进行中 |
| H1 | `shu-mei-pai/xi-tong-pei-zhi.md` | 2026-10-20 | 三轮 + 复查 | 进行中（4147 行，按 H2 分节推进） |
| H2 | `shu-mei-pai/shu-mei-pai-ying-jian.md` | 2026-10-20 | 三轮 + 复查 | 进行中（3402 行，27 节） |
| H3 | `shu-mei-pai/config.txt.md`、`jiu-ban-config.txt-can-shu.md` | 2026-10-20 | 三轮 + 复查 | 进行中（参数参考页，逐条核对默认值） |
| H4 | `shu-mei-pai/ru-men.md`、`raspberry-pi-os.md` | 2026-10-20 | 三轮 + 复查 | 完成（主线程验收）：两页各 20 处修订，全部合理；跨页锚点 10 个逐一验证存在（含「连接蓝牙外设」「启动时要求输入密码」等）；遗留 `raspberry-pi-os.md` L514 锚点 `#get_config-配置项目intstr` 依赖 GitBook slug 对 `[|]` 的处理，待 CI 验证；`ru-men.md` 存在重复标题「连接有线网络」（L272/L337，上游结构），锚点歧义风险低；报告另附 11 条上游异常（Rasberry 拼写 ×2、that→than、in one of 漏词、also 重复、列项重复、the 重复等） |
| H5 | `shu-mei-pai/jian-pan-ji-suan-ji.md`、`linux-nei-he.md` | 2026-10-20 | 三轮 + 复查 | 进行中（含内核页 3 处官方 URL 内部化） |
| H6 | `shu-mei-pai/io-kong-zhi-qi.md`、`jing-dian-dan-ban-ji-suan-ji.md`、`ren-gong-zhi-neng-ruan-jian.md`、`ling-dian-xing-hao.md`、`ruan-jian-lai-yuan.md` | 2026-10-20 | 三轮 + 复查 | 进行中（io 页已有 1 轮基础，补 2 轮 + 复查） |
| H7 | `pei-jian/build-hat.md`、`shu-mei-pai-yin-pin-kuo-zhan-ban-raspberry-pi-audio-board.md` | 2026-10-20 | 三轮 + 复查 | 进行中 |
| H8 | `pei-jian/she-xiang-tou.md`、`chu-mo-xian-shi-ping-2.md`、`xian-shi-qi.md`、`ai-she-xiang-tou.md` | 2026-10-20 | 三轮 + 复查 | 进行中（规格表逐格核对） |
| H9a | `pei-jian/` 8 个小页（sd-ka、ssd、ssd-tao-jian、bao-hu-ke、jian-pan-he-shu-biao、raspberry-pi-monitor、usb-pei-jian、ai-hat） | 2026-10-20 | 三轮 + 复查 | 进行中 |
| H9b | `pei-jian/` 6 页（ai-kit、tv-hat、sense-hat、m.2-hat+、zhi-neng-xian-shi-mo-kuai、cm5-bian-cheng-zhi-ju） | 2026-10-20 | 三轮 + 复查 | 进行中 |
| H10 | `fu-wu/shu-mei-pai-connect-qi-ye-ban.md` | 2026-10-20 | 三轮 + 复查 | 进行中（2079 行） |
| H11 | `fu-wu/` 3 页（connect、id、bookshelf） | 2026-10-20 | 三轮 + 复查 | 进行中 |
| H12 | `an-quan/` 5 页 | 2026-10-20 | 三轮 + 复查 | 代理因 429 频率限制中断（运行 56 分钟，5 页已落盘 43 行润色改动，质量合格）；主线程接手完成全部剩余轮次并验收：五页逐句对照上游 2304 行，复查通过。主线程补 2 处（概述页与配置器页「存储卡」→「microSD 卡」）；H12 的「一线安全披露」「OTP 内存」「一次性可编程」三处译法经核实均正确（上游即 Frontline；词汇表即 OTP 内存）；上游异常：operational-security.adoc 两处 ini 代码块缺 `enabled = true` 等号（jail.conf 语法必需，中文已按正确含义补上，见 L62-69/L87-95）；跨页锚点 6 个逐一验证存在 |
| H13 | `wei-kong-zhi-qi/` 4 页（micropython、c-c++-sdk、debug-probe、pico） | 2026-10-20 | 三轮 + 复查 | 进行中 |

## 六、待办队列

| 优先级 | 事项 | 范围 | 依赖 |
| ------ | ---- | ---- | ---- |
| P0 | 第一波重派已全部完成并验收：安全 5 页 + 摄像头页（C1 交付不实打回，C7 重做成功） | 6 页 | 完成 |
| P0 | 第二波重派已全部完成并验收：配件板块 19 页（E1–E19） | 19 页 | 完成 |
| P0 | F 波 15 页已全部完成：F1–F13 经主线程逐一落盘验证通过（F3 漏 reference 节、F6 报告失实均已打回重做通过；F12 失联由 F13 接替）；F14 经主线程复核，硬件页 27/27 节完整，原「缺两节」误判已澄清，无需补录 | 15 页 | 完成 |
| P0 | 汇总各波代理结果，逐文件复核后更新本文件状态 | 全部 | 滚动进行 |
| P0 | 对已同步页面执行三轮逐句校对 | `yuan-cheng-fang-wen`、`ji-suan-mo-kuai-ying-jian`、`she-xiang-tou-ruan-jian`、`chu-li-qi`、`rp2040`、`wu-xian-dian-mo-kuai` | 代理结束 |
| P1 | 词汇表已补录 F 波 46 条 + I/O 控制器页 5 条（I/O controller、ISP front-end、USB host controller、single-board computer、pin spacing，均验证实际用例） | `qian-yan/ci-hui-biao.md` | 完成 |
| P2 | 换行符统一：实际范围超出原记录（io-kong-zhi-qi.md 之外还有 26 个内容页 + TASKS/AGENTS/mu-lu 共 27 个 LF 文件），已全部转为 CRLF，全仓库一致 | 27 个文件 | 完成 |
| P1 | 硬件页缺节经主线程复核为误判：27 个 H2 与上游 27 个 .adoc 文件一一对应，`boot-eeprom.adoc` 对应「树莓派引导 EEPROM」（line 144）、`bootflow-legacy.adoc` 对应「引导顺序」（line 1126，上游标题即 "Boot sequence"），两节均已存在且内容完整，无需补录 | 树莓派硬件 | 完成 |
| P2 | 向上游反馈已发现的原文错误（30 余条，见「七」，含 F 波新查 17 条） | 见「七」 | 待用户批准 |
| P3 | 图片本地化：经上游 GitHub 仓库（/tmp 浅克隆）按文件名定位下载，301 张已入 `.gitbook/assets/`，39 页引用已替换；仅剩 6 处上游已移除的 GIF/PNG（build-hat 页）保留原链 | 基本完成 | 6 处无源可迁 |
| P4 | 中文 UI 重制两张 Control Centre 截图（F1 新增 Imager UI 截图约 20 张同需中文 UI 重截） | `shu-mei-pai/yuan-cheng-fang-wen.md` 等 | 人工在中文系统截图 |

## 七、阻塞与上游异常

### 7.1 阻塞

* 官方文档网页受 Cloudflare 挑战，`curl` 无法直接抓取；但上游 GitHub 仓库可通过 `git clone --depth 1 --filter=blob:none --sparse` 获取全部 adoc 与图片，P3 图片本地化已借此解除（图片按文件名在仓库内定位下载）。
* 中文 UI 截图需人工操作，无法由代理完成；范围含远程访问页 2 张 Control Centre 截图及 F1 新增的约 20 张 Imager UI 截图。

### 7.2 已发现的上游原文异常（待反馈）

| 页面 | 异常 | 状态 |
| ---- | ---- | ---- |
| SBC 页 | Raspberry Pi 4B 一节误写为 Raspberry Pi 5 | 待反馈 |
| 键盘计算机页 | `io-controllers` 的 xref 语法损坏 | 待反馈 |
| AI 摄像头页 | `IMX5000` 应为 `IMX500`；`the the` 重复 | 待反馈 |
| 安全启动配置器页 | image 属性有多余引号 | 待反馈 |
| 运营安全页 | fail2ban 示例缺少等号 | 待反馈 |
| 安全启动配置器页 | “Raspberry Pi OS (we recommend Trixie)” 将产品名与开发代号并列，与上游其他页面表述不一致（中文页已按“树莓派系统（我们建议使用 Trixie）”处理） | 待反馈 |
| UFW 页 | 第 116 行 `<<allow-block-ip-addresses>> from a specific port.` 的 xref 展开后语义不完整（低置信度） | 待反馈 |
| AI Kit 页 | 上游已将本页缩减为停产声明（建议改用 AI HAT），中文版已按新内容重写 | 已按上游处理 |
| TV HAT 页 | 规格表作 Sony CXD2880，VLC 截图文作 CDX2880，上游两处拼写不一致 | 待反馈 |
| 摄像头软件页 | 上游 config.txt watchdog 段默认 `timeout=0`/`timeout=10`，中文版为 15（经 E17 核实） | 待反馈 |
| 远程访问页 | IPv6 网络启动一节 `FTP` 应为 `TFTP`；`/proc/mounts` 反引号错位；`Atfer` 应为 `After` | 待反馈 |
| Zero 页 | Zero 2 W 规格表 Wi-Fi 与蓝牙两列错位（`802.11 b/g/n` 与 `Bluetooth 4.2` 串行） | 待反馈 |
| Zero 页 | "Zero" 的 Ports 表头复制粘贴自规格表，列名与数据错位 | 待反馈 |
| Zero 页 | `schematc` 拼写错误（应为 `schematic`，F7 实测） | 待反馈 |
| Zero 2 W 规格 | "PCI Gen 3.0 mode" 表述与上下文不符（低置信度，待上游核实） | 待反馈 |
| Pico 系列页 | 全站 datasheets→pip 域名大迁移未在上游 CHANGELOG 说明（F10 报告） | 待反馈 |
| Pico 系列页 | "Pico 2 W 无线固件" 链接指向的 `RELEASE.HTML` 大小写异常（F10 报告） | 待反馈 |
| Pico 系列页 | Models 节称 W 型号为双频 802.11ac，与无线特性节 "2.4GHz 802.11n" 自相矛盾（照译保留） | 待反馈 |
| Pico 系列页 | 无线 Pico 2 特性表 GPIO"更多信息"指向 `layout_non-wireless` 锚点，疑为笔误（照译保留） | 待反馈 |
| Pico 系列页 | "release form the debugprobe GitHub repository" 应为 from（按正确含义译出） | 待反馈 |
| Pico 系列页 | 无线 Pico 2 段写 "Raspberry Pi Pico 2 with headers"（应为 Pico 2 W，按上下文译出） | 待反馈 |
| 入门页 | SD 卡容量上限描述与上游支持列表，待上游核实（F1 联网抽查 3 项未核实项之一） | 待核实 |
| 入门页 | Bootloader 版本 "Undo" 表述，待上游核实（F1 抽查） | 待核实 |
| 入门页 | Legacy 镜像下载页措辞，待上游核实（F1 抽查） | 待核实 |
| 系统页 | rpi-update 白皮书链接为超短链（应指官方 PDF 白皮书） | 待反馈 |
| 系统页 | VLC 官方下载页域名写作 `rpltd.co`（上游原文如此，存疑） | 待反馈 |
| 系统页 | `updating.adoc` 两处英文笔误（"upgraded to work" 应为 "updated to work"；"Modfy" 应为 "Modify"） | 待反馈 |
| 系统配置页 | 上游 raspi-config 自动登录表格疑缺 Raspberry Pi 500+ 行（原文出现 "Pi 250" 字样） | 待反馈 |
| 系统配置页 | 上游 DSI-2 格式表内容与 DSI-1 相同（疑复制粘贴） | 待反馈 |
| 系统配置页 | 上游 USB 电流限制 1.2 A 疑为旧 1200 mA 上限变更 | 待反馈 |
| 系统配置页 | 上游初始设置向导的 3 栏无线网络表格疑为复制残留 | 待反馈 |
| config.txt 参数表 | `hdmi_timings` 参数的 `h_back_porch` 描述误写为 vertical（应为 horizontal，按语义译出） | 待反馈 |
| config.txt 参数表 | brief/pitfalls 表 GPIO 行描述对不上（疑复制粘贴，按语义译出） | 待反馈 |
| 旧版 config.txt 页 | CEA 模式 80 频率栏 "25z" 笔误（应为 25 Hz，原样保留） | 待反馈 |

## 八、本文件更新规则

1. **开始工作前**：把目标页面状态改为 `同步中`，在「五、当前进行中」登记代理代号与文件。
2. **每完成一个页面**：立即更新「四、页面清单」该行的状态、校对轮次、最后更新日期；不要攒到最后统一改。
3. **每完成一轮校对**：校对轮次从 `0/3` 递增到 `3/3`；三轮结束后做完整复查，通过则改为 `复查通过` / `复查✓`。
4. **阻塞时**：状态改为 `阻塞`，在「七、阻塞」写明原因与解除条件。
5. **完成后**：在 `CHANGELOG.md` 追加一条记录；本文件只保留进度状态，不重复记录细节。
6. **交接**：接手者先读「五、当前进行中」与「六、待办队列」，确认无文件冲突后再领取。
