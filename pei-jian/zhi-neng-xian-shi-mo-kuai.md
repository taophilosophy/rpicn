# 智能显示模块

树莓派智能显示模块是一款用于树莓派计算模块 5（CM5）的转接板，使你无需外部线缆或外部电源，即可将 CM5 集成到兼容的数字标牌中。

更多信息请参阅[产品页面](https://www.raspberrypi.com/products/smart-display-module)。

![树莓派智能显示模块](https://www.raspberrypi.com/documentation/accessories/images/smart-display-module-hero.png)

树莓派智能显示模块

如果你从 Sharp 购买树莓派智能显示模块，模块中已安装并配置好一块 CM5。更多信息请参阅 [Sharp 网站](https://business.sharpusa.com/computing)。

## 规格

本节介绍树莓派智能显示模块的物理特性和能力，包括功能、硬件和尺寸。

### 功能

智能显示模块包含以下功能：

* **兼容 Intel® 智能显示模块（SDM）规范。** 转接板可直接插入支持该规范的主机显示器。
* **兼容计算模块 5。** CM5 安装在智能显示模块上。
* **散热器。** 散热器符合 SDM 外形尺寸，可将热量从 CM5 导出。
* **集成供电。** 主机显示器直接为 CM5 供电。
* **M.2 M key 扩展。** M.2 M key PCIe 插槽兼容 2230、2242、2260 和 2280 外形尺寸，为添加存储设备或 AI 加速器提供扩展空间。
* **外部天线空间。** 使用[树莓派天线套件](../shu-mei-pai/ji-suan-mo-kuai-ying-jian.md)，你可以在主机显示器外部安装外置天线。
* **HDMI 输出。** 支持第二路独立的视频流。
* **连接器。** 将各种[连接器](#连接器)暴露到主机显示器外部。
* **启动模式开关。** 在从 eMMC 启动（标记为 **NORMAL**）和从 USB 设备模式启动（标记为 **USB**）之间切换 CM5。
* **外部电源按钮。** 独立于显示器对 CM5 进行电源循环。
* **LED 指示灯。** 指示 CM5 的电源状态和存储活动。此指示灯显示与树莓派 5 相同的 LED 行为。更多信息请参阅 [LED 行为](https://www.raspberrypi.com/documentation/computers/configuration.html#led-behaviour)。

### 硬件

智能显示模块包装箱包含以下部件：

* 一个智能显示模块。
* 一个被动式铝制散热器。
* 四颗 M3 螺丝，用于固定散热器。
* 两颗 M2 螺丝，用于固定 CM5。
* 一颗驱动器固定螺丝，用于固定 M.2 设备。

### 尺寸

树莓派智能显示模块的尺寸兼容 [Intel® SDM 规范](https://www.intel.com/content/www/us/en/products/docs/smart-display-module/overview.html)。

智能显示模块采用 SDM-L 外形尺寸。主板及其组件的尺寸为 175 × 100 × 20 mm。包括面板、把手和金手指接口在内，模块的完整尺寸为 193 × 125 × 25 mm。

智能显示模块单独重量约为 146 g。与 CM5、散热器和螺丝组装在一起后，重量约为 225 g。

### 连接器

智能显示模块直接连接到树莓派计算模块 5。它通过转接板内侧边缘的金手指接口（Intel SDM 边缘连接器）连接到主机显示器。

Intel SDM 边缘连接器将以下接口或信号从 CM5 传输到主机显示器：

| CM5 接口 | Intel SDM 接口 |
| ---- | ---- |
| HDMI0 | HDMI |
| USB 3.0 port 1 | USB3 |
| GPIO7/9/10/11 (SPI0) | GSPI |
| GPIO14/GPIO15 (UART0) | UART |
| GPIO2/GPIO3 (I2C1) | I2C0（CM5 为目标端） |
| GPIO38/39 (I2C0) | I2C1（CM5 为控制器） |
| PWR_Button | Power Button |
| PMIC_Enable | Power Reset |
| GPIO5/GPIO17 | SLP_S4 |
| GPIO4 | System Fan Control |
| HDMI0_CEC | HDMI CEC |

>**注意**
>
> 树莓派 SDM 不会通过 Intel SDM 边缘连接器连接 DisplayPort、PCIe 或以太网接口。

在主机显示器的外部，智能显示模块暴露以下连接器：

* HDMI 2.0。连接到 CM5 上的 HDMI1。
* USB-C（USB 2.0）。此端口仅支持设备模式，用于在安装后为 CM5 编程。
* 以太网（RJ45）连接器。
* USB-A（USB 3.0）。连接到 CM5 上的 USB 3.0 端口 0。

在内部，智能显示模块暴露以下连接器：

* 22 针摄像头和显示接口。连接到 CM5 上的 CAM/DISP 0。
* RTC 电池座（CR2032）。
* M.2 M key PCIe 插槽。
* CM5 插槽。

在内部，智能显示模块还在最靠近 CM5 的短边上暴露以下引脚。

引脚以两个为一组标注。在引脚标签方向正确时，顶部四对引脚左侧为接地引脚，右侧为有效引脚；底部四对引脚每对都有两个功能相同的有效引脚。

![顶部四对引脚的引脚布局](https://www.raspberrypi.com/documentation/accessories/images/wlan-header.jpg)

顶部四对引脚的引脚布局

![底部四对引脚的引脚布局](https://www.raspberrypi.com/documentation/accessories/images/fan-header.jpg)

底部四对引脚的引脚布局

| 标签 | CM5 引脚名称 | 说明 |
| ---- | ---- | ---- |
| **WP_N** | `EEPROM_nWP` | 将相邻的接地引脚连接到有效引脚，以防止板载 EEPROM 的内容发生变化。 |
| **BL_ON** | `BT_nDisable` | 将相邻的接地引脚连接到有效引脚，以禁用蓝牙功能。 |
| **WL_ON** | `WL_nDisable` | 将相邻的接地引脚连接到有效引脚，以禁用 Wi-Fi 功能。 |
| **12V** | 不适用 | 来自主机显示器的电源（12 V）。注意不要将 12 V 引脚连接到接地连接；否则会损坏板卡。 |
| **VBUS** | `VBUS_EN` | 向外置 USB 3.0 端口供电的信号。 |
| **FPWM** | `Fan_PWM` | 驱动各种 PWM 控制的风扇。 |
| **GND** | `GND` | 接地（0 V） |
| **FTACH** | `Fan_Tacho` | 读取许多 PWM 风扇上存在的转速计输出信号。 |

有关这些引脚及其使用方法的更多信息，请参阅[计算模块 5 数据手册](https://pip.raspberrypi.com/documents/RP-008180-DS)和[计算模块 5 IO 板数据手册](https://pip.raspberrypi.com/documents/RP-008182-DS)。

## 设置智能显示模块

你可以将计算模块 5 安装到智能显示模块上，连接可选的附加组件，然后将整个模块安装到主机显示器中。

如果你从 Sharp 购买了树莓派智能显示模块，CM5 已在散热器下方配置并安装完毕。你无需遵循此过程，但如果要安装可选组件，可能需要参考其中一些步骤。

此过程所需的设备：

* 智能显示模块。
* 随附的散热器和螺丝。
* 一块计算模块 5。
* 一把十字螺丝刀。
* 可选：树莓派天线套件。
* 可选：一个 M.2 M key 设备。
* 一台带有兼容 SDM 插槽的主机显示器。

>**重要**
>
> 在完成以下步骤之前，请断开主机显示器与电源的连接。即使显示器已关闭并处于待机状态，除非完全断开电源，否则它仍可能为 SDM 插槽供电。

要配置并组装智能显示模块：

1. 为计算模块 5 安装操作系统镜像以及你的使用场景所需的任何软件，从而完成配置。更多信息请参阅[为计算模块刷写镜像](../shu-mei-pai/ji-suan-mo-kuai-ying-jian.md#刷写-emmc)。

   或者，你也可以在组装好智能显示模块后完成此步骤。更多信息请参阅[在原位编程 CM5](#在原位编程-cm5)。

2. 从智能显示模块上取下散热器，以便接触计算模块 5 的安装位置。

   ![标有散热器位置的智能显示模块](https://www.raspberrypi.com/documentation/accessories/images/sdm-assembly-w-antenna-step-2.png)

   使用十字螺丝刀松开固定散热器的四颗 M3 螺丝。保留这些螺丝以备后用。

3. 使用十字螺丝刀松开 CM5 插槽中的两颗 M2 螺丝。保留这些螺丝以备后用。

   ![已从 CM5 插槽上拆下固定螺丝的智能显示模块](https://www.raspberrypi.com/documentation/accessories/images/sdm-assembly-w-antenna-step-3.png)

4. 将 CM5 安装到智能显示模块上。
   * 使 CM5 和智能显示模块上的树莓派标志均朝上且方向正确，将 CM5 放入标有 **COMPUTE MODULE 5** 的区域，使其孔位与安装柱对齐。
   * 轻轻将 CM5 向下压到连接器上，直到固定到位。

   ![标有 CM5 位置的智能显示模块](https://www.raspberrypi.com/documentation/accessories/images/sdm-assembly-w-antenna-step-5.png)

5. 使用 M2 螺丝将 CM5 固定到板卡上。这些螺丝的建议扭矩为 0.15 Nm。

   ![已安装 CM5 并标有螺丝位置的智能显示模块](https://www.raspberrypi.com/documentation/accessories/images/sdm-assembly-w-antenna-step-7.png)

6. 可选：安装一个 M.2 M key 设备。如果你要安装 M.2 NVMe 驱动器或 AI 加速器，最好在安装散热器之前进行。
   * 用手指取下驱动器固定螺丝。
   * 将 M.2 设备插入 M.2 边缘连接器，以略微向上的角度将驱动器滑入插槽。不要强行将驱动器插入插槽；请轻轻滑入。
   * 将驱动器固定螺丝上的缺口推入 M.2 驱动器末端的插槽。
   * 将 M.2 设备平压在板卡上，用手指顺时针转动驱动器固定螺丝，直到感觉固定牢靠。不要过度拧紧螺丝。

7. 可选：如果你的 CM5 带有板载 Wi-Fi，你可以连接外置天线。如果要在你的设备上安装天线，请在安装散热器之前进行。

   ![标有天线位置的智能显示模块](https://www.raspberrypi.com/documentation/accessories/images/sdm-assembly-w-antenna-step-11.png)

   * 从智能显示模块内部的天线端口上取下橡胶塞。
   * 确保齿形垫圈位于 SMA 连接器上。
   * 从智能显示模块内部，将 SMA 连接器（平面朝向其他端口）推入天线端口，使其伸出并可从外部接触到。
   * 从外部装上开口垫圈，并顺时针将固定六角螺母拧到 SMA 连接器上，直到牢固就位。为避免损坏，拧紧时不要用力过度。
   * 将天线连接到 SMA 连接器，使天线朝外，然后顺时针转动天线以固定。
   * 将天线转到适合你的显示器的角度，使其进入最终位置。
   * 如果安装了 M.2 设备，避免将天线线缆布置在它上方。请将天线线缆布置在 M.2 插槽与智能显示模块外表面之间。

   ![标有天线线缆走线路径的智能显示模块](https://www.raspberrypi.com/documentation/accessories/images/sdm-assembly-w-antenna-step-13.png)

   * 将天线线缆上的 U.FL 连接器连接到计算模块 5 上与 U.FL 兼容的连接器，位置在 CM5 左上角安装孔旁边。

   ![已安装天线的智能显示模块](https://www.raspberrypi.com/documentation/accessories/images/sdm-assembly-w-antenna-step-15.png)

8. 安装散热器。散热器的一个安装点是偏置的；这可以确保散热器以正确的方式安装。
   * 取下散热器上的套筒和导热垫上的保护纸。
   * 如果你安装了天线，请确保天线线缆的走线避开散热器安装点。
   * 将散热器放在计算模块 5 上方，使其安装点与智能显示模块板卡上的孔对齐。

   ![已安装 CM5 和天线并标有散热器位置的智能显示模块](https://www.raspberrypi.com/documentation/accessories/images/sdm-assembly-w-antenna-step-16.png)

   * 使用十字螺丝刀将 M3 螺丝穿过板卡并拧入散热器安装点。均匀拧紧螺丝。这些螺丝的建议扭矩为 0.25 Nm。

   ![已安装 CM5、天线和散热器的智能显示模块](https://www.raspberrypi.com/documentation/accessories/images/sdm-assembly-w-antenna-step-17.png)

9. 可选：在 RTC 电池座中安装一颗 CR2032 电池。

10. 可选：将 22 针摄像头 FFC 或 22 针显示 FFC 连接到摄像头/显示接口，并将线缆穿过 IO 挡板开口。CM5 不会自动检测这些设备。你必须在 `config.txt` 文件中配置这些设备。更多信息请参阅[连接摄像头模块](../shu-mei-pai/ji-suan-mo-kuai-ying-jian.md#连接摄像头模块)或[连接 Touch Display 2](https://www.raspberrypi.com/documentation/accessories/touch-display-2.html#connect-to-raspberry-pi)。

11. 确保主机显示器已完全断开电源。

12. 将智能显示模块安装到主机显示器中。有关此安装过程的更多信息，请参阅主机显示器的文档。

13. 为主机显示器接通电源并将其开启。主机显示器为智能显示模块供电，CM5 随即启动。

根据主机显示器的默认行为，你可能需要选择智能显示模块作为其输入。更多信息请参阅主机显示器的文档。

## 在原位编程 CM5

你可以在将 CM5 安装到智能显示模块中，并将智能显示模块安装到主机显示器中之后，再对 CM5 进行配置。

为此，你需要以下设备：

* 已安装智能显示模块的主机显示器。
* 一台安装了[树莓派启动盘制作工具](https://www.raspberrypi.com/software/) 2.0.11 或更高版本的计算机。
* 一根 USB-C 线缆。

请完成以下步骤：

1. 在计算机上启动树莓派启动盘制作工具。
2. 配置树莓派启动盘制作工具，使其能够使用 `rpiboot` 检测 CM5，并将其视为大容量存储设备。
   * 打开 **Debug Options**：
      * 在 Windows 或 Linux 上，按 **Ctrl + Alt + S**。
      * 在 macOS 上，按 **Cmd + Option + S**。
   * 滚动到 **Advanced Features**。
   * 使用切换开关选择 **Enable Rpiboot/Fastboot Support**。
   * 选择 **Apply** 保存更改并退出 **Debug Options** 对话框。
3. 确保主机显示器已完全断开电源。
4. 使用 USB-C 线缆将计算机连接到智能显示模块上标有 **SERVICE** 的 USB-C 连接器。
5. 将启动模式开关从 **NORMAL** 切换到 **USB**。
6. 为主机显示器接通电源。CM5 会在树莓派启动盘制作工具中显示为大容量存储设备。
7. 在计算机上使用树莓派启动盘制作工具为 CM5 安装操作系统。安装完成后，计算机会弹出该大容量存储设备。
8. 断开智能显示模块上的线缆。
9. 关闭显示器电源。
10. 将启动模式开关从 **USB** 切回 **NORMAL**。
11. 开启显示器电源。

## 移除智能显示模块

有关此过程的信息，请参阅主机显示器的文档。

>**重要**
>
> * 在移除智能显示模块之前，请断开主机显示器与电源的连接。即使显示器已关闭并处于待机模式，除非完全断开电源，否则它仍可能为 SDM 插槽供电。
> * 移除智能显示模块时，请使用把手将其从主机显示器中笔直拉出。
