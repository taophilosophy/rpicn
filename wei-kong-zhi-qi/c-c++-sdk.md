# C/C++ SDK

## 配置 SDK 

对于如何开始使用 C/C++ SDK 的完整演示，请阅读我们的“入门”文档。但是，如果您打算在树莓派上开发 Pico，那么您可以通过从命令行运行我们的设置脚本来快速配置 C/C++ 工具链。

>**注意**
>
>在运行配置脚本之前，请确保您树莓派上的操作系统是最新的。

## 树莓派 Pico C/C++ SDK

我们官方的 C SDK 既可以在命令行使用，也可以在流行的集成开发环境如 Visual Studio Code、Eclipse 和 CLion 中使用。要开始，请下载我们的 C/C++ SDK 和示例，并查看我们的“入门”文档以开始。如果要快速配置，请参阅下一节。

* SDK Github 仓库
* 示例 Github 存储库

您可以在这里找到关于 C/C++ SDK 的文档;

使用树莓派 Pico 和其他基于 RP2040 的微控制器板开始进行树莓派 Pico C/C++ 开发

使用树莓派 Pico W 连接互联网使用 C/C++ 或 MicroPython 在线获取树莓派 Pico W

树莓派 Pico C/C++ SDK 适用于 RP2040 微控制器的 C/C++ 开发库和工具

API 级文档树莓派 Pico C/C++ SDK 的文档

>**注意**
>
>如果您正在使用 C/C++ SDK 构建应用程序，并且目标开发板不是树莓派 Pico，则需要将 -DPICO_BOARD=boardname 传递给 CMake。这里 boardname 是您的主板名称，例如，假设是 Adafruit Feather RP2040，您应该传参 -DPICO_BOARD=adafruit_feather_rp2040 。有关更多信息，请参阅树莓派 Pico SDK 中的 boards/ 目录和论坛。 

>**注意**
>
>在《连接到树莓派 Pico W 互联网》书中介绍了如何使用 C/C++ 或 MicroPython 在树莓派 Pico W 上使用 Wi-Fi 和蓝牙的文档。 

>**注意**
>
>如果您正在使用 C/C++ SDK 为树莓派 Pico W 构建应用程序，并且要连接到网络，则需要把 -DPICO_BOARD=pico_w -DWIFI_SSID="WIFI 名" -DWIFI_PASSWORD="WIFI 密码" 传参给 CMake。如果只需要启用蓝牙支持，则无需传参 SSID 和密码，但仍需要将 -DPICO_BOARD=pico_w 字符串传参给 CMake。

## 您的第一个二进制文件

>**警告**
>
>如果您使用的是 Apple Mac，并且运行着 macOS Ventura，则由于 Finder 的工作方式发生了变化，导致拖放操作失败。请查看我们的博客文章以获取完整解释及解决方法，以及我们的 Github 问题跟踪的实时状态。 

### 点亮 LED

当使用新的微控制器时，大部分人编写的第一个程序是让 LED 灯闪烁。 树莓派 Pico 配备了一个单独的 LED。 该 LED 连接到了该板的树莓派 RP2040 的 GP25 ，以及 Pico W 的 Infineon 43439 无线芯片的 WL_GPIO0 。

![Blink an LED 640x360 v2](https://www.raspberrypi.com/documentation/microcontrollers/images/Blink-an-LED-640x360-v2.gif)

您可以通过以下方式让其闪烁。

1. 下载适用于树莓派 Pico 或 Pico W 的 Blink UF2。
2. 按住 BOOTSEL 按钮并将您的 Pico 插入树莓派或其他计算机的 USB 接口。
3. 它将被挂载成一个名为 RPI-RP2 的大容量存储设备。
4. 将 Blink UF2 二进制文件拖放到 RPI-RP2 卷上。Pico 将重启。

你应该看到了板载 LED 在闪烁。

您可以在 Github 上查看树莓派 Pico 和 Pico W 版本的代码。

### 说“Hello World”

大部分人编写的下一个程序是通过 USB 串口说“Hello World”。

![Hello World 640x360 v2](https://www.raspberrypi.com/documentation/microcontrollers/images/Hello-World-640x360-v2.gif)

1. 下载“Hello World” UF2。
2. 按住 BOOTSEL 按钮，然后将您的 Pico 插入树莓派或其他计算机的 USB 接口。
3. 它将作成名为 RPI-RP2 的大容量存储设备挂载。
4. 将“Hello World” UF2 二进制文件拖放到 RPI-RP2 卷上。Pico 将重新启动。
5. 打开一个终端窗口，然后输入：

    ```
    sudo apt install minicom
    minicom -b 115200 -o -D /dev/ttyACM0
    ```

您应该看到“Hello, world!”打印到终端。

您可以在 Github 上查看代码

## 快速启动您自己的项目

>**注意**
>
>以下说明简洁，仅基于 Linux。对于详细步骤、其他平台的说明，或者通用建议，推荐阅读书籍《树莓派 Pico 入门指南》和《树莓派 Pico C/C++ SDK》。 

安装 CMake（至少版本 3.13）和 GCC 交叉编译器

```
$ sudo apt install cmake gcc-arm-none-eabi libnewlib-arm-none-eabi libstdc++-arm-none-eabi-newlib
```

设置项目指向本地克隆的树莓派 Pico SDK，以使用 SDK：

```
$ git clone https://github.com/raspberrypi/pico-sdk.git
```

将 `external/pico_sdk_import.cmake` 从 SDK 复制到您的项目目录中

将 PICO_SDK_PATH 设置为您环境中的 SDK 位置，或稍后将其 ( -DPICO_SDK_PATH= ) 传递给 cmake

 设置类似于 CMakeLists.txt 的内容：

```
cmake_minimum_required(VERSION 3.13)

# 根据 PICO_SDK_PATH 初始化 SDK
# 注意：必须在 project() 之前进行
include(pico_sdk_import.cmake)

project(my_project)

# 初始化树莓派 Pico SDK
pico_sdk_init()

# rest of your project
```

继续编写您的代码，查看 pico-examples 或树莓派 Pico C/C++ SDK 书籍，了解更多相关信息。

最简单的方法是一个单一的源文件（例如 hello_world.c ）

```
#include <stdio.h>
#include "pico/stdlib.h"

int main() {
    setup_default_uart();
    printf("Hello, world!\n");
    return 0;
}
```

并将以下内容添加到您的 CMakeLists.txt：

```
add_executable(hello_world
    hello_world.c
)

# 添加 pico_stdlib 库，该库汇集了常用功能。
target_link_libraries(hello_world pico_stdlib)

# 除了 ELF 文件外，还创建 map/bin/hex/uf2 文件
pico_add_extra_outputs(hello_world)
```

>**注意**
>
>此示例使用默认的 UART 用于标准输出；如果要使用默认的 USB，请参阅 hello-usb 示例。


设置一个 CMake 构建目录。例如，如果不使用 IDE：

```
$ mkdir build
$ cd build
$ cmake ..
```

当为树莓派 Pico 之外的主板构建时，您应该将 -DPICO_BOARD=board_name 传递给上面的 cmake 命令，例如，cmake -DPICO_BOARD=pico_w .. 以相应地为该特定板卡配置 SDK 和构建选项。

这样做会设置各种编译器定义（例如，默认的 UART 和其他硬件的引脚编号），在某些情况下还会启用使用附加库（例如，在构建 PICO_BOARD=pico_w 时无法构建不提供必要功能的板）。

要查看 SDK 本身定义的主板列表，请查看此目录，其中为每个命名板都有一个标题。

从您创建的构建目录中制作目标。

```
$ make hello_world
```

您现在可以通过调试器加载 hello_world.elf ，或者通过拖放安装并在您的树莓派 Pico 上运行 hello_world.uf2 。
