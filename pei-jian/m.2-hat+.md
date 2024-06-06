# M.2 HAT+

## 关于

![m2 hat plus](https://www.raspberrypi.com/documentation/accessories/images/m2-hat-plus.jpg)

树莓派 M.2 HAT+

树莓派 M.2 HAT+ M Key 可让您将 M.2 外围设备（如 NVMe 存储设备和其他 PCIe 配件）转接到树莓派 5 的 PCIe 接口。

M.2 HAT+ 扩展板可把树莓派 5 上的 PCIe 接口同单个 M.2 M key 接口的设备进行转接。您可以连接使用 2230 或 2242 尺寸的设备。M.2 HAT+ 可提供高达 3A 的功率。

M.2 HAT+ 使用树莓派的 HAT+ 规范，Raspberry Pi OS 可自动检测 HAT+ 及其连接的设备。

附带的螺纹间隔柱提供了充足的空间，以便在 M.2 HAT+ 下安装树莓派主动散热器。

M.2 HAT+ 仅兼容树莓派 5 的树莓派外壳（需要您移除盖子和附带的风扇）。

## 特点

* 单通道 PCIe 2.0 接口（500 MB/s 峰值传输速率）
* 支持使用 M.2 M Key 接口的设备
* 支持 2230 或 2242 尺寸的设备
* 为连接的 M.2 设备提供高达 3A 的电流
* 电源和状态指示灯
* 符合树莓派 HAT+ 规范
* 包含:
  * 连接线缆
  * 16 毫米 GPIO 堆叠排针
  * 4 个螺纹间隔柱
  * 8 颗螺丝
  * 1 个带有花纹的双凸缘 SSD 配件螺丝（用于固定和支撑 M.2 外围设备）

## 安装

要使用树莓派 M.2 HAT+，您需要：

* 树莓派 5

每个 M.2 HAT+ 都配备了排线、GPIO 堆叠头和安装硬件。请按照以下说明来完成 M.2 HAT+ 的安装：

1. 首先，请确保您的树莓派运行的是最新软件。运行以下命令进行更新：

    ```
    $ sudo apt update && sudo apt upgrade
    ```
2. 接下来，请确保您的树莓派固件也是最新的。运行以下命令查看您正在运行的固件版本：

    ```
    $ sudo rpi-eeprom-update
    ```

    如果您看到的日期是 2023 年 12 月 6 日或更晚，请继续下一步。如果您看到的日期早于 2023 年 12 月 6 日，请运行以下命令打开树莓派配置 CLI：

    ```
    $ sudo raspi-config
    ```

    在 Advanced Options 下 > Bootloader Version ，选择 Latest 。然后，使用 Finish 键或 Escape 键退出 raspi-config 。

    运行以下命令以将固件更新到最新版本：

    ```
    $ sudo rpi-eeprom-update -a
    ```

    然后，使用 sudo reboot 重启。
3. 在开始安装之前，请断开树莓派的电源。
4. M.2 HAT+ 兼容树莓派 5 主动散热器。如果您有主动散热器，请在安装 M.2 HAT+ 之前先安装散热器。
5. 使用提供的四颗螺丝安装间隔柱。将 GPIO 堆叠排针牢固地压在树莓派的 GPIO 引脚上；只要所有引脚都能正确插入即可，方向并不重要。将 Ribbon 线缆从 M.2 HAT+上拔下，并将另一端插入树莓派的 PCIe 接口。从两侧抬起 Ribbon 线缆固定器，然后将带有铜接点朝向内部、朝向 USB 的线缆插入。确保 Ribbon 线缆完全且均匀地插入 PCIe 接口，然后从两侧向下按紧线缆固定器，将 Ribbon 线缆牢固地固定在位。
6. 把 M.2 HAT+ 放在螺柱上面，并使用剩下的四颗螺丝将其固定在位。
7. 把排线插入 M.2 HAT+ 上的插槽。从两侧抬起排线固定器，然后插入铜接点朝上的电缆。将排线完全均匀地插入端口，从两侧向下推动电缆固定器，将排线牢固地固定在位。
8. 通过逆时针旋转螺丝来取下驱动附件螺丝。将您的 M.2 SSD 插入 M.2 key 接口，将 SSD 以轻微向上的角度滑入插槽。不要强行将 SSD 插入插槽：而应轻轻地滑入。
9. 将 SSD 附件螺丝上的凹口推入 M.2 SSD 尾部的插槽中。将 SSD 平放在 M.2 HAT+ 上，并顺时针旋转螺丝，直到 SSD 固定。不要太过紧拧螺丝。
10. 恭喜，您已成功的安装了 M.2 HAT+。现在把您的树莓派接入电源；Raspberry Pi OS 能自动检测到 M.2 HAT+。如果您使用 Raspberry Pi Desktop，您应该在桌面上看到代表硬盘的图标。如果您不使用桌面版，您可以在 /dev/nvme0n1 找到硬盘。要使硬盘自动可用于文件访问，请考虑配置自动挂载。![m2 hat plus installation 07](https://www.raspberrypi.com/documentation/accessories/images/m2-hat-plus-installation-07.png)

>**警告**
>
>在连接或断开 M.2 插槽上的设备之前，务必将树莓派断开电源。 

## 从 NVMe 启动

要从连接到 M.2 HAT+ 的 NVMe 存储设备启动，请完成以下步骤：

1. 使用 Raspberry Pi Imager 格式化您的 NVMe 存储设备。如果您已经有带有 Raspberry Pi OS 镜像的 SD 卡，可以在您的树莓派上执行此操作。
2. 使用 SD 卡或 USB 存储设备将树莓派启动到 Raspberry Pi OS，以持久性更改板载 EEPROM 配置中的引导顺序。
3. 在树莓派终端上运行 sudo raspi-config 以打开树莓派配置 CLI。
4. 在 Advanced Options > Boot Order 下，选择 NVMe/USB boot 。然后，使用 Finish 或 Esc 键退出 raspi-config 。
5. 使用 sudo reboot 重启您的树莓派。

要获取更多信息，请参阅 NVMe 启动。

## 启用 PCIe Gen 3

>**警告**
>
>树莓派 5 未经 Gen 3.0 速度认证。PCIe Gen 3.0 连接可能不稳定。 

要启用 PCIe Gen 3 速度，请按照在启用 PCIe Gen 3.0 中的说明操作。

## 框图

![m2 hat plus schematics](https://www.raspberrypi.com/documentation/accessories/images/m2-hat-plus-schematics.png)

树莓派 M.2 HAT+ 的原理图

PDF 格式的原理图。

## 产品简介

有关 M.2 HAT+ 的更多信息，包括机械规格和操作环境限制，请参阅产品简介。
