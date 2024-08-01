# MicroPython

## 什么是 MicroPython？


MicroPython 是编程语言 Python 3 的完整实现，直接运行在嵌入式硬件（如树莓派 Pico）上。你可以用 USB 串口获得交互提示（REPL），立即执行命令，并且内置了文件系统。Pico 版的 MicroPython 包含了用于访问底层芯片特定硬件的模块。

* [MicroPython Wiki](https://github.com/micropython/micropython/wiki)
* [MicroPython 论坛 ](https://forum.micropython.org/)

## 拖放安装 MicroPython

你可以通过将 Pico 通过 USB 连接到计算机，然后将文件拖放到其上来编程，因此我们提供了可下载的 UF2 文件，以便更轻松地安装 MicroPython。

![MicroPython 640x360 v2](https://www.raspberrypi.com/documentation/microcontrollers/images/MicroPython-640x360-v2.gif)

下载适合你板子的正确 MicroPython UF2 文件：

* [树莓派 Pico](https://micropython.org/download/rp2-pico/rp2-pico-latest.uf2)
* 带有 Wi-Fi 和蓝牙 LE 功能的[树莓派 Pico W](https://micropython.org/download/rp2-pico-w/rp2-pico-w-latest.uf2)

要在树莓派 Pico W 上使用 Wi-Fi 和蓝牙，可以使用 C/C++ 或 MicroPython，参见 [Connecting to the Internet with 树莓派 Pico W](https://datasheets.raspberrypi.com/picow/connecting-to-the-internet-with-pico-w.pdf)。有关支持的蓝牙协议和配置文件的详细信息，请查看 Blue Kitchen 的 [BTStack](https://github.com/bluekitchen/btstack) GitHub 仓库。

>**注意**
>
>其他基于 RP2040 的板子的 MicroPython 发行版可在 [MicroPython 下载页面 ](https://micropython.org/download/) 上找到。 

要编程你的设备，请按照以下步骤操作：

1. 在连接 Pico 到计算机的 USB 电缆时，按住 BOOTSEL 按钮。当你的 Pico 显示成 RPI-RP2 的大容量存储设备时，请释放 BOOTSEL 按钮。
2. 将 MicroPython UF2 文件拖放到 RPI-RP2 卷上。你的 Pico 将重启。MicroPython 将自动运行。
3. 通过 USB 串口访问 REPL。

[树莓派 Pico Python SDK](https://datasheets.raspberrypi.com/pico/raspberry-pi-pico-python-sdk.pdf) 书籍提供了逐步连接你的 Pico 并使用命令行和 [Thonny](https://thonny.org/) IDE 编程 MicroPython 的说明。

## 我可以在哪里找到文档？


你可以在以下位置找到有关 MicroPython 到 RP2040 的端口的信息：

[树莓派 Pico Python SDK](https://datasheets.raspberrypi.com/pico/raspberry-pi-pico-python-sdk.pdf) - 用于 RP2040 微控制器的 MicroPython 环境

[Connecting to the Internet with 树莓派 Pico W](https://datasheets.raspberrypi.com/picow/connecting-to-the-internet-with-pico-w.pdf) - 使用 C/C++ 或 MicroPython 将树莓派 Pico W 连接到互联网

[RP2 Quick Reference](https://docs.micropython.org/en/latest/rp2/quickref.html) - 关于 MicroPython RP2040 端口的官方文档

[RP2 Library](https://docs.micropython.org/en/latest/library/rp2.html) - 关于 MicroPython 中 `rp2` 模块的官方文档

### 进一步阅读

![MicroPython 书籍 ](https://www.raspberrypi.com/documentation/microcontrollers/images/micropython_book.png?hash=0cedc967a40584b41bd815d9f3382012)

查看 *[Get Started with MicroPython on 树莓派 Pico](https://store.rpipress.cc/collections/getting-started/products/get-started-with-micropython-on-raspberry-pi-pico-2nd-edition)* 了解如何使用 MicroPython 编程语言让你的 Pico 与周围的世界互动。本书已完全更新，适用于 树莓派 Pico W 和最新版本的 MicroPython，它向你展示如何：

* 设置并开始使用你的 Pico、Pico W
* 使用 MicroPython 编写程序
* 控制和感知电子组件
* 发现如何使用 Pico 独特的可编程 IO
* 将树莓派 Pico W 转换为物联网的网络连接节点
* 将你的 Pico W 与智能手机、平板电脑或另一个 Pico W 通过蓝牙低功耗（BLE）连接起来

## 我正在用的硬件是哪个？

在 MicroPython 中，没有直接的方法可以通过查看硬件来判断是在树莓派 Pico 还是 Pico W 上运行的软件。然而，你可以间接地通过查看你的特定 MicroPython 固件中是否包含网络功能来判断：

```python
import network
if hasattr(network, "WLAN"):
   # 该主板搭载了 WLAN 功能
```

另外，你可以使用`sys`模块检查 MicroPython 固件的版本，以确定它是否为树莓派 Pico 或 Pico W 编译而成：

```python
>>> import sys
>>> sys.implementation
(name='micropython', version=(1, 19, 1), _machine='Raspberry Pi Pico W with RP2040', _mpy=4102)
```

如果`sys.implementation._machine`中包含字符串 'Pico W'，那么你的固件是为 Pico W 编译的。
