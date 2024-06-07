# 传感器扩展板（Sense HAT）

## 传感器扩展板（Sense HAT）简介

树莓派传感器扩展板（Sense HAT）可为您的树莓派提供一系列传感功能。板载传感器可让您监测压力、湿度、温度、颜色、方向和运动。明亮的 8×8 RGB LED 矩阵可使传感器数据可视化，五个按钮的摇杆能让用户与您的项目进行交互。

![Sense HAT](https://www.raspberrypi.com/documentation/accessories/images/Sense-HAT.jpg)

传感器扩展板最初是为国际空间站开发的：作为由树莓派基金会与欧洲航天局（ESA）合作，开展的 Astro Pi 教育计划的一部分。它非常适合许多需要位置、运动、方向或环境感知的项目。传感器扩展板从连接的树莓派上取电。

由官方支持的 Python 库提供了对所有板载传感器、LED 矩阵和操纵杆的控制。传感器扩展板兼容带有 40 针 GPIO 引脚排针型号的树莓派计算机。

## 安装

为了正确工作，传感器扩展板需要最新的内核，启用 I2C，并准备一些库来继续。

确保您的 APT 软件源是最新的：

```
 sudo apt update
```

接下来，安装传感器扩展板软件包，这将确保内核是最新的，启用 I2C，并安装必要的库和程序：

```
 sudo apt install sense-hat
```

最后，如果 I2C 被禁用或在安装之前内核是旧的，则可能需要重启：

```
 sudo reboot
```

## 入门指南

安装后，可在 `/usr/src/sense-hat/examples` 下找到示例代码。

### 进一步阅读

![](https://www.raspberrypi.com/documentation/accessories/images/experiment-with-the-sense-hat.png)

您可以在由树莓派出版的《Experiment with the Sense HAT》一书中找到有关如何使用传感器扩展板的更多信息。由 Raspberry Pi 基金会的教育团队编写，这本书是由 Raspberry Pi Press 出版的 MagPi Essentials 系列的一部分。该书涵盖了 Astro Pi 项目的背景，并指导您如何使用 Python 库利用所有传感器扩展板的功能。

您可以以 PDF 格式免费下载这本书，它已根据知识共享署名-非商业性使用-相同方式共享 3.0 未本地化（CC BY NC-SA）许可发布。

### 使用 Python 与传感器扩展板

sense-hat 是传感器扩展板的官方支持库；它提供对所有板载传感器和 LED 矩阵的访问。

可在 sense-hat.readthedocs.io 找到该库的完整文档。

### 使用 C++ 与传感器扩展板

RTIMULib 是一个 C++ 和 Python 库，可使嵌入式 Linux 系统与 9 自由度和 10 自由度 IMU 的使用变得更加容易。 /etc/RTIMULib.ini 中提供了一个预校准的设置文件，也被 sense-hat 复制并使用。包含的示例在当前工作目录中查找 RTIMULib.ini ，因此您可能希望将文件复制到那里以获得更准确的数据。

RTIMULibDrive11 示例已经被预编译，以确保一切按预期工作。可以通过运行 RTIMULibDrive11 启动，并通过按 Ctrl C 停止。

>**注意**
>
>可以通过在适当的目录中运行 make 来编译 C/C++ 示例。 

## 传感器扩展板硬件

传感器扩展板配备有 8×8 RGB LED 点阵和五向按钮摇杆，并包含以下传感器：

* 陀螺仪
* 加速度计
* 磁力计
* 温度
* 气压
* 湿度
* 颜色和亮度

Sense HAT 和 Sense HAT V2 的原理图和机械图可供下载。

* Sense HAT V1 原理图。
* Sense HAT V2 原理图。
* 传感器扩展板机械图纸。

### LED 点阵

LED 点阵是一个带有 id“RPi-Sense FB”的 RGB565 帧缓冲区。适当的设备节点可以被写入为标准文件或进行 mmap 映射。包含的“snake”示例展示了如何访问帧缓冲区。

### 操纵杆

操纵杆显示为名为“Raspberry Pi Sense HAT Joystick”的输入事件设备，映射到箭头键和`回车键`。它应该受到任何能够处理输入的库的支持，或直接通过 evdev 接口。适用的库包括 SDL、pygame 和 python-evdev。包含的“snake”示例显示了如何直接访问操纵杆。

## 硬件校准

安装必要的软件并按照以下步骤运行校准程序：

```
$ sudo apt update
$ sudo apt install octave -y
$ cd
$ cp /usr/share/librtimulib-utils/RTEllipsoidFit ./ -a
$ cd RTEllipsoidFit
$ RTIMULibCal
```

然后您将看到此菜单：

```
Options are:

  m - calibrate magnetometer with min/max
  e - calibrate magnetometer with ellipsoid (do min/max first)
  a - calibrate accelerometers
  x - exit

Enter option:
```

按小写的 `m` 。然后将显示以下消息。按任意键开始。

```
    Magnetometer min/max calibration
    --------------------------------
    Waggle the IMU chip around, ensuring that all six axes
    (+x, -x, +y, -y and +z, -z) go through their extrema.
    When all extrema have been achieved, enter 's' to save, 'r' to reset
    or 'x' to abort and discard the data.

    Press any key to start...
```

启动后，您将看到屏幕上滚动的类似内容：

```
 Min x:  51.60  min y:  69.39  min z:  65.91
 Max x:  53.15  max y:  70.97  max z:  67.97
```

关注屏幕底部的两行，因为这些是程序中最近发布的测量结果。

现在，拿起树莓派和传感器扩展板，以尽可能多的方式移动它。最好拔掉所有非必要的电缆，以避免混乱。

尝试在俯仰、横滚和偏航轴上各获得一个完整的圆圈。在执行此操作时，请注意不要意外弹出 SD 卡。花几分钟移动传感器扩展板，当您发现数字不再变化时停止。

现在按小写 s 然后小写 x 退出程序。如果现在运行 ls 命令，您会看到已创建一个新的 RTIMULib.ini 文件。

除了这些步骤，您还可以通过执行上述步骤，但按 m 键而不是 e 键来执行椭球拟合。

当您完成后，将生成的 RTIMULib.ini 复制到 /etc/ 并删除 `~/.config/sense_hat/` 中的本地副本：

```
$ rm ~/.config/sense_hat/RTIMULib.ini
$ sudo cp RTIMULib.ini /etc
```

## 读取和写入 EEPROM 数据

通过向 /boot/firmware/config.txt 文件添加以下行来启用 I2C0 和 I2C1：

```
 dtparam=i2c_vc=on
 dtparam=i2c_arm=on
```

输入以下命令以重新启动：

```
 sudo systemctl reboot
```

下载并构建闪存工具：

```
$ git clone https://github.com/raspberrypi/hats.git
$ cd hats/eepromutils
$ make
```

>**注意**
>
>这些步骤可能不适用于树莓派 2 Model B Rev 1.0 和树莓派 3 Model B。固件将控制 I2C0，致使 ID 引脚被配置为输入。


### 阅读

可以使用以下命令读取 EEPROM 数据：

```
$ sudo ./eepflash.sh -f=sense_read.eep -t=24c32 -r
```

### 写入

下载 EEPROM 设置并构建 .eep 二进制文件：

```
$ wget https://github.com/raspberrypi/rpi-sense/raw/master/eeprom/eeprom_settings.txt -O sense_eeprom.txt
 ./eepmake sense_eeprom.txt sense.eep /boot/firmware/overlays/rpi-sense-overlay.dtb
```

禁用写保护：

```
$ i2cset -y -f 1 0x46 0xf3 1
```

写入 EEPROM 数据：

```
$ sudo ./eepflash.sh -f=sense.eep -t=24c32 -w
```

重新启用写保护:

```
 i2cset -y -f 1 0x46 0xf3 0
```

>**警告**
>
>此操作不会损坏您的树莓派或传感器扩展板，但如果发生错误，扩展板可能不能被自动检测到。上述步骤仅供调试目的。
