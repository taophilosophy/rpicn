# 树莓派 Pico 和 Pico W

## 产品家族


![four picos](https://www.raspberrypi.com/documentation/microcontrollers/images/four_picos.jpg)

树莓派 Pico 系列目前包括四款板卡；树莓派 Pico（最左侧）、Pico H（左中）、Pico W（右中）和 Pico WH（最右侧）。

## 树莓派 Pico 和 Pico H

树莓派 Pico 是一款价格低廉、性能卓越的微控制器板，具有灵活的数字接口。主要特点包括：

* 树莓派在英国设计的 RP2040 微控制器芯片
* 双核 Arm Cortex M0+ 处理器，灵活时钟运行高达 133 MHz
* 264KB 的 SRAM，和 2MB 的板载闪存存储器
* USB 1.1，具备设备和主机支持
* 低功耗睡眠和休眠模式
* 通过 USB 进行大容量存储的拖放式编程
* 26 × 多功能 GPIO 引脚
* 2 × SPI，2 × I2C，2 × UART，3 × 12 位 ADC，16 × 可控 PWM 通道
* 芯片上准确的时钟和定时器
* 温度传感器
* 芯片上的加速浮点库
* 8 个可编程 I/O（PIO）状态机，用于自定义外围支持

树莓派 Pico 作为一个铸铁模块，可以直接焊接到载板上，而 Pico H 则带有预先焊接的引脚。

>**注意**
>
>两个板都有一个三针串行线调试（SWD）头。但是，Pico H 将其拆分为一个小的，带有键的 3 针连接器，而 Pico 则有三个铸造过孔引脚，靠近板的边缘。 

### 引脚分配和设计文件

![pico pinout](https://www.raspberrypi.com/documentation/microcontrollers/images/pico-pinout.svg)

* 下载引脚图（PDF）
* 下载设计文件（Cadence Allegro）
* 下载 STEP 文件
* 下载用于树莓派 Pico 的 Fritzing 部件
* 下载树莓派 Pico H 的 Fritzing 部件

>**注意**
>
>有关 Fritzing 的更多信息，请访问 fritzing.org 网站。 |

树莓派 Pico W 和 Pico WH

树莓派 Pico W 添加了内置的单频 2.4GHz 无线接口（802.11n），使用 Infineon CYW43439，同时保留了 Pico 的外形因素。内置的 2.4GHz 无线接口具有以下功能：

* 无线（802.11n），单频（2.4 GHz）
* WPA3
* 支持最多四个客户端的软接入点
* 蓝牙 5.2
  * 支持蓝牙 LE 中心和外围角色
  * 支持蓝牙经典

天线是一款授权自 ABRACON（前身为 ProAnt）的板载天线。 无线接口通过 SPI 连接到 RP2040 微控制器。

由于引脚限制，一些无线接口引脚是共享的。 CLK 与 VSYS 监视器共享，因此只有在没有 SPI 事务正在进行时，才能通过 ADC 读取 VSYS。 Infineon CYW43439 DIN/DOUT 和 IRQ 都共享 RP2040 上的一个引脚。 只有在没有 SPI 事务正在进行时，才适合检查 IRQ。 该接口通常以 33MHz 运行。

为获得最佳无线性能，天线应放置在自由空间中。例如，在天线下方或附近放置金属会降低其增益和带宽性能。在天线两侧添加接地金属可以提高天线的带宽。

>**注意**
>
>CYW43439 无线芯片通过 SPI 连接到 RP2040。CYW43439 支持通过此接口的 802.11 无线和蓝牙。 

>**重要**
>
>默认情况下， libcyw43 获得非商业使用许可，但 Pico W 用户以及任何围绕 RP2040 和 CYW43439 构建其产品的用户都可以获得免费的商业使用许可。

>**重要**
>
> 除了标准的 BTstack 许可条款外，还提供了一份补充许可，涵盖了在树莓派 Pico W 或树莓派 Pico WH 上商业使用 BTstack 的内容。
### 引脚分配和设计文件

![picow pinout](https://www.raspberrypi.com/documentation/microcontrollers/images/picow-pinout.svg)

* 下载引脚分配图（PDF）
* 下载设计文件（Cadence Allegro）
* 下载 STEP 文件
* 下载适用于树莓派 Pico W 的 Fritzing 部件

## 文档


适用于树莓派 Pico 和其他基于 RP2040 的板的文档。

### RP2040 设备

[ RP2040 数据表](https://datasheets.raspberrypi.com/rp2040/rp2040-datasheet.pdf)

树莓派的微控制器

[使用 RP2040 进行硬件设计](https://datasheets.raspberrypi.com/rp2040/hardware-design-with-rp2040.pdf)

使用 RP2040 微控制器构建板和产品

### 树莓派 Pico

[树莓派 Pico 数据表](https://datasheets.raspberrypi.com/pico/pico-datasheet.pdf)

基于 RP2040 的微控制器板

[使用树莓派 Pico 入门](https://datasheets.raspberrypi.com/pico/getting-started-with-pico.pdf)

使用树莓派 Pico 和其他基于 RP2040 的微控制器开发 C/C++

### 树莓派 Pico W

[Raspberry Pi Pico W 数据表](https://datasheets.raspberrypi.com/picow/pico-w-datasheet.pdf)

使用基于 RP2040 的微控制器板进行无线连接

[使用树莓派 Pico W 连接互联网](https://datasheets.raspberrypi.com/picow/connecting-to-the-internet-with-pico-w.pdf)

使用 C/C++或 MicroPython 让树莓派 Pico W 联机

>**注意**
>
>在《使用 C/C++ 或 MicroPython 在树莓派 Pico W 上使用 Wi-Fi 和蓝牙》一书中介绍了如何在树莓派 Pico W 上连接互联网。 

### 软件开发

[Raspberry Pi Pico C/C++ SDK](https://datasheets.raspberrypi.com/pico/raspberry-pi-pico-c-sdk.pdf)

用于在 RP2040 微控制器上进行 C/C++开发的库和工具

[树莓派 Pico Python SDK](https://datasheets.raspberrypi.com/pico/raspberry-pi-pico-python-sdk.pdf)

用于 RP2040 微控制器的 MicroPython 环境

Raspberry Pi Pico C/C++ SDK 的 API 级别 Doxygen 文档也可作为微型站点使用。

>**注意**
>
>适用于 Windows 10 和 Windows 11 的 Pico C/C++ SDK 一键安装程序已经准备就绪。 

## 软件实用工具

### 你的 Pico 上有什么？

如果您忘记了在您的树莓派 Pico 中编程的内容，并且该程序是使用我们的 Pico C/C++ SDK 构建的，通常会将名称和其他有用信息嵌入到二进制文件中。您可以使用 Picotool 命令行实用程序查找这些详细信息。如何使用 Picotool 执行此操作的完整说明可在我们的“入门”文档中找到。

* 转到 Picotool Github 存储库。

### 使用另一个树莓派 Pico 进行调试

您可以使用一个树莓派 Pico 来调试另一个 Pico。这是通过 debugprobe 实现的，该应用程序允许 Pico 充当 USB → SWD 和 UART 转换器。

您可以在 debugprobe GitHub 存储库中找到固件的最新版本。

从最新版本下载 debugprobe_on_pico.uf2 。

在将调试器 Pico 插入计算机时，按住 BOOTSEL 按钮以挂载名为 "RPI-RP2" 的卷。

将 debugprobe_on_pico.uf2 复制到卷上。文件复制到设备后，卷将自动卸载。

您的 Pico 将重新启动，现在运行更新版本的 debugprobe 固件。现在可以进行调试。

>**技巧**
>
>有关如何使用调试器的说明，请参阅《Pico 入门指南》。 
