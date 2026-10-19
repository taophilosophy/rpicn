# Zero 型号

树莓派 **Zero** 提供超紧凑的单板计算机（SBC）设计，功耗低于我们的[经典型单板计算机](jing-dian-dan-ban-ji-suan-ji.md)。这些型号省略了经典型树莓派 SBC 上的某些功能，以实现更小的外形尺寸，更适合嵌入式和便携式应用。所有 Zero 型号共享相同的硬件基线，包括：

* 一个 microSD 卡槽。
* 一个 mini HDMI 端口。
* 两个 micro-USB 端口，一个用于输入电源，一个用于外部设备。

自初代 Zero 的 1.3 版起，所有 Zero 型号还包含一个 mini 22 针、0.5 mm（细）间距、11.5 mm 宽的 CSI（摄像头）端口。

同一代树莓派 Zero 内各型号的主要区别取决于主板是否包含：

* **无线连接。** 带有 *W* 后缀的型号包含用于 Wi-Fi 和蓝牙的板载无线电模块；不带 W 后缀的型号没有无线功能，需要 USB 适配器才能联网。
* **预焊 GPIO 排针。** 带有 *H* 后缀或 *with headers* 标签（视代数而定）的型号配有预焊的 40 针排针。不带后缀或标签的型号只有未焊接的孔；如果你想使用 GPIO，需要手动焊接排针或安装兼容的第三方引脚套件。

## 型号列表

下表按时间倒序列出树莓派 Zero 型号，便于快速查阅其主要区别特征。

带有无线连接的树莓派 Zero 型号（以 *W* 后缀标示）具备：

* 2.4 GHz 单频 802.11n Wi-Fi（35 Mb/s）。
* 蓝牙 4.2 和低功耗蓝牙（BLE）。

树莓派 **Zero 2 W** 使用 *with headers* 而非 *H* 后缀来表示带排针版本。缺少 *H* 或 *with headers* 后缀的型号，其 GPIO 排针未焊接引脚。有关各型号的更多信息，请参见本页后面的专门章节。

| 型号 | 微处理器 | 内存（RAM） | GPIO 排针 | GPU | CPU |
| ---- | -------- | ----------- | --------- | --- | --- |
| Raspberry Pi Zero 2 W with headers（2021） | 树莓派 [RP3A0](chu-li-qi.md#rp3a0) | 512 MB 内存 | 40 针 GPIO 排针 | VideoCore IV | 1 GHz 四核 64 位 Cortex-A53 |
| Raspberry Pi Zero 2 W（2021） | 树莓派 [RP3A0](chu-li-qi.md#rp3a0) | 512 MB 内存 | 未焊接引脚的 40 针 GPIO 排针 | VideoCore IV | 1 GHz 四核 64 位 Cortex-A53 |
| Raspberry Pi Zero WH（2018） | Broadcom [BCM2835](chu-li-qi.md#bcm2835) | 512 MB 内存 | 40 针 GPIO 排针 | VideoCore IV | 1 GHz 单核 32 位 ARM11 |
| Raspberry Pi Zero W（2017） | Broadcom [BCM2835](chu-li-qi.md#bcm2835) | 512 MB 内存 | 未焊接引脚的 40 针 GPIO 排针 | VideoCore IV | 1 GHz 单核 32 位 ARM11 |
| Raspberry Pi Zero（2015/2016） | Broadcom [BCM2835](chu-li-qi.md#bcm2835) | 512 MB 内存 | 未焊接引脚的 40 针 GPIO 排针 | VideoCore IV | 1 GHz 单核 32 位 ARM11 |

## Raspberry Pi Zero 2 W（带与不带排针）

![不带排针的 Raspberry Pi Zero 2 W（左）和带排针的版本（右）](https://www.raspberrypi.com/documentation/computers/images/zero2wandwh.jpg)

[Raspberry Pi Zero 2 W](https://www.raspberrypi.com/products/raspberry-pi-zero-2-w/) 配有未焊接引脚的 GPIO 排针；Raspberry Pi Zero 2 W with headers 配有预焊的 GPIO 排针。与 [Zero W 和 WH](#raspberry-pi-zero-w-和-wh) 一样，两个型号都可以通过 Wi-Fi 连接到网络。

Raspberry Pi Zero 2 W（带与不带排针）的尺寸约为 65 mm × 30 mm。更详细的尺寸，请参阅 [Raspberry Pi Zero 2 W 的机械图](https://pip.raspberrypi.com/documents/RP-008358-DS)。有关电路、元件和引脚连接的工程图，请参阅 [Raspberry Pi Zero 2 W 的原理图](https://pip.raspberrypi.com/documents/RP-008360-DS)。

### 相比 Raspberry Pi Zero W 和 WH 的功能变化

Raspberry Pi Zero 2 W（带与不带排针）具有与 Raspberry Pi Zero W 和 WH 相同的外形尺寸、连接器和安装孔，但还引入了以下性能和连接性改进：

* **系统级封装（SiP）。** SoC 和内存集成在单个 SiP（*RP3A0*）中，它包括：
  * 一个 Broadcom BCM2710A1 SoC，带有四个 64 位 Arm Cortex-A53 CPU 核心；每个 CPU 核心运行频率为 1 GHz。
  * 一个 400 MHz 的 Broadcom VideoCore IV GPU，用于视频和 3D 渲染任务。
  * 512 MB 的 LPDDR2 内存，运行频率为 450 MHz。
* **更快的处理器。** 以四核 64 位 Cortex-A53 处理器取代 Raspberry Pi Zero 上的单核 ARM11 处理器。
* **升级的蓝牙。** 将无线连接从蓝牙 4.0 升级到蓝牙 4.2。

以下各节在介绍这些变化的同时，还介绍：

* 焊接在 Raspberry Pi Zero 2 W 上的其他内部组件。
* 允许你将外部硬件连接到这些组件的物理插座和排针。

### Raspberry Pi Zero 2 W（带与不带排针）组件

Raspberry Pi Zero 2 W（带与不带排针）包含以下板载组件：

| 组件 | 说明 |
| ---- | ---- |
| **SiP** | SoC 和内存包含在同一组件（SiP）中。SiP 为 *RP3A0*，包含 Broadcom BCM2710A1 SoC（内含 1 GHz 四核 64 位 Cortex-A53 CPU 和 400 MHz VideoCore IV GPU），以及运行频率为 450 MHz 的 512 MB LPDDR2（增强型低功耗双倍数据速率 2）内存。 |
| **无线模块** | 一个充当两个组件的无线电模块：用于连接计算机网络的 *Wi-Fi* 无线电，提供单频（2.4 GHz）802.11b/g/n Wi-Fi；以及用于连接外设的*蓝牙*无线电，提供蓝牙 4.2 和低功耗蓝牙（BLE）。 |

### Raspberry Pi Zero 2 W（带与不带排针）端口

Raspberry Pi Zero 2 W（带与不带排针）包含以下端口：

| 端口类型 | Raspberry Pi Zero 2 W | Raspberry Pi Zero 2 W with headers |
| -------- | --------------------- | ---------------------------------- |
| **Micro USB 端口** | 两个 micro USB 端口，一个用于输入电源，一个用于 USB On-The-Go（OTG），兼容 OTG 适配器以连接键盘、鼠标、USB 集线器和其他外部设备。 | 同左 |
| **Mini-HDMI 端口** | 一个 mini-HDMI 端口，支持单显示器，视频和音频输出最高 1080p、60 Hz。 | 同左 |
| **CSI（摄像头）端口** | 一个 2 通道 MIPI 摄像头串行接口（CSI）端口，可连接摄像头。采用 mini 22 针、0.5 mm（细）间距、11.5 mm 宽的 CSI 端口。 | 同左 |
| **GPIO 排针（未焊接或已焊接）** | 标准 40 针 GPIO 接口，排列为两行各 20 针。GPIO 排针未焊接引脚；焊接 2 × 20、2.54 mm 排针后，其引脚可让你的 Raspberry Pi Zero 2 W 与其他硬件（如 LED、按钮、传感器等）通信。 | 标准 40 针 GPIO 接口，排列为两行各 20 针，带有预焊的 2 × 20、2.54 mm 排针。其引脚可让你的 Raspberry Pi Zero 2 W with headers 与其他硬件（如 LED、按钮、传感器等）通信。 |
| **MicroSD 卡槽** | 一个 microSD 卡槽，用于加载操作系统和存储数据。 | 同左 |

### 测试点位置

![Zero 2 W 测试点示意图](https://www.raspberrypi.com/documentation/computers/images/zero2-pad-diagram.png)

Raspberry Pi Zero 2 W（带与不带排针）有若干在生产过程中使用的测试点，如下表所列。

| 标签 | 功能 | X（距原点 mm） | Y（距原点 mm） |
| ---- | ---- | -------------- | -------------- |
| `STATUS_LED` | LED 电源状态（LOW = 亮） | 5.15 | 8.8 |
| `CORE` | 处理器电源 | 6.3 | 18.98 |
| `RUN` | 连接到 `GND` 以复位 | 8.37 | 22.69 |
| `5V` | 5 V 输入 | 8.75 | 11.05 |
| `5V` | 5 V 输入 | 11.21 | 6.3 |
| `GND` | 接地引脚 | 10.9 | 3.69 |
| `GND` | 接地引脚 | 17.29 | 2.41 |
| `USB_DP` | USB 端口 | 22.55 | 1.92 |
| `USB_DM` | USB 端口 | 24.68 | 1.92 |
| `OTG` | On-the-go ID 引脚 | 39.9 | 7.42 |
| `1V8` | 1.8 V 模拟电源 | 42.03 | 8.42 |
| `TV` | 复合视频输出 | 45.58 | 3.17 |
| `GND` | 接地引脚 | 49.38 | 3.05 |
| `GND` | 接地引脚 | 55.99 | 22.87 |
| `3V3` | 3.3 V I/O 电源 | 48.55 | 22.44 |
| `SD_CLK` | SD 卡时钟引脚 | 60.95 | 18.45 |
| `SD_CMD` | SD 卡命令引脚 | 58.2 | 16.42 |
| `SD_DAT0` | SD 数据引脚 | 58.13 | 20.42 |
| `SD_DAT1` | SD 数据引脚 | 60.65 | 21.1 |
| `SD_DAT2` | SD 数据引脚 | 57.78 | 13.57 |
| `SD_DAT3` | SD 数据引脚 | 60.8 | 15.22 |
| `BT_ON` | 蓝牙电源状态 | 25.13 | 19.55 |
| `WL_ON` | 无线局域网电源状态 | 27.7 | 19.2 |

## Raspberry Pi Zero W 和 WH

![Raspberry Pi Zero W（左）和 WH（右）](https://www.raspberrypi.com/documentation/computers/images/zerowandwh.jpg)

[Raspberry Pi Zero W](https://www.raspberrypi.com/products/raspberry-pi-zero-w/) 配有未焊接引脚的 GPIO 排针；Raspberry Pi Zero WH 配有预焊的 GPIO 排针。两个型号都不包含有线以太网端口，但你仍然可以通过 Wi-Fi 连接到网络。

Raspberry Pi Zero W 和 WH 的尺寸约为 65 mm × 30 mm。更详细的尺寸，请参阅 [Raspberry Pi Zero W 的机械图](https://pip.raspberrypi.com/documents/RP-008367-DS)。有关电路、元件和引脚连接的工程图，请参阅 [Raspberry Pi Zero W 的原理图](https://pip.raspberrypi.com/documents/RP-008368-DS)。

### 相比 Raspberry Pi Zero 的功能变化

Raspberry Pi Zero W 和 WH 具有与 Raspberry Pi Zero 相同的外形尺寸、组件、连接器和安装孔，但还加入了**无线网络**：

* 单频（2.4 GHz）802.11b/g/n Wi-Fi。
* 蓝牙 4.0 和低功耗蓝牙（BLE）。

此外，Raspberry Pi Zero WH 是首个提供**预焊 GPIO 排针**的 Zero 型号。

以下各节在介绍这些变化的同时，还介绍：

* 焊接在 Raspberry Pi Zero W 上的其他内部组件。
* 允许你将外部硬件连接到这些组件的物理插座和排针。

### Raspberry Pi Zero W 和 WH 组件

Raspberry Pi Zero W 和 WH 包含以下板载组件：

| 组件 | 说明 |
| ---- | ---- |
| **SiP** | *Broadcom BCM2835*，包含 1 GHz 单核 32 位 ARM11 CPU 和 400 MHz VideoCore IV GPU。 |
| **内存** | 512 MB *LPDDR2*（低功耗双倍数据速率 2）内存，运行频率为 450 MHz。 |
| **无线模块** | 一个充当两个组件的无线电模块：用于连接计算机网络的 *Wi-Fi* 无线电，提供单频（2.4 GHz）802.11b/g/n Wi-Fi；以及用于连接外设的*蓝牙*无线电，提供蓝牙 4.0 和低功耗蓝牙（BLE）。 |

### Raspberry Pi Zero W 端口

Raspberry Pi Zero W 和 WH 包含以下端口：

| 端口类型 | Raspberry Pi Zero W | Raspberry Pi Zero WH |
| -------- | ------------------- | -------------------- |
| **Micro USB 端口** | 两个 micro USB 端口，一个用于输入电源，一个用于 USB on-the-go（OTG），兼容 OTG 适配器以连接键盘、鼠标、USB 集线器和其他外部设备。 | 同左 |
| **Mini-HDMI 端口** | 一个 mini-HDMI 端口，支持单显示器，视频和音频输出最高 1080p、60 Hz。 | 同左 |
| **CSI（摄像头）端口** | 一个 2 通道 MIPI 摄像头串行接口（CSI）端口，可连接摄像头。采用 mini 22 针、0.5 mm（细）间距、11.5 mm 宽的 CSI 端口。 | 同左 |
| **GPIO 排针（未焊接或已焊接）** | 标准 40 针 GPIO 接口，排列为两行各 20 针。GPIO 排针未焊接引脚；焊接 2 × 20、2.54 mm 排针后，其引脚可让你的 Raspberry Pi Zero 2 W 与其他硬件（如 LED、按钮、传感器等）通信。 | 标准 40 针 GPIO 接口，排列为两行各 20 针，带有预焊的 2 × 20、2.54 mm 排针。其引脚可让你的 Raspberry Pi Zero WH 与其他硬件（如 LED、按钮、传感器等）通信。 |
| **MicroSD 卡槽** | 一个 microSD 卡槽，用于加载操作系统和存储数据。 | 同左 |

## Raspberry Pi Zero

Raspberry Pi Zero 是经典型树莓派型号的更紧凑版本，连接器更少，GPIO 排针未焊接引脚。

![Raspberry Pi Zero](https://www.raspberrypi.com/documentation/computers/images/zero1.jpg)

Raspberry Pi Zero 的尺寸约为 65 mm × 30 mm。更详细的尺寸，请参阅 [Raspberry Pi Zero 的机械图](https://pip.raspberrypi.com/documents/RP-008366-DS)。有关电路、元件和引脚连接的工程图，请参阅 [Raspberry Pi Zero 的原理图](https://pip.raspberrypi.com/documents/RP-008365-DS)。

还有适用于 Raspberry Pi Zero 机箱的机械图：

* [Raspberry Pi Zero 机箱机械图（PDF）](https://pip.raspberrypi.com/documents/RP-008362-DS)
* [带 GPIO 盖板的 Raspberry Pi Zero 机箱机械图（PDF）](https://pip.raspberrypi.com/documents/RP-008364-DS)
* [带摄像头盖板的 Raspberry Pi Zero 机箱机械图（PDF）](https://pip.raspberrypi.com/documents/RP-008363-DS)

### Raspberry Pi Zero 组件

Raspberry Pi Zero 包含以下板载组件：

| 组件 | 说明 |
| ---- | ---- |
| **SoC** | *Broadcom BCM2835*，包含 1 GHz 单核 32 位 ARM11 CPU 和 400 MHz VideoCore IV GPU。 |
| **内存** | 512 MB *LPDDR2*（低功耗双倍数据速率 2）内存，运行频率为 450 MHz。 |

### Raspberry Pi Zero 端口

Raspberry Pi Zero 包含以下端口：

| 端口类型 | 说明 |
| -------- | ---- |
| **Micro USB 端口** | 两个 micro USB 端口，一个用于输入电源，一个用于 USB on-the-go（OTG），兼容 OTG 适配器以连接键盘、鼠标、USB 集线器和其他外部设备。 |
| **Mini-HDMI 端口** | 一个 mini-HDMI 端口，支持单显示器，视频和音频输出最高 1080p、60 Hz。 |
| **CSI（摄像头）端口** | 一个 2 通道 MIPI 摄像头串行接口（CSI）端口，可连接摄像头。采用 mini 22 针、0.5 mm（细）间距、11.5 mm 宽的 CSI 端口。 |
| **GPIO 排针（未焊接）** | 标准 40 针 GPIO 接口，排列为两行各 20 针。GPIO 排针未焊接引脚；焊接 2 × 20、2.54 mm 排针后，其引脚可让你的 Raspberry Pi Zero 与其他硬件（如 LED、按钮、传感器等）通信。 |
| **MicroSD 卡槽** | 一个 microSD 卡槽，用于加载操作系统和存储数据。 |
