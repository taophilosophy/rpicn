# 树莓派调试器（Raspberry Pi Debug Probe）

## 关于调试器

![debug probe](https://www.raspberrypi.com/documentation/microcontrollers/images/debug-probe.jpg)

树莓派调试器是一种提供了 UART 串口和标准 Arm 串行线调试（SWD）接口的 USB 设备。该调试器设计用于简单、无需焊接的即插即用调试。它具有以下功能：

* USB 到 ARM 串行线调试（SWD）接口
* USB 到 UART 桥接器
* 兼容 CMSIS-DAP 标准
* 与支持 CMSIS-DAP 的 OpenOCD 和其他工具配合使用
* 开源，易升级的固件

>**注意**
>
>有关树莓派三针调试连接器的更多信息，请参阅规格书。 

这使得在 Windows、macOS 和 Linux 等没有 GPIO 引脚头来直连 Pico 串口或 SWD 接口的设备也可轻松使用树莓派 Pico。

### 调试器

调试器在 3.3V 名义 I/O 电压下运行。

![the probe](https://www.raspberrypi.com/documentation/microcontrollers/images/the-probe.png)

调试器附带一根 USB 线和三根调试线：

* 三针 JST-SH 连接器到 3 针 JST-SH 连接器电缆
* 三针 JST-SH 连接器到 0.1 英寸排针（母）
* 三针 JST-SH 连接器到 0.1 英寸排针（公）

两根 0.1 英寸排针电缆 — 用于面包板（公头）或直接连接到带排针的板上（母头） — 颜色如下：

橙色 TX/SC（调试器输出）

 黑色 GND

YellowRX/SD（输入到调试器或 I/O）

带有三针 JST-SH 连接器的电缆旨在与较新的树莓派主板用于 SWD 调试端口和 UART 连接器的标准三针连接器一起使用。

调试器有五个 LED 灯：一个是红色 LED 电源指示灯，另外四个是状态指示灯。

![debug leds](https://www.raspberrypi.com/documentation/microcontrollers/images/debug-leds.png)

>**注意**
>
>当目标连接时，OpenOCD 会同时打开 DAP 的两个 LED，并在调用 DAP_DISCONNECT 时将它们关闭。

## 入门指南

![labelled wiring](https://www.raspberrypi.com/documentation/microcontrollers/images/labelled-wiring.jpg)

根据您的设置，有不同的方法可以将调试器连接到树莓派 Pico。在下面的示例中，我们将调试器连接到具有更新的三针 JST-SH 连接器用于 SWD 的树莓派 Pico H。

 连接以下内容：

* 将调试器“D”接口连接到 Pico H SWD JST-SH 连接器
* 将调试器“U”接口，带有三针 JST-SH 连接器连接到 0.1 英寸排针（公头）:
  * 调试器 RX 连接到 Pico H TX 引脚
  * 调试器 TX 连接到 Pico H RX 引脚
  * 调试器 GND 连接到 Pico H GND 引脚

>**注意**
>
>如果您有非 H Pico 或 Pico W（没有 JST-SH 连接器），您仍然可以将其连接到调试器。在板上的 SWCLK ， GND 和 SWDIO 引脚上焊接一个公连接器。使用随调试器附带的备用 3 引脚 JST-SH 连接器到 0.1 英寸排针（母）电缆，连接到调试器的“D”端口。分别将 Pico 或 Pico W 上的 SWCLK ， GND 和 SWDIO 连接到调试器上的 SC ， GND 和 SD 引脚。

![wiring](https://www.raspberrypi.com/documentation/microcontrollers/images/wiring.png)

## 安装工具

要使用调试器，需安装以下工具。

### 安装 OpenOCD

您需要安装 OpenOCD。

要安装 OpenOCD，请在终端中运行以下命令：

```
$ sudo apt install openocd
```

在终端中使用 openocd 命令来运行 OpenOCD。

#### 在 macOS 上安装 OpenOCD

首先，安装包管理器 Homebrew：

```
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

在 macOS 上安装 OpenOCD，请运行以下命令：

```
$ brew install openocd
```

要运行 OpenOCD，请在终端中使用 openocd 命令。

### 安装 GDB

我们还需要安装 GNU 调试器 (GDB)。

#### Linux

 安装 gdb-multiarch ：

```
$ sudo apt install gdb-multiarch
```

#### macOS

运行以下命令安装 gdb ：

```
$ brew install gdb
```

您可以安全地忽略安装过程中关于“特殊权限”请求的消息。

>**重要**
>
>GDB 不支持 gdb Arm-based Macs。因此，要么从源代码编译 `gdb`，要么使用 `lldb` 来代替 `gdb`。开发者没有为在 Arm-based Macs 上运行 GDB 提供官方支持。可以在 Sourceware.org 的 GDB 邮件列表中找到有关 GDB 的支持。 lldb 可作为 Xcode 命令行工具的一部分进行安装。

#### MS Windows

GDB 包含在我们的 Pico Windows 安装程序中。它也包含在 Arm GNU Toolchain Downloads 中。

或者，您可以在我们的《树莓派 Pico 入门指南》第 9 章和附录 A 中找到有关手动安装的信息。

>**注意**
>
> 不建议在 Windows 上手动安装 GDB。 

## 串行线调试（SWD）

Serial Wire Debug (SWD)是一种两引脚接口（SWDIO 和 SWCLK），可替代 JTAG 四或五引脚调试接口标准。

### 将新程序上传到您的 Pico

Pico 调试器可使您通过 SWD 接口和 OpenOCD 来加载二进制文件：从而无需在每次将新二进制文件推送到 Pico 后拔下，然后按住 BOOTSEL 按钮这些操作。使用调试器上传新的二进制文件是完全自动化的。

假如您构建了一个二进制文件：

```
$ sudo openocd -f interface/cmsis-dap.cfg -f target/rp2040.cfg -c "adapter speed 5000" -c "program blink.elf verify reset exit"
```

>**注意**
>
>当您使用调试器上传二进制文件时，使用的是文件的 ELF 版本，而不是您在拖放时使用的 UF2 文件。

### 使用 SWD 进行调试

它还将让您在服务器模式下使用 openocd ，并连接 GDB，这将为您提供断点和“正确”的调试。

```
$ cd ~/pico/pico-examples/
$ rm -rf build
$ mkdir build
$ cd build
$ export PICO_SDK_PATH=../../pico-sdk
$ cmake -DCMAKE_BUILD_TYPE=Debug ..
$ cd blink
$ make -j4
```

在调试构建中，当您在调试器下运行时，您将获得更多信息，因为编译器会使用信息构建您的程序，以告诉 GDB 您的程序正在做什么。

 有关更多信息，请参阅《树莓派 Pico 入门指南》第 6 章。

要启动 OpenOCD 服务器，请运行以下命令：

```
$ sudo openocd -f interface/cmsis-dap.cfg -f target/rp2040.cfg -c "adapter speed 5000"
```

然后打开第二个终端窗口，切换到包含您构建的二进制文件的目录，并启动调试器以将其附加到 OpenOCD 服务器：

```
$ gdb blink.elf
> target remote localhost:3333
> monitor reset init
> continue
```

GDB 不适用于所有平台。根据您的操作系统和设备，请使用以下替代方案取代 gdb ：

* 在非树莓派设备上使用 `gdb-multiarch`。
* 在基于 Arm 的 macOS 设备上使用 `lldb`。

## 串行连接

确保调试器连接到了您树莓派 Pico 的 UART 引脚。

![wiring](https://www.raspberrypi.com/documentation/microcontrollers/images/wiring.png)

树莓派 Pico UART0 的默认引脚如下：

| 默认 UART0 | 物理引脚 | GPIO 引脚 |
| ------------ | ---------- | ----------- |
| GND        | 3        | 不适用    |
| UART0_TX   | 1        | GP0       |
| UART0_RX   | 2        | GP1       |

在连接后，树莓派 Pico 的 UART 上的流量将通过调试器中继到您的计算机，并显示为 CDC UART。在树莓派上，显示为 /dev/ttyACM0 ；在其他平台上，此串口将以不同方式显示（例如，在 macOS 上，显示为 /dev/cu.usbmodemXXXX ）。

如果您尚未安装 minicom，请执行以下操作：

```
$ sudo apt install minicom
```

并打开串口：

```
$ minicom -b 115200 -o -D /dev/ttyACM0
```

>**技巧**
>
>要退出 minicom ，请按 CTRL-A，然后按 X 键。 

要测试串行通信，您可以构建并上传“Hello World”示例应用程序。

进入 pico-examples 树中的 hello_world 目录，并运行 make 。之后，您可以使用 openocd 将其上传到您的树莓派 Pico。要了解构建 hello_serial 示例程序的完整步骤，请参阅《开始使用树莓派 Pico》第 4 章。

```
$ cd pico-examples
$ mkdir build
$ cd build
$ export PICO_SDK_PATH=../../pico-sdk
$ cmake ..
$ cd hello_world/serial
$ make -j4
$ sudo openocd -f interface/cmsis-dap.cfg -f target/rp2040.cfg -c "adapter speed 5000" -c "program hello_serial.elf verify reset exit"
$ minicom -b 115200 -o -D /dev/ttyACM0
```

打开 minicom 后，应该在控制台上看到打印出了"Hello, world!"。

对于支持的终端程序，USB 串行 UART 的描述会在 USB 设备描述中进行广告。

![description](https://www.raspberrypi.com/documentation/microcontrollers/images/description.jpg)

此描述中的唯一序列号意味着在 Windows 上，您的 COM 端口编号是"粘性"的每个设备，并且将允许您编写 udev 规则以将命名设备节点与特定的调试器绑定起来。

## 更新调试器固件

调试器固件以 UF2 文件的形式由树莓派分发。

调试器固件的最新版本是版本 2。如果您正在运行旧版，或者如果您意外地覆盖了调试器的固件，您可以在 debugprobe GitHub 存储库中找到最新版本的固件。

从最新版本下载 debugprobe.uf2 。

捏住调试器外壳顶部以拆除。

在将调试器插入计算机时按住 BOOTSEL 按钮，以挂载名为“RPI-RP2”的卷。

将 debugprobe.uf2 复制到 "RPI-RP2" 卷。文件复制到设备后，将自动卸载设备。

您的调试器将重启，现在运行更新版本的调试器固件。现在已准备好进行调试了。

## 框图

调试器的原理图和机械图纸可用：

* 原理图（PDF）
* 机械图（PDF）

原理图上显示的测试点（TP）位于下图所示位置。

![debug probe tps](https://www.raspberrypi.com/documentation/microcontrollers/images/debug-probe-tps.jpg)
