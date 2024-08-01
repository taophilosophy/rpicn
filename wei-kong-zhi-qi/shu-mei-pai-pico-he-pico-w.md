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

## 树莓派 Pico W 和 Pico WH

树莓派 Pico W 在保持 Pico 形态因素的同时，添加了内置的单频段 2.4GHz 无线接口（802.11n），使用 Infineon CYW43439 芯片。内置的 2.4GHz 无线接口具有以下特性：

- 无线（802.11n），单频段（2.4 GHz）
- WPA3
- 软接入点，支持最多四个客户端
- 蓝牙 5.2
  - 支持蓝牙低功耗中心与外围角色
  - 支持经典蓝牙

天线是来自 ABRACON（前身为 ProAnt）的内置天线。无线接口通过 SPI 连接到 [RP2040](https://www.raspberrypi.com/documentation/microcontrollers/rp2040.html#welcome-to-rp2040) 微控制器。

由于引脚限制，部分无线接口引脚是共享的。CLK 与 VSYS 监视器共享，因此只有在没有 SPI 事务进行时才能通过 ADC 读取 VSYS。Infineon CYW43439 的 DIN/DOUT 和 IRQ 都共用一个 RP2040 引脚。只有在没有 SPI 事务进行时才适合检查 IRQ。接口通常以 33MHz 运行。

为了获得最佳的无线性能，天线应置于自由空间中。例如，在天线下方或附近放置金属会降低其增益和带宽性能。在天线的两侧添加接地金属可以提高天线的带宽。

>**注意**
>
>CYW43439 无线芯片通过 SPI 连接到 RP2040。CYW43439 支持通过这一接口的 802.11 无线和蓝牙。 

>**重要**
>
>默认情况下，`libcyw43` 只授权非商业使用，但是 Pico W 用户和其他围绕 RP2040 和 CYW43439 构建其产品的用户可以获得免费的[商业使用许可证](https://github.com/georgerobotics/cyw43-driver/blob/195dfcc10bb6f379e3dea45147590db2203d3c7b/LICENSE.RP)。 

>**重要**
>
> 除了[标准 BTstack 许可](https://github.com/bluekitchen/btstack/blob/master/LICENSE) 条款外，还提供了一个[补充许可证](https://github.com/raspberrypi/pico-sdk/blob/master/src/rp2_common/pico_btstack/LICENSE.RP)，涵盖了在树莓派 Pico W 和树莓派 Pico WH 上使用 BTstack 的商业用途。 

### 引脚定义和设计文件

![picow 引脚定义](https://www.raspberrypi.com/documentation/microcontrollers/images/picow-pinout.svg)

- 下载 [引脚定义图](https://datasheets.raspberrypi.com/picow/PicoW-A4-Pinout.pdf)（PDF）
- 下载 [设计文件](https://datasheets.raspberrypi.com/picow/RPi-PicoW-PUBLIC-20220607.zip)（Cadence Allegro）
- 下载 [STEP 文件](https://datasheets.raspberrypi.com/picow/PicoW-step.zip)
- 下载适用于树莓派 Pico W 的 [Fritzing 部件](https://datasheets.raspberrypi.com/picow/PicoW-Fritzing.fzpz)

## 文档

关于树莓派 Pico 和其他基于 RP2040 的板的文档。

### RP2040 设备

- [RP2040 数据手册](https://datasheets.raspberrypi.com/rp2040/rp2040-datasheet.pdf)：Raspberry Pi 开发的微控制器
- [使用 RP2040 进行硬件设计](https://datasheets.raspberrypi.com/rp2040/hardware-design-with-rp2040.pdf)：使用 RP2040 微控制器构建板和产品

### 树莓派 Pico

- [树莓派 Pico 数据手册](https://datasheets.raspberrypi.com/pico/pico-datasheet.pdf)：基于 RP2040 的微控制器板
- [开始使用树莓派 Pico](https://datasheets.raspberrypi.com/pico/getting-started-with-pico.pdf)：使用树莓派 Pico 和其他基于 RP2040 的微控制器板进行 C/C++ 开发


### 树莓派 Pico W

[树莓派 Pico W Datasheet](https://datasheets.raspberrypi.com/picow/pico-w-datasheet.pdf)
一款基于 RP2040 芯片的无线微控制器板。

[连接树莓派 Pico W 到互联网](https://datasheets.raspberrypi.com/picow/connecting-to-the-internet-with-pico-w.pdf)
使用 C/C++ 或 MicroPython 将树莓派 Pico W 连接到互联网的指南。

| 注意 | 关于如何在树莓派 Pico W 上使用 C/C++ 或 MicroPython 连接 Wi-Fi 和蓝牙的文档可以在 [连接树莓派 Pico W 到互联网](https://datasheets.raspberrypi.com/picow/connecting-to-the-internet-with-pico-w.pdf) 中找到。 |
| ------ | ---------------------------------------------------------------------------------------------------------------------------------------- |

### 软件开发

[树莓派 Pico C/C++ SDK](https://datasheets.raspberrypi.com/pico/raspberry-pi-pico-c-sdk.pdf)
用于在 RP2040 微控制器上进行 C/C++ 开发的库和工具。

[树莓派 Pico Python SDK](https://datasheets.raspberrypi.com/pico/raspberry-pi-pico-python-sdk.pdf)
为 RP2040 微控制器提供的 MicroPython 开发环境。

树莓派 Pico C/C++ SDK 的 API 级别的 Doxygen 文档也可以作为一个微型网站访问，链接为 [这里](https://rptl.io/pico-doxygen)。

>**注意**
>
>可以通过 [一键安装程序](https://github.com/raspberrypi/pico-setup-windows/releases/latest/download/pico-setup-windows-x64-standalone.exe) 在 Windows 10 和 Windows 11 上安装 Pico C/C++ SDK。 

## 软件工具

### Pico 上的内容是什么？

如果你忘记了已编程到树莓派 Pico 上的内容，并且该程序是使用我们的 Pico C/C++ SDK 构建的，则通常会在二进制文件中嵌入名称和其他有用信息。你可以使用 [Picotool](https://github.com/raspberrypi/picotool) 命令行实用程序查找这些详细信息。关于如何使用 Picotool 的完整说明可以在我们的 '[入门指南](https://datasheets.raspberrypi.com/pico/getting-started-with-pico.pdf)' 文档中找到。

* 访问 [Picotool GitHub 仓库](https://github.com/raspberrypi/picotool)。

### 使用另一个树莓派 Pico 进行调试

你可以使用一个树莓派 Pico 来调试另一个 Pico。这可以通过 `debugprobe` 实现，它允许一个 Pico 充当 USB → SWD 和 UART 转换器。

你可以在 [debugprobe GitHub 仓库](https://github.com/raspberrypi/debugprobe/releases/latest) 中找到最新版本的固件。

从最新版本中下载 `debugprobe_on_pico.uf2`。

在将调试器 Pico 插入计算机时，按住 BOOTSEL 按钮以挂载名为 "RPI-RP2" 的卷。

将 `debugprobe_on_pico.uf2` 复制到该卷上。文件复制完成后，卷将自动卸载。

你的 Pico 将重新启动，并且现在运行更新版本的 `debugprobe` 固件。现在可以开始进行调试了。

>**技巧**
>
>如需了解如何使用调试器，请参阅 [Getting Started with Pico](https://datasheets.raspberrypi.com/pico/getting-started-with-pico.pdf)。

### 重置 Flash 存储器

Pico 的 BOOTSEL 模式存储在 RP2040 芯片内的只读存储器中，不会意外被覆盖。无论如何，如果你在插入 Pico 时按住 BOOTSEL 按钮，它将显示为一个驱动器，你可以将新的 UF2 文件拖放到其中。没有办法通过软件使板子变砖。但是，在某些情况下，你可能希望确保 Flash 存储器为空。你可以在 Pico 处于大容量存储模式时通过拖放一个特殊的 UF2 二进制文件来实现这一点。

* 下载 [UF2 文件](https://datasheets.raspberrypi.com/soft/flash_nuke.uf2)
* 在 Github 上查看[代码](https://github.com/raspberrypi/pico-examples/blob/master/flash/nuke/nuke.c)
