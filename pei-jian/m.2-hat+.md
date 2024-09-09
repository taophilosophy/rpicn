# M.2 HAT+

## 关于

![树莓派 M.2 HAT+](https://www.raspberrypi.com/documentation/accessories/images/m2-hat-plus.jpg)

树莓派 M.2 HAT+

树莓派 M.2 HAT+ M 键（key）能让你把 M.2 外部设备（如 NVMe 存储设备和其他 PCIe 配件）转接到树莓派 5 的 PCIe 接口。

M.2 HAT+ 扩展板可把树莓派 5 上的 PCIe 接口同单个 M.2 M 键接口的设备进行转接。你可以连接使用 2230/2242 尺寸的设备。M.2 HAT+ 可提供高达 3A 的功率。

M.2 HAT+ 遵守树莓派 HAT+ 规范，树莓派系统可自动检测 HAT+ 及其连接的设备。

附带的螺纹间隔柱提供了充足的空间，可在 M.2 HAT+ 下方安装树莓派主动散热器。

M.2 HAT+ 仅兼容树莓派 5 的树莓派外壳（需要你移除盖子和附带的风扇）。

## 特点

* 单通道 PCIe 2.0 接口（500 MB/s 峰值传输速率）
* 支持使用 M.2 M 键接口的设备
* 支持 2230/2242 尺寸的设备
* 为接入的 M.2 设备提供高达 3A 的电流
* 电源和状态指示灯
* 符合树莓派 HAT+ 规范
* 包含:
  * 连接线
  * 16 mm GPIO 堆叠排针
  * 4 个螺纹间隔柱
  * 8 颗螺丝
  * 1 个带有花纹的双凸缘固态硬盘配件螺丝（用于固定和支撑 M.2 外围设备）

## 安装

要使用树莓派 M.2 HAT+，你需要：

* 树莓派 5

每份 M.2 HAT+ 都配备了排线、GPIO 堆叠排针和要安装的硬件。请按照以下说明来完成 M.2 HAT+ 的安装：

1. 首先，请确保你的树莓派运行的是最新软件。运行以下命令，进行更新：

    ```bash
    $ sudo apt update && sudo apt full-upgrade
    ```
2. 接下来，请确保你的树莓派固件也是最新的。运行以下命令查看你正在运行的固件版本：

    ```bash
    $ sudo rpi-eeprom-update
    ```

    如果你看到的日期是 2023 年 12 月 6 日及更晚，请继续下一步。如果你看到的日期早于 2023 年 12 月 6 日，请运行以下命令打开树莓派配置 CLI：

    ```bash
    $ sudo raspi-config
    ```

    在 **Advanced Options** 下 > **Bootloader Version**，选择 **Latest**。然后，点击 **Finish** 或 **Esc 键** 退出 raspi-config。

    运行以下命令以将固件更新到最新版本：

    ```bash
    $ sudo rpi-eeprom-update -a
    ```

    然后，使用 `sudo reboot` 重启。
3. 在开始安装之前，请断开树莓派的电源。
4. M.2 HAT+ 兼容于树莓派 5 主动散热器。如果你有主动散热器，请在安装 M.2 HAT+ 之前先安装散热器。
5. 使用提供的四颗螺丝安装间隔柱。将 GPIO 堆叠排针牢固地压在树莓派的 GPIO 引脚上；只要所有引脚都能正确插入即可，方向并不重要。将扁平带状线缆从 M.2 HAT+ 上拔下，并将另一端插入树莓派的 PCIe 接口。从两侧抬起扁平带状线缆固定器，然后将带有铜触点朝向内部、即朝向 USB 的线缆插入。确保扁平带状线缆完全且均匀地插入 PCIe 接口，然后从两侧向下按紧线缆固定器，将扁平带状线缆牢固地固定在位。
6. 把 M.2 HAT+ 放在螺柱上面，然后使用剩下的四颗螺丝将其固定在位。
7. 把排线插入 M.2 HAT+ 上的插槽。从两侧抬起排线固定器，然后插入铜触点朝上的电缆。将排线完全均匀地插入端口，从两侧向下推动电缆固定器，将排线牢固地固定在位。
8. 通过逆时针旋转螺丝来取下驱动附件螺丝。将你的 M.2 固态硬盘插入 M.2 键接口，将固态硬盘以轻微向上的角度滑入插槽。不要强行将固态硬盘插入插槽：而应轻轻地滑入。
9. 将固态硬盘附件螺丝上的凹口推入 M.2 固态硬盘尾部的插槽中。将固态硬盘平放在 M.2 HAT+ 上，并顺时针旋转螺丝，直到固态硬盘固定。不要太过紧拧螺丝。
10. 恭喜，你已成功的安装了 M.2 HAT+。现在把你的树莓派接入电源；树莓派系统能自动检测到 M.2 HAT+。如果你使用桌面版树莓派系统，你应该能在桌面上看到代表硬盘的图标。如果你不使用桌面版，你可以在 `/dev/nvme0n1` 找到硬盘。要使硬盘自动可用于文件访问，请考虑配置自动挂载。

![安装树莓派 M.2 HAT+](https://www.raspberrypi.com/documentation/accessories/images/m2-hat-plus-installation-07.png)

>**警告**
>
> 在连接/断开 M.2 插槽上的设备之前，务必将树莓派断开电源。

## 从 NVMe 启动

要从连接到 M.2 HAT+ 的 NVMe 存储设备启动，请完成以下步骤：

1. 使用树莓派启动盘制作工具格式化你的 NVMe 存储设备。如果你已经有带有树莓派系统镜像的存储卡，可以在你的树莓派上执行此操作。
2. 使用存储卡或 USB 存储设备将树莓派启动到树莓派系统，以持久性更改板载 EEPROM 配置中的引导顺序。
3. 在树莓派终端上运行 `sudo raspi-config` 以打开树莓派配置 CLI。
4. 在 **Advanced Options** > **Boot Order** 下，选择 **NVMe/USB boot**。然后，点击 **Finish**  或按 **Esc 键** 退出 `raspi-config`。
5. 使用 `sudo reboot` 重启你的树莓派。

要获取更多信息，请参阅 NVMe 启动。

## 启用 PCIe Gen 3

>**警告**
>
> 树莓派 5 未获 Gen 3.0 速度认证。PCIe Gen 3.0 连接可能不稳定。

要启用 PCIe Gen 3 速度，请按照在启用 PCIe Gen 3.0 中的说明操作。

## 框图

![树莓派 M.2 HAT+ 原理图](https://www.raspberrypi.com/documentation/accessories/images/m2-hat-plus-schematics.png)


[PDF 格式](https://datasheets.raspberrypi.com/m2-hat-plus/raspberry-pi-m2-hat-plus-schematics.pdf?_gl=1*1qlaav3*_ga*ODAwMTM3MTg4LjE3MTc1NzY1NTQ.*_ga_22FD70LWDS*MTcyMzcwMjM3Ny44NC4xLjE3MjM3MDI0MTAuMC4wLjA.)的原理图。

## 产品简介

更多有关 M.2 HAT+ 的信息，如机械规格和操作环境限制，请参阅产品简介。
