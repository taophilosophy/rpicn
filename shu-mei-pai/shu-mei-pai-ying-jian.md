# 树莓派硬件


## GPIO 和 40 针排针

树莓派的一个强大功能是主板的顶部沿着一排 GPIO（通用输入/输出）引脚。当前所有树莓派主板上都有一个 40 针的 GPIO 引脚排针（尽管在树莓派 Zero、树莓派 Zero W 和树莓派 Zero 2 W 上是未焊接的）。所有主板上的 GPIO 引脚的引脚间距都是 0.1 英寸（2.54 毫米）。

![GPIO pins](https://www.raspberrypi.com/documentation/computers/images/GPIO-Pinout-Diagram-2.png)

所有 GPIO 引脚都可以在软件中指定为输入或输出引脚，并用于各种用途。

![GPIO layout](../.gitbook/assets/GPIO.png)

>**注意**
>
>GPIO 引脚编号方案不按数字顺序排列。 GPIO 引脚 0 和 1 位于板上（物理引脚 27 和 28），但保留供高级使用。

### 电压

板上有两个 5V 引脚和两个 3.3V 引脚，以及若干接地引脚（GND），这些引脚无法重新配置。其余引脚均为通用 3.3V 引脚，意味着输出设置为 3.3V，输入为 3.3V 容忍。

### 输出

指定为输出引脚的 GPIO 引脚可以设置为高电平（3.3V）或低电平（0V）。

### 输入

将作为输入引脚指定的 GPIO 引脚可以读取为高电平（3.3V）或低电平（0V）。使用内部上拉或下拉电阻可以更容易地实现这一点。GPIO2 和 GPIO3 引脚具有固定的上拉电阻，但对于其他引脚，可以在软件中进行配置。

### 其他 GPIO 功能

除了简单的输入和输出设备外，GPIO 引脚还可以与各种替代功能一起使用。一些功能适用于所有引脚，另一些适用于特定引脚：

* 脉冲宽度调制（PWM）

  * 所有引脚上都可用的软件 PWM
  * GPIO12、GPIO13、GPIO18、GPIO19 上可用的硬件 PWM
* SPI
  * SPI0：MOSI（GPIO10）；MISO（GPIO9）；SCLK（GPIO11）；CE0（GPIO8），CE1（GPIO7）
  * SPI1：MOSI（GPIO20）；MISO（GPIO19）；SCLK（GPIO21）；CE0（GPIO18）；CE1（GPIO17）；CE2（GPIO16）
* I2C
  * 数据：（GPIO2）；时钟（GPIO3）
  * EEPROM 数据：（GPIO0）；EEPROM 时钟（GPIO1）
* 串行
  * TX（GPIO14）; RX（GPIO15）

### 查看树莓派的 GPIO 引脚布局

通过打开终端窗口并运行命令 pinout ，可以在您的树莓派上访问 GPIO 参考。此工具由 GPIO Zero Python 库提供，在 Raspberry Pi OS 中默认安装。

>**警告**
>
>尽管连接简单的组件到 GPIO 引脚是安全的，但要小心如何连接它们。LED 应该有电阻器来限制通过它们的电流。不要为 3.3V 组件使用 5V。不要直接把电机连接到 GPIO 引脚，而应使用 H 桥电路或电机控制板。 

### 权限

为了使用 GPIO，您的用户必须是 gpio 组的成员。默认用户帐户默认是成员，但您必须使用以下命令手动添加其他用户：

```
$ sudo usermod -a -G gpio <username>
```

### Python 中的 GPIO

使用 GPIO Zero 库可以轻松使用 Python 控制 GPIO 设备。该库在 gpiozero.readthedocs.io 上有全面的文档。

#### LED

以下示例代码控制连接到 GPIO17 的 LED：

```
from gpiozero import LED
from time import sleep

led = LED(17)

while True:
    led.on()
    sleep(1)
    led.off()
    sleep(1)
```

在类似 Thonny 的 IDE 中运行此代码，LED 将会重复闪烁。

LED 方法包括 on() 、 off() 、 toggle() 和 blink() 。

#### 按钮

以下示例代码读取连接到 GPIO2 的按钮的状态：

```
from gpiozero import Button
from time import sleep

button = Button(2)

while True:
    if button.is_pressed:
        print("Pressed")
    else:
        print("Released")
    sleep(1)
```

按钮功能包括属性 is_pressed 和 is_held ；回调 when_pressed ， when_released 和 when_held ；以及方法 wait_for_press() 和 wait_for_release 。

#### 按钮和 LED

以下示例代码读取连接到 GPIO2 的按钮的状态，并在按下按钮时点亮连接到 GPIO17 的 LED。

```
from gpiozero import LED, Button

led = LED(17)
button = Button(2)

while True:
    if button.is_pressed:
        led.on()
    else:
        led.off()
```

 或者：

```
from gpiozero import LED, Button

led = LED(17)
button = Button(2)

while True:
    button.wait_for_press()
    led.on()
    button.wait_for_release()
    led.off()
```

 或：

```
from gpiozero import LED, Button

led = LED(17)
button = Button(2)

button.when_pressed = led.on
button.when_released = led.off
```

#### 深入探讨

![](https://www.raspberrypi.com/documentation/computers/images/simple-electronics-with-gpio-zero.jpg)[https://github.com/raspberrypipress/released-pdfs/raw/main/simple-electronics-with-gpio-zero.pdf](https://github.com/raspberrypipress/released-pdfs/raw/main/simple-electronics-with-gpio-zero.pdf)

您可以在 Raspberry Pi Press 的《使用 GPIO Zero Python 库的简单电子学》一书中找到有关如何使用 GPIO Zero Python 库编程连接到您树莓派的更多信息。该书将带您开始使用 GPIO Zero 库，并通过构建一系列项目来指导您如何使用它。

您可以免费下载这本书的 PDF 文件，它已根据知识共享署名-非商业性使用-相同方式共享 3.0 未本地化版本（CC BY NC-SA）许可发布。

## 框图和机械图纸

各种树莓派开发板版本的原理图：

### 树莓派 5

* [机械图，PDF](https://datasheets.raspberrypi.com/rpi5/raspberry-pi-5-mechanical-drawing.pdf)
* 树莓派 5 的 STEP 文件

### 树莓派 4 Model B

* [4.0 版本的原理图](https://datasheets.raspberrypi.com/rpi4/raspberry-pi-4-reduced-schematics.pdf)
* [机械图纸，PDF](https://datasheets.raspberrypi.com/rpi4/raspberry-pi-4-mechanical-drawing.pdf)
* [机械图纸，DXF](https://datasheets.raspberrypi.com/rpi4/raspberry-pi-4-mechanical-drawing.dxf)

### 树莓派 3 Model B+

* [原理图，版本 1.0](https://datasheets.raspberrypi.com/rpi3/raspberry-pi-3-b-plus-reduced-schematics.pdf)
* [机械图纸，PDF](https://datasheets.raspberrypi.com/rpi3/raspberry-pi-3-b-plus-mechanical-drawing.pdf)
* [机械图纸，DXF](https://datasheets.raspberrypi.com/rpi3/raspberry-pi-3-b-plus-mechanical-drawing.dxf)
* [ 案例图，PDF](https://datasheets.raspberrypi.com/case/raspberry-pi-3-b-plus-case-mechanical-drawing.pdf)

### 树莓派 3 Model B

* [电路图，修订版 1.2](https://datasheets.raspberrypi.com/rpi3/raspberry-pi-3-b-reduced-schematics.pdf)
* [机械图纸，PDF](https://datasheets.raspberrypi.com/rpi3/raspberry-pi-3-b-mechanical-drawing.pdf)
* [机械图纸，DXF](https://datasheets.raspberrypi.com/rpi3/raspberry-pi-3-b-mechanical-drawing.dxf)

### 树莓派 2 Model B

* [电路图，版本 1.2](https://datasheets.raspberrypi.com/rpi2/raspberry-pi-2-b-reduced-schematics.pdf)

### 树莓派 1 Model B+

* [电路图，版本 1.2](https://datasheets.raspberrypi.com/rpi/raspberry-pi-b-plus-reduced-schematics.pdf)
* [机械图纸，PDF](https://datasheets.raspberrypi.com/rpi/raspberry-pi-b-plus-mecahnical-drawing.pdf)
* [机械图纸，DXF](https://datasheets.raspberrypi.com/rpi/raspberry-pi-b-plus-mecahnical-drawing.dxf)

### 树莓派 3 Model A+

* [原理图，修订版 1.0](https://datasheets.raspberrypi.com/rpi3/raspberry-pi-3-a-plus-reduced-schematics.pdf)
* [机械图纸，PDF](https://datasheets.raspberrypi.com/rpi3/raspberry-pi-3-a-plus-mechanical-drawing.pdf)
* [ 机箱图纸，PDF](https://datasheets.raspberrypi.com/case/raspberry-pi-3-a-plus-case-mechanical-drawing.pdf)

>**注意**
>
>树莓派 3 Model A+ 的机械图也适用于树莓派 1 Model A+。 

### 树莓派 1 Model A+

* [电路图，版本 1.1](https://datasheets.raspberrypi.com/rpi/raspberry-pi-a-plus-reduced-schematics.pdf)

### 树莓派 Zero

* [电路图，版本 1.3](https://datasheets.raspberrypi.com/rpizero/raspberry-pi-zero-reduced-schematics.pdf)
* [机械图纸，PDF](https://datasheets.raspberrypi.com/rpizero/raspberry-pi-zero-mechanical-drawing.pdf)
* [盒子图纸，PDF - 空盖](https://datasheets.raspberrypi.com/case/raspberry-pi-zero-case-mechanical-drawing.pdf)
* [盒子图纸，PDF - GPIO 盖](https://datasheets.raspberrypi.com/case/raspberry-pi-zero-case-with-gpio-mechanical-drawing.pdf)
* [盒子图纸，PDF - 摄像头盖](https://datasheets.raspberrypi.com/case/raspberry-pi-zero-case-with-camera-mechanical-drawing.pdf)

### 树莓派 Zero W

* [电路图，版本 1.1](https://datasheets.raspberrypi.com/rpizero/raspberry-pi-zero-w-reduced-schematics.pdf)
* [机械图纸，PDF](https://datasheets.raspberrypi.com/rpizero/raspberry-pi-zero-w-mechanical-drawing.pdf)

### 树莓派 Zero 2 W

* [ 电路图](https://datasheets.raspberrypi.com/rpizero2/raspberry-pi-zero-2-w-reduced-schematics.pdf)
* [机械图纸，PDF](https://datasheets.raspberrypi.com/rpizero2/raspberry-pi-zero-2-w-mechanical-drawing.pdf)
* [ 测试垫位置](https://datasheets.raspberrypi.com/rpizero2/raspberry-pi-zero-2-w-test-pads.pdf)

#### 测试垫位置

树莓派 Zero 2 W 在生产过程中使用了许多测试垫位置。

![zero2 pad diagram](https://www.raspberrypi.com/documentation/computers/images/zero2-pad-diagram.png)

| 标签       | 功能                        | X（距原点的毫米） | 原点处的 Y（毫米） |
| ------------ | ----------------------------- | ------------------- | -------------------- |
| STATUS_LED | LED 的电源状态（低 = 开启） | 5.15              | 8.8                |
| CORE       | 处理器电源                  | 6.3               | 18.98              |
| RUN        | 连接到 GND 以复位           | 8.37              | 22.69              |
| 5V         | 5V 输入                     | 8.75              | 11.05              |
| 5V         | 5V 输入                     | 11.21             | 6.3                |
| GND        | 地线引脚                    | 10.9              | 3.69               |
| GND        | 地线引脚                    | 17.29             | 2.41               |
| USB_DP     | USB 端口                    | 22.55             | 1.92               |
| USB_DM     | USB 端口                    | 24.68             | 1.92               |
| OTG        | 在路上 ID 引脚              | 39.9              | 7.42               |
| 1V8        | 1.8V 模拟供电               | 42.03             | 8.42               |
| TV         | 复合电视输出                | 45.58             | 3.17               |
| GND        | 地针                        | 49.38             | 3.05               |
| GND        | 地针                        | 55.99             | 22.87              |
| 3V3        | 3.3V I/O 供应               | 48.55             | 22.44              |
| SD_CLK     | SD 卡时钟引脚               | 60.95             | 18.45              |
| SD_CMD     | SD 卡命令引脚               | 58.2              | 16.42              |
| SD_DAT0    | SD 数据引脚                 | 58.13             | 20.42              |
| SD_DAT1    | SD 数据引脚                 | 60.65             | 21.1               |
| SD_DAT2    | SD 数据引脚                 | 57.78             | 13.57              |
| SD_DAT3    | SD 数据引脚                 | 60.8              | 15.22              |
| BT_ON      | 蓝牙电源状态                | 25.13             | 19.55              |
| WL_ON      | 无线局域网电源状态          | 27.7              | 19.2               |

## 产品合规性和安全性

所有的树莓派产品均经过了广泛的合规性测试。有关更多信息，请参阅产品信息门户。

### 燃烧性评级

树莓派设备中使用的 PCB 符合 UL94-V0 标准。


>**注意**
>
>仅适用于 PCB。 

### 树莓派合规支持

旧版支持计划旨在消除导航合规问题的负担，使公司更容易将新产品带给消费者。它提供了访问与我们的树莓派在合规测试期间合作的相同测试工程师的机会，将用户连接到 UL 的专门团队，他们通过对树莓派的深入了解来评估和测试用户的产品。

了解更多关于树莓派合规支持计划。

### 由树莓派提供支持

由树莓派提供支持的 Powered by Raspberry Pi 计划为希望使用 Raspberry Pi 标志形式的公司提供流程，涵盖搭载树莓派计算机或芯片的产品，以及由树莓派提供的服务。如果您希望开始申请流程，可以在线进行。

### 已批准的设计合作伙伴

我们的已批准设计合作伙伴名单提供了一组我们与之密切合作并支持的咨询公司，以便它们可以在硬件、软件和机械领域提供付费设计服务。

## 频率管理和热控制

所有型号的树莓派在高负荷情况下都会执行一定程度的热管理，以避免过热。SoC 具有内部温度传感器，GPU 上的软件会定期轮询以确保温度不超过我们设定的 85°C 的限制。可以将此值设置为较低的值，但不能设置提高此值。当设备接近极限时，芯片（Arm、GPU）上使用的各种频率和有时电压会降低。这样可以减少产生的热量，保持温度在可控范围内。

当核心温度在 80°C 和 85°C 之间时，Arm 核心将逐渐降速。如果温度达到 85°C，Arm 核心和 GPU 都将降速。

对于树莓派 3 Model B+，PCB 技术已经更改，以提供更好的散热和增加热量。此外，引入了软温度限制，旨在最大限度地延长设备在达到 85°C 的硬限制之前可以“冲刺”的时间。当达到软限制时，时钟速度从 1.4GHz 降低到 1.2GHz，并且操作电压略微降低。这减少了温度增加的速度：我们以 1.4GHz 的短暂时期换取了 1.2GHz 的较长时期。默认情况下，软限制为 60°C，可以通过 config.txt 中的 temp_soft_limit 设置进行更改。

树莓派4 Model B 采用与树莓派 3 Model B+ 相同的 PCB 技术，以帮助散热。目前尚未定义软限制。

### 使用 DVFS

>**注意**
>
>仅适用于树莓派 4 Model B、树莓派 400 和计算模块 4 的 DVFS 讨论。 

树莓派 4 设备实现动态电压和频率调节（DVFS）。这种技术使树莓派 4 设备能够在提供相同性能的同时以更低的温度运行。

SoC 内部的各种时钟（例如 Arm、Core、V3D、ISP、H264、HEVC）由固件监视，每当它们未以全速运行时，供应给由时钟驱动的芯片特定部分的电压会相对于全速降低。实际上，只提供足够的电压以使块在其运行的特定速度下正确运行。这可能导致 SoC 使用的功率大幅减少，从而减少总体产生的热量。

由于在运行欠电压时可能涉及与使用欠电压固定时钟外设（例如 PCIe）相关的系统稳定性问题，因此有三种 DVFS 模式可供配置，在 /boot/firmware/config.txt 中具有以下属性。大多数系统应该使用 dvfs=3 ，无头系统可能会从 dvfs=1 的小功耗降低中受益，但存在 PCIe 稳定性问题的风险。

| 属性=值 | 说明                                                                                                                    |
| --------- | -------------------------------------------------------------------------------------------------------------------------- |
| dvfs=1  | 允许降压                                                                                                                 |
| dvfs=2  | 默认操作频率的固定电压                                                                                                   |
| dvfs=3  | 根据需求增加电压以进行超频（默认）。如果 over_voltage 在 config.txt 中指定，则禁用动态电压调节，导致系统恢复到 dvfs=2 。 |

>**注意**
>
>该设置已在树莓派 5 上移除，实际上始终处于模式 3。 

另外，还使用了更加分级的 CPU 调度程序来更精细地控制 ARM 核频率，这意味着 DVFS 更加有效。现在的步长为 1500MHz、1000MHz、750MHz 和 600MHz。这些步骤在 SoC 被限制时也会有帮助，意味着很少会出现一直降至 600MHz 的限制，从而在完全负载性能上有所提升。

默认的 CPU 调度程序是 ondemand 。可以使用 cpufreq-set 命令（来自 cpufrequtils 软件包）手动更改调度程序以减少空闲功耗：

```
 sudo apt install cpufrequtils
 sudo cpufreq-set -g powersave
```

### 测量温度

由于树莓派设备上使用的 SoC 架构，以及树莓派 OS 发行版中使用的上游温度监控代码，基于 Linux 的温度测量可能不准确。然而， vcgencmd 命令提供了当前 SoC 温度的准确和即时读数，因为它直接与 GPU 通信：

```
 vcgencmd measure_temp
```

### 添加散热片

由于内置节流，不需要散热片来防止 SoC 过热损坏。但是，散热片或小风扇可以减少热节流并提高性能。将树莓派垂直安装以获得最佳气流，从而略微改善散热。

### 风扇外壳

树莓派 5 有两种官方风扇选项可用于辅助冷却：

* [ 主动散热器](https://www.raspberrypi.com/products/active-cooler/)
* [树莓派 5 机箱](https://www.raspberrypi.com/products/raspberry-pi-5-case/)

这两者都插入到板子右上角的四针 JST-SH PWM 风扇连接器中，位于 40 针 GPIO 引脚排线和 USB 2 端口之间。风扇连接器从与 USB 外设相同的电流限制中提取电流。我们建议超频者使用主动散热器机箱，因为它提供更好的散热性能。

可用的两个官方配件都由树莓派固件进行积极管理。随着树莓派的温度升高，风扇会做出以下反应：

* 在 50°C 以下，风扇根本不转动（0%速度）
* 在 50°C 时，风扇以低速运转（30%速度）
* 在 60°C 时，风扇速度增加到中速（50% 速度）
* 在 67.5°C 时，风扇速度增加到高速（70% 速度）
* 在 75°C 时，风扇速度增加到全速（100% 速度）

温度降低时，使用相同的映射，带有 5°C 的滞后；当温度降至以上阈值的每个下方 5°C 时，风扇速度降低。

在启动时，风扇会打开，并检查转速输入，以查看风扇是否在旋转。如果是，则启用 cooling_fan 设备树叠加。此叠加默认情况下位于 bcm2712-rpi-5-b.dtb ，但带有 status=disabled 。

#### 风扇连接器引脚分配

风扇连接器是一个 1mm 间距的 JST-SH 插座，包含以下四个引脚：

| 引脚 | 功能 | 电线颜色 |
| ------ | ------ | ---------- |
| 1    | +5V  | 红色     |
| 2    | PWM  | 蓝色     |
| 3    | GND  | 黑色     |
| 4    | 转速 | 黄色     |

## 树莓派引导 EEPROM

树莓派 5，树莓派 4，400，计算模块 4 和计算模块 4S 计算机使用 EEPROM 引导系统。树莓派计算机的所有其他型号使用位于引导文件系统中的 bootcode.bin 文件。

>**注意**
>
>您可以在 rpi-eeprom GitHub 存储库中找到用于创建 rpi-eeprom 的脚本和预编译的二进制文件。

### 启动诊断

如果在启动过程中发生错误，则将通过绿色 LED 显示错误代码。较新版本的引导加载程序将显示诊断消息，该消息将显示在两个 HDMI 显示器上。

### 更新引导程序

有多种方法可以更新您的树莓派的引导程序。

#### 树莓派 5，树莓派 4 和 树莓派 400

Raspberry Pi OS 会自动更新引导加载程序以进行重要的错误修复。手动更新引导加载程序或更改引导模式的推荐方法是使用 Raspberry Pi Imager 和 raspi-config。

#### 使用 Raspberry Pi Imager 更新引导加载程序

Raspberry Pi Imager 提供了一个 GUI，用于更新引导加载程序和选择引导模式。

* 下载 Raspberry Pi Imager
* 选择一个备用的 SD 卡（引导加载程序映像会覆盖整个卡）
* 启动 Raspberry Pi Imager
* 选择 Choose OS
* 选择 Misc utility images ![Select Misc utility images](https://www.raspberrypi.com/documentation/computers/images/misc-utility-images.png)
* 为您的树莓派版本选择 Bootloader （Pi 400 是 4 系列的一部分）![Choose a family for your bootloader](https://www.raspberrypi.com/documentation/computers/images/bootloader-family-select.png)
* 选择引导模式： SD （推荐）， USB 或 Network ![Choose the storage from which you’d like to boot](https://www.raspberrypi.com/documentation/computers/images/bootloader-storage-select.png)
* 选择 SD card 然后 Write
* 点击 Yes 继续
* 使用新镜像启动树莓派并等待至少十秒
* 当绿色活动 LED 以稳定的模式闪烁且 HDMI 显示器显示绿屏时，您已成功写入引导程序
* 关闭树莓派并取出 SD 卡

#### 使用 raspi-config 更新引导加载程序

要在 Raspberry Pi OS 内部更改引导模式或引导加载程序版本，请运行 raspi-config。

* 更新 Raspberry Pi OS 以获取 rpi-eeprom 软件包的最新版本
* 运行 sudo raspi-config
* 选择 Advanced Options
* 选择 Bootloader Version
* 选择 Default 以恢复出厂设置，或选择 Latest 以获取最新的引导加载程序版本。
* 重新启动

### 更新引导加载程序配置

default 版本的引导加载程序代表最新的出厂默认固件映像。它会更新以提供关键的错误修复，硬件支持，并在 latest 版本中经过测试后定期提供功能。 latest 引导加载程序更新更频繁，以包括最新的修复和改进。

高级用户可以切换到 latest 引导加载程序以获得最新功能。

打开命令提示符并启动 raspi-config 。

```
$ sudo raspi-config
```

转到 Advanced Options ，然后选择 Bootloader Version 。选择 Latest 并选择 Yes 以确认。选择 Finish 并确认要重新启动。重新启动后，再次打开命令提示符并更新您的系统：

```
$ sudo apt update
```

如果运行 sudo rpi-eeprom-update ，您会看到一个更新的引导加载程序版本可用，它是 latest 版本。

```
*** UPDATE AVAILABLE ***
BOOTLOADER: update available
   CURRENT: Thu 18 Jan 13:59:23 UTC 2024 (1705586363)
    LATEST: Mon 22 Jan 10:41:21 UTC 2024 (1705920081)
   RELEASE: latest (/lib/firmware/raspberrypi/bootloader-2711/latest)
            Use raspi-config to change the release.

  VL805_FW: Using bootloader EEPROM
     VL805: up to date
   CURRENT: 000138c0
    LATEST: 000138c0
```

现在您可以更新您的引导加载程序。

```
$ sudo rpi-eeprom-update -a
$ sudo reboot
```

重新启动，然后运行 sudo rpi-eeprom-update 。现在，您应该看到 CURRENT 日期已更新为引导加载程序的最新版本：

```
BOOTLOADER: up to date
   CURRENT: Mon 22 Jan 10:41:21 UTC 2024 (1705920081)
    LATEST: Mon 22 Jan 10:41:21 UTC 2024 (1705920081)
   RELEASE: latest (/lib/firmware/raspberrypi/bootloader-2711/latest)
            Use raspi-config to change the release.

  VL805_FW: Using bootloader EEPROM
     VL805: up to date
   CURRENT: 000138c0
    LATEST: 000138c0
```

#### 读取当前引导加载程序配置

要查看当前运行引导加载程序使用的配置，请运行：

* `rpi-eeprom-config`

#### 从引导加载程序映像中读取配置

从引导加载程序映像中读取配置：

```
$ rpi-eeprom-config pieeprom.bin
```

#### 编辑当前引导加载程序配置

以下命令将当前引导加载程序配置加载到文本编辑器中。当编辑器关闭时， rpi-eeprom-config 将更新后的配置应用于最新可用的引导加载程序版本，并使用 rpi-eeprom-update 在系统重新启动时安排更新：

```
$ sudo -E rpi-eeprom-config --edit
$ sudo reboot
```

如果更新后的配置相同或为空，则不会进行任何更改。

编辑器由环境变量 EDITOR 决定。

#### 应用已保存的配置

以下命令将 boot.conf 应用于最新可用的引导加载程序映像，并使用 rpi-eeprom-update 在系统重新启动时安排更新。

```
$ sudo rpi-eeprom-config --apply boot.conf
$ sudo reboot
```

### 自动更新

rpi-eeprom-update systemd 服务在启动时运行，并在有新镜像可用时应用更新，自动迁移当前的引导加载程序配置。

要禁用自动更新：

```
$ sudo systemctl mask rpi-eeprom-update
```

要重新启用自动更新：

```
$ sudo systemctl unmask rpi-eeprom-update
```

>**注意**
>
>如果设置了 FREEZE_VERSION bootloader 配置，则更新服务将跳过任何自动更新。这样可以避免在安装了多个操作系统或交换 SD 卡时需要逐个禁用更新服务。 

#### `rpi-eeprom-update`

Raspberry Pi OS 使用 rpi-eeprom-update 脚本来实现自动更新服务。该脚本也可以交互式运行，或者包装成自定义 bootloader 更新服务。

读取当前 bootloader 版本：

```
$ vcgencmd bootloader_version
```

检查是否有可用更新：

```
$ sudo rpi-eeprom-update
```

 安装更新：

```
$ sudo rpi-eeprom-update -a
$ sudo reboot
```

取消待定更新：

```
$ sudo rpi-eeprom-update -r
```

安装特定的引导加载程序映像：

```
$ sudo rpi-eeprom-update -d -f pieeprom.bin
```

参数 `-d` 指示 rpi-eeprom-update 使用指定的映像文件中的配置，而不是自动迁移当前配置。

显示内置文档：

```
$ rpi-eeprom-update -h
```

### 引导加载程序发布状态

固件发布状态对应于引导加载程序固件映像的特定子目录（ /lib/firmware/raspberrypi/bootloader/... ），可以更改以选择不同的发布流。

* default - 为新硬件支持、关键错误修复和通过 latest 发布测试的新功能的定期更新进行更新
* 当新功能可用时更新

由于发布状态字符串只是一个子目录名称，因此可以创建自己的发布流，例如固定的发布或自定义网络引导配置。

#### 更改引导加载程序版本

>**注意**
>
>您可以通过编辑 /etc/default/rpi-eeprom-update 文件并将 FIRMWARE_RELEASE_STATUS 条目更改为适当的流来更改更新期间要使用的发布流。 

#### 在引导加载程序映像文件中更新引导加载程序配置

以下命令将 pieeprom.bin 中的引导加载程序配置替换为 boot.conf ，并将新映像写入 new.bin ：

```
$ rpi-eeprom-config --config boot.conf --out new.bin pieeprom.bin
```

#### `recovery.bin`

在上电后，BCM2711 和 BCM2712 上的 ROM 会在 SD 卡的引导分区的根目录中查找名为 recovery.bin 的文件。如果找到有效的 recovery.bin ，则 ROM 会执行该文件，而不是 EEPROM 的内容。这种机制可确保引导加载程序闪存映像始终可以重置为具有出厂默认设置的有效映像。

另请参阅树莓派引导流程

#### 引导加载程序更新文件

| 文件名 | 目的                                                                           |
| -------- | -------------------------------------------------------------------------------- |
| `recovery.bin`       | 引导加载程序恢复可执行文件                                                     |
| `pieeprom.upd`       | 引导加载程序 EEPROM 映像                                                       |
| `pieeprom.bin`       | 引导加载程序 EEPROM 映像 - 与 pieeprom.upd 相同，但更改了 recovery.bin 的行为  |
| `pieeprom.sig`       | bootloader 镜像（pieeprom.upd/pieeprom.bin）的 sha256 校验和                   |
| `vl805.bin`       | VLI805 USB 固件 EEPROM 镜像 - 仅适用于树莓派 4B 修订版 1.3 及更早版本。 |
| `vl805.sig`       | vl805.bin 的 sha256 校验和                                                     |

* 如果引导加载程序更新映像名为 pieeprom.upd ，则更新完成后， recovery.bin 将重命名为 recovery.000 ，然后系统将重新启动。由于 recovery.bin 不再存在，ROM 将从 SPI 闪存加载新更新的引导加载程序，操作系统将正常启动。
* 如果引导加载程序更新映像名为 pieeprom.bin ，则更新完成后 recovery.bin 将停止。成功后，HDMI 输出将变为绿色，绿色活动指示灯将快速闪烁。如果更新失败，HDMI 输出将变为红色，并通过活动指示灯显示错误代码。
* .sig 文件包含相应映像文件的十六进制 sha256 校验和；将来可能会添加其他字段。
* BCM2711 和 BCM2712 上找到的 ROM 不支持从 USB 大容量存储器或 TFTP 加载 recovery.bin 。相反，更新版本的引导加载程序支持自更新机制，其中引导加载程序能够重新刷新 SPI 闪存本身。请参阅引导加载程序配置页面上的 ENABLE_SELF_UPDATE 。
* 临时 EEPROM 更新文件会在启动时由 rpi-eeprom-update 服务自动删除。

有关 rpi-eeprom-update 配置文件的更多信息，请参阅 rpi-eeprom-update -h 。

#### EEPROM 写保护

引导加载程序和 VLI EEPROM 都支持硬件写保护。有关在刷新 EEPROM 时如何启用此功能的更多信息，请参阅 eeprom_write_protect 选项。

## 树莓派 4 上的启动诊断

从 树莓派 4 bootloader 的 2020-04-16 版本开始，诊断信息可以在 HDMI 显示器上显示。要查看此诊断信息，请关闭树莓派 4，取出 SD 卡，然后重新上电。应该在连接的显示器上出现类似下面的诊断显示。

![Boot diagnostics screen](https://www.raspberrypi.com/documentation/computers/images/bootloader-diagnostics.png)

如果引导加载程序无法从插入的 SD 卡引导，或无法进行网络引导，则还会出现此诊断页面；例如，如果卡上没有可引导的映像，或者卡有缺陷，或者网络引导参数不正确。

一旦显示诊断页面，只能通过重新循环设备的电源（即拔掉电源然后重新插上）来重新启动。

树莓派型号及其内存容量的顶部行描述。QR 码是指向下载页面的链接。

诊断信息如下：

| 行：         | 信息                                                                                                                        |
| -------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| 引导加载程序 | 引导加载程序 git 版本 - RO（如果 EEPROM 受写保护）- 软件构建日期                                                            |
| 更新时间戳   | EEPROM 配置更新的时间戳。在自更新模式中检查此时间戳，以避免更新到旧配置。                                                   |
| 安全启动     | 如果启用了安全启动，则会显示处理器版本（B0/C0）和已签名启动状态标志。否则，此行为空白。                                     |
| 板           | 板修订版 - 序列号 - 以太网 MAC 地址                                                                                         |
| 引导         | 模式（当前引导模式名称和编号）顺序（BOOT ORDER 配置）重试（当前引导模式中的重试次数）重新启动（引导模式列表中的循环次数）。 |
| SD           | SD 卡检测状态（已检测/未检测）。                                                                                            |
| 部分         | 主引导记录主分区类型：LBA。                                                                                                 |
| 防火墙       | 如果存在，请提供 start.elf 和 fixup.dat 的文件名（例如 start4x.elf ， fixup4x.dat ）。                                      |
| 网络         | 网络引导：链接状态（上/下），客户端 IP 地址（IP），子网（SN），默认网关（GW）                                               |
| tftp         | 网络引导：TFTP 服务器 IP 地址                                                                                               |
| 显示         | 指示是否检测到热插拔（ HPD=1 ），以及每个 HDMI 输出是否成功读取了 EDID。                                                    |

可以使用 DISABLE_HDMI 选项禁用此显示器，请参阅引导加载程序配置。

>**注意**
>
>这仅用于诊断引导失败；这不是交互式引导加载程序。如果您需要交互式引导加载程序，请考虑使用 U-Boot 等工具。

## 树莓派启动模式

树莓派有许多不同的启动阶段。本文解释了启动模式的工作原理，以及哪些模式适用于 Linux 启动。

### 特殊 bootcode.bin -only 启动模式

基于 BCM2837 的树莓派（即树莓派 2B 版本 1.2、树莓派 3B 和 树莓派 3B+）可以执行 USB 主机和以太网引导（由于树莓派 3A+没有内置以太网接口，因此无法进行网络引导）。此外，所有旧版树莓派型号在树莓派4 之前可以使用仅 bootcode.bin 方法启用 USB 主机引导。

>**注意**
>
>树莓派 4 和 5 不使用 bootcode.bin 文件。他们的引导加载程序位于板载 EEPROM 芯片中。请参阅有关树莓派引导流程和 SPI 引导 EEPROM 的文档。

将 SD 卡格式化为 FAT32 并复制最新的 bootcode.bin 到 SD 卡上。SD 卡必须放在树莓派中才能引导。在从 SD 卡加载了 bootcode.bin 后，树莓派将继续使用 USB 主机模式引导。

这对基于 BCM2835 和 BCM2836 芯片的树莓派 1、2 和 Zero 型号非常有用，在树莓派 3 无法启动的情况下（与烧录到 BCM2837A0 的引导代码相比，最新的 bootcode.bin 包含了额外的错误修复）。

如果您遇到大容量存储设备仍无法工作的问题，即使使用了这个 bootcode.bin，那么请在 SD 卡上添加一个名为"timeout"的新文件。这将使其等待大容量存储设备初始化的时间延长到六秒。

### bootcode.bin UART 启用

>**注意**
>
>适用于早于树莓派 4 Model B 的主板。 

有关在树莓派 4 bootloader 上启用 UART 的信息，请参阅 bootloader 配置文档。

可以启用早期阶段的 UART 来调试启动问题（与上述 bootcode.bin 仅引导模式一起使用很有用）。要做到这一点，请确保您有最新版本的固件（包括 bootcode.bin）。要检查当前固件是否支持 UART：

```
 strings bootcode.bin | grep BOOT_UART
```

从 bootcode.bin 启用 UART：

```
sed -i -e "s/BOOT_UART=0/BOOT_UART=1/" bootcode.bin
```

接下来，将合适的 USB 串口线连接到您的主机计算机（树莓派将起作用，尽管您可能会发现，最简单的方法是使用 USB 串口线，因为它可以在无需任何烦人的 config.txt 设置的情况下立即使用）。在树莓派或计算模块上使用标准引脚 6、8 和 10（GND、GPIO14、GPIO15）。

然后在 Linux 或 Mac 上使用 screen ，或在 Windows 上使用 putty 连接到串口。

设置串口以接收 115200-8-N-1，并启动您的树莓派。您应该在设备上立即收到来自 bootcode.bin 的串行输出。

## 启动顺序

>**重要**
>
>以下启动顺序仅适用于基于 BCM2837 和 BCM2837B0 的树莓派型号。在此之前的型号上，树莓派将尝试 SD 卡引导，然后是 USB 设备模式引导。有关树莓派 4 和树莓派 5 的引导顺序，请参阅树莓派i 4 和树莓派 5 引导流程部分。 

树莓派 3 上的 USB 启动默认取决于使用的版本。有关在默认情况下未启用时启用 USB 启动模式的信息，请参阅此页面。

当 BCM2837 启动时，它使用两个不同的源来确定要启用哪些启动模式。首先，检查一次可编程（OTP）存储器块，以查看启用了哪些启动模式。如果启用了 GPIO 启动模式设置，则会测试相关的 GPIO 线以选择应尝试哪些已在 OTP 中启用的启动模式。请注意，GPIO 启动模式只能用于选择已在 OTP 中启用的启动模式。有关配置 GPIO 启动模式的详细信息，请参阅 GPIO 启动模式。默认情况下，GPIO 启动模式已禁用。

接下来，引导 ROM 会检查每个引导源是否存在名为 bootcode.bin 的文件；如果成功，它将将代码加载到本地 128K 缓存中并跳转到该代码。总体引导模式流程如下：

* BCM2837 引导
* 读取 OTP 以确定要启用的引导模式
* 如果启用了 GPIO 引导模式，请使用 GPIO 引导模式来优化已启用的引导模式列表
* 如果启用：检查 GPIO 48-53 上的主要 SD 卡上的 bootcode.bin
  * 成功 - 启动
  * 失败 - 超时（五秒）
* 如果启用：检查次要 SD
  * 成功 - 启动
  * 失败 - 超时（五秒）
* 如果启用：检查 NAND
* 如果启用：检查 SPI
* 如果启用：检查 USB
  * 如果 OTG 引脚== 0
    * 启用 USB，等待有效的 USB 2.0 设备（两秒）
      * 发现设备：
        * 如果设备类型 == hub
          * 递归每个端口
        * 如果设备类型 == (大容量存储或 LAN951x)
          * 存储在设备列表中
    * 通过每个 MSD 进行递归
      * 如果找到 bootcode.bin，则启动
    * 通过每个 LAN951x 进行递归
      * DHCP / TFTP 引导
  * 其他（设备模式引导）
    * 启用设备模式并等待主机 PC 枚举
    * 我们使用 VID: 0a5c PID: 0x2763（树莓派 1 或树莓派 2）或 0x2764（树莓派 3）回复 PC

>**注意**
>
>如果没有插入 SD 卡，则 SD 启动模式需要五秒钟才能失败。为了减少这一时间并更快地回退到 USB，您可以插入一个空 SD 卡，或者使用上面描述的 GPIO 启动模式 OTP 设置来仅启用 USB。GPIO 的默认拉电定义在 ARM 外设数据手册的第 102 页。如果在启动时的值不等于默认拉电，则启用该启动模式。USB 枚举是一种启用下游设备在集线器上的电源，然后等待设备拉动 D+ 和 D- 线以指示其是 USB 1 还是 USB 2 的方法。这可能需要时间：对于某些设备，硬盘驱动器可能需要长达三秒才能启动并开始枚举过程。因为这是检测硬件连接的唯一方法，我们必须等待最短时间（两秒）。如果设备在此最大超时后仍未响应，则可以使用 program_usb_boot_timeout=1 在 config.txt 中将超时增加到五秒。*MSD 启动优先于以太网启动。不再需要第一个分区是 FAT 分区，因为 MSD 启动将继续搜索第一个分区之外的 FAT 分区。引导 ROM 现在还支持 GUID 分区，并已经测试了使用 Mac、Windows 和 Linux 分区的硬盘。*使用供应商 ID 0x0424 和产品 ID 0xec00 检测 LAN951x，这与独立的 LAN9500 设备不同，后者的产品 ID 为 0x9500 或 0x9e00。要使用独立的 LAN9500，需要添加 I2C EEPROM 以更改这些 ID 以匹配 LAN951x。

主要的 SD 卡引导模式，标准情况下设置为 GPIOs 49-53。可以从第二组引脚上的次要 SD 卡引导，即将次要 SD 卡添加到 GPIO 引脚上。但是，我们尚未启用此功能。

NAND 引导和 SPI 引导模式确实可以工作，尽管它们尚未完全支持 GPU。

USB 设备引导模式在制造时默认启用，但 USB 主机引导模式仅在 program_usb_boot_mode=1 时启用。只要启用，处理器将使用处理器上的 OTGID 引脚的值来决定两种模式之间的选择。在任何树莓派 Model B/B+上，OTGID 引脚被驱动为 0，因此如果启用，将只能通过主机模式引导（无法通过设备模式引导，因为 LAN951x 设备会阻碍）。

如果将 OTGID 引脚悬空（例如插入 PC），USB 将作为树莓派 Zero 或计算模块上的 USB 设备启动，因此您可以将 bootcode.bin 推送到设备中。用于执行此操作的 usbboot 代码可在 GitHub 上找到。

## 树莓派 4 和 树莓派 5 启动流程

与以前的产品相比，主要区别在于第二阶段引导加载程序是从 SPI 闪存 EEPROM 而不是从以前产品上的 bootcode.bin 文件加载的。

### 第一阶段引导加载程序

ROM（第一阶段）的引导流程如下：

* SoC 上电
* 读取 OTP 以确定 nRPIBOOT GPIO 是否已配置
* 如果 nRPIBOOT GPIO 为高电平或 OTP 未定义 nRPIBOOT GPIO
  * 检查 OTP，看看是否可以从 SD/EMMC 加载 recovery.bin
    * 如果启用 SD 恢复.bin，则检查主 SD / EMMC 是否为 recovery.bin
      * 成功-运行 recovery.bin 并更新 SPI EEPROM
      * 失败-继续
  * 检查 SPI EEPROM 以获取第二阶段加载程序
    * 成功 - 运行第二阶段引导加载程序
    * 失败 - 继续
* 当为真时
  * 尝试从 USB 设备引导加载 recovery.bin
    * 成功 - 运行 recovery.bin 并更新 SPI EEPROM 或切换到 USB 大容量存储设备模式
    * 失败 - 重试 USB 设备引导

>**注意**
>
>recovery.bin 是一个用于刷新引导加载程序 SPI EEPROM 图像的最小第二阶段程序。

### 第二阶段引导加载程序

本节描述第二阶段引导加载程序的高级流程。

有关每个引导模式的更多信息，请参阅引导加载程序配置页面，有关此阶段加载的 GPU 固件文件的描述，请参阅引导文件夹页面。

* 初始化时钟和 SDRAM
* 读取 EEPROM 配置文件
* 检查 PM_RSTS 寄存器以确定是否请求了 HALT
  * 检查 POWER_OFF_ON_HALT 和 WAKE_ON_GPIO EEPROM 配置设置
  * 如果 POWER_OFF_ON_HALT 是 1 而且 WAKE_ON_GPIO 是 0 则
    * 使用 PMIC 关闭系统电源
  * 否则如果 WAKE_ON_GPIO 是 1
    * 在 GPIO3 上启用下降沿中断，以便在 GPIO3 被拉低时唤醒
  * 睡眠
* 当为真时
  * 从 EEPROM 配置文件的 BOOT_ORDER 参数中读取下一个引导模式。
  * 如果引导模式 == RESTART
    * 跳回 BOOT_ORDER 字段中的第一个引导模式。
  * 如果引导模式 == STOP
    * 显示 start.elf 未找到错误模式并永远等待。
  * 如果引导模式 == SD CARD
    * 尝试从 SD 卡加载固件
      * 成功-运行固件
      * 失败-继续
  * 如果引导模式 == NETWORK 则
    * 使用 DHCP 协议请求 IP 地址
    * 从 DHCP 或静态定义的 TFTP 服务器加载固件
    * 如果未找到固件或发生超时或网络错误，则继续
  * 否则，如果引导模式 == USB-MSD 或引导模式 == BCM-USB-MSD ，那么
    * 在 USB 发现未超时时
      * 检查 USB 大容量存储设备
      * 如果发现新的大容量存储设备
        * 对于每个驱动器（LUN）
          * 尝试加载固件
            * 成功 - 运行固件
            * 失败 - 转到下一个 LUN
  * 如果引导模式 == NVME 则
    * 扫描 PCIe 查找 NVMe 设备，如果找到
      * 尝试从 NVMe 设备加载固件
        * 成功 - 运行固件
        * 失败 - 继续
  * 否则如果引导模式 == RPIBOOT 则
    * 尝试使用 USB 设备模式从 USB OTG 端口加载固件-请参阅 USB 启动。 RPIBOOT 模式没有超时。

#### 树莓派 5 的不同点

* 电源按钮用于从 PMIC STANDBY 或 HALT 而不是 GPIO 3 唤醒。
* 固件加载 Linux 内核，而不是 start.elf 。实际上，引导加载程序嵌入了 start.elf 的版本。
* 默认情况下，连接到 3A 电源时禁用 USB 启动。可在 `/boot/firmware/config.txt` 中设置 usb_max_current_enable=1 以启用 USB 启动。或者，您可以在 USB 启动失败时单击一次电源按钮，临时启用 usb_max_current_enable 并继续启动。但是，如果通过按电源按钮启用，此设置在重新启动后不会持续。

### 引导加载程序更新

如果找到 pieeprom.upd 文件，可以在启动固件之前更新引导加载程序。有关引导加载程序更新的更多信息，请参阅引导加载程序 EEPROM 页面。

### 安全更新操作系统（ tryboot ）

引导加载程序/固件提供一次性标志，如果设置，则清除但导致加载 tryboot.txt 而不是 config.txt 。此备用配置将指定待处理的操作系统更新固件、cmdline、内核和 os_prefix 参数。由于在启动固件之前清除了该标志，崩溃或重置将导致在下次重新启动时加载原始 config.txt 文件。

要设置 tryboot 标志，请在 reboot 命令中的分区号后添加 tryboot 。通常，分区号默认为零，但如果添加了额外的参数，则必须指定。

```
# Quotes are important. Reboot only accepts a single argument.
sudo reboot '0 tryboot'
```

所有型号的树莓派都支持 tryboot ，但在树莓派 4 Model B 修订版 1.0 和 1.1 上，EEPROM 不能被写保护。这是因为旧版树莓派 4B 设备必须重置电源供应（丢失 tryboot 状态），因此这些信息存储在 EEPROM 中。

如果 secure-boot 已启用，则 tryboot 模式将导致加载 tryboot.img 而不是 boot.img 。

### tryboot_a_b 模式

如果 autoboot.txt 中的 tryboot_a_b 属性设置为 1 ，那么加载的是 config.txt 而不是 tryboot.txt 。这是因为在更高级别（分区）已经进行了 tryboot 切换，因此在备用分区本身内部拥有 tryboot.txt 文件是不必要的。

注意：当从 boot.img ramdisk 中加载文件时， tryboot_a_b 属性会被隐式设置为 1 。

## 树莓派引导加载程序配置

### 编辑配置

在编辑引导加载程序配置之前，请更新您的系统以获取 rpi-eeprom 软件包的最新版本。

查看当前 EEPROM 配置，请运行以下命令：

```
rpi-eeprom-config
```

要编辑当前 EEPROM 配置并将更新应用到最新的 EEPROM 发布版，请运行以下命令：

```
sudo -E rpi-eeprom-config --edit
```

有关 EEPROM 更新过程的更多信息，请参阅启动 EEPROM。

### 配置属性

本节描述引导加载程序中所有可用配置项。语法与 config.txt 相同，但属性特定于引导加载程序。条件过滤器也受支持，除了 EDID。

#### `BOOT_UART`

如果 1 ，则在 GPIO 14 和 15 上启用 UART 调试输出。将接收调试终端配置为 115200bps，8 位，无奇偶校验位，1 个停止位。

 默认: 0

#### `UART_BAUD`

仅适用于树莓派 5。

更改引导加载程序 UART 的波特率。

支持的值: 9600 , 19200 , 38400 , 57600 , 115200 , 230400 , 460800 , 921600

 默认: 115200

#### `WAKE_ON_GPIO`

如果 1 则 sudo halt 将在低功耗模式下运行，直到 GPIO3 或 GLOBAL_EN 短接到地。

由于专用电源按钮可始终用于唤醒 HALT 或 STANDBY ，因此树莓派 5 上此设置无关紧要。

 默认值： 1

#### `POWER_OFF_ON_HALT`

如果 1 和 WAKE_ON_GPIO=0 ，则 sudo halt 将关闭所有 PMIC 输出。这是停机的最低功耗状态，但可能会导致一些 HAT 出现问题，因为 5V 仍然开启。必须将 GLOBAL_EN 短接到地以启动。

树莓派 400 具有专用电源按钮，即使处理器关闭，也可以操作。此行为默认情况下已启用，但 WAKE_ON_GPIO=2 可以设置为使用外部 GPIO 电源按钮，而不是专用电源按钮。

在树莓派 5 上，这将使 PMIC 处于 STANDBY 模式，其中所有输出都已关闭。无需设置 WAKE_ON_GPIO ，按下专用电源按钮将启动设备。

 默认： 0

#### `BOOT_ORDER`

BOOT_ORDER 设置允许灵活配置不同引导模式的优先级。它表示为一个 32 位无符号整数，其中每个半字节表示一个引导模式。引导模式按照从最低有效半字节到最高有效半字节的顺序尝试。

##### BOOT_ORDER 字段

BOOT_ORDER 属性定义了不同引导模式的顺序。它从右向左读取，最多可以定义八位数字。

| 值  | 模式        | 说明                                                                                                   |
| ----- | ------------- | -------------------------------------------------------------------------------------------------------- |
| 0x0 | SD 卡检测   | 尝试 SD 卡，然后等待卡检测指示卡片已更改。现在已弃用，因为 0xf（重新启动）可用。                       |
| 1   | SD 卡       | SD 卡（或 Compute Module 4 上的 eMMC）。                                                               |
| 2   | NETWORK     | 网络引导 - 请参阅网络引导服务器教程。                                                                  |
| 3   | RPIBOOT     | RPIBOOT - 查看 usbboot。                                                                               |
| 4   | USB-MSD     | USB 大容量存储启动 - 请参阅 USB 大容量存储启动。                                                       |
| 5   | BCM-USB-MSD | 通过 USB Type C 插座从 USB 2.0 引导（CM4：CM4IO 板上的 USB Type A 插座）。在树莓派 5 上不可用。 |
| 6   | NVME        | 仅限 CM4 和 Pi 5：从连接到 PCIe 接口的 NVMe SSD 启动。有关更多详细信息，请参阅 NVMe 启动。             |
| 7   | HTTP        | 通过以太网进行 HTTP 引导。有关更多详细信息，请参阅 HTTP 引导。                                         |
| 14  | STOP        | 停止并显示错误模式。需要重新上电才能退出此状态。                                                       |
| 15  | RESTART     | 从 BOOT_ORDER 字段中的第一个启动模式重新启动，即循环。                                                 |

RPIBOOT 旨在与 Compute Module 4 一起使用，以加载自定义调试映像（例如 Linux RAM-disk）而不是正常启动。这应该是最后的启动选项，因为它目前不支持超时或重试。

##### BOOT_ORDER 示例

| BOOT_ORDER | 说明                                                                  |
| ------------ | -------------------------------------------------------------------------- |
| 3905       | 首先尝试 SD 卡，然后是 USB-MSD，然后重复（如果 BOOT_ORDER 为空，则默认） |
| 3860       | 首先尝试 USB，然后 SD，然后重复                                          |
| 3873       | 首先尝试 SD，然后尝试网络，然后重复                                      |

#### `MAX_RESTARTS`

如果遇到 RESTART（ 0xf ）引导模式超过 MAX_RESTARTS 次数，则会触发看门狗复位。这不建议用于一般用途，但可能对需要完全重置以解决硬件或网络接口问题的测试或远程系统有用。

默认： -1 （无限）

#### `SD_BOOT_MAX_RETRIES`

在移动到 BOOT_ORDER 定义的下一个引导模式之前，在失败后重试 SD 引导的次数。

-1 表示无限重试。

 默认： 0

#### `NET_BOOT_MAX_RETRIES`

在移动到由 BOOT_ORDER 定义的下一个引导模式之前，在失败后网络引导将重试的次数。

-1 表示无限重试。

 默认： 0

#### `DHCP_TIMEOUT`

整个 DHCP 序列超时时间（毫秒），在当前迭代失败之前。

 最小值: 5000

 默认值: 45000

#### `DHCP_REQ_TIMEOUT`

重试 DHCP DISCOVER 或 DHCP REQ 前的超时时间（毫秒）。

 最小值： 500

 默认值： 4000

#### `TFTP_FILE_TIMEOUT`

通过 TFTP 进行单个文件下载的超时时间（毫秒）。

 最小值： 5000

 默认值： 30000

#### `TFTP_IP`

可选的点分十进制 IP 地址（例如 192.168.1.99 ）用于覆盖 DHCP 请求中的服务器 IP。

在家庭网络中，这可能很有用，因为 tftpd-hpa 可以代替 DHCP 服务器的 dnsmasq。

 默认值： ""

#### `TFTP_PREFIX`

为了支持每个树莓派的唯一 TFTP 引导目录，引导加载程序使用设备特定目录作为文件名的前缀。如果在带前缀的目录中找不到 start4.elf 或 start.elf，则清除前缀。

在旧版模型上，序列号被用作前缀，但是在树莓派 4 和 5 上，MAC 地址不再从序列号生成，这使得通过检查 DHCPDISCOVER 数据包自动创建 tftpboot 目录在服务器上变得困难。为了支持这一点，TFTP_PREFIX 可以定制为 MAC 地址、固定值或序列号（默认）。

| 值 | 说明                                   |
| ---- | ---------------------------------------- |
| 0  | 使用序列号，例如 9ffefdef/             |
| 1  | 使用由 TFTP_PREFIX_STR 指定的字符串    |
| 2  | 使用 MAC 地址，例如 dc-a6-32-01-36-c2/ |

 默认值：0

#### `TFTP_PREFIX_STR`

当 TFTP_PREFIX 设置为 1 时，指定用于自定义目录前缀字符串。例如：- TFTP_PREFIX_STR=tftp_test/

 默认: ""

最大长度: 32 个字符

#### `PXE_OPTION43`

使用不同的字符串覆盖 PXE Option43 匹配字符串。通常最好将自定义应用于 DHCP 服务器，而不是更改客户端行为，但在无法实现该目标的情况下提供此选项。

 默认: Raspberry Pi Boot

#### `DHCP_OPTION97`

在旧版中，客户端 GUID（Option97）只是将序列号重复四次。默认情况下，新的 GUID 格式是四字符代码（FourCC）的串联（树莓派 4 为 RPi4 0x34695052，树莓派 5 为 RPi5 0x35695052），板子修订版（例如 0x00c03111 或 0x00d04170）（4 字节），MAC 地址的最低有效 4 字节和 4 字节序列号。这旨在是独一无二的，但也向 DHCP 服务器提供了结构化信息，允许识别树莓派 4 和 5 计算机，而无需依赖以太网 MAC OUID。

指定 DHCP_OPTION97=0 以恢复旧行为，或指定自定义 4 字节前缀的非零十六进制值。

 默认： 0x34695052

#### `MAC_ADDRESS`

使用给定值覆盖树莓派的以太网 MAC 地址。例如 dc:a6:32:01:36:c2

 默认： ""

#### `MAC_ADDRESS_OTP`

使用存储在客户 OTP 寄存器中的值覆盖树莓派的以太网 MAC 地址。

例如，要使用存储在 Customer OTP 的第 0 行和第 1 行中的 MAC 地址。

```
MAC_ADDRESS_OTP=0,1
```

第一个值（例如中的第 0 行）包含 OUI 和 MAC 地址的最高 8 位。第二个值（例如中的第 1 行）存储 MAC 地址的其余 16 位。这与制造时为树莓派编程的 MAC 地址使用的格式相同。

任意两个客户行可以选择并以任何顺序组合。

Customer OTP 行是 OTP 寄存器 36 到 43，在 vcgencmd otp_dump 输出中，因此如果前两行按照以下方式编程，则 MAC_ADDRESS_OTP=0,1 将给出一个 MAC 地址为 e4:5f:01:20:24:7e 。

```
36:247e0000
37:e45f0120
```

 默认： ""

#### 静态 IP 地址配置

如果设置了 TFTP_IP 和以下选项，则将跳过 DHCP，并应用静态 IP 配置。如果 TFTP 服务器与客户端位于同一子网上，则可能省略网关。

##### `CLIENT_IP`

客户端的 IP 地址，例如 192.168.0.32

 默认: ""

##### `SUBNET`

子网地址掩码 例如 255.255.255.0

 默认: ""

##### `GATEWAY`

如果 TFTP 服务器位于不同子网上，则使用的网关地址，例如 192.168.0.1

 默认： ""

#### `DISABLE_HDMI`

如果 DISABLE_HDMI=1 ，则禁用 HDMI 引导诊断显示。其他非零值保留供将来使用。

 默认值: 0

#### `HDMI_DELAY`

在 N 秒内跳过 HDMI 诊断显示的渲染（默认为 5 秒），除非发生致命错误。默认行为旨在避免在正常的 SD/USB 启动过程中短暂出现引导加载程序诊断屏幕。

 默认值: 5

#### `ENABLE_SELF_UPDATE`

使启动加载程序能够从 TFTP 或 USB 大容量存储设备（MSD）启动文件系统更新自身。

如果启用了自更新，则引导加载程序将在启动文件系统中查找更新文件（.sig/.upd）。如果更新映像与当前映像不同，则应用更新并重置系统。否则，如果 EEPROM 映像是逐字节相同的，则引导将继续正常进行。

 注意：

* 2021 年之前的引导加载程序版本不支持 self-update 。
* 在 2022 年之前，SD 卡引导中未启用自更新。在树莓派 4 上，ROM 可以从 SD 卡加载 recovery.bin。在 CM4 上，自更新和 recovery.bin 均无效，需要使用 USB 引导（请参阅 CM4 引导加载程序文档）。
* 从 2022 年开始（beta 和稳定版），可以从 SD 卡启用自更新。
* 用于网络引导，请确保可以通过 NFS 挂载 TFTP boot 目录，并且 rpi-eeprom-update 可以对其进行写入。

 默认值： 1

#### `FREEZE_VERSION`

以前，此属性仅由 rpi-eeprom-update 脚本检查。但是，现在自更新已启用，引导加载程序也将检查此属性。如果设置为 1，则会覆盖 ENABLE_SELF_UPDATE 以停止自动更新。要禁用 FREEZE_VERSION ，您必须使用带有 recovery.bin 的 SD 卡引导。

自定义 EEPROM 更新脚本还必须检查此标志。

 默认： 0

#### `HTTP_HOST`

如果启动网络安装或 HTTP 引导，则从此服务器下载 boot.img 和 boot.sig 。

无效的主机名将被忽略。它们应仅包含小写字母数字字符和 - 或 . 。如果设置了 HTTP_HOST ，则禁用 HTTPS，而改用普通 HTTP。您可以指定 IP 地址，以避免需要进行 DNS 查找。主机名中不要包含 HTTP 方案或任何斜杠。

 默认： fw-download-alias1.raspberrypi.com

#### `HTTP_PORT`

您可以使用此属性更改用于网络安装和 HTTP 引导的端口。在使用默认主机 fw-download-alias1.raspberrypi.com 时启用 HTTPS。如果更改了 HTTP_HOST ，则禁用 HTTPS，而改用普通 HTTP。

当 HTTPS 被禁用时，即使 HTTP_PORT 被更改为 443 ，仍将使用纯 HTTP。

默认值：如果启用了 HTTPS，则为 443 ，否则为 80

#### `HTTP_PATH`

用于网络安装和 HTTP 引导的路径。

区分大小写。使用正斜杠（Linux）作为路径分隔符。前导和尾随正斜杠不是必需的。

如果 HTTP_HOST 未设置，则 HTTP_PATH 将被忽略，URL 将是 https://fw-download-alias1.raspberrypi.com:443/net_install/boot.img 。如果设置了 HTTP_HOST ，URL 将是 http://<HTTP_HOST>:<HTTP_PORT>/<HTTP_PATH>/boot.img

 默认： net_install

#### `IMAGER_REPO_URL`

嵌入式 Raspberry Pi Imager 应用程序配置为在启动时下载的 json 文件。

您可以更改嵌入式 Raspberry Pi Imager 应用程序使用的 json 文件的 URL，以便提供您自己的图像。您可以通过 --repo 参数传递 URL 来测试标准 Raspberry Pi Imager 应用程序。

 默认值： http://downloads.raspberrypi.org/os_list_imagingutility_v3.json

#### `NET_INSTALL_ENABLED`

当网络安装启用时，如果检测到键盘，引导加载程序会在启动时显示网络安装屏幕。

要启用网络安装，请添加 NET_INSTALL_ENABLED=1 ，要禁用网络安装，请添加 NET_INSTALL_ENABLED=0 。

如果设置了 DISABLE_HDMI=1 ，则会忽略此设置并禁用网络安装。

为了检测键盘，网络安装必须初始化 USB 控制器并枚举设备。这会增加约 1 秒的启动时间，因此在某些嵌入式应用中禁用网络安装可能是有利的。

默认值：在树莓派 4 和树莓派 400 上为 1 ，在 Compute Module 4 上为 0 。

#### `NET_INSTALL_KEYBOARD_WAIT`

如果启用了网络安装，引导加载程序会尝试检测键盘和 SHIFT 键以启动网络安装。您可以使用此属性更改此等待时间的长度（以毫秒为单位）。

设置此项为 0 会禁用键盘等待，尽管如果未找到引导文件且 USB 引导模式 4 处于 BOOT_ORDER 状态，仍然可以启动网络安装。

>**注意**
>
>测试表明键盘和 SHIFT 检测至少需要 750 毫秒。

 默认值： 900

#### NETCONSOLE - 高级日志记录

NETCONSOLE 复制调试消息到网络接口。IP 地址和端口由 NETCONSOLE 字符串定义。

>**注意**
>
>NETCONSOLE 阻塞，直到以太网链路建立或超时发生。超时值为 DHCP_TIMEOUT ，尽管除非请求网络引导，否则不会尝试 DHCP。


##### 格式

请参阅 https://wiki.archlinux.org/index.php/Netconsole

```
src_port@src_ip/dev_name,dst_port@dst_ip/dst_mac
E.g. 6665@169.254.1.1/,6666@/
```

为了简化解析，引导加载程序要求每个字段分隔符都必须存在。必须指定源 IP 地址，但以下字段可以留空并分配默认值。

* 源端口 - 6665
* 设备名称 - "" (设备名称始终被忽略)
* 目标端口 - 6666
* 目的地 IP - 255.255.255.255
* 目的地 MAC - 00:00:00:00:00

查看数据的一种方法是将测试树莓派 4 连接到另一台运行 WireShark 的树莓派，并选择“udp.srcport == 6665”作为过滤器，然后选择分析 → 跟踪 → UDP 流以 ASCII 日志形式查看。

NETCONSOLE 不应默认启用，因为它可能会导致网络问题。可以通过 GPIO 过滤器按需启用：

```
# Enable debug if GPIO 7 is pulled low
[gpio7=0]
NETCONSOLE=6665@169.254.1.1/,6666@/
```

默认值： "" （未启用）

最大长度：32 个字符

#### `PARTITION`

如果未明确由 reboot 命令（例如 sudo reboot N ）或 boot_partition=N 在 autoboot.txt 中设置，可以使用 PARTITION 选项指定引导分区号。如果用户按下按钮，可以使用此选项从救援分区引导。

```
# Boot from partition 2 if GPIO 7 is pulled low
[gpio7=0]
PARTITION=2
```

 默认值：0

#### `PSU_MAX_CURRENT`

仅适用于树莓派 5。

如果设置，则此属性指示固件跳过 USB 供电协商，并假定连接到具有给定电流评级的电源。通常，这通常设置为 3000 或 5000 ，即低电流或高电流能力的电源。

 默认： ""

#### `USB_MSD_EXCLUDE_VID_PID`

一个最多包含四个 VID/PID 对的列表，指定引导加载程序应忽略的设备。如果这与 HUB 匹配，则 HUB 将不被枚举，导致所有下游设备被排除在外。这旨在允许在引导枚举期间忽略有问题的（例如，枚举速度非常慢）设备。这是引导加载程序特有的，不会传递给操作系统。

格式是以 VID 作为最高有效四位的十六进制值的逗号分隔列表。不允许空格。例如 034700a0,a4231234

 默认： ""

#### `USB_MSD_DISCOVER_TIMEOUT`

如果在此超时内未找到任何 USB 大容量存储设备，则停止 USB-MSD，并选择下一个引导模式。

最小值: 5000 (5 秒)

默认值: 20000 (20 秒)

#### `USB_MSD_LUN_TIMEOUT`

在前进到下一个 LUN 之前等待的毫秒数，例如，多槽 SD 卡阅读器。这仍在调整中，但可能有助于加快引导速度，如果连接了旧/慢设备以及包含操作系统的快速 USB-MSD 设备。

 最小值: 100

默认值: 2000 (2 秒)

#### `USB_MSD_PWR_OFF_TIME`

仅适用于树莓派 4。

当树莓派重新启动时，USB 电源会被硬件关闭。短暂的断电时间可能会导致一些 USB 设备出现问题，因此可以使用此参数来强制延长断电时间，就好像电缆被物理拔出一样。

在 Pi4 v1.3 版本及更旧版本上，可配置/长时间断电需要启用 XHCI 控制器，因此实际上会出现短暂的断电，然后是较长的可配置断电。通过将此参数设置为零，可以跳过较长的可配置断电。

在更新的版本中，硬件确保 USB 电源在重新启动后关闭，并且引导加载程序仅在此超时时间过去后才启用电源。这发生在内存初始化之后，确保 USB 电源至少关闭两秒钟。因此，此参数通常不会影响更新的硬件版本。

 最小值: 0

 最大值: 5000

默认值: 1000 (1 秒)

#### `USB_MSD_STARTUP_DELAY`

如果定义了，在 USB 主机控制器初始化后，延迟给定超时时间进行 USB 枚举。如果 USB 硬盘需要很长时间初始化并触发 USB 超时，那么可以使用此延迟来为驱动程序提供额外的初始化时间。可能还需要增加整体 USB 超时时间 ( USB_MSD_DISCOVER_TIMEOUT )。

 最小值: 0

最大值: 30000 (30 秒)

 默认: 0

#### `VL805`

仅适用于 Compute Module 4。

如果 VL805 属性设置为 1 ，则引导加载程序将搜索 VL805 PCIe XHCI 控制器，并尝试使用嵌入在引导加载程序 EEPROM 中的 VL805 固件进行初始化。这使得工业设计可以使用 VL805 XHCI 控制器，而无需为 VL805 固件提供专用的 SPI EEPROM。

* 在 Compute Module 4 上，引导加载程序永远不会写入专用的 VL805 SPI EEPROM。此选项只是配置控制器从 SDRAM 加载固件。
* 如果 VL805 XHCI 控制器有专用的 EEPROM，请不要使用此选项。如果安装了 VL805 ROM，它将无法初始化，因为 VL805 ROM 将尝试使用专用的 SPI EEPROM。
* 嵌入式的 VL805 固件假定与树莓派 4B 相同的 USB 配置（两个 USB 3.0 端口和四个 USB 2.0 端口）。不支持加载替代的 VL805 固件映像，应该使用专用的 VL805 SPI EEPROM 来代替这样的配置。

 默认: 0

#### `XHCI_DEBUG`

此属性是一个位字段，用于控制大容量存储引导模式下 USB 调试消息的详细程度。启用所有这些消息会生成大量日志数据，这将减慢启动速度，甚至可能导致启动失败。对于详细日志，最好使用 NETCONSOLE 。

| 值 | 记录                        |
| ---- | ----------------------------- |
| 1  | USB 描述符                  |
| 2  | 大容量存储模式状态机        |
| 4  | 大容量存储模式状态机 - 详细 |
| 8  | 所有 USB 请求               |
| 16 | 设备和集线器状态机          |
| 32 | 所有 xHCI TRB（非常详细）   |
| 64 | 所有 xHCI 事件（非常详细）  |

将值相加以组合它们。例如：

```
# Enable mass storage and USB descriptor logging
XHCI_DEBUG=0x3
```

默认： 0x0 （未启用 USB 调试消息）

#### [config.txt] 部分

阅读 config.txt 后，GPU 固件 start4.elf 会读取引导加载程序 EEPROM 配置，并检查是否存在名为 [config.txt] 的部分。如果 [config.txt] 部分存在，则将此部分开头到文件末尾的内容附加到内存中，以便与从引导分区读取的 config.txt 文件的内容合并。这可用于自动将设置应用于每个操作系统，例如 dtoverlays。

>**警告**
>
>如果指定了导致引导失败的无效配置，则必须重新刷新引导加载程序 EEPROM。 

### config.txt 中的配置属性

树莓派 5 需要存在一个 config.txt 文件来指示分区是可引导的。

#### `boot_ramdisk`

如果将此属性设置为 1 ，则引导加载程序将尝试加载一个名为 boot.img 的 ramdisk 文件，其中包含引导文件系统。随后的文件（例如 start4.elf ）将从 ramdisk 中读取，而不是从原始引导文件系统中读取。

boot_ramdisk 的主要目的是支持 secure-boot ，然而，未签名的 boot.img 文件也对网络引导或 RPIBOOT 配置很有用。

* RAM 磁盘文件的最大大小为 96MB。
* boot.img 文件是原始磁盘 .img 文件。建议的格式是一个没有主引导记录的普通 FAT32 分区。
* RAM 磁盘文件系统的内存在操作系统启动之前被释放。
* 如果选择 TRYBOOT，则引导加载程序将搜索 tryboot.img 而不是 boot.img 。
* 另请参阅 autoboot.txt。

有关 secure-boot 和创建 boot.img 文件的更多信息，请参阅 USBBOOT。

 默认: 0

#### `boot_load_flags`

自定义固件的实验性属性（裸机）。

第 0 位（0x1）表示.elf 文件是自定义固件。这将禁用任何兼容性检查（例如 USB MSD 启动支持），并在启动可执行文件之前重置 PCIe。

在树莓派 5 上不相关，因为没有 start.elf 文件。

 默认： 0x0

#### `pciex4_reset`

仅适用于树莓派 5。

默认情况下， RP1 使用的 PCIe x4 控制器在启动操作系统之前被重置。如果将此参数设置为 0 ，则禁用重置，允许操作系统或裸金属代码继承 PCIe 配置设置从引导加载程序。

 默认值： 1

#### `uart_2ndstage`

如果 uart_2ndstage 是 1 ，则启用通过 UART 进行调试记录。此选项还会自动在 start.elf 中启用 UART 记录。这也在引导选项页面上有描述。

BOOT_UART 属性还可以启用引导加载程序 UART 记录，但不会在 start.elf 中启用 UART 记录，除非还设置了 uart_2ndstage=1 。

 默认值： 0

#### `erase_eeprom`

如果 erase_eeprom 设置为 1 ，那么 recovery.bin 将擦除整个 SPI EEPROM 而不是刷新引导加载程序映像。此属性在正常引导过程中不起作用。

 默认: 0

#### `eeprom_write_protect`

配置 EEPROM write status register 。这可以设置为将整个 EEPROM 标记为写保护，或清除写保护。

此选项必须与控制对 EEPROM Write Status Register 的更新的 EEPROM /WP 引脚一起使用。将 /WP 拉低（CM4 EEPROM_nWP 或树莓派 4 TP5 ）不会写保护 EEPROM，除非还配置了 Write Status Register 。

查看 Winbond W25x40cl 或 Winbond W25Q16JV 数据表以获取更多详细信息。

eeprom_write_protect 设置在 config.txt 中为 recovery.bin 。

| 值 | 描述                              |
| ---- | ----------------------------------- |
| 1  | 配置写保护区域以覆盖整个 EEPROM。 |
| 0  | 清除写保护区域。                  |
| -1 | 什么也不做。                      |

>**注意**
>
>flashrom 不支持清除写保护区域，如果定义了写保护区域，则更新 EEPROM 将失败。

在树莓派 5 上， /WP 默认被拉低，因此只要配置了 Write Status Register ，写保护就会被启用。要清除写保护，请通过连接 TP14 和 TP1 将 /WP 拉高。

 默认： -1

#### `os_check`

在树莓派 5 上，固件会在尝试从当前分区引导之前自动检查兼容的设备树文件。否则，会加载旧版的不兼容内核，然后挂起。要禁用此检查（例如用于裸机开发），请在 config.txt 中设置 os_check=0

 默认： 1

#### `bootloader_update`

此选项可设置为 0，以阻止自更新，而无需更新 EEPROM 配置。在通过网络引导更新多个树莓派时，有时会很有用，因为此选项可以针对每个树莓派进行控制（例如，通过 config.txt 中的序列号过滤器）。

 默认： 1

### config.txt 中的安全启动配置属性

##### [如何使用树莓派安全启动](https://pip.raspberrypi.com/categories/685-whitepapers-app-notes/documents/RP-003466-WP/Boot-Security-Howto.pdf)

如何使用树莓派安全启动

本白皮书描述了如何在基于树莓派 4 的设备上实现安全启动。有关我们实现安全启动方法的概述，请参阅树莓派 4 启动安全白皮书。安全启动系统旨在与 buildroot -based OS 映像一起使用；不建议或支持将其与 Raspberry Pi OS 一起使用。

以下 config.txt 属性用于编程 secure-boot OTP 设置。这些更改是不可逆的，只能在刷新引导加载程序 EEPROM 图像时通过 RPIBOOT 编程。这确保 secure-boot 无法远程设置，也无法通过意外插入陈旧的 SD 卡图像来设置。

要了解有关启用 secure-boot 的更多信息，请参阅 Secure Boot 自述文件和 USBBOOT 存储库中的 Secure Boot 教程。

#### `program_pubkey`

如果将此属性设置为 1 ，则 recovery.bin 将 EEPROM 图像中公钥的哈希写入 OTP。只要设置了，引导加载程序将拒绝使用不同 RSA 密钥签名的 EEPROM 图像或未签名图像。

 默认: 0

#### `revoke_devkey`

如果将此属性设置为 1 ，则 recovery.bin 将向 OTP 写入一个值，防止 ROM 加载不支持 secure-boot 的旧版本第二阶段引导加载程序，这可以防止通过恢复到较旧版本的引导加载程序来关闭 secure-boot 。

 默认: 0

#### `program_rpiboot_gpio`

由于树莓派 4B 或树莓派 400 上没有专用的 nRPIBOOT 跳线帽，因此必须使用替代的 GPIO 来选择 RPIBOOT 模式，通过将 GPIO 拉低来实现。只能选择一个 GPIO，并且可用选项为 2, 4, 5, 6, 7, 8 。此属性不取决于 secure-boot ，但请验证此 GPIO 配置不会与在引导过程中将 GPIO 拉低的任何 HAT 发生冲突。

由于出于安全考虑，此属性只能通过 RPIBOOT 进行编程，因此必须首先使用 erase_eeprom 清除引导加载程序 EEPROM。这会导致 BCM2711 ROM 切换到 RPIBOOT 模式，然后允许设置此选项。

 默认：``

#### `program_jtag_lock`

如果将此属性设置为 1 ，则 recovery.bin 将编程一个防止使用 VideoCore JTAG 的 OTP 值。此选项要求 program_pubkey 和 revoke_devkey 也设置。此选项可以防止故障分析，在设备完全测试后才应设置。

 默认： 0

## USB 启动模式

>**警告**
>
>默认情况下，树莓派从 SD 卡启动。这是新用户和经验不足用户的推荐方法。 

USB 有两种独立的启动模式：USB 设备启动和 USB 主机启动。

在启动时，固件通过读取 OTP 位来选择两种启动模式之间的选择。有两个位来控制 USB 启动。第一个启用 USB 设备启动，默认情况下启用；第二个启用 USB 主机启动。如果设置了 USB 主机启动模式位，则处理器会读取 OTGID 引脚以决定是作为主机（驱动为零，如任何树莓派 Model B/B+上）还是作为设备（悬空）。树莓派 Zero 通过 USB 连接器上的 OTGID 引脚访问此引脚，计算模块通过边缘连接器访问此引脚。

还有 OTP 位，允许使用某些 GPIO 引脚来选择树莓派应尝试使用哪些引导模式。

>**注意**
>
>仅适用于某些型号的 USB 引导模式。 

### USB 设备引导模式

>**注意**
>
>仅适用于树莓派计算模块、计算模块3、树莓派 Zero、Zero W、A、A+ 和 3A+ 上可用的设备引导。 

当激活此引导模式（通常在从 SD 卡引导失败后），树莓派将其 USB 端口置于设备模式，并等待主机发送 USB 复位。示例代码显示主机需要如何与树莓派通信可在 Github 上找到。

主机首先向设备发送一个结构，通过控制端点 0 传输。其中包含引导的大小和签名（未启用安全性，因此不需要签名）。其次，代码通过端点 1 传输（bootcode.bin）。最后，设备将以成功代码回复：

* 0 - 成功
* 0x80 - 失败

### USB 主机启动模式

>**注意**
>
>仅适用于树莓派 3B、3B+、3A+ 和 2B v1.2 的主机引导。树莓派 3A+ 仅支持大容量存储引导，不支持网络引导。

USB 主机引导模式遵循以下顺序：

* 启用 USB 端口，并等待 D+ 线被拉高，表示连接了 USB 2.0 设备（我们仅支持 USB2.0）
* 如果设备是集线器：
  * 启用集线器的所有下游端口的电源
  * 对于每个端口，循环最多两秒（如果已设置 program_usb_boot_timeout=1 ，则为五秒）
    * 释放复位并等待 D+被拉高以指示设备已连接
    * 如果检测到设备：
      * 发送“获取设备描述符”
        * 如果 VID == SMSC && PID == 9500
          * 将设备添加到以太网设备列表
      * 如果类接口 == 大容量存储类
        * 将设备添加到大容量存储设备列表
* 否则
  * 枚举单个设备
* 浏览大容量存储设备列表
  * 从大容量存储设备启动
* 浏览以太网设备列表
  * 从以太网启动

## USB 大容量存储启动

>**注意**
>
>仅适用于树莓派 2B v1.2、3A+、3B、3B+、4B、400 和 Zero 2 W，以及树莓派计算模块 3、3+ 和 4。 

您可能希望从 USB 大容量存储设备（如闪存驱动器或 USB 硬盘）引导您的树莓派。连接 USB 设备时，特别是硬盘和固态硬盘时，请注意它们的功率要求。如果您计划连接多个固态硬盘或硬盘到树莓派，通常需要外部电源 - 要么是带电源的硬盘外壳，要么是带电源的 USB 集线器。

>**注意**
>
>旧版树莓派 4B 之前的型号存在已知问题，无法使用某些 USB 设备启动。

### 树莓派 4B 和 树莓派 400

树莓派 400 和更新的树莓派 4B 板上的引导加载程序默认支持 USB 引导，尽管 BOOT_ORDER 引导加载程序配置可能需要修改。在旧版的树莓派 4B 板上，或者选择备用引导模式时，必须更新引导加载程序。

 查看：

* 通过 Raspberry Pi Imager 更改引导模式的说明
* 通过 raspi-config 更改启动模式的说明
* 其他启动配置选项的引导加载程序配置页面

### 计算模块 4

请查看闪存计算模块 eMMC 以获取引导加载程序更新说明。

### 树莓派 3B+

树莓派 3B+支持开箱即用的 USB 大容量存储启动。

### 树莓派 2B, 3A+, 3B, CM3, CM3+, Zero 2 W

在 树莓派 2B v1.2、3A+、3B、Zero 2 W 和 Compute Module 3 和 3+ 上，您必须首先启用 USB 主机启动模式。这是为了允许 USB 大容量存储启动和网络启动。

>**注意**
>
>树莓派 3A+ 或 Zero 2 W 上不支持网络启动。

要启用 USB 主机启动模式，树莓派需要从带有特殊选项的 SD 卡引导，以在一次性可编程（OTP）存储器中设置 USB 主机启动模式位。只要设置了此位，就不再需要 SD 卡。

>**警告**
>
>对 OTP 所做的任何更改都是永久的，无法撤消。 

* 在树莓派 3A+上，将 OTP 位设置为启用 USB 主机启动模式将永久阻止该树莓派以 USB 设备模式启动。

您可以使用运行 Raspberry Pi OS 的任何 SD 卡来编程 OTP 位。

启用 USB 主机启动模式：

```
echo program_usb_boot_mode=1 | sudo tee -a /boot/firmware/config.txt
```

这将 program_usb_boot_mode=1 添加到 /boot/firmware/config.txt 的末尾。

虽然选项被命名为 program_usb_boot_mode ，但它只启用了 USB 主机启动模式。 USB 设备启动模式仅适用于某些树莓派型号-请参阅 USB 设备启动模式。

使用 sudo reboot 重新启动树莓派，并检查 OTP 是否已被编程：

```
vcgencmd otp_dump | grep 17:
17:3020000a
```

检查输出 0x3020000a 是否显示。如果没有显示，则 OTP 位未成功编程。在这种情况下，请再次执行编程过程。如果位仍未设置，则可能表明树莓派硬件本身存在故障。

如果您愿意，可以从 config.txt 中删除 program_usb_boot_mode 行，这样，如果您将 SD 卡插入另一台树莓派，它将不会编程 USB 主机启动模式。确保 config.txt 末尾没有空行。

您现在可以像从 SD 卡引导一样从 USB 大容量存储设备引导。有关更多信息，请参阅以下部分。

### 从 USB 大容量存储设备引导

过程与 SD 卡相同-只需使用操作系统映像对 USB 存储设备进行映像。

准备存储设备后，连接驱动器并启动树莓派，注意外部驱动器的额外 USB 功率要求。

五到十秒后，树莓派应开始引导并在连接的显示器上显示彩虹闪屏。确保在树莓派中没有插入 SD 卡，因为如果有，它将首先从 SD 卡引导。

查看引导模式文档，了解引导顺序和备用引导模式（网络、USB 设备、GPIO 或 SD 引导）。

### 已知问题

>**注意**
>
>这些不适用于树莓派 4 Model B。

* 检查可引导 USB 设备的默认超时时间为两秒。一些闪存驱动器和硬盘启动速度太慢。可以将此超时时间延长到五秒（在 SD 卡上添加一个新文件 timeout ），但请注意，有些设备响应时间甚至更长。
* 一些闪存驱动器具有非常特定的协议要求，这些要求不受引导代码处理，因此可能不兼容。

### 特殊 bootcode.bin -only 引导模式

>**重要**
>
>这不适用于树莓派 4 Model B。 

如果您无法使用特定的 USB 设备来引导您的树莓派，另一种选择（适用于树莓派 2B v1.2、3A+、3B 和 3B+）是使用特殊的 bootcode.bin-only 引导模式。树莓派仍将从 SD 卡引导，但只有 bootcode.bin 从中读取的文件。

### 硬件兼容性

在尝试从 USB 大容量存储设备启动之前，建议在 Linux 下验证设备是否正常工作。使用 SD 卡启动，然后插入 USB 大容量存储设备。这应该显示为可移动驱动器。这在使用 USB SATA 适配器时尤为重要，该适配器可能受到引导加载程序在大容量存储模式下的支持，但如果 Linux 选择 USB 附加 SCSI-UAS 模式，则可能失败。

旋转硬盘驱动器几乎总是需要有电源的 USB 集线器。即使一切看起来正常，没有有电源的 USB 集线器，您可能会遇到间歇性故障。

### 多个可引导驱动器

在搜索可引导分区时，引导加载程序并行扫描所有 USB 大容量存储设备，并将选择第一个响应的设备。如果引导分区不包含适当的 start.elf 文件，则会选择下一个可用设备。根据 USB 拓扑结构指定引导设备的方法不存在，因为这会减慢引导速度并增加不必要且难以支持的配置复杂性。

>**注意**
>
>config.txt 文件条件过滤器可用于在复杂设备配置中选择备用固件。 

## 网络引导

本节描述了树莓派 3B、3B+ 和 2B v1.2 上的网络引导工作原理。

在 Pi 4 和 Pi 5 上，网络引导是在 EEPROM 中的第二阶段引导加载程序中实现的。有关更多信息，请参阅树莓派 4 引导加载程序配置。

我们还有关于设置网络引导系统的教程。

仅适用于上述树莓派型号内置有线适配器的网络引导。不支持通过无线局域网引导，也不支持通过任何其他有线网络设备引导。

### 网络引导流程

要进行网络引导，引导 ROM 执行以下操作：

* 初始化板载以太网设备（Microchip LAN9500 或 LAN7500）
* 发送 DHCP 请求（使用厂商类标识符 DHCP 选项 60 设置为 PXEClient:Arch:00000:UNDI:002001 ）
* 接收 DHCP 回复
* (可选)接收 DHCP 代理回复
* ARP 到 tftpboot 服务器
* ARP 回复包括 tftpboot 服务器以太网地址
* TFTP RRQ `bootcode.bin`
  * 未找到文件：服务器用带有文本错误消息的 TFTP 错误响应回复
  * 文件已存在：服务器将用带有头部中块编号的文件的第一个块（512 字节）的数据回复
    * 树莓派用包含块编号的 TFTP ACK 数据包进行回复，并重复直到最后一个不是 512 字节的块
* TFTP RRQ `bootsig.bin`
  * 通常会导致错误 file not found 。这是可以预料到的，TFTP 引导服务器应该能够处理它。

从这一点开始， bootcode.bin 代码继续加载系统。它将尝试访问的第一个文件是 <serial_number>/start.elf 。如果这不会导致错误，那么要读取的任何其他文件都将以 serial_number 为前缀。这很有用，因为它使您能够为您的树莓派创建具有单独 start.elf / 内核的单独目录。

要获取设备的序列号，您可以尝试使用 tcpdump / wireshark 查看访问的文件，或者运行标准的 Raspberry Pi OS SD 卡和 cat /proc/cpuinfo 。

如果您将所有文件放入 TFTP 目录的根目录中，那么随后访问的所有文件都将从那里访问。

### 调试网络引导模式

首先要检查的是 OTP 位是否正确编程。为此，您需要将 program_usb_boot_mode=1 添加到 config.txt ，然后重新启动（使用能够正确引导到 Raspberry Pi OS 的标准 SD 卡）。完成这些步骤后，您应该能够执行以下操作：

```
$ vcgencmd otp_dump | grep 17:
```

如果第 17 行包含 3020000a ，则 OTP 已正确编程。现在，您应该能够移除 SD 卡，插入以太网，然后在树莓派上电约 5 秒后，以太网 LED 灯应该亮起。

要在服务器上捕获以太网数据包，请在 tftpboot 服务器（或 DHCP 服务器，如果它们不同）上使用 tcpdump。否则，您将无法看到直接发送的数据包，因为网络交换机不是集线器！

```
$ sudo tcpdump -i eth0 -w dump.pcap
```

这将把 eth0 上的所有内容写入名为 dump.pcap 的文件中。然后，您可以对数据包进行后处理或将其上传到 cloudshark 进行通信。

#### DHCP 请求/响应

作为最低要求，您应该看到类似以下内容的 DHCP 请求和回复：

```
6:44:38.717115 IP (tos 0x0, ttl 128, id 0, offset 0, flags [none], proto UDP (17), length 348)
    0.0.0.0.68 > 255.255.255.255.67: [no cksum] BOOTP/DHCP, Request from b8:27:eb:28:f6:6d, length 320, xid 0x26f30339, Flags [none] (0x0000)
	  Client-Ethernet-Address b8:27:eb:28:f6:6d
	  Vendor-rfc1048 Extensions
	    Magic Cookie 0x63825363
	    DHCP-Message Option 53, length 1: Discover
	    Parameter-Request Option 55, length 12:
	      Vendor-Option, Vendor-Class, BF, Option 128
	      Option 129, Option 130, Option 131, Option 132
	      Option 133, Option 134, Option 135, TFTP
	    ARCH Option 93, length 2: 0
	    NDI Option 94, length 3: 1.2.1
	    GUID Option 97, length 17: 0.68.68.68.68.68.68.68.68.68.68.68.68.68.68.68.68
	    Vendor-Class Option 60, length 32: "PXEClient:Arch:00000:UNDI:002001"
	    END Option 255, length 0
16:44:41.224619 IP (tos 0x0, ttl 64, id 57713, offset 0, flags [none], proto UDP (17), length 372)
    192.168.1.1.67 > 192.168.1.139.68: [udp sum ok] BOOTP/DHCP, Reply, length 344, xid 0x26f30339, Flags [none] (0x0000)
	  Your-IP 192.168.1.139
	  Server-IP 192.168.1.1
	  Client-Ethernet-Address b8:27:eb:28:f6:6d
	  Vendor-rfc1048 Extensions
	    Magic Cookie 0x63825363
	    DHCP-Message Option 53, length 1: Offer
	    Server-ID Option 54, length 4: 192.168.1.1
	    Lease-Time Option 51, length 4: 43200
	    RN Option 58, length 4: 21600
	    RB Option 59, length 4: 37800
	    Subnet-Mask Option 1, length 4: 255.255.255.0
	    BR Option 28, length 4: 192.168.1.255
	    Vendor-Class Option 60, length 9: "PXEClient"
	    GUID Option 97, length 17: 0.68.68.68.68.68.68.68.68.68.68.68.68.68.68.68.68
	    Vendor-Option Option 43, length 32: 6.1.3.10.4.0.80.88.69.9.20.0.0.17.82.97.115.112.98.101.114.114.121.32.80.105.32.66.111.111.116.255
	    END Option 255, length 0
```

Vendor-Option Option 43 包含回复的重要部分。这部分必须包含字符串“Raspberry Pi Boot”。由于引导 ROM 中的一个错误，您可能需要在字符串末尾添加三个空格。

#### TFTP 文件读取

当正确指定供应商选项时，您将看到随后发送的 TFTP RRQ 数据包。 RRQ 可以通过数据的第一个块或错误消息（文件未找到）进行回复。在某些情况下，它们甚至会收到第一个数据包，然后传输会被树莓派中止（当检查文件是否存在时会发生这种情况）。下面的示例仅包括三个数据包：原始读取请求，第一个数据块（始终为 516 字节，包含标头和 512 字节数据，尽管最后一个块始终少于 512 字节，可能为零长度），以及第三个数据包（包含与数据块中的帧编号匹配的 ACK）。

```
16:44:41.224964 IP (tos 0x0, ttl 128, id 0, offset 0, flags [none], proto UDP (17), length 49)
    192.168.1.139.49152 > 192.168.1.1.69: [no cksum]  21 RRQ "bootcode.bin" octet
16:44:41.227223 IP (tos 0x0, ttl 64, id 57714, offset 0, flags [none], proto UDP (17), length 544)
    192.168.1.1.55985 > 192.168.1.139.49152: [udp sum ok] UDP, length 516
16:44:41.227418 IP (tos 0x0, ttl 128, id 0, offset 0, flags [none], proto UDP (17), length 32)
    192.168.1.139.49152 > 192.168.1.1.55985: [no cksum] UDP, length 4
```

### 已知问题

以太网引导模式存在一些已知问题。由于引导模式的实现在芯片本身中，除了使用仅包含 bootcode.bin 文件的 SD 卡外，没有其他解决方法。

#### DHCP 请求在五次尝试后超时

树莓派将尝试在五秒内进行五次 DHCP 请求，总共持续 25 秒。如果服务器在此时间内无法响应，则树莓派将进入低功耗状态。除了在 SD 卡上的 bootcode.bin 之外，没有其他解决方法。

#### 分开子网上的 TFTP 服务器不受支持

在树莓派 3 Model B+ (BCM2837B0) 中修复。

#### DHCP 中继损坏

DHCP 检查还检查跳数值是否为 1 ，而使用 DHCP 中继时不会是这个值。

在 树莓派 3 Model B+ 中修复。

#### 树莓派启动字符串

由于计算字符串长度时出错，“Raspberry Pi Boot”字符串在 DHCP 回复中需要额外的三个空格。

在 树莓派 3 Model B+ 中修复。

#### DHCP UUID 常量

DHCP UUID 被设置为一个常量值。

在 树莓派 3 Model B+ 中修复;该值设置为 32 位序列号。

#### ARP 检查可能在 TFTP 事务中间失败响应

当树莓派处于初始化阶段时，它只会响应 ARP 请求;只要开始传输数据，它将无法继续响应。

在树莓派 3 Model B+ 中修复。

#### DHCP 请求/回复/确认序列未正确实现

在引导时，树莓派广播 DHCPDISCOVER 数据包。DHCP 服务器以 DHCPOFFER 数据包回复。然后树莓派继续引导而不执行 DHCPREQUEST 或等待 DHCPACK。这可能导致两个不同的设备被提供相同的 IP 地址并在未正确分配给客户端的情况下使用它。

在这种情况下，不同的 DHCP 服务器有不同的行为。dnsmasq（取决于设置）将对 MAC 地址进行哈希处理以确定 IP 地址，并 ping 该 IP 地址以确保它尚未被使用。这降低了发生这种情况的几率，因为它需要在哈希中发生冲突。

## GPIO 引导模式

>**注意**
>
>GPIO 引导模式仅适用于 树莓派 3A+、3B、3B+、Compute Module 3 和 3+。 

旧版的树莓派可以配置，允许在使用连接到 GPIO 连接器的硬件时在上电时选择引导模式。这是通过在 SoC 的 OTP 存储器中设置位来完成的。如果设置了这些位，它们将永久地分配五个 GPIO 以允许进行此选择。如果设置了 OTP 位，它们就无法取消设置。在启用此功能时，您应该仔细考虑，因为这五个 GPIO 线将始终控制引导。虽然在树莓派启动后，您可以使用这些 GPIO 进行其他功能，但必须设置它们以使其在树莓派引导时启用所需的引导模式。

要启用 GPIO 引导模式，请将以下行添加到 config.txt 文件中：

```
program_gpio_bootmode=n
```

其中 n 是您希望使用的 GPIO 组。然后重新启动树莓派一次，以使用此设置对 OTP 进行编程。第 1 组是 GPIO 22-26，第 2 组是 GPIO 39-43。除非您使用的是计算模块，否则必须使用第 1 组：第 2 组中的 GPIO 仅在计算模块上可用。由于 OTP 位的排列方式，如果您首先为第 1 组编程 GPIO 引导模式，然后稍后可以选择第 2 组。反之则不成立：如果选择了第 2 组作为 GPIO 引导模式，就无法选择第 1 组。

倘若启用了 GPIO 引导模式，树莓派将不再启动。您必须拉高至少一个引导模式 GPIO 引脚，以便启动树莓派。

### 引脚分配

#### 树莓派 3B 和计算模块 3

| 引脚 1 | 引脚 2 | 引导类型                 |
| -------- | -------- | -------------------------- |
| 22     | 39     | SD0                      |
| 23     | 40     | SD1                      |
| 24     | 41     | NAND（目前不支持 Linux） |
| 25     | 42     | SPI（目前不支持 Linux）  |
| 26     | 43     | USB                      |

在上表中，USB 选择 USB 设备启动模式和 USB 主机启动模式。要使用 USB 启动模式，必须在 OTP 存储器中启用它。有关更多信息，请参阅 USB 设备启动和 USB 主机启动。

#### 旧版树莓派 3B（带金属盖的 BCM2837B0），树莓派 3A+，3B+ 和计算模块 3+

| 引脚 1 | 引脚 2 | 引导类型                  |
| -------- | -------- | --------------------------- |
| 20     | 37     | SD0                       |
| 21     | 38     | SD1                       |
| 22     | 39     | NAND（目前不支持 Linux）  |
| 23     | 40     | SPI（目前不支持 Linux）   |
| 24     | 41     | USB 设备                  |
| 25     | 42     | USB 主机 - 大容量存储设备 |
| 26     | 43     | USB 主机 - 以太网         |

>**注意**
>
>各种引导模式按照 GPIO 线的数字顺序尝试，即 SD0，然后 SD1，然后 NAND 等等。

### 引导流程

SD0 是 Broadcom SD 卡/MMC 接口。当 SoC 中的引导 ROM 运行时，它总是将 SD0 连接到内置的 microSD 卡槽。在带有 eMMC 设备的计算模块上，SD0 连接到该设备；在计算模块 Lite 上，SD0 可在边缘连接器上使用，并连接到 CMIO 扩展板中的 microSD 卡槽。SD1 是 Arasan SD 卡/MMC 接口，还能够支持 SDIO。所有具有内置无线局域网的树莓派型号都使用 SD1 通过 SDIO 连接到无线芯片。

GPIO 线上的默认拉电阻为 50KΩ，如 BCM2835 ARM 外围设备数据表第 102 页所述。建议使用 5KΩ的拉电阻来拉高 GPIO 线：这将使 GPIO 正常工作但不会消耗太多功率。

## NVMe SSD 引导

NVMe（非易失性内存表达）是通过 PCIe 总线访问外部存储的标准。您可以通过 Compute Module 4（CM4）IO 板或树莓派 5 上的 PCIe 插槽连接 NVMe 驱动器。通过一些额外的配置，您可以从 NVMe 驱动器引导。

### 先决条件

#### 硬件

* NVMe M.2 固态硬盘
* 从 PCIe 转换为 M.2 标准的适配器。
  * 对于树莓派 5，我们推荐使用 M.2 HAT+，它可以将树莓派的 PCIe FFC 插槽转换为 M 键接口。
  * 对于 CM4，请搜索"PCI-E 3.0 ×1 通道到 M.2 NGFF M 键 SSD NVMe PCI Express 适配器卡"。

要检查 NVMe 驱动器是否正确连接，请从另一个存储设备（如 SD 卡）引导您的树莓派，并运行 ls -l /dev/nvme* 。示例输出如下。

```
crw------- 1 root root 245, 0 Mar  9 14:58 /dev/nvme0
brw-rw---- 1 root disk 259, 0 Mar  9 14:58 /dev/nvme0n1
```

#### 软件

运行以下命令查看您正在运行的固件版本：

```
$ sudo rpi-eeprom-update
```

对于树莓派 5，您需要在 2023 年 12 月 6 日或之后发布的固件。

对于 CM4，NVMe 启动支持是在 2021 年 7 月引入的。您需要自那日期以来发布的以下软件版本：

* 引导加载程序
* VideoCore 固件
* Raspberry Pi OS Linux 内核

最新的 Raspberry Pi OS 发行版包含您所需的一切。使用 Raspberry Pi Imager 将 Raspberry Pi OS 镜像安装到您的驱动器上。

### 编辑 EEPROM 启动顺序

对于树莓派 5，您需要启动 Raspberry Pi OS 来编辑启动顺序。您可以从 SD 卡或 USB 驱动器引导您的树莓派进行此步骤。即使更改引导设备，EEPROM 配置也会持续存在，因为 EEPROM 配置存储在板上本身。

使用树莓派 配置 CLI 更新引导加载程序：

```
$ sudo raspi-config
```

在 Advanced Options > Bootloader Version 下，选择 Latest 。然后，使用 Finish 键或 Escape 键退出 raspi-config 。

运行以下命令以将固件更新到最新版本：

```
$ sudo rpi-eeprom-update -a
```

然后，使用 sudo reboot 重新启动。您的树莓派 5 应该从 NVMe 启动。

对于 CM4，请使用 rpiboot 来更新引导加载程序。您可以在 USB 启动 GitHub 存储库中找到构建 rpiboot 和配置 IO 板以将 ROM 切换到 usbboot 模式的说明。

对于带有 eMMC 的 CM4 版本，请确保您已将 NVMe 首选设置为启动顺序中的第一项。记得在 recovery/boot.conf 中将 NVMe 启动模式 6 添加到 BOOT_ORDER 中。

当 SD 卡槽为空时，CM4 Lite 会自动从 NVMe 启动。

### NVMe `BOOT_ORDER`

EEPROM 配置中的 BOOT_ORDER 设置控制引导行为。对于 NVMe 引导，请使用引导模式 6 。有关更多信息，请参阅树莓派引导加载程序配置。

### 示例

当引导加载程序检测到 NVMe 驱动器时，UART 输出的示例如下：

```
Boot mode: SD (01) order f64
Boot mode: USB-MSD (04) order f6
Boot mode: NVME (06) order f
VID 0x144d MN Samsung SSD 970 EVO Plus 250GB
NVME on
```

然后它将找到一个 FAT 分区并加载 start4.elf ：

```
Read start4.elf bytes  2937840 hnd 0x00050287 hash ''
```

然后它将加载内核并启动操作系统：

```
MESS:00:00:07.096119:0: brfs: File read: /mfs/sd/kernel8.img
MESS:00:00:07.098682:0: Loading 'kernel8.img' to 0x80000 size 0x1441a00
MESS:00:00:07.146055:0:[    0.000000] Booting Linux on physical CPU 0x0000000000 [0x410fd083]
```

在 Linux 中，SSD 显示为 /dev/nvme0 ，"namespace"显示为 /dev/nvme0n1 。将有两个分区 /dev/nvme0n1p1 （FAT）和 /dev/nvme0n1p2 （EXT4）。使用 lsblk 检查分区分配情况：

```
NAME        MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
nvme0n1     259:0    0 232.9G  0 disk
├─nvme0n1p1 259:1    0   256M  0 part /boot/firmware
└─nvme0n1p2 259:2    0 232.6G  0 part /
```

### 故障排除

如果启动过程失败，请在 rpi-eeprom GitHub 存储库上提交问题报告，确保附上控制台副本和启动过程中屏幕上显示的任何内容。

## HTTP 引导

网络安装功能使用以太网上的 HTTP 引导树莓派进入嵌入式树莓派 Imager。

除了网络安装，您还可以使用通过 HTTP 下载的文件显式引导设备，使用引导模式 7 。即使禁用了引导时的网络安装，您仍然可以使用此功能。

例如，您可以将此添加到您的 BOOT_ORDER 作为备用启动方法，或者将其放在 GPIO 条件之后，以在 GPIO 引脚被拉低时从您自己的服务器启动 HTTP 引导。

例如，如果您将以下内容添加到您的 EEPROM 配置和 GPIO 8（其默认状态为 1 或高电平）被拉低，文件 http://downloads.raspberrypi.org:80/net_install/boot.img 和 http://downloads.raspberrypi.org:80/net_install/boot.sig 将被下载。如果启用了启动时网络安装，它将使用相同的 URL。如果 GPIO 8 未被拉低，则行为将保持不变。

```
[gpio8=0]
BOOT_ORDER=0xf7
HTTP_HOST=downloads.raspberrypi.org
NET_INSTALL_ENABLED=0
```

boot.img 和 boot.sig 签名文件是包含引导文件系统的 RAM 磁盘。有关更多详细信息，请参阅 boot_ramdisk。

如果启用了安全启动并且未设置 HTTP_HOST，则 BOOT_ORDER 中的 HTTP 将被忽略。

### 要求

要使用 HTTP 引导，请更新到 2022 年 3 月 10 日或之后发布的引导加载程序。HTTP 引导需要有线以太网连接。

要使用自定义 CA 证书，请更新到 2024 年 4 月 5 日或之后发布的引导加载程序。只有运行 BCM2712 CPU 的设备支持自定义 CA 证书。

### 键

所有 HTTP 下载必须经过签名。引导加载程序包含默认主机 fw-download-alias1.raspberrypi.com 上文件的公钥。除非您设置 HTTP_HOST 并在 EEPROM 中包含公钥，否则将使用此密钥来验证网络安装映像。这使您可以在自己的服务器上托管树莓派网络安装映像。

>**警告**
>
>使用您自己的网络安装映像将需要您对映像进行签名并将您的公钥添加到 EEPROM 中。如果您之后应用公共 EEPROM 更新，您的密钥将丢失并需要重新添加。 

USBBOOT 具有编程公钥所需的所有工具。

```
# Add your PUBLIC key to the eeprom. boot.conf contains your modifications
rpi-eeprom-config -c boot.conf -p mypubkey.pem -o pieeprom.upd pieeprom.original.bin

# Generate signature for your eeprom
rpi-eeprom-digest -i pieeprom.upd -o pieeprom.sig

# Sign the network install image with your PRIVATE key
# Put boot.img and boot.sig on your web server
rpi-eeprom-digest -i boot.img -o boot.sig -k myprivkey.pem
```

### 证书

为了安全起见，网络安装使用 HTTPS 从 Raspberry Pi 网站下载 OS 映像。此功能使用我们自己的 CA 根证书包含在引导加载程序中，用于验证主机。

您可以将自己的自定义 CA 证书添加到设备的 EEPROM 中，以安全地从您自己的网站下载映像。使用 --cacertder 工具的 rpi-eeprom-config 选项添加 DER 编码的证书。您必须将证书的哈希放置在 EEPROM 配置设置中，以确保证书未被修改。

运行以下命令生成 DER 编码的证书：

```
$ openssl x509 -in your_ca_root_cert.pem -out cert.der -outform DER
```

然后，运行以下命令生成证书的 SHA-256 哈希：

```
$ sha256sum cert.der
```

您应该看到类似以下内容的输出：

```
701bd97f67b0f5483a9734e6e5cf72f9a123407b346088638f597878563193fc  cert.der
```

接下来，更新 boot.conf 以包含证书的哈希值：

```
$ sudo rpi-eeprom-config --edit
```

在 [gpio8=0] 部分配置以下设置，替换为：

* 使用您的网站替换 <your_website> ，例如 yourserver.org
* 使用您网站上托管的操作系统镜像路径替换 <path_to_files> ，例如 path/to/files
* 使用上面生成的哈希值 701bd97f67b0f5483a9734e6e5cf72f9a123407b346088638f597878563193fc ，例如 <hash>

```
[all]
BOOT_UART=1
POWER_OFF_ON_HALT=0
BOOT_ORDER=0xf461

[gpio8=0]
BOOT_ORDER=0xf7
NET_INSTALL_ENABLED=0
HTTP_HOST=<your_website>
HTTP_PATH=<path_to_files>
HTTP_CACERT_HASH=<hash>
```

当您指定一个 HTTP_CACERT_HASH 时，网络安装会通过端口 443 上的 HTTPS 下载镜像。没有哈希值时，网络安装会通过端口 80 上的 HTTP 下载镜像。

最后，使用以下命令将所有内容加载到 EEPROM 中：

```
$ rpi-eeprom-config -c boot.conf -p mypubkey.pem -o pieeprom.bin --cacertder cert.der pieeprom.original.bin
$ rpi-eeprom-digest -k myprivkey.pem -i pieeprom.bin -o pieeprom.sig
```

在网络引导期间，您的树莓派应该使用 HTTPS 而不是 HTTP。要查看由网络安装解析的完整 HTTPS URL 以进行下载，请检查引导输出：

```
Loading boot.img ...
HTTP: GET request for https://yourserver.org:443/path/to/files/boot.sig
HTTP: GET request for https://yourserver.org:443/path/to/files/boot.img
```

### 安全引导

如果启用了安全引导，则树莓派只能运行由客户私钥签名的代码。因此，如果您想要在启用安全引导的情况下使用网络安装或 HTTP 引导模式，您必须使用自己的密钥签署 boot.img 并生成 boot.sig ，并在某处托管这些文件以供下载。EEPROM 中的公钥将用于验证镜像。

如果启用了安全启动并且未设置 HTTP_HOST，则网络安装和 HTTP 引导将被禁用。

有关安全启动的更多信息，请参阅 USBBOOT 。

## 并行显示接口

##### [在树莓派上使用 DPI 显示器](https://pip.raspberrypi.com/categories/685-whitepapers-app-notes/documents/RP-003471-WP/Using-a-DPI-display.pdf)

在树莓派上使用 DPI 显示器

可以通过 40 针通用输入/输出(GPIO)连接器将 Display Parallel Interface (DPI)显示器连接到树莓派设备，作为使用专用 Display Serial Interface (DSI)或高清多媒体接口(HDMI)端口的替代方案。

所有带有 40 针排针和计算模块的树莓派主板上都提供了高达 24 位并行 RGB 接口。该接口允许将并行 RGB 显示器连接到树莓派 GPIO，无论是以 RGB24（每色 8 位红、绿和蓝）还是 RGB666（每色 6 位）或 RGB565（5 位红、6 位绿和 5 位蓝）的形式。

该接口由 GPU 固件控制，并可以通过用户通过特殊 config.txt 参数和启用正确的 Linux 设备树叠加来进行编程。

### GPIO 引脚

树莓派 GPIO 第 0 银行可选择的一个备用功能是 DPI（显示并行接口），这是一个简单的时钟并行接口（最多 8 位的 R、G 和 B；时钟、使能、水平同步和垂直同步）。此接口在 GPIO 第 0 银行上作为备用功能 2（ALT2）可用：

| GPIO   | ALT2      |
| -------- | ----------- |
| GPIO0  | PCLK      |
| GPIO1  | DE        |
| GPIO2  | LCD_VSYNC |
| GPIO3  | LCD_HSYNC |
| GPIO4  | DPI_D0    |
| GPIO5  | DPI_D1    |
| GPIO6  | DPI_D2    |
| GPIO7  | DPI_D3    |
| GPIO8  | DPI_D4    |
| GPIO9  | DPI_D5    |
| GPIO10 | DPI_D6    |
| GPIO11 | DPI_D7    |
| GPIO12 | DPI_D8    |
| GPIO13 | DPI_D9    |
| GPIO14 | DPI_D10   |
| GPIO15 | DPI_D11   |
| GPIO16 | DPI_D12   |
| GPIO17 | DPI_D13   |
| GPIO18 | DPI_D14   |
| GPIO19 | DPI_D15   |
| GPIO20 | DPI_D16   |
| GPIO21 | DPI_D17   |
| GPIO22 | DPI_D18   |
| GPIO23 | DPI_D19   |
| GPIO24 | DPI_D20   |
| GPIO25 | DPI_D21   |
| GPIO26 | DPI_D22   |
| GPIO27 | DPI_D23   |

>**注意**
>
>DPI 输出引脚上的颜色值可以以 565、666 或 24 位模式的各种方式呈现（请参阅以下表格和 output_format 参数的 dpi_output_format 部分）：
| **模式** | **RGB 位** | **GPIO**  |
| ----------- | ------------- | --- |
| **27**          | **26**            | **25**  |
| 1         | -           | - |
| 2         | 565         | - |
| 3         | 565         | - |
| 4         | 565         | - |
| 5         | 666         | - |
| 6         | 666         | - |
| 7         | 888         | 7 |

### 禁用其他 GPIO 外围设备

必须禁用所有使用冲突 GPIO 引脚的其他外围叠加层。在 config.txt 中，务必注释掉或反转任何启用 I2C 或 SPI 的 dtparams：

```
dtparam=i2c_arm=off
dtparam=spi=off
```

### 配置显示器

内核模式设置（KMS）通用显示接口使输出到任意显示器成为可能，只要您有适当的驱动程序。

#### 自动检测

自动检测允许您的树莓派在不需要手动配置设备树叠加的情况下连接显示器。自动检测默认情况下已启用。您可以通过将以下行添加到 config.txt 来启用显示器自动检测：

```
`display_auto_detect=1`
```

用 0 替换 1 以禁用自动检测。当您连接启用自动检测的官方树莓派显示器时，KMS 会自动确定显示器型号并配置适当的显示设置。

#### 手动配置显示器

>**注意**
>
>在 Raspberry Pi OS Bookworm 或更高版本中，以前用于设置 DPI 的 dpi_output_format 和 dpi_timings 条目在 config.txt 中已被 vc4-kms-dpi-generic 覆盖。 

要使用官方树莓派显示器之外的任何显示器，必须在 config.txt 中指定一个 dtoverlay 条目。面板制造商应在 Linux 内核代码中为您的显示器配置时间，并提供一个覆盖来启用这些设置。请参阅 Adafruit Kippah 显示器条目以获取示例。以下示例演示了如何在您的 /boot/firmware/config.txt 文件中为 Kippah 显示器设置 dtoverlay 条目：

```
dtoverlay=vc4-kms-kippah-7inch-overlay
```

显示定时通常在内核中定义，但您也可以在提供的 panel-dpi 驱动程序中定义它们。如果您的面板在内核代码中缺乏定义的覆盖，您可以使用 panel-dpi 驱动程序将显示定时作为参数定义。这使您能够为任何显示器手动配置设备树条目。

以下示例演示了如何使用设备树参数定义时间：

```
dtoverlay=vc4-kms-v3d
dtoverlay=vc4-kms-dpi-generic,hactive=480,hfp=26,hsync=16,hbp=10
dtparam=vactive=640,vfp=25,vsync=10,vbp=16
dtparam=clock-frequency=32000000,rgb666-padhi
```

>**注意**
>
>设备树行长度不得超过 80 个字符。当设置需要超过 80 个字符的行时，请将该参数的赋值拆分成多行。 

参数显示树定义支持以下选项：

| 选项 | 说明                                               |
| ------ | ---------------------------------------------------- |
| `clock-frequency`     | 显示时钟频率 (Hz)                                  |
| `hactive`     | 水平活动像素                                       |
| `hfp`     | 水平前廊                                           |
| `hsync`     | 水平同步脉冲宽度                                   |
| `hbp`     | 水平背廊                                           |
| `vactive`     | 垂直活动线                                         |
| `vfp`     | 垂直前廊                                           |
| `vsync`     | 垂直同步脉冲宽度                                   |
| `vbp`     | 垂直后肩                                           |
| `hsync-invert`     | 水平同步低电平                                     |
| `vsync-invert`     | 垂直同步低电平                                     |
| `de-invert`     | 数据使能低电平                                     |
| `pixclk-invert`     | 负边沿像素时钟                                     |
| `width-mm`     | 在毫米中定义屏幕宽度                               |
| `height-mm`     | 在毫米中定义屏幕高度                               |
| `rgb565`     | 在 GPIOs 0-19 上更改为 RGB565 输出                 |
| `rgb666-padhi`     | 在 GPIO 0-9、12-17 和 20-25 上更改为 RGB666 输出   |
| `rgb888`     | 在 GPIO 0-27 上更改为 RGB888 输出                  |
| `bus-format`     | 覆盖 MEDIA_BUS_FMT_*值的总线格式，也被 rgbXXX 覆盖 |
| `backlight-gpio`     | 定义要用于背光控制的 GPIO（默认值：无）            |

## 通用输入/输出（GPIO）

通用输入/输出（GPIO）引脚可配置为通用输入、通用输出，或者作为最多六个特殊备用设置之一，其功能取决于引脚。

BCM2835 上有三个 GPIO bank。每个 bank 都有自己的 VDD 输入引脚。在树莓派上，所有 GPIO bank 都由 3.3V 供电。

>**警告**
>
>将 GPIO 连接到高于 3.3V 的电压可能会摧毁 SoC 内部的 GPIO 块。

在树莓派的 P1 引脚上提供了来自 Bank 0 的引脚选择。

### GPIO 引脚

BCM2835 封装上的 GPIO 连接有时在外设数据表中被称为“pads” — 一种半导体设计术语，意思是“芯片连接到外部世界”。

这些 pads 是可配置的 CMOS 推挽输出驱动器/输入缓冲器。可用于基于寄存器的控制设置：

* 内部上拉/下拉使能/禁用
* 输出驱动强度
* 输入施密特触发滤波

#### 通电状态

所有 GPIO 引脚在上电复位时恢复为通用输入。还应用了默认的拉电流状态，这些状态在 Arm 外设数据表的备用功能表中有详细说明。大多数 GPIO 引脚都有默认的拉电流状态。

### 中断

当配置为通用输入时，每个 GPIO 引脚可以配置为 Arm 的中断源。可配置多个中断生成源：

* 电平敏感（高/低）
* 上升/下降沿
* 异步上升/下降沿

等级中断会保持中断状态，直到系统软件清除了该等级（例如，通过为生成中断的附加外围设备提供服务）。

正常的上升/下降沿检测在检测中具有少量的同步。在系统时钟频率下，引脚在三个周期窗口内进行采样，生成中断的标准是在稳定的转换中，即记录为 1 0 0 或 0 1 1。异步检测绕过此同步，以便检测非常窄的事件。

### 替代功能

几乎所有的 GPIO 引脚都有替代功能。 SoC 内部的外围模块可以选择出现在一组 GPIO 引脚中的一个或多个上，例如，I2C 总线可以配置为至少三个单独的位置。 当引脚配置为替代功能时，仍然适用 Pad 控制，如驱动强度或施密特触发。

### 电压规格

下表列出了针对 BCM2835、BCM2836、BCM2837 和 RP3A0 系列产品（例如树莓派 Zero 或树莓派 3+）的 GPIO 引脚的各种电压规格。有关计算模块的信息，请参阅相关数据表。

| 符号   | 参数          | 条件        | 最小 | 典型 | 最大 | 单元   |
| -------- | --------------- | ------------- | ------ | ------ | ------ | -------- |
| V~IL~  | 输入低电压    | -           | -    | -    | 0.9  | V      |
| V~IH~  | 输入高电压^a^ | -           | 1.6  | -    | -    | V      |
| 我~IL~ | 输入泄漏电流  | TA = +85◦C | -    | -    | 5    | 微安   |
| C~IN~  | 输入电容      | -           | -    | 5    | -    | pF     |
| V~OL~  | 输出低电压^b^ | IOL = -2mA  | -    | -    | 0.14 | V      |
| V~OH~  | 输出高电压^b^ | IOH = 2mA   | 3.0  | -    | -    | V      |
| I~OL~  | 输出低电流^c^ | 电压 = 0.4V | 18   | -    | -    | 毫安   |
| I~OH~  | 输出高电流^c^ | VO = 2.3V   | 17   | -    | -    | 毫安   |
| 上拉   | 上拉电阻      | -           | 50   | -    | 65   | 千欧姆 |
| 树莓派 | 下拉电阻      | -           | 50   | -    | 65   | 千欧姆 |

^a^ 滞后启用 ^b^ 默认驱动强度（8mA） ^c^ 最大驱动强度（16mA）

下表列出了基于 BCM2711 的产品（例如树莓派 4 和树莓派 400）的 GPIO 引脚的电压规格。有关计算模块的信息，您应查看相关的数据表。

| 符号       | 参数          | 条件          | 最小值 | 典型的 | 最大 | 单位 |
| ------------ | --------------- | --------------- | -------- | -------- | ------ | ------ |
| 输入低电压 | 输入低电压    | -             | -      | -      | 0.8  | V    |
| 输入高电压 | 输入高电压^a^ | -             | 2.0    | -      | -    | V    |
| I~IL~      | 输入漏电流    | TA = +85℃    | -      | -      | 10   | 微安 |
| V~OL~      | 输出低电压^b^ | IOL = -4 毫安 | -      | -      | 0.4  | V    |
| V~OH~      | 输出高电压^b^ | IOH = 4 毫安  | 2.6    | -      | -    | V    |
| I~OL~      | 输出低电流^c^ | VO = 0.4V     | 7      | -      | -    | 毫安 |
| 我~氧化氢~ | 输出高电流^c^ | VO = 2.6 伏   | 7      | -      | -    | 毫安 |
| R~PU~      | 上拉电阻      | -             | 33     | -      | 73   | kΩ  |
| R~PD~      | 下拉电阻      | -             | 33     | -      | 73   | kΩ  |

^a^ 磁滞启用 ^b^ 默认驱动强度 (4mA) ^c^ 最大驱动强度 (8mA)

## GPIO 引脚控制

GPIO 驱动强度并不表示最大电流，而是在该电流下垫还能满足规格要求。您应该设置 GPIO 驱动强度以匹配所连接的设备，以确保设备能正常工作。

### 驱动强度是如何控制的

在垫子内部有许多并联的驱动器。如果驱动强度设置低（0b000），则大多数驱动器都是三态的，因此它们不会对输出电流产生影响。如果增加驱动强度，将会并联更多驱动器。图表显示了这种行为。

>**警告**
>
>对于树莓派 4、树莓派 400 和计算模块 4，当前级别是图表中显示值的一半。


![GPIO drive strength diagram](https://www.raspberrypi.com/documentation/computers/images/pi_gpio_drive_strength_diagram.png)

### 当前值代表什么意思？

>**注意**
>
>当前值指定了在该值以下的最大电流下，焊盘仍将符合规格。

* 当前值不是垫子将提供的电流，也不是电流限制。

垫子输出是电压源：

* 如果设置为高电平，垫子将尝试将输出驱动到电压轨（3.3V）
* 如果设置为低电平，则该引脚将尝试将输出引脚接地（0V）

该引脚将尝试将输出引脚驱动至高电平或低电平。成功取决于连接的要求。如果该引脚短接到地，它将无法驱动至高电平。它将尝试提供尽可能多的电流，电流仅受内部电阻限制。

如果该引脚被驱动至高电平并短接到地，它将在适当的时间内失效。如果将其连接到 3.3V 并驱动至低电平，情况也是如此。

符合规范取决于保证的电压电平。由于垫是数字的，有两个电压电平，高电平和低电平。I/O 端口有两个参数，用于处理输出电平：

* V~OL~，最大低电平电压（3.3V VDD IO 时为 0.14V）
* V~OH~，最小高电平电压（3.3V VDD IO 时为 3.0V）

V~OL~=0.14V 意味着如果输出为低，则<= 0.14V。V~OH~=3.0V 意味着如果输出为高，则>= 3.0V。

例如，16mA 的驱动强度意味着如果您将引脚设置为高，可以吸取高达 16mA，并且输出电压保证>=V~OH~。这也意味着如果您设置为 2mA 的驱动强度并吸取 16mA，则电压将不会是 V~OH~而是更低。实际上，它可能不够高，无法被外部设备视为高电平。

GPIO 引脚的物理特性有更多信息。

>**注意**
>
>在计算模块设备上，可以将 VDD IO 从标准的 3.3V 更改。在这种情况下，V~OL~和 V~OH~将根据 GPIO 部分的表格进行更改。


### 为什么我不能将所有引脚都设置为最大电流？

* 树莓派 3.3V 供电设计时每个 GPIO 引脚的最大电流为~3mA。如果您将每个引脚负载为 16mA，则总电流为 272mA。3.3V 供电将在该负载水平下崩溃。
* 大电流峰值将会发生，特别是在具有电容负载时。峰值将在附近的所有其他引脚之间反弹。这很可能会干扰 SD 卡，甚至 SDRAM 的行为。

### 什么是安全电流？

所有电路板的电子元件设计为 16mA。这是一个安全值，不会损坏设备。即使您将驱动强度设置为 2mA，然后负载使其输出 16mA，也不会损坏设备。除此之外，没有保证的最大安全电流。

### GPIO 地址

* 0x 7e10 002c PADS（GPIO 0-27）
* 0x 7e10 0030 PADS（GPIO 28-45）
* 0x 7e10 0034 PADS（GPIO 46-53）

| 位    | 字段名称 | 说明                              | 类型 | 重置 |
| ------- | ---------- | ------------------------------------ | ------ | ------ |
| 31:24 | PASSWRD  | 写入时必须为 0x5A；意外写保护密码  | W    | 0    |
| 23:5  |          | 保留 - 写为 0，读取时不关心        |      |      |
| 4     | SLEW     | 斜率；0 = 斜率受限；1 = 斜率不受限 | RW   | 1    |
| 3     | HYST     | 启用输入滞后; 0 = 禁用; 1 = 启用   | RW   | 1    |
| 2:0   | DRIVE    | 驱动强度，请参见下面的列表         | RW   | 3    |

要注意同时切换输出（SSO）的限制，这些限制取决于设备，还取决于 PCB 的质量和布局，去耦电容的数量和质量，焊盘上的负载类型（电阻，电容）以及树莓派无法控制的其他因素。

### 驱动强度列表

* 0 = 2 毫安
* 1 = 4 毫安
* 2 = 6 毫安
* 3 = 8 毫安
* 4 = 10 毫安
* 5 = 12 毫安
* 6 = 14 毫安
* 7 = 16 毫安

## 树莓派的工业用途

树莓派经常作为另一产品的一部分使用。本文档描述了一些额外的功能，可用于使用树莓派的其他功能。

### 一次性可编程设置

##### [在树莓派单板计算机上使用一次性可编程存储器](https://pip.raspberrypi.com/categories/685-whitepapers-app-notes/documents/RP-003611-WP/Using-the-One-time-programmable-memory-on-Raspberry-Pi-single-board-computers.pdf)

在树莓派单板计算机上使用一次性可编程存储器

所有树莓派单板计算机（SBCs）都有一个内置的一次性可编程（OTP）存储器区域，实际上是主 SoC 的一部分。正如其名称所示，OTP 存储器只能写入一次（即，二进制 0 可以更改为 1）。只要某个位被更改为 1，就永远无法恢复为 0。看待 OTP 的一种方式是将每个位视为保险丝。编程涉及故意烧断保险丝 - 这是一个不可逆的过程，因为您无法进入芯片内部进行更换！

本白皮书假定树莓派正在运行 Raspberry Pi OS，并且已完全更新到最新的固件和内核。

有许多可以使用的 OTP 值。要查看所有 OTP 值的列表，您可以使用：

```
vcgencmd otp_dump
```

从此转储中提取的一些有趣行。

* 28 - 序列号
* 29 - 序列号的补码
* 30 - 板子修订号

此外，在 36 到 43（包括）之间，有八行 32 位可供客户使用。

>**注意**
>
>在 BCM2712 设备上，这些数字是不同的。第 31 行是序列号，第 32 行是板子修订号。客户行是 77 到 84（包括）。 

这些行中的一些可以使用 vcmailbox 进行编程。这是一个 Linux 驱动程序接口，用于处理行的编程。要做到这一点，请参考文档和 vcmailbox 示例应用程序。

vcmailbox 应用程序可以直接从 Raspberry Pi OS 命令行中使用。一个示例用法是：

```
vcmailbox 0x00010004 8 8 0 0
```

…将返回类似以下内容：

```
0x00000020 0x80000000 0x00010004 0x00000008 0x800000008 0xnnnnnnnn 0x00000000 0x00000000
```

以上使用邮箱属性接口 GET_BOARD_SERIAL ，请求大小为 8 字节，响应大小为 8 字节（发送两个整数作为请求 0, 0）。对此的响应将是两个整数（0x00000020 和 0x80000000），后跟标签代码、请求长度、响应长度（第 31 位设置为指示它是响应），然后是 64 位序列号（其中 MS 32 位始终为 0）。

### 编写和读取客户 OTP 值

>**警告**
>
>OTP 值是一次性可编程的。如果将位从 0 更改为 1，就无法再更改回来。 

要设置客户 OTP 值，您需要使用 SET_CUSTOMER_OTP （0x38021）标记，如下所示：

```
vcmailbox 0x00038021 [8 + number * 4] [8 + number * 4] [start_num] [number] [value] [value] [value] ...
```

* start_num = 从 0-7 编程的第一行
* number = 要编程的行数
* value = 要编程的每个值

因此，要将 OTP 客户行 4、5 和 6 编程为分别为 0x11111111、0x22222222、0x33333333，您可以使用：

```
vcmailbox 0x00038021 20 20 4 3 0x11111111 0x22222222 0x33333333
```

然后将编程行 40、41 和 42。

要读取值，您可以使用：

```
vcmailbox 0x00030021 20 20 4 3 0 0 0
```

 这应该显示:

```
0x0000002c 0x80000000 0x00030021 0x00000014 0x80000014 0x00000000 0x00000003 0x11111111 0x22222222 0x33333333
```

如果您想将此功能集成到您自己的代码中，您应该能够通过使用 vcmailbox.c 代码作为示例来实现这一点。

### 在非 BCM2712 设备上锁定 OTP

可以锁定 OTP 更改，以避免它们被再次编辑。

可以使用 OTP 写邮箱的特殊参数来完成此操作：

```
vcmailbox 0x00038021 8 8 0xffffffff 0xaffe0000
```

只要锁定，客户的 OTP 值将无法再被更改。请注意，此锁定操作是不可逆转的。

### 在 BCM2712 设备上锁定 OTP

可以使用以下命令将客户区域标记为只读。

```
vcmailbox 0x00030086 4 4 0
```

OTP 仅在设备重置时被锁定，因此需要在每次启动时重新应用 OTP 锁定。

### 在非 BCM2712 设备上使客户 OTP 位不可读

可以通过在 OTP 写邮箱中使用特殊参数来完全阻止读取客户 OTP 位。

```
vcmailbox 0x00038021 8 8 0xffffffff 0xaffebabe
```

这个操作对绝大多数用户来说可能没有用，而且是不可逆转的。

### 在 BCM2712 设备上的客户 MAC 地址

在 BCM2712 设备上，以太网、Wi-Fi 和蓝牙 MAC 地址设置在 OTP 存储器中。这些值可以随客户值而更改。

获取客户 MAC 地址 vcmailbox 0x00030082/3/4 6 6 0 0 ，其中 2 是以太网，3 是 Wi-Fi，4 是蓝牙。

 例子…

```
vcmailbox 0x00030083 6 6 0 0
0x00000020 0x80000000 0x00030083 0x00000006 0x80000006 0xddccbbaa 0x0000ffee 0x00000000
```

为了设置客户端 MAC 地址，必须将其作为两个 32 位字发送，字节顺序正确。您可以运行一个命令来检查它是否格式正确。

 例子…

```
vcmailbox 0x00030085 6 6 0x44332211 0x6655
```

检查日志，查看 MAC 地址是否符合预期。

```
sudo vclog -m
1057826.701: read mac address 11:22:33:44:55:66
```

多播地址不被视为有效。MAC 地址中最重要的八位中最不重要的位是多播位，因此请确保未设置该位。

然后可以使用命令 vcmailbox 0x00038082/3/4 6 6 <row1> <row0> 设置客户端 MAC。

 示例...

```
vcmailbox 0x00038082 6 6 0x44332211 0x6655
```

如果客户 MAC 地址设置为 ff:ff:ff:ff:ff:ff，则会被忽略。

### 设备特定的私钥

使用 Broadcom BCM2712 处理器的设备具有 16 行 OTP 数据（512 位），以支持文件系统加密。不使用 BCM2712 的设备可用 8 行 OTP（256 位）作为设备特定私钥。

可以使用类似于用于管理客户 OTP 行的 vcmailbox 命令来编程和读取这些行。如果不需要安全启动/文件系统加密，则设备私钥行可用于存储通用信息。

* 设备私钥行只能通过 vcmailbox 命令读取，该命令需要访问 /dev/vcio ，该访问受限于 Raspberry Pi OS 上的 video 组。
* 树莓派计算机没有硬件保护的密钥存储。建议与安全启动一起使用此功能，以限制对这些数据的访问。
* 树莓派 OS 不支持加密的根文件系统。

有关开源磁盘加密的更多信息，请参阅 Cryptsetup。

#### 键编程脚本 rpi-otp-private-key

该 rpi-otp-private-key 脚本包装了设备私钥 vcmailbox API，使得在 OpenSSL 格式中更易于读写密钥。

>**注意**
>
>该 usbboot 存储库包含您需要的所有工具，包括 rpi-eeprom 作为 Git 子模块。

将 32 字节密钥读取为 64 字符十六进制数：

```
cd usbboot/tools
rpi-otp-private-key
```

 示例输出：

```
f8dbc7b0a4fcfb1d706e298ac9d0485c2226ce8df7f7596ac77337bd09fbe160
```

将 32 字节随机生成的数字写入设备私钥。

>**警告**
>
>该操作无法撤销。

```
# rpi-otp-private-key -w $(openssl rand -hex 32)
```

>**注意**
>
>要指定要使用的 OTP 行数，请传递 -l <word count> 。要指定密钥存储中的起始位置，请传递 `-o <word offset>` 。 

#### 用于读取/写入密钥的邮箱 API。

阅读所有行。

```
vcmailbox 0x00030081 40 40 0 8 0 0 0 0 0 0 0 0
```

 示例输出：

```
0x00000040 0x80000000 0x00030081 0x00000028 0x80000028 0x00000000 0x00000008 0xf8dbc7b0 0xa4fcfb1d 0x706e298a 0xc9d0485c 0x2226ce8d 0xf7f7596a 0xc77337bd 0x09fbe160 0x00000000
```

写入所有行（用关键数据替换末尾的八个零）：

```
vcmailbox 0x00038081 40 40 0 8 0 0 0 0 0 0 0 0
```

在上一个示例中写下显示的密钥：

```
vcmailbox 0x38081 40 40 0 8 0xf8dbc7b0 0xa4fcfb1d 0x706e298a 0xc9d0485c 0x2226ce8d 0xf7f7596a 0xc77337bd 0x09fbe160
```

## OTP 寄存器和位定义

树莓派系列使用的所有 SoC 都具有内置的一次性可编程 (OTP) 存储器块。少数位置具有出厂编程数据。

 OTP 存储器大小：

* 非 BCM2712 设备：66 个 32 位值
* BCM2712 设备：192 个 32 位值

用于显示 OTP 内容的 vcgencmd 是：

```
vcgencmd otp_dump
```

### 非 BCM2712 设备上的 OTP 寄存器

此列表包含寄存器的公开信息。如果某个寄存器或位未在此处定义，则表示其不是公开的。

16 OTP 控制寄存器 - BCM2711

* 位 26：禁用 VC JTAG
* 位 27：禁用 VC JTAG

  17 引导模式寄存器

* 位 1：将振荡器频率设置为 19.2MHz
* 位 3：启用 SDIO 引脚上的上拉电阻
* 位 15：禁用 ROM RSA 密钥 0 -（如果设置，则启用安全启动）（BCM2711）
* 位 19：启用 GPIO 引导模式
* 位 20：设置要检查 GPIO 引导模式的银行
* 位 21：启用从 SD 卡引导
* 位 22：设置要引导的银行
* 位 28：启用 USB 设备引导
* 位 29：启用 USB 主机引导（以太网和大容量存储）

>**注意**
>
>在 BCM2711 上，引导模式由引导加载程序 EEPROM 配置定义，而不是 OTP。 

18 引导模式寄存器的副本

  28 序列号

  29 ~(序列号)

30 修订代码 ^1^

33 板上修订版扩展 - 其含义取决于板型。这可通过设备树在 /proc/device-tree/chosen/rpi-boardrev-ext 中获得，出于测试目的，可以通过在 config.txt 中设置 board_rev_ext 来临时覆盖此 OTP 值。

* 计算模块 4
  * 位 30：计算模块是否安装了 Wi-Fi 模块
    * 0 - 无线网络
    * 1 - 无 Wi-Fi
  * 位 31: 计算模块是否安装了 EMMC 模块
    * 0 - EMMC
    * 1 - 无 EMMC（精简版）
* 树莓派 400
  * 位 0-7：piwiz 使用的默认键盘国家代码
36-43 客户 OTP 值

  45 MPG2 解码密钥

  46 WVC1 解码密钥


47-54 用于安全启动的 RSA 公钥的 SHA256

55 安全启动标志（由引导加载程序保留使用）

56-63 256 位设备特定私钥

64-65 MAC 地址；如果设置，系统将优先使用此地址，而不是基于序列号自动生成的地址

66 高级引导寄存器（非 BCM2711）

* 位 0-6：ETH_CLK 输出引脚的 GPIO
* 位 7：启用 ETH_CLK 输出
* 位 8-14：LAN_RUN 输出引脚的 GPIO
* 位 15：启用 LAN_RUN 输出
* 位 24：延长 USB HUB 超时参数
* 位 25：ETH_CLK 频率:
  * 0 - 25MHz
  * 1 - 24MHz

^1^还包含用于禁用过压、OTP 编程和 OTP 读取的位。

### BCM2712 设备上的 OTP 寄存器

此列表包含寄存器的公开信息。如果某个寄存器或位未在此处定义，则其不是公开的。

  22 引导模式寄存器

* 位 1：从 SD 卡启动
* 位 2-4：从 SPI EEPROM 启动（以及使用的 GPIO）
* 位 10：禁用从 SD 卡启动
* 位 11: 禁用从 SPI 引导
* 位 12: 禁用从 USB 引导

23 引导模式寄存器的副本

  29 高级引导模式

* 位 0-7：用于 SD 卡检测的 GPIO
* 位 8-15：用于 RPIBOOT 的 GPIO

31 序列号的低 32 位

  32 主板版本

33 主板属性 - 其含义取决于主板型号。这可通过设备树在 /proc/device-tree/chosen/rpi-boardrev-ext 中获取

35 序列号的高 32 位 完整的 64 位序列号可在 /proc/device-tree/serial-number 中找到

50-51 以太网 MAC 地址 这将传递到设备树中的操作系统，例如 /proc/device-tree/axi/pcie@120000/rp1/ethernet@100000/local-mac-address

52-53 Wi-Fi MAC 地址 这将传递到设备树中的操作系统，例如 /proc/device-tree/axi/mmc@1100000/wifi@1/local-mac-address

54-55 蓝牙 MAC 地址 这是传递给操作系统的设备树中的内容，例如 /proc/device-tree/soc/serial@7d50c000/bluetooth/local-bd-address

77-84 客户 OTP 值

86board 国家 - piwiz 使用的默认键盘国家代码 如果设置，可通过设备树在 /proc/device-tree/chosen/rpi-country-code 中获取

87-88 客户以太网 MAC 地址，如果设置，将覆盖 OTP 行 50-51

89-90 客户 Wi-Fi MAC 地址，如果设置，将覆盖 OTP 行 52-53

89-90 客户蓝牙 MAC 地址，如果设置，将覆盖 OTP 行 54-55

109-114 工厂设备 UUID 目前是一个 16 位数字 id，应与设备上的条形码匹配。使用零字符填充并进行 c40 编码。

通过设备树在 /proc/device-tree/chosen/rpi-duid 中可用。

## 树莓派连接器用于 PCIe

![Raspberry Pi connector for PCIe](https://www.raspberrypi.com/documentation/computers/images/pcie.jpg)

树莓派连接器用于 PCIe

树莓派 5 在板的右侧有一个 FPC 连接器。该连接器为快速外围设备提供了一个 PCIe Gen 2.0 ×1 接口。

要连接 PCIe HAT+设备，请将其连接到您的树莓派。您的树莓派应该会自动检测到该设备。要连接非 HAT+设备，请将其连接到您的树莓派，然后手动启用 PCIe。

有关 PCIe FPC 连接器引脚布局及创建第三方设备、配件和 HAT 所需的其他详细信息，请参阅 Raspberry Pi Connector for PCIe 标准文档。应与 Raspberry Pi HAT+ 规范一起阅读。

>**注意**
>
>目前不支持枚举位于交换机后面的 PCIe 设备。 

### 启用 PCIe

默认情况下，除非连接到 HAT+ 设备，否则 PCIe 连接器不会被启用。要启用连接器，请将以下行添加到 /boot/firmware/config.txt ：

```
dtparam=pciex1
```

使用 sudo reboot 重新启动，以使配置更改生效。

>**注意**
>
>您还可以使用别名 nvme 。 

### 从 PCIe 启动

默认情况下，树莓派设备不会从 PCIe 存储启动。要启用从 PCIe 启动，请更改引导加载程序配置中的 BOOT_ORDER 。使用以下命令编辑 EEPROM 配置：

```
$ sudo rpi-eeprom-config --edit
```

用以下行替换 BOOT_ORDER 行：

```
BOOT_ORDER=0xf416
```

要从非 HAT+ 设备启动，请添加以下行：

```
PCIE_PROBE=1
```

保存更改后，使用 sudo reboot 重新启动您的树莓派以更新 EEPROM。

### PCIe Gen 3.0

>**警告**
>
>树莓派 5 未获 Gen 3.0 速度认证。PCIe Gen 3.0 连接可能不稳定。 

#### 通过 config.txt

该连接已获得 Gen 2.0 速度认证（5 GT/sec），但您可以强制使用 Gen 3.0（10 GT/sec）速度。要启用 PCIe Gen 3.0 速度，请将以下行添加到 /boot/firmware/config.txt ：

```
dtparam=pciex1_gen=3
```

使用 sudo reboot 重新启动您的树莓派以使这些设置生效。

#### 通过 raspi-config

运行以下命令以打开树莓派配置 CLI：

```
$ sudo raspi-config
```

完成以下步骤以启用 PCIe Gen 3.0 速度：

1. 选择 Advanced Options 。
2. 选择 PCIe Speed 。
3. 选择 Yes 以启用 PCIe Gen 3 模式。
4. 选择 Finish 以退出。

使用 sudo reboot 重新启动您的树莓派，以使这些设置生效。

## 电源按钮

>**注意**
>
>本节仅适用于带有电源按钮的树莓派型号，例如树莓派 5。 

当您首次将树莓派插入电源时，它将自动打开并启动操作系统，无需按按钮。

如果您运行 Raspberry Pi Desktop，则可以通过简短按下电源按钮来启动干净的关机。 一个窗口将出现，询问您是否要关机、重新启动或注销。

选择一个选项或再次按下电源按钮以启动干净的关机。

>**注意**
>
>如果您运行 Raspberry Pi Desktop，则可以快速连续按两次电源按钮来关闭。 如果您运行没有桌面的 Raspberry Pi OS Lite，请按一次电源按钮来启动关机。

### 重新启动

如果树莓派主板已关闭，但仍连接电源，则按下电源按钮会重新启动主板。

>**注意**
>
>重置电源管理集成电路（PMIC）也可以重新启动主板。连接 HAT 可以重置 PMIC。在连接 HAT 之前，始终将设备与电源断开连接。 

### 强制关机

要强制关机，请按住电源按钮。

### 添加您自己的电源按钮

![The J2 jumper on Raspberry Pi 5](https://www.raspberrypi.com/documentation/computers/images/j2.jpg)

 J2 跳线

J2 跳线位于 RTC 电池连接器和板边之间。这个引脚允许您通过添加一个常开（NO）瞬时开关来为树莓派 5 添加自己的电源按钮。简短地关闭此开关将执行与板载电源按钮相同的操作。

## 电源供应

树莓派型号的电源供应要求有所不同。所有型号都需要 5.1V 的供应，但根据型号，所需的电流通常会增加。直到树莓派 3 型号，所有型号都需要一个 micro USB 电源连接器，而树莓派 4、树莓派 400 和树莓派 5 使用 USB-C 连接器。

每个树莓派耗的电流取决于连接的外围设备。

### 推荐的电源供应

对于树莓派 1、树莓派 2 和 树莓派 3，我们建议使用 2.5A 微型 USB 电源适配器。对于树莓派 4 和树莓派 400，我们建议使用 3A USB-C 电源适配器。对于树莓派 5，我们建议使用 27W USB-C 电源适配器。

>**注意**
>
>所有型号的树莓派都不支持 USB-PPS。 

>**注意**
>
>如果您使用第三方 USB-PD 多端口电源适配器，在连接树莓派时插入其他设备会导致电源适配器和树莓派间重新协商。如果树莓派已上电，这将无缝进行。如树莓派已关机，此重新协商可能导致树莓派启动。 

### 通过以太网（PoE）连接器

![The PoE connector,width=](https://www.raspberrypi.com/documentation/computers/images/poe.jpg)

树莓派 5 PoE 标头

树莓派 5 上的以太网插孔支持 IEEE 802.3at-2009 PoE 标准，支持 PoE+。

树莓派 4B 和 Pi 3B+上的以太网插孔支持 IEEE 802.3af-2003 PoE 标准，可提供 PoE 功能。

所有具有 PoE 功能的树莓派型号都需要一个 HAT 来通过以太网端口提取电源。对于支持 PoE 的型号，我们推荐 PoE HAT。对于支持 PoE+的型号，我们推荐 PoE+ HAT。

### 典型功率需求

| 产品                    | 推荐的电源供应器电流容量 | 最大总 USB 外围设备电流吸收                  | 典型裸板活动电流消耗 |
| ------------------------- | -------------------------- | ---------------------------------------------- | ------------------------ |
|树莓派1 Model A  | 700 毫安                 | 500 毫安                                     | 200 毫安               |
| 树莓派 1 型 B           | 1.2A                     | 500 毫安                                     | 500 毫安               |
| 树莓派 1 Model A+ | 700 毫安                 | 500 毫安                                     | 180 毫安               |
| 树莓派 1 型 B+          | 1.8A                     | 1.2A                                         | 330 毫安               |
| 树莓派 2 型 B           | 1.8A                     | 1.2A                                         | 350 毫安               |
| 树莓派 3 Model B  | 2.5A                     | 1.2A                                         | 400 毫安               |
| 树莓派 3 Model A+ | 2.5A                     | 受电源、主板和连接器额定值的限制。           | 350 毫安               |
| 树莓派 3 型 B+          | 2.5A                     | 1.2A                                         | 500 毫安               |
| 树莓派 4 型 B           | 3.0A                     | 1.2A                                         | 600 毫安               |
| 树莓派 5          | 5.0A                     | 1.6 安培（如果使用 3 安培电源则为 600 毫安） | 800 毫安               |
| 树莓派 400        | 3.0A                     | 1.2A                                         | 800 毫安               |
| 树莓派 Zero       | 1.2A                     | 仅受电源、板和连接器额定值限制               | 100 毫安               |
| 树莓派 Zero W           | 1.2A                     | 仅受电源、板和连接器额定值限制。             | 150 毫安               |
| 树莓派 Zero 2 W         | 2A                       | 仅受电源、板和连接器额定值限制。             | 350 毫安               |

>**注意**
>
>树莓派 5 在连接到 5A、+5V（25W）的功率适配器时，为下游 USB 外设提供 1.6A 的电源。当连接到任何其他兼容的电源时，树莓派 5 将限制下游 USB 设备的电流为 600mA。

大多数树莓派提供足够的电流给 USB 外设，以供应大多数 USB 设备，包括键盘、鼠标和适配器。然而，一些设备需要额外的电流，包括调制解调器、外部磁盘和高功率天线。要连接功率要求超过上表规定值的 USB 设备，请使用外部供电的 USB 集线器。

随着您在树莓派上使用各种接口，其功率需求会增加。GPIO 引脚的总和可以安全地吸收 50mA；每个引脚可以单独吸收高达 16mA。HDMI 端口使用 50mA。摄像头模块需要 250mA。USB 键盘和鼠标的电流范围可以从 100mA 到 1000mA 不等。检查您计划连接到树莓派的设备的功率评级，并相应购买电源适配器。如果不确定，请使用外部供电的 USB 集线器。

您可以使用 vcgencmd 检查 USB 端口的电源输出状态。

```
vcgencmd get_config usb_max_current_enable
```

以下表格描述了不同树莓派型号在各种工作负载期间所吸收的功率量（安培）：

|                   |      | 树莓派 1B+ | 树莓派 2B | 树莓派 3B | 树莓派 Zero | 树莓派 4B |
| ------------------- | ------ | ------------------ | ----------- | ----------- | ------------- | ----------- |
| 引导              | 最大 | 0.26             | 0.40      | 0.75      | 0.20        | 0.85      |
|                   | 平均 | 0.22             | 0.22      | 0.35      | 0.15        | 0.7       |
| 空闲              | 平均 | 0.20             | 0.22      | 0.30      | 0.10        | 0.6       |
| 视频播放（H.264） | 最大 | 0.30             | 0.36      | 0.55      | 0.23        | 0.85      |
|                   | 平均 | 0.22             | 0.28      | 0.33      | 0.16        | 0.78      |
| 压力              | 最大 | 0.35             | 0.82      | 1.34      | 0.35        | 1.25      |
|                   | 平均 | 0.32             | 0.75      | 0.85      | 0.23        | 1.2       |
| 停止当前          |      |                  |           | 0.10      | 0.055       | 0.023     |

>**注意**
>
>这些测量使用了标准的 Raspberry Pi OS 镜像（截至 2016 年 2 月 26 日，或 2019 年 6 月对于树莓派 4），在室温下进行，树莓派连接到 HDMI 显示器，USB 键盘和 USB 鼠标。树莓派 3 Model B 连接到无线局域网接入点，树莓派 4 连接到以太网。所有这些功耗测量均为近似值，不考虑来自额外 USB 设备的功耗；如果连接了多个额外的 USB 设备或 HAT 到树莓派，功耗很容易超过这些测量值。 

##### [树莓派4 和计算模块 4 上的额外 PMIC 功能](https://pip.raspberrypi.com/categories/685-whitepapers-app-notes/documents/RP-004340-WP/Extra-PMIC-features-on-Raspberry-Pi-4-and-Compute-Module-4.pdf)

树莓派 4 和计算模块 4 上的额外 PMIC 功能

树莓派 4 和 CM4 上使用了许多不同的 PMIC 设备。所有的 PMIC 都提供了除电压供应之外的额外功能。本文描述了如何在软件中访问这些功能。

#### 降低树莓派 5 在关机状态下的功率

默认情况下，树莓派 5 在关闭状态时消耗约 1W 到 1.4W 的功率。这可以通过手动编辑 EEPROM 配置来降低，使用 sudo rpi-eeprom-config -e 。将设置更改为以下内容：

```
BOOT_UART=1
POWER_OFF_ON_HALT=1
BOOT_ORDER=0xf416
```

这应该将关机时的功耗降低到约 0.01W。

### 电源供应警告

自 2014 年树莓派 B+（除 Zero 系列外）的所有型号上，都有低电压检测电路，可检测供电电压是否低于 4.63V（±5%）。这将导致内核日志中增加一个条目。

如果看到警告，请切换到更高质量的电源和电缆。低质量的电源可能会损坏存储器或导致树莓派内部出现不可预测的行为。

电压可能因多种原因而下降。您可能已经插入了太多高需求的 USB 设备。电源可能不足。或者电源线可能使用了太细的导线。

##### [制作更具弹性的文件系统](https://pip.raspberrypi.com/categories/685-whitepapers-app-notes/documents/RP-003610-WP/Making-a-more-resilient-file-system.pdf)

制作更具弹性的文件系统

树莓派设备经常被用作数据存储和监控设备，通常用于可能发生突然断电的地方。与任何计算设备一样，断电会导致存储损坏。

这份白皮书提供了一些选项，说明如何通过选择适当的文件系统和设置来防止数据损坏，在这种和其他情况下确保数据完整性。

### 电源和 Raspberry Pi OS

引导加载程序通过设备树 /proc/device-tree/chosen/power 传递有关电源供应的信息。用户通常不会直接阅读这些信息。

最大电流（mA）

PDOs 的转储 - 高级用户的调试

是否将电流限制器设置为高或低

检测到 USB 过流在将控制权转移给操作系统之前是否发生任何 USB 过流

复位事件 PMIC 复位原因，例如看门狗、过压或欠压、过温

PMIC 具有内置 ADC，可以测量供电电压 EXT5V_V 等内容。使用以下命令查看 ADC 测量值:

```
vcgencmd pmic_read_adc
```

>**注意**
>
>您无法看到连接到 5V 的 USB 电流或其他任何内容，因为这会绕过 PMIC。您不应该期望这些内容加起来等于电源供应的瓦特数。但是，监视核心电压等内容可能会很有用。 

### 反向供电

USB 规范要求 USB 设备不得向上游设备提供电流。如果 USB 设备确实向上游设备提供电流，则称为反向供电。通常情况下，当连接了制作不良的供电 USB 集线器时会发生这种情况，并且将导致供电 USB 集线器向主机树莓派供电。这不被推荐，因为通过集线器向树莓派供电的电源将绕过树莓派内置的保护电路，使其在电涌事件中容易受损。

## 实时时钟（RTC）

树莓派 5 包含一个 RTC 模块。这可以通过位于 USB-C 电源连接器右侧的板上的 J5（BAT）连接器用电池供电。

![The J5 battery connector](https://www.raspberrypi.com/documentation/computers/images/j5.png)

J5 电池连接器

您可以设置唤醒闹钟，将板子切换到非常低功耗状态（约 3mA）。当闹钟时间到达时，板子将重新上电。这对于像延时摄影这样的周期性工作非常有用。

要支持唤醒闹钟的低功耗模式，请编辑引导加载程序配置：

```
$ sudo -E rpi-eeprom-config --edit
```

添加以下两行。

```
POWER_OFF_ON_HALT=1
WAKE_ON_GPIO=0
```

您可以使用以下功能进行测试：

```
$ echo +600 | sudo tee /sys/class/rtc/rtc0/wakealarm
$ sudo halt
```

这将使板卡进入非常低功耗状态，然后在 10 分钟后唤醒并重新启动。

RTC 还提供引导时的时间，例如在 dmesg 中，用于缺乏 NTP 访问的用例：

```
[    1.295799] rpi-rtc soc:rpi_rtc: setting system clock to 2023-08-16T15:58:50 UTC (1692201530)
```

>**注意**
>
>即使未连接备用电池到 J5 连接器，RTC 仍然可用。 

### 添加备用电池

![Lithium-manganese rechargeable RTC battery](https://www.raspberrypi.com/documentation/computers/images/rtc-battery.jpg)

锂锰可充电 RTC 电池

官方电池部件是可充电的锰酸锂硬币电池，带有预装的双引脚 JST-SH 插头和粘贴式安装垫。当板子的主电源断开时，这适用于为 RTC 供电。由于关机时的电流吸收为个位数µA，保持时间为几个月。

>**注意**
>
>我们不建议为 RTC 使用主要（非可充电）锂电池。RTC 备份电流消耗高于大多数专用 RTC 模块，将导致使用寿命缩短。


>**警告**
>
>不要给 RTC 使用锂离子电池。

### 启用电池充电

RTC 配备了恒流（3mA）恒压充电器。

默认情况下禁用电池充电。有 sysfs 个文件显示充电电压和限制：

```
/sys/devices/platform/soc/soc:rpi_rtc/rtc/rtc0/charging_voltage:0
/sys/devices/platform/soc/soc:rpi_rtc/rtc/rtc0/charging_voltage_max:4400000
/sys/devices/platform/soc/soc:rpi_rtc/rtc/rtc0/charging_voltage_min:1300000
```

为了以设定电压充电，请将 rtc_bbat_vchg 添加到 /boot/firmware/config.txt ：

```
dtparam=rtc_bbat_vchg=3000000
```

使用 sudo reboot 重新启动以使用新的电压设置。检查 sysfs 文件，确保充电电压已正确设置。

### 禁用电池充电

要停止充电，请从 config.txt 中删除包含 rtc_bbat_vchg 的任何行。

## 串行外围接口（SPI）

树莓派计算机配备了多个 SPI 总线。SPI 可用于连接各种外围设备 - 显示器，网络控制器（以太网，CAN 总线），UART 等。这些设备最好由内核设备驱动程序支持，但 spidev API 允许用户空间驱动程序用多种语言编写。

### SPI 硬件

树莓派 Zero、1、2 和 3 都有三个 SPI 控制器：

* SPI0 具有两个硬件芯片选择信号，在所有树莓派的引脚上都可以找到；还有一种仅适用于计算模块的备用映射。
* SPI1，具有三个硬件芯片选择，适用于除旧版树莓派 1 Model A 和 Model B 之外的所有的树莓派型号。
* SPI2，也具有三个硬件芯片选择，仅适用于计算模块 1、3 和 3+。

在树莓派 4、400 和 Compute Module 4 上，有四个额外的 SPI 总线：SPI3 到 SPI6，每个总线都有两个硬件芯片选择。这些额外的 SPI 总线可通过某些 GPIO 引脚的备用功能分配使用。有关更多信息，请参阅 BCM2711 Arm 外围设备数据表。

BCM2835 Arm 外围设备数据表中的第 10 章描述了主控制器。第 2.3 章描述了辅助控制器。

#### 引脚/GPIO 映射

##### SPI0

| SPI 功能 | 标头引脚 | Broadcom 引脚名称 | Broadcom 引脚功能 |
| ---------- | ---------- | ------------------- | ------------------- |
| MOSI     | 19       | GPIO10            | SPI0_MOSI         |
| MISO     | 21       | GPIO09            | SPI0_MISO         |
| SCLK     | 23       | GPIO11            | SPI0_SCLK         |
| CE0      | 24       | GPIO08            | SPI0_CE0_N        |
| CE1      | 26       | GPIO07            | SPI0_CE1_N        |

##### SPI0 备用映射（仅适用于计算模块，除 CM4 外）

| SPI 功能 | Broadcom 引脚名称 | Broadcom 引脚功能 |
| ---------- | ------------------- | ------------------- |
| MOSI     | GPIO38            | SPI0_MOSI         |
| MISO     | GPIO37            | SPI0_MISO         |
| SCLK     | GPIO39            | SPI0_SCLK         |
| CE0      | GPIO36            | SPI0_CE0_N        |
| CE1      | GPIO35            | SPI0_CE1_N        |

##### SPI1

| SPI 功能 | 标头引脚 | Broadcom 引脚名称 | Broadcom 引脚功能 |
| ---------- | ---------- | ------------------- | ------------------- |
| MOSI     | 38       | GPIO20            | SPI1_MOSI         |
| MISO     | 35       | GPIO19            | SPI1_MISO         |
| SCLK     | 40       | GPIO21            | SPI1_SCLK         |
| CE0      | 12       | GPIO18            | SPI1_CE0_N        |
| CE1      | 11       | GPIO17            | SPI1_CE1_N        |
| CE2      | 36       | GPIO16            | SPI1_CE2_N        |

##### SPI2（仅限计算模块，不包括 CM4）

| SPI 功能 | Broadcom 引脚名称 | Broadcom 引脚功能 |
| ---------- | ------------------- | ------------------- |
| MOSI     | GPIO41            | SPI2_MOSI         |
| MISO     | GPIO40            | SPI2_MISO         |
| SCLK     | GPIO42            | SPI2_SCLK         |
| CE0      | GPIO43            | SPI2_CE0_N        |
| CE1      | GPIO44            | SPI2_CE1_N        |
| CE2      | GPIO45            | SPI2_CE2_N        |

##### SPI3（仅限 BCM2711）

| SPI 功能 | 标头引脚 | Broadcom 引脚名称 | Broadcom 引脚功能 |
| ---------- | ---------- | ------------------- | ------------------- |
| MOSI     | 03       | GPIO02            | SPI3_MOSI         |
| MISO     | 28       | GPIO01            | SPI3_MISO         |
| SCLK     | 05       | GPIO03            | SPI3_SCLK         |
| CE0      | 27       | GPIO00            | SPI3_CE0_N        |
| CE1      | 18       | GPIO24            | SPI3_CE1_N        |

##### SPI4（仅限 BCM2711）

| SPI 功能 | 标头引脚 | Broadcom 引脚名称 | Broadcom 引脚功能 |
| ---------- | ---------- | ------------------- | ------------------- |
| MOSI     | 31       | GPIO06            | SPI4_MOSI         |
| MISO     | 29       | GPIO05            | SPI4_MISO         |
| SCLK     | 26       | GPIO07            | SPI4_SCLK         |
| CE0      | 07       | GPIO04            | SPI4_CE0_N        |
| CE1      | 22       | GPIO25            | SPI4_CE1_N        |

##### SPI5（仅限 BCM2711）

| SPI 功能 | 标头引脚 | Broadcom 引脚名称 | Broadcom 引脚功能 |
| ---------- | ---------- | ------------------- | ------------------- |
| MOSI     | 08       | GPIO14            | SPI5_MOSI         |
| MISO     | 33       | GPIO13            | SPI5_MISO         |
| SCLK     | 10       | GPIO15            | SPI5_SCLK         |
| CE0      | 32       | GPIO12            | SPI5_CE0_N        |
| CE1      | 37       | GPIO26            | SPI5_CE1_N        |

##### SPI6（仅限 BCM2711）

| SPI 功能 | 标头引脚 | Broadcom 引脚名称 | Broadcom 引脚功能 |
| ---------- | ---------- | ------------------- | ------------------- |
| MOSI     | 38       | GPIO20            | SPI6_MOSI         |
| MISO     | 35       | GPIO19            | SPI6_MISO         |
| SCLK     | 40       | GPIO21            | SPI6_SCLK         |
| CE0      | 12       | GPIO18            | SPI6_CE0_N        |
| CE1      | 13       | GPIO27            | SPI6_CE1_N        |

#### 主模式

信号名称缩写

```
SCLK - serial clock
CE   - chip enable (often called chip select)
MOSI - master out slave in
MISO - master in slave out
MOMI - master out master in
```

##### 标准模式

在标准 SPI 模式下，外围设备实现标准的三线串行协议（SCLK、MOSI 和 MISO）。

##### 双向模式

在双向 SPI 模式下，实现了相同的 SPI 标准，只是在数据传输时使用单根线（MOMI），而不是标准模式中使用的两根线（MISO 和 MOSI）。在此模式下，MOSI 引脚充当 MOMI 引脚。

##### 低速串行接口（LoSSI）模式

LoSSI 标准允许向外围设备（LCD）发出命令，并与其之间传输数据。LoSSI 命令和参数为 8 位长，但额外使用一位来指示字节是命令还是参数/数据。对于数据，将此额外位设置为高位，对于命令，将其设置为低位。生成的 9 位值被串行化到输出。LoSSI 通常与 MIPI DBI 类型 C 兼容的 LCD 控制器一起使用。

>**注意**
>
>一些命令会触发 SPI 控制器的自动读取，因此这种模式不能用作多功能 9 位 SPI。

#### 传输模式

* 轮询
* 中断
* DMA

#### 速度

CLK 寄存器的时钟分频器 (CDIV) 字段设置 SPI 时钟速度：

```
SCLK = Core Clock / CDIV
```

如果 CDIV 设置为 0，则除数为 65536。除数必须是 2 的倍数，奇数向下取整。请注意，由于模拟电气问题 (上升时间、驱动强度等)，并非所有可能的时钟速率都可用。

有关更多信息，请参阅 Linux 驱动程序部分。

#### 芯片选择

在 DMA 模式下操作时，与 CS 线自动断言和去断言相关的设置和保持时间如下：

* 在传输的第一个字节的 msb 之前至少提前三个核心时钟周期，CS 线将被断言。
* CS 线将在最后一个时钟脉冲的下降沿后不早于一个核心时钟周期取消断言。

### SPI 软件

#### Linux 驱动

默认的 Linux 驱动程序是 spi-bcm2835 。

SPI0 默认情况下被禁用。要启用它，请使用 raspi-config，或确保 dtparam=spi=on 一行没有被注释掉在 /boot/firmware/config.txt 中。默认情况下，它使用两个芯片选择线，但可以使用 dtoverlay=spi0-1cs 将其减少到一个。还有 dtoverlay=spi0-2cs ；没有任何参数时，它等同于 dtparam=spi=on 。

要启用 SPI1，您可以使用 1、2 或 3 个芯片选择线，在每种情况下添加：

```
dtoverlay=spi1-1cs  #1 chip select
dtoverlay=spi1-2cs  #2 chip select
dtoverlay=spi1-3cs  #3 chip select
```

…到 /boot/firmware/config.txt 文件。类似的叠加层也适用于 SPI2、SPI3、SPI4、SPI5 和 SPI6。

由于某些限制，驱动程序不使用硬件芯片选择线。相反，它可以使用任意数量的 GPIO 作为软件/GPIO 芯片选择。这意味着您可以自由选择任何空闲的 GPIO 作为 CS 线，所有这些 SPI 叠加层都包括该控制 - 详细信息请参见 /boot/firmware/overlays/README ，或运行（例如） dtoverlay -h spi0-2cs （ dtoverlay -a | grep spi 可能有助于列出所有内容）。

##### 速度

驱动程序支持所有作为核心时钟的偶数整数除数的速度，尽管如上所述，并非所有这些速度都会由于 GPIO 和连接的设备的限制而支持数据传输。作为经验法则，超过 50MHz 的任何速度都不太可能工作，但您的情况可能有所不同。

##### 支持的模式位

```
SPI_CPOL    - clock polarity
SPI_CPHA    - clock phase
SPI_CS_HIGH - chip select active high
SPI_NO_CS   - 1 device per bus, no Chip select
SPI_3WIRE   - bidirectional mode, data in and out pin shared
```

双向模式，也称为 3 线模式，由 spi-bcm2835 内核模块支持。请注意，在此模式下， spi_transfer 结构体的 tx 或 rx 字段必须是 NULL 指针之一，因为只支持半双工通信。否则，传输将失败。 spidev_test.c 源代码未正确考虑这一点，因此在 3 线模式下根本无法工作。

##### 每字支持的位数

* 8 - 普通
* 9 - 这是使用 LoSSI 模式支持的

##### 传输模式

所有 SPI 总线都支持中断模式。SPI0 和 SPI3-6 还支持 DMA 传输。

##### SPI 驱动程序延迟

该线程讨论延迟问题。

#### spidev

spidev 提供了基于 ioctl 的用户空间接口，用于单独的 SPI CS 线。设备树用于指示 CS 线是由内核驱动模块驱动还是由 spidev 代表用户管理；不能同时执行两者。请注意，树莓派自己的内核对于使用设备树启用 spidev 更为宽松 - 上游内核会打印关于这种用法的警告，并最终可能完全阻止它。

##### 使用 C 中的 spidev

Linux 文档中有一个回送测试程序，可用作起点。请参阅故障排除部分。

##### 使用 Python 中的 spidev

有几个 Python 库可提供对 spidev 的访问，包括 spidev （ pip install spidev -请参阅 https://pypi.org/project/spidev/）和 SPI-Py （https://github.com/lthiery/SPI-Py）。

##### 从诸如 bash 之类的 shell 使用 spidev

```
# Write binary 1, 2 and 3
echo -ne "\x01\x02\x03" > /dev/spidev0.0
```

#### 其他 SPI 库

有其他用户空间库可通过直接操作硬件来提供 SPI 控制：不建议这样做。

### 故障排除

#### 回环测试

这可以用来测试 SPI 发送和接收。在 MOSI 和 MISO 之间放一根导线。它不测试 CE0 和 CE1。

```
wget https://raw.githubusercontent.com/raspberrypi/linux/rpi-6.1.y/tools/spi/spidev_test.c
gcc -o spidev_test spidev_test.c
./spidev_test -D /dev/spidev0.0
spi mode: 0
bits per word: 8
max speed: 500000 Hz (500 KHz)

FF FF FF FF FF FF
40 00 00 00 00 95
FF FF FF FF FF FF
FF FF FF FF FF FF
FF FF FF FF FF FF
DE AD BE EF BA AD
F0 0D
```

上面的一些内容是从 elinux SPI 页面复制过来的，该页面也从这里借鉴。两者都受 CC-SA 许可证保护。

## 通用串行总线（USB）

一般来说，Linux 支持的每个设备都可以与树莓派一起使用，尽管旧版树莓派 4 之前的型号存在一些限制。

### 最大功率输出

与所有计算机一样，树莓派上的 USB 端口提供有限的功率。通常，USB 设备的问题是由功率问题引起的。为了排除问题的原因是功率不足，将您的 USB 设备连接到树莓派使用有源集线器。

| 型号                 | USB 端口的最大功率输出                                      |
| ---------------------- | ------------------------------------------------------------- |
| 树莓派 Zero, 1 | 每个端口 500 毫安^1^                                        |
| 树莓派 2, 3, 4 | 所有端口总共 1200 毫安                                      |
| 树莓派 5             | 如果使用 3A 电源，则为 600mA，如果使用 5A 电源，则为 1600mA |

1. 对于旧版树莓派 1 Model B，每个端口的限制为 100mA。

### 树莓派 5

树莓派 5 需要一款能够提供 3A 的高质量 USB-C 电源适配器（+5V，15W）才能启动。然而，使用这样的电源会限制外围设备的电流。如果您在首次启动时使用无法提供 5A 的+5V 电源，操作系统将警告您外围设备的电流将被限制在 600mA。

对于希望驱动高功率外围设备（如硬盘和固态硬盘）并保留峰值工作负载余量的用户，应使用支持 USB-PD 的电源适配器，能够提供 5A 的+5V（25W）。如果树莓派 5 固件检测到这样的电源，它会增加外围设备的 USB 电流限制至 1.6A，为下游 USB 设备提供额外的 5W 电力，并为板载设备提供额外的 5W 电力预算。

>**注意**
>
>USB 端口和风扇头共享电源预算。 

### 树莓派 4

树莓派 4 提供两个 USB 3.0 端口和两个 USB 2.0 端口，这些端口连接到 VL805 USB 控制器。所有四个端口上的 USB 2.0 线路连接到 VL805 内的单个 USB 2.0 集线器。这限制了 USB 1.1 和 USB 2.0 设备的总可用带宽与单个 USB 2.0 端口相同。

在树莓派 4 上，以前型号上使用的 USB 控制器位于 USB 类型 C 端口上，并且默认情况下已禁用。

### 树莓派 Zero, 1, 2 和 3

树莓派 1 Model B+、树莓派2 和树莓派 3 主板提供四个 USB 2.0 端口。树莓派 Zero 主板具有一个 micro USB On-The-Go（OTG）端口。

旧版的树莓派 4 之前的型号上的 USB 控制器仅对某些设备提供基本级别的支持，这会带来更高的软件处理开销。它还仅支持一个根 USB 端口：所有连接设备的流量都会被导向这个单一总线，其最大速度为 480Mbps。

USB 2.0 规范定义了三种设备速度 - 低速、全速和高速。大多数鼠标和键盘是低速，大多数 USB 声音设备是全速，而大多数视频设备（网络摄像头或视频捕捉设备）是高速。

通常，连接多个高速 USB 设备到树莓派上不会出现问题。

与低速和全速设备通信时产生的软件开销意味着同时活动的低速和全速设备数量存在限制。连接到树莓派的这些类型设备数量较少不会造成问题。

### 已知的 USB 问题

#### 与 USB 3.0 集线器的互操作性

使用 USB 3.0 集线器与全速或低速设备（包括大多数鼠标和键盘）存在问题。大多数 USB 3.0 集线器硬件中的错误意味着旧版树莓派 4 之前的型号无法与连接到 USB 3.0 集线器的全速或低速设备通信。

USB 2.0 高速设备，包括 USB 2.0 集线器，当通过 USB 3.0 集线器连接时可以正常运行。

避免将低速或全速设备连接到 USB 3.0 集线器。作为解决方法，将 USB 2.0 集线器插入 USB 3.0 集线器的下游端口，并连接低速设备，或者在树莓派和 USB 3.0 集线器之间使用 USB 2.0 集线器，然后将低速设备插入 USB 2.0 集线器。

#### USB 1.1 网络摄像头

旧版网络摄像头可能是全速设备。由于这些设备传输大量数据并产生额外的软件开销，可靠的操作不能保证。作为解决方法，请尝试以较低分辨率使用摄像头。

#### 神秘的 USB 声卡

昂贵的发烧友级声卡通常使用大量的 USB 带宽。无法保证与 96kHz/192kHz DAC 的可靠操作。作为解决方法，强制输出流为 CD 音质（44.1kHz/48kHz 16 位）将带宽降低到可靠水平。

#### 单 TT USB 集线器

USB 2.0 和 3.0 集线器具有一种用于与连接到其下游端口的全速或低速设备通信的机制，称为事务转换器（TT）。该设备缓冲来自主机的高速请求，并将它们以全速或低速传输到下游设备。USB 规范允许两种集线器配置：单 TT（所有端口共用一个 TT）和多 TT（每个端口一个 TT）。由于硬件限制，如果将太多全速或低速设备插入单个 TT 集线器，则这些设备可能表现不可靠。建议使用多 TT 集线器与多个全速和低速设备进行接口。作为解决方法，将全速和低速设备分散在树莓派 自己的 USB 端口和单 TT 集线器之间。

## 树莓派修订代码

每个不同的 树莓派型号修订版都有一个独特的修订代码。您可以通过运行以下命令查找树莓派的修订代码：

```
cat /proc/cpuinfo
```

最后三行显示硬件类型、修订代码和树莓派的唯一序列号。例如：

```
Hardware    : BCM2835
Revision    : a02082
Serial      : 00000000765fc593
```

>**注意**
>
>所有树莓派算机报告 BCM2835 ，即使是搭载 BCM2836、BCM2837、BCM2711 和 BCM2712 处理器的那些。您不应该使用此字符串来检测处理器。请使用以下信息解码修订代码，或者 cat /sys/firmware/devicetree/base/model 。 
### 旧版修订代码

第一批树莓派型号从 0002 到 0015 被赋予了顺序十六进制修订代码：

| 代码 | 型号 | 修订 | RAM         | 制造商   |
| ------ | ------ | ------ | ------------- | ---------- |
| 0002 | B    | 1.0  | 256MB       | Egoman   |
| 0003 | B    | 1.0  | 256MB       | Egoman   |
| 0004 | B    | 2.0  | 256MB       | 索尼英国 |
| 0005 | B    | 2.0  | 256MB       | 奇达     |
| 0006 | B    | 2.0  | 256MB       | 亿高曼   |
| 0007 | A    | 2.0  | 256MB       | 伊戈曼   |
| 0008 | A    | 2.0  | 256MB       | 索尼英国 |
| 0009 | A    | 2.0  | 256MB       | 奇达     |
| 000d | B    | 2.0  | 512MB       | 埃戈曼   |
| 000e | B    | 2.0  | 512MB       | 索尼英国 |
| 000f | B    | 2.0  | 512MB       | Egoman   |
| 0010 | B+   | 1.2  | 512MB       | 索尼英国 |
| 0011 | CM1  | 1.0  | 512MB       | 索尼英国 |
| 0012 | A+   | 1.1  | 256MB       | 索尼英国 |
| 0013 | B+   | 1.2  | 512MB       | 嵌入式   |
| 0014 | CM1  | 1.0  | 512MB       | 嵌入式   |
| 0015 | A+   | 1.1  | 256MB/512MB | Embest   |

### 新版修订代码

使用树莓派 2 的推出，引入了新式的修订代码。每个十六进制代码的每一位代表有关修订的一部分信息：

```
NOQuuuWuFMMMCCCCPPPPTTTTTTTTRRRR
```

| 部分                | 代表        | 选项                  |
| --------------------- | ------------- | ----------------------- |
| N（位 31）          | 过压        | 0：允许过压           |
|                     |             | 1：禁止过压           |
| O（位 30）          | OTP 程序^1^ | 0：允许 OTP 编程      |
|                     |             | 1：禁止 OTP 编程      |
| Q（位 29）          | OTP 读取^1^ | 0：OTP 读取允许       |
|                     |             | 1：OTP 阅读不允许     |
| uuu（位 26-28）     | 未使用      | 未使用                |
| W（位 25）          | 保修位^2^   | 0：保修有效           |
|                     |             | 1：保修因超频作废     |
| u（第 24 位）       | 未使用      | 未使用                |
| F（位 23）          | 新标志      | 1：新风格修订         |
|                     |             | 0：旧版风格修订       |
| MMM（位 20-22）     | 内存大小    | 0：256MB              |
|                     |             | 1：512MB              |
|                     |             | 2：1GB                |
|                     |             | 3：2GB                |
|                     |             | 4：4GB                |
|                     |             | 5：8GB                |
| CCCC（位 16-19）    | 制造商      | 0: 索尼英国           |
|                     |             | 1: Egoman             |
|                     |             | 2：Embest             |
|                     |             | 3：Sony Japan         |
|                     |             | 4：Embest             |
|                     |             | 5：体育场             |
| PPPP（位 12-15）    | 处理器      | 0：BCM2835            |
|                     |             | 1：BCM2836            |
|                     |             | 2：BCM2837            |
|                     |             | 3：BCM2711            |
|                     |             | 4：BCM2712            |
| TTTTTTTT（位 4-11） | 类型        | 0：A                  |
|                     |             | 1：B                  |
|                     |             | 2：A+                 |
|                     |             | 3：B+                 |
|                     |             | 4：2B                 |
|                     |             | 5：阿尔法（早期原型） |
|                     |             | 6：CM1                |
|                     |             | 8：3B                 |
|                     |             | 9：Zero               |
|                     |             | a：CM3                |
|                     |             | c：Zero W             |
|                     |             | d：3B+                |
|                     |             | ext: e：3A+           |
|                     |             | f：仅限内部使用       |
|                     |             | 10：CM3+              |
|                     |             | 11：4B                |
|                     |             | 12：Zero 2 W          |
|                     |             | 13: 400               |
|                     |             | 14：CM4               |
|                     |             | 15：CM4S              |
|                     |             | 16：仅限内部使用      |
|                     |             | 17: 5                 |
| RRRR（位 0-3）      | 修订版      | 0、1、2、等           |

^1^ 编程 OTP 位的信息。

^2^ 在树莓派 4 上从未设置过保修位。

### 使用中的新版式修订代码。

>**注意**
>
>此列表并非详尽无遗 - 可能存在未在此表中列出的正在使用的代码。请参阅下一节，了解如何使用修订代码识别板。

| 代码   | 型号               | 修订版 | RAM   | 制造商    |
| -------- | -------------------- | -------- | ------- | ----------- |
| 900021 | A+                 | 1.1    | 512MB | 索尼英国  |
| 900032 | B+                 | 1.2    | 512MB | 索尼英国  |
| 900092 | Zero                 | 1.2    | 512MB | 索尼英国  |
| 900093 | Zero                 | 1.3    | 512MB | 索尼英国  |
| 9000c1 | Zero W             | 1.1    | 512MB | 索尼英国  |
| 9020   | 3A+                | 1.0    | 512MB | 索尼英国  |
| 90200  | 3A+                | 1.1    | 512MB | 索尼英国  |
| 920092 | Zero                 | 1.2    | 512MB | 恩贝斯    |
| 920093 | Zero                 | 1.3    | 512MB | 恩贝斯特  |
| 900061 | CM1                | 1.1    | 512MB | 索尼英国  |
| a01040 | 2B                 | 1.0    | 1GB   | 索尼英国  |
| a01041 | 2B                 | 1.1    | 1GB   | 索尼英国  |
| a02082 | 3B                 | 1.2    | 1GB   | 索尼英国  |
| a020a0 | CM3                | 1.0    | 1GB   | 索尼英国  |
| a020d3 | 3B+                | 1.3    | 1GB   | 索尼英国  |
| a020d4 | 3B+                | 1.4    | 1GB   | 索尼英国  |
| a02042 | 2B（带有 BCM2837） | 1.2    | 1GB   | 索尼英国  |
| a21041 | 2B                 | 1.1    | 1GB   | Embest    |
| a22042 | 2B（带有 BCM2837） | 1.2    | 1GB   | Embest    |
| a22082 | 3B                 | 1.2    | 1GB   | Embest    |
| a220a0 | CM3                | 1.0    | 1GB   | Embest    |
| a32082 | 3B                 | 1.2    | 1GB   | 索尼日本  |
| a52082 | 3B                 | 1.2    | 1GB   | 体育场    |
| a22083 | 3B                 | 1.3    | 1GB   | Embest    |
| a02100 | CM3+               | 1.0    | 1GB   | 索尼英国  |
| a03111 | 4B                 | 1.1    | 1GB   | 索尼英国  |
| b03111 | 4B                 | 1.1    | 2GB   | 索尼英国  |
| b03112 | 4B                 | 1.2    | 2GB   | 索尼英国  |
| b03114 | 4B                 | 1.4    | 2GB   | 索尼英国  |
| b03115 | 4B                 | 1.5    | 2GB   | 索尼英国  |
| c03111 | 4B                 | 1.1    | 4GB   | 索尼英国  |
| c03112 | 4B                 | 1.2    | 4GB   | 索尼英国  |
| c03114 | 4B                 | 1.4    | 4GB   | 索尼英国  |
| c03115 | 4B                 | 1.5    | 4GB   | 索尼英国  |
| d03114 | 4B                 | 1.4    | 8GB   | 索尼英国  |
| d03115 | 4B                 | 1.5    | 8GB   | 索尼英国  |
| c03130 | 树莓派 400         | 1.0    | 4GB   | 索尼 英国 |
| a03140 | CM4                | 1.0    | 1GB   | 英国索尼  |
| b03140 | CM4                | 1.0    | 2GB   | 索尼英国  |
| c03140 | CM4                | 1.0    | 4GB   | 索尼英国  |
| d03140 | CM4                | 1.0    | 8GB   | 索尼英国  |
| 902120 | Zero 2 W           | 1.0    | 512MB | 索尼英国  |
| c04170 | 5                  | 1.0    | 4GB   | 索尼英国  |
| d04170 | 5                  | 1.0    | 8GB   | 索尼英国  |

### 使用修订代码进行板识别

从命令行，我们可以使用以下内容来获取板的修订代码：

```
$ cat /proc/cpuinfo | grep Revision
Revision      : c03111
```

在上面的示例中，我们有一个十六进制修订代码为 c03111 。将其转换为二进制，我们得到 0 0 0 000 0 0 1 100 0000 0011 00010001 0001 。已插入空格以显示修订代码的各部分之间的边界，根据上表。

从最低位开始，最低的四位（0-3）是板的修订号，因此此板的修订号为 1。接下来的八位（4-11）是板类型，在本例中为二进制 00010001 ，十六进制 11 ，因此这是个树莓派 4B。使用相同的过程，我们可以确定处理器是 BCM2711，板是由索尼英国制造的，并且具有 4GB 的 RAM。

#### 在程序中获取修订代码

很明显，有很多编程语言，不可能为所有这些语言提供示例，但是这里有两个快速示例，适用于 C 和 Python 。这两个示例都使用系统调用来运行一个 bash 命令，获取 cpuinfo 并将结果传输到 awk 以恢复所需的修订代码。然后，它们使用位操作从代码中提取 New ， Model 和 Memory 字段。

```
#include <stdio.h>
#include <stdlib.h>

int main( int argc, char *argv[] )
{
  FILE *fp;
  char revcode[32];

  fp = popen("cat /proc/cpuinfo | awk '/Revision/ {print $3}'", "r");
  if (fp == NULL)
    exit(1);
  fgets(revcode, sizeof(revcode), fp);
  pclose(fp);

  int code = strtol(revcode, NULL, 16);
  int new = (code >> 23) & 0x1;
  int model = (code >> 4) & 0xff;
  int mem = (code >> 20) & 0x7;

  if (new && model == 0x11 && mem >= 3)  // Note, 3 in the mem field is 2GB
     printf("We are a 4B with at least 2GB of RAM!\n" );

  return 0;
}
```

在 Python 中也是一样：

```
import subprocess

cmd = "cat /proc/cpuinfo | awk '/Revision/ {print $3}'"
revcode = subprocess.check_output(cmd, shell=True)

code = int(revcode, 16)
new = (code >> 23) & 0x1
model = (code >> 4) & 0xff
mem = (code >> 20) & 0x7

if new and model == 0x11 and mem >= 3 : # Note, 3 in the mem field is 2GB
    print("We are a 4B with at least 2GB RAM!")
```

### 修订代码使用的最佳实践

为避免在创建新的板卡版本时出现问题，请勿使用修订代码（例如 c03111 ）。

一个天真的实现使用支持的修订代码列表，将检测到的代码与列表进行比较，以决定设备是否受支持。当出现新的板卡版本或生产地点更改时，这种方法会中断：每次出现新的修订代码时，都会在支持的修订代码列表中创建一个新的修订代码。这将导致同一板卡类型的新修订版本被拒绝，尽管它们始终向后兼容。每次出现新的修订版本时，您都必须发布一个包含新修订代码的新支持的修订代码列表 - 这是一个繁重的开发负担。

应该使用以下方法之一：

* 通过板类型字段（3A、4B 等）进行过滤，该字段表示型号，但不表示修订版。
* 通过内存量字段进行过滤，因为 RAM 大致对应于板的计算能力。

例如，您可以将支持限制为具有 2GB RAM 或更多的树莓派 4B 型号。前一节中的示例使用了这种推荐方法。

>**注意**
>
>始终检查第 23 位，即“New”标志，以确保修订代码是新版本，然后再检查其他字段。

#### 在各个发行版中检查树莓派型号和 CPU

在各个 Linux 发行版中，对 /proc/cpuinfo 的支持和格式化各不相同。要在任何 Linux 发行版（包括 Raspberry Pi OS）上检查树莓派设备的型号或 CPU，请查看设备树：

```
$ cat /proc/device-tree/compatible | tr '\0' '\n'
raspberrypi,5-model-b
brcm,bcm2712
```

这将输出两个空值分隔的字符串值，每个字符串值包含一个逗号分隔的制造商和型号。例如，树莓派 5 会输出上述板和 CPU 字符串。这些对应以下值：

* raspberrypi （板制造商）
* 5-model-b （板载型号）
* brcm （CPU 制造商）
* bcm2712 （CPU 型号）

树莓派型号具有以下设备树数值：

| 设备名称                   | 制造商 | 型号 | CPU 制造商 | CPU |
| ---------------------------- | -------- | ------ | ------------ | ----- |
| 树莓派 5             | `raspberrypi`       | `5-model-b`     | `brcm`           | `bcm2712`    |
| 树莓派 400                 | `raspberrypi`       | `400`     | `brcm`           | `bcm2711`    |
| 树莓派计算模块 4           | `raspberrypi`       | `4-compute-module`     | `brcm`           | `bcm2711`    |
| 树莓派 4A           | `raspberrypi`       | `4-model-a`     | `brcm`           | `bcm2711`    |
| 树莓派 4B           | `raspberrypi`       | `4-model-b`     | `brcm`           | `bcm2711`    |
| 树莓派计算模块 3    | `raspberrypi`       | `3-compute-module`     | `brcm`           | `bcm2837`    |
| 树莓派 3A+          | `raspberrypi`       | `3-model-a-plus`     | `brcm`           | `bcm2837`    |
| 树莓派 3B+             | `raspberrypi`       | `3-model-b-plus`     | `brcm`           | `bcm2837`    |
| 树莓派 3 B              | `raspberrypi`       | `3-model-b`     | `brcm`           | `bcm2837`    |
| 树莓派 2B              | `raspberrypi`       | `2-model-b`     | `brcm`           | `bcm2836`    |
| 树莓派计算模块             | `raspberrypi`       | `compute-module`     | `brcm`           | `bcm2835`    |
| 树莓派 A+              | `raspberrypi`       | `model-a-plus`     | `brcm`           | `bcm2835`    |
| 树莓派 B+              | `raspberrypi`       | `model-b-plus`     | `brcm`           | `bcm2835`    |
| 树莓派 B Rev 2 | `raspberrypi`       | `model-b-rev2`     | `brcm`           | `bcm2835`    |
| 树莓派 A       | `raspberrypi`       | `model-a`     | `brcm`           | `bcm2835`    |
| 树莓派 B       | `raspberrypi`       | `model-b`     | `brcm`           | `bcm2835`    |
| 树莓派 Zero 2 W            | `raspberrypi`       | `model-zero-2-w`     | `brcm`           | `bcm2837`    |
| 树莓派 Zero                | `raspberrypi`       | `model-zero`     | `brcm`           | `bcm2835`    |
| 树莓派 Zero W              | `raspberrypi`       | `model-zero-w`     | `brcm`           | `bcm2835`    |
