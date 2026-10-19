# 处理器


## BCM2835

BCM2835 是用于树莓派 1 的 A、A+、B、B+ 型号，以及树莓派 Zero、树莓派 Zero W 和树莓派计算模块 1 的博通芯片。芯片的一些详细信息可在[外设规格文档](https://pip.raspberrypi.com/documents/RP-008249-DS)中找到。它内置一颗单核 ARM1176JZF-S 处理器。

>**注意**
>
> 外设规格文档中有一些错误，不过目前有一份[已知勘误表](https://elinux.org/BCM2835_datasheet_errata)。

有关处理器的其他信息可在以下文档中找到：

* [GPU 文档](https://docs.broadcom.com/docs/12358545)和[开源驱动程序](https://docs.broadcom.com/docs/12358546)
* [ARM1176JZF-S](https://support.arm.com/documentation/ddi0301)

## BCM2836

这是早期树莓派 2B 型号中使用的博通芯片。BCM2836 的底层架构与 BCM2835 相同，唯一的显著区别是用四核 Cortex-A7 簇替换了 ARM1176JZF-S 处理器。

你应该参考：

* [BCM2836 Arm 本地外设](https://pip.raspberrypi.com/documents/RP-008250-DS)
* [Cortex-A7 MPCore 处理器参考手册](https://support.arm.com/documentation/ddi0464/f/)

>**重要**
>
> 该 SoC 已停产。后期版本的树莓派 2B 使用不同的 SoC。更多信息请参见[树莓派 2B 产品变更通知](https://pip.raspberrypi.com/documents/RP-004577-PC)。

## BCM2837

这是早期树莓派 3B 型号、部分树莓派 2B 型号以及树莓派计算模块 3 中使用的博通芯片。BCM2837 的底层架构与 BCM2836 相同，唯一的显著区别是用四核 Arm Cortex A53（Armv8）簇替换了四核 Armv7 簇。

Arm 核心运行在 1.2 GHz，使该设备比树莓派 2 快约 50%。VideoCore IV 运行在 400 MHz。

关于同样适用于 BCM2837 的 Arm 外设规格的详细信息，请参考以下 BCM2836 文档：

* [BCM2836 Arm 本地外设](https://pip.raspberrypi.com/documents/RP-008250-DS)
* [Cortex-A53 MPCore 处理器技术参考手册](https://support.arm.com/documentation/ddi0500/latest/)

>**重要**
>
> 该 SoC 已停产。包含该芯片的树莓派设备要么生命周期已经结束（EOL），要么使用不同的 SoC。更多信息请参见[树莓派 3B 产品变更通知](https://pip.raspberrypi.com/documents/RP-001029-PC)、[树莓派 2B 1.1 和 1.2 版停产通知 1](https://pip.raspberrypi.com/documents/RP-009284-PC)以及[树莓派计算模块 3 和计算模块 3 Lite 停产通知 2](https://pip.raspberrypi.com/documents/RP-009286-PC)。

## BCM2837B0

这是后期树莓派 2B 型号、后期树莓派 3B 型号、树莓派 3A+ 和 3B+ 以及树莓派计算模块 3+ 中使用的博通芯片。BCM2837B0 的底层架构与用于其他版本树莓派的 BCM2837 芯片相同。Arm 核心硬件相同，只是额定频率更高。

Arm 核心最高可运行在 1.4 GHz，使 3B+ 和 3A+ 比初代树莓派 3 快约 17%。VideoCore IV 运行在 400 MHz。Arm 核心为 64 位，而 VideoCore IV 为 32 位。

BCM2837B0 芯片的封装与 BCM2837 略有不同，最显著的是配备了金属散热片，以实现更好的散热。这使得更高的时钟频率成为可能，也能更准确地监控和控制芯片温度。

树莓派博客上的[这篇文章](https://www.raspberrypi.com/news/raspberry-pi-3-model-bplus-sale-now-35/)详细介绍了 BCM2837B0 芯片。

## BCM2711

这是树莓派 4B、树莓派计算模块 4 和树莓派 400 中使用的博通芯片。BCM2711 的架构相比早期树莓派机型所用 SoC 的架构有大幅升级。它延续了 BCM2837 的四核 CPU 设计，但采用更强大的 Arm A72 核心。它拥有大幅改进的 GPU 功能集，输入/输出速度也快得多：这得益于一条连接 USB 2.0 和 USB 3.0 端口的 PCIe 链路，以及原生集成的以太网控制器。它可寻址的内存也比此前使用的 SoC 更多。

Arm 核心最高可运行在 1.5 GHz，使树莓派 4B 比树莓派 3B+ 快约 50%。新的 VideoCore VI 3D 单元最高运行频率为 500 MHz。Arm 核心为 64 位；VideoCore 虽然是 32 位，但配备了新的内存管理单元，因此可访问的内存比之前的版本更多。

BCM2711 芯片沿用 BCM2837B0 开始采用的散热技术，提供了更好的散热管理。

处理器：四核 [Cortex-A72](https://en.wikipedia.org/wiki/ARM_Cortex-A72)（Armv8-A）64 位 SoC @ 1.5 GHz。

内存：最高可访问 8 GB LPDDR4-2400 SDRAM（视型号而定）。

缓存：每个核心有 32 kB 数据缓存 + 48 kB 指令 L1 缓存。1 MB L2 缓存。

多媒体：H.265（4Kp60 解码）；H.264（1080p60 解码，1080p30 编码）；OpenGL ES 3.0 图形。

I/O：PCIe 总线，板载以太网端口，2 × DSI 端口（树莓派 4B 仅引出一个），2 × CSI 端口（树莓派 4B 仅引出一个），最多 6 个 I²C，最多 6 个 UART（与 I²C 复用），最多 6 个 SPI（树莓派 4B 仅引出五个），双 HDMI 视频输出，复合视频输出。

[BCM2711 的数据表](https://pip.raspberrypi.com/documents/RP-008248-DS)包含更多细节。

## BCM2712

博通 BCM2712 是用于树莓派 5、500、500+ 和计算模块 5 的 16 纳米应用处理器。它是树莓派 4 所用 BCM2711 的后继产品，并与早期树莓派产品所用 BCM27xx 系列的其他设备共享许多架构特性。

它以四核 Arm Cortex-A76 CPU 簇为核心，主频最高可达 2.4 GHz，每个核心配有 512 kB L2 缓存，并带有 2 MB 共享 L3 缓存；集成了改进的 12 核 VideoCore VII GPU；硬件视频缩放器和 HDMI 控制器可驱动双 4Kp60 显示器；还集成了由树莓派开发的 HEVC 解码器和图像信号处理器。32 位 LPDDR4X 内存接口提供高达 17 GB/s 的内存带宽，而 ×1 和 ×4 PCI Express 接口支持高带宽外部设备；在树莓派 5 上，后者用于连接树莓派 RP1 南桥，该南桥提供了平台上大部分对外 I/O 功能。

主要功能包括：

* 四核 Arm Cortex-A76 @ 2.4 GHz
  * Armv8-A ISA
  * 64 kB 指令缓存和数据缓存
  * 每个核心 512 kB L2 缓存，2 MB 共享 L3 缓存
* 树莓派新开发的 ISP
  * 1 gigapixel/s
* 改进的 HVS 和显示管线
  * 双 4Kp60 支持
* VideoCore V3D VII
  * 速度约为树莓派 4 的 2–2.5 倍（硬件更多，960 MHz 对比 500 MHz）
  * OpenGL ES 3.1，Vulkan 1.3
* 4Kp60 HEVC 硬件解码
  * 其他编解码器由软件处理
  * H264 1080p24 解码约占 CPU 的 10–20%
  * H264 1080p60 解码约占 CPU 的 50–60%
  * H264 1080p30 编码（来自 ISP）约占 CPU 的 30–40%

总体而言，对于常见的 CPU 或 I/O 密集型用例，BCM2712 的新功能相较树莓派 4 可带来 2–3 倍的性能提升。

### 漏洞与缓解措施

BCM2712 SoC 中使用的 Cortex-A76 CPU 存在已知漏洞，这些漏洞在树莓派系统中都得到了缓解。

要查看漏洞及缓解措施的完整列表，可运行以下命令，它会列出当前生效的所有缓解措施。

```bash
$ lscpu | grep Vulnerability | grep -v "Not affected"
Vulnerability Spec store bypass:      Mitigation; Speculative Store Bypass disabled via prctl
Vulnerability Spectre v1:             Mitigation; __user pointer sanitization
Vulnerability Spectre v2:             Mitigation; CSV2, BHB
```

>**警告**
>
> 上述列表在 2025 年 4 月时是正确的，但可能已经过时。请在你的树莓派上运行 `lscpu` 获取最新信息。使用第三方操作系统时这一点尤为重要，因为它们的 Linux 内核构建中可能不包含所有最新的缓解措施。Raspberry Pi Ltd 使用的 Arm 处理器不使用微码，因此所有缓解措施都在内核层面完成。

`lscpu` 报告的漏洞信息基于当前运行内核的检测方案，可能无法准确反映硬件的真实漏洞状态，尤其是在操作系统缺少最新内核更新的情况下。如需了解 CPU 厂商安全公告中的更多漏洞信息，可参考 `lscpu` 报告的供应商 ID 和型号名称，从 [Arm 支持](https://support.arm.com/documentation/#cf-navigationhierarchiesproducts=Arm%20Security%20Center,CPU%20Product%20Security)获取。

## RP3A0

树莓派 RP3A0 是我们首款系统级封装（SiP）产品，由博通 BCM2710A1 和 512 MB DRAM 组成。BCM2710A1 是封装在博通 [BCM2837](#bcm2837) 芯片内部的硅裸片，该芯片用于[树莓派 3](jing-dian-dan-ban-ji-suan-ji.md)。

它用于[树莓派 Zero 2 W](ling-dian-xing-hao.md)。

![RP3A0 剖面图](https://www.raspberrypi.com/documentation/computers/images/RP3A0-crosssection.png)

RP3A0 是四核 64 位 Arm Cortex A53 CPU，主频为 1 GHz；不过，如果加装散热片或采用其他散热方案，该芯片最高可超频至 1.2 GHz。

关于同样适用于 BCM2837 和 RP3A0 的 Arm 外设规格的详细信息，请参考以下 BCM2836 文档。

* [BCM2836 Arm 本地外设](https://pip.raspberrypi.com/documents/RP-008250-DS)
* [Cortex-A53 MPCore 处理器技术参考手册](https://support.arm.com/documentation/ddi0500/latest/)

>**注意**
>
> [初代树莓派 Zero](ling-dian-xing-hao.md) 使用堆叠封装（PoP）DRAM，其中 DRAM 直接焊接在 [BCM2835](#bcm2835) 芯片上方。
