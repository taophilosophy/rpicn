# 计算模块硬件

树莓派**计算模块（Compute Module，CM）**是标准树莓派单板计算机（SBC）的紧凑版本，主要面向嵌入式和工业应用。计算模块包含树莓派的核心组件，但不带 HDMI、USB 或以太网等标准连接器。

树莓派**计算模块 IO 板（Compute Module IO Board，CMIO）**提供访问和扩展计算模块功能所需的物理连接器、外设接口与扩展选项。计算模块 IO 板既可作为独立产品使用，用于快速原型开发和嵌入式系统开发，也可作为自研载板（IO 板）的参考设计。无论哪种用法，你都可以只选用应用所需的连接器。

本页内容：

* 概述可用的树莓派计算模块与 IO 板型号，包括其兼容性与主要特性。
* 介绍计算模块 5（CM5）及其 IO 板（CM5IO）可用的配件。
* 说明如何刷写和启动树莓派计算模块。
* 说明如何配置计算模块的 EEPROM 引导加载程序。
* 说明如何使用设备树和叠加层连接并启用摄像头、显示屏等外设。
* 提供数据表、原理图和设计资源的链接。

树莓派计算模块是旗舰级树莓派单板计算机（SBC）的**系统级模块（system-on-module，SoM）**版本。它们面向工业和商业应用，如数字标牌、瘦客户机和流程自动化。许多开发者和系统设计者选择计算模块而非旗舰级树莓派型号，是因为其紧凑的设计、灵活性以及对板载 eMMC 存储的支持。

### 内存、存储与无线版本

树莓派计算模块有多种版本，区别在于内存、嵌入式多媒体卡（eMMC）闪存容量（焊接在板上）以及无线连接能力（Wi-Fi 和蓝牙）。

* **内存。** 计算模块 1、3 和 3+ 提供固定容量的内存。计算模块 4、4S 和 5 提供不同容量的内存；可用选项的详细信息，请参见本页各计算模块型号的专门章节。
* **存储。** 计算模块 3、3+、4、4S 和 5 提供不同的存储选项，较新的型号提供更多选项和更大容量。计算模块 1 提供固定的 4 GB 存储。存储由 eMMC 闪存提供，可持久保存数据，功耗低，并内置提升可靠性的功能。不带板载存储的版本以 *Lite* 或 *L* 为后缀，例如“CM5Lite”或“CM3L”。
* **无线。** 计算模块 4 和 5 提供可选的 Wi-Fi 和蓝牙。

### 型号

下表按时间倒序列出树莓派计算模块，便于快速查阅其 SoC、GPU、CPU 和外形规格。有关各型号（包括内存和存储选项）的更多信息，请参见本页后面的专门章节。

| 型号 | 基于 | SoC | GPU | CPU | 外形规格 |
| ---- | ---- | --- | --- | --- | -------- |
| **CM5**（2024） | 树莓派 5 | Broadcom [BCM2712](chu-li-qi.md) | VideoCore VII | 4 × Cortex-A76 @ 2.4 GHz | 双 100 针连接器 |
| **CM4S**（2022） | 树莓派 4 Model B（CM3 外形规格） | Broadcom [BCM2711](chu-li-qi.md) | VideoCore VI | 4 × Cortex-A72 @ 1.5 GHz | DDR2 SODIMM |
| **CM4**（2020） | 树莓派 4 Model B | Broadcom [BCM2711](chu-li-qi.md) | VideoCore VI | 4 × Cortex-A72 @ 1.5 GHz | 双 100 针连接器 |
| **CM3+**（2019） | 树莓派 3 Model B+ | Broadcom [BCM2837B0](chu-li-qi.md) | VideoCore IV | 4 × Cortex-A53 @ 1.2 GHz | DDR2 SODIMM |
| **CM3**（2017；2025 年 10 月停产） | 树莓派 3 Model B | Broadcom [BCM2837](chu-li-qi.md) | VideoCore IV | 4 × Cortex-A53 @ 1.2 GHz | DDR2 SODIMM |
| **CM1**（2014） | 树莓派 Model B | Broadcom [BCM2835](chu-li-qi.md) | VideoCore IV | 1 × ARM1176JZF-S @ 700 MHz | DDR2 SODIMM |

>**重要**
>
>采用 DDR2 SODIMM 物理外形规格的计算模块与 DDR2 SODIMM 的电气规范并不兼容。

### 计算模块 5

![计算模块 5](.gitbook/assets/cm5.png)

计算模块 5（CM5）融合了树莓派 5 的核心组件，并可选配闪存存储。主要特性包括：

* **处理器。** Broadcom BCM2712。
* **内存选项。** 2 GB、4 GB、8 GB 或 16 GB 内存。
* **存储选项。** 0 GB（*CM5Lite*）、16 GB、32 GB 或 64 GB 的 eMMC 闪存。
* **外形规格。** 两个 100 针高密度连接器，用于连接配套载板。

CM5 与 *CM4* 采用相同的外形规格，并提供标准树莓派板卡之外的输入/输出（I/O）接口，为更复杂的系统与设计提供更多选择。

### 计算模块 4S

![计算模块 4S](.gitbook/assets/cm4s.jpg)

计算模块 4S（CM4S）融合了树莓派 4 的核心组件，并可选配闪存存储。主要特性包括：

* **处理器。** Broadcom BCM2711。
* **内存选项。** 1 GB、2 GB、4 GB 或 8 GB 内存。
* **存储选项。** 0 GB（*CM4SLite*）、8 GB、16 GB、32 GB 或 64 GB 的 eMMC 闪存。
* **连接选项。** 双频（2.4 GHz 或 5 GHz）802.11ac Wi-Fi（300 Mb/s）和蓝牙（5 和 BLE）。
* **外形规格。** 标准 DDR2 SODIMM 模块。

与 *CM4* 不同，CM4S 保留了 *CM1*、*CM3* 和 *CM3+* 所用的 DDR2 SODIMM 外形规格。

### 计算模块 4

![计算模块 4](.gitbook/assets/cm4.jpg)

计算模块 4（CM4）融合了树莓派 4 的核心组件，并可选配闪存存储。主要特性包括：

* **处理器。** Broadcom BCM2711。
* **内存选项。** 1 GB、2 GB、4 GB 或 8 GB 内存。
* **存储选项。** 0 GB（*CM4Lite*）、8 GB、16 GB、32 GB 或 64 GB 的 eMMC 闪存。
* **连接选项。** 双频（2.4 GHz 或 5 GHz）802.11ac Wi-Fi（300 Mb/s）和蓝牙（5 和 BLE）。
* **外形规格。** 两个 100 针高密度连接器，用于连接配套载板。
* **温度范围选项。** 标准版本的工作温度为 -20°C 至 +85°C，宽温版本为 -40°C 至 +85°C。

与早期模块（*CM1*、*CM3*、*CM3+*）不同，CM4 舍弃了 DDR2 SODIMM 外形规格，改用双 100 针高密度连接器布局，物理尺寸更小。这一重新设计支持以下新增特性：

* 双 HDMI 连接器
* PCIe
* 以太网连接器

### 计算模块 3+

![计算模块 3+](.gitbook/assets/cm3-plus.jpg)

计算模块 3+（CM3+）融合了树莓派 3 Model B+ 的核心组件，并可选配闪存存储。主要特性包括：

* **处理器。** Broadcom BCM2837B0。
* **内存。** 1 GB 内存。
* **存储选项。** 0 GB（*CM3+Lite*）或 8 GB、16 GB、32 GB、64 GB 的 eMMC 闪存。
* **外形规格。** 标准 DDR2 SODIMM 模块。

### 计算模块 3

![计算模块 3](.gitbook/assets/compute-module-cm3.jpg)

>**重要**
>
>由于核心 SoC 停产，树莓派计算模块 3（CM3）和计算模块 3 Lite（CM3Lite）已进入生命周期终止（End-of-Life，EoL）状态。官方 EoL 日期为 2025 年 10 月 16 日。与 CM3 最接近的替代品是计算模块 3+（CM3+），它具有相同的机械尺寸、改进的散热设计和 BCM2837B0 处理器，因此推荐用于既有设计。对于需要 SODIMM 外形规格的新设计，我们推荐计算模块 4S（CM4S）；对于其他所有新设计，我们推荐计算模块 4（CM4）或计算模块 5（CM5）。更多信息，请参阅官方[停产通知](https://pip.raspberrypi.com/documents/RP-009286-PC)。

计算模块 3（CM3）融合了树莓派 3 的核心组件，并可选配 4 GB 闪存。主要特性包括：

* **处理器。** Broadcom BCM2837。
* **内存。** 1 GB 内存。
* **存储选项。** 0 GB（*CM3Lite*）或 4 GB 的 eMMC 闪存。
* **外形规格。** 标准 DDR2 SODIMM 模块。

### 计算模块 1

![计算模块 1](.gitbook/assets/cm1.jpg)

计算模块 1（CM1）融合了树莓派 Model B 的核心组件，并配备 4 GB 闪存。主要特性包括：

* **处理器。** Broadcom BCM2835。
* **内存。** 512 MB 内存。
* **存储。** 4 GB 的 eMMC 闪存。
* **外形规格。** 标准 DDR2 SODIMM 模块。

## IO 板

树莓派计算模块 IO 板是配套载板，提供连接计算模块各类输入/输出（I/O）外设所需的连接器。树莓派计算模块 IO 板提供以下功能：

* 为计算模块供电。
* 将通用输入/输出（GPIO）引脚连接到标准排针，以便连接传感器或电子元件。
* 通过柔性扁平电缆（FFC）连接器提供摄像头和显示屏接口。
* 通过 HDMI 连接器提供 HDMI 信号。
* 通过标准 USB 连接器提供 USB 接口，用于连接外设。
* 提供指示电源和活动状态的 LED。
* 支持通过 USB 对模块的板载存储进行 eMMC 编程（刷写）。
* 在 CM4IO 和 CM5IO 上，通过连接器引出 PCIe，以便连接 SSD、网卡等存储设备或外设。

树莓派 IO 板是通用板卡，用于计算模块的开发、测试和原型设计。在生产环境中，你可以设计一块更小的定制载板，只包含你的用例所需的连接器。

### IO 板与兼容性

并非所有 IO 板都适用于所有计算模块型号。下表按时间倒序列出树莓派计算模块 IO 板，包括其兼容的计算模块（含 Lite 版本）、电源输入和尺寸。有关各板卡（包括可用接口）的更多信息，请参见本页后面的专门章节。

| IO 板 | 兼容的计算模块 | 电源输入 | 尺寸 |
| ----- | -------------- | -------- | ---- |
| **计算模块 5 IO 板（CM5IO）**（2024） | CM5；CM4（功能受限） | 通过 USB Type-C 输入 5 V | 160 mm × 90 mm |
| **计算模块 4 IO 板（CM4IO）**（2020） | CM4；CM5（功能受限） | 通过 GPIO 排针输入 5 V，或通过 DC 桶形插座输入 12 V | 160 mm × 90 mm |
| **计算模块 IO 板版本 3（CMIO3）**（2017） | CM1、CM3、CM3+ 和 CM4S | 通过 GPIO 或 micro USB 连接器输入 5 V | 85 mm × 105 mm |
| **计算模块 IO 板版本 1（CMIO；CMIO1）**（2014） | CM1 | 通过 GPIO 或 micro USB 连接器输入 5 V | 85 mm × 105 mm |

### 计算模块 5 IO 板

![计算模块 5 IO 板](.gitbook/assets/cm5io.png)

计算模块 5 IO 板（CM5IO）提供以下功能：

* **电源和控制连接器。**
  * 与树莓派 5 相同标准的 USB-C 供电：5 V/5 A（25 W），或 5 V/3 A（15 W）且外设限流 600 mA。
  * CM5 的电源按钮。
  * 实时时钟（RTC）电池插座。
* **视频和显示连接器。**
  * 两个 HDMI 连接器。
  * 两个 MIPI DSI/CSI-2 复合显示/摄像头 FPC 连接器（22 针、0.5 mm 间距电缆）。
* **网络与连接连接器。**
  * 两个 USB 3.0（Type-A）连接器，用于键盘、存储或外设。
  * 一个 USB 2.0（Type-C）连接器，用于刷写 CM5 或连接其他外设。
  * 一个支持 PoE 的千兆以太网 RJ45 连接器。
* **扩展和存储选项。**
  * 一个 M.2 M key PCIe 插槽，兼容 2230、2242、2260 和 2280 外形规格。
  * 一个 microSD 卡槽（仅用于不带 eMMC 的 *CM5Lite*；其他版本会忽略该卡槽）。
  * 带 40 针 GPIO 连接器的扩展板安装位。
  * PoE 排针。
* **配置选项。**
  * 用于禁用 eMMC 启动、EEPROM 写入和无线连接等功能的跳线。
  * 可选 1.8 V 或 3.3 V GPIO 电压。
* **风扇连接器。** 一个四针 JST-SH PWM 风扇连接器。

### 计算模块 4 IO 板

![计算模块 4 IO 板](.gitbook/assets/cm4io.jpg)

计算模块 4 IO 板（CM4IO）提供以下功能：

* **电源和控制连接器。**
  * 通过 GPIO 排针输入 5 V，或通过桶形插座输入 12 V；如未使用 PCIe，最高支持 26 V。
  * 实时时钟（RTC）电池插座。
* **视频和显示连接器。**
  * 两个 HDMI 连接器。
  * 两个 MIPI DSI 显示 FPC 连接器（22 针、0.5 mm 间距电缆）。
  * 两个 MIPI CSI-2 摄像头 FPC 连接器（22 针、0.5 mm 间距电缆）。
* **网络与连接连接器。**
  * 两个 USB 2.0 连接器。
  * 一个 micro USB 上行端口。
  * 一个支持 PoE 的千兆以太网 RJ45 连接器。
* **扩展和存储选项。**
  * PCIe Gen 2 插槽。
  * 一个 microSD 卡槽（仅用于不带 eMMC 的 *CM4Lite*；其他版本会忽略该卡槽）。
  * 带 40 针 GPIO 连接器的扩展板安装位。
  * PoE 排针。
* **配置选项。**
  * 用于禁用 eMMC 启动、EEPROM 写入和无线连接等功能的跳线。
  * 可选 1.8 V 或 3.3 V GPIO 电压。
* **风扇连接器。** 支持标准 12 V PWM 风扇的风扇连接器。

### 计算模块 IO 板（版本 1 和 3）

![计算模块 IO 板（版本 3）](.gitbook/assets/cmio.jpg)

计算模块 IO 板有两个版本：

* 版本 1（CMIO），仅兼容 CM1。
* 版本 3（CMIO3），兼容 CM1、CM3、CM3+ 和 CM4S。该版本增加了 CMIO（版本 1）所没有的 microSD 卡槽。

计算模块 IO 板（CMIO 和 CMIO3）提供以下功能：

* **电源和控制连接器。** 通过 GPIO 或 micro USB 连接器输入 5 V。
* **视频和显示连接器。**
  * 一个全尺寸 Type-A HDMI 连接器。
  * 两个 MIPI DSI 显示 FPC 连接器（22 针、0.5 mm 间距电缆）。
  * 两个 MIPI CSI-2 摄像头 FPC 连接器（22 针、0.5 mm 间距电缆）。
* **网络和连接连接器。** 一个 USB 2.0 Type-A 连接器。
* **扩展和存储选项。**
  * 46 个 GPIO 引脚。
  * （仅 CMIO3）一个 microSD 卡槽（仅用于不带 eMMC 的 *CM3Lite*、*CM3+Lite* 和 *CM4SLite*）。

## CM5 与 CM5IO 配件

树莓派为 CM5 和 CM5IO 提供以下配件：

* [CM5IO 机箱](#cm5io-机箱)，用于 CM5IO（及连接的 CM5）的外壳。机箱还可以选装天线和散热器。
* [天线（CM4 和 CM5）](#天线cm4-和-cm5)，用于通过 CM4 或 CM5 进行无线连接的 2.4 GHz 和 5 GHz 天线。
* [CM5 散热器](#cm5-散热器)，用于散发 CM5 热量的无源散热片。
* [智能显示模块](../pei-jian/zhi-neng-xian-shi-mo-kuai.md)，用于在支持 Intel® 智能显示模块（Intel® SDM）规范的显示系统中使用 CM5 的转接板。

### CM5IO 机箱

![计算模块 5 IO 板机箱（版本 2）](.gitbook/assets/cm5io-case-v2.jpg)

计算模块 5 IO 板（CM5IO）机箱是一个两件式金属外壳，组装后可为装有 CM5 的 CM5IO 提供物理保护。

以下特性适用于最新版 CM5IO 机箱（版本 2）：

* 为朝外的连接器和 LED 预留的开口。
* 预装的可控风扇，可以拆卸。
* 树莓派天线套件的安装点。
* 预装风扇旁边可容纳 CM5 散热器的空间。
* 可容纳连接到 IO 板的配件，如 M.2 SSD 或 PoE+ HAT+。

机箱的原始版本无法同时容纳上述所有项目。有关不同版本的更多信息，请参见[机箱版本](#机箱版本)。

#### 机箱规格

![CM5IO 机箱端口](.gitbook/assets/cm5io-case-front.png)

组装后，CM5IO 机箱的尺寸约为 170 mm × 94 mm × 28 mm。它由金属板制成，重约 350 g。

在散热方面，机箱配有预装风扇，可将气流导向 CM5 和 CM5IO 的组件。你可以根据散热需求拆卸或更换风扇。视机箱版本不同，你还可以选装 CM5 散热器以改善散热性能；原始版本需要先拆下风扇，而更新版本可同时容纳风扇和散热器。

下图展示了 CM5IO 机箱的物理尺寸（单位：毫米）。两个版本的机箱尺寸相同，唯一区别是风扇的位置。有关不同版本的信息，请参见[机箱版本](#机箱版本)。

![CM5IO 机箱（版本 2）物理规格](.gitbook/assets/case-physical.png)

#### 机箱版本

CM5IO 机箱有两个版本，区别在于预装风扇的位置：版本 1 和版本 2。

![左：CM5IO 机箱版本 1；右：CM5IO 机箱版本 2](.gitbook/assets/case-versions.jpg)

版本 1 的风扇更靠近外壳的长边。该版本的内部布局和可用间隙不允许同时将风扇和 CM5 散热器安装在机箱内。如果要将 CM5 散热器装进机箱，必须先拆下风扇。

版本 2 更新了内部布局，风扇更靠近外壳的短边。改进后的布局无需改动即可同时容纳风扇和 CM5 散热器。

有关将 CM5 散热器安装到 CM5 上（之后可以装到 IO 板上并装入 CM5IO 机箱）的说明，请参见[安装 CM5 散热器](#安装-cm5-散热器)。

#### 机箱组装

以下步骤介绍如何组装最新版 CM5IO 机箱（版本 2）。版本 1 在不作改动的情况下无法同时容纳风扇和 CM5 散热器。如果你使用的是版本 1 机箱，可以拆下风扇（见第 4 步）或跳过下面说明中的第 6 步。有关不同版本的信息，请参见[机箱版本](#机箱版本)。

要将 CM5IO 装入机箱：

1. **将 CM5 装到 CM5IO 上。** 将 CM5 顺时针旋转 90 度，使 CM5 上的双 100 针连接器与 CM5IO 上的连接器对齐，然后轻轻但用力地按压连接。安装孔也应相互对齐。
2. **打开机箱。** 用十字螺丝刀拧下并取出四颗螺丝（机箱左侧两颗、右侧两颗），然后将机箱顶部与底部分离。请妥善保管螺丝。
3. **将 CM5IO 组件装入机箱。** 将 CM5IO（已装有 CM5）放入机箱底部，使其与板子四角附近的四个安装孔对齐。确保所有朝外的连接器都与机箱前部对应的开口对齐。然后用四颗 M2.5 螺丝将 CM5IO 组件固定到机箱底部的四个安装孔上。
4. **连接或拆下风扇。**
   * 如果使用预装风扇，请将风扇连接器插入 CM5IO 上标有 *FAN (J14)* 的四针风扇插座。
   * 如果要拆下风扇，请从机箱顶部内侧拧下风扇四角的螺丝。
5. **（可选）连接外置天线。** 如果要安装天线，请按照[连接天线](#通过-cm5io-机箱连接天线)中的说明操作。
6. **（可选）安装散热器。** 如果要安装散热器，请按照[安装 CM5 散热器](#安装-cm5-散热器)中的说明操作。如果同时还要连接天线，请先连接天线的 U.FL 连接器，以便操作。
7. **（可选）连接摄像头或显示屏。** 如果使用摄像头或显示屏，请将扁平电缆穿过机箱背面的其中一个槽口，并连接到 CM5IO 上的一个 *CAM/DISP* 端口。
8. **（可选）安装 M.2 SSD。** 如果要安装 M.2 SSD，请将其插入 CM5IO 右下角的 M.2 插槽，并用安装螺丝固定另一端。
9. **（可选）安装扩展板。** 如果要安装 HAT 扩展板，请将其与 40 针 GPIO 排针和安装柱对齐，使扩展板覆盖电池插槽，然后用力按压到位并用螺丝固定。
10. **合上机箱。** 将机箱顶部折回底部，对齐机箱左右两侧的螺丝孔以及背面的电源按钮。用十字螺丝刀将四颗螺丝拧回原位，注意不要拧得过紧。

>**注意**
>
>SD 卡槽是推入推出式卡槽。插入 SD 卡时，将卡的触点朝下推入卡槽；取出时，向卡槽内推一下将其释放，然后拔出。

### 天线（CM4 和 CM5）

树莓派天线套件提供经过认证的外置天线，用于增强 CM4 或 CM5 的无线接收能力。

![连接到 CM4 的天线](.gitbook/assets/cm4-cm5-antenna.jpg)

#### 天线规格

该天线支持双频 Wi-Fi，可连接到 CM4 或 CM5 上的 [U.FL 连接器](https://en.wikipedia.org/wiki/Hirose_U.FL)。天线完全展开时高约 108.5 mm，弯折 90 度时长约 87.5 mm；SMA 转 U.FL 电缆长约 205 mm。

![CM4 和 CM5 天线物理规格](.gitbook/assets/cm4-cm5-antenna-physical.png)

#### 通过 CM5IO 机箱连接天线

天线可以与 [CM5IO 机箱](#cm5io-机箱)配合使用。要通过 CM5IO 机箱将天线连接到计算模块，请先完成[机箱组装](#机箱组装)中的前四步，然后完成以下步骤：

1. **连接 U.FL 连接器。** 将天线电缆上的 U.FL 连接器连接到计算模块上兼容 U.FL 的连接器（位于 CM5 左上角安装孔旁边）。请在安装散热器（如果使用）之前完成此操作，因为散热器会使 U.FL 连接器的连接更困难。
2. **插入 SMA 连接器。** 取下 CM5IO 机箱内侧天线端口上的橡胶塞。然后从机箱内侧将 SMA 连接器（平面朝上）推入天线端口，使其穿出并可从外部接触。
3. **固定 SMA 连接器。** 将固定用的六角螺母和垫圈顺时针拧到 SMA 连接器上，直到牢固就位。拧紧时避免过度用力，以免损坏。
4. **将天线连接到 SMA 连接器。** 将 SMA 连接器插入天线端口，天线朝外，顺时针拧动天线以固定。
5. **调整天线。** 将天线转至最大 90 度角，调整到最终位置。

现在你可以完成[机箱组装](#机箱组装)中剩余的步骤，将 CM5IO 装入机箱。

![CM4 和 CM5 天线组装图](.gitbook/assets/cm4-cm5-antenna-assembly.svg)

要将天线与计算模块配合使用，请在 `/boot/firmware/config.txt` 中添加 `dtparam` 指令。在 `config.txt` 文件末尾添加以下行：`dtparam=ant2`

### CM5 散热器

CM5 散热器是无源散热片，帮助散发 CM5 的热量，从而改善 CPU 性能并延长使用寿命。

![CM5 散热器](.gitbook/assets/cm5-cooler.jpg)

#### 散热器规格

CM5 散热器的尺寸约为 41 mm × 56 mm × 12.7 mm。它是一款铝制散热片，底部带有导热硅胶垫。较新版本的 [CM5IO 机箱](#cm5io-机箱)允许同时将散热器和预装风扇装入机箱。如果你使用的是旧版 CM5IO 机箱，必须拆下风扇才能为散热器腾出空间。

![CM5 散热器物理规格](.gitbook/assets/cm5-cooler-physical.png)

#### 安装 CM5 散热器

要将散热器安装到 CM5 上：

1. 从散热器底部的硅胶垫上取下保护纸。
2. 将散热器底部的硅胶贴到 CM5 顶部。放置散热器时，使散热器上的开口位于板载天线（CM5 左侧的梯形区域）上方，并避开旁边的 [U.FL 连接器](https://en.wikipedia.org/wiki/Hirose_U.FL)（如果有）。
3. （可选）用螺丝拧入四角的安装点以固定散热器。如果省略螺丝，散热器与 CM5 之间的粘合会随时间的推移和使用而增强。

## 将镜像刷写到计算模块

>**技巧**
>
>要将同一镜像刷写到多个计算模块，请使用[树莓派安全启动配置器](https://github.com/raspberrypi/rpi-sb-provisioner)。要定制刷写到这些设备的操作系统镜像，请使用 [pi-gen](https://github.com/RPi-Distro/pi-gen)。

计算模块搭载了连接到主 SD 卡接口的内置 eMMC 设备。本指南介绍如何将操作系统镜像刷写到单个计算模块的 eMMC 存储器。

**Lite** 版本的计算模块不带板载 eMMC。请改为按照其他树莓派设备的存储设备刷写流程操作：[安装操作系统](ru-men.md#将操作系统安装到启动介质)。

### 准备工作

要刷写计算模块 eMMC，你需要以下物品：

* 另一台计算机，本指南中称为**主机设备**。你可以使用 Linux（推荐树莓派系统或 Ubuntu）、Windows 11 或 macOS。
* 与你的计算模块型号对应的[计算模块 IO 板](#io-板与兼容性)。
* 一根 micro USB 线；CM5IO 及之后的计算模块型号则需要 USB-C 线。

>**技巧**
>
>某些情况下，USB 集线器会导致主机设备无法识别计算模块。如果你的主机设备无法识别计算模块，请尝试将计算模块直接连接到主机设备。更多诊断建议，请参阅 [usbboot 故障排除指南](https://github.com/raspberrypi/usbboot/blob/master/docs/troubleshooting.md)。

### 设置 IO 板

首先，完成 IO 板的硬件设置，包括将计算模块和主机设备连接到 IO 板。

#### 使用计算模块 5 IO 板

设置计算模块 5 IO 板：

1. 将计算模块连接到 IO 板。连接后，计算模块应该平放。
2. 将 `nRPI_BOOT` 跳线帽装到 IO 板跳线 J2（`disable eMMC Boot`）上。
3. 将一根电缆从 IO 板上的 USB-C 从机端口 J11 连接到主机设备。

#### 使用计算模块 4 IO 板

设置计算模块 4 IO 板：

1. 将计算模块连接到 IO 板。连接后，计算模块应该平放。
2. 将 `nRPI_BOOT` 跳线帽装到 IO 板跳线 J2（`disable eMMC Boot`）上。
3. 将一根电缆从 IO 板上的 micro USB 从机端口 J11 连接到主机设备。

#### 使用计算模块 IO 板

要设置计算模块 IO 板：

1. 将计算模块连接到 IO 板。连接后，计算模块应平行于板放置，使接合夹牢固地卡入到位。
2. 将 J4（`USB SLAVE BOOT ENABLE`）设置为 `1-2`（`USB BOOT ENABLED`）。
3. 将一根电缆从 IO 板上的 micro USB 从机端口 J15 连接到主机设备。

### 配置主机设备

接下来，在主机设备上配置软件。

>**技巧**
>
>作为主机设备，我们推荐运行 64 位树莓派系统的树莓派 4 或更新机型。

#### 在 Linux 上配置软件

在 Linux 主机设备上配置软件：

1. 运行以下命令安装 `rpiboot`（也可以[从源代码编译 `rpiboot`](https://github.com/raspberrypi/usbboot)）：

    ```bash
    $ sudo apt install rpiboot
    ```
2. 将 IO 板接入电源。
3. 然后运行 `rpiboot`：

    ```bash
    $ sudo rpiboot
    ```
4. 几秒钟后，计算模块应该会显示成一个大容量存储设备。检查 `/dev/` 目录（通常是 `/dev/sda` 或 `/dev/sdb`）以找到该设备。或者，运行 `lsblk` 并搜索一个存储容量与你的计算模块容量相匹配的设备。

#### 在 macOS 上配置软件

在 macOS 主机设备上配置软件：

1. 首先，从源代码编译 `rpiboot`。
2. 将 IO 板连接到电源。
3. 然后，使用以下命令运行 `rpiboot` 可执行文件：

    ```bash
    $ rpiboot -d mass-storage-gadget64
    ```
4. 命令运行完成后，你应该会看到一条提示：“The disk you inserted was not readable by this computer.”（你插入的磁盘无法被此计算机读取。）点击 **Ignore**（忽略）。你的计算模块现在应该显示为一个大容量存储设备。

#### 在 Windows 上配置软件

在 Windows 11 主机设备上配置软件：

1. 从[发布页面](https://github.com/raspberrypi/usbboot/releases)下载最新的 Windows 安装程序，或[从源代码编译 `rpiboot`](https://github.com/raspberrypi/usbboot)。
2. 双击安装程序运行。这将安装驱动程序和引导工具。安装过程中出现的任何驱动程序安装窗口都不要关闭。
3. 重启计算机。
4. 将 IO 板接入电源。Windows 应能发现硬件并配置所需的驱动程序。
5. 从开始菜单选择 **rpiboot - Mass Storage Gadget**。几秒钟后，计算模块的 eMMC、NVMe 或 SD 卡会显示为 USB 大容量存储设备。这还会提供一个作为串口设备的调试控制台。

### 刷写 eMMC

你可以使用树莓派启动盘制作工具把操作系统镜像刷写到计算模块上。

还可使用 `dd` 将裸操作系统镜像（例如树莓派系统）写入你的计算模块。运行以下命令，请把 `/dev/sdX` 替换为你的计算模块所对应的大容量存储设备的路径，并把 `raw_os_image.img` 替换为你的原始操作系统镜像的路径：

```bash
$ sudo dd if=raw_os_image.img of=/dev/sdX bs=4MiB
```

镜像写入后，断开并重新连接计算模块。你现在会看到两个分区（用于树莓派系统）：

```bash
/dev/sdX    <- 设备
/dev/sdX1   <- 第一个分区（FAT）
/dev/sdX2   <- 第二个分区（Linux 文件系统）
```

你可以正常挂载分区 `/dev/sdX1` 和 `/dev/sdX2`。

### 从 eMMC 启动

#### 使用计算模块 5 IO 板

从 IO 板跳线 J2（`disable eMMC Boot`）上取下 `nRPI_BOOT`。

#### 使用计算模块 4 IO 板

从 IO 板跳线 J2（`disable eMMC Boot`）上取下 `nRPI_BOOT`。

#### 使用计算模块 IO 板

将 J4（`USB SLAVE BOOT ENABLE`）设置为 `2-3`（`USB BOOT DISABLED`）。

#### 启动

断开 USB 从机端口。将 IO 板断电再重新上电，从你刚刚写入 eMMC 的新镜像引导计算模块。

### 已知问题

* 小部分 CM3 设备可能出现启动问题。我们已将这些问题的原因追溯到创建 FAT32 分区的方法；我们认为问题是由 CPU 和 eMMC 之间的时序差异造成的。如果你在启动 CM3 时遇到问题，请使用以下命令手动创建分区：

  ```bash
  $ sudo parted /dev/<设备>
  (parted) mkpart primary fat32 4MiB 64MiB
  (parted) q
  $ sudo mkfs.vfat -F32 /dev/<设备>
  $ sudo cp -r <文件>/* <挂载点>
  ```
* CM1 引导加载程序会向主机返回一个略有错误的 USB 数据包。大多数 USB 主机会忽略它，但由于该问题，某些 USB 端口无法工作。CM3 修复了该错误。
* Ubuntu 24.04 及更早版本随附的 `rpiboot` 版本存在无法与设备通信的问题。要解决此问题，请[从源代码编译 `rpiboot`](https://github.com/raspberrypi/usbboot?tab=readme-ov-file#linux--cygwin--wsl)。

## 计算模块 EEPROM 引导加载程序

自计算模块 4 起，计算模块改用 EEPROM 引导加载程序。该引导加载程序位于板载存储的一小段空间中，而不是启动分区。因此，它的更新流程有所不同。在生产环境中使用带 EEPROM 引导加载程序的计算模块之前，请始终遵循以下最佳实践：

* 选定特定的引导加载程序版本，并验证你使用的每个计算模块都烧录了该版本。`usbboot` 存储库中的版本始终是较新的稳定版本。
* 通过设置 `BOOT_ORDER` 配置启动设备。
* 在引导加载程序 EEPROM 上启用硬件写保护，确保无法触及的产品（如远程或嵌入式设备）上的引导加载程序无法被修改。

### 刷写计算模块引导加载程序 EEPROM

要刷写引导加载程序 EEPROM：

1. 按刷写 eMMC 的方式设置硬件，但确保 `EEPROM_nWP` **未**被拉低。
2. 运行以下命令，将 `recovery/pieeprom.bin` 写入引导加载程序 EEPROM：

    ```bash
    $ ./rpiboot -d recovery
    ```

3. 完成后，可以再次将 `EEPROM_nWP` 拉低。

### 刷写存储卡之外的存储设备

基于 Linux 的 [`mass-storage-gadget`](https://github.com/raspberrypi/usbboot/blob/master/mass-storage-gadget64/README.md) 支持刷写 NVMe、eMMC 和 USB 块设备。`mass-storage-gadget` 写入设备的速度比基于固件的 `rpiboot` 机制更快，并且还会为设备提供 UART 控制台以便调试。

`usbboot` 还包含许多[扩展](https://github.com/raspberrypi/usbboot/tree/master#provisioning-extensions)，使你能够配置安全启动或启动自定义的 Linux initramfs 镜像。

### 更新计算模块引导加载程序

对于带 EEPROM 引导加载程序的计算模块，ROM 从不在 SD/eMMC 上运行 `recovery.bin`。这些计算模块默认禁用 `rpi-eeprom-update` 服务，因为 eMMC 不可拆卸，无效的 `recovery.bin` 文件可能导致系统无法启动。

你可以使用 `self-update` 模式覆盖此行为。在 `self-update` 模式下，你可以从 USB MSD 或网络引导更新引导加载程序。

>**警告**
>
>`self-update` 模式不会以原子方式更新引导加载程序。如果在更新 EEPROM 期间发生断电，可能会损坏 EEPROM。

### 修改引导加载程序配置

要修改计算模块 EEPROM 引导加载程序配置：

1. 切换到目录 `usbboot/recovery`。
2. 如果需要特定的引导加载程序版本，请用该版本中的对应文件替换 `pieeprom.original.bin`。
3. 编辑默认的引导加载程序配置文件 `boot.conf`，设置 `BOOT_ORDER`：
    * 网络启动使用 `BOOT_ORDER=0xf2`。
    * SD/eMMC 启动使用 `BOOT_ORDER=0xf1`。
    * USB 启动失败后转到 eMMC，使用 `BOOT_ORDER=0xf15`。
    * NVMe 启动使用 `BOOT_ORDER=0xf6`。
4. 运行 `./update-pieeprom.sh` 生成新的 EEPROM 镜像文件 `pieeprom.bin`。
5. 如果需要 EEPROM 写保护，请将 `eeprom_write_protect=1` 添加到 `/boot/firmware/config.txt`。
    * 通过软件启用后，可以将 `EEPROM_nWP` 引脚拉低，锁定硬件写保护。
6. 运行以下命令，将更新后的 `pieeprom.bin` 镜像写入 EEPROM：

    ```bash
    $ ../rpiboot -d .
    ```

## 连接外围设备

本指南帮助开发者将外设连接到计算模块引脚，并说明如何在软件中启用这些外设。

SoC 的大多数引脚（GPIO、两个 CSI 摄像头接口、两个 DSI 显示接口、HDMI 等）都可用于接线。通常可以将未使用的引脚保持未连接状态。

采用 DDR2 SODIMM 外形规格的计算模块与任何 DDR2 SODIMM 插座物理兼容。但是，引脚定义与 SODIMM 内存模块**不**相同。

要使用计算模块，用户设计的主板必须满足：

* 为计算模块供电（至少 3.3 V 和 1.8 V）
* 将引脚连接到用户应用程序所需的外围设备

本指南首先介绍引导过程，以及设备树如何描述所连接的硬件。

然后介绍如何将 I²C 和 SPI 外围设备连接到 IO 板。最后，创建在树莓派系统上使用这两个外围设备所需的设备树文件。

### BCM283x GPIO

BCM283x 带有三个通用输入/输出（GPIO）引脚组：BANK0 上有 28 个引脚，BANK1 上有 18 个引脚，BANK2 上有 8 个引脚，总共 54 个引脚。这些引脚可以用作真正的 GPIO 引脚：软件可以将它们设置为输入或输出，读取和/或设置状态，并将它们用作中断。它们还可以运行诸如 I²C、SPI、I²S、UART、SD 卡等其他功能。

你可以在任何计算模块上使用 BANK0 或 BANK1。不要使用 BANK2：它控制 eMMC、HDMI 热插拔检测和 ACT LED/USB 引导控制。

使用 `pinctrl` 检查 GPIO 引脚的电压和功能，以确认你的设备树是否按预期工作。

### BCM283x 引导过程

BCM283x 设备搭载了 VideoCore GPU 和 Arm CPU 核心。GPU 包括 DSP 处理器和用于图像处理、视频编解码、3D 图形和图像合成的硬件加速器。

在 BCM283x 设备中，最先启动的是 GPU 中的 DSP 核心，它会在启动主 Arm 处理器之前完成准备工作。

树莓派 BCM283x 设备有三阶段引导过程：

* GPU DSP 退出复位并从小型内部引导 ROM 执行代码。该代码通过外部接口加载第二阶段引导加载程序。该代码首先在引导分区的引导设备上查找名为 `bootcode.bin` 的第二阶段引导加载程序。如果未找到引导设备或未找到 `bootcode.bin`，引导 ROM 将在 USB 引导模式下等待主机提供第二阶段引导加载程序（`usbbootcode.bin`）。
* 第二阶段引导加载程序负责设置 LPDDR2 SDRAM 接口和其他关键系统功能。设置完成后，第二阶段引导加载程序加载并执行主 GPU 固件（`start.elf`）。
* `start.elf` 处理额外的系统设置并启动 Arm 处理器子系统。它包含 GPU 固件。GPU 固件首先读取 `dt-blob.bin` 以确定初始 GPIO 引脚状态和 GPU 特定接口和时钟，然后解析 `config.txt`。随后加载特定于型号的 Arm 设备树文件以及 `config.txt` 中指定的任何叠加层，最后启动 Arm 子系统，并将设备树数据传递给正在引导的 Linux 内核。

### 设备树

树莓派的 Linux 设备树描述了系统中连接的硬件，以及用于与该硬件通信的驱动程序。

引导分区包含几个二进制设备树（`.dtb`）文件。设备树编译器使用可读的设备树描述（`.dts`）创建这些二进制文件。

>**注意**
>
>树莓派计算模块 5 需要更新的设备树支持和内核驱动。从 CM4 迁移到 CM5 时，请使用树莓派系统 Bookworm 或更高版本、6.12.x 或更高版本的内核，以及 2025 年 3 月 10 日或之后的固件。

引导分区包含两种不同类型的设备树文件。一种仅供 GPU 使用；其余是针对每个基于 BCM283x 的树莓派产品的标准 Arm 设备树文件：

* `dt-blob.bin`（供 GPU 使用）
* `bcm2708-rpi-b.dtb`（用于树莓派 1 Model A 和 B）
* `bcm2708-rpi-b-plus.dtb`（用于树莓派 1 Model B+ 和 A+）
* `bcm2709-rpi-2-b.dtb`（用于树莓派 2B）
* `bcm2710-rpi-3-b.dtb`（用于树莓派 3B）
* `bcm2711-rpi-4-b.dtb`（用于树莓派 4 Model B）
* `bcm2712-rpi-5-b.dtb`（用于树莓派 5）
* `bcm2708-rpi-cm.dtb`（用于树莓派计算模块 1）
* `bcm2710-rpi-cm3.dtb`（用于树莓派计算模块 3）
* `bcm2711-rpi-cm4.dtb`（用于树莓派计算模块 4；如果找不到该文件，则改用 `bcm2711-rpi-4-b.dtb`）
* `bcm2712-rpi-cm5.dtb`（用于树莓派计算模块 5；如果找不到 CM5 设备树文件，则改用树莓派 5 的 `bcm2712-rpi-5-b.dtb`）

启动过程中，你可以在 `config.txt` 中通过 `device_tree` 参数指定要使用的 Arm 设备树。例如，`config.txt` 中的 `device_tree=mydt.dtb` 一行指定使用名为 `mydt.dtb` 的文件中的 Arm 设备树。

你可以为计算模块产品创建完整的设备树，但我们建议改用叠加层。叠加层为基本设备树添加与具体板卡无关的硬件描述。这包括使用的 GPIO 引脚及其功能，以及连接的设备，以便正确加载驱动程序。引导加载程序在将设备树传递给 Linux 内核之前将叠加层与基本设备树合并。基本设备树偶尔会更改，通常不会破坏叠加层。

使用 `dtoverlay` 参数在 `config.txt` 中加载设备树叠加层。树莓派系统假定所有叠加层都位于 `/overlays` 目录中，并使用 `-overlay.dtb` 后缀。例如，`dtoverlay=myoverlay` 这行加载了叠加层 `/overlays/myoverlay-overlay.dtb`。

要将外围设备连接到计算模块，请在叠加层中描述连接到 BANK0 和 BANK1 GPIO 的所有硬件。这样你就可以使用标准的树莓派系统镜像，因为叠加层已合并到标准基础设备树中。或者，你还可以为你的应用程序定义自定义设备树，但你将无法使用标准的树莓派系统镜像。因此，你每分发一次操作系统更新，都必须创建一个包含自定义设备树的修改版树莓派系统镜像。如果基础叠加层发生更改，则可能需要更新你的定制设备树。

### `dt-blob.bin`

当 `start.elf` 运行时，它首先读取 `dt-blob.bin`。这是一种特殊形式的设备树 blob，告诉 GPU 如何设置 GPIO 引脚状态。

`dt-blob.bin` 包含由 GPU 而不是 SoC 控制的 GPIO 和外围设备的信息。例如，GPU 管理摄像头模块。GPU 需要独占访问 I²C 接口和一些引脚，以便与摄像头模块通信。

在大多数树莓派型号上，I2C0 保留给 GPU 独占使用。`dt-blob.bin` 定义了用于 I2C0 的 GPIO 引脚。

默认情况下，`dt-blob.bin` 并不存在，`start.elf` 中内置了该文件的一个版本。许多计算模块项目提供了自定义 `dt-blob.bin`，用来覆盖内置的默认版本。

`dt-blob.bin` 指定了：

* 用于 HDMI 热插拔检测的引脚
* 用作 GPCLK 输出的 GPIO 引脚
* GPU 在引导过程中可以使用的 ACT LED

[`minimal-cm-dt-blob.dts`](https://pip.raspberrypi.com/documents/RP-008166-DS) 是一个示例 `.dts` 设备树文件。它设置了 HDMI 热插拔检测、ACT LED，并将所有其他 GPIO 设置为带默认上拉/下拉的输入。

要将 `minimal-cm-dt-blob.dts` 编译为 `dt-blob.bin`，请使用设备树编译器 `dtc`。要在树莓派上安装 `dtc`，请运行以下命令：

```bash
$ sudo apt install device-tree-compiler
```

然后，运行以下命令将 `minimal-cm-dt-blob.dts` 编译为 `dt-blob.bin`：

```bash
$ dtc -I dts -O dtb -o dt-blob.bin minimal-cm-dt-blob.dts
```

更多信息，请参阅我们的 `dt-blob.bin` 创建指南。

### Arm Linux 设备树

在 `start.elf` 读取 `dt-blob.bin`、设置初始引脚状态和时钟后，它就会读取 `config.txt`，其中包含许多其他系统设置选项。

在读取 `config.txt` 后，`start.elf` 会读取一个特定于模型的设备树文件。例如，计算模块 3 使用 `bcm2710-rpi-cm.dtb`。该文件是一个标准的 Arm Linux 设备树文件，详细说明连接到处理器的硬件。它枚举了：

* 外围设备的种类和位置
* 使用了哪些 GPIO
* 这些 GPIO 有什么功能
* 连接了哪些物理设备

如果与 `dt-blob.bin` 不同，此文件将通过覆盖引脚状态来设置 GPIO，并尝试为特定设备加载驱动程序。

特定型号的设备树文件包含针对外围设备的禁用条目。除 eMMC/SD 卡外设（它带有 GPIO 定义并使用固定引脚）外，该文件不包含其他 GPIO 引脚定义。

### 设备树源码和编译

树莓派系统镜像提供预编译的 `dtb` 文件，但源 `dts` 文件位于树莓派 Linux 内核分支中。请在文件名中查找 `rpi`。

默认叠加层 `dts` 文件位于 `arch/arm/boot/dts/overlays`。这些叠加层文件是创建自己的叠加层的好起点。要将这些 `dts` 文件编译为 `dtb` 文件，请使用设备树编译器 `dtc`。

编译自己的内核时，构建主机需要 `scripts/dtc` 中的设备树编译器。要让叠加层自动构建，请将它们添加到 `arch/arm/boot/dts/overlays/Makefile` 的 `dtbs` make 目标中。

### 设备树调试

当启动 Linux 内核时，GPU 使用基础 `dts` 和任意叠加层创建完整的设备树。这棵完整的树可以通过 Linux 的 proc 接口在 `/proc/device-tree` 中浏览。节点变成目录，属性变成文件。

你可以使用 `dtc` 将其写成人类可读的 `dts` 文件以进行调试。要查看完整组装后的设备树，请运行以下命令：

```bash
$ dtc -I fs -O dts -o proc-dt.dts /proc/device-tree
```

`pinctrl` 提供了 GPIO 引脚的状态。如果出现问题，请尝试转储 GPU 日志消息：

```bash
$ sudo vclog --msg
```

>**技巧**
>
>要在输出中包含更多诊断信息，请将 `dtdebug=1` 添加到 `config.txt`。

你可以在[树莓派设备树论坛](https://forums.raspberrypi.com/viewforum.php?f=107)提出设备树相关问题，或报告缺陷。

### 示例

以下示例使用的 IO 板通过跳线连接外围设备。我们假设使用全新安装的精简版树莓派系统运行 CM1+CMIO 或 CM3+CMIO3。这里的示例需要互联网连接，因此我们建议将 USB 集线器、键盘和无线局域网或以太网转接器插入 IO 板的 USB 端口。

#### 将 I²C RTC 连接到 BANK1 引脚

在这个示例中，我们将 NXP PCF8523 实时时钟（RTC）连接到 IO 板的 BANK1 GPIO 引脚：3V3、GND、GPIO44 上的 `I2C1_SDA` 和 GPIO45 上的 `I2C1_SCL`。

下载 [`minimal-cm-dt-blob.dts`](https://pip.raspberrypi.com/documents/RP-008166-DS)，将其复制到 `/boot/firmware/` 的引导分区中。

编辑 `minimal-cm-dt-blob.dts`，将 GPIO44 和 45 的引脚状态更改为带上拉的 I2C1：

```bash
$ sudo nano /boot/firmware/minimal-cm-dt-blob.dts
```

替换以下行：

```bash
pin@p44 { function = "input"; termination = "pull_down"; }; // 原状态为输入且无上下拉
pin@p45 { function = "input"; termination = "pull_down"; }; // 原状态为输入且无上下拉
```

使用以下上拉定义：

```bash
pin@p44 { function = "i2c1"; termination = "pull_up"; }; // SDA1
pin@p45 { function = "i2c1"; termination = "pull_up"; }; // SCL1
```

我们可以在不进行任何改动的情况下使用此 `dt-blob.dts`，因为 Linux 设备树会在特定驱动程序加载时重新配置这些引脚。但是，如果配置了 `dt-blob.dts`，GPIO 会在 GPU 引导阶段尽早达到最终状态。在某些情况下，必须在 GPU 引导时配置引脚，以便在加载 Linux 驱动程序时处于特定状态。例如，复位线可能需要保持在正确的电平状态。

运行以下命令编译 `dt-blob.bin`：

```bash
$ sudo dtc -I dts -O dtb -o /boot/firmware/dt-blob.bin /boot/firmware/minimal-cm-dt-blob.dts
```

下载 [`example1-overlay.dts`](https://pip.raspberrypi.com/documents/RP-008165-DS)，将其复制到 `/boot/firmware/` 中的引导分区，然后使用以下命令编译：

```bash
$ sudo dtc -@ -I dts -O dtb -o /boot/firmware/overlays/example1.dtbo /boot/firmware/example1-overlay.dts
```

`-@` 标志用于编译带外部引用的 `dts` 文件，通常必不可少。

将以下行添加到 `/boot/firmware/config.txt` 中：

```bash
dtoverlay=example1
```

最后，使用 `sudo reboot` 重启。

重启后，`/dev` 中会出现 `rtc0`。运行以下命令查看硬件时钟时间：

```bash
$ sudo hwclock
```

#### 在 BANK0 上连接一个 ENC28J60 SPI 以太网控制器

在本示例中，我们使用已在 `/boot/firmware/overlays` 中定义的叠加层，将 ENC28J60 SPI 以太网控制器添加到 BANK0。以太网控制器使用 SPI 引脚 CE0、MISO、MOSI 和 SCLK（分别为 GPIO8-11），GPIO25 用于下降沿中断，另外还有 GND 和 3.3 V。

在本示例中，我们不会更改 `dt-blob.bin`。而是将以下行添加到 `/boot/firmware/config.txt` 中：

```bash
dtoverlay=enc28j60
```

使用 `sudo reboot` 重启。

如果现在运行 `ifconfig`，你应该会看到 ENC28J60 网卡多出一个 `eth<n>` 条目。你还应该具备以太网连接。运行以下命令测试连接性：

```bash
$ ping 8.8.8.8
```

运行以下命令显示 GPIO 功能；GPIO8-11 现在应提供 ALT0（SPI）功能：

```bash
$ pinctrl
```

## 连接摄像头模块

计算模块具有两个 CSI-2 摄像头接口：CAM1 和 CAM0。本节将说明如何使用计算模块 I/O 板将一个或两个树莓派摄像头连接到计算模块的 CAM1 和 CAM0 接口。

### 更新你的系统

在配置摄像头之前，请确保树莓派的固件为最新版本。

```bash
$ sudo apt update
$ sudo apt full-upgrade
```

### 连接一个摄像头

要将单个摄像头连接到计算模块，请完成以下步骤：

1. 断开计算模块的电源。
2. 使用 RPI-CAMERA 板或树莓派 Zero 摄像头电缆将摄像头模块连接到 CAM1 接口。

![连接到转接板](.gitbook/assets/CMIO-Cam-Adapter.jpg)

3. （仅限 CM5）：按照板上的书面说明，在 J6 上装两个跳线。

![CAM1 的 J6 跳线](.gitbook/assets/cm5io-j6-cam1.png)

4. （仅限 CM1、CM3、CM3+ 和 CM4S）：使用跳线电缆连接以下 GPIO 引脚：

    * 0 到 CD1_SDA
    * 1 到 CD1_SCL
    * 2 到 CAM1_I01
    * 3 到 CAM1_I00

![单个摄像头的 GPIO 连接](.gitbook/assets/CMIO-Cam-GPIO.jpg)

5. 将计算模块重新连接到电源。
6. 如果 `/boot/firmware/config.txt` 中存在以下行，请删除（或用前缀 `#` 注释掉）：

    ```bash
    camera_auto_detect=1
    ```

    ```bash
    dtparam=i2c_arm=on
    ```
7. （仅限 CM1、CM3、CM3+ 和 CM4S）：向 `/boot/firmware/config.txt` 添加以下指令，以适配 I/O 板上互换的 GPIO 引脚分配：

    ```bash
    dtoverlay=cm-swap-i2c0
    ```
8. （仅限 CM1、CM3、CM3+ 和 CM4S）：向 `/boot/firmware/config.txt` 添加以下指令，将 GPIO 3 分配为 CAM1 稳压器：

    ```bash
    dtparam=cam1_reg
    ```
9. 向 `/boot/firmware/config.txt` 添加适当的指令，为你的摄像头型号手动配置驱动程序：

| 摄像头型号 | 参数 |
| :----------: | :---: |
| 摄像头模块 1 | `dtoverlay=ov5647` |
| 摄像头模块 2 | `dtoverlay=imx219` |
| 摄像头模块 3 | `dtoverlay=imx708` |
| HQ 摄像头 | `dtoverlay=imx477` |
| GS 摄像头 | `dtoverlay=imx296` |

10. 使用 `sudo reboot` 重启你的计算模块。
11. 运行以下命令查看检测到的摄像头列表：

     ```bash
     $ rpicam-hello --list
     ```

     输出中应能看到上表驱动指令所对应的摄像头型号。

### 连接两台摄像头

要将两台摄像头连接到计算模块，请完成以下步骤：

1. 按照上述单摄像头说明操作。
2. 断开计算模块的电源。
3. 使用 RPI-CAMERA 板或树莓派 Zero 摄像头电缆将摄像头模块连接到 CAM0 接口。

![连接到转接板](.gitbook/assets/CMIO-Cam-Adapter.jpg)

4. （仅限 CM1、CM3、CM3+ 和 CM4S）：使用跳线连接以下 GPIO 引脚：

    * 28 到 CD0_SDA
    * 29 到 CD0_SCL
    * 30 到 CAM0_I01
    * 31 到 CAM0_I00

![搭载附加摄像头的 GPIO 连接](.gitbook/assets/CMIO-Cam-GPIO2.jpg)

5. （CM4）：使用两根垂直方向的跳线连接 J6 GPIO 引脚。

![连接到垂直方向的 J6 GPIO 引脚](.gitbook/assets/j6_vertical.jpg)

6. 将计算模块重新连接到电源。
7. （仅限 CM1、CM3、CM3+ 和 CM4S）：向 `/boot/firmware/config.txt` 添加以下指令，将 GPIO 31 分配为 CAM0 稳压器：

    ```bash
    dtparam=cam0_reg
    ```
8. 向 `/boot/firmware/config.txt` 添加对应的参数，为你的摄像头型号手动配置驱动程序：

| 摄像头型号 | 参数 |
| :-------------------: | :---: |
| 摄像头模块 1 | `dtoverlay=ov5647,cam0` |
| 摄像头模块 2 | `dtoverlay=imx219,cam0` |
| 摄像头模块 3 | `dtoverlay=imx708,cam0` |
| HQ 摄像头 | `dtoverlay=imx477,cam0` |
| GS 摄像头 | `dtoverlay=imx296,cam0` |

9. 使用 `sudo reboot` 重启你的计算模块。
10. 运行以下命令查看检测到的摄像头列表：

     ```bash
     $ rpicam-hello --list
     ```

     输出中应能看到上表驱动指令所对应的两款摄像头型号。

### 软件

树莓派系统内置了 `libcamera` 库，可帮助你使用树莓派拍摄照片。

#### 拍照

使用以下命令立即拍照，并将其保存为 PNG 编码的文件，文件名采用 `MMDDhhmmss` 日期格式：

```bash
$ rpicam-still --datetime -e png
```

使用 `-t` 参数可按毫秒设置延迟。使用 `--width` 和 `--height` 参数可指定图像的宽度和高度。

#### 拍摄视频

使用以下命令立即开始录制十秒钟的视频，并将其保存为使用 h264 编解码器、名为 `video.h264` 的文件：

```bash
$ rpicam-vid -t 10000 -o video.h264
```

#### 指定要使用的摄像头

默认情况下，`libcamera` 总是使用 `--list-cameras` 列表中编号为 `0` 的摄像头。要指定使用哪个摄像头，请运行以下命令获取每个摄像头的编号：

```bash
$ rpicam-hello --list-cameras
Available cameras
-----------------
0 : imx477 [4056x3040] (/base/soc/i2c0mux/i2c@1/imx477@1a)
    Modes: 'SRGGB10_CSI2P' : 1332x990 [120.05 fps - (696, 528)/2664x1980 crop]
           'SRGGB12_CSI2P' : 2028x1080 [50.03 fps - (0, 440)/4056x2160 crop]
                             2028x1520 [40.01 fps - (0, 0)/4056x3040 crop]
                             4056x3040 [10.00 fps - (0, 0)/4056x3040 crop]

1 : imx708 [4608x2592] (/base/soc/i2c0mux/i2c@0/imx708@1a)
    Modes: 'SRGGB10_CSI2P' : 1536x864 [120.13 fps - (768, 432)/3072x1728 crop]
                             2304x1296 [56.03 fps - (0, 0)/4608x2592 crop]
                             4608x2592 [14.35 fps - (0, 0)/4608x2592 crop]
```

在上述输出中：

* `imx477` 指的是编号为 `0` 的 HQ 摄像头
* `imx708` 指的是编号为 `1` 的摄像头模块 3

要使用 HQ 摄像头，请将其编号（`0`）传给 `--camera` 选项：

```bash
$ rpicam-hello --camera 0
```

要使用摄像头模块 3，请将其编号（`1`）传给 `--camera` 选项：

```bash
$ rpicam-hello --camera 1
```

### GPIO 引脚的 I²C 映射

默认情况下，随附的摄像头驱动程序假定 CAM1 使用 `i2c-10`，CAM0 使用 `i2c-0`。计算模块 I/O 板将以下 GPIO 引脚映射到 `i2c-10` 和 `i2c-0`：

| I/O 板型号 | `i2c-10` 引脚 | `i2c-0` 引脚 |
| :-------------: | :--------- | :------------: |
| CM4 I/O 板 | GPIO 44、45 | GPIO 0、1 |
| CM1、CM3、CM3+ 和 CM4S I/O 板 | GPIO 0、1 | GPIO 28、29 |

要将摄像头连接到 CM1、CM3、CM3+ 和 CM4S I/O 板，请将以下指令添加到 `/boot/firmware/config.txt`，以适应交换后的引脚分配：

```bash
dtoverlay=cm-swap-i2c0
```

其他板卡可能采用不同的引脚分配。请查阅你的板卡文档，并根据你的布局使用以下替代叠加层：

| 交换 | 叠加层 |
| :-----------------: | :------: |
| 使用 GPIO 0、1 进行 i2c0 | `i2c0-gpio0` |
| 使用 GPIO 28、29 进行 i2c0（默认） | `i2c0-gpio28` |
| 使用 GPIO 44、45 进行 i2c0 | `i2c0-gpio44` |
| 使用 GPIO 0、1 进行 i2c10（默认） | `i2c10-gpio0` |
| 使用 GPIO 28、29 进行 i2c10 | `i2c10-gpio28` |
| 使用 GPIO 44、45 进行 i2c10 | `i2c10-gpio44` |

#### 用于关机的 GPIO 引脚

摄像头的关断由设备树使用叠加层 `cam1_reg` 和 `cam0_reg` 分配的引脚控制。

CM4 IO 板为这两个别名提供同一个 GPIO 引脚，因此两个摄像头共享同一个稳压器。

CM1、CM3、CM3+ 和 CM4S I/O 板未提供 `cam1_reg` 和 `cam0_reg` 的 GPIO 引脚，因此这些板上的稳压器处于禁用状态。但是，你可以通过在 `/boot/firmware/config.txt` 中使用以下指令来启用它们：

* `dtparam=cam1_reg`
* `dtparam=cam0_reg`

要将 `cam1_reg` 和 `cam0_reg` 分配到自定义板上的特定引脚，请在 `/boot/firmware/config.txt` 中加入以下参数：

* `dtparam=cam1_reg_gpio=<引脚编号>`
* `dtparam=cam0_reg_gpio=<引脚编号>`

例如，要将引脚 42 用作 CAM1 的稳压器，请将指令 `dtparam=cam1_reg_gpio=42` 添加到 `/boot/firmware/config.txt`。

这些指令仅对直连 SoC 的 GPIO 引脚有效，对 GPIO 扩展器引脚无效。

## 连接触摸显示屏 LCD 面板

* 要连接树莓派触摸显示屏，请参阅[触摸显示屏](../pei-jian/xian-shi-qi.md)。
* 要连接树莓派触摸显示屏 2，请参阅[触摸显示屏 2](../pei-jian/chu-mo-xian-shi-ping-2.md)。

## 规格

### 计算模块 5 数据表

要了解有关计算模块 5（CM5）及其对应 IO 板的更多信息，请参阅以下文档：

* [CM5 数据表](https://pip.raspberrypi.com/documents/RP-008180-DS)
* [CM5 设计文件](https://rpltd.co/cm5-design-files)

### 计算模块 5 IO 板数据表

计算模块 5 IO 板（CM5IO）的设计数据可以在其数据表中找到：

* [CM5IO 数据表](https://pip.raspberrypi.com/documents/RP-008182-DS)
* [CM5IO 设计文件](https://rpltd.co/cm5io-design-files)

### 计算模块 4 数据表

要了解有关计算模块 4（CM4）及其相应 IO 板的更多信息，请参阅以下文档：

* [CM4 数据表](https://pip.raspberrypi.com/documents/RP-008168-DS)

##### 白皮书

>[配置计算模块 4](https://pip.raspberrypi.com/documents/RP-003470-WP)
>
>计算模块 4 有多种不同的硬件配置。一些用例会禁用不需要的某些功能。
>
>本文档描述了如何禁用各种硬件和软件接口。

### 计算模块 4 IO 板数据表

设计数据可以在计算模块 4 IO 板（CM4IO）的数据表中找到：

* [CM4IO 数据表](https://pip.raspberrypi.com/documents/RP-008172-DS)

我们还为 CM4 IO 板提供 KiCad PCB 设计套件：

* [CM4IO KiCad 文件](https://pip.raspberrypi.com/documents/RP-008173-DS)

### 计算模块 4S 数据表

计算模块 4S（CM4S）采用 CM1、CM3 和 CM3+ 的 DDR2-SODIMM 外形规格，提供 CM4 的内部组件。要了解有关 CM4S 的更多信息，请参阅以下文档：

* [CM4S 数据表](https://pip.raspberrypi.com/documents/RP-008177-DS)

### 计算模块 3+ 数据表

计算模块 3+（CM3+）是一款受支持的产品，其生命周期终止（EOL）日期不早于 2028 年 1 月。要了解有关 CM3+ 及其对应 IO 板的更多信息，请参阅以下文档：

* [CM3+ 数据表](https://pip.raspberrypi.com/documents/RP-008163-DS)

### 计算模块 1 和计算模块 3 数据表

树莓派计算模块 1（CM1）和计算模块 3（CM3）是受支持的产品，其生命周期终止（EOL）日期不早于 2026 年 1 月。要了解有关 CM1 和 CM3 的更多信息，请参阅以下文档：

* [CM1 和 CM3 数据表](https://pip.raspberrypi.com/documents/RP-008161-DS)
* [CM1 的原理图](https://pip.raspberrypi.com/documents/RP-008162-DS)
* [CM3 的原理图](https://pip.raspberrypi.com/documents/RP-008164-DS)

##### 白皮书

>[从计算模块 1 和计算模块 3 过渡到计算模块 4](https://pip.raspberrypi.com/documents/RP-003469-WP)
>
>这份白皮书帮助开发者从计算模块 1 和计算模块 3 迁移到计算模块 4。

### 计算模块 IO 板原理图

计算模块 IO 板（CMIO）为 CM1、CM3、CM3+ 和 CM4S 提供各种接口。计算模块 IO 板有两个衍生版本：版本 1 和版本 3。版本 1 仅兼容 CM1。版本 3 兼容 CM1、CM3、CM3+ 和 CM4S。计算模块 IO 板版本 3 有时简写为 CMIO3。要了解有关 CMIO1 和 CMIO3 的更多信息，请参阅以下文档：

* [CMIO 的原理图](https://pip.raspberrypi.com/documents/RP-008256-DS)
* [CMIO Version 1.2（CMIO/CMIO1）的设计文档](https://pip.raspberrypi.com/documents/RP-008376-DS)
* [CMIO Version 3.0（CMIO3）的设计文档](https://pip.raspberrypi.com/documents/RP-008377-DS)

### 计算模块摄像头/显示适配板原理图

计算模块摄像头/显示适配板（CMCDA）为计算模块提供摄像头和显示接口。要了解有关 CMCDA 的更多信息，请参阅以下文档：

* [CMCDA 的原理图](https://pip.raspberrypi.com/documents/RP-008255-DS)
* [CMCDA Version 1.1 的设计文档](https://pip.raspberrypi.com/documents/RP-008375-DS)

### 欠压检测

以下原理图描述了旧款树莓派型号中使用的欠压检测电路：

![欠压检测](.gitbook/assets/under_voltage_detect.png)
