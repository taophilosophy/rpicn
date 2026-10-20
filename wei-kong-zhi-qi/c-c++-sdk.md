# C/C++ SDK

## 设置 SDK

要开始使用 C/C++ SDK，请阅读我们的[入门文档](https://pip.raspberrypi.com/documents/RP-008276-DS)，其中介绍了如何为 VS Code 安装[树莓派 Pico 扩展](https://pip.raspberrypi.com/documents/RP-008276-DS)，并创建一个简单的项目。支持的操作系统可在[扩展的 readme](https://github.com/raspberrypi/pico-vscode#requirements-by-os)中找到。

不过，如果你打算在 [32 位树莓派系统或精简版树莓派系统](../shu-mei-pai/raspberry-pi-os.md)上开发 Pico，我们的 VS Code 扩展并不支持这些操作系统。你可以改为在命令行中运行我们的设置脚本，快速完成 C/C++ 工具链的安装。

1. 在运行设置脚本之前，先确保你树莓派上的树莓派系统[更新到最新版本](../shu-mei-pai/raspberry-pi-os.md#更新软件)。
2. 运行以下命令，下载并执行设置脚本：

```bash
wget https://raw.githubusercontent.com/raspberrypi/pico-setup/master/pico_setup.sh
chmod +x pico_setup.sh
./pico_setup.sh
```

3. 有关更多信息以及测试安装的说明，请参阅 pico-setup 的 [README](https://github.com/raspberrypi/pico-setup)。

## 树莓派 Pico C/C++ SDK

我们的官方 C SDK 可以在命令行中使用，也可以在 Visual Studio Code 和 CLion 等流行的集成开发环境中使用。要开始使用，请下载我们的 C/C++ SDK 和示例，并查看我们的[入门文档](https://pip.raspberrypi.com/documents/RP-008276-DS)。或者，想快速完成安装可参见下一节。

你可以在以下位置找到有关 C/C++ SDK 的文档：

- [树莓派 Pico C/C++ SDK API 文档](https://www.raspberrypi.com/documentation/pico-sdk/index_doxygen.html)

- [Getting started with Raspberry Pi Pico-series](https://pip.raspberrypi.com/documents/RP-008276-DS)

- [Wi-Fi and Bluetooth connectivity on Pico W-series devices](https://pip.raspberrypi.com/documents/RP-008257-DS)

- [Raspberry Pi Pico-series C/C++ SDK](https://pip.raspberrypi.com/documents/RP-009085-KB)

- [pico-examples 仓库](https://github.com/raspberrypi/pico-examples)

SDK 源代码是开源的，可在 [pico-sdk GitHub 仓库](https://github.com/raspberrypi/pico-sdk)中获取。

>**注意**
>
> 如果要使用 C/C++ SDK 为树莓派 Pico 以外的板子构建应用程序，请向 CMake 传递 `-DPICO_BOARD=boardname`，其中 `boardname` 是你的板子名称。例如：
>
> * 要为 Adafruit Feather RP2040 构建应用程序，请传递 `-DPICO_BOARD=adafruit_feather_rp2040`。
> * 要为 Pico W 构建应用程序，请传递 `-DPICO_BOARD=pico_w`（如果要连接无线网络，还要加上 -DWIFI_SSID="Your Network" -DWIFI_PASSWORD="Your Password"）。
>
> 更多信息请参阅树莓派 Pico SDK 中的 [`boards/` 目录](https://github.com/raspberrypi/pico-sdk/tree/master/src/boards)以及[论坛](https://forums.raspberrypi.com/viewtopic.php?f=147&t=304393)。

## 第一个二进制程序

### 闪烁 LED

使用新的微控制器时，每个人写的第一个程序都是让板上的 LED 闪烁。树莓派 Pico 板上有一个单独的 LED。对于 Pico 和 Pico 2，该 LED 连接到板载微控制器的 `GP25`；对于 Pico W 和 Pico 2 W，则连接到 Infineon 43439 无线芯片的 `WL_GPIO0`。

![闪烁 LED 演示](.gitbook/assets/Blink-an-LED.webm)

你可以按以下步骤让它闪烁：

1. 下载 [Blink UF2](https://github.com/raspberrypi/pico-sdk-prebuilts/releases/latest/download/blink_universal.uf2) 文件。该文件支持所有 Pico 变体。
2. 按住 BOOTSEL 按钮，将 Pico 插入树莓派或其他计算机的 USB 端口。
3. 它会以名为 “RPI-RP2”（Pico）或 “RP2350”（Pico 2）的大容量存储设备的形式挂载。
4. 将 Blink UF2 二进制文件拖放到 RPI-RP2 卷上。Pico 会重启。

如果一切正常，板上的 LED 就会闪烁。

你可以在 [GitHub](https://github.com/raspberrypi/pico-examples/blob/master/blink/blink.c) 上查看编写自己的闪烁程序的代码。

### 打印 “Hello World”

下一个程序是通过 USB 串口连接打印 “Hello World”。

![Hello World 演示](.gitbook/assets/Hello-World.webm)

1. 下载 [“Hello World” UF2](https://github.com/raspberrypi/pico-sdk-prebuilts/releases/latest/download/hello_universal.uf2)。
2. 按住 BOOTSEL 按钮，将 Pico 插入树莓派或其他计算机的 USB 端口。
3. 它会以名为 “RPI-RP2”（Pico）或 “RP2350”（Pico 2）的大容量存储设备的形式挂载。
4. 将 “Hello World” UF2 二进制文件拖放到挂载的卷上。Pico 会重启。
5. 打开一个终端窗口并输入：

```bash
$ sudo apt install minicom
$ minicom -b 115200 -o -D /dev/ttyACM0
```

终端上会打印出 “Hello, world!”。

你可以在 [GitHub](https://github.com/raspberrypi/pico-examples/blob/master/hello_world/usb/hello_usb.c) 上查看编写自己的 hello_world 程序的代码。

## 快速启动你的项目

>**注意**
>
> 以下说明较为简略，且仅适用于 Linux。详细的步骤、其他平台的说明以及一般性内容，请参阅《[Getting started with Raspberry Pi Pico](https://pip.raspberrypi.com/documents/RP-008276-DS)》和《[Raspberry Pi Pico C/C++ SDK](https://pip.raspberrypi.com/documents/RP-009085-KB)》两本书。

安装 CMake（版本不低于 3.13）和 GCC 交叉编译器：

```bash
$ sudo apt install cmake gcc-arm-none-eabi libnewlib-arm-none-eabi libstdc++-arm-none-eabi-newlib
```

将 SDK 克隆到本地，把你的项目设置为使用树莓派 Pico SDK：

```bash
$ git clone https://github.com/raspberrypi/pico-sdk.git
```

从 SDK 中把 `external/pico_sdk_import.cmake` 复制到你的项目目录。

在你的环境中把 `PICO_SDK_PATH` 设置为 SDK 的位置，或者在稍后把它（`-DPICO_SDK_PATH=`）传递给 `cmake`。

按如下方式编写 `CMakeLists.txt`：

```cmake
cmake_minimum_required(VERSION 3.13)

# 基于 PICO_SDK_PATH 初始化 SDK
# 注意：这必须发生在 project() 之前
include(pico_sdk_import.cmake)

project(my_project)

# 初始化树莓派 Pico SDK
pico_sdk_init()

# 你的项目的其余部分
```

接着就可以编写你的代码了；具体做法可参见 [pico-examples](https://github.com/raspberrypi/pico-examples) 或《[Raspberry Pi Pico C/C++ SDK](https://pip.raspberrypi.com/documents/RP-009085-KB)》一书。

最简单的做法可以只写一个源文件（例如 `hello_world.c`）：

```c
#include <stdio.h>
#include "pico/stdlib.h"

int main() {
    setup_default_uart();
    printf("Hello, world!\n");
    return 0;
}
```

并将以下内容添加到你的 CMakeLists.txt：

```cmake
add_executable(hello_world
    hello_world.c
)

# 添加 pico_stdlib 库，它聚合了常用的功能
target_link_libraries(hello_world pico_stdlib)

# 除 ELF 外，还创建 map/bin/hex/uf2 文件。
pico_add_extra_outputs(hello_world)
```

>**注意**
>
> 此示例使用默认 UART 作为 stdout；如果你想使用默认 USB，请参见 hello-usb 示例。

建立 CMake 构建目录。例如，如果不使用 IDE：

```bash
$ mkdir build
$ cd build
$ cmake ..
```

在为树莓派 Pico 以外的板子构建时，请在上面的 cmake 命令中传递 `-DPICO_BOARD=board_name`，例如 `cmake -DPICO_BOARD=pico_w ..`，以便为该特定板子配置相应的 SDK 和构建选项。

这样做会设置各种编译器定义（例如 UART 和其他硬件的默认引脚号），并且在某些情况下还会启用额外库的使用（例如在为 `PICO_BOARD=pico_w` 构建时启用无线支持）；如果没有提供相应功能的板子，这些库是无法构建的。

要查看 SDK 自身定义的板子列表，请查看[这个目录](https://github.com/raspberrypi/pico-sdk/blob/master/src/boards/include/boards)，其中每个命名的板子都有一个头文件。

从你创建的构建目录构建你的目标：

```bash
$ make hello_world
```

现在你就有了 `hello_world.elf`，可以使用调试器加载；或者有了 `hello_world.uf2`，可以通过拖放安装并在树莓派 Pico 上运行。
