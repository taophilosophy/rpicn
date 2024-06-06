# 人工智能套件（AI Kit）

## 关于

![ai kit](https://www.raspberrypi.com/documentation/accessories/images/ai-kit.jpg)

树莓派 AI 套件

树莓派 AI 套件将树莓派 M.2 HAT+ 与 Hailo AI 加速模块捆绑在一起，可用于树莓派 5。该套件包含以下内容：

* Hailo AI 模块包含神经处理单元（NPU）
* 树莓派 M.2 HAT+，用于将 AI 模块接入您的树莓派 5
* 模块和 M.2 HAT+ 之间预装了导热垫
* 安装硬件套件
* 16 毫米堆叠 GPIO 引脚

## AI 模块功能

* 每秒 13 万亿次（TOPS）神经网络推理加速器，构建在 Hailo-8L 芯片周围。
* M.2 2242 形态因子

## 安装

要使用 Ai 套件，您需要：

* 树莓派 5

每个 Ai 套件都配备了预安装的 Ai 模块、排线电缆、GPIO 堆叠排针和安装硬件。请按照以下说明完成安装您的 Ai 套件：

1. 首先，请确保您的树莓派运行的软件是最新的。运行以下命令进行更新：

    ```
    $ sudo apt update && sudo apt full-upgrade
    ```
2. 接下来，请确保您的树莓派固件是最新的。运行以下命令查看您正在运行的固件版本：

    ```
    $ sudo rpi-eeprom-update
    ```

    如果您看到的日期是 2023 年 12 月 6 日或更晚，请继续下一步。如果您看到的日期早于 2023 年 12 月 6 日，请运行以下命令打开树莓派配置 CLI：

    ```
    $ sudo raspi-config
    ```

    在 Advanced Options > Bootloader Version 下，选择 Latest 。然后，使用 Finish 键或 Escape 键退出 raspi-config 。

    运行以下命令以将固件更新到最新版本：

    ```
    $ sudo rpi-eeprom-update -a
    ```

    然后，使用 sudo reboot 重新启动。
3. 在开始安装前，请断开树莓派的电源。
4. 为了获得最佳性能，我们建议将 Ai 套件与树莓派主动散热器一起使用。如果您有主动散热器，请在安装 Ai 套件之前安装它。![ai kit installation 01](https://www.raspberrypi.com/documentation/accessories/images/ai-kit-installation-01.png)
5. 使用提供的四颗螺丝安装间隔柱。牢固地将 GPIO 堆叠排针压在树莓派的 GPIO 引脚顶部；只要所有引脚都能正确插入即可，方向无所谓。从 Ai 套件上断开排线电缆，并将另一端插入树莓派的 PCIe 接口。从两侧抬起排线电缆固定器，然后将带有铜接点朝向内部、朝向 USB 接口的线缆插入。确保排线电缆完全且均匀地插入 PCIe 接口，然后从两侧按下电缆固定器，将排线电缆牢固地固定在位。![ai kit installation 02](https://www.raspberrypi.com/documentation/accessories/images/ai-kit-installation-02.png)
6. 将 AI 套件放在间隔物顶部，并使用剩下的四颗螺丝将其固定在位。![ai kit installation 03](https://www.raspberrypi.com/documentation/accessories/images/ai-kit-installation-03.png)
7. 将排线插入 AI 套件上的插槽。从两侧抬起排线固定器，然后插入铜接点朝上的电缆。将排线完全均匀地插入接口，从两侧按下电缆固定器，牢固地固定排线电缆。![ai kit installation 04](https://www.raspberrypi.com/documentation/accessories/images/ai-kit-installation-04.png)
8. 恭喜，现在您已成功的安装 AI 套件了。将您的树莓派接入电源；Raspberry Pi OS 可自动检测 AI 套件。![ai kit installation 05](https://www.raspberrypi.com/documentation/accessories/images/ai-kit-installation-05.png)

>**警告**
>
>在连接或断开 M.2 插槽上的设备之前，务必先将您的树莓派断开电源。 

## 入门指南

本指南将帮助您设置树莓派 5 与树莓派 AI 套件配合使用。这将使您能够使用 Hailo AI 神经网络加速器运行 rpicam-apps 摄像头演示。

### 先决条件

对于本指南，您将需要以下内容：

* 树莓派 5
* 树莓派 Ai 套件，其中包括：
  * M.2 HAT+
  * 预装的 Hailo-8L Ai 模块
* 64 位 Raspberry Pi OS Bookworm 系统
* 官方树莓派摄像头（例如摄像头模块 3 或高质量摄像头）

### 硬件设置

1. 将摄像头连接到您的树莓派 5 主板，按照在安装树莓派摄像头中的说明进行操作。您可以跳过电源连接，因为您需要在下一步中断开树莓派的电源。
2. 按照安装说明将您的 AI 套件硬件连接到您的树莓派 5。
3. 按照说明启用 PCIe Gen 3.0。这一步骤是可选的，但为了使您的 AI 套件获得最佳性能，强烈建议启用它。
4. 安装使用 Ai 套件所需的依赖包。在终端运行以下命令：

    ```
    $ sudo apt install hailo-all
    ```

    这将安装以下依赖项：

    * Hailo 内核设备驱动程序和固件
    * HailoRT 中间件软件
    * Hailo Tappas 核心后处理库
    * rpicam-apps Hailo 后处理软件演示阶段
5. 最后，使用 sudo reboot 重启您的树莓派，以使这些设置生效。
6. 为确保一切正常运行，请运行以下命令：

    ```
    $ hailortcli fw-control identify
    ```

    如果您看到类似以下内容的输出，则已成功安装了 Ai 套件及其软件依赖包：

    ```
    Executing on device: 0000:01:00.0
    Identifying board
    Control Protocol Version: 2
    Firmware Version: 4.17.0 (release,app,extended context switch buffer)
    Logger Version: 0
    Board Name: Hailo-8
    Device Architecture: HAILO8L
    Serial Number: HLDDLBB234500054
    Part Number: HM21LB1C2LAE
    Product Name: HAILO-8L AI ACC M.2 B+M KEY MODULE EXT TMP
    ```

    另外，您可以运行 `dmesg | grep -i hailo` 来查看内核日志，应该会产生类似以下的输出：

    ```
    [    3.049657] hailo: Init module. driver version 4.17.0
    [    3.051983] hailo 0000:01:00.0: Probing on: 1e60:2864...
    [    3.051989] hailo 0000:01:00.0: Probing: Allocate memory for device extension, 11600
    [    3.052006] hailo 0000:01:00.0: enabling device (0000 -> 0002)
    [    3.052011] hailo 0000:01:00.0: Probing: Device enabled
    [    3.052028] hailo 0000:01:00.0: Probing: mapped bar 0 - 000000000d8baaf1 16384
    [    3.052034] hailo 0000:01:00.0: Probing: mapped bar 2 - 000000009eeaa33c 4096
    [    3.052039] hailo 0000:01:00.0: Probing: mapped bar 4 - 00000000b9b3d17d 16384
    [    3.052044] hailo 0000:01:00.0: Probing: Force setting max_desc_page_size to 4096 (recommended value is 16384)
    [    3.052052] hailo 0000:01:00.0: Probing: Enabled 64 bit dma
    [    3.052055] hailo 0000:01:00.0: Probing: Using userspace allocated vdma buffers
    [    3.052059] hailo 0000:01:00.0: Disabling ASPM L0s
    [    3.052070] hailo 0000:01:00.0: Successfully disabled ASPM L0s
    [    3.221043] hailo 0000:01:00.0: Firmware was loaded successfully
    [    3.231845] hailo 0000:01:00.0: Probing: Added board 1e60-2864, /dev/hailo0
    ```
7. 为了确保摄像头正常运行，请运行以下命令：

    ```
    $ rpicam-hello -t 10s
    ```

    这将启动摄像头并显示一个十秒钟的预览窗口。如果您已经验证一切安装正确，就该运行一些演示了。

### 演示

rpicam-apps 摄像头应用套件实现了一个后处理框架。本节包含一些演示后处理阶段，突出了 Ai 套件的一些功能。

以下演示使用 rpicam-hello ，默认情况下显示一个预览窗口。但是，您也可以使用其他 rpicam-apps ，包括 rpicam-vid 和 rpicam-still 。您可能需要添加或修改一些命令行选项，以使演示命令与替代应用程序兼容。

要开始，请下载演示所需的后处理 JSON 文件。这些文件确定要运行的后处理阶段，并配置每个阶段的行为。例如，您可以在对象检测演示中启用、禁用、加强或减弱时间滤波的强度。或者您可以在分割演示中启用或禁用输出蒙版绘制。

要下载完整的后处理 JSON 文件集合，请克隆 rpicam-apps 存储库。运行以下命令仅拉取存储库中最新的提交，以节省空间：

```
$ git clone --depth 1 https://github.com/raspberrypi/rpicam-apps.git ~/rpicam-apps
```

>**技巧**
>
>后续部分提供的命令使用此存储库中的 JSON 文件。为了便于引用这些文件，此命令在您的主文件夹中创建了克隆的 rpicam-apps 目录。如果您修改了此目录的位置，则还必须修改下面的演示命令，以引用 JSON 文件的新位置。


#### 目标检测

此演示显示神经网络检测到的物体周围的边界框。要禁用取景器，请使用参数 `-n`。要返回纯文本输出，说明检测到的物体，请添加参数 `-v 2`。运行以下命令在您的树莓派上尝试演示：

```
$ rpicam-hello -t 0 --post-process-file ~/rpicam-apps/assets/hailo_yolov6_inference.json --lores-width 640 --lores-height 640
```

或者，您可以尝试另一个具有性能和效率上不同权衡的模型。

使用 Yolov8 模型运行演示，请运行以下命令：

```
$ rpicam-hello -t 0 --post-process-file ~/rpicam-apps/assets/hailo_yolov8_inference.json --lores-width 640 --lores-height 640
```

使用 YoloX 模型运行演示，请运行以下命令：

```
$ rpicam-hello -t 0 --post-process-file ~/rpicam-apps/assets/hailo_yolox_inference.json --lores-width 640 --lores-height 640
```

使用 Yolov5 人脸模型运行演示，请运行以下命令：

```
$ rpicam-hello -t 0 --post-process-file ~/rpicam-apps/assets/hailo_yolov5_personface.json --lores-width 640 --lores-height 640
```

#### 图像分割

此演示执行对象检测，并通过在取景器图像上绘制颜色掩模来对对象进行分割。运行以下命令在您的树莓派上尝试演示：

```
$ rpicam-hello -t 0 --post-process-file ~/rpicam-apps/assets/hailo_yolov5_segmentation.json --lores-width 640 --lores-height 640 --framerate 20
```

#### 姿势估计

此演示执行 17 点人体姿势估计，绘制连接检测点的线条。运行以下命令在您的树莓派上尝试演示：

```
$ rpicam-hello -t 0 --post-process-file ~/rpicam-apps/assets/hailo_yolov8_pose.json --lores-width 640 --lores-height 640
```

### 进一步资源

Hailo 还创建了一组演示，您可以在树莓派 5 上运行，可在 hailo-ai/hailo-rpi5-examples GitHub 存储库中找到。

您可以在 hailo-ai/hailo_model_zoo GitHub 存储库中找到 Hailo 广泛的模型库，其中包含大量神经网络。

查看 Hailo 社区论坛和开发者区，进一步讨论有关 Hailo 硬件和工具的内容。

## 产品简介

有关 Ai 套件的更多信息，包括机械规格和操作环境限制，请参阅产品简介。
