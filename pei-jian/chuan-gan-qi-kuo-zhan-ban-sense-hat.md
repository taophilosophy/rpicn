# 传感器扩展板（Sense HAT）

## 传感器扩展板（Sense HAT）简介

[树莓派传感器扩展板（Sense HAT）](https://www.raspberrypi.com/products/sense-hat/)可为你的树莓派提供一系列传感功能。板载传感器可让你监测压力、湿度、温度、颜色、方向和运动。8×8 RGB LED 矩阵可让你将传感器数据可视化，五按钮摇杆可供用户与你的项目交互。

![树莓派传感器扩展板（Sense HAT）](.gitbook/assets/Sense-HAT.jpg)

Sense HAT 最初是为国际空间站开发的，属于[树莓派基金会](https://raspberrypi.org/)与[欧洲航天局](https://www.esa.int/)合作开展的 [Astro Pi](https://astro-pi.org/) 教育计划的一部分。你可以借助它完成任何需要位置、运动、方向或环境传感的项目。

官方支持的 [Python 库](#使用-python-与传感器扩展板)可让你访问所有板载传感器、LED 矩阵和摇杆。传感器扩展板兼容所有带有 40 针 GPIO 排针的树莓派设备。

## 特性

传感器扩展板配备 8×8 RGB LED 矩阵和五按钮摇杆，并包含以下传感器：

* 陀螺仪
* 加速度计
* 磁力计
* 温度
* 气压
* 湿度
* 颜色和亮度

Sense HAT 和 Sense HAT V2 的原理图和机械图可在[产品信息门户](https://pip.raspberrypi.com/categories/676-raspberry-pi-sense-hat)下载。

### LED 矩阵

LED 矩阵是一个 ID 为 `RPi-Sense FB` 的 RGB565 [帧缓冲区](https://www.kernel.org/doc/Documentation/fb/framebuffer.txt)。你可以把对应的设备节点当作普通文件写入，也可以用 mmap 映射。附带的 `snake` 示例展示了如何访问帧缓冲区。

### 摇杆

摇杆会作为一个名为 `Raspberry Pi Sense HAT Joystick` 的输入事件设备出现，映射到方向键和**回车键**。任何能够处理输入的库都支持它，你也可以直接通过 [evdev 接口](https://www.kernel.org/doc/Documentation/input/input.txt)访问它。适用的库包括 [SDL](https://www.libsdl.org/)、[pygame](https://www.pygame.org/docs/) 和 [python-evdev](https://python-evdev.readthedocs.org/en/latest/)。附带的 `snake` 示例展示了如何直接访问摇杆。

## 安装

为了让传感器扩展板正确工作，需要满足以下条件：

* 最新的内核
* 在你的树莓派上启用 [I²C](https://en.wikipedia.org/wiki/I%C2%B2C)
* 若干依赖项

请完成以下步骤，使树莓派设备准备好连接传感器扩展板：

首先，确保树莓派运行的是最新的软件。运行以下命令进行更新：

```bash
$ sudo apt update && sudo apt full-upgrade
```

接下来，安装 `sense-hat` 软件包，这将确保内核是最新的，启用 I²C，并安装必要的依赖项：

```bash
$ sudo apt install sense-hat
```

最后，重启树莓派以启用 I²C 并加载新内核（如果内核有变化的话）：

```bash
$ sudo reboot
```

## 校准

安装必要的软件，并按照以下步骤运行校准程序：

```bash
$ sudo apt update
$ sudo apt install octave -y
$ cd
$ cp /usr/share/librtimulib-utils/RTEllipsoidFit ./ -a
$ cd RTEllipsoidFit
$ RTIMULibCal
```

校准程序会显示以下菜单：

```
Options are:

  m - calibrate magnetometer with min/max
  e - calibrate magnetometer with ellipsoid (do min/max first)
  a - calibrate accelerometers
  x - exit

Enter option:
```

按小写字母 `m`。随后会显示以下消息，按任意键开始。

```
Magnetometer min/max calibration
-------------------------------
Waggle the IMU chip around, ensuring that all six axes
(+x, -x, +y, -y and +z, -z) go through their extrema.
When all extrema have been achieved, enter 's' to save, 'r' to reset
or 'x' to abort and discard the data.

Press any key to start...
```

启动后，屏幕上会滚动显示类似以下的输出：

```
Min x:  51.60  min y:  69.39  min z:  65.91
Max x:  53.15  max y:  70.97  max z:  67.97
```

请留意屏幕最底部的两行，它们是程序最近输出的测量结果。

现在，拿起树莓派和传感器扩展板，以你能想到的所有可能方式移动它。拔掉所有非必要的电缆以避免杂乱，会更有帮助。

尝试在俯仰、横滚和偏航三个轴上各转出完整的一圈。操作时请注意不要意外弹出存储卡。花几分钟移动传感器扩展板，当你发现数字不再变化时停止。

现在按小写字母 `s`，再按小写字母 `x` 退出程序。如果现在运行 `ls` 命令，你会看到新生成了一个 `RTIMULib.ini` 文件。

除上述步骤外，你也可以按同样流程操作，只是把 `m` 换成 `e`，即可进行椭球拟合。

当你完成后，将生成的 `RTIMULib.ini` 复制到 `/etc/`，并删除 `~/.config/sense_hat/` 中的本地副本：

```bash
$ rm ~/.config/sense_hat/RTIMULib.ini
$ sudo cp RTIMULib.ini /etc
```

## 入门指南

安装后，可在 `/usr/src/sense-hat/examples` 下找到示例代码。

### 使用 Python 与传感器扩展板

`sense-hat` 是传感器扩展板官方支持的库，可访问所有板载传感器和 LED 矩阵。

该库的完整文档可在 [sense-hat.readthedocs.io](https://sense-hat.readthedocs.io/en/latest/) 找到。

### 使用 C++ 与传感器扩展板

[RTIMULib](https://github.com/RPi-Distro/RTIMULib) 是一个 C++ 和 Python 库，可使嵌入式 Linux 系统使用 9 轴和 10 轴 IMU 变得更加容易。`/etc/RTIMULib.ini` 中提供了一个预校准的设置文件，`sense-hat` 也会复制并使用该文件。附带的示例会在当前工作目录中查找 `RTIMULib.ini`，因此你可能希望先把该文件复制到当前工作目录，以获得更准确的数据。

RTIMULibDrive11 示例预编译好了，可帮助你确认一切是否按预期工作。运行 `RTIMULibDrive11` 即可启动，按 `Ctrl C` 可关闭。

>**注意**
>
> 可以在相应的目录中运行 `make` 来编译 C/C++ 示例。

## 故障排除

### 读取和写入 EEPROM 数据

这些步骤仅供调试之用。

>**注意**
>
> 在树莓派 2 Model B Rev 1.0 和树莓派 3 Model B 上，这些步骤可能无法正常工作。固件将接管 I2C0，致使 ID 引脚被配置为输入。

在对传感器扩展板进行 EEPROM 数据读写之前，你必须完成以下步骤：

通过向 [`/boot/firmware/config.txt`](../shu-mei-pai/config.txt.md) 文件添加以下行来启用 I2C0 和 I2C1：

```ini
dtparam=i2c_vc=on
dtparam=i2c_arm=on
```

运行以下命令以重启：

```bash
$ sudo reboot
```

下载并构建闪存工具：

```bash
$ git clone https://github.com/raspberrypi/hats.git
$ cd hats/eepromutils
$ make
```

#### 读取

要读取 EEPROM 数据，请运行以下命令：

```bash
$ sudo ./eepflash.sh -f=sense_read.eep -t=24c32 -r
```

#### 写入

>**注意**
>
> 此操作不会损坏你的树莓派或传感器扩展板，但如果发生错误，你的树莓派可能无法自动检测到该扩展板。

首先，下载 EEPROM 设置并构建 `.eep` 二进制文件：

```bash
$ wget https://github.com/raspberrypi/rpi-sense/raw/master/eeprom/eeprom_settings.txt -O sense_eeprom.txt
$ ./eepmake sense_eeprom.txt sense.eep /boot/firmware/overlays/rpi-sense-overlay.dtb
```

接下来，禁用写保护：

```bash
$ i2cset -y -f 1 0x46 0xf3 1
```

写入 EEPROM 数据：

```bash
$ sudo ./eepflash.sh -f=sense.eep -t=24c32 -w
```

最后，重新启用写保护：

```bash
$ i2cset -y -f 1 0x46 0xf3 0
```
