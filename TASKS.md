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
| 树莓派 | 17 | 17 | 1 | 3 | 0 | 13 | 0 | 6% |
| 配件 | 20 | 20 | 0 | 0 | 4 | 9 | 7 | 0% |
| 微控制器 | 6 | 6 | 0 | 2 | 0 | 4 | 0 | 0% |
| 服务 | 4 | 4 | 0 | 0 | 0 | 4 | 0 | 0% |
| 安全 | 5 | 5 | 0 | 0 | 0 | 0 | 5 | 0% |
| 合计 | 52 | 52 | 1 | 5 | 4 | 30 | 12 | 2% |

完成率按「复查通过 / 总页数」计算，仅统计完成三轮逐句校对并复查的页面。

## 四、页面清单

状态取值：`待同步`、`同步中`、`部分同步`、`已同步`、`三轮完成`、`复查通过`、`阻塞`。
校对轮次取值：`0/3`、`1/3`、`2/3`、`3/3`、`复查✓`。

### 4.1 树莓派（17）

| 中文文件 | 上游 adoc | 状态 | 校对轮次 | 负责人 | 最后更新 | 备注 |
| -------- | --------- | ---- | -------- | ------ | -------- | ---- |
| `shu-mei-pai/ru-men.md` | `getting-started.adoc` | 同步中 | 0/3 | 代理 B2 | 2026-10-20 | |
| `shu-mei-pai/raspberry-pi-os.md` | `os.adoc` | 同步中 | 0/3 | 代理 B3 | 2026-10-20 | |
| `shu-mei-pai/xi-tong-pei-zhi.md` | `configuration.adoc` | 同步中 | 0/3 | 代理 A10 | 2026-10-20 | |
| `shu-mei-pai/config.txt.md` | `config_txt.adoc` | 同步中 | 0/3 | 代理 A10 | 2026-10-20 | 参数表，重点核对默认值 |
| `shu-mei-pai/linux-nei-he.md` | `linux_kernel.adoc` | 同步中 | 0/3 | 代理 B4 | 2026-10-20 | |
| `shu-mei-pai/yuan-cheng-fang-wen.md` | `remote-access.adoc` | 复查通过 | 复查✓ | 主线程 | 2026-10-18 | 约 160 处修订；截图待中文 UI 重制 |
| `shu-mei-pai/she-xiang-tou-ruan-jian.md` | `camera_software.adoc` | 已同步 | 0/3 | 代理（已结束） | 2026-10-20 | 全页重写至当前上游，待三轮校对 |
| `shu-mei-pai/ren-gong-zhi-neng-ruan-jian.md` | `ai.adoc` | 同步中 | 0/3 | 代理 B9 | 2026-10-20 | |
| `shu-mei-pai/shu-mei-pai-ying-jian.md` | `raspberry-pi.adoc` | 同步中 | 0/3 | 代理 B1 | 2026-10-20 | 全文最长；缺 boot-eeprom 小节待核 |
| `shu-mei-pai/ling-dian-xing-hao.md` | `zero.adoc` | 同步中 | 0/3 | 代理 B5 | 2026-10-20 | |
| `shu-mei-pai/ji-suan-mo-kuai-ying-jian.md` | `compute-module.adoc` | 已同步 | 0/3 | 主线程 | 2026-10-20 | CM5 时代全面同步，待三轮校对 |
| `shu-mei-pai/chu-li-qi.md` | `processors.adoc` | 已同步 | 0/3 | 代理（已结束） | 2026-10-20 | 结构已对齐，待三轮校对 |
| `shu-mei-pai/io-kong-zhi-qi.md` | `io-controllers.adoc` | 同步中 | 0/3 | 代理 B8 | 2026-10-20 | |
| `shu-mei-pai/ruan-jian-lai-yuan.md` | `software-sources.adoc` | 同步中 | 0/3 | 代理 A10 | 2026-10-20 | |
| `shu-mei-pai/jiu-ban-config.txt-can-shu.md` | `legacy_config_txt.adoc` | 同步中 | 0/3 | 代理 A10 | 2026-10-20 | 参数表，重点核对默认值 |
| `shu-mei-pai/jing-dian-dan-ban-ji-suan-ji.md` | `sbcs.adoc` | 同步中 | 0/3 | 代理 B6 | 2026-10-20 | 上游本页有 Raspberry Pi 4B/5 笔误 |
| `shu-mei-pai/jian-pan-ji-suan-ji.md` | `keyboard-computers.adoc` | 同步中 | 0/3 | 代理 B7 | 2026-10-20 | |

### 4.2 配件（20）

| 中文文件 | 上游 adoc | 状态 | 校对轮次 | 负责人 | 最后更新 | 备注 |
| -------- | --------- | ---- | -------- | ------ | -------- | ---- |
| `pei-jian/sd-ka.md` | `sd-cards.adoc` | 同步中 | 0/3 | 代理 A5 | 2026-10-20 | |
| `pei-jian/ssd.md` | `ssds.adoc` | 同步中 | 0/3 | 代理 A5 | 2026-10-20 | |
| `pei-jian/ssd-tao-jian.md` | `ssd-kit.adoc` | 同步中 | 0/3 | 代理 A5 | 2026-10-20 | |
| `pei-jian/m.2-hat+.md` | `m2-hat-plus.adoc` | 部分同步 | 0/3 | 未领取（A4 失败） | 2026-10-20 | 225 行已提交（`7582f30`），工作区另有 37 行未提交改动 |
| `pei-jian/xian-shi-qi.md` | `display.adoc` | 部分同步 | 0/3 | 未领取（A2 失败） | 2026-10-20 | 已有 36 行改动提交（`e04ca00`），需重新领取核对完整性 |
| `pei-jian/chu-mo-xian-shi-ping-2.md` | `touch-display-2.adoc` | 待同步 | 0/3 | 未领取（A2 失败） | 2026-10-20 | 代理连接中断，无改动 |
| `pei-jian/raspberry-pi-monitor.md` | `monitor.adoc` | 待同步 | 0/3 | 未领取（A2 失败） | 2026-10-20 | 代理连接中断，无改动 |
| `pei-jian/she-xiang-tou.md` | `camera.adoc` | 待同步 | 0/3 | 未领取（A1 失败） | 2026-10-20 | 代理连接中断，无改动 |
| `pei-jian/ai-she-xiang-tou.md` | `ai-camera.adoc` | 同步中 | 0/3 | 代理 B10 | 2026-10-20 | 上游本页有 IMX5000 笔误 |
| `pei-jian/jian-pan-he-shu-biao.md` | `keyboard-and-mouse.adoc` | 部分同步 | 0/3 | 未领取（A3 失败） | 2026-10-20 | 仅 5 行改动（`e6053ca`），需重新领取核对 |
| `pei-jian/usb-pei-jian.md` | `usb.adoc` | 同步中 | 0/3 | 代理 A5 | 2026-10-20 | |
| `pei-jian/build-hat.md` | `build-hat.adoc` | 待同步 | 0/3 | 未领取（A3 失败） | 2026-10-20 | 代理未触及，内容停留在 2024 年 |
| `pei-jian/chuan-gan-qi-kuo-zhan-ban-sense-hat.md` | `sense-hat.adoc` | 部分同步 | 0/3 | 未领取（A3 失败） | 2026-10-20 | 434 行改动已提交（`7582f30`），需重新领取核对 |
| `pei-jian/ren-gong-zhi-neng-tao-jian-ai-kit.md` | `ai-kit.adoc` | 待同步 | 0/3 | 未领取（A4 失败） | 2026-10-20 | 代理未触及，内容停留在 2024 年 |
| `pei-jian/ai-hat.md` | `ai-hat-plus.adoc` | 同步中 | 0/3 | 代理 A5 | 2026-10-20 | 产品名含 `+`，勿误判为 AsciiDoc 软换行 |
| `pei-jian/shu-mei-pai-yin-pin-kuo-zhan-ban-raspberry-pi-audio-board.md` | `audio.adoc` | 待同步 | 0/3 | 未领取（A4 失败） | 2026-10-20 | 代理未触及，内容停留在 2024 年 |
| `pei-jian/dian-shi-kuo-zhan-ban-tv-hat.md` | `tv-hat.adoc` | 待同步 | 0/3 | 未领取（A3 失败） | 2026-10-20 | 代理未触及，内容停留在 2024 年 |
| `pei-jian/cm5-bian-cheng-zhi-ju.md` | `cm5-programming-jig.adoc` | 同步中 | 0/3 | 代理 A5 | 2026-10-20 | |
| `pei-jian/zhi-neng-xian-shi-mo-kuai.md` | `smart-display-module.adoc` | 同步中 | 0/3 | 代理 A5 | 2026-10-20 | |
| `pei-jian/bao-hu-ke.md` | `bumper.adoc` | 同步中 | 0/3 | 代理 A5 | 2026-10-20 | |

### 4.3 微控制器（6）

| 中文文件 | 上游 adoc | 状态 | 校对轮次 | 负责人 | 最后更新 | 备注 |
| -------- | --------- | ---- | -------- | ------ | -------- | ---- |
| `wei-kong-zhi-qi/wu-xian-dian-mo-kuai.md` | `radio-modules.adoc` | 已同步 | 0/3 | 主线程 | 2026-10-20 | 本轮新建；含 RM2 规格与认证 |
| `wei-kong-zhi-qi/rp2040.md` | `microcontroller-chips.adoc` | 已同步 | 0/3 | 主线程 | 2026-10-20 | H1 改为「微控制器芯片」；RP1 节仅保留指引 |
| `wei-kong-zhi-qi/shu-mei-pai-pico-he-pico-w.md` | `pico-series.adoc` | 同步中 | 0/3 | 代理 A6 | 2026-10-20 | |
| `wei-kong-zhi-qi/shu-mei-pai-tiao-shi-tao-jian-raspberry-pi-debug-probe.md` | `debug-probe.adoc` | 同步中 | 0/3 | 代理 A6 | 2026-10-20 | |
| `wei-kong-zhi-qi/micropython.md` | `micropython.adoc` | 同步中 | 0/3 | 代理 A6 | 2026-10-20 | |
| `wei-kong-zhi-qi/c-c++-sdk.md` | `c_sdk.adoc` | 同步中 | 0/3 | 代理 A6 | 2026-10-20 | |

### 4.4 服务（4）

| 中文文件 | 上游 adoc | 状态 | 校对轮次 | 负责人 | 最后更新 | 备注 |
| -------- | --------- | ---- | -------- | ------ | -------- | ---- |
| `fu-wu/shu-mei-pai-zhang-hao-raspberry-pi-id.md` | `id.adoc` | 同步中 | 0/3 | 代理 A7 | 2026-10-20 | |
| `fu-wu/shu-mei-pai-yuan-cheng-fang-wen-raspberry-pi-connect.md` | `connect.adoc` | 同步中 | 0/3 | 代理 A7 | 2026-10-20 | |
| `fu-wu/shu-mei-pai-connect-qi-ye-ban.md` | `connect-for-organisations.adoc` | 同步中 | 0/3 | 代理 A7 | 2026-10-20 | |
| `fu-wu/shu-mei-pai-shu-jia.md` | `bookshelf.adoc` | 同步中 | 0/3 | 代理 A7 | 2026-10-20 | |

### 4.5 安全（5）

| 中文文件 | 上游 adoc | 状态 | 校对轮次 | 负责人 | 最后更新 | 备注 |
| -------- | --------- | ---- | -------- | ------ | -------- | ---- |
| `an-quan/an-quan-gai-shu.md` | `security.adoc` | 待同步 | 0/3 | 未领取（A8 失败） | 2026-10-20 | 代理连接中断，无改动 |
| `an-quan/an-quan-jia-gou.md` | `security-architecture.adoc` | 待同步 | 0/3 | 未领取（A8 失败） | 2026-10-20 | 代理连接中断，无改动 |
| `an-quan/an-quan-qi-dong-pei-zhi-qi.md` | `secure-boot-provisioner.adoc` | 待同步 | 0/3 | 未领取（A8 失败） | 2026-10-20 | 上游 image 属性有多余引号 |
| `an-quan/yun-ying-an-quan.md` | `operational-security.adoc` | 待同步 | 0/3 | 未领取（A8 失败） | 2026-10-20 | 上游 fail2ban 示例缺等号 |
| `an-quan/ufw-fang-huo-qiang.md` | `ufw.adoc` | 待同步 | 0/3 | 未领取（A8 失败） | 2026-10-20 | 端口号与规则须逐条核对 |

### 4.6 项目自有（3）

| 中文文件 | 上游 | 状态 | 最后更新 | 备注 |
| -------- | ---- | ---- | -------- | ---- |
| `qian-yan/ci-hui-biao.md` | 无 | 维护中 | 2026-10-20 | 已补 Control Centre、NFS export |
| `qian-yan/guan-yu-wo-men.md` | 无 | 不适用 | 2024 | |
| `qian-yan/ban-quan-shuo-ming.md` | 无 | 不适用 | 2024 | |

## 五、当前进行中

统计时间：2026-10-20 03:14。滚动更新：每次代理领取或结束时立即修改本节。

| 代理 | 负责文件 | 开始时间 | 目标检查点 | 状态 |
| ---- | -------- | -------- | ---------- | ---- |
| A1 | `pei-jian/she-xiang-tou.md` | 2026-10-20 | CP-2 + CP-3 | 失败（连接中断），无改动 |
| A2 | `pei-jian/xian-shi-qi.md`、`chu-mo-xian-shi-ping-2.md`、`raspberry-pi-monitor.md` | 2026-10-20 | CP-2 + CP-3 | 失败（连接中断），仅 `xian-shi-qi.md` 有部分改动 |
| A3 | `pei-jian/jian-pan-he-shu-biao.md`、`build-hat.md`、`chuan-gan-qi-kuo-zhan-ban-sense-hat.md`、`dian-shi-kuo-zhan-ban-tv-hat.md` | 2026-10-20 | CP-2 + CP-3 | 失败（连接中断），键鼠与 Sense HAT 有部分改动 |
| A4 | `pei-jian/m.2-hat+.md`、`ren-gong-zhi-neng-tao-jian-ai-kit.md`、`shu-mei-pai-yin-pin-kuo-zhan-ban-raspberry-pi-audio-board.md` | 2026-10-20 | CP-2 + CP-3 | 失败（连接中断），仅 `m.2-hat+.md` 有改动 |
| A5 | `pei-jian/sd-ka.md`、`ssd.md`、`ssd-tao-jian.md`、`usb-pei-jian.md`、`ai-hat.md`、`bao-hu-ke.md`、`cm5-bian-cheng-zhi-ju.md`、`zhi-neng-xian-shi-mo-kuai.md` | 2026-10-20 | CP-2 + CP-3 | 进行中 |
| A6 | `wei-kong-zhi-qi/shu-mei-pai-pico-he-pico-w.md`、`shu-mei-pai-tiao-shi-tao-jian-raspberry-pi-debug-probe.md`、`micropython.md`、`c-c++-sdk.md` | 2026-10-20 | CP-2 + CP-3 | 进行中 |
| A7 | `fu-wu/` 4 页 | 2026-10-20 | CP-2 + CP-3 | 进行中 |
| A8 | `an-quan/` 5 页 | 2026-10-20 | CP-2 + CP-3 | 失败（连接中断），无改动 |
| A9 | `ru-men.md`、`raspberry-pi-os.md`、`linux-nei-he.md` | 2026-10-20 | CP-2 + CP-3 | 失败（连接中断），由 B2/B3/B4 接替 |
| A10 | `xi-tong-pei-zhi.md`、`config.txt.md`、`jiu-ban-config.txt-can-shu.md`、`ruan-jian-lai-yuan.md` | 2026-10-20 | CP-2 + CP-3 | 进行中 |
| B1 | `shu-mei-pai/shu-mei-pai-ying-jian.md` | 2026-10-20 | CP-2 + CP-3 | 进行中 |
| B2 | `shu-mei-pai/ru-men.md` | 2026-10-20 | CP-2 + CP-3 | 进行中 |
| B3 | `shu-mei-pai/raspberry-pi-os.md` | 2026-10-20 | CP-2 + CP-3 | 进行中 |
| B4 | `shu-mei-pai/linux-nei-he.md` | 2026-10-20 | CP-2 + CP-3 | 进行中 |
| B5 | `shu-mei-pai/ling-dian-xing-hao.md` | 2026-10-20 | CP-2 + CP-3 | 进行中 |
| B6 | `shu-mei-pai/jing-dian-dan-ban-ji-suan-ji.md` | 2026-10-20 | CP-2 + CP-3 | 进行中 |
| B7 | `shu-mei-pai/jian-pan-ji-suan-ji.md` | 2026-10-20 | CP-2 + CP-3 | 进行中 |
| B8 | `shu-mei-pai/io-kong-zhi-qi.md` | 2026-10-20 | CP-2 + CP-3 | 进行中 |
| B9 | `shu-mei-pai/ren-gong-zhi-neng-ruan-jian.md` | 2026-10-20 | CP-2 + CP-3 | 进行中 |
| B10 | `pei-jian/ai-she-xiang-tou.md` | 2026-10-20 | CP-2 + CP-3 | 进行中 |

## 六、待办队列

| 优先级 | 事项 | 范围 | 依赖 |
| ------ | ---- | ---- | ---- |
| P0 | 重新派发 A1、A2、A3、A4、A8 五路失败代理 | 15 页 | 代理恢复 |
| P0 | 汇总本轮 20 路代理结果，逐文件复核后更新本文件状态 | 全部 | 代理结束 |
| P0 | 对已同步页面执行三轮逐句校对 | `yuan-cheng-fang-wen`、`ji-suan-mo-kuai-ying-jian`、`she-xiang-tou-ruan-jian`、`chu-li-qi`、`rp2040`、`wu-xian-dian-mo-kuai` | 代理结束 |
| P1 | CP-5：本地跑 markdownlint（`npx markdownlint-cli2`），并对 `TASKS.md` 等新增文件补一次 PR 检查 | CI | 无 |
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
| 远程访问页 | IPv6 网络启动一节 `FTP` 应为 `TFTP`；`/proc/mounts` 反引号错位；`Atfer` 应为 `After` | 待反馈 |

## 八、本文件更新规则

1. **开始工作前**：把目标页面状态改为 `同步中`，在「五、当前进行中」登记代理代号与文件。
2. **每完成一个页面**：立即更新「四、页面清单」该行的状态、校对轮次、最后更新日期；不要攒到最后统一改。
3. **每完成一轮校对**：校对轮次从 `0/3` 递增到 `3/3`；三轮结束后做完整复查，通过则改为 `复查通过` / `复查✓`。
4. **阻塞时**：状态改为 `阻塞`，在「七、阻塞」写明原因与解除条件。
5. **完成后**：在 `CHANGELOG.md` 追加一条记录；本文件只保留进度状态，不重复记录细节。
6. **交接**：接手者先读「五、当前进行中」与「六、待办队列」，确认无文件冲突后再领取。
