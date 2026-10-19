# M.2 HAT+

## 关于

![树莓派 M.2 HAT+](https://www.raspberrypi.com/documentation/accessories/images/m2-hat-plus.jpg)

![树莓派 M.2 HAT+ Compact 装在树莓派外壳中](https://www.raspberrypi.com/documentation/accessories/images/m2-hat-plus-compact-with-case.jpg)

树莓派 M.2 HAT+ M 键（M Key）和 M.2 HAT+ Compact M 键可以让你把 M.2 外部设备（如 NVMe 存储设备和其他 PCIe 配件）连接到树莓派 5 的 PCIe 接口。

M.2 HAT+ 和 M.2 HAT+ Compact 转接板可在树莓派 5 上的 PCIe 接口与单个 M.2 M 键边型连接器之间进行转换。M.2 HAT+ 支持任何使用 2230 或 2242 外形尺寸的设备；M.2 HAT+ Compact 支持任何使用 2230 外形尺寸的设备。

M.2 HAT+ 提供标准版和 Compact 版两种形式，各自适用于不同的使用场景。

* M.2 HAT+ 附带螺纹间隔柱，可在其下方为树莓派主动散热器留出充足的空间。不过，只有在移除盖子和附带的风扇后，它才兼容[树莓派 5 的树莓派外壳](https://www.raspberrypi.com/products/raspberry-pi-5-case/)。
* M.2 HAT+ Compact 的设计可以绕开[树莓派 5 的树莓派外壳](https://www.raspberrypi.com/products/raspberry-pi-5-case/)中附带的风扇。不过，它下方无法安装主动散热器。

M.2 HAT+ 和 M.2 HAT+ Compact 都符合[树莓派 HAT+ 规范](https://pip.raspberrypi.com/documents/RP-008281-DS)，这使得树莓派系统能够自动检测 HAT+ 及其连接的任何设备。

## 特点

M.2 HAT+ 和 M.2 HAT+ Compact 都具备以下特点：

* 单通道 PCIe 2.0 接口（峰值传输速率 500 MB/s）
* 支持使用 M.2 M 键边型连接器的设备
* 为接入的 M.2 设备提供高达 3 A 的电流
* 电源和活动指示灯

M.2 HAT+ 和 M.2 HAT+ Compact 的不同之处如下：

* M.2 HAT+ 支持 2230 或 2242 外形尺寸的设备；M.2 HAT+ Compact 仅支持 2230 外形尺寸。

### 硬件

树莓派 M.2 HAT+ 或 M.2 HAT+ Compact 的包装盒内含以下部件：

* 排线
* 螺纹间隔柱
* 螺丝
* 1 颗带滚花的双凸缘驱动器固定螺丝，用于固定和支撑 M.2 外部设备

M.2 HAT+ 还附带一个 16 mm GPIO 堆叠排针；M.2 HAT+ Compact 不含此部件。

要使用 M.2 HAT+ 或 M.2 HAT+ Compact，你还需要：

* 树莓派 5

## 准备你的树莓派

1. 确保你的树莓派运行的是最新软件。运行以下命令进行更新：

    ```bash
    $ sudo apt update && sudo apt full-upgrade
    ```
2. [确保你的树莓派固件是最新的](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#update-the-bootloader-configuration)。运行以下命令查看你正在运行的固件版本：

    ```bash
    $ sudo rpi-eeprom-update
    ```

    如果你看到的日期是 2023 年 12 月 6 日及更晚，请继续下一步。如果你看到的日期早于 2023 年 12 月 6 日，请运行以下命令打开树莓派配置 CLI：

    ```bash
    $ sudo raspi-config
    ```

    在 `Advanced Options` > `Bootloader Version` 下，选择 `Latest`。然后，使用 `Finish` 或 **Escape** 键退出 `raspi-config`。

    运行以下命令以将固件更新到最新版本：

    ```bash
    $ sudo rpi-eeprom-update -a
    ```

    然后，使用 `sudo reboot` 重启。
3. 在开始安装之前，请断开树莓派的电源。

## 安装 M.2 HAT+

按照以下步骤安装 M.2 HAT+。如果要安装 M.2 HAT+ Compact，请参阅[安装 M.2 HAT+ Compact](#安装-m2-hat-compact)。

### （可选）安装主动散热器

1. M.2 HAT+ 兼容树莓派 5 主动散热器。如果你有主动散热器，请在安装 M.2 HAT+ 之前先安装散热器。

    ![安装主动散热器](https://www.raspberrypi.com/documentation/accessories/images/m2-hat-plus-installation-01.png)

### 安装固定硬件

1. 使用随附的螺丝安装间隔柱。
2. 将 GPIO 堆叠排针牢固地压在树莓派 GPIO 引脚顶部。方向并不重要，但所有引脚都必须完全插到位。
3. 在断开排线之前，从两侧轻轻抬起 M.2 HAT+ 上的排线固定器。
4. 从两侧抬起树莓派 PCIe 接口上的排线固定器，然后将排线以金属触点朝向 USB 接口的方向插入。
5. 将排线完全且均匀地插入 PCIe 接口后，从两侧向下按压排线固定器，将排线牢固地固定到位。

    ![安装固定硬件](https://www.raspberrypi.com/documentation/accessories/images/m2-hat-plus-installation-02.png)

### 安装转接板

1. 将 M.2 HAT+ 放在间隔柱上，使用剩余的螺丝将其固定到位。

    ![安装转接板](https://www.raspberrypi.com/documentation/accessories/images/m2-hat-plus-installation-03.png)

2. 将排线插入 M.2 HAT+ 上的插槽。

    从两侧抬起排线固定器，然后将排线以铜触点朝上的方向插入。将排线完全且均匀地插入接口后，从两侧向下按压排线固定器，将排线牢固地固定到位。

    ![插入排线](https://www.raspberrypi.com/documentation/accessories/images/m2-hat-plus-installation-04.png)

### 安装你的 M.2 存储设备

1. 逆时针旋转螺丝，取下驱动器固定螺丝。将你的 M.2 固态硬盘插入 M.2 键边型连接器，以轻微向上的角度将存储设备滑入插槽。不要强行将存储设备插入插槽：它应该能轻轻滑入。

    ![安装 M.2 存储设备](https://www.raspberrypi.com/documentation/accessories/images/m2-hat-plus-installation-05.png)

2. 将驱动器固定螺丝上的凹口推入你的 M.2 存储设备尾部的插槽。将存储设备平放贴紧 M.2 HAT+，然后顺时针旋转拧入 SSD 固定螺丝，直到感觉到 SSD 已固定。不要过度拧紧螺丝。

    ![固定 M.2 存储设备](https://www.raspberrypi.com/documentation/accessories/images/m2-hat-plus-installation-06.png)

恭喜，你已成功安装 M.2 HAT+。

![已安装的 M.2 HAT+](https://www.raspberrypi.com/documentation/accessories/images/m2-hat-plus-installation-07.png)

## 安装 M.2 HAT+ Compact

按照以下步骤安装 M.2 HAT+ Compact。如果要安装 M.2 HAT+，请参阅[安装 M.2 HAT+](#安装-m2-hat)。

### 安装固定硬件

1. 使用随附的螺丝安装间隔柱。

    ![安装固定硬件](https://www.raspberrypi.com/documentation/accessories/images/m2-hat-plus-compact-installation-02.png)

### 安装转接板

1. 将 M.2 HAT+ Compact 放在间隔柱上，使用剩余的螺丝将其固定到位。

    ![安装转接板](https://www.raspberrypi.com/documentation/accessories/images/m2-hat-plus-compact-installation-03.png)

2. 将排线插入树莓派的 PCIe 接口。

    从两侧抬起排线固定器，然后将排线以铜触点朝内、朝向 USB 接口的方向插入。将排线完全且均匀地插入 PCIe 接口后，从两侧向下按压排线固定器，将排线牢固地固定到位。

    ![插入排线](https://www.raspberrypi.com/documentation/accessories/images/m2-hat-plus-compact-installation-04.png)

### 安装你的 M.2 存储设备

1. 逆时针旋转螺丝，取下驱动器固定螺丝。将你的 M.2 固态硬盘插入 M.2 键边型连接器，以轻微向上的角度将存储设备滑入插槽。不要强行将存储设备插入插槽：它应该能轻轻滑入。

    ![安装 M.2 存储设备](https://www.raspberrypi.com/documentation/accessories/images/m2-hat-plus-compact-installation-05.png)

2. 将驱动器固定螺丝上的凹口推入你的 M.2 存储设备尾部的插槽。将存储设备平放贴紧 M.2 HAT+ Compact，然后顺时针旋转拧入 SSD 固定螺丝，直到感觉到 SSD 已固定。不要过度拧紧螺丝。

    ![固定 M.2 存储设备](https://www.raspberrypi.com/documentation/accessories/images/m2-hat-plus-compact-installation-06.png)

恭喜，你已成功安装 M.2 HAT+ Compact。

![已安装的 M.2 HAT+ Compact](https://www.raspberrypi.com/documentation/accessories/images/m2-hat-plus-compact-installation-07.png)

## 启动你的树莓派

如果你的 NVMe 存储设备是新的或未经格式化的，它不会作为图标显示在树莓派系统桌面上。此外，`sudo blkid` 等命令也不会显示分区 UUID。你必须对存储设备进行分区和格式化（例如，使用[树莓派启动盘制作工具](https://www.raspberrypi.com/software/)中的 **Erase** 选项），才能让它对操作系统可见并可供访问。更多信息，请参阅[从 NVMe 启动](#从-nvme-启动)或[自动挂载存储设备](../shu-mei-pai/xi-tong-pei-zhi.md#自动挂载存储设备)。

1. 将你的树莓派连接电源。树莓派系统会自动检测 M.2 HAT+ 或 M.2 HAT+ Compact。

    * 要验证硬件是否被检测到，请打开终端并运行：

        ```bash
        $ ls -l /dev/nvme*
        ```

        如果存储设备被正确检测到，你会看到 `/dev/nvme0` 和 `/dev/nvme0n1`。

    * 如果你计划从该存储设备启动，请参阅[从 NVMe 启动](#从-nvme-启动)。树莓派启动盘制作工具会在安装过程中自动对存储设备进行分区和格式化。
    * 如果你计划将存储设备纯粹用作额外存储，请在[配置自动挂载](../shu-mei-pai/xi-tong-pei-zhi.md#自动挂载存储设备)之前对存储设备进行格式化。

2. 要让你的存储设备自动可用于文件访问，请考虑[配置自动挂载](../shu-mei-pai/xi-tong-pei-zhi.md#自动挂载存储设备)。

>**警告**
>
> 在连接或断开 M.2 插槽上的设备之前，务必先断开树莓派的电源。

## 从 NVMe 启动

要从连接到 M.2 HAT+ 或 M.2 HAT+ Compact 的 NVMe 存储设备启动，请完成以下步骤：

1. 使用树莓派启动盘制作工具将树莓派系统刷写到你的 NVMe 存储设备。更多信息，请参阅[安装树莓派系统](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html)。

    * 如果你的树莓派已经在使用存储卡上的树莓派系统，可以直接在你的树莓派上运行树莓派启动盘制作工具，并选择 NVMe 存储设备作为目标存储。
    * 或者，如果你的引导加载程序固件是最新的，可以使用树莓派网络安装程序（Raspberry Pi Network Installer）通过以太网连接下载并运行树莓派启动盘制作工具，而无需存储卡。更多信息，请参阅[网络安装](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#network-installation)。

2. 重启你的树莓派。

    * 如果你的树莓派 5 中没有插入存储卡，它会自动从 NVMe 存储设备启动。
    * 如果你的树莓派 5 中插入了存储卡，它会先尝试从存储卡启动。你可以通过完成以下步骤来更改树莓派上的启动顺序：

        1. 使用存储卡将你的树莓派启动到树莓派系统。
        2. 在树莓派上的终端中运行 `sudo raspi-config`，打开树莓派配置 CLI。
        3. 在 **Advanced Options** > **Boot Order** 下，选择 **NVMe/USB boot**。
        4. 使用 `Finish` 或 **Escape** 键退出 `raspi-config`。
        5. 使用 `sudo reboot` 重启你的树莓派。

要了解有关 NVMe 启动的详细信息，请参阅 [NVMe 启动](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#nvme-boot)。

## 启用 PCIe Gen 3

>**警告**
>
> 树莓派 5 未通过 Gen 3.0 速度认证。PCIe Gen 3.0 连接可能不稳定。

要启用 PCIe Gen 3 速度，请按照[启用 PCIe Gen 3.0](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#pcie-gen-3-0)中的说明操作。

## 原理图

M.2 HAT+ 的原理图以 [PDF](https://pip.raspberrypi.com/documents/RP-008218-DS) 格式提供。

## 产品简介

要了解更多有关 M.2 HAT+ 和 M.2 HAT+ Compact 的信息（包括机械规格和工作环境限制），请参阅[产品简介](https://pip.raspberrypi.com/documents/RP-009234-MM)。
