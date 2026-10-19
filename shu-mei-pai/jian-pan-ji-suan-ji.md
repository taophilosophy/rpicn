# 键盘计算机

Raspberry Pi 键盘计算机是内置在键盘中的完整个人计算机。它们采用与 Raspberry Pi 单板计算机（SBC）相同的片上系统（SoC）。

键盘计算机使用 `<X00>` 形式的型号标识，其中 `X` 表示对应的经典单板计算机（SBC）系列设备。例如，Raspberry Pi 400 是 Raspberry Pi 4 的键盘版本。

Raspberry Pi 提供三款键盘计算机：

* [Raspberry Pi 400](#raspberry-pi-400-及套件)
* [Raspberry Pi 500](#raspberry-pi-500-及套件)
* [Raspberry Pi 500+](#raspberry-pi-500-键盘计算机及套件)

Raspberry Pi 键盘计算机提供不同的地区版本，键盘布局和所需电源会有所不同。

## 特性

Raspberry Pi 键盘计算机的特性取决于具体型号。

得益于 Cortex-A76 CPU、更大的内存和升级的 GPU，**Raspberry Pi 500** 和 **Raspberry Pi 500+** 比 **Raspberry Pi 400** 更快。Raspberry Pi 400 键盘计算机与 Raspberry Pi 500、500+ 键盘计算机的主要区别如下：

* **处理器。** Raspberry Pi 400 使用 1.8 GHz 的 Cortex-A72；Raspberry Pi 500 和 500+ 均使用 2.4 GHz 的 Cortex-A76，性能和能效更高。
* **内存（RAM）。** Raspberry Pi 400 配备 4 GB RAM；Raspberry Pi 500 配备 8 GB RAM；Raspberry Pi 500+ 配备 16 GB RAM，多任务处理更流畅，并能支持要求更高的应用。
* **GPU。** Raspberry Pi 400 配备 500 MHz 的 VideoCore VI；Raspberry Pi 500 和 500+ 均配备 910 MHz 的 VideoCore VII，图形处理更快，视频解码能力更强。
* **HDR 视频。** 所有 Raspberry Pi 键盘计算机均配备两个 micro-HDMI 端口，可提供 4K 显示，但 Raspberry Pi 500 和 500+ 还支持 HDMI 输出上的 HDR。
* **电源按键。** Raspberry Pi 400 没有电源按键，而是通过组合按键（**Fn** + **F10**）开关机；Raspberry Pi 500 和 500+ 均配有专用电源键。
* **SoC。** Raspberry Pi 400 采用 Broadcom 芯片 BCM2711；Raspberry Pi 500 和 500+ 均采用 Broadcom 芯片 BCM2712，并搭配 RP1 I/O 控制器。

Raspberry Pi 500+ 还提供以下附加特性：

* 机械按键，带有可自定义的 RGB LED 和可更换的键帽。更多信息，请参阅 [Raspberry Pi 500+ 机械按键](#raspberry-pi-500-机械按键)。操作说明请参阅[自定义背光](#自定义背光)和[更换键帽](#更换键帽)。
* 内置 256 GB M.2 SSD，预装树莓派系统，且可更换。操作说明请参阅[更换 M.2 SSD](#更换-m2-ssd)。
* 更大的内存（16 GB）。对比请参阅下表。

## 规格

下表列出各键盘计算机型号之间的主要相同点和不同点。

**键盘计算机型号规格对比**

|  | Raspberry Pi 400 | Raspberry Pi 500 | Raspberry Pi 500+ |
| :--- | :--- | :--- | :--- |
| **尺寸** | 286 × 122 × 23 mm | 286 × 122 × 23 mm | 312 × 123 × 35 mm |
| **按键** | 78、79 或 83 个薄膜按键，视地区版本而定 | 78、79 或 83 个薄膜按键，视地区版本而定 | 84、85 或 88 个机械按键，视地区版本而定 |
| **处理器** | 四核 64 位 Arm 处理器（1.8 GHz 的 Cortex-A72） | 四核 64 位 Arm 处理器（2.4 GHz 的 Cortex-A76） | 四核 64 位 Arm 处理器（2.4 GHz 的 Cortex-A76） |
| **SoC 和 I/O 控制器** | [BCM2711](chu-li-qi.md#bcm2711) SoC | [BCM2712](chu-li-qi.md#bcm2712) SoC 和 [RP1 I/O 控制器](https://www.raspberrypi.com/documentation/computers/io-controllers.html) | [BCM2712](chu-li-qi.md#bcm2712) SoC 和 [RP1 I/O 控制器](https://www.raspberrypi.com/documentation/computers/io-controllers.html) |
| **内存（RAM）** | 4 GB 同步动态 RAM（SDRAM） | 8 GB 同步动态 RAM（SDRAM） | 16 GB 同步动态 RAM（SDRAM） |
| **GPU** | 500 MHz 的 VideoCore VI | 910 MHz 的 VideoCore VII | 910 MHz 的 VideoCore VII |
| **视频输出** | 两个 micro-HDMI 端口，可提供单台 60 Hz 的 4K 显示器或两台 30 Hz 的 4K 显示器 | 两个 micro-HDMI 端口，可提供 60 Hz 的 4K 显示并支持 HDR | 两个 micro-HDMI 端口，可提供 60 Hz 的 4K 显示并支持 HDR |
| **散热控制** | 铝制一体化散热片 | 铝制一体化散热片 | 铝制一体化散热片 |
| **无线连接** | 双频（2.4 GHz 或 5 GHz）802.11ac Wi-Fi（120 Mb/s）和蓝牙（5 和 BLE） | 双频（2.4 GHz 或 5 GHz）802.11ac Wi-Fi（300 Mb/s）和蓝牙（5 和 BLE） | 双频（2.4 GHz 或 5 GHz）802.11ac Wi-Fi（300 Mb/s）和蓝牙（5 和 BLE） |
| **USB 端口** | 两个 USB 3.0 端口；一个 USB 2.0 端口 | 两个 USB 3.0 端口；一个 USB 2.0 端口 | 两个 USB 3.0 端口；一个 USB 2.0 端口 |
| **千兆（1 Gb/s）以太网（RJ45）** | 是 | 是 | 是 |
| **GPIO** | 水平 40 针 GPIO 排针 | 水平 40 针 GPIO 排针 | 水平 40 针 GPIO 排针 |
| **存储** | 存储卡槽 | 存储卡槽 | 存储卡槽和 M.2 SSD 驱动器（256 GB） |
| **电源输入** | 通过 USB-C 提供 5 V 3 A（15 W） | 通过 USB-C 提供 5 V 5 A（25 W），外设电流限制为 600 mA | 通过 USB-C 提供 5 V 5 A（25 W） |
| **电源按键** | 组合键（**Fn** + **F10**） | 专用按键 | 专用按键 |
| **可自定义性** | – | 按键重映射 | 按键重映射；RGB 背光；可更换键帽 |

## 键盘计算机与套件

Raspberry Pi 键盘计算机既可以单独购买，也可以作为套件的一部分购买，套件中包含入门所需的基本配件。

### Raspberry Pi 400 及套件

Raspberry Pi 400 键盘计算机于 2020 年发布，基于 Raspberry Pi 4（4 GB）。

![Raspberry Pi 400 键盘计算机](https://www.raspberrypi.com/documentation/computers/images/rpi400.jpg)

Raspberry Pi 400 套件包含以下物品：

* Raspberry Pi 400 键盘计算机。
* 15 W Raspberry Pi USB-C 电源适配器。
* Raspberry Pi USB 鼠标。
* 16 GB 存储卡，预装树莓派系统。
* micro-HDMI 线缆。
* 《初学者指南》图书。

### Raspberry Pi 500 及套件

Raspberry Pi 500 键盘计算机于 2024 年发布，基于 Raspberry Pi 5（8 GB）。

![Raspberry Pi 500 键盘计算机](https://www.raspberrypi.com/documentation/computers/images/rpi500.png)

Raspberry Pi 500 套件包含以下物品：

* Raspberry Pi 500 键盘计算机。
* 27 W Raspberry Pi USB-C 电源适配器。
* Raspberry Pi USB 鼠标。
* 32 GB A2 级存储卡，预装树莓派系统。
* micro-HDMI 线缆。
* 《初学者指南》图书。

### Raspberry Pi 500+ 键盘计算机及套件

Raspberry Pi 500+ 键盘计算机于 2025 年发布，基于 Raspberry Pi 5（16 GB）。

![Raspberry Pi 500+ 键盘计算机](https://www.raspberrypi.com/documentation/computers/images/rpi500plus.png)

Raspberry Pi 500+ 套件包含以下物品：

* Raspberry Pi 500+ 键盘计算机，内含一块预装树莓派系统的 SSD。
* 27 W Raspberry Pi USB-C 电源适配器。
* Raspberry Pi USB 鼠标。
* micro-HDMI 线缆。
* 撬棒（开口工具），用于接触 M.2 SSD（单独购买键盘时也会附带）。
* 拔键器，用于拆卸键帽（单独购买键盘时也会附带）。
* 《初学者指南》图书。

## 入门

本节将指导你为 Raspberry Pi 键盘计算机配置[树莓派系统（OS）](https://www.raspberrypi.com/documentation/computers/os.html#os-installation)、Wi-Fi 和外设（鼠标和显示器），以便将其作为台式计算机使用。有关设置 Raspberry Pi 的更详细指导，或想采用其他配置方式入门，请参阅[入门](ru-men.md)。

如果符合以下情况，你可以跳过[第 1 步：准备启动介质](#第-1-步准备启动介质)，改为从[第 2 步：连接外设](#第-2-步连接外设)开始：

* 你使用的是 Raspberry Pi 500+，它附带一块预装树莓派系统的 M.2 SSD。
* 你的 Raspberry Pi 400 或 500 是作为套件的一部分购买的，套件中包含一块预装树莓派系统的存储卡。

>**注意**
>
>首批 Raspberry Pi 500+ 键盘计算机预装的是上一版树莓派系统 Bookworm。较新的 Raspberry Pi 500+ 键盘计算机预装的是最新的树莓派系统 Trixie。

### 硬件前提条件

如果你不是通过键盘计算机套件来设置 Raspberry Pi 键盘计算机，则需要以下硬件：

* 一台 Raspberry Pi 400、500 或 500+。
* 适用于你的 Raspberry Pi 键盘计算机的官方 Raspberry Pi [电源适配器](ru-men.md#电源适配器)。
* 一张容量至少为 32 GB 的[存储卡](https://www.raspberrypi.com/documentation/accessories/sd-cards.html)，以及将其连接到另一台计算机的方法。以下情况需要存储卡：
  * 你没有使用键盘计算机套件来设置 Raspberry Pi 400 或 500。
  * 你使用的是 Raspberry Pi 500+，并且想使用存储卡而不是预装的 M.2 SSD 作为启动介质。
* 一台运行 Windows、macOS 或 Linux 的计算机，用于准备存储卡。如果你从 Raspberry Pi 500+ 内部预装的 M.2 SSD 启动，则不需要该计算机。
* 如果你想连接到网络，需要以下一项或两项：
  * 你的 Wi-Fi 凭据（SSID 和密码）。
  * 一根以太网线。
* 一个用于连接 Raspberry Pi 键盘计算机的 USB 鼠标。
* 一台用于连接 Raspberry Pi 键盘计算机的显示器或显示屏（以及合适的电源线）。为方便起见，我们推荐 [Raspberry Pi Monitor](https://www.raspberrypi.com/documentation/accessories/monitor.html)，你可以通过 Raspberry Pi 键盘计算机为其供电。
* 一根 micro-HDMI 转 HDMI 线缆，用于将显示器或显示屏连接到 Raspberry Pi 键盘计算机。

### 第 1 步：准备启动介质

仅当你的键盘计算机不是作为套件的一部分购买，或者你设置的是 Raspberry Pi 500+ 并想使用存储卡而不是预装的 M.2 SSD 时，才需要执行此步骤。

1. 在你的计算机上，[安装并启动树莓派启动盘制作工具](ru-men.md#树莓派启动盘制作工具的使用方法)。你可以使用该工具将[树莓派系统](https://www.raspberrypi.com/documentation/computers/os.html#os-installation)写入存储卡，使其成为 Raspberry Pi 键盘计算机的启动介质。
2. 按照 Imager 中的说明配置 Raspberry Pi 设备、操作系统、存储、自定义设置和 Imager 选项。有关应配置哪些内容的指导，请参阅[使用 Imager 安装](ru-men.md#树莓派启动盘制作工具的使用方法)中的第 2 步至第 4 步。
3. 将镜像写入存储卡。这样存储设备就变成了你的启动介质。
4. Raspberry Pi Imager 完成启动介质写入后，从计算机中安全取出存储卡，然后将其插入 Raspberry Pi 键盘计算机。从键盘计算机背面看，存储卡槽位于 USB 端口右侧、电源端口左侧。

如果你遇到任何问题、想更详细地设置设备，或想以其他方式开始使用 Raspberry Pi，请参阅[入门](ru-men.md)。

### 第 2 步：连接外设

对于台式计算机配置，你可以将以下外设直接连接到键盘计算机背面：

* USB 鼠标，可连接到白色的 USB 2.0 端口，把更快的 USB 3.0 端口留给你可能想连接的更高速外设。
* 根据需要连接一台或两台显示器。
  * 将线缆较大的一端（全尺寸 HDMI 端）连接到显示器。
  * 两个 micro-HDMI 端口均支持最高 4K 分辨率，但刷新率因型号而异；有关 Raspberry Pi 400、500 和 500+ 分辨率选项的更多详细信息，请参阅[配置显示设置](xi-tong-pei-zhi.md#显示)。
  * 显示器通常需要独立电源。如果你使用的是官方 [Raspberry Pi Monitor](https://www.raspberrypi.com/documentation/accessories/monitor.html)，可以通过连接到 Raspberry Pi 键盘计算机的 USB 线缆为显示器供电。打开键盘计算机后，它便为 Raspberry Pi Monitor 供电。
* 可选：用于音频输出的扬声器或耳机。
  * 你可以通过 micro-HDMI、USB 或蓝牙输出音频。
  * 官方 [Raspberry Pi Monitor](https://www.raspberrypi.com/documentation/accessories/monitor.html) 配有两个前置扬声器。你也可以通过显示器背面的 3.5 mm 音频插孔连接扬声器或耳机。

### 第 3 步：连接电源

将 Raspberry Pi 键盘计算机连接到电源即可开机。

* 在 **Raspberry Pi 400** 和 **500** 上，LED 状态灯会亮起，树莓派系统会执行首次启动设置流程。
* 在 **Raspberry Pi 500+** 上，键盘会亮起，树莓派系统会执行首次启动设置流程。

Raspberry Pi 键盘计算机启动可能需要 60 到 90 秒，在此期间你无需进行任何操作。

>**注意**
>
>如果你使用的是预装好系统的存储卡或 SSD，首次启动时会打开配置向导，帮助你配置键盘计算机。更多信息，请参阅[首次启动配置](ru-men.md#首次启动配置)。

之后，你可以使用 Raspberry Pi 400 上的 **Fn + F10**，或 Raspberry Pi 500 和 500+ 右上角的电源按键来开关键盘计算机。

### 第 4 步：连接网络（可选）

按照上述说明设置好键盘计算机后，你可以将其连接到网络。可以是有线（以太网）连接，也可以是无线（Wi-Fi）连接。有关这两种连接的详细说明，请参阅[入门](ru-men.md)页面中的[连接到网络](ru-men.md#网络)。

无线网络通常在[第 1 步：准备启动介质](#第-1-步准备启动介质)期间配置，但你也可以在桌面或命令行中配置无线连接。

如果你因为使用预装好系统的存储卡或 SSD 而跳过[第 1 步：准备启动介质](#第-1-步准备启动介质)，可以在首次启动时通过配置向导配置 Wi-Fi。更多信息，请参阅[首次启动配置](ru-men.md#首次启动配置)。

## Raspberry Pi 500+ 机械按键

Raspberry Pi 500+ 上的每个按键在键帽下方都有一个独立的机械轴体，用于记录按键操作。Raspberry Pi 500+ 使用 Gateron KS-33 矮轴机械开关。默认情况下，Gateron KS-33 轴体使用彩色轴心指示轴体类型（clicky 有声段落、tactile 段落感或 linear 线性）。Raspberry Pi 500+ 使用带定制灰色轴心的 clicky Gateron KS-33 轴体。

键帽安装在 Gateron 轴体顶部的十字形轴心上。这些轴体采用行业标准的 Cherry MX 兼容十字形轴心。有关在 Raspberry Pi 500+ 上拆卸和更换键帽的指导与说明，请参阅本页的[更换键帽](#更换键帽)。

## Raspberry Pi 500+ 自定义

Raspberry Pi 500+ 是最新的键盘计算机。它提供以下自定义选项：

* 可更换的 M.2 SSD 存储。操作说明请参阅[更换 M.2 SSD](#更换-m2-ssd)。
* 更换键帽套装。操作说明请参阅[更换键帽](#更换键帽)。
* 背光预设、颜色和亮度。操作说明请参阅[自定义背光](#自定义背光)。

对于更高级的用户，Raspberry Pi 500+ 还支持：

* 配置内置预设之外的 LED。
* 即时重新映射按键。

更多信息，请参阅[高级软件设置](#高级软件设置)。

### 更换 M.2 SSD

你可以通过更换 Raspberry Pi 500+ 中的 M.2 SSD 来扩展存储容量。也可以使用该插槽安装其他 PCIe 外设。Raspberry Pi 500+ 支持使用 M.2 M key 边缘连接器、外形尺寸为 2230、2242、2260 和 2280 的设备。

完成此操作需要十字螺丝刀、一字螺丝刀以及随附的塑料开口工具（撬棒）。

1. **拧下键盘螺丝。** 找到键盘底部的五颗螺丝，用十字螺丝刀将其拧下。请妥善保管螺丝。

   ![拧下键盘螺丝](https://www.raspberrypi.com/documentation/computers/images/M2-step-1.jpg)

2. **撬开键盘顶部与底部。** 将撬棒放入键盘前部的凹槽中，然后向上倾斜撬棒，开始分离键盘。

   ![撬棒](https://www.raspberrypi.com/documentation/computers/images/M2-step-2.jpg)

3. **使键盘顶部与底部分离。** 将撬棒楔入键盘前部的开口槽并沿槽滑动，使键盘顶部与底部分离。

   ![沿凹槽滑动撬棒](https://www.raspberrypi.com/documentation/computers/images/M2-step-3.jpg)

4. **打开键盘。** 将键盘底部放在平坦表面上，把键盘顶部翻转（不要提起）过来，使其正面朝下放在同一表面上。注意不要将顶部和底部完全拉开，因为它们通过柔性排线相连。

   ![翻转打开键盘](https://www.raspberrypi.com/documentation/computers/images/M2-step-4.jpg)

5. **松开 M.2 SSD。** 用手或一字螺丝刀逆时针转动 M.2 SSD 右侧的螺丝，将其拧松。取下螺丝并妥善保管。拧下螺丝后，M.2 SSD 会弹起。

   ![松开 M.2 SSD](https://www.raspberrypi.com/documentation/computers/images/M2-step-5.jpg)

6. **拔出 M.2 SSD。** 先将 M.2 SSD 向外拉，然后从键盘中取出。

   ![拔出 M.2 SSD](https://www.raspberrypi.com/documentation/computers/images/M2-step-6.jpg)

7. **安装新的 M.2 SSD。** 将另一块 M.2 SSD 滑入左侧的插槽。SSD 只能以一个方向装入。按住新插入的 M.2 SSD，装回其右侧的螺丝，并顺时针拧紧。
8. **合上键盘。** 将键盘顶部翻回键盘底部上方，并咔嗒一声扣回原位。
9. **拧紧键盘螺丝。** 用十字螺丝刀将五颗螺丝放回原位并拧紧。

### 更换键帽

你可以将 Raspberry Pi 500+ 上的默认键帽更换为自定义键帽套装。由于 Raspberry Pi 500+ 上的 Gateron KS-33 轴体采用行业标准的 Cherry MX 轴心形状，大多数专为 Cherry MX 设计的第三方键帽都兼容。避免选择较高的键帽高度，因为它们可能碰到键盘框架或产生过多噪音。有关选择替代键帽的更多指导，请参阅本节的[键盘布局](#键盘布局)、[键帽高度](#键帽高度)和[灯光](#灯光)。

拆卸键帽：

1. 将拔键器的两个爪脚插入要拆卸或更换的键帽两侧。让爪脚落到键帽下方。
2. 按压爪脚两侧以夹住键帽，确保两侧受力均匀。
3. 轻轻将键帽垂直向上拔出键盘。避免斜向拉拽。

>**注意**
>
>你也可以拆下键帽，以便清洁键帽下方。

现在你可以用另一个键帽替换它，或将同一键帽重新装回原位：

1. 对齐键帽：将键帽下方的十字形轴心与对应轴体上的十字形轴心对齐。
2. 轻轻但用力地按下键帽，直到键帽完全就位且感觉牢固。

#### 键盘布局

键帽有多种语言版本，其中美式布局最易获得，其次是英式布局。其他语言的键帽可能较难买到。

Raspberry Pi 500+ 键盘采用改进的 75% 布局，这意味着某些按键为非标准按键，典型键帽套装中可能没有匹配的键帽：

* **电源键。** 键盘右上角的电源键可能不包含在其他键帽套装中。
* **灯光标识。** Raspberry Pi 500+ 的 **F4**、**F5** 和 **F6** 键上的灯光标识为非标准标识。
* **音量标识。** Raspberry Pi 500+ 的 **F10**、**F11** 和 **F12** 键上的音量标识为非标准标识。
* **系统请求键。** Raspberry Pi 500+ 上的 **SysRq** 键为非标准按键。
* **插入键。** Raspberry Pi 500+ 上的 **Ins** 键为非标准按键。
* **Command 键。** 在键帽套装中，**Cmd** 键通常标为 **Win**，而且第三方键帽套装不包含 Raspberry Pi 标志。

#### 键帽高度

Raspberry Pi 500+ 附带的矮键帽具有传统机械按键的手感，同时保持键盘紧凑。对于替换键帽，我们推荐 **DSA** 或 **Cherry** 高度：

* **DSA** 键帽为平顶高度，可以在不同行之间互换。
* **Cherry** 键帽通常兼容，但为了符合人体工学，每一行采用了不同的曲面高度。这意味着每一行的高度或角度可能略有不同。为获得一致的手感，请检查行对齐。

>**注意**
>
>不建议使用 **XDA**、**OEM** 和 **SA** 键帽，因为它们较高，可能产生更多噪音或碰到键盘框架。

#### 灯光

Raspberry Pi 500+ 键盘上的 LED 照亮键帽的上半部分，因此完全不透明的键帽可能会挡住光线。

### 自定义背光

Raspberry Pi 500+ 默认关闭大部分背光。默认仅启用以下灯光：

* Raspberry Pi 500+ 键盘开启时，电源键后方的活动 LED。该 LED：
  * 在 Raspberry Pi 500+ 接通电源但处于关闭状态时呈红色。
  * 在 Raspberry Pi 500+ 开启时呈绿色。
  * 随存储卡活动闪烁。
* 启动 Raspberry Pi 500+ 键盘时，按键上流动的彩虹灯光动画。高级用户可以使用配置软件为特定背光预设关闭该动画。更多信息，请参阅[高级软件设置](#高级软件设置)中的[更改预设启动动画](#更改预设启动动画)。
* Caps Lock 指示灯，在启用时亮起。

Raspberry Pi 500+ 还支持其他 RGB 背光预设，由 [Vial QMK 固件](https://github.com/raspberrypi/vial-qmk)提供支持。操作说明请参阅[选择背光预设](#选择背光预设)。

#### 选择背光预设

Raspberry Pi 500+ 附带七个预设，即保存在 Raspberry Pi 500+ 键盘上的灯光配置。要向前循环切换这些预设，请按键盘上的 **Fn** + **F4**；要向后循环切换，请按键盘上的 **Fn** + **Shift** + **F4**。

|  | 预设名称 | 说明 |
| :---: | :--- | :--- |
| **0** | **Off**（关闭） | 默认预设，仅点亮电源键、启动动画和 Caps Lock 指示灯。 |
| **1** | **Solid Colour White**（纯白） | 纯白色背光。 |
| **2** | **Solid Colour**（纯色） | 纯色背光，你可以使用 **Fn** + **F3** 更改颜色。 |
| **3** | **Gradient Left Right**（左右渐变） | 固定的彩虹背光。 |
| **4** | **Cycle Pinwheel**（循环风车） | 动画彩虹背光，按键以彩虹图案在键盘上循环显示不同颜色。 |
| **5** | **Typing Heatmap**（打字热力图） | 按键次数越多，颜色越接近红色，周围按键也会越亮。 |
| **6** | **Solid Reactive Simple**（纯色反应简单模式） | 反应式键盘，按下按键时按键会亮起。你可以使用 **Fn** + **F3** 选择颜色。 |

#### 背光控制

你可以使用以下键盘快捷键自定义 RGB 背光颜色（取决于预设）和亮度：

* **更改颜色。** 按 **Fn** + **F3** 向前循环切换 16 种背光颜色；按 **Fn** + **Shift** + **F3** 向后循环切换。
* **调整亮度。** 按 **Fn** + **F5** 降低亮度；按 **Fn** + **F6** 提高亮度。

>**注意**
>
>键盘上的 **Shift** 键要么向后循环切换可用选项，要么反转按键功能。例如，**Fn** + **Shift** + **F5** 会提高亮度而不是降低亮度。

## 高级软件设置

Raspberry Pi 提供用于控制 Raspberry Pi 500 和 500+ 内置键盘的固件。使用此工具，你可以：

* 为 Raspberry Pi 500+ 启用并配置高级 LED 设置。更多信息，请参阅[高级 LED 设置](#高级-led-设置)。
* 在 Raspberry Pi 500 和 500+ 上重新映射按键。更多信息，请参阅[重新映射键盘按键](#重新映射键盘按键)。
* 在 Raspberry Pi 500+ 上玩一个 Flappy Bird 风格的游戏。相关信息请参阅 [Flappy Bird 游戏](#flappy-bird-游戏)。

有关本页所述内容之外的更多信息和选项，请参阅 GitHub 上[配置工具的 README](https://github.com/raspberrypi/rpi-keyboard-config/blob/main/README.md)。

### 固件设置

要使用软件控制的灯光并重新映射按键，必须首先更新键盘固件并安装配置工具：

1. 安装固件更新包。运行以下命令：`sudo apt install rpi-keyboard-fw-update`。
2. 更新到最新的键盘固件，该固件会检查并安装高级功能所需的固件。运行以下命令：`sudo rpi-keyboard-fw-update`。
3. 安装配置工具，它可用于调整 LED 和重新映射按键。运行以下命令：`sudo apt install rpi-keyboard-config`。

你可以在 GitHub 上的 [Vial QMK](https://github.com/raspberrypi/vial-qmk) 存储库中查看键盘固件源代码。

### 基本信息命令

在自定义键盘计算机的灯光或重新映射按键之前，可根据需要使用以下命令查看其当前状态。

| 命令 | 说明 |
| :--- | :--- |
| `rpi-keyboard-config info --ascii` | 查看键盘型号、锁定状态和布局图。如果不需要布局图，请从命令中删除 `--ascii`。 |
| `rpi-keyboard-config help` | 列出所有可用命令及其简要说明。 |
| `rpi-keyboard-config list-effects` | 列出所有可用的灯光效果，可临时应用或应用到预设。 |
| `rpi-keyboard-config preset get` | 列出所有当前预设，编号为 0 到 6。 |

### 高级 LED 设置

高级用户可以自定义 Raspberry Pi 500+ 基本预设之外的背光。具体来说，`rpi-keyboard-config` 软件允许你：

* 为 Raspberry Pi 500+ 添加其他灯光效果，可临时应用或保存为预设。相关信息请参阅[灯光效果](#灯光效果)。
* 为每个预设设置不同的启动动画。相关信息请参阅[更改预设启动动画](#更改预设启动动画)。
* 为效果或预设添加速度、饱和度和色相参数。相关信息请参阅[效果和预设参数](#效果和预设参数)。
* 控制全局色相和亮度。相关信息请参阅[全局灯光控制](#全局灯光控制)。
* 通过配置并应用 `direct` 效果来控制单个 LED 的灯光。相关信息请参阅[单个 LED 控制](#单个-led-控制)。

>**注意**
>
>高级 LED 设置仅适用于 Raspberry Pi 500+，因为只有该型号的键盘计算机具有背光按键。

#### 灯光效果

你可以通过各种效果和参数控制 Raspberry Pi 500+ 的背光。除电源按键不受任何效果影响外，键盘灯光效果均通过配置软件控制。使用该软件，你可以：

* 临时对键盘应用一个效果，直到键盘关机并重新启动，或直到你再次开始循环切换预设。循环切换预设时，会从应用临时效果之前的最后一个预设继续。
* 将效果分配给七个键盘预设之一。默认预设列于[选择背光预设](#选择背光预设)。你还可以为预设添加参数和启动动画。

使用以下命令选择、应用和查看键盘上的临时效果。

| 命令 | 说明 |
| :--- | :--- |
| `rpi-keyboard-config list-effects` | 列出可用的灯光效果。 |
| `rpi-keyboard-config effect "effect-name"` | 临时应用一个效果，将 `effect-name` 替换为上一条命令输出中列出的效果名称。 |
| `rpi-keyboard-config effect` | 查看当前活动的效果。 |

你还可以调整效果的以下参数：速度、饱和度和色相。例如，以下命令将 `"Cycle Spiral"` 效果的速度更改为 42。

```bash
$ rpi-keyboard-config effect "Cycle Spiral" --speed 42
```

添加的任何参数都必须是 0 到 255 之间的数字。有关这些参数的更多信息，包括何时适合添加、何时不适合添加，请参阅[效果和预设参数](#效果和预设参数)。

#### 查看预设

你可以使用配置软件查看当前所在的预设、在预设之间切换，或查看每个预设的详细信息。每个预设都有一个 0 到 6 之间的索引号，对应七个可用槽位。

| 命令 | 说明 | 示例（假设为默认预设） |
| :--- | :--- | :--- |
| `rpi-keyboard-config preset index` | 显示当前预设的索引。 | 如果你当前位于 **Gradient Left Right**（左右渐变）预设，该命令会显示你位于预设 3。 |
| `rpi-keyboard-config preset index X` | 跳到预设循环中的其他位置，其中 `X` 是预设的索引（`0` 到 `6` 之间的数字）。 | 以下命令会切换到 **Typing Heatmap**（打字热力图）预设：`rpi-keyboard-config preset index 5`。 |
| `rpi-keyboard-config preset get` | 列出所有当前预设。 | 该命令会列出七个预设，编号为 0 到 6。默认预设的概述见[选择背光预设](#选择背光预设)。 |
| `rpi-keyboard-config preset get X` | 显示特定预设的详细信息，其中 `X` 是预设的索引（`0` 到 `6` 之间的数字）。 | 以下命令会显示预设 5 是 **Typing Heatmap**（打字热力图）预设：`rpi-keyboard-config preset get 5`。 |

#### 重新分配预设

你可以重新分配预设，使其使用不同的效果。有关效果的信息，包括如何获取可用效果列表，请参阅[灯光效果](#灯光效果)。

>**注意**
>
>你对预设所做的更改会在每次重启 Raspberry Pi 500+ 后保留。你可以随时按照[重置预设和 LED 自定义](#重置预设和-led-自定义)中的说明将预设恢复为默认值。

以下示例将 **Gradient Left Right**（左右渐变，`3`）预设更改为引号中指定的效果。

```bash
$ rpi-keyboard-config preset set 3 "effect-name"
```

重新分配预设时，可以添加以下一个或多个参数：速度、色相或饱和度。你还可以为该预设设置特定的启动动画。有关这些选项的信息，请参阅[效果和预设参数](#效果和预设参数)和[更改预设启动动画](#更改预设启动动画)。

例如，以下命令将默认的 **Gradient Left Right**（左右渐变）预设替换为 **Rainbow Beacon** 效果，速度为 140。它还会替换该预设的默认启动动画，使启动动画在白色 LED 上结束，然后淡入 **Rainbow Beacon** 效果。

```bash
$ rpi-keyboard-config preset set 3 "Rainbow Beacon" --speed 140 --startup-animation "START_ANIM_W_FADE_SAT"
```

#### 更改预设启动动画

对于每个预设，你可以使用以下命令指定启动动画：

```bash
$ --startup-animation "name_of_animation"
```

将 `name_of_animation` 替换为以下五种可能的启动动画之一：

| 启动动画名称 | 说明 |
| :--- | :--- |
| `START_ANIM_NONE` | 无启动动画。 |
| `START_ANIM_B_NO_FADE` | 脉冲彩虹动画，随后 LED 熄灭，然后立即进入所选效果。 |
| `START_ANIM_B_FADE_VAL` | 脉冲彩虹动画，随后 LED 熄灭并淡入所选效果。这是**默认**启动动画。 |
| `START_ANIM_W_NO_FADE` | 脉冲彩虹动画，随后 LED 变为白色，然后立即进入所选效果。 |
| `START_ANIM_W_FADE_SAT` | 脉冲彩虹动画，随后 LED 变为白色并淡入所选效果。 |

例如，以下命令会将预设 3 的启动动画替换为脉冲彩虹动画，该动画在白色 LED 上结束，然后淡入该预设：

```bash
$ rpi-keyboard-config preset set 3 --startup-animation "START_ANIM_W_FADE_SAT"
```

#### 效果和预设参数

你可以为任何效果或预设添加以下速度、饱和度和色相参数：

* **速度。** 要设置速度，请在命令中添加 `--speed X`，其中 `X` 是 0 到 255 之间的数字。如果不添加速度参数，默认速度为 128。
* **饱和度。** 要设置饱和度，请在命令中添加 `--sat X`，其中 `X` 是 0 到 255 之间的数字。如果不添加饱和度参数，默认值为 255（最大饱和度）。
* **色相。** 要设置色相，请在命令中添加 `--hue X`，其中 `X` 是 0 到 255 之间的数字。如果不设置色相，默认使用键盘的全局色相，该色相通过键盘上的 **Fn + F3** 设置。更多信息，请参阅[背光控制](#背光控制)。

某些效果和预设不受某些参数影响。例如，纯色是一种静态效果，因此不受速度更改的影响。

#### 全局灯光控制

色相和亮度的管理范围为 0 到 255。你可以通过在 `rpi-keyboard-config` 命令中添加 `hue` 和 `brightness` 来查看和设置 Raspberry Pi 500+ 的色相与亮度。

| 命令 | 说明 |
| :--- | :--- |
| `rpi-keyboard-config hue` | 显示 Raspberry Pi 500+ 当前的全局色相（颜色）。 |
| `rpi-keyboard-config hue X` | 设置全局色相，其中 `X` 是 0 到 255 之间的数字。 |
| `rpi-keyboard-config brightness` | 显示 Raspberry Pi 500+ 当前的灯光亮度。 |
| `rpi-keyboard-config brightness X` | 设置灯光亮度，其中 `X` 是 0 到 255 之间的数字。 |

#### 单个 LED 控制

你可以自定义 Raspberry Pi 500+ 上单个 LED 的背光。这对于精确的视觉调整和创建独特的背光图案很有用。

你可以进行的所有单个 LED 自定义都会应用到名为 `direct` 的效果。然后，你可以通过以下任一方式应用 `direct` 效果：

* 按照[灯光效果](#灯光效果)中的说明临时应用。
* 按照[重新分配预设](#重新分配预设)中的说明将其分配给某个预设。

如果尚未通过上述任一方法应用 `direct` 效果，则在运行任何单个 LED 自定义命令时，会自动临时应用该效果。

下表列出了设置 LED 颜色（全局或单个 LED）以及保存和加载 LED 配置的命令。

| 命令 | 说明 |
| :--- | :--- |
| `rpi-keyboard-config leds clear` | 关闭除电源按键外的所有 LED。 |
| `rpi-keyboard-config leds set --colour <colour>` | 指定所有 LED 的颜色。将 `<colour>` 替换为常见颜色名称（例如 `red`）、用引号括起来的 0 到 255 的 HSV 数值（例如 `"0,255,255"`），或用引号括起来的 RGB 数值（例如 `"rgb(255,0,0)"`）。 |
| `rpi-keyboard-config led set "<row>,<column>" --colour <colour>` | 指定特定 LED 的颜色，其中 LED 由行列坐标（`"<row>,<column>"`）表示。你可以使用以下命令查看 LED 的行列坐标以及每个按键当前的设置：`rpi-keyboard-config info --ascii`。 |
| `rpi-keyboard-config leds save` | 保存 LED 配置。要使用保存的配置，你可以按照[重新分配预设](#重新分配预设)中的说明将 `direct` 效果分配给某个预设，或使用下面的 `load` 命令直接加载配置。 |
| `rpi-keyboard-config leds load` | 临时应用 `direct` 效果以加载保存的 LED 配置。如果你尚未将 `direct` 效果分配给预设，这会很有用。 |

在以下示例中，行列坐标（`"2,6"`）所指向的特定 LED 使用色相-饱和度-明度（HSV）数值（`"85,255,255"`）设置为绿色：

```bash
$ rpi-keyboard-config led set "2,6" --colour "85,255,255"
```

#### 重置预设和 LED 自定义

以下命令将预设重置为默认设置，并清除保存的 LED 自定义：

```bash
$ rpi-keyboard-config reset-presets
```

### 重新映射键盘按键

高级用户可以重新映射 Raspberry Pi 500 和 500+ 上的按键，从而自定义键盘布局，以匹配你的工作流程或游戏需求。

使用 `rpi-keyboard-config` 软件可以：

* 列出可用于重新映射的所有键码。相关信息请参阅[列出键码](#列出键码)。
* 查看当前键位映射。相关信息请参阅[查看键位映射](#查看键位映射)。
* 重新映射键盘上的按键。相关信息请参阅[重新映射按键](#重新映射按键)。
* 在配置软件中监视按键按下。相关信息请参阅[监视按键按下](#监视按键按下)。
* 最多编辑四层键位映射。相关信息请参阅[管理层](#管理层)。
* 在 Raspberry Pi 500 和 500+ 上使用 [Vial](https://get.vial.today/) 重新映射按键。相关信息请参阅[使用 Vial 重新映射按键](#使用-vial-重新映射按键)。
* 将键盘重置为默认键位映射。相关信息请参阅[重置为默认键盘布局](#重置为默认键盘布局)。

#### 列出键码

要重新映射键盘，你需要知道想在 Raspberry Pi 500 或 500+ 上分配的按键的键码。以下命令列出所有可能的键码：

```bash
$ rpi-keyboard-config list-keycodes
```

你还可以使用 `--category` 仅列出特定类别中的键码。例如，以下命令列出 `basic` 类别中的所有键码：

```bash
$ rpi-keyboard-config list-keycodes --category basic
```

#### 查看键位映射

使用以下命令查看键盘上所有位置的当前键位映射：

```bash
$ rpi-keyboard-config key get-all
```

使用以下命令查看特定按键的键码，位置由该按键的行列坐标指定。将 `<row>` 和 `<column>` 替换为相应的数字：

```bash
$ rpi-keyboard-config key get <row> <column>
```

>**注意**
>
>你可以使用 `rpi-keyboard-config info --ascii` 查看按键的行列坐标。该命令会提供键盘布局图。

例如，要获取键盘上 **Q** 键（行列坐标为 `2 2`）的键码：

```bash
$ rpi-keyboard-config key 2 2
```

#### 重新映射按键

使用以下命令在按键的行列坐标所指定的位置设置不同的键码。将 `<row>` 和 `<column>` 替换为相应的数字，将 `<keycode>` 替换为要映射到该按键的键码。

```bash
$ rpi-keyboard-config key set <row> <column> <keycode>
```

>**注意**
>
>你可以使用 `rpi-keyboard-config info --ascii` 查看按键的行列坐标。你可以使用 `rpi-keyboard-config list-keycodes` 查看按键的键码。

例如，如果你想将键盘上的 **Q** 键（行列坐标为 `2 2`）重新映射为 **R** 键（键码为 `KC_R`）：

```bash
$ rpi-keyboard-config key set 2 2 KC_R
```

#### 监视按键按下

你可以读取按键状态，在配置工具中监视按键活动，了解哪些按键被按下和释放。在此之前，必须先解锁键盘。

检查键盘的锁定状态：

```bash
$ rpi-keyboard-config info
```

解锁键盘以便随后监视按键按下：

```bash
$ rpi-keyboard-config unlock
```

配置工具会引导你按住特定按键，直到倒计时结束。默认情况下，这些按键是 **Enter** + **Escape**，它们会亮起红光为你提供指引。如果你重新映射了这些按键，解锁序列使用的是这些按键的物理位置，而不是它们的新标签；命令会告诉你针对你的设置应按下哪些重新映射后的按键。

键盘解锁后，你可以使用以下命令监视按键活动：

```bash
$ rpi-keyboard-config key watch
```

每当按下或释放按键时，终端都会输出信息。作为 LED 反馈，按下键盘上的按键时，相应按键也会亮起红光。要在监视按键按下时关闭点亮功能，请在上面的命令中添加 `--no-leds`：

```bash
$ rpi-keyboard-config key watch --no-leds
```

完成后请锁定键盘。以下 `lock` 命令无需任何确认，会立即锁定键盘。

```bash
$ rpi-keyboard-config lock
```

#### 管理层

你可以在不同层上设置不同的键位映射。可编辑的层有四层，编号为 0–3；默认层为 0。默认情况下，**Fn** 键会将键盘从层 0 切换到层 1。你可以根据需要将 `--layer` 添加到以下任一命令中：

* `rpi-keyboard-config key get-all`
* `rpi-keyboard-config key get`
* `rpi-keyboard-config key set`

#### 使用 Vial 重新映射按键

你可以使用 Vial 网页界面重新映射按键。Vial 与键盘固件配合，可实时配置键盘。

1. 在 Raspberry Pi 500 或 500+ 上，访问 [Vial 网页界面](https://vial.rocks/)。
2. 在出现的窗口中，选择你的键盘，然后选择 **Connect**。
3. 使用 Vial 网页界面更改键位映射。

有关如何使用 Vial 的信息，请参阅 [Vial 文档](https://get.vial.today/)。

>**重要**
>
>我们建议仅使用 Vial 处理键位映射，不要用它自定义 RGB LED。

#### 重置为默认键盘布局

以下命令将键盘布局重置为默认键位映射，包括重置所有层：

```bash
$ rpi-keyboard-config reset-keymap
```

### 恢复默认设置

由软件控制的偏好设置保存在闪存中，并在重启和固件更新后保留。要重置背光设置和键盘布局，请使用以下命令擦除存储这些设置的闪存区域：

```bash
$ sudo rpi-keyboard-fw-update -w -i
```

这会清除所有自定义设置，并将键盘恢复为默认背光和键位映射。

如果键盘布局配置错误到无法在 Raspberry Pi 500+ 上输入的程度，你仍然可以通过将外接 USB 键盘连接到任一可用 USB 端口，并改用该设备输入命令，来完成恢复默认设置的操作。

### Flappy Bird 游戏

为了增添一些乐趣，以下命令允许你使用键盘背光在 Raspberry Pi 500+ 上玩一个简单的 Flappy Bird 风格游戏：

```bash
$ rpi-keyboard-config game
```

游戏将键盘背光用作“屏幕”，灯光以特定图案闪烁来表示小鸟和管道。你的目标是让小鸟避开管道，与经典的 Flappy Bird 类似。按空格键可以让小鸟飞过管道（点亮的 LED）。如果不按空格键，“小鸟”会持续下落。你的得分取决于成功通过的管道数量，键盘顶部紫色 LED 的数量会显示该分数。

要退出游戏，请按键盘上的 **Q**。
