# 显示器

## 树莓派触摸显示屏

树莓派触摸显示屏是一款可通过 DSI 连接器连接到树莓派的液晶显示屏。您可以同时使用触摸显示屏和 HDMI 显示输出。

![The Raspberry Pi 7-inch Touch Display](https://www.raspberrypi.com/documentation/accessories/images/display.png)

树莓派 7 英寸触摸显示屏

触摸显示屏与除了树莓派 Zero 和 Zero 2 W 外的所有树莓派型号兼容（这两款型号没有 DSI 接口）。最早的树莓派型号缺少适当的安装孔，需要额外的硬件来安装显示屏 PCB 上的支架。

该显示屏具有以下关键参数：

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
* 功率要求：在最大亮度下，典型值为 5V 200mA。
* 外部尺寸：192.96 × 110.76 毫米
* 可视区域：154.08 × 85.92 毫米

### 安装触摸显示屏

您可以使用支架将树莓派安装在触摸显示屏背面，然后连接适当的电缆。如果有可用的机箱，您也可以将触摸显示屏安装在单独的机箱中。连接保持不变，但根据机箱的不同，您可能需要更长的电缆。

![Image of Raspberry Pi connected to the Touch Display](https://www.raspberrypi.com/documentation/accessories/images/GPIO_power-500x333.jpg)

连接到触摸显示屏的树莓派

将扁平柔性电缆（FFC）的一端连接到触摸显示 PCB 上的 RPI-DISPLAY 接口。银色或金色接触点应远离显示屏。然后将另一端的 FFC 连接到树莓派上的 DISPLAY 接口。此接口的接触点应朝向树莓派。

如果 FFC 没有完全插入或位置不正确，您将在显示屏上遇到问题。在故障排除时，特别是如果您在显示屏上看不到任何内容或显示屏只显示单一颜色时，您应始终仔细检查连接状况。

>**注意**
>
>触摸显示屏的机械图可供下载。

### 为触摸显示屏供电

我们建议使用树莓派的 GPIO 为触摸显示屏供电。或者您可以直接使用单独的 Mirco USB 电源适配器为显示屏供电。

#### 用树莓派供电

要使用树莓派为触摸显示屏供电，您需要在树莓派的 GPIO 上的 5V 和 GND 引脚之间以及显示屏上的 5V 和 GND 引脚之间连接两根跳线。如下图所示。

![Illustration of display pins](https://www.raspberrypi.com/documentation/accessories/images/display_plugs.png)

显示屏的 5V 和 GND 引脚的位置

在开始之前，请确保树莓派已关机且未连接到任何电源。将黑色跳线的一端连接到树莓派上的引脚六 ( GND )，将红色跳线的一端连接到引脚四 (5V)。如果引脚六不可用，您可以使用任何其他开放的 GND 引脚来连接黑线。如果引脚四不可用，您可以使用任何其他 5V 引脚来连接红线，例如引脚二。

![Illustration of Raspberry Pi headers](https://www.raspberrypi.com/documentation/accessories/images/pi_plugs.png)

树莓派标头的位置

接下来，将黑线的另一端连接到显示器上的 GND 引脚，将红线的另一端连接到显示器上的 5V 引脚。完成所有连接后，下次打开树莓派时，您应该会看到触摸显示屏被点亮。

使用触摸显示屏上的另外三个引脚将显示器连接到早期树莓派 1 Model A 或 B。有关更多信息，请参考我们关于旧版支持的文档。

>**注意**
>
> 要识别早期的树莓派，请检查 GPIO 头连接器。只有早期型号有 26 个引脚的 GPIO 头连接器；后续型号都有 40 个引脚。 

#### 用 Mirco USB 电源适配器供电

如果您不想用树莓派为触摸显示屏供电，可用 Mirco USB 电源适配器。我们建议使用树莓派 12.5W 电源适配器，以确保显示屏正常运行。

如果选择使用 Mirco USB 供电，请不要把树莓派的 GPIO 引脚连接到显示器上。两个板之间唯一的连接应该是扁平柔性电缆。


>**警告**
>
>若使用 micro USB 线为显示器供电，并将其安装在机箱内，在使用时会无法触及显示器的 PCB 板。

### 使用屏幕键盘

在 Raspberry Pi OS Bookworm 及更高版本中，您可以将 wvkbd 屏幕键盘用作输入设备。要安装 wvkbd ，请运行以下命令：

```
$ sudo apt install wvkbd
```

>**技巧**
>
>在旧版 Raspberry Pi OS 发行版中，您可以使用 `matchbox-keyboard` 来代替。 

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

>**注意**
>
>使用 cmdline.txt 无法单独旋转 DSI 显示器，与 HDMI 显示器分开。当同时使用 DSI 和 HDMI 时，它们共享相同的旋转值。

#### 旋转触摸输入

>**警告**
>
>通过设备树旋转触摸输入可能会与您的输入库发生冲突。请尽可能在您的输入库或桌面中配置触摸事件旋转。



触摸输入的旋转与显示本身的方向无关。要更改此设置，您需要在 /boot/firmware/config.txt 中手动添加 dtoverlay 指令。在 config.txt 中添加以下行：

```
dtoverlay=vc4-kms-dsi-7inch,invx,invy
```

然后，在 config.txt 中删除以下行（如果有）来禁用自动显示检测：

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

>**警告**
>
>这些说明仅适用于最老的树莓派、Model A 和 B 版本的主卡。要识别最老的树莓派，请检查 GPIO 头连接器。只有原始型号有一个 26 引脚的 GPIO 头连接器；后续型号有 40 个引脚。


树莓派 1 Model A 和 B 版本上的 DSI 连接器没有与触摸屏控制器和 DSI 控制器通信所需的 I2C 连接。为了解决这个问题，请使用显示套件附带的额外一组跳线。将 GPIO 头上的 SCL/SDA 连接到显示板上标有 SCL/SDA 的水平引脚。使用跳线电缆通过 GPIO 引脚为 Model A/B 供电。

这些主板上默认禁用了 DSI 显示自动检测。要启用检测，请在 /boot/firmware/config.txt 文件中添加以下行：

```
ignore_lcd=0
```

请用 Mirco USB 电源适配器连接到显示屏上的 PWR IN 来供电。不要通过树莓派的 Mirco USB 为设备供电。这将超过流过保险丝的最大电流额定值，因为显示屏的消耗大约为 400mA。
