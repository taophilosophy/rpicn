# 显示器

## Raspberry Pi 触摸显示屏

Raspberry Pi 触摸显示屏是一款液晶显示屏，可通过 DSI 连接器连接到 Raspberry Pi。您可以同时使用触摸显示屏和 HDMI 显示输出。

![The Raspberry Pi 7-inch Touch Display](https://www.raspberrypi.com/documentation/accessories/images/display.png)

Raspberry Pi 7 英寸触摸显示屏

触摸显示屏与除了 Raspberry Pi Zero 和 Zero 2 W 外的所有 Raspberry Pi 型号兼容，这两款型号缺少 DSI 连接器。最早的 Raspberry Pi 型号缺少适当的安装孔，需要额外的安装硬件来安装显示屏 PCB 上的支架。

该显示屏具有以下关键特性：

* 800×480 RGB LCD 显示屏
* 24 位色彩
* 工业品质：水平 140 度视角，垂直 120 度视角
* 10 点多点触摸触摸屏
* 通过 I2C 接口进行 PWM 背光控制和电源控制
* 金属框架背面带有安装点，可用于树莓派显示转换板和树莓派
* 背光寿命：20000 小时
* 工作温度：-20 至+70 摄氏度
* 存储温度：-30 至+80 摄氏度
* 对比度：500
* 平均亮度：250 cd/m^2^
* 视角（度）：
  * 顶部 - 50
  * 底部 - 70
  * 左侧 - 70
  * 右侧 - 70
* 功率要求：典型值为 5V 时 200mA，在最大亮度下。
* 外部尺寸：192.96 × 110.76 毫米
* 可视区域：154.08 × 85.92 毫米

### 安装触摸显示屏

您可以使用支架将 Raspberry Pi 安装在触摸显示屏背面，然后连接适当的电缆。如果有可用的机箱，您也可以将触摸显示屏安装在单独的机箱中。连接保持不变，但根据机箱的不同，您可能需要更长的电缆。

![Image of Raspberry Pi connected to the Touch Display](https://www.raspberrypi.com/documentation/accessories/images/GPIO_power-500x333.jpg)

连接到触摸显示屏的 Raspberry Pi

将扁平柔性电缆（FFC）的一端连接到触摸显示 PCB 上的 RPI-DISPLAY 端口。银色或金色接触点应远离显示屏。然后将另一端的 FFC 连接到 Raspberry Pi 上的 DISPLAY 端口。这一端的接触点应朝向 Raspberry Pi。

如果 FFC 没有完全插入或位置不正确，您将在显示屏上遇到问题。在故障排除时，特别是如果您在显示屏上看不到任何内容或显示屏只显示单一颜色时，您应始终仔细检查此连接。

| NOTE | 触摸显示屏的机械图可供下载。 |
| ------ | ------------------------------ |

### 为触摸显示屏供电

我们建议使用树莓派的 GPIO 为触摸显示屏供电。或者，您可以直接使用单独的微型 USB 电源为显示屏供电。

#### 从树莓派供电

要使用 Raspberry Pi 为触摸显示屏供电，您需要在 Raspberry Pi 的 GPIO 上的 5V 和 GND 引脚之间以及显示屏上的 5V 和 GND 引脚之间连接两根跳线。如下图所示。

![Illustration of display pins](https://www.raspberrypi.com/documentation/accessories/images/display_plugs.png)

显示屏的 5V 和 GND 引脚的位置

在开始之前，请确保 Raspberry Pi 已关闭电源并且未连接到任何电源。将黑色跳线的一端连接到 Raspberry Pi 上的引脚六 ( GND )，将红色跳线的一端连接到引脚四 (5V)。如果引脚六不可用，您可以使用任何其他开放的 GND 引脚来连接黑线。如果引脚四不可用，您可以使用任何其他 5V 引脚来连接红线，例如引脚二。

![Illustration of Raspberry Pi headers](https://www.raspberrypi.com/documentation/accessories/images/pi_plugs.png)

Raspberry Pi 标头的位置

接下来，将黑线的另一端连接到显示器上的 GND 引脚，将红线的另一端连接到显示器上的 5V 引脚。完成所有连接后，下次打开 Raspberry Pi 时，您应该会看到触摸显示屏打开。

使用触摸显示屏上的另外三个引脚将显示器连接到原始 Raspberry Pi 1 Model A 或 B。有关更多信息，请参考我们关于旧版支持的文档。

| NOTE | 要识别原始的 Raspberry Pi，请检查 GPIO 头连接器。只有原始型号有 26 个引脚的 GPIO 头连接器；后续型号有 40 个引脚。 |
| ------ | ------------------------------------------------------------------------------------------------------------------- |

#### 从微型 USB 电源供应器供电

如果您不想使用 Raspberry Pi 为触摸显示屏提供电源，可以使用微型 USB 电源适配器。我们建议使用 Raspberry Pi 12.5W 电源适配器，以确保显示屏正常运行。

如果选择使用 micro USB 供电，请不要将 Raspberry Pi 的 GPIO 引脚连接到显示器上。两个板之间唯一的连接应该是扁平柔性电缆。

| WARNING | 使用 micro USB 电缆为显示器供电时，将其安装在一个机箱内，在使用过程中阻止访问显示器的 PCB。 |
| --------- | --------------------------------------------------------------------------------------------- |

### 使用屏幕键盘

在 Raspberry Pi OS Bookworm 及更高版本中，您可以将 wvkbd 屏幕键盘用作输入设备。要安装 wvkbd ，请运行以下命令：

```
$ sudo apt install wvkbd
```

| TIP | 在旧版 Raspberry Pi OS 发行版中，您可以使用 matchbox-keyboard 代替。 |
| ----- | ---------------------------------------------------------------------- |

### 更改屏幕方向

如果您想要在物理上旋转显示屏，或者将其安装在特定位置，您可以使用软件调整屏幕的方向，以更好地匹配您的设置。

#### 从桌面旋转屏幕

要从桌面环境设置屏幕方向，请从“首选项”菜单中选择“屏幕配置”。在布局编辑器中右键单击 DSI-1 显示矩形，选择“方向”，然后选择最适合您需求的选项。您还可以通过“触摸屏”选项确保触摸叠加层分配给正确的显示屏。

![Screenshot of orientation options in screen configuration](https://www.raspberrypi.com/documentation/accessories/images/display-rotation.png)

#### 在没有桌面的情况下旋转屏幕

要在缺少桌面环境的设备上设置屏幕方向，请编辑 /boot/firmware/cmdline.txt 配置文件，向系统传递一个方向。将以下行添加到 cmdline.txt ：

```
video=DSI-1:800x480@60,rotate=<rotation-value>
```

用以下值替换 <rotation-value> 占位符，这些值对应于相对于显示器默认值的旋转度数：

* `0`
* `90`
* `180`
* `270`

例如，旋转值为 90 会将显示旋转 90 度到右侧。 180 将显示旋转 180 度，或者颠倒。

| NOTE | 使用 cmdline.txt 无法单独旋转 DSI 显示器，与 HDMI 显示器分开。当同时使用 DSI 和 HDMI 时，它们共享相同的旋转值。 |
| ------ | ----------------------------------------------------------------------------------------------------------------- |

#### 旋转触摸输入

| WARNING | 通过设备树旋转触摸输入可能会与您的输入库发生冲突。在可能的情况下，请在您的输入库或桌面中配置触摸事件旋转。 |
| --------- | ------------------------------------------------------------------------------------------------------------ |

触摸输入的旋转与显示本身的方向无关。要更改此设置，您需要在 /boot/firmware/config.txt 中手动添加 dtoverlay 指令。在 config.txt 中添加以下行：

```
dtoverlay=vc4-kms-dsi-7inch,invx,invy
```

然后，通过从 config.txt 中删除以下行（如果存在）来禁用自动显示检测：

```
display_auto_detect=1
```

#### 触摸显示设备树选项参考

vc4-kms-dsi-7inch 叠加支持以下选项：

| DT 参数 | 行动                      |
| --------- | --------------------------- |
| `sizex`        | 设置 X 分辨率（默认 800） |
| `sizey`        | 设置 Y 分辨率（默认 480） |
| `invx`        | 反转 X 坐标               |
| `invy`        | 反转 Y 坐标               |
| `swapxy`        | 交换 X 和 Y 坐标          |
| `disable_touch`        | 完全禁用触摸叠加          |

要指定这些选项，请将它们用逗号分隔添加到您的 dtoverlay 行中的 /boot/firmware/config.txt 。当存在时，布尔值默认为 true，但您可以使用后缀“=0”将其设置为 false。整数值需要一个值，例如 sizey=240 。例如，要将 X 分辨率设置为 400 像素并反转 X 和 Y 坐标，请使用以下行：

```
dtoverlay=vc4-kms-dsi-7inch,sizex=400,invx,invy
```

## 旧版支持

| WARNING | 这些说明仅适用于原始 Raspberry Pi、Model A 和 B 版本的板卡。要识别原始 Raspberry Pi，请检查 GPIO 头连接器。只有原始型号有一个 26 引脚的 GPIO 头连接器；后续型号有 40 个引脚。 |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Raspberry Pi 1 Model A 和 B 版本上的 DSI 连接器没有与触摸屏控制器和 DSI 控制器通信所需的 I2C 连接。为了解决这个问题，请使用显示套件附带的额外一组跳线。将 GPIO 头上的 SCL/SDA 连接到显示板上标有 SCL/SDA 的水平引脚。使用跳线电缆通过 GPIO 引脚为 Model A/B 供电。

这些板卡上默认禁用了 DSI 显示自动检测。要启用检测，请在 /boot/firmware/config.txt 文件中添加以下行：

```
ignore_lcd=0
```

通过显示板上的 PWR IN 微型 USB 连接器为设置供电。不要通过 Raspberry Pi 的微型 USB 端口为设置供电。这将超过输入保险丝的最大电流额定值，因为显示屏大约消耗 400mA。
