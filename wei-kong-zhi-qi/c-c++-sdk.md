# C/C++ SDK

## 设置 SDK

要全面了解如何使用 C/C++ SDK，请阅读我们的[入门指南 ](https://datasheets.raspberrypi.com/pico/getting-started-with-pico.pdf)文档。然而，如果你打算在 [树莓派 ](https://www.raspberrypi.com/documentation/computers/os.html) 上开发 Pico，可以通过命令行快速设置 C/C++ 工具链，只需运行我们的 [设置脚本 ](https://raw.githubusercontent.com/raspberrypi/pico-setup/master/pico_setup.sh)。

| 注意 | 在运行设置脚本之前，请确保你的树莓派操作系统已经 [更新到最新版本 ](https://www.raspberrypi.com/documentation/computers/os.html#update-software)。 |
| ------ | --------------------------------------------------------------------------------------- |

## 树莓派 Pico C/C++ SDK

我们的官方 C SDK 可以从命令行使用，也可以与 Visual Studio Code、Eclipse 和 CLion 等流行的集成开发环境一起使用。要开始，请下载我们的 C/C++ SDK 和示例，并查看我们的 '[入门指南 ](https://datasheets.raspberrypi.com/pico/getting-started-with-pico.pdf)'。或者，可以查看下一节进行快速设置。

* SDK [Github 仓库 ](https://github.com/raspberrypi/pico-sdk)
* 示例 [Github 仓库 ](https://github.com/raspberrypi/pico-examples)

你可以在以下位置找到有关 C/C++ SDK 的文档：

[使用 Raspberry Pi Pico 入门 ](https://datasheets.raspberrypi.com/pico/getting-started-with-pico.pdf) 与基于 RP2040 的微控制器板的 C/C++ 开发

[使用 Raspberry Pi Pico W 连接互联网 ](https://datasheets.raspberrypi.com/picow/connecting-to-the-internet-with-pico-w.pdf) 使用 C/C++ 或 MicroPython 将 Raspberry Pi Pico W 连接到互联网

[Raspberry Pi Pico C/C++ SDK](https://datasheets.raspberrypi.com/pico/raspberry-pi-pico-c-sdk.pdf) 用于 RP2040 微控制器的库和工具的 C/C++ 开发

[API 级文档 ](https://www.raspberrypi.com/documentation/pico-sdk/index_doxygen.html) Raspberry Pi Pico C/C++ SDK 的文档

| 注意 | 如果你正在使用 C/C++ SDK 构建应用程序，并且目标板不仅限于 Raspberry Pi Pico，你需要在 CMake 中传递 `-DPICO_BOARD=boardname`。这里的 `boardname` 是你的开发板名称，例如，对于 Adafruit Feather RP2040，你应该传递 `-DPICO_BOARD=adafruit_feather_rp2040`。更多信息请参考 Raspberry Pi Pico SDK 中的 [`boards/`](https://github.com/raspberrypi/pico-sdk/tree/master/src/boards) 目录和 [论坛 ](https://forums.raspberrypi.com/viewtopic.php?f=147&t=304393)。 |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

| 注意 | 关于在 Raspberry Pi Pico W 上使用 C/C++ SDK 构建应用程序并连接到网络，你需要在 CMake 中传递 `-DPICO_BOARD=pico_w -DWIFI_SSID="你的网络" -DWIFI_PASSWORD="你的密码"`。如果只需启用蓝牙支持，则无需传递 SSID 和密码，但仍需传递 `-DPICO_BOARD=pico_w` 字符串至 CMake。 |
| ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## 第一个二进制程序

### 闪烁 LED

当使用新的微控制器时，第一个程序通常是控制板上的 LED 闪烁。树莓派 Pico 板上有一个单独的 LED，连接到板上的 `GP25`（用于 Raspberry Pi RP2040 for Pico），以及 `WL_GPIO0`（用于 Pico W 上的 Infineon 43439 无线芯片）。

![Blink an LED 640x360 v2](https://www.raspberrypi.com/documentation/microcontrollers/images/Blink-an-LED-640x360-v2.gif)

你可以按照以下步骤进行 LED 的闪烁：

1. 下载适用于 [Raspberry Pi Pico](https://datasheets.raspberrypi.com/soft/blink.uf2) 或 [Pico W](https://datasheets.raspberrypi.com/soft/blink_picow.uf2) 的 Blink UF2。
2. 按住 BOOTSEL 按钮，将 Pico 插入树莓派或其他计算机的 USB 端口。
3. 它将作为名为 RPI-RP2 的大容量存储设备挂载。
4. 将 Blink UF2 二进制文件拖放到 RPI-RP2 卷上。Pico 将重新启动。

你应该看到板上的 LED 闪烁。

你可以在 Github 上查看 [Raspberry Pi Pico](https://github.com/raspberrypi/pico-examples/blob/master/blink/blink.c) 和 [Pico W](https://github.com/raspberrypi/pico-examples/blob/master/pico_w/wifi/blink/picow_blink.c) 版本的代码。

### 打印 "Hello World"

下一个程序是通过 USB 串行连接打印 'Hello World'。

![Hello World 640x360 v2](https://www.raspberrypi.com/documentation/microcontrollers/images/Hello-World-640x360-v2.gif)

1. 下载 [&apos;Hello World&apos; UF2](https://datasheets.raspberrypi.com/soft/hello_world.uf2)。
2. 按住 BOOTSEL 按钮，将 Pico 插入树莓派或其他计算机的 USB 端口。
3. 它将作为名为 RPI-RP2 的大容量存储设备挂载。
4. 将 'Hello World' UF2 二进制文件拖放到 RPI-RP2 卷上。Pico 将重新启动。
5. 打开终端窗口并键入：

    ```
    $ sudo apt install minicom
    $ minicom -b 115200 -o -D /dev/ttyACM0
    ```

你应该在终端看到 'Hello, world!' 的输出。

你可以在 Github 上查看 [代码 ](https://github.com/raspberrypi/pico-examples/blob/master/hello_world/usb/hello_usb.c)。

## 快速启动你的项目

| 注意 | 以下说明简洁，并且仅适用于基于 Linux 的系统。有关详细步骤、其他平台的说明以及一般建议，请参阅 [Getting started with Raspberry Pi Pico](https://datasheets.raspberrypi.com/pico/getting-started-with-pico.pdf) 和 [Raspberry Pi Pico C/C++ SDK](https://datasheets.raspberrypi.com/pico/raspberry-pi-pico-c-sdk.pdf) 书籍。 |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |


安装 CMake（至少版本 3.13）和 GCC 交叉编译器

```
$ sudo apt install cmake gcc-arm-none-eabi libnewlib-arm-none-eabi libstdc++-arm-none-eabi-newlib
```

设置项目以使用树莓派 Pico SDK，通过将 SDK 克隆到本地：

```
$ git clone https://github.com/raspberrypi/pico-sdk.git
```

从 SDK 中将 `external/pico_sdk_import.cmake` 复制到您的项目目录中

在您的环境中设置 `PICO_SDK_PATH` 为 SDK 的路径，或者稍后通过 `-DPICO_SDK_PATH=` 选项传递给 `cmake`。

设置一个 `CMakeLists.txt` 如下：

```
cmake_minimum_required(VERSION 3.13)

# 基于 PICO_SDK_PATH 初始化 SDK
# 注意：这必须在 project() 之前发生
include(pico_sdk_import.cmake)

project(my_project)

# 初始化树莓派 Pico SDK
pico_sdk_init()

# 您的项目的其余部分
```

接着编写您的代码，参见 [pico-examples](https://github.com/raspberrypi/pico-examples) 或 [Raspberry Pi Pico C/C++ SDK](https://datasheets.raspberrypi.com/pico/raspberry-pi-pico-c-sdk.pdf) 书籍获取更多信息。

最简单的例子可以是一个单一源文件（例如 `hello_world.c`）：

```
#include <stdio.h>
#include "pico/stdlib.h"

int main() {
    setup_default_uart();
    printf("Hello, world!\n");
    return 0;
}
```

并将以下内容添加到您的 CMakeLists.txt 中：

```
add_executable(hello_world
    hello_world.c
)

# 添加 pico_stdlib 库，它聚合了常用功能
target_link_libraries(hello_world pico_stdlib)

# 除 ELF 外还创建 map/bin/hex/uf2 文件。
pico_add_extra_outputs(hello_world)
```

| 注意 | 此示例使用默认的 UART 作为 stdout；如果要使用默认的 USB，请参见 hello-usb 示例。 |
| ------ | -------------------------------------------------------------------------------------------------------------- |

设置一个 CMake 构建目录。例如，如果不使用 IDE：

```
$ mkdir build
$ cd build
$ cmake ..
```

当为树莓派 Pico 以外的板子构建时，您应该将 `-DPICO_BOARD=board_name` 传递给上述 cmake 命令，例如 `cmake -DPICO_BOARD=pico_w ..`，以相应地配置 SDK 和构建选项。

这样做会设置各种编译器定义（例如 UART 和其他硬件的默认引脚号），在某些情况下还会启用其他库的使用（例如在构建 `PICO_BOARD=pico_w` 时启用无线支持），这些库在没有提供所需功能的板子上无法构建。

有关 SDK 自身定义的板子列表，请查看 [此目录](https://github.com/raspberrypi/pico-sdk/blob/master/src/boards/include/boards) 中每个命名板子的头文件。

从您创建的构建目录中制作您的目标。

```
$ make hello_world
```

现在您有了 `hello_world.elf`，可以通过调试器加载，或者有了 `hello_world.uf2`，可以通过拖放安装并在树莓派 Pico 上运行。
