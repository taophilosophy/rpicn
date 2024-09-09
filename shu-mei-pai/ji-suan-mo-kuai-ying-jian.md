# 计算模块硬件


## 计算模块

树莓派计算模块是衍生于旗舰级树莓派的嵌入式核心板（system-on-module，SOM）。计算模块在工业和商业应用中极受欢迎，如数字标牌、瘦客户机和自动化流程。上述程序有设计用于旗舰级树莓派的，但许多用户希望拥有更紧凑的设计及内置 eMMC 存储。

计算模块有多款衍生产品，内存和嵌入式多媒体卡（eMMC）闪存容量各不相同。eMMC 类似于 SD 卡，只是焊接在主板上。与 SD 卡不同，eMMC 专门设计用作磁盘，包含增强功能来提高可靠性。Lite 型号未搭载内置存储，并且有时用简写后缀 L 来表？示，例如“CM3L”。

计算模块使用以下树莓派 SoC（片上系统）:

* CM1 采用 BCM2835
* CM3, CM3+ 采用 BCM2837
* 适用于 CM4，CM4S 的 BCM2711

### 计算模块 4

最新款的计算模块是计算模块 4（CM4）。我们建议，现在所有的开发都应使用 CM4。

![计算模块 4](https://www.raspberrypi.com/documentation/computers/images/cm4.jpg)

计算模块 4

计算模块 4（CM4）搭载了树莓派 4 的内部构件（BCM2711 处理器和 1GB、2GB、4GB 或 8GB 的 RAM），以及可选的 0GB（Lite）、8GB、16GB 或 32GB 的 eMMC 闪存存储。

与 CM1、CM3 和 CM3+ 不同，CM4 未使用 DDR2 SODIMM 外形规格。相反，CM4 使用了两个 100 针高密度连接器，有更小的物理空间占用。这种变化帮助增加了以下接口：

* 额外的第二个 HDMI
* PCIe
* 以太网

旧版的外形规格无法支持这些接口。

### 计算模块 4S

![计算模块 4S](https://www.raspberrypi.com/documentation/computers/images/cm4s.jpg)

计算模块 4S

计算模块 4S（CM4S）搭载了树莓派 4 的内部构件（BCM2711 处理器和 1GB、2GB、4GB 或 8GB 的 RAM），以及可选的 0GB（Lite）、8GB、16GB 或 32GB 的 eMMC 闪存存储。与 CM4 不同，CM4S 采用了与 CM1、CM3 和 CM3+ 相同的 DDR2 SODIMM 外形规格。

### 计算模块 3+

![计算模块 3+](https://www.raspberrypi.com/documentation/computers/images/cm3-plus.jpg)

计算模块 3+

计算模块 3+（CM3+）搭载了树莓派 3B+（BCM2837 处理器和 1GB 内存）的内部构件，以及可选的 0GB（Lite）、8GB、16GB 或 32GB eMMC 闪存存储。

### 计算模块 3

![计算模块 3](https://www.raspberrypi.com/documentation/computers/images/cm3.jpg)

计算模块 3

计算模块 3（CM3）搭载了树莓派 3 的内部构件（BCM2837 处理器和 1GB 的 RAM），以及可选的 4GB eMMC 闪存存储。

### 计算模块 1

![计算模块 1](https://www.raspberrypi.com/documentation/computers/images/cm1.jpg)

计算模块 1

计算模块 1（CM1）搭载了树莓派的内部构件（BCM2835 处理器和 512MB 内存），以及可选的 4GB eMMC 闪存存储。

## IO 板

树莓派 IO 板提供了一种将单个计算模块连接到各种 I/O（输入/输出）接口的方法。由于计算模块本质上较小，因此它们缺少端口和连接器。IO 板提供了一种将计算模块连接到各种外围设备的方法。

IO 板是旨在开发的分支板；在生产中，你应该使用一个更小的、也许是定制的板——这块板仅提供了你的用例所需的端口和外部设备。

### 计算模块 4 IO 板

![计算模块 4 IO 板](https://www.raspberrypi.com/documentation/computers/images/cm4io.jpg)

计算模块 4 IO 板

计算模块 4 IO 板提供以下接口：

* 带有 40 针 GPIO 连接器和 PoE 标头的 HAT 印记
* 两个 HDMI 端口
* 两个 USB 2.0 端口
* 带 PoE 支持的千兆以太网 RJ45
* MicroSD 卡槽（仅适用于没有 eMMC 的 Lite 衍生款）
* PCIe Gen 2 接口
* 通过圆形插孔输入 12V（如未使用 PCIe，最高可达 26V）
* MIPI DSI × 2 显示 FPC 连接器（22 引脚 0.5 mm 间距电缆）
* MIPI CSI-2 × 2 摄像头 FPC 连接器（22 引脚 0.5 mm 间距电缆）
* 带电池插座的实时时钟

### 计算模块 IO 板

![计算模块 IO 板](https://www.raspberrypi.com/documentation/computers/images/cmio.jpg)

计算模块 IO 板

计算模块 IO 板提供以下接口：

* 120 个 GPIO 引脚
* 一个 HDMI 端口
* 一个 USB-A 端口
* MIPI DSI × 2 显示器 FPC 连接器（22 针 0.5 mm 间距电缆）
* MIPI CSI-2 × 2 相机 FPC 连接器（22 针 0.5 mm 间距电缆）

计算模块 IO 板有两个衍生：版本 1 和版本 3。版本 1 仅兼容 CM1。版本 3 兼容 CM1、CM3、CM3+ 和 CM4S。计算模块 IO 板版本 3 有时被简写为 CMIO3。

### IO 板兼容性

不是所有计算模块 IO 板都适用于所有计算模块型号。以下表格显示了每个 IO 板适用于哪些计算模块：

| IO 板                               | 兼容的计算模块                                |
| ------------------------------------- | ----------------------------------------------- |
|计算模块 IO 板版本 1 (CMIO)/(CMIO1) | - CM1                                         |
|计算模块 IO 板版本 3 (CMIO)/(CMIO3) |计算模块 1 计算模块 3 计算模块 3+计算模块 4S |
|计算模块 4 IO 板 (CM4IO)            |计算模块 4                                    |

## 将镜像刷写到计算模块

计算模块搭载了连接到主 SD 卡接口的内置 eMMC 设备。本指南解释了如何将操作系统镜像刷写到单个计算模块的 eMMC 存储器。

当向多个计算模块刷写镜像时，请考虑使用计算模块配置工具：

##### [使用计算模块配置器进行大规模配置](https://pip.raspberrypi.com/categories/685-whitepapers-app-notes/documents/RP-003468-WP/Using-the-Compute-Module-Provisioner.pdf)

使用计算模块配置器进行大规模配置

计算模块配置器是一款 Web 应用程序，可帮助开发人员同时为多个计算模块设备编程。

它提供了内核镜像数据库和在闪存过程中运行脚本的能力，以及自动标签打印和固件更新。

### 准备工作

要刷写计算模块 eMMC，你需要以下物品：

* 本指南中称为主机设备的其他计算机。你可以使用 Linux（树莓派系统或 Ubuntu）、Windows 和 macOS。
* 与你的计算模块型号对应的计算模块 IO 板。
* 一根 Micro USB 线。

### 设置 IO 板

要开始，物理设置你的 IO 板。比如将计算模块和主机设备接入 IO 板。

#### 使用计算模块 4 IO 板

设置计算模块 4 IO 板：

1. 将计算模块连接到 IO 板。连接后，计算模块应该平放。
2. 将 nRPI_BOOT 安装到 IO 板跳线帽 J2（ disable eMMC Boot ）。
3. 将一根电缆从 IO 板上的 micro USB 从机端口 J11 连接到主机设备。

#### 使用计算模块 IO 板

要设置计算模块 IO 板：

1. 将计算模块连接到 IO 板。连接后，计算模块应平行于板放置，使接合夹牢固地卡入位。
2. 将 J4（启用 USB SLAVE BOOT）设置为 `1-2 =`（启用 USB BOOT）
3. 将一根电缆从 IO 板上的 micro USB 从机端口 J15 连接到主机设备。

### 配置主机设备

接下来，在主机设备上配置软件。

#### 在 Linux 上配置软件

在 Linux 主机设备上配置软件：

1. 运行以下命令安装 `rpiboot` ：

    ```bash
    $ sudo apt install rpiboot
    ```
2. 将 IO 板接入电源。
3. 然后运行 `rpiboot` :

    ```bash
    $ sudo rpiboot
    ```
4. 几秒钟后，计算模块应该会显示成一个大容量存储设备。查看 `/dev/` 目录，可能是 `/dev/sda` 或 `/dev/sdb`，查找该设备。或者，运行 `lsblk` 并搜索一个存储容量与你的计算模块容量相匹配的设备。

>**技巧**
>
> 你还可以从源代码编译 `rpiboot`。

#### 在 macOS 上配置软件

在 macOS 主机设备上配置软件：

1. 首先，从源代码编译 `rpiboot`。
2. 将 IO 板连接到电源。
3. 然后，使用以下命令运行 `rpiboot` 可执行文件：

    ```bash
    $ sudo ./rpiboot
    ```
4. 在命令运行完成后，你应该会看到一条消息，宣称“The disk you inserted was not readable by this computer.（你插入的磁盘无法被此计算机读取）” 点击“**Ignore（忽略）**”。你的计算模块现在应该显示成了一个大容量存储设备。

#### 在 Windows 上配置软件

在 Windows 主机设备上配置软件：

1. 下载 Windows 安装程序
2. 双击安装程序运行。这将安装驱动程序和引导工具。
3. 将 IO 板连接到电源。Windows 应该会发现硬件并配置所需的驱动程序。
4. 双击运行 `RPiBoot.exe`。几秒钟后，计算模块 eMMC 应该会显示为 USB 大容量存储设备。

>**技巧**
>
> 或者，你可以从源代码编译 `rpiboot`。

### 刷写 eMMC

你可以使用树莓派启动盘制作工具把操作系统镜像刷写到计算模块上。

还可使用 `dd` 来将裸操作系统镜像（例如树莓派系统）写入你的计算模块。运行以下命令，请把 `/dev/sdX` 替换成你的计算模块的大容量存储设备代表形式的路径，并把 `raw_os_image.img` 替换为你的原始操作系统镜像的路径：

```bash
$ sudo dd if=raw_os_image.img of=/dev/sdX bs=4MiB
```

镜像写入后，断开计算模块，然后重新接入。现在应该能看到两个分区（用于树莓派系统）：

```json
/dev/sdX    <- 设备
/dev/sdX1   <- 第一个分区（FAT）
/dev/sdX2   <- 第二个分区（Linux 文件系统）
```

你可以正常挂载分区 `/dev/sdX1` 和 `/dev/sdX2`。

### 从 eMMC 启动

#### 使用计算模块 4 IO 板

从 IO 板跳线上的 J2 (禁用 eMMC Boot) 断开 `nRPI_BOOT`。

#### 使用计算模块 IO 板

将 J4（启用 USB SLAVE BOOT）设置为 `2-3`（禁用 USB BOOT）。

#### 启动

断开 USB 从属端口。重启 IO 板，从你刚刚写入 eMMC 的新镜像引导计算模块。

### 已知问题

* 小部分 CM3 存在启动问题。我们已经认识到这些问题与创建 FAT32 分区的方法有关；我们认为问题是由于 CPU 和 eMMC 之间的时序差异造成的。如果你在启动 CM3 时遇到问题，请使用以下命令手动创建分区：

  ```bash
  $ sudo parted /dev/<设备>
  (parted) mkpart primary fat32 4MiB 64MiB
  (parted) q
  $ sudo mkfs.vfat -F32 /dev/<设备>
  $ sudo cp -r <文件>/* <挂载点>
  ```
* CM1 引导加载程序会向主机返回一个略有错误的 USB 数据包。大多数 USB 主机会忽略它，但由于该问题，某些 USB 接口无法工作。CM3 已修复该错误。

### 计算模块 4 引导加载程序

CM4 上的默认引导加载程序配置旨在支持在计算模块 4 IO 板上启动和开发，并且在制造时刷写的软件版本可能比最新版本要旧。对于最终产品，请考虑：

* 选择并验证特定的引导加载程序版本。usbboot 存储库中的版本始终是最新稳定版本。
* 配置引导设备（例如网络引导）。请参阅引导加载程序配置指南中的 BOOT_ORDER 部分。
* 启用引导加载程序 EEPROM 上的硬件写保护，可确保在无法触及的产品（如远程和嵌入式设备）上的引导加载程序无法被篡改。

>**注意**
>
> 计算模块 4 ROM 不从 SD/EMMC 运行 `recovery.bin`，在默认情况下，服务 `rpi-eeprom-update` 未启用。这是必要的，因为 EMMC 不可拆卸，无效的 `recovery.bin` 文件将妨碍系统启动。这可以被覆盖，与 `self-update` 模式一同使用，其中引导加载程序可以从 USB 大容量存储设备和网络引导进行更新。但是，在更新 EEPROM 时发生断电后，`self-update` 模式不是原子更新，所以不安全。


#### 除存储卡之外的闪存设备

基于 Linux 的大容量存储设备支持 NVMe、EMMC 和 USB 设备的闪存存储。这通常比使用 `rpiboot` 固件驱动程序更快，还为设备提供串口控制台，可更容易地进行调试。

另请参阅：CM4 `rpiboot` 扩展。

#### 修改引导加载程序配置

要修改 CM4 引导加载程序配置：

* 切换到目录 `usbboot/recovery`
* 如果需要特定的引导加载程序版本，请替换 `pieeprom.original.bin`
* 编辑默认的引导加载程序配置文件 `boot.conf`；通常至少需要更新 BOOT_ORDER：
  * 若使用网络启动，请使用 `BOOT_ORDER=0xf2`
  * 若使用 SD/EMMC 启动，请使用 `BOOT_ORDER=0xf1`
  * 若要在 USB 启动失败后切换到 EMMC，请使用 `BOOT_ORDER=0xf15`
* 运行 `./update-pieeprom.sh` 可更新用于 EEPROM 镜像的镜像文件 `pieeprom.bin` 
* 如果需要 EEPROM 写保护，请编辑 `config.txt`，添加 `eeprom_write_protect=1`。硬件写保护必须通过软件启用，然后通过将 `EEPROM_nWP` 引脚拉低进行锁定
* 运行 `../rpiboot -d .` 可使用用于更新的 EEPROM 镜像的 `pieeprom.bin` 更新引导加载程序

文件 `pieeprom.bin` 现在已准备好刷写到计算模块 4 了。

#### 为计算模块 4 刷写引导加载程序 EEPROM

要刷写引导加载程序 EEPROM，请遵循与刷写 EMMC 相同的硬件设置，但还要确保 `EEPROM_nWP` 未被拉低。完成后，`EEPROM_nWP` 可以再次被拉低。运行以下命令将 `recovery/pieeprom.bin` 写入引导加载程序 EEPROM：

```bash
$ ./rpiboot -d recovery
```

## 连接外围设备

本指南帮助开发人员将外围设备连接到计算模块引脚。此外，本指南解释了如何更改软件以启用这些外围设备。

SoC 的大多数引脚（GPIO、两个 CSI 摄像头接口、两个 DSI 显示接口、HDMI 等）可用于连接。通常可以将未使用的引脚保持未连接状态。

带有 DDR2 SODIMM 外形规格的计算模块能插入 DDR2 SODIMM 插槽。但是，引脚分配与 SODIMM 内存模块不同。

要使用计算模块，用户设计的主板必须满足：

* 为计算模块供电（3.3V，最低 1.8V）
* 将引脚连接到用户应用程序所需的外围设备

树莓派的 IO 板提供以下功能：

* 为模块供电
* 将 GPIO 引线连接到引脚排
* 将摄像头和显示接口引线连接到 FFC 连接器
* 将 HDMI 引线连接到 HDMI 端口
* 将 USB 线连接到 USB 端口
* 将活动监视器连接到“ACT” LED
* 通过 USB 进行 eMMC 编程

本指南首先解释了引导过程以及设备树如何描述连接的硬件。

然后，我们将解释如何将 I²C 和 SPI 外围设备连接到 IO 板。最后，我们将创建使用这两个外围设备所需的设备树文件，以便在树莓派系统上使用。

### BCM283x GPIO

BCM283x 带有三个通用输入/输出（GPIO）引脚组：BANK0 上有 28 个引脚，BANK1 上有 18 个引脚，BANK2 上有 8 个引脚，总共 54 个引脚。这些引脚可以用作真正的 GPIO 引脚：软件可以将它们设置为输入或输出，读取和/或设置状态，并将它们用作中断。它们还可以运行诸如 I²C、SPI、I²S、UART、SD 卡等其他功能。

所有计算模块上都可以使用 BANK0 和 BANK1。不要使用 BANK2：它控制 eMMC、HDMI 热插拔检测和 ACT LED/USB 引导控制。

使用 `pinctrl` 来检查 GPIO 引脚的电压和功能，以查看你的设备树是否按预期工作。

### BCM283x 引导过程

BCM283x 设备搭载了 VideoCore GPU 和 Arm CPU 核心。GPU 包括 DSP 处理器和用于图像处理、视频编解码、3D 图形和图像合成的硬件加速器。

在 BCM283x 设备中，首先启动了 GPU 中的 DSP 核心。它在启动主 Arm 处理器之前处理设置。

树莓派 BCM283x 设备有三阶段引导过程：

* GPU DSP 退出复位并从小型内部引导 ROM 执行代码。此代码通过外部接口加载第二阶段引导加载程序。此代码首先在称为 `bootcode.bin` 的引导分区上查找第二阶段引导加载程序。如果未找到引导设备或未找到 `bootcode.bin`，引导 ROM 将在 USB 引导模式下等待主机提供第二阶段引导加载程序（`usbbootcode.bin`）。
* 第二阶段引导加载程序负责设置 LPDDR2 SDRAM 接口和其他关键系统功能。设置完成后，第二阶段引导加载程序加载并执行主 GPU 固件（`start.elf`）。
* `start.elf` 处理额外的系统设置并启动 Arm 处理器子系统。它包含 GPU 固件。GPU 固件首先读取 `dt-blob.bin` 以确定初始 GPIO 引脚状态和 GPU 特定接口和时钟，然后解析 `config.txt`。然后加载特定于模型的 Arm 设备树文件和在 `config.txt` 中指定的任意设备树叠加，然后启动 Arm 子系统并将设备树数据传递给正在引导的 Linux 内核。

### 设备树

树莓派的 Linux 设备树编码了连接到系统的硬件信息以及用于与该硬件通信的驱动程序。

引导分区包含几个二进制设备树（`.dtb`）文件。设备树编译器使用可读的设备树描述（`.dts`）创建这些二进制文件。

引导分区包含两种不同类型的设备树文件。一种仅供 GPU 使用；其余是针对每个基于 BCM283x 的树莓派产品的标准 Arm 设备树文件：

* dt-blob.bin （供 GPU 使用）
* bcm2708-rpi-b.dtb （用于树莓派 1B 和 B）
* bcm2708-rpi-b-plus.dtb （用于树莓派 i 1B+ 和 A+）
* bcm2709-rpi-2-b.dtb （用于树莓派 2B）
* bcm2710-rpi-3-b.dtb （用于树莓派 3B）
* bcm2708-rpi-cm.dtb （用于树莓派计算模块 1）
* bcm2710-rpi-cm3.dtb （用于树莓派计算模块 3）

在启动过程中，用户可以通过 `device_tree` 参数在 `config.txt` 中指定了要使用的特定 Arm 设备树。例如，`config.txt` 中的 `device_tree=mydt.dtb` 这行指定了一个名为 `mydt.dtb` 文件中的 Arm 设备树。

你可以为计算模块产品创建完整的设备树，但我们建议改用叠加层。叠加层向基本设备树添加非特定于板的硬件描述。这包括使用的 GPIO 引脚及其功能，以及连接的设备，以便正确加载驱动程序。引导加载程序在将设备树传递给 Linux 内核之前将叠加层与基本设备树合并。基本设备树偶尔会更改，通常不会破坏叠加层。

使用 dtoverlay 参数在 config.txt 中加载设备树叠加层。树莓派系统假定所有叠加层位于目录 `/overlays` 中，使用后缀 `-overlay.dtb`。例如，`dtoverlay=myoverlay` 这行加载了叠加层 `/overlays/myoverlay-overlay.dtb`。

要将外围设备连接到计算模块，请在叠加层中描述连接到 BANK0 和 BANK1 GPIO 的所有硬件。这样你就可以使用标准的树莓派系统镜像，因为叠加层已合并到标准基础设备树中。或者，你还可以为你的应用程序定义自定义设备树，但你将无法使用标准的树莓派系统镜像。因此，你必须创建一个包含你自定义设备树的修改后的树莓派系统镜像，以便分发你想分发的每个操作系统更新。如果基础叠加层发生更改，则可能需要更新你的定制设备树。

### `dt-blob.bin`

当 `start.elf` 运行时，它首先读取 `dt-blob.bin`。这是一种特殊形式的设备树 blob，告诉 GPU 如何设置 GPIO 引脚状态。

dt-blob.bin 包含由 GPU 而不是 SoC 控制的 GPIO 和外围设备的信息。例如，GPU 管理摄像头模块。GPU 需要独占访问 I²C 接口和一些引脚，以便与摄像头模块通信。

在大多数树莓派型号上，I2C0 专为 GPU 独占使用。`dt-blob.bin` 定义了用于 I2C0 的 GPIO 引脚。

默认情况下，`dt-blob.bin` 不存在。作为替代，`start.elf` 是此文件的内置版本。许多计算模块项目提供了一个自定义 `dt-blob.bin`，该文件覆盖了默认的内置文件。

  `dt-blob.bin` 指定了：

* 用于 HDMI 热插拔检测的引脚
* 用作 GPCLK 输出的 GPIO 引脚
* GPU 在引导过程中可以使用的 ACT LED

`minimal-cm-dt-blob.dts` 是一个示例 `.dts` 设备树文件。它设置了 HDMI 热插拔检测，ACT LED，并将所有其他 GPIO 设置为带有默认拉电的输入。

要将 `minimal-cm-dt-blob.dts` 编译为 `dt-blob.bin`，请使用设备树编译器 `dtc`。要在树莓派上安装 `dtc`，请运行以下命令：

```bash
$ sudo apt install device-tree-compiler
```

然后，运行以下命令将 `minimal-cm-dt-blob.dts` 编译为 `dt-blob.bin` ：

```bash
$ dtc -I dts -O dtb -o dt-blob.bin minimal-cm-dt-blob.dts
```

获取更多信息，请参阅我们的创建指南 dt-blob.bin。

### Arm Linux 设备树

在 `start.elf` 读取 `dt-blob.bin`，设置初始引脚状态和时钟后，它就会读取 `config.txt`，其中包含许多其他系统设置选项。

在读取 `config.txt` 后，`start.elf` 会读取一个特定于模型的设备树文件。例如，计算模块 3 使用 `bcm2710-rpi-cm.dtb`。该文件是一个标准的 Arm Linux 设备树文件，详细说明连接到处理器的硬件。它枚举了：

* 外围设备的种类和位置
* 使用了哪些 GPIO
* 这些 GPIO 有什么功能
* 连接了哪些物理设备

如果与 `dt-blob.bin` 不同，此文件将通过覆盖引脚状态来设置 GPIO，并尝试为特定设备加载驱动程序。

特定型号的设备树文件包含了对外围设备的禁用条目。除了 eMMC/SD 卡外设备的 GPIO 引脚定义外，它不包含其他 GPIO 引脚定义，并且始终使用相同的引脚。

### 设备树源码和编译

树莓派系统镜像提供了预编译的 dtb 文件，但源 dts 文件位于树莓派 Linux 内核分支中。在文件名中查找 `rpi`。

默认叠加层 dts 文件位于 `arch/arm/boot/dts/overlays`。这些叠加层文件是创建自己的叠加层的好起点。要将这些 dts 文件编译为 dtb 文件，请使用设备树编译器 dtc。

在编译自己的内核时，构建主机需要 `scripts/dtc` 中的设备树编译器。要自动构建叠加层，请将它们添加到 dtbs 中的 `make` 目标中 `arch/arm/boot/dts/overlays/Makefile`。

### 设备树调试

当启动 Linux 内核时，GPU 使用基础 dts 和任意叠加层创建完整的设备树。这个完整的树可以通过 Linux proc 接口在 `/proc/device-tree` 中浏览。节点变成目录，属性变成文件。

你可以使用 `dtc` 将其写成可供人类阅读的 dts 文件以进行调试。要查看完整的组装设备树，请运行以下命令：

```bash
$ dtc -I fs -O dts -o proc-dt.dts /proc/device-tree
```

`pinctrl` 提供了 GPIO 引脚的状态。如果出现问题，请尝试转储 GPU 日志消息：

```bash
$ sudo vclog --msg
```

>**技巧**
>
> 要在输出中包含更多诊断信息，请将 `dtdebug=1` 添加到 `config.txt`。

使用设备树树莓派论坛提出设备树相关问题或报告问题。

### 示例

以下示例使用带有通过跳线连接的外围设备的 IO 板。我们假设使用了旧版的精简版树莓派系统运行 CM1+CMIO 或 CM3+CMIO3。这里的示例需要互联网连接，因此我们建议将 USB 集线器、键盘和无线局域网或以太网转接器插入 IO 板的 USB 端口。

#### 将 I²C RTC 连接到 BANK1 引脚

在这个示例中，我们将 NXP PCF8523 实时时钟（RTC）连接到 IO 板的 BANK1 GPIO 引脚：3V3、GND、GPIO44 上的 `I2C1_SDA` 和 GPIO45 上的 `I2C1_SCL`。

下载 `minimal-cm-dt-blob.dts`，将其复制到 `/boot/firmware/` 的引导分区中。

编辑 `minimal-cm-dt-blob.dts`,将 GPIO44 和 45 的引脚状态更改为带上拉的 I2C1：

```bash
$ sudo nano /boot/firmware/minimal-cm-dt-blob.dts
```

替换以下行：

```bash
pin@p44 { function = "input"; termination = "pull_down"; }; // 默认状态为输入无拉取
pin@p45 { function = "input"; termination = "pull_down"; }; // 默认状态为输入无拉取
```

使用以下上拉定义：

```bash
pin@p44 { function = "i2c1"; termination = "pull_up"; }; // SDA1
pin@p45 { function = "i2c1"; termination = "pull_up"; }; // SCL1
```

我们可以在不进行任何改动的情况下使用此 `dt-blob.dts`，因为 Linux 设备树在特定驱动程序加载时重新配置这些引脚。但是，如果配置了 `dt-blob.dts`，GPIO 在 GPU 引导阶段尽快达到最终状态。在某些情况下，必须在 GPU 引导时配置引脚，以便在加载 Linux 驱动程序时处于特定状态。例如，重置线可能需要保持在正确的方向上。

运行以下命令编译 `dt-blob.bin` ：

```bash
$ sudo dtc -I dts -O dtb -o /boot/firmware/dt-blob.bin /boot/firmware/minimal-cm-dt-blob.dts
```

下载 `example1-overlay.dts`，将其复制到 `/boot/firmware/` 中的引导分区，然后使用以下命令编译：

```bash
$ sudo dtc -@ -I dts -O dtb -o /boot/firmware/overlays/example1.dtbo /boot/firmware/example1-overlay.dts
```

参数 `-@` 编译具有外部引用的 dts 文件。一般是必要的。

将以下行添加到 `/boot/firmware/config.txt` 中：

```bash
dtoverlay=example1
```

最后，使用 `sudo reboot` 重启。

重启后，你将在 `/dev` 中看到一项 `rtc0`。运行以下命令查看硬件时钟时间：

```bash
$ sudo hwclock
```

#### 在 BANK0 上连接一个 ENC28J60 SPI 以太网控制器

在这个示例中，我们使用已在 `/boot/firmware/overlays` 中定义的叠加层，将以太网控制器 ENC28J60 SPI 添加到 BANK0。以太网控制器使用 SPI 引脚 CE0、MISO、MOSI 和 SCLK（分别为 GPIO8-11），GPIO25 用于下降沿中断，另外还有 GND 和 3.3V。

在本示例中，我们不会更改 `dt-blob.bin`。而是将以下行添加到 `/boot/firmware/config.txt` 中：

```
dtoverlay=enc28j60
```

 使用 sudo reboot 重启。

你将在 `/dev` 中看到一项 `rtc0`。运行以下命令查看硬件时钟时间：

```bash
$ sudo hwclock
```

你还应该具有以太网连接性。运行以下命令测试你的连接性：

```bash
$ ping 8.8.8.8
```

运行以下命令显示 GPIO 功能；GPIO8-11 现在应提供 ALT0（SPI）功能：

```bash
$ pinctrl
```

## 连接摄像头模块

计算模块具有两个 CSI-2 摄像头接口：CAM1 和 CAM0。本节将说明如何使用计算模块 I/O 板将一个或两个树莓派摄像头连接到计算模块的 CAM1 和 CAM0 接口。

### 更新你的系统

在配置摄像头之前，请确保你树莓派的固件是最新的。

```bash
$ sudo apt update
$ sudo apt full-upgrade
```

### 连接一个摄像头

要将单个摄像头连接到计算模块，请完成以下步骤：

1. 断开计算模块的电源。
2. 使用 RPI-CAMERA 板/树莓派 Zero 摄像头电缆将摄像头模块连接到 CAM1 接口。

![连接到转接板](https://www.raspberrypi.com/documentation/computers/images/CMIO-Cam-Adapter.jpg)

3. （仅限 CM1、CM3、CM3+ 和 CM4S）：使用跳线电缆连接以下 GPIO 引脚：

    * 0 到 CD1_SDA
    * 1 到 CD1_SCL
    * 2 到 CAM1_I01
    * 3 到 CAM1_I00 

![接入单个相机的 GPIO 连接器](https://www.raspberrypi.com/documentation/computers/images/CMIO-Cam-GPIO.jpg)

4. 重新连接计算模块到电源。
5. 在 `/boot/firmware/config.txt` 中删除（或使用前缀 `#` 注释掉）以下行，如果存在的话：

    ```bash
    camera_auto_detect=1
    ```

    ```bash
    dtparam=i2c_arm=on
    ```
6. (仅适用于 CM1、CM3、CM3+ 和 CM4S)：向 /boot/firmware/config.txt 添加以下指令，以适应 I/O 板上 GPIO 引脚分配的交换：

    ```bash
    dtoverlay=cm-swap-i2c0
    ```
7. (仅适用于 CM1、CM3、CM3+ 和 CM4S)：向 /boot/firmware/config.txt 添加以下指令，将 GPIO 3 分配为 CAM1 稳压器：

    ```bash
    dtparam=cam1_reg
    ```
8. 向 /boot/firmware/config.txt 添加适当的指令，手动配置相机型号的驱动程序： 

    | 相机型号 | 参数 | | :---------------------------------------------------------------------------: | :--: |
    | v1 相机                                                                   | `dtoverlay=ov5647,cam1` |
    | v2 相机                                                                   | `dtoverlay=imx219,cam1` |
    | v3 相机                                                                   | `dtoverlay=imx708,cam1` |
    | HQ 相机                                                                   | `dtoverlay=imx477,cam1` |
    | GS 相机                                                                   | `dtoverlay=imx296,cam1` |

9. 使用 sudo reboot 重启你的计算模块。
10. 运行以下命令以检查检测到的相机列表：

     ```bash
     $ rpicam-hello --list
     ```

     你应该能在上表中由驱动程序指令引用的摄像头型号中看到输出。

### 连接两台摄像头

要将两台摄像头连接到计算模块，请完成以下步骤：

1. 按照上述单摄像头说明操作。
2. 断开计算模块的电源。
3. 使用 RPI-CAMERA 板/树莓派 Zero 摄像头电缆将摄像头模块连接到 CAM0 接口。

![连接到转接板](https://www.raspberrypi.com/documentation/computers/images/CMIO-Cam-Adapter.jpg)

4. (仅适用于 CM1、CM3、CM3+ 和 CM4S)：使用跳线连接以下 GPIO 引脚：

    * 28 到 CD0_SDA
    * 29 到 CD0_SCL
    * 30 到 CAM0_I01
    * 31 到 CAM0_I00 

![搭载了附加摄像头的 GPIO 连接器](https://www.raspberrypi.com/documentation/computers/images/CMIO-Cam-GPIO2.jpg)

5. (仅限 CM4)：使用两根垂直方向的跳线连接 J6 GPIO 引脚。

![连接到垂直方向的 J6 GPIO 引脚](https://www.raspberrypi.com/documentation/computers/images/j6_vertical.jpg)

6. 重新连接计算模块到电源。
7. （仅适用于 CM1、CM3、CM3+ 和 CM4S）：向 `/boot/firmware/config.txt` 添加以下指令，将 GPIO 31 分配为 CAM0 调节器：

    ```
    dtparam=cam0_reg
    ```
8. 向 `/boot/firmware/config.txt` 添加对应的参数，手动配置相机型号的驱动程序： 

    | 相机型号 | 参数 | 
| :-------------------: | :--: |
    | v1 相机                                                                   | `dtoverlay=ov5647,cam0` |
    | v2 相机                                                                   | `dtoverlay=imx219,cam0` |
    | v3 相机                                                                   | `dtoverlay=imx708,cam0` |
    | HQ 相机                                                                   | `dtoverlay=imx477,cam0` |
    | GS 相机                                                                   | `dtoverlay=imx296,cam0` |

9. 使用 `sudo reboot` 重启你的计算模块。
10. 运行以下命令以检查检测到的相机列表：

     ```bash
     $ rpicam-hello --list
     ```

     你应该在上表中的驱动指令中看到两个摄像头型号的输出。

### 软件

树莓派系统内置了 libcamera 库，可帮助你使用树莓派拍摄图像。

#### 拍照

使用以下命令即时拍照，并将其保存成 PNG 编码的文件，文件名使用日期格式为 MMDDhhmmss：

```bash
$ rpicam-still --datetime -e png
```

使用参数 `-t` 添加毫秒级延迟。使用参数 `--width` 和 `--height` 可指定图像的宽度和高度。

#### 拍摄视频

使用以下命令立即开始录制十秒钟的视频，并将其保存到一个名为 `video.h264`，带有 h264 编解码器的文件中：

```bash
$ rpicam-vid -t 10000 -o video.h264
```

#### 指定要使用的摄像头

默认情况下，`libcamera` 总是使用 `--list-cameras` 列表中编号为 `0` 的相机。要指定相机参数，请从以下命令获取每个相机的编号值：

```bash
$ rpicam-hello --list-cameras
Available cameras
-----------------
0 : imx477 [4056x3040] (/base/soc/i2c0mux/i2c@1/imx477@1a)
    Modes: 'SRGGB10_CSI2P' : 1332x990 [120.05 fps - (696, 528)/2664x1980 crop]
           'SRGGB12_CSI2P' : 2028x1080 [50.03 fps - (0, 440)/4056x2160 crop]
                             2028x1520 [40.01 fps - (0, 0)/4056x3040 crop]
                             4056x3040 [10.00 fps - (0, 0)/4056x3040 crop]

1 : imx708 [4608x2592] (/base/soc/i2c0mux/i2c@0/imx708@1a)
    Modes: 'SRGGB10_CSI2P' : 1536x864 [120.13 fps - (768, 432)/3072x1728 crop]
                             2304x1296 [56.03 fps - (0, 0)/4608x2592 crop]
                             4608x2592 [14.35 fps - (0, 0)/4608x2592 crop]
```

在上述输出中：

* imx477 指的是编号为 `0` 的 HQ 相机
* imx708 指的是具有编号 `1` 的摄像头模块 3

要使用 HQ 摄像头，请将其编号(`0`) 传给参数 `--camera libcamera`：

```bash
$ rpicam-hello --camera 0
```

要使用摄像头模块 3，请将其编号 (`1`) 传给参数 `--camera libcamera`：

```bash
$ rpicam-hello --camera 1
```

### GPIO 引脚的 I²C 映射

在默认情况下，提供的摄像头驱动程序假定 CAM1 使用 `i2c-10`，CAM0 使用 `i2c-0`。计算模块 I/O 板将以下 GPIO 引脚映射到 `i2c-10` 和 `i2c-0` ：

|I/O 板型号   |i2c-10 引脚 | i2c-0 引脚 |
| :-------------:| :---------| :------------: |
| CM4 I/O 板   | GPIOs 44,45 | GPIOs 0,1  |
|计算模块 1、3、3+,计算模块 4S I/O 板 | GPIO 0,1   | GPIO 28,29 |

要连接相机到计算模块 1、计算模块 3、计算模块 3+和计算模块 4S I/O 板，添加以下参数到 `/boot/firmware/config.txt` 可匹配交换的引脚分配:

```bash
dtoverlay=cm-swap-i2c0
```

替代板可能使用其他引脚分配。查阅你板子的文档，并根据你的布局使用以下替代叠加层：

| 交换              | 叠加层|
| :-----------------: | :------: |
| 使用 GPIO 0、1 进行 i2c0           | `i2c0-gpio0`     |
| 使用 GPIO 28、29 进行 i2c0（默认） | `i2c0-gpio28`     |
| 使用 GPIO 44 和 45 进行 i2c0       | `i2c0-gpio44`     |
| 使用 GPIO 0&1 进行 i2c10 (默认)    | `i2c10-gpio0`     |
| 使用 GPIO 28&29 进行 i2c10         | `i2c10-gpio28`     |
| 使用 GPIO 44&45 进行 i2c10         | `i2c10-gpio44`     |

#### 用于关机的 GPIO 引脚

对于相机关机，设备树使用叠加层 `cam1_reg` 和 `cam0_reg` 分配的引脚。

CM4 IO 板为两个别名提供单个 GPIO 引脚，因此两个相机共享同一个调节器。

CM1、CM3、CM3+ 和 CM4S I/O 板未提供 `cam1_reg` 和 `cam0_reg` 的 GPIO 引脚，因此这些板上的稳压器已禁用。但是，你可以通过在 `/boot/firmware/config.txt` 中使用以下指令来启用它们：

* `dtparam=cam1_reg`
* `dtparam=cam0_reg`

要将 `cam1_reg` 和 `cam0_reg` 分配到自定义板上的特定引脚，请在 `/boot/firmware/config.txt` 中加入以下参数：

* `dtparam=cam1_reg_gpio=<pin 值>`
* `dtparam=cam0_reg_gpio=<pin 值>`

例如，要将引脚 42 用作 CAM1 的稳压器，请将指令 `dtparam=cam1_reg_gpio=42` 添加到 `/boot/firmware/config.txt`。

这些指令仅适用于直连 SoC 的 GPIO 引脚，而不适用于扩展的 GPIO 引脚。

## 连接官方 7 吋显示屏

在开始之前，请将系统软件和固件更新到最新版本。计算模块大多使用相同的流程，但有时物理差异会迫使针对特定型号进行更改。

### 连接显示器到 DISP1

>**注意**
>
> 树莓派 Zero 相机线不能作为 RPI-DISPLAY 适配器的替代品。这两款线的布线不同。

要连接显示器到 DISP1：

1. 断开计算模块的电源。
2. 通过 22W 至 15W 显示适配器，将显示器连接到计算模块 IO 板上的 DISP1 接口。
3. （仅限 CM1、CM3、CM3+和 CM4S）：使用跳线电缆连接以下 GPIO 引脚：
    * 0 到 `CD1_SDA`
    * 1 到 `CD1_SCL`
4. 重新连接计算模块到电源。
5. 将以下行添加到 `/boot/firmware/config.txt` ：

    ```json
    dtoverlay=vc4-kms-dsi-7inch
    ```
6. 使用 `sudo reboot` 重启你的计算模块。你的设备应该能检测到显示器并开始显示输出。

### 将显示器连接到 DISP0

连接显示器到 DISP0：

1. 通过 15w-22W 电源适配器将显示器连接到计算模块 IO 板上的 `DISP0` 接口。
2. （仅适用于 CM1、CM3、CM3+和 CM4S）：使用跳线电缆连接以下 GPIO 引脚：
    * 28 到 `CD0_SDA`
    * 29 到 `CD0_SCL`
3. 重新连接计算模块到电源。
4. 将以下行添加到 `/boot/firmware/config.txt`：

    ```json
    dtoverlay=vc4-kms-dsi-7inch
    ```
5. 使用 `sudo reboot` 重启你的计算模块。你的设备应该检测到显示器，然后开始显示输出。

### 禁用触摸屏

触摸屏不需要额外配置。将其连接到你的计算模块，如果成功检测到，触摸屏元素和显示器都应该正常工作。

要禁用触摸功能，但仍使用显示器，请在 `/boot/firmware/config.txt` 中添加以下行：

```bash
disable_touchscreen=1
```

### 禁用显示器

在连接时完全忽略显示器，请将以下行添加到 `/boot/firmware/config.txt`：

```bash
ignore_lcd=1
```

## 规格

### 计算模块 4 数据表

了解有关计算模块 4（CM4）及其相应 IO 板的更多信息，请参阅以下文档：

* [CM4 数据表](https://datasheets.raspberrypi.com/cm4/cm4-datasheet.pdf)

##### [配置计算模块 4](https://pip.raspberrypi.com/categories/685-whitepapers-app-notes/documents/RP-003470-WP/Configuring-the-Compute-Module-4.pdf)

配置计算模块 4

计算模块 4 有多种不同的硬件配置。一些用例禁用不需要的某些功能。

本文档描述了如何禁用各种硬件和软件接口。

### 计算模块 4 IO 板数据表

设计数据可以在计算模块 4 IO 板（CM4IO）的数据表中找到：

* [CM4IO 数据表](https://datasheets.raspberrypi.com/cm4io/cm4io-datasheet.pdf)

我们还为 CM4 IO 板提供 KiCad PCB 设计套件：

* [CM4IO KiCad 文件](https://datasheets.raspberrypi.com/cm4io/CM4IO-KiCAD.zip)

### 计算模块 4S 数据表

计算模块 4S（CM4S）在 CM1、CM3 和 CM3+的 DDR2-SODIMM 尺寸中提供了 CM4 的内部组件。要了解有关 CM4S 的更多信息，请参阅以下文档：

* [CM4S 数据表](https://datasheets.raspberrypi.com/cm4s/cm4s-datasheet.pdf)

### 计算模块 3+ 数据表

计算模块 3+ (CM3+) 是一款受支持的产品，其终止生命周期（EOL）日期不早于 2028 年 1 月。要了解有关 CM3+及其对应 IO 板的更多信息，请参阅以下文档：

* [CM3+ 数据表](https://datasheets.raspberrypi.com/cm/cm3-plus-datasheet.pdf)

### 计算模块 1 和计算模块 3 数据表

树莓派计算模块 1 (CM1) 和计算模块 3 (CM3) 是支持的产品，其终止生命周期 (EOL) 日期不早于 2026 年 1 月。要了解有关 CM1 和 CM3 的更多信息，请参阅以下文档：

* [CM1 和 CM3 数据表](https://datasheets.raspberrypi.com/cm/cm1-and-cm3-datasheet.pdf)
* [CM1 的原理图](https://datasheets.raspberrypi.com/cm/cm1-schematics.pdf)
* [CM3 的原理图](https://datasheets.raspberrypi.com/cm/cm3-schematics.pdf)

##### [从计算模块 1 和计算模块 3 过渡到计算模块 4](https://pip.raspberrypi.com/categories/685-whitepapers-app-notes/documents/RP-003469-WP/Transitioning-from-CM3-to-CM4.pdf)

从计算模块 1 和计算模块 3 过渡到计算模块 4

这份白皮书帮助开发人员从计算模块 1 和计算模块 3 迁移到计算模块 4。

### 计算模块 IO 板原理图

计算模块 IO 板（CMIO）为 CM1、CM3、CM3L 和 CM3+提供各种接口。计算模块 IO 板有两个衍生版本：版本 1 和版本 3。版本 1 仅兼容 CM1。版本 3 兼容 CM1、CM3、CM3+和 CM4S。计算模块 IO 板版本 3 有时被简写为 CMIO3。要了解有关 CMIO1 和 CMIO3 的更多信息，请参阅以下文档：

* [CMIO 的原理图](https://datasheets.raspberrypi.com/cmio/cmio-schematics.pdf)
* [CMIO Version 1.2（CMIO/CMIO1）的设计文档](https://datasheets.raspberrypi.com/cmio/RPi-CMIO-R1P2.zip)
* [CMIO Version 3.0（CMIO3）的设计文档](https://datasheets.raspberrypi.com/cmio/RPi-CMIO-R3P0.zip)

### 计算模块摄像头/显示适配板原理图

计算模块摄像头/显示适配板（CMCDA）为计算模块提供摄像头和显示接口。要了解有关 CMCDA 的更多信息，请参阅以下文档：

* [CMCDA 的原理图](https://datasheets.raspberrypi.com/cmcda/cmcda-schematics.pdf)
* [CMCDA Version 1.1 的设计文档](https://datasheets.raspberrypi.com/cmcda/RPi-CMCDA-1P1.zip)

### 欠压检测

以下原理图描述了用于旧款树莓派的欠压检测电路：

![Under-voltage detect](https://www.raspberrypi.com/documentation/computers/images/under_voltage_detect.png)
