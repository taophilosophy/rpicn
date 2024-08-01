# 树莓派 Pico 和 Pico W

## 产品家族

![四款 Pico](https://www.raspberrypi.com/documentation/microcontrollers/images/four_picos.jpg?hash=3f928dff64ab31c4f3b1caecf4fb83a4)

树莓派 Pico 家族目前拥有四款开发板：树莓派 Pico（最左侧）、Pico H（中左）、Pico W（中右）和 Pico WH（最右侧）。

## 树莓派 Pico、Pico H

树莓派 Pico 是一款低成本、高性能的微控制器板，搭载了灵活的数字接口。其主要特性包括：

* 由英国树莓派设计的 [RP2040](https://www.raspberrypi.com/documentation/microcontrollers/rp2040.html#welcome-to-rp2040) 微控制器芯片
* 双核 Arm Cortex M0+ 处理器，最高可动态提升至 133 MHz
* 264kB SRAM，2MB 板载闪存存储器
* USB 1.1，支持设备和主机模式
* 低功耗睡眠模式，低功耗休眠模式
* 通过 USB 实现拖放式编程
* 26 针多功能 GPIO 引脚
* 2 个 SPI，2 个 I²C，2 个串口，3 个 12 位 ADC，16 位可调 PWM 通道
* 内置精准时钟和定时器
* 温度传感器
* 芯片内加速浮点库支持
* 8 个可编程 I/O（PIO）状态机，用于自定义外设支持

树莓派 Pico 以铸边模块形式提供，可直接焊接到基板上，而 Pico H 则预焊接了引脚。

>**注意**
>
>两款主板均带有三针串行线调试（SWD）接头。但是，Pico H 将其拆分为一个小型的、带键向连接器的 [3 针连接器](https://datasheets.raspberrypi.com/debug/debug-connector-specification.pdf)，而 Pico 则有三个铸边过孔引脚，靠近主板边缘。 


### 引脚定义和设计文件

![Pico 引脚定义](https://www.raspberrypi.com/documentation/microcontrollers/images/pico-pinout.svg)

* 下载 [引脚定义图](https://datasheets.raspberrypi.com/pico/Pico-R3-A4-Pinout.pdf)（PDF）
* 下载 [设计文件](https://datasheets.raspberrypi.com/pico/RPi-Pico-R3-PUBLIC-20200119.zip)（Cadence Allegro）
* 下载 [STEP 文件](https://datasheets.raspberrypi.com/pico/Pico-R3-step.zip)
* 下载适用于树莓派 Pico 的 [Fritzing 部件](https://datasheets.raspberrypi.com/pico/Pico-R3-Fritzing.fzpz)
* 下载适用于树莓派 Pico H 的 [Fritzing 部件](https://datasheets.raspberrypi.com/pico/PicoH-Fritzing.fzpz)

>**注意**
>
>更多有关 Fritzing 的信息请访问 [fritzing.org](https://fritzing.org/) 网站。

## 树莓派 Pico W、Pico WH

树莓派 Pico W 在维系 Pico 外形尺寸的同时，搭载了内置的 2.4GHz 单频无线接口（802.11n），基于英飞凌（Infineon）CYW43439 芯片。内置的 2.4GHz 无线接口拥有以下功能：

- 无线（802.11n），单频（2.4 GHz）
- WPA3
- 软接入点，最多支持四个客户端
- 蓝牙 5.2
  - 支持蓝牙低功耗中心与外围角色
  - 兼容传统蓝牙

内置天线来自艾博康（ABRACON，前身为 ProAnt）。无线端口通过 SPI 连接至 [RP2040](https://www.raspberrypi.com/documentation/microcontrollers/rp2040.html#welcome-to-rp2040) 微控制器。

由于引脚限制，部分无线接口引脚是复用的。CLK 与 VSYS 监视器复用，因此仅在没有运行时 SPI 事务才能通过 ADC 读取 VSYS。英飞凌 CYW43439 的 DIN/DOUT 和 IRQ 都复用一个 RP2040 引脚。只有在没有运行时 SPI 事务才适合检查 IRQ。端口通常运行在 33MHz。

为了使无线性能呈最佳，天线应位于开放空间中。如果在天线下方（及附近）放置金属将会干扰天线增益，降低带宽性能。在天线的两侧添加接地金属可以提高天线的带宽。

>**注意**
>
>无线芯片 CYW43439 通过 SPI 连接到 RP2040。CYW43439 通过此端口提供 802.11 无线和蓝牙。 

>**重要**
>
>在默认情况下，`libcyw43` 仅授权非商业使用，但是 Pico W 和其他基于 RP2040 和 CYW43439 衍生产品的用户可免费获取[商业使用许可证](https://github.com/georgerobotics/cyw43-driver/blob/195dfcc10bb6f379e3dea45147590db2203d3c7b/LICENSE.RP)。 

>**重要**
>
> 除了[BTstack 标准许可](https://github.com/bluekitchen/btstack/blob/master/LICENSE) 条款外，还附带了一份[补充许可证](https://github.com/raspberrypi/pico-sdk/blob/master/src/rp2_common/pico_btstack/LICENSE.RP)，涉及了在树莓派 Pico W、Pico WH 上 BTstack 的商业使用用途。 

### 引脚定义和设计文件

![picow 引脚定义](https://www.raspberrypi.com/documentation/microcontrollers/images/picow-pinout.svg)

- 下载 [引脚定义图](https://datasheets.raspberrypi.com/picow/PicoW-A4-Pinout.pdf)（PDF）
- 下载 [设计文件](https://datasheets.raspberrypi.com/picow/RPi-PicoW-PUBLIC-20220607.zip)（Cadence Allegro）
- 下载 [STEP 文件](https://datasheets.raspberrypi.com/picow/PicoW-step.zip)
- 下载适用于树莓派 Pico W 的 [Fritzing 部件](https://datasheets.raspberrypi.com/picow/PicoW-Fritzing.fzpz)

## 文档

关于树莓派 Pico 和其他基于 RP2040 的主板文档。

### RP2040 设备

- [RP2040 数据手册](https://datasheets.raspberrypi.com/rp2040/rp2040-datasheet.pdf)：树莓派开发的微控制器
- [使用 RP2040 进行硬件设计](https://datasheets.raspberrypi.com/rp2040/hardware-design-with-rp2040.pdf)：使用 RP2040 微控制器构建主板和产品

### 树莓派 Pico

- [树莓派 Pico 数据手册](https://datasheets.raspberrypi.com/pico/pico-datasheet.pdf)：基于 RP2040 的微控制器板
- [开始使用树莓派 Pico](https://datasheets.raspberrypi.com/pico/getting-started-with-pico.pdf)：使用树莓派 Pico 和其他基于 RP2040 的微控制器板进行 C/C++ 开发


### 树莓派 Pico W

[树莓派 Pico W Datasheet](https://datasheets.raspberrypi.com/picow/pico-w-datasheet.pdf)

一款基于 RP2040 芯片的无线微控制器板。

[将树莓派 Pico W 接入互联网](https://datasheets.raspberrypi.com/picow/connecting-to-the-internet-with-pico-w.pdf)

使用 C/C++、MicroPython 将树莓派 Pico W 接入互联网的指南。

>**注意**
>
>在树莓派 Pico W 上使用 C/C++、MicroPython 连接 WiFi 和蓝牙的文档可以在[连接树莓派 Pico W 到互联网](https://datasheets.raspberrypi.com/picow/connecting-to-the-internet-with-pico-w.pdf) 中找到。 

### 软件开发

[树莓派 Pico C/C++ SDK](https://datasheets.raspberrypi.com/pico/raspberry-pi-pico-c-sdk.pdf)

在 RP2040 微控制器上进行 C/C++ 开发的库和工具。

[树莓派 Pico Python SDK](https://datasheets.raspberrypi.com/pico/raspberry-pi-pico-python-sdk.pdf)

为 RP2040 微控制器提供的 MicroPython 开发环境。

在一个小型网站中能访问树莓派 Pico C/C++ SDK 的 API 级的 Doxygen 文档，链接在[此处](https://rptl.io/pico-doxygen)。

>**注意**
>
>可以用[一键安装程序](https://github.com/raspberrypi/pico-setup-windows/releases/latest/download/pico-setup-windows-x64-standalone.exe) 在 Windows 10 和 Windows 11 上安装 Pico C/C++ SDK。 

## 软件工具

### Pico 上的内容是什么？

如果你忘记了已编程到树莓派 Pico 上的内容，且该程序是由我们的 Pico C/C++ SDK 构建的，则通常会在二进制文件中嵌入名称和其他有用信息。你可以使用 [Picotool](https://github.com/raspberrypi/picotool) 命令行实用程序查找这些详细信息。可以在我们的 '[入门指南](https://datasheets.raspberrypi.com/pico/getting-started-with-pico.pdf)' 文档中找到有关Picotool 的完整使用说明。

* 访问 [Picotool GitHub 存储库](https://github.com/raspberrypi/picotool)。

### 使用另一个树莓派 Pico 进行调试

你可以使用一个树莓派 Pico 来调试另一个 Pico。这可以用 `debugprobe` 做到，它能让一个 Pico 充当 USB → SWD 和 UART 转换器。

你可以在 [debugprobe GitHub 存储库](https://github.com/raspberrypi/debugprobe/releases/latest) 中找到最新版固件。

下载最新版本 `debugprobe_on_pico.uf2`。

将调试器 Pico 插入计算机，同时按住 BOOTSEL 按钮以挂载卷，显示为 "RPI-RP2"。

将 `debugprobe_on_pico.uf2` 复制到该卷上。文件复制完成后，卷会自动弹出。

你的 Pico 将重启，且现在运行着新版本的 `debugprobe` 固件。现在可以着手进行调试了。

>**技巧**
>
>如需了解调试器的使用方法，请参阅 [Getting Started with Pico](https://datasheets.raspberrypi.com/pico/getting-started-with-pico.pdf)。

### 重置 Flash 存储器

Pico 的 BOOTSEL 模式存储在 RP2040 芯片内的只读存储器中，不会被意外覆盖。无论如何，只要你在插入 Pico 时按住 BOOTSEL 按钮，它将呈现为一个硬盘驱动器，你可以将新的 UF2 文件拖放到里面。软件无法把开发板变砖。但是，在某些情况下，你可能希望确保 Flash 存储器为空。你可以在 Pico 位于大容量存储模式时，拖放一个特殊的 UF2 二进制文件来做到这一点。

* 下载 [UF2 文件](https://datasheets.raspberrypi.com/soft/flash_nuke.uf2)
* 在 Github 上查看[代码](https://github.com/raspberrypi/pico-examples/blob/master/flash/nuke/nuke.c)
