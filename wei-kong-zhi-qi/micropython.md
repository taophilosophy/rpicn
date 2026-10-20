# MicroPython

## 什么是 MicroPython？

MicroPython 是 Python 3 编程语言的完整实现，可直接运行在树莓派 Pico 等嵌入式硬件上。你可以通过 USB 串口获得交互式提示符（REPL），立即执行命令，还拥有一个内置文件系统。Pico 版 MicroPython 包含用于访问底层芯片特定硬件的模块。

* [MicroPython Wiki](https://github.com/micropython/micropython/wiki)
* [MicroPython Discussions](https://github.com/orgs/micropython/discussions/)
* [MicroPython Discord](https://discord.com/invite/RB8HZSAExQ)

## 拖放安装 MicroPython

你可以将 Pico 通过 USB 连接到计算机，然后拖放文件来编程，因此我们提供了一个可下载的 UF2 文件，让你能更轻松地安装 MicroPython。

![MicroPython 安装演示](.gitbook/assets/MicroPython.webm)

下载适合你板子的 MicroPython UF2 文件：

* [Pico](https://micropython.org/download/rp2-pico/rp2-pico-latest.uf2)

* [Pico W](https://micropython.org/download/rp2-pico-w/rp2-pico-w-latest.uf2)

* [Pico 2](https://micropython.org/download/RPI_PICO2/RPI_PICO2-latest.uf2)

* [Pico 2 W](https://micropython.org/download/RPI_PICO2_W/RPI_PICO2_W-latest.uf2)

有关在树莓派 Pico W 系列设备上通过 C/C++ 或 MicroPython 使用 Wi-Fi 和蓝牙的更多信息，请参阅《[Wi-Fi and Bluetooth connectivity on Pico W-series devices](https://pip.raspberrypi.com/documents/RP-008257-DS)》。

有关[支持的蓝牙协议和配置文件](https://github.com/bluekitchen/btstack#supported-protocols-and-profiles)的更多信息，请参阅 Blue Kitchen 的 [BTStack](https://github.com/bluekitchen/btstack) GitHub 仓库。

>**注意**
>
> 其他基于 RP2040 和 RP2350 的板子的 MicroPython 发行版可在 [MicroPython 下载页面](https://micropython.org/download/)找到。

要给设备编程，请按以下步骤操作：

1. 在将 Pico 通过 USB 电缆连接到计算机时按住 BOOTSEL 按钮。当你的 Pico 以名为 “RPI-RP2”（Pico）或 “RP2350”（Pico 2）的大容量存储设备出现时，松开 BOOTSEL 按钮。
2. 将 MicroPython UF2 文件拖放到挂载的卷上。你的 Pico 会重启，现在运行的就是 MicroPython。
3. 通过 USB 串口访问 REPL。

《[树莓派 Pico 系列 Python SDK](https://pip.raspberrypi.com/documents/RP-008355-DS)》一书包含逐步说明，指导你如何连接 Pico，并使用命令行和 [Thonny](https://thonny.org/) IDE 以 MicroPython 编程。

## 我可以在哪里找到文档？

你可以在以下位置找到有关 MicroPython 移植到树莓派微控制器的信息：

- [树莓派 Pico Python SDK](https://pip.raspberrypi.com/documents/RP-008355-DS)

- [Wi-Fi and Bluetooth connectivity on Pico W-series devices](https://pip.raspberrypi.com/documents/RP-008257-DS)

- [RP2 Quick Reference](https://docs.micropython.org/en/latest/rp2/quickref.html)

- [RP2 Library](https://docs.micropython.org/en/latest/library/rp2.html)

- [pico-micropython-examples 仓库](https://github.com/raspberrypi/pico-micropython-examples)

## 我正在用的硬件是哪个？

对于用 MicroPython 编写的软件来说，没有直接的方法可以通过查看硬件来判断自己运行在树莓派 Pico 还是 Pico W 上。不过，你可以间接判断：看看你所用的 MicroPython 固件中是否包含网络功能：

```python
import network
if hasattr(network, "WLAN"):
   # 该板子具备 WLAN 功能
```

另外，你也可以使用 `sys` 模块检查 MicroPython 固件版本，以确认它是为树莓派 Pico 还是为 Pico W 编译的：

```python
>>> import sys
>>> sys.implementation
(name='micropython', version=(1, 19, 1), _machine='Raspberry Pi Pico W with RP2040', _mpy=4102)
```

如果 `sys.implementation._machine` 中存在 'Pico W' 字符串，那么你的固件就是为 Pico W 编译的。
