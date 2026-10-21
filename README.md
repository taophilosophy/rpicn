# Raspberry Pi 树莓派中文文档

本文档是 [Raspberry Pi Documentation](https://www.raspberrypi.com/documentation/) 的简体中文翻译版本。

本项目开源地址：<https://github.com/taophilosophy/rpicn>

**[点击此处可浏览目录](mu-lu.md)**

>**注意**
>
>全部 52 个页面已完成三轮逐句校对并复查通过（2026-10-21，完成率 100%）。后续将随上游版本更新持续同步，具体历史请参考[编辑日志](CHANGELOG.md)。

## PDF 文档

> **PDF 文档**
>
> - 使用由 [safreya](https://github.com/safreya) 提供的脚本：
>   
>><https://github.com/FreeBSD-Ask/gitbook-pdf-export> 
>>
>>可用于导出本书的 PDF 文档。该脚本使用 Python 3 编写，仅在 Windows 10、FreeBSD 14 上测试过。
>> 
>> 具体使用方法见该项目的 README。

## 关于我们

本项目由 FreeBSD 中文社区发起。

如有问题请 PR 或 Issue。

## 版本说明

**2026-10-20 起全部 52 个页面已同步至 [树莓派官方文档](https://raspberrypi.com/documentation) 当前版本**（英文原版 GitHub `master` 分支；上一基线为 [2024.9.8 版本](https://github.com/raspberrypi/documentation/commit/1b7709fea907aed7af8950f936ccfd1b82a29edd)，其间上游新增配件 11 页、计算机 6 页、微控制器 2 页、安全板块 5 页、服务 2 页，本项目已全部补译）。

### 翻译校对进度（2026-10-21）

52 页 **全部完成“三轮逐句校对 + 一轮复查”，完成率 100%**：

| 板块 | 页数 | 已复查 |
| ---- | ---- | ---- |
| 树莓派 | 17 | 17（100%） |
| 配件 | 20 | 20（100%） |
| 微控制器 | 6 | 6（100%） |
| 服务 | 4 | 4（100%） |
| 安全 | 5 | 5（100%） |
| **合计** | **52** | **52（100%）** |

校对覆盖事实完整性（对照上游 AsciiDoc 逐句、表格逐格、代码块逐行）、语言质量（术语统一、欧化句式）与规范合规（CRLF、图片 `../` 前缀、提示块、引号、锚点有效性）。逐页状态见[任务书](TASKS.md)，编辑历史见[编辑日志](CHANGELOG.md)。

### 校对标准

| 维度 | 要求 |
| ---- | ---- |
| 事实完整性 | 逐句对照 `script/upstream-*/` 中的 AsciiDoc 原文；表格逐格核对，代码块逐行比对；上游笔误按正确含义译出并记入异常清单 |
| 语言质量 | 术语遵循[词汇表](qian-yan/ci-hui-biao.md)；避免欧化句式与不必要被动句；标点用全角 |
| 规范合规 | 全文件 CRLF 换行、UTF-8 无 BOM；图片引用统一 `../.gitbook/assets/` 前缀；提示块写作 `>**注意**`（不做 `> 正文`） |
| 引号 | 一律使用中文弯引号 `""` `''`；**禁止**日式/直角引号 `「」` `『』` |
| 链接 | 站内链接使用相对路径，锚点必须命中实际标题；禁止“见第 X 节”式硬编码引用 |

### 项目结构

| 目录 | 内容 |
| ---- | ---- |
| `shu-mei-pai/` | 树莓派（17 页）：入门、系统、硬件、配置、摄像头等 |
| `pei-jian/` | 配件（20 页）：摄像头、HAT、显示屏、音频板、SSD 等 |
| `wei-kong-zhi-qi/` | 微控制器（6 页）：Pico、RP2040、MicroPython、C/C++ SDK 等 |
| `fu-wu/` | 服务（4 页）：树莓派 ID/账号、Connect、Connect 企业版、书架 |
| `an-quan/` | 安全（5 页）：概述、架构、启动配置器、UFW、运营安全 |
| `qian-yan/` | 前言与词汇表 |
| `script/upstream-*/` | 各页对应的上游 AsciiDoc 原文（校对基准） |
| `.gitbook/assets/` | 全部配图与视频资源 |
| `TASKS.md` / `AGENTS.md` | 逐页状态任务书 / 仓库约定与接手说明 |

## 参与贡献

本项目欢迎 PR 与 Issue。翻译规范、上游追踪方法与用词约定请见[贡献指南](CONTRIBUTING.md)，行为准则见[行为准则](CODE_OF_CONDUCT.md)。

有权限协作的译者请注意：开工前必读[任务书](TASKS.md)与[仓库约定](AGENTS.md)，其中包含检查点定义、逐页状态、术语规范与接手说明。

## 版权说明

[树莓派官方文档](https://raspberrypi.com/documentation)使用 [Creative Commons Attribution-ShareAlike 4.0 International](http://creativecommons.org/licenses/by-sa/4.0/)（CC BY-SA 4.0，署名-相同方式共享 4.0 国际）授权。非常抱歉，根据协议要求，本项目也只能使用 [Creative Commons Attribution-ShareAlike 4.0 International](http://creativecommons.org/licenses/by-sa/4.0/)（CC BY-SA 4.0，署名-相同方式共享 4.0 国际）及兼容的协议（兼容协议要求与该协议基本相同）进行授权。该协议要求您：

* 您必须给出适当的署名 ，提供指向本许可协议的链接，同时标明是否（对原始作品）作了修改。树莓派官方英文文档项目位于 <https://github.com/raspberrypi/documentation>。**我们特别授予所有人免于对本项目进行署名及链接的权利。但是您仍然需要遵守[树莓派文档项目](https://github.com/raspberrypi/documentation)本身的许可协议。**
* 相同方式共享 — 如果您再混合、转换或者基于本作品进行创作，您必须基于与原先许可协议相同的许可协议分发您贡献的作品。

>Raspberry Pi documentation is copyright © 2012-2024 Raspberry Pi Ltd and is licensed under a Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA) licence.
>
>Some content originates from the eLinux wiki, and is licensed under a Creative Commons Attribution-ShareAlike 3.0 Unported licence.
>
>The terms HDMI, HDMI High-Definition Multimedia Interface, HDMI trade dress and the HDMI Logos are trademarks or registered trademarks of HDMI Licensing Administrator, Inc
