# 处理器


## BCM2835

BCM2835 是在树莓派 1 型号 A、A+、B、B+、树莓派 Zero、树莓派 Zero W 和树莓派计算模块 1 中使用的博通（Broadcom）芯片。可以在外围规格文档中找到芯片的一些详细信息。它含有一个单核 ARM1176JZF-S 处理器。

>**注意**
>
>外围规格文档中有一些错误。但是有个当前已知勘误表。 
可以在以下文档中找到处理器的其他信息;

* GPU 文档和开源驱动程序
* [ARM1176JZF-S](https://developer.arm.com/documentation/ddi0301)

## BCM2836

这是树莓派 2 Model B 中使用的博通芯片。BCM2836 中的底层架构与 BCM2835 相同。唯一显著的区别是删除了 ARM1176JZF-S 处理器，并用四核 Cortex-A7 簇进行替换。

你应该参考：

* [BCM2836 ARM 本地外围设备](https://datasheets.raspberrypi.com/bcm2836/bcm2836-peripherals.pdf)
* [Cortex-A7 MPcore 处理器参考手册](http://infocenter.arm.com/help/index.jsp?topic=/com.arm.doc.ddi0464f/index.html)

## BCM2837

这是树莓派 3 Model B、树莓派 2 Model B 的后续型号以及树莓派计算模块 3 中使用的博通芯片。BCM2837 的底层架构与 BCM2836 相同。唯一显著的区别是用四核 ARM Cortex A53（ARMv8）簇替换了 ARMv7 四核簇。

ARM 核心运行在 1.2GHz，使设备比树莓派 2 快约 50%。VideoCore IV 运行在 400MHz。

请参考以下 BCM2836 文档，了解 ARM 外围设备规格的详细信息，该规格也适用于 BCM2837。

* [BCM2836 ARM 本地外围设备](https://datasheets.raspberrypi.com/bcm2836/bcm2836-peripherals.pdf)
* [Cortex-A53 MPCore 处理器技术参考手册](https://developer.arm.com/documentation/ddi0500/latest/)

## BCM2837B0

这是用于树莓派 3 Model A+、B+ 和树莓派计算模块 3+ 的博通芯片。BCM2837B0 的底层架构与其他版本的树莓派中使用的 BCM2837 芯片相同。ARM 核心硬件相同，只是频率更高。

ARM 核心可运行高达 1.4GHz，使 3B+/3A+ 比老的树莓派 3 快约 17%。VideoCore IV 运行在 400MHz。ARM 核心是 64 位的，而 VideoCore IV 是 32 位的。

BCM2837B0 芯片的封装略有不同于 BCM2837，并且最显著的是包括了散热片以获得更好的热管理。这使得更高的时钟频率成为可能，并且更准确地监控和控制芯片的温度。

树莓派博客上的这篇文章详细介绍了 BCM2837B0 芯片。

## BCM2711

这是在树莓派 4 Model B、树莓派 400 和树莓派计算模块 4 中使用的博通芯片。BCM2711 的架构是对旧版树莓派模型中 SoC 使用的架构的显著升级。它延续了 BCM2837 的四核 CPU 设计，但使用了更强大的 ARM A72 核心。它具有大大改进的 GPU 功能集，由于 USB 2 和 USB 3 使用了 PCIe 通道，并且具有本地连接的以太网控制器，因此输入/输出速度更快。它能够使用的内存也比以前采用的 SoC 更大。

ARM 核心可运行高达 1.5 GHz，使树莓派 4 比树莓派 3B+ 快约 50%。新的 VideoCore VI 3D 单元现在最高运行速度为 500 MHz。ARM 核心为 64 位，而 VideoCore 为 32 位，但有一个新的内存管理单元，这意味着它的可用内存比以前的 SoC 更大。

BCM2711 芯片继续使用自 BCM2837B0 开始的散热技术，可提供更好的热管理。

处理器：四核 Cortex-A72（ARM v8）64 位 SoC @ 1.5 GHz。

内存：根据型号可使用最高 8GB LPDDR4-2400 SDRAM

缓存：每个核心有 32kB 数据 + 48kB 指令 L1 缓存。1MB L2 缓存。

多媒体：H.265（4Kp60 解码）；H.264（1080p60 解码，1080p30 编码）；OpenGL ES，3.0 图形

I/O：PCIe 总线，板载以太网，2×DSI （在树莓派 4B 上仅暴露一个），2×CSI（在树莓派 4B 上仅暴露一个），最多 6×I2C，最多 6×UART（与 I2C 复用），最多 6×SPI（在树莓派 4B 上仅有五个暴露），双 HDMI 视频输出，复合视频输出。

BCM2711 的数据表包含更多细节。

## BCM2712

博通 BCM2712 是树莓派 5 核心的 16 纳米应用处理器。它是树莓派 4 中使用的 BCM2711 设备的后继产品，并与 BCM27xx 系列中其他设备共享许多常见的架构特性，这些设备曾用于旧版树莓派产品。

以四核 Arm Cortex-A76 CPU 簇为核心，主频高达 2.4GHz，每个核心具有 512KB 的 L2 缓存和 2MB 的共享 L3 缓存，集成了改进的 12 核 VideoCore VII GPU；硬件视频缩放器和 HDMI 控制器可驱动双 4kp60 显示器；还集成了由树莓派开发的 HEVC 解码器和图像信号处理器。32 位 LPDDR4X 内存接口提供了高达 17GB/s 的内存带宽，而 x1 和 x4 PCI Express 接口支持高带宽外部外设；在树莓派 5 上，后者用于连接树莓派 RP1 南桥（提供了主板上大部分外部 I/O 功能）。

重要功能包括:

* 四核 Arm Cortex-A76 @ 2.4GHz
  * ARMv8-A ISA
  * 64K 字节 I 和 D 缓存
  * 每个核心 512KB L2 缓存，2MB 共享 L3 缓存
* 新的树莓派开发的 ISP
  * 1 千兆像素/秒
* 改进的 HVS 和显示管线
  * 双 4Kp60 支持
* VideoCore V3D VII
  * ~2-2.5× 速度（更多硬件，Pi 4 上的 1GHz 对比 600MHz）
  * OpenGL ES 3.1，Vulkan 1.3
* 4Kp60 HEVC 硬件解码
  * 其他 CODEC 在软件中运行
  * H264 1080p24 解码约占 CPU 的 10-20%
  * H264 1080p60 解码约占 CPU 的 50-60%
  * H264 1080p30 编码（来自 ISP）~30-40％的 CPU

总体而言，BCM2712 中的新功能为常见的 CPU 或 I/O 密集型用例显示了相比树莓派 4 有 2-3 倍的性能提升。

## RP3A0

我们首次采用系统级封装（SiP）的是树莓派 RP3A0，它包含了博通 BCM2710A1 — 这是封装在博通 BCM2837 芯片内部的硅芯片，该芯片用于树莓派 3 — 以及 512MB 的 DRAM。

它被树莓派 Zero 2 W 使用。

![RP3A0 crosssection](https://www.raspberrypi.com/documentation/computers/images/RP3A0-crosssection.png)

RP3A0 是一款四核 64 位 Arm Cortex A53 CPU，主频为 1 GHz，但是如果安装了散热片或使用其他冷却解决方案，该芯片的潜在超频频率可达 1.2 GHz。

请参考 BCM2836 文档，了解 ARM 外围设备规格的详细信息，该规格也适用于 BCM2837 和 RP3A0。

* [BCM2836 ARM 本地外围设备](https://datasheets.raspberrypi.com/bcm2836/bcm2836-peripherals.pdf)
* [Cortex-A53 MPCore 处理器技术参考手册](https://developer.arm.com/documentation/ddi0500/latest/)

>**注意**
>
>旧版树莓派 Zero 使用堆叠封装（PoP）DRAM，其中 DRAM 直接焊接在 BCM2835 芯片顶层。 
