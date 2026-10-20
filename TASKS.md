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
| CP-2 逐段同步 | 52 页 | 进行中 | | 见「四、页面清单」逐页状态 |
| CP-3 规范合规 | 52 页 | 进行中 | | 见「四、页面清单」逐页校对轮次 |
| CP-4 引用与目录 | `SUMMARY.md`、`mu-lu.md`、正文 | 通过 | 2026-10-20 | `SUMMARY.md` 58 条与 `mu-lu.md` 卡片链接均无失效；55 个页面的站内相对链接 0 处失效 |
| CP-5 构建与 CI | 全仓库 | 部分通过 | 2026-10-20 | `sync-headers`、`file-name-check` 在 main 上均为 success；`Markdown-lint2-pr` 仅在 PR 触发、`links` 为定时/手动，尚未执行 |

### 3.2 页面统计

统计时间：2026-10-20 03:20

| 板块 | 上游页数 | 中文页数 | 复查通过 | 已同步待复查 | 部分同步 | 同步中 | 待同步 | 完成率 |
| ---- | -------- | -------- | -------- | ------------ | -------- | ------ | ------ | ------ |
| 树莓派 | 17 | 17 | 1 | 6 | 0 | 8 | 2 | 6% |
| 配件 | 20 | 20 | 0 | 0 | 4 | 1 | 15 | 0% |
| 微控制器 | 6 | 6 | 0 | 2 | 0 | 4 | 0 | 0% |
| 服务 | 4 | 4 | 0 | 0 | 0 | 4 | 0 | 0% |
| 安全 | 5 | 5 | 0 | 1 | 0 | 4 | 0 | 0% |
| 合计 | 52 | 52 | 1 | 9 | 4 | 21 | 17 | 2% |

完成率按「复查通过 / 总页数」计算，仅统计完成三轮逐句校对并复查的页面。

## 四、页面清单

状态取值：`待同步`、`同步中`、`部分同步`、`已同步`、`三轮完成`、`复查通过`、`阻塞`。
校对轮次取值：`0/3`、`1/3`、`2/3`、`3/3`、`复查✓`。

### 4.1 树莓派（17）

| 中文文件 | 上游 adoc | 状态 | 校对轮次 | 负责人 | 最后更新 | 备注 |
| -------- | --------- | ---- | -------- | ------ | -------- | ---- |
| `shu-mei-pai/ru-men.md` | `getting-started.adoc` | 同步中 | 0/3 | 代理 F1 | 2026-10-20 | B2 失败重派；无改动，全新同步；本地存档 `script/upstream-gettingstarted/` |
| `shu-mei-pai/raspberry-pi-os.md` | `os.adoc` | 同步中 | 0/3 | 代理 F2 | 2026-10-20 | B3 失败重派；无改动，全新同步；本地存档 `script/upstream-os/` |
| `shu-mei-pai/xi-tong-pei-zhi.md` | `configuration.adoc` | 同步中 | 0/3 | 代理 F3 | 2026-10-20 | A10 失联无改动，F3 全新同步 |
| `shu-mei-pai/config.txt.md` | `config_txt.adoc` | 同步中 | 0/3 | 代理 F4 | 2026-10-20 | 参数表，重点核对默认值；A10 失联无改动，F4 全新同步 |
| `shu-mei-pai/linux-nei-he.md` | `linux_kernel.adoc` | 已同步 | 0/3 | 代理 B4（完成） | 2026-10-20 | B4 整页重写已提交（`79d516b`），主线程已复核：7 节与上游一一对应（含 5 级标题）、BCM2712/kernel_2712 等齐备；待三轮逐句校对 |
| `shu-mei-pai/yuan-cheng-fang-wen.md` | `remote-access.adoc` | 复查通过 | 复查✓ | 主线程 | 2026-10-18 | 约 160 处修订；截图待中文 UI 重制 |
| `shu-mei-pai/she-xiang-tou-ruan-jian.md` | `camera_software.adoc` | 已同步 | 0/3 | 代理（已结束） | 2026-10-20 | 全页重写至当前上游，待三轮校对 |
| `shu-mei-pai/ren-gong-zhi-neng-ruan-jian.md` | `ai.adoc` | 已同步 | 0/3 | 代理 F7（完成） | 2026-10-20 | B9 落盘版逐句核验零改动，主线程已验证；待三轮逐句校对 |
| `shu-mei-pai/shu-mei-pai-ying-jian.md` | `raspberry-pi.adoc` | 已同步 | 0/3 | 未领取（B1 失败） | 2026-10-20 | 继承 `771d4f3` 的同步结果，B1 无新增改动；缺 boot-eeprom 小节待核 |
| `shu-mei-pai/ling-dian-xing-hao.md` | `zero.adoc` | 已同步 | 0/3 | 代理 F7（完成） | 2026-10-20 | F7 完成 4 处修正（microSD→存储卡插槽），B5 落盘版核验可用，主线程已验证落盘；待三轮逐句校对 |
| `shu-mei-pai/ji-suan-mo-kuai-ying-jian.md` | `compute-module.adoc` | 已同步 | 0/3 | 主线程 | 2026-10-20 | CM5 时代全面同步，待三轮校对 |
| `shu-mei-pai/chu-li-qi.md` | `processors.adoc` | 已同步 | 0/3 | 代理（已结束） | 2026-10-20 | 结构已对齐，待三轮校对 |
| `shu-mei-pai/io-kong-zhi-qi.md` | `io-controllers.adoc` | 已同步 | 1/3 | 代理 B8（完成） | 2026-10-20 | 8 处修订；RP1 规格与上游一致；视频宏改为普通链接。注意本文件为 LF，与仓库其他 CRLF 文件不同 |
| `shu-mei-pai/ruan-jian-lai-yuan.md` | `software-sources.adoc` | 同步中 | 0/3 | 代理 F11 | 2026-10-20 | A10 失联，部分改动已落盘（`da040ea`），F11 核验补齐 |
| `shu-mei-pai/jiu-ban-config.txt-can-shu.md` | `legacy_config_txt.adoc` | 同步中 | 0/3 | 代理 F6（打回重做中） | 2026-10-20 | 首轮报告与落盘不符（声称 3 处修正与 11 H2，实测文件无改动、H2 为 9），主线程已打回并要求附 grep 证据 |
| `shu-mei-pai/jing-dian-dan-ban-ji-suan-ji.md` | `sbcs.adoc` | 已同步 | 0/3 | 代理 F8（完成） | 2026-10-20 | F8 仅修 1 处（如实翻译上游 Pi 5 笔误，2 行 diff），B6 落盘版核验可用，主线程已验证；待三轮逐句校对 |
| `shu-mei-pai/jian-pan-ji-suan-ji.md` | `keyboard-computers.adoc` | 同步中 | 0/3 | 代理 F9 | 2026-10-20 | B7 失联，部分改动已落盘（`4a6ac8e`），F9 核验补齐 |

### 4.2 配件（20）

| 中文文件 | 上游 adoc | 状态 | 校对轮次 | 负责人 | 最后更新 | 备注 |
| -------- | --------- | ---- | -------- | ------ | -------- | ---- |
| `pei-jian/sd-ka.md` | `sd-cards.adoc` | 已同步 | 0/3 | 代理 E8（完成） | 2026-10-20 | E8 核查与上游零差异，主线程已复核；待三轮逐句校对 |
| `pei-jian/ssd.md` | `ssds.adoc` | 已同步 | 0/3 | 代理 E9（完成） | 2026-10-20 | E9 核查与上游零差异，主线程已复核；待三轮逐句校对 |
| `pei-jian/ssd-tao-jian.md` | `ssd-kit.adoc` | 已同步 | 0/3 | 代理 E10（完成） | 2026-10-20 | E10 核查与上游一致并清理 2 行冗余，主线程已复核；待三轮逐句校对 |
| `pei-jian/m.2-hat+.md` | `m2-hat-plus.adoc` | 已同步 | 0/3 | 代理 E5（完成） | 2026-10-20 | E5 重写同步至上游（新增 Compact/Boot 两节、修订 NVMe 启动），主线程已复核；待三轮逐句校对 |
| `pei-jian/xian-shi-qi.md` | `display.adoc` | 已同步 | 0/3 | 代理 E17（完成） | 2026-10-20 | E17 完成 2 处 config.txt 站内链接修正（上游 xref 已核实），主线程已复核；待三轮逐句校对 |
| `pei-jian/chu-mo-xian-shi-ping-2.md` | `touch-display-2.adoc` | 已同步 | 0/3 | 代理 E18（完成） | 2026-10-20 | E18 完成 2 处修订（any and all 漏译、Lite 术语），主线程已复核；待三轮逐句校对 |
| `pei-jian/raspberry-pi-monitor.md` | `monitor.adoc` | 已同步 | 0/3 | 代理 E19（完成） | 2026-10-20 | E19 核查与上游零差异，主线程已复核；待三轮逐句校对 |
| `pei-jian/she-xiang-tou.md` | `camera.adoc` | 已同步 | 0/3 | 代理 C7（完成） | 2026-10-20 | C7 全页重写同步至上游（12 节 1:1；RFI/光谱/规格表/Picamera2 链接齐备），主线程已复核；待三轮逐句校对 |
| `pei-jian/ai-she-xiang-tou.md` | `ai-camera.adoc` | 已同步 | 0/3 | 代理 E16（完成） | 2026-10-20 | E16 完成 1 处修订（IMX5000→IMX500，上游笔误），主线程已复核；待三轮逐句校对 |
| `pei-jian/jian-pan-he-shu-biao.md` | `keyboard-and-mouse.adoc` | 已同步 | 0/3 | 代理 E1（完成） | 2026-10-20 | E1 完成 1 处修订（标题与上游 "with your Mouse" 一致），主线程已复核；待三轮逐句校对 |
| `pei-jian/usb-pei-jian.md` | `usb.adoc` | 已同步 | 0/3 | 代理 E11（完成） | 2026-10-20 | E11 核查与上游零差异，主线程已复核；待三轮逐句校对 |
| `pei-jian/build-hat.md` | `build-hat.adoc` | 已同步 | 0/3 | 代理 E2（完成） | 2026-10-20 | E2 全页重写同步至上游（Trixie 警告、Keyboard-series、配方步骤序号、根身份运行配置生成器），主线程已复核；待三轮逐句校对 |
| `pei-jian/chuan-gan-qi-kuo-zhan-ban-sense-hat.md` | `sense-hat.adoc` | 已同步 | 0/3 | 代理 E3（完成） | 2026-10-20 | E3 重组为上游 6 节结构并完成 13 类修正（椭球拟合 e/m、故障排除节、sudo reboot 等），主线程已复核；待三轮逐句校对 |
| `pei-jian/ren-gong-zhi-neng-tao-jian-ai-kit.md` | `ai-kit.adoc` | 已同步 | 0/3 | 代理 E6（完成） | 2026-10-20 | E6 按上游重写（AI Kit 已停产，页缩减为停产声明 + 硬件/安装/后续步骤），主线程已复核；待三轮逐句校对 |
| `pei-jian/ai-hat.md` | `ai-hat-plus.adoc` | 已同步 | 0/3 | 代理 E12（完成） | 2026-10-20 | E12 完成 4 处修订（AI HAT+ 2、Hailo-10H 40 TOPS、Viador），主线程已复核；待三轮逐句校对 |
| `pei-jian/shu-mei-pai-yin-pin-kuo-zhan-ban-raspberry-pi-audio-board.md` | `audio.adoc` | 已同步 | 0/3 | 代理 E7（完成） | 2026-10-20 | E7 全页重写同步至上游（17 类修订，涵盖 DAC Pro/DAC+/DigiAMP+/Codec Zero 全线），主线程已复核；待三轮逐句校对 |
| `pei-jian/dian-shi-kuo-zhan-ban-tv-hat.md` | `tv-hat.adoc` | 已同步 | 0/3 | 代理 E4（完成） | 2026-10-20 | E4 重写同步至上游（删陈旧截图链接、修正 2B 要求与 Freeview/VLC 链接），主线程已复核；待三轮逐句校对 |
| `pei-jian/cm5-bian-cheng-zhi-ju.md` | `cm5-programming-jig.adoc` | 已同步 | 0/3 | 代理 E14（完成） | 2026-10-20 | E14 核查与上游零差异（8 节含安全警告全齐），主线程已复核；待三轮逐句校对 |
| `pei-jian/zhi-neng-xian-shi-mo-kuai.md` | `smart-display-module.adoc` | 已同步 | 0/3 | 代理 E15（完成） | 2026-10-20 | E15 完成 3 处锚点/链接修正（`684ec85` 已落盘），主线程已复核；待三轮逐句校对 |
| `pei-jian/bao-hu-ke.md` | `bumper.adoc` | 已同步 | 0/3 | 代理 E13（完成） | 2026-10-20 | E13 核查与上游零差异，主线程已复核；待三轮逐句校对 |

### 4.3 微控制器（6）

| 中文文件 | 上游 adoc | 状态 | 校对轮次 | 负责人 | 最后更新 | 备注 |
| -------- | --------- | ---- | -------- | ------ | -------- | ---- |
| `wei-kong-zhi-qi/wu-xian-dian-mo-kuai.md` | `radio-modules.adoc` | 已同步 | 0/3 | 主线程 | 2026-10-20 | 本轮新建；含 RM2 规格与认证 |
| `wei-kong-zhi-qi/rp2040.md` | `microcontroller-chips.adoc` | 已同步 | 0/3 | 主线程 | 2026-10-20 | H1 改为「微控制器芯片」；RP1 节仅保留指引 |
| `wei-kong-zhi-qi/shu-mei-pai-pico-he-pico-w.md` | `pico-series.adoc` | 已同步 | 0/3 | 代理 F10（完成） | 2026-10-20 | F10 全页重写：上游结构重构（8 型号汇总表、两代变体表、SWD 表），23 个链接迁 pip.raspberrypi.com，主线程已验证落盘；待三轮逐句校对 |
| `wei-kong-zhi-qi/shu-mei-pai-tiao-shi-tao-jian-raspberry-pi-debug-probe.md` | `debug-probe.adoc` | 已同步 | 0/3 | 代理 F5（完成） | 2026-10-20 | F5 全量重写（8 H2；改用 VS Code 扩展安装路线、补 UART 连接、RTT 表），主线程已验证落盘；待三轮逐句校对 |
| `wei-kong-zhi-qi/micropython.md` | `micropython.adoc` | 已同步 | 0/3 | 代理 F5（完成） | 2026-10-20 | F5 全量重写（4 H2；数据手册编号、Bug 列表与 Pico 2 W 变体），主线程已验证落盘；待三轮逐句校对 |
| `wei-kong-zhi-qi/c-c++-sdk.md` | `c_sdk.adoc` | 已同步 | 0/3 | 代理 F5（完成） | 2026-10-20 | F5 全量重写（4 H2；blink_universal、pico_setup.sh 等），主线程已验证落盘；待三轮逐句校对 |

### 4.4 服务（4）

| 中文文件 | 上游 adoc | 状态 | 校对轮次 | 负责人 | 最后更新 | 备注 |
| -------- | --------- | ---- | -------- | ------ | -------- | ---- |
| `fu-wu/shu-mei-pai-zhang-hao-raspberry-pi-id.md` | `id.adoc` | 同步中 | 0/3 | 代理 F12 | 2026-10-20 | A7 失联，改动已落盘（`d441b30`），F12 核验补齐 |
| `fu-wu/shu-mei-pai-yuan-cheng-fang-wen-raspberry-pi-connect.md` | `connect.adoc` | 同步中 | 0/3 | 代理 F12 | 2026-10-20 | A7 失联，改动已落盘（`3c4e97f`），F12 核验补齐 |
| `fu-wu/shu-mei-pai-connect-qi-ye-ban.md` | `connect-for-organisations.adoc` | 同步中 | 0/3 | 代理 F12 | 2026-10-20 | A7 失联，改动已落盘（`a67a29d`），F12 核验补齐 |
| `fu-wu/shu-mei-pai-shu-jia.md` | `bookshelf.adoc` | 同步中 | 0/3 | 代理 F12 | 2026-10-20 | A7 失联，改动已落盘（`a67a29d`），F12 核验补齐 |

### 4.5 安全（5）

| 中文文件 | 上游 adoc | 状态 | 校对轮次 | 负责人 | 最后更新 | 备注 |
| -------- | --------- | ---- | -------- | ------ | -------- | ---- |
| `an-quan/an-quan-gai-shu.md` | `security.adoc` | 已同步 | 0/3 | 代理 C2（完成） | 2026-10-20 | C2 完成 2 处修订（microSD→存储卡、security hygiene 误译修正），主线程已逐条复核；待三轮逐句校对 |
| `an-quan/an-quan-jia-gou.md` | `security-architecture.adoc` | 已同步 | 0/3 | 代理 C3（完成） | 2026-10-20 | C3 逐段核查与上游完全一致，无需修改；主线程已复核结构；待三轮逐句校对 |
| `an-quan/an-quan-qi-dong-pei-zhi-qi.md` | `secure-boot-provisioner.adoc` | 已同步 | 0/3 | 代理 C4（完成） | 2026-10-20 | C4 完成 5 处修订（安全启动链、遭到入侵、存储卡、锚点、CSV 导语），主线程已逐条复核；待三轮逐句校对 |
| `an-quan/yun-ying-an-quan.md` | `operational-security.adoc` | 已同步 | 0/3 | 代理 C5（完成） | 2026-10-20 | C5 修正 fail2ban 示例缺等号（上游已知问题）并将 2 处外链内部化，主线程已复核锚点；待三轮逐句校对 |
| `an-quan/ufw-fang-huo-qiang.md` | `ufw.adoc` | 已同步 | 0/3 | 代理 C6（完成） | 2026-10-20 | C6 逐段核查零修改，主线程已复核结构与 CP-3；待三轮逐句校对 |

### 4.6 项目自有（3）

| 中文文件 | 上游 | 状态 | 最后更新 | 备注 |
| -------- | ---- | ---- | -------- | ---- |
| `qian-yan/ci-hui-biao.md` | 无 | 维护中 | 2026-10-20 | 已补 Control Centre、NFS export |
| `qian-yan/guan-yu-wo-men.md` | 无 | 不适用 | 2024 | |
| `qian-yan/ban-quan-shuo-ming.md` | 无 | 不适用 | 2024 | |

## 五、当前进行中

统计时间：2026-10-20 03:50。滚动更新：每次代理领取或结束时立即修改本节。

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
| F1 | `shu-mei-pai/ru-men.md` | 2026-10-20 | CP-2 + CP-3 | 进行中（B2 失败重派，全新同步） |
| F2 | `shu-mei-pai/raspberry-pi-os.md` | 2026-10-20 | CP-2 + CP-3 | 进行中（B3 失败重派，全新同步） |
| F3 | `shu-mei-pai/xi-tong-pei-zhi.md` | 2026-10-20 | CP-2 + CP-3 | 进行中（A10 失联接替，全新同步） |
| F4 | `shu-mei-pai/config.txt.md` | 2026-10-20 | CP-2 + CP-3 | 进行中（A10 失联接替，全新同步，参数表） |
| F5 | `wei-kong-zhi-qi/shu-mei-pai-tiao-shi-tao-jian-raspberry-pi-debug-probe.md`、`micropython.md`、`c-c++-sdk.md` | 2026-10-20 | CP-2 + CP-3 | 完成：三页全量重写至上游新结构（主线程已验证落盘） |
| F6 | `shu-mei-pai/jiu-ban-config.txt-can-shu.md` | 2026-10-20 | CP-2 + CP-3 | 打回重做：首轮报告失实（声称修正未落盘），已限期重做并要求附 grep 证据 |
| F7 | `shu-mei-pai/ling-dian-xing-hao.md`、`ren-gong-zhi-neng-ruan-jian.md` | 2026-10-20 | CP-2 + CP-3 | 完成：零型页 4 处修正、AI 软件页零改动（主线程已验证落盘） |
| F8 | `shu-mei-pai/jing-dian-dan-ban-ji-suan-ji.md` | 2026-10-20 | CP-2 + CP-3 | 完成：1 处修正（如实翻译上游 Pi 5 笔误；主线程已验证） |
| F9 | `shu-mei-pai/jian-pan-ji-suan-ji.md` | 2026-10-20 | CP-2 + CP-3 | 完成：零改动，B7 落盘版核验可用（主线程已验证） |
| F10 | `wei-kong-zhi-qi/shu-mei-pai-pico-he-pico-w.md` | 2026-10-20 | CP-2 + CP-3 | 完成：全页重写至上游新结构（主线程已验证落盘） |
| F11 | `shu-mei-pai/ruan-jian-lai-yuan.md` | 2026-10-20 | CP-2 + CP-3 | 进行中（A10 失联接替，核验补齐） |
| F12 | `fu-wu/` 4 页 | 2026-10-20 | CP-2 + CP-3 | 进行中（A7 失联接替，核验补齐） |

## 六、待办队列

| 优先级 | 事项 | 范围 | 依赖 |
| ------ | ---- | ---- | ---- |
| P0 | 第一波重派已全部完成并验收：安全 5 页 + 摄像头页（C1 交付不实打回，C7 重做成功） | 6 页 | 完成 |
| P0 | 第二波重派已全部完成并验收：配件板块 19 页（E1–E19） | 19 页 | 完成 |
| P0 | 原「待派」`ru-men.md`、`raspberry-pi-os.md` 已派 F1/F2；失联代理（A6/A7/A10/B5/B6/B7/B9）遗留 13 页已派 F3–F12 接替（全新同步 7 页 + 核验补齐 6 页） | 15 页 | F 波进行中 |
| P0 | 汇总各波代理结果，逐文件复核后更新本文件状态 | 全部 | 滚动进行 |
| P0 | 对已同步页面执行三轮逐句校对 | `yuan-cheng-fang-wen`、`ji-suan-mo-kuai-ying-jian`、`she-xiang-tou-ruan-jian`、`chu-li-qi`、`rp2040`、`wu-xian-dian-mo-kuai` | 代理结束 |
| P1 | 词汇表补录 I/O 控制器页报告的新术语（I/O controller、single-board computer、pin spacing、USB host controller、tightly-coupled memory、Timing generator、ISP front-end、bitstream 等 12 条） | `qian-yan/ci-hui-biao.md` | 无 |
| P2 | 统一 `shu-mei-pai/io-kong-zhi-qi.md` 的换行符（当前 LF，其余页面 CRLF） | 1 页 | 无 |
| P1 | 检查 `shu-mei-pai-ying-jian.md` 是否缺 `boot-eeprom` 小节 | 树莓派硬件 | B1 结果 |
| P2 | 向上游反馈已发现的原文错误 | 见「七」 | 用户批准 |
| P3 | 图片本地化：正文中仍指向 `www.raspberrypi.com` 的图片迁至 `.gitbook/assets/` | 全部页面 | 需可访问图片源 |
| P4 | 中文 UI 重制两张 Control Centre 截图 | `shu-mei-pai/yuan-cheng-fang-wen.md` | 人工在中文系统截图 |

## 七、阻塞与上游异常

### 7.1 阻塞

* 官方文档网页受 Cloudflare 挑战，`curl` 无法直接抓取；图片也无法下载，P3 图片本地化暂时受阻。
* 中文 UI 截图需人工操作，无法由代理完成。

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

## 八、本文件更新规则

1. **开始工作前**：把目标页面状态改为 `同步中`，在「五、当前进行中」登记代理代号与文件。
2. **每完成一个页面**：立即更新「四、页面清单」该行的状态、校对轮次、最后更新日期；不要攒到最后统一改。
3. **每完成一轮校对**：校对轮次从 `0/3` 递增到 `3/3`；三轮结束后做完整复查，通过则改为 `复查通过` / `复查✓`。
4. **阻塞时**：状态改为 `阻塞`，在「七、阻塞」写明原因与解除条件。
5. **完成后**：在 `CHANGELOG.md` 追加一条记录；本文件只保留进度状态，不重复记录细节。
6. **交接**：接手者先读「五、当前进行中」与「六、待办队列」，确认无文件冲突后再领取。
