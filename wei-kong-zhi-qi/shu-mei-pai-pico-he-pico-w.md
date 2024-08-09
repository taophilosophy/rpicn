# Pico 系列微控制器

Pico 系列设备根据产品代次划分**系列**。

第一代树莓派 Pico 系列被称为 Pico（或 Pico 1），包含四个型号：

- 树莓派 Pico
- 树莓派 Pico H
- 树莓派 Pico W
- 树莓派 Pico WH

第二代树莓派 Pico 系列被称为 Pico 2，包含两个型号：

- 树莓派 Pico 2
  - 带有插针的树莓派 Pico 2

## Pico 2 系列

![Pico 2](https://www.raspberrypi.com/documentation/microcontrollers/images/pico-2.png?hash=c4b2ccf2504c98fdd111405dd95346b5)

树莓派 Pico 2 系列包含两款开发板：树莓派 Pico 2 和带有插针的树莓派 Pico 2。

### 树莓派 Pico 2

树莓派 Pico 2 是一款低成本、高性能的微控制器开发板，具有灵活的数字接口。主要特点包括：

- 由 Raspberry Pi 在英国设计的 [RP2350](https://www.raspberrypi.com/documentation/microcontrollers/silicon.html#rp2350) 微控制器芯片
- 双核 Cortex-M33、或双核 Hazard3 处理器，最高可达 150MHz
- 520KB 的 SRAM 和 4MB 的板载闪存
- 带设备模式和主机模式支持的 USB 1.1
- 低功耗睡眠和休眠模式
- 通过 USB 大容量存储拖放编程
- 多功能 GPIO 引脚 ×26，其中 3 个可用于 ADC
- SPI ×2，I²C ×2，UART ×2，12 位 500ksps 模拟到数字转换器 (ADC) ×3，可控 PWM 通道 ×24
- 定时器 ×2，带 4 个报警，AON 定时器 ×1
- 温度传感器
- 3× 可编程 IO (PIO) 模块，总共 12 个状态机，支持自定义外围设备
  - 灵活、用户可编程的高速 IO
  - 可以模拟接口，如 SD 卡和 VGA

树莓派 Pico 2 采用镀边模块设计，便于直接焊接到载板上，而带有插针的 Pico 2 预装有插针。

>**注意**
>
>两款开发板均配备三针串行线调试 (SWD) 插针。然而，带有插针的 Pico 2 使用的是小型、带定位的 [3 针连接器](https://datasheets.raspberrypi.com/debug/debug-connector-specification.pdf)，而 Pico 2 则是板边相邻的三个镀边通孔插针。 

### 引脚分布图和设计文件

![Pico 2 R4 引脚分布图](https://www.raspberrypi.com/documentation/microcontrollers/images/pico-2-r4-pinout.svg)

- 下载 [引脚分布图](https://datasheets.raspberrypi.com/pico/Pico-2-Pinout.pdf) (PDF)
- 下载 [设计文件](https://datasheets.raspberrypi.com/pico/RPi-Pico-2-PUBLIC-20240708.zip) (Cadence Allegro)
- 下载 [STEP 文件](https://datasheets.raspberrypi.com/pico/Pico-2-step-20240708.zip)
- 下载树莓派 Pico 的 [Fritzing 部件](https://datasheets.raspberrypi.com/pico/Pico-2-Fritzing-20240708.fzpz)

>**注意**
>
>关于 Fritzing 的更多信息，请访问网站 [fritzing.org](https://fritzing.org/) 。 
## Pico 1 系列

![Pico 1 系列](https://www.raspberrypi.com/documentation/microcontrollers/images/pico-1s.png?hash=37f90d0137e81859630d4f0943b6f3d5)

树莓派 Pico 1 系列包含四款开发板：树莓派 Pico（最左侧），Pico H（左中），Pico W（右中），Pico WH（最右侧）。

### 树莓派 Pico 和 Pico H

树莓派 Pico 是一款低成本、高性能的微控制器开发板，具有灵活的数字接口。主要特点包括：

- 由 Raspberry Pi 在英国设计的 [RP2040](https://www.raspberrypi.com/documentation/microcontrollers/silicon.html#rp2040) 微控制器芯片
- 双核 Arm Cortex M0+ 处理器，灵活的时钟频率最高可达 133 MHz
- SRAM 为 264KB，板载闪存 2MB
- 带设备模式和主机模式支持的 USB 1.1
- 低功耗睡眠和休眠模式
- 通过 USB 大容量存储拖放编程
- 多功能 GPIO 引脚 ×26
- SPI ×2，I²C ×2，串口 ×2，3× 12 位 ADC，可控 PWM 通道 ×2
- 精确的片上时钟和定时器
- 温度传感器
- 片上加速浮点库
- 可编程 IO (PIO) 状态机 ×8，支持自定义外围设备

树莓派 Pico 采用镀边模块设计，便于直接焊接到载板上，而 Pico H 则预装有插针。

>**注意**
>
>两款开发板均配备三针串行线调试 (SWD) 插针。然而，Pico H 使用的是小型、带定位的 [3 针连接器](https://datasheets.raspberrypi.com/debug/debug-connector-specification.pdf)，而 Pico 则是板边相邻的三个镀边通孔插针。

#### 引脚分布图和设计文件

![Pico 引脚分布图](https://www.raspberrypi.com/documentation/microcontrollers/images/pico-pinout.svg)

- 下载 [引脚分布图](https://datasheets.raspberrypi.com/pico/Pico-R3-A4-Pinout.pdf) (PDF)
- 下载 [设计文件](https://datasheets.raspberrypi.com/pico/RPi-Pico-R3-PUBLIC-20200119.zip) (Cadence Allegro)
- 下载 [STEP 文件](https://datasheets.raspberrypi.com/pico/Pico-R3-step.zip)
- 下载树莓派 Pico 的 [Fritzing 部件](https://datasheets.raspberrypi.com/pico/Pico-R3-Fritzing.fzpz)
- 下载树莓派 Pico H 的 [Fritzing 部件](https://datasheets.raspberrypi.com/pico/PicoH-Fritzing.fzpz)

>**注意**
>
>关于 Fritzing 的更多信息，请访问网站 [fritzing.org](https://fritzing.org/) 。


### 树莓派 Pico W 和 Pico WH

树莓派 Pico W 在保持 Pico 外形尺寸的同时，增加了板载单频 2.4GHz 无线接口（802.11n），该接口采用 Infineon CYW43439 芯片。板载的 2.4GHz 无线接口具有以下特性：

* 无线（802.11n），单频（2.4 GHz）
* WPA3 安全协议
* 支持最多四个客户端的软接入点
* 蓝牙 5.2
  * 支持蓝牙低功耗（LE）中央和外围角色
  * 支持经典蓝牙

天线为板载天线，由 ABRACON（前身为 ProAnt）授权。无线接口通过 SPI 连接到 [RP2040](https://www.raspberrypi.com/documentation/microcontrollers/silicon.html#rp2040) 微控制器。

由于引脚限制，部分无线接口的引脚是共享的。时钟信号（CLK）与 VSYS 监视器共享，因此只有在没有 SPI 事务进行时，才能通过 ADC 读取 VSYS。Infineon CYW43439 的 DIN/DOUT 和 IRQ 引脚都与 RP2040 上的一个引脚共享。仅在没有 SPI 事务进行时，才适合检查 IRQ。该接口通常以 33MHz 运行。

为了获得最佳的无线性能，天线应处于空旷空间。例如，在天线下方或附近放置金属会降低其增益和带宽性能。将接地金属添加到天线两侧可以改善天线的带宽。

>**注意**
>
>CYW43439 无线芯片通过 SPI 连接到 RP2040。CYW43439 支持通过此接口进行 802.11 无线和蓝牙通信。 

>**重要**
>
>一般情况下，`libcyw43` 仅授权用于非商业用途，但 Pico W 用户以及任何其他围绕 RP2040 和 CYW43439 构建其产品的用户都可以享受免费的[商业使用许可证](https://github.com/georgerobotics/cyw43-driver/blob/195dfcc10bb6f379e3dea45147590db2203d3c7b/LICENSE.RP)。 

>**重要**
>
>除了 [BTstack 标准许可](https://github.com/bluekitchen/btstack/blob/master/LICENSE)条款外，还提供了一个 [补充许可](https://github.com/raspberrypi/pico-sdk/blob/master/src/rp2_common/pico_btstack/LICENSE.RP)，涵盖了树莓派 Pico W 或树莓派 Pico WH 商业使用 BTstack 的情况。 

#### 引脚图和设计文件

![picow 引脚图](https://www.raspberrypi.com/documentation/microcontrollers/images/picow-pinout.svg)

* 下载 [引脚图](https://datasheets.raspberrypi.com/picow/PicoW-A4-Pinout.pdf) (PDF)
* 下载 [设计文件](https://datasheets.raspberrypi.com/picow/RPi-PicoW-PUBLIC-20220607.zip) (Cadence Allegro)
* 下载 [STEP 文件](https://datasheets.raspberrypi.com/picow/PicoW-step.zip)
* 下载适用于树莓派 Pico W 的 [Fritzing 部件](https://datasheets.raspberrypi.com/picow/PicoW-Fritzing.fzpz)

## 文档

Pico 系列及其他基于 Raspberry Pi 微控制器的板卡文档。

### RP2350

[RP2350 数据手册](https://datasheets.raspberrypi.com/rp2350/rp2350-datasheet.pdf)

Raspberry Pi 的微控制器

[使用 RP2350 进行硬件设计](https://datasheets.raspberrypi.com/rp2350/hardware-design-with-rp2350.pdf)

使用 RP2350 微控制器构建板卡和产品

### RP2040

[RP2040 数据手册](https://datasheets.raspberrypi.com/rp2040/rp2040-datasheet.pdf)

Raspberry Pi 的微控制器

[使用 RP2040 进行硬件设计](https://datasheets.raspberrypi.com/rp2040/hardware-design-with-rp2040.pdf)

使用 RP2040 微控制器构建板卡和产品

### 树莓派 Pico 2

[树莓派 Pico 2 数据手册](https://datasheets.raspberrypi.com/pico/pico-2-datasheet.pdf)

基于 RP2350 的微控制器板

[入门指南：使用树莓派 Pico 系列微控制器](https://datasheets.raspberrypi.com/pico/getting-started-with-pico.pdf)

使用树莓派 Pico 系列设备及其他基于 Raspberry Pi 微控制器的板卡进行 C/C++ 开发

### 树莓派 Pico

[树莓派 Pico 数据手册](https://datasheets.raspberrypi.com/pico/pico-datasheet.pdf)

基于 RP2040 的微控制器板

[入门指南：使用树莓派 Pico](https://datasheets.raspberrypi.com/pico/getting-started-with-pico.pdf)

使用树莓派 Pico 及其他基于 RP2040 的微控制器板进行 C/C++ 开发

### 树莓派 Pico W

[树莓派 Pico W 数据手册](https://datasheets.raspberrypi.com/picow/pico-w-datasheet.pdf)

带无线功能的 RP2040 微控制器板

[使用树莓派 Pico W 连接互联网](https://datasheets.raspberrypi.com/picow/connecting-to-the-internet-with-pico-w.pdf)

使用 C/C++ 或 MicroPython 让树莓派 Pico W 上网

>**注意**
>
>在 [使用树莓派 Pico W 连接互联网](https://datasheets.raspberrypi.com/picow/connecting-to-the-internet-with-pico-w.pdf)一书中介绍了使用 C/C++ 或 MicroPython 进行 Wi-Fi 和蓝牙开发的文档。


### 软件开发

[树莓派 Pico C/C++ SDK](https://datasheets.raspberrypi.com/pico/raspberry-pi-pico-c-sdk.pdf)

用于在 RP2040 微控制器上进行 C/C++ 开发的库和工具

[树莓派 Pico Python SDK](https://datasheets.raspberrypi.com/pico/raspberry-pi-pico-python-sdk.pdf)

用于 RP2040 微控制器的 MicroPython 环境

树莓派 Pico C/C++ SDK 的 API 级 Doxygen 文档也可以通过 [微型站点](https://rptl.io/pico-doxygen) 获取。

>**注意**
>
>提供了一个适用于 Windows 10 和 Windows 11 的 Pico C/C++ SDK [一键安装程序](https://github.com/raspberrypi/pico-setup-windows/releases/latest/download/pico-setup-windows-x64-standalone.exe)。 

## 软件工具

### 如何查看 Pico 系列设备上的内容？

如果您不确定树莓派 Pico 系列设备上编写了什么程序，并且该程序是使用 Pico C/C++ SDK 构建的，通常会在二进制文件中嵌入一个名称和其他有用信息。您可以使用 [Picotool](https://github.com/raspberrypi/picotool) 命令行工具来查找这些详细信息。关于如何使用 Picotool 的完整说明可在我们的 '[入门指南](https://datasheets.raspberrypi.com/pico/getting-started-with-pico.pdf)' 文档中找到。

* 前往 [Picotool 的 GitHub 仓库](https://github.com/raspberrypi/picotool)。

### 使用另一台 Pico 系列设备进行调试

>**注意**
>
> `debuprobe_on_pico` 调试软件尚不支持 Pico 2。

您可以使用一台 Pico 系列设备来调试另一台 Pico 系列设备。这可以通过 `debugprobe` 实现，`debugprobe` 是一个允许 Pico 充当 USB → SWD 和 UART 转换器的应用程序。

您可以在 [debugprobe GitHub 仓库](https://github.com/raspberrypi/debugprobe/releases/latest) 中找到最新版本的固件。

下载最新发布的 `debugprobe_on_pico.uf2` 文件。

按住 BOOTSEL 按钮并将调试设备插入计算机，以挂载名为“RPI-RP2”的卷。

将 `debugprobe_on_pico.uf2` 复制到该卷上。文件复制完成后，卷会自动卸载。

您的设备将重启，并运行更新版本的 `debugprobe` 固件。现在它已准备好进行调试。

>**注意**
>
>有关如何使用调试器的说明，请参见 [Pico 系列微控制器入门指南](https://datasheets.raspberrypi.com/pico/getting-started-with-pico.pdf)。


### 重置 Flash 内存

Pico 的 BOOTSEL 模式存储在 RP2040 芯片的只读内存中，无法意外覆盖。无论如何，只要按住 BOOTSEL 按钮并插入 Pico，它都会显示为一个驱动器，您可以将新的 UF2 文件拖放到该驱动器上。通过软件无法将板卡刷砖。但是，在某些情况下，您可能希望确保 Flash 内存为空。您可以通过在 Pico 处于大容量存储模式时拖放一个特殊的 UF2 二进制文件来完成此操作。

* 下载 [UF2 文件](https://datasheets.raspberrypi.com/soft/flash_nuke.uf2)
* 查看 [GitHub 上的代码](https://github.com/raspberrypi/pico-examples/blob/master/flash/nuke/nuke.c)
