# MicroPython


## 什么是 MicroPython？

MicroPython 是 Python 3 编程语言的完整实现，可直接在嵌入式硬件上运行，如树莓派 Pico。您可以通过 USB 串口获得交互式提示符（REPL）立即执行命令，并具有内置文件系统。MicroPython 的 Pico 端口包括用于访问底层芯片特定硬件的模块。

* MicroPython 维基
* MicroPython 论坛

## 安装 MicroPython

您可以通过 USB 将 Pico 连接到计算机，然后把文件拖放到上面，我们已经准备了可下载的 UF2 文件，让您更轻松地安装 MicroPython。

![MicroPython 640x360 v2](https://www.raspberrypi.com/documentation/microcontrollers/images/MicroPython-640x360-v2.gif)

下载适用于您的主板的正确 MicroPython UF2 文件：

* [树莓派 Pico](https://micropython.org/download/rp2-pico/rp2-pico-latest.uf2)
* 带有 Wi-Fi 和蓝牙 LE 支持的树莓派 Pico W

在《连接到树莓派 Pico W 的互联网》一书中介绍了如何使用 C/C++ 或 MicroPython 在树莓派 Pico W 上使用 Wi-Fi 和蓝牙。支持的蓝牙协议和配置文件的详细信息请参阅 Blue Kitchen BTStack Github 仓库。

>**注意**
>
>可在 MicroPython 下载页面上找到其他基于 RP2040 的板载 MicroPython 发行版。


然后继续：

1. 按住 BOOTSEL 按钮，并将 Pico 插入树莓派或其他计算机的 USB 接口。在 Pico 连接后松开 BOOTSEL 按钮。
2. 它将作成名为 RPI-RP2 的大容量存储设备挂载。
3. 将 MicroPython UF2 文件拖放到 RPI-RP2 卷上。您的 Pico 将重启。MicroPython 将自动运行。
4. 您可以通过 USB 串口访问 REPL。

树莓派 Pico Python SDK 书籍包含了连接到您的 Pico 并使用命令行和 Thonny IDE 在 MicroPython 中对其进行编程的逐步说明。

>**警告**
>
>如果您使用的是 Apple Mac 并运行着 macOS Ventura，则 Finder 的工作方式发生了变化，导致拖放操作失败。此问题已在 macOS Ventura 版本 13.1 中修复。如果您无法升级到最新版本的 Ventura，请参阅我们的博客文章，了解完整的解释以及解决方法。 

## 在哪里可以找到文档？

您可以在 RP2040 上找到 MicroPython 端口的信息；

树莓派 Pico Python SDK 是为 RP2040 微控制器提供的 MicroPython 环境

使用树莓派 Pico W 连接互联网使用 C/C++ 或 MicroPython 在线获取树莓派 Pico W

RP2 快速参考 RP2040 MicroPython 端的官方文档

RP2 库关于 MicroPython 中 rp2 模块的官方文档

### 进一步阅读

Raspberry Pi Press 出版的一本由 Gareth Halfacree 和 Ben Everard 撰写的书。

在“在树莓派 Pico 上开始使用 MicroPython”中，您将学习如何使用初学者友好的语言 MicroPython 编写程序，并连接硬件，使您的树莓派 Pico 与周围世界互动。利用这些技能，您可以创建自己的电机械项目，无论是为了娱乐还是让生活更轻松。

* 设置您的树莓派 Pico 并开始使用
* 使用 MicroPython 开始编写程序
* 控制和感知电子元件
* 发现如何使用 Pico 独特的可编程 IO
* 制作反应游戏、防盗警报、温度计等等

## 我正在使用的硬件是什么？

在 MicroPython 编写的软件中，没有直接的方法可以发现它是在树莓派 Pico 还是 Pico W 上运行，通过查看硬件。但是，您可以间接地通过查看您特定的 MicroPython 固件是否包含网络功能来判断：

```
import network
if hasattr(network, "WLAN"):
   # the board has WLAN capabilities
```

或者，您可以使用 sys 模块来查看 MicroPython 的固件版本，以检查它是否为树莓派 Pico 或 Pico W 编译而成。

```
>>> import sys
>>> sys.implementation
(name='micropython', version=(1, 19, 1), _machine='Raspberry Pi Pico W with RP2040', _mpy=4102)
```

因此，如果'Pico W'字符串存在并且位于 sys.implementation._machine 中，那么可以用来确定您的固件是否为 Pico W 编译。
