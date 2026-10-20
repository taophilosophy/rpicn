# 人工智能软件

本页提供在树莓派 5 上运行由 Hailo NPU 驱动的 AI 模型的说明。Hailo NPU 是专为运行神经网络设计的 AI 加速芯片；AI 工作不由树莓派设备的 CPU 完成，而由 NPU 更高效地处理。

你可以通过以下任一方式将 Hailo NPU 连接到树莓派 5：

* [树莓派人工智能套件（AI Kit）](../pei-jian/ren-gong-zhi-neng-tao-jian-ai-kit.md)，由预装 Hailo-8L NPU 的 M.2 HAT+ 组成。
* [树莓派 AI HAT+](../pei-jian/ai-hat.md)，板载 Hailo-8L NPU 或 Hailo-8 NPU。
* [树莓派 AI HAT+ 2](../pei-jian/ai-hat.md)，板载 Hailo-10H NPU。

>**注意**
>
>以上三种方式都可以在树莓派 5 上运行视觉 AI 模型。不过，AI Kit 已停止生产，因此对于新设计，我们推荐使用 AI HAT+ 或 AI HAT+ 2。

AI HAT+ 2 还允许你运行生成式 AI（GenAI）模型。使用 AI HAT+ 2，你可以：

* 运行大语言模型（LLM）。如果你有 AI HAT+ 2 并且想同时运行视觉 AI 模型和 LLM，请遵循两组说明：[在树莓派 5 上运行视觉 AI 模型](#在树莓派-5-上运行视觉-ai-模型)和[在树莓派 5 上运行 LLM](#在树莓派-5-上运行-llm仅-ai-hat-2)。
* 运行视觉语言模型（VLM）和其他 GenAI 任务。有关说明，请参阅 Hailo 的 GitHub 仓库：[hailo-apps](https://github.com/hailo-ai/hailo-apps)。

## 硬件前提

运行 AI 模型需要一台[树莓派 5](https://www.raspberrypi.com/products/raspberry-pi-5/)，安装[64 位树莓派系统](https://www.raspberrypi.com/software/operating-systems/)（Trixie），以及以下 Hailo AI 加速器（NPU）选项之一：

* 树莓派 AI HAT+ 或 AI HAT+ 2（推荐），两者均带有板载 Hailo 模块。有关这些配件的更多信息，请参阅 [AI HAT](../pei-jian/ai-hat.md)。
* 树莓派人工智能套件（AI Kit），包含预装 Hailo-8L AI 加速器的 M.2 HAT+。有关 AI Kit 的更多信息，请参阅[人工智能套件（AI Kit）](../pei-jian/ren-gong-zhi-neng-tao-jian-ai-kit.md)。

>**注意**
>
>AI Kit 已停止生产；对于新设计，我们推荐使用 AI HAT+ 或 AI HAT+ 2。

如果你想运行视觉 AI 模型，还需要一个受支持的摄像头，例如树莓派摄像头模块 3。我们建议在连接 AI 硬件之前先接好摄像头。有关说明，请参阅[安装树莓派摄像头](../pei-jian/she-xiang-tou.md#安装树莓派摄像头)。请跳过重新接通树莓派电源的步骤，因为下一步需要先断开树莓派的电源。

然后，根据你的 AI 硬件，按照说明将 [AI HAT](../pei-jian/ai-hat.md)（HAT+ 或 HAT+ 2）或 [AI Kit](../pei-jian/ren-gong-zhi-neng-tao-jian-ai-kit.md) 连接到树莓派 5。

接下来，按照[软件前提](#软件前提)中的说明启用 PCIe Gen 3.0（仅 AI Kit）、安装所需依赖项，并确认所有设置都正确无误。

## 软件前提

在树莓派 5 上运行视觉 AI 模型或 GenAI 模型之前，你必须配置所需的软件。总体而言，这包括以下任务，按顺序执行：

1. [启用 PCIe Gen 3.0](#启用-pcie-gen-30仅-ai-kit)。手动配置 PCIe 接口，使 Hailo NPU 能以全速通信。仅 AI Kit 需要此步骤。
2. [更新树莓派系统](#更新树莓派系统)。确保你的树莓派系统软件包完全更新。
3. [安装所需依赖项](#安装所需依赖项)。安装必要的软件依赖项，使操作系统（OS）和应用程序能够检测 Hailo NPU、与其通信并在其上运行 AI 模型。
4. [验证](#重启并验证)。验证你的 AI 硬件已被正确检测并准备就绪。

### 启用 PCIe Gen 3.0（仅 AI Kit）

如果你使用 AI Kit，我们强烈建议启用 PCIe Gen 3.0。对于 AI HAT+ 和 AI HAT+ 2，此设置会自动应用，可以跳过。

默认情况下，树莓派 5 的 PCIe 接口使用 Gen 2.0（5 GT/s）速度。为获得 NPU 的最佳性能，请使用以下任一方法启用 Gen 3.0（8 GT/s）速度：

* 通过配置命令行（CLI）工具（`raspi-config`）在树莓派 5 上启用 Gen 3.0。
* 更新配置文件（`config.txt`），使树莓派 5 上的 PCIe 接口以 PCIe Gen 3.0 速度运行。

有关此设置的更多信息，请参阅 [PCIe Gen 3.0](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#pcie-gen-3-0)。

**使用 raspi-config**

首先打开树莓派配置 CLI；在树莓派终端中运行以下命令：

```sh
$ sudo raspi-config
```

然后，在配置 CLI 中完成以下步骤：

1. 选择 **Advanced Options > PCIe Speed**。
2. 选择 **Yes** 以启用 PCIe Gen 3.0 模式。
3. 选择 **Finish** 退出配置 CLI。
4. 重启树莓派以使更改生效。你可以在终端中使用 **`sudo reboot`** 完成。

**使用 config.txt**

首先，以 root 用户打开配置文件（`/boot/firmware/config.txt`）。然后：

1. 在 `config.txt` 文件中添加以下行：

```ini
dtparam=pciex1_gen=3
```

2. 重启树莓派以使这些设置生效：

```sh
$ sudo reboot
```

### 更新树莓派系统

确保树莓派 5 运行的是安装有最新软件的树莓派系统 Trixie，并具有最新的树莓派固件：

```sh
$ sudo apt update
$ sudo apt full-upgrade -y
$ sudo rpi-eeprom-update -a
$ sudo reboot
```

更多信息，请参阅[更新软件](raspberry-pi-os.md#更新当前的树莓派软件)和[更新引导加载程序配置](../shu-mei-pai/shu-mei-pai-ying-jian.md#更新引导加载程序配置)。

### 安装所需依赖项

在将树莓派更新到最新的树莓派软件和固件后，使用 NPU 需要以下依赖项：

* Hailo 内核设备驱动和固件。
* Hailo RT 中间件软件。
* Hailo Tappas 核心后处理库。

这些依赖项的安装方式取决于你使用的 AI 硬件。请为你的 AI 硬件选择合适的安装选项：

>**注意**
>
>AI Kit 和 AI HAT+ 需要不同的软件包（`hailo-all`），而 AI HAT+ 2 需要 `hailo-h10-all`。这两个软件包不能共存。

**AI Kit 和 AI HAT+**

要为 AI Kit 或 AI HAT+ 安装所需依赖项，请打开树莓派终端并运行以下命令：

```sh
$ sudo apt install dkms
$ sudo apt install hailo-all
```

**AI HAT+ 2**

要为 AI HAT+ 2 安装所需依赖项，请打开树莓派终端并运行以下命令：

```sh
$ sudo apt install dkms
$ sudo apt install hailo-h10-all
```

### 重启并验证

安装所需依赖项后，你必须重启树莓派 5。你可以在树莓派终端中使用以下命令完成：

```sh
$ sudo reboot
```

树莓派 5 重新启动完成后，运行以下命令检查一切是否正常运行：

```sh
$ hailortcli fw-control identify
```

如果你看到类似以下的输出，说明你已成功安装 NPU 及其软件依赖项：

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

AI HAT+ 和 AI HAT+ 2 的 `Serial Number`、`Part Number` 和 `Product Name` 可能显示为 `<N/A>`。这是预期行为，不影响功能。

此外，你可以运行 `dmesg | grep -i hailo` 检查内核日志，预期输出类似以下内容：

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

## 在树莓派 5 上运行视觉 AI 模型

本节提供在树莓派 5 上设置 Hailo NPU 的指导，使摄像头应用程序能够在摄像头输入上运行实时 AI 任务，如目标检测。以下说明适用于 AI Kit、AI HAT+ 和 AI HAT+ 2。

### 第 1 步：安装摄像头依赖项

首先，你必须安装树莓派摄像头软件栈。`rpicam-apps` 软件包提供树莓派系统使用的摄像头实用工具，并包含视觉 AI 流水线所需的 Hailo 后处理软件演示阶段。

使用以下命令安装最新的 rpicam-apps 软件包：

```sh
$ sudo apt update && sudo apt install rpicam-apps
```

然后，运行以下命令确保摄像头正常工作：

```sh
$ rpicam-hello
```

这会启动摄像头并显示预览窗口五秒钟。如果预览窗口出现，说明摄像头设置正确。

### 第 2 步：运行实时视觉 AI 演示

验证一切安装正确后，你可以使用 `rpicam-apps` 摄像头软件运行摄像头 AI 演示。该软件使用[后处理框架](she-xiang-tou-ruan-jian.md#使用-rpicam-apps-进行后处理)实现 AI 演示；它使用预训练的神经网络，通过 NPU 对摄像头帧运行 AI 推理。

为展示 NPU 的部分能力，本节概述了一些演示，展示不同的模型和后处理阶段，例如在物体周围绘制边界框或在人体上绘制姿态线。结果显示在实时预览窗口上（默认），或在树莓派终端中显示为文本。

以下演示使用 [`rpicam-hello`](she-xiang-tou-ruan-jian.md#rpicam-hello)，但你也可以使用其他 rpicam-apps 应用，如用于视频录制的 [`rpicam-vid`](she-xiang-tou-ruan-jian.md#rpicam-vid) 和用于静态图像的 [`rpicam-still`](she-xiang-tou-ruan-jian.md#rpicam-still)。这些应用程序可能需要你添加或修改一些命令行选项才能兼容。

#### 目标检测

以下 `rpicam-apps` 演示使用 `rpicam-hello` 和不同的 YOLO 模型执行目标检测。每个演示都会在检测到的物体周围绘制边界框，并支持可选标志以修改输出，如 `-n` 关闭取景器、`-v 2` 仅显示文本输出。

不同演示在速度和准确性上有不同的取舍。运行以下命令在树莓派 5 上尝试每个演示：

| 模型 | 命令 | 后处理阶段 |
| ---- | ---- | ---------- |
| YOLOv6 | `rpicam-hello -t 0 --post-process-file /usr/share/rpi-camera-assets/hailo_yolov6_inference.json` | 目标检测。 |
| YOLOv8 | `rpicam-hello -t 0 --post-process-file /usr/share/rpi-camera-assets/hailo_yolov8_inference.json` | 目标检测。 |
| YOLOX | `rpicam-hello -t 0 --post-process-file /usr/share/rpi-camera-assets/hailo_yolox_inference.json` | 轻量快速的目标检测。 |
| YOLOv5 | `rpicam-hello -t 0 --post-process-file /usr/share/rpi-camera-assets/hailo_yolov5_inference.json` | 人体与人脸检测。 |

#### 图像分割

以下 `rpicam-apps` 演示使用 `rpicam-hello` 执行目标检测，然后通过在取景器图像上绘制颜色掩码来分割物体。运行以下命令在树莓派 5 上尝试该演示：

```sh
$ rpicam-hello -t 0 --post-process-file /usr/share/rpi-camera-assets/hailo_yolov5_segmentation.json --framerate 20
```

#### 姿态估计

以下 `rpicam-apps` 演示使用 `rpicam-hello` 执行 17 点人体姿态估计，绘制连接检测点的线条。运行以下命令在树莓派 5 上尝试该演示：

```sh
$ rpicam-hello -t 0 --post-process-file /usr/share/rpi-camera-assets/hailo_yolov8_pose.json
```

### AI Kit 与 AI HAT+ 的软件包版本

如果你想使用由特定版本 Hailo 工具链生成的 AI Kit 或 AI HAT+ 运行模型，必须确保使用兼容版本的 Hailo 软件包和设备驱动。如果版本不匹配，这些组件将无法正常工作。

首先，如果你之前曾用 `apt-mark` 固定过任何相关软件包，可能需要使用以下命令取消固定：

```sh
$ sudo apt-mark unhold hailo-tappas-core hailort hailo-dkms
```

然后你可以安装所需版本的软件包：

**4.19**

要安装 4.19 版本的 Hailo 神经网络工具，请运行以下命令：

```sh
$ sudo apt install hailo-tappas-core=3.30.0-1 hailort=4.19.0-3 hailo-dkms=4.19.0-1 python3-hailort=4.19.0-2
```

```sh
$ sudo apt-mark hold hailo-tappas-core hailort hailo-dkms python3-hailort
```

**4.18**

要安装 4.18 版本的 Hailo 神经网络工具，请运行以下命令：

```sh
$ sudo apt install hailo-tappas-core=3.29.1 hailort=4.18.0 hailo-dkms=4.18.0-2
```

```sh
$ sudo apt-mark hold hailo-tappas-core hailort hailo-dkms
```

**4.17**

要安装 4.17 版本的 Hailo 神经网络工具，请运行以下命令：

```sh
$ sudo apt install hailo-tappas-core=3.28.2 hailort=4.17.0 hailo-dkms=4.17.0-1
```

```sh
$ sudo apt-mark hold hailo-tappas-core hailort hailo-dkms
```

### 更多资源

* 有关 Hailo 自有的、可在树莓派 5 上运行的演示集，请参阅 [hailo-apps](https://github.com/hailo-ai/hailo-apps) GitHub 仓库。
* 有关 Hailo 的模型库（包含大量神经网络），请参阅 [Hailo Model Explorer](https://hailo.ai/products/hailo-software/model-explorer-vision/)。
* 有关 Hailo 硬件和工具的讨论，请参阅 [Hailo 社区](https://community.hailo.ai/)论坛和[开发者专区](https://hailo.ai/developer-zone)。

## 在树莓派 5 上运行 LLM（仅 AI HAT+ 2）

本节提供在 AI HAT+ 2 上设置 Hailo 10 NPU 的说明，以便在树莓派 5 上本地运行大语言模型（LLM）。完成以下设置后，你可以通过以下方式访问 LLM：

* **POST 请求（API 调用）**：直接向 hailo-ollama 服务器发送查询。
* **Web UI 前端**：使用基于浏览器的聊天式界面。

### 运行本地 LLM 的组件

在树莓派 5 上运行本地 LLM 涉及多个协同工作的系统层，以实现硬件加速推理。

#### 硬件层

运行本地 LLM 所需的物理计算能力来自：

* **树莓派 5**：提供主 CPU、内存和通用 I/O，用于运行操作系统、管理软件并协调与 AI 加速器的通信。
* **Hailo AI 加速芯片**（通过 AI HAT+ 2 提供的 Hailo-10H NPU）：提供 AI 推理的神经处理能力，让你可以运行本地 LLM。

有关这些前提的更多信息，请参阅[硬件前提](#硬件前提)。

#### 软件层

要在树莓派 5 上使用 Hailo NPU 运行本地 LLM，你必须安装一组软件依赖项、驱动和运行时组件。

运行 LLM（以及视觉 AI）需要软件依赖项。有关所需依赖项及安装说明，请参阅[软件前提中的安装所需依赖项](#安装所需依赖项)。

#### AI 模型层

**Hailo Gen-AI Model Zoo** 包含适合在 Hailo-10H 上运行的预训练 LLM。这些模型作为[第 1 步](#第-1-步安装-hailo-ollama-服务器)的一部分安装。随后运行时加载这些模型，并由 AI 加速器执行。

#### 后端层

LLM 由 **Hailo Ollama 服务器**加载和运行。该后端层：

* 从 Hailo Gen-AI Model Zoo 加载 LLM。
* 管理 Hailo-10H NPU 上的推理。
* 提供 REST API，用于向 NPU 发送请求（提交提示）并返回 AI 推理结果（接收响应）。

Hailo Ollama 服务器作为[第 2 步](#第-2-步启动-hailo-ollama-服务器并运行-llm)的一部分安装。

#### 前端层（可选）

由 **Open WebUI** 提供的前端层是一个可选的、基于浏览器的聊天界面，用于与 LLM 交互。或者，你也可以继续使用[第 2 步](#第-2-步启动-hailo-ollama-服务器并运行-llm)中介绍的基于终端的 POST 请求与 LLM 交互。

虽然运行 LLM 并不需要 Open WebUI，但它提供了一种更友好的方式来提交提示和查看响应，而不是使用基于终端的 POST 请求。Open WebUI 通过其 REST API 与 Hailo Ollama 服务器通信，并在对话式 UI 中显示模型输出。

Open WebUI 需要运行在 Docker 容器中。这是因为 Open WebUI 与 Python 3.13（树莓派系统 Trixie 所用版本）不兼容。Docker 提供容器化环境以保证稳定运行。

Open WebUI 的设置由[第 3 步](#第-3-步安装-docker用于-open-webui)和[第 4 步](#第-4-步安装并使用-open-webui可选)组成。

### 第 1 步：安装 Hailo Ollama 服务器

Hailo Ollama 服务器提供：

* 为 Hailo-10H NPU 优化的预训练 LLM。
* 暴露 REST API 以供模型推理的 Hailo Ollama 服务器。

要安装 Hailo Ollama 服务器，请下载适用于树莓派 5 的 Hailo Model Zoo GenAI **5.1.1 版** [Debian 软件包](https://dev-public.hailo.ai/2025_12/Hailo10/hailo_gen_ai_model_zoo_5.1.1_arm64.deb)，然后在树莓派终端中使用以下命令安装：

```sh
sudo dpkg -i hailo_gen_ai_model_zoo_5.1.1_arm64.deb
```

### 第 2 步：启动 Hailo Ollama 服务器并运行 LLM

安装完成后，启动本地 `hailo-ollama` 服务器以暴露供 LLM 请求使用的 REST API，然后下载并运行一些 LLM。

1. 在树莓派终端中运行以下命令启动本地 `hailo-ollama` 服务器：

```sh
$ hailo-ollama
```

2. 在新的终端窗口中运行以下命令获取 LLM 列表：

```sh
$ curl --silent http://localhost:8000/hailo/v1/list
```

3. 运行以下命令从提供的列表中下载模型，将 `"examplemodel:tag"` 替换为所列的任一模型（例如 `"qwen2:1.5b"`）：

```sh
$ curl --silent http://localhost:8000/api/pull \
     -H 'Content-Type: application/json' \
     -d '{ "model": "examplemodel:tag", "stream" : true }'
```

4. 运行以下命令通过 POST 请求向 LLM 发送查询，将 `"examplemodel:tag"` 替换为你已下载并想要运行的模型：

```sh
$ curl --silent http://localhost:8000/api/chat \
     -H 'Content-Type: application/json' \
     -d '{"model": "examplemodel:tag", "messages": [{"role": "user", "content": "Translate to French: The cat is on the table."}]}'
```

### 第 3 步：安装 Docker（用于 Open WebUI）

如果你不打算使用 Open WebUI 界面，可以跳过此步骤。

以下说明在树莓派 5 上安装 Docker，这是部署和运行 Open WebUI 的前提，详见[第 4 步](#第-4-步安装并使用-open-webui可选)。更全面的安装说明，请参阅 Docker 的页面：[在 Debian 上安装 Docker Engine](https://docs.docker.com/engine/install/debian/)。

要安装 Docker：

1. 移除任何现有的 Docker 软件包：

```sh
$ sudo apt remove $(dpkg --get-selections docker.io docker-compose docker-doc podman-docker containerd runc | cut -f1)
```

2. 安装 Docker apt 仓库：

```sh
# 添加 Docker 的官方 GPG 密钥：
$ sudo apt update
$ sudo apt install ca-certificates curl
$ sudo install -m 0755 -d /etc/apt/keyrings
$ sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
$ sudo chmod a+r /etc/apt/keyrings/docker.asc

# 将仓库添加到 Apt 源：
$ sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
Types: deb
URIs: https://download.docker.com/linux/debian
Suites: $(. /etc/os-release && echo "$VERSION_CODENAME")
Components: stable
Signed-By: /etc/apt/keyrings/docker.asc
EOF

$ sudo apt update
```

3. 检查 `docker.sources` 文件是否已正确创建：

```sh
$ cat /etc/apt/sources.list.d/docker.sources
```

预期输出会列出以下内容，其中 `Suites` 是操作系统的 `VERSION_CODENAME`（`trixie`）：

```
Types: deb
URIs: https://download.docker.com/linux/debian
Suites: trixie
Components: stable
Signed-By: /etc/apt/keyrings/docker.asc
```

4. 安装并运行 Docker 服务：

```sh
$ sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

$ sudo systemctl start docker
```

5. 创建 `docker` 组：

```sh
$ sudo groupadd docker
```

6. 将你的用户添加到 `docker` 组：

```sh
$ sudo usermod -aG docker $USER
```

7. 注销并重新登录以使组成员资格重新评估，或运行以下命令激活组成员资格更改：

```sh
$ newgrp docker
```

8. 测试 Docker：

```sh
$ docker run hello-world
```

### 第 4 步：安装并使用 Open WebUI（可选）

在上一节安装 Docker 后，你可以使用 Docker 部署并运行 Open WebUI 容器。

>**注意**
>
>以下方法是部署和使用容器的一种方式，并非唯一方法。例如，你也可以改用 `docker-compose` 进行容器管理。

1. 要使用 Open WebUI，首先需要安装它。下载运行前端层所需的 Open WebUI 镜像：

```sh
$ docker pull ghcr.io/open-webui/open-webui:main
```

2. 确保 `hailo-ollama` 已在运行。然后启动 Open WebUI 容器并将其连接到 `hailo-ollama` 后端服务器：

```sh
$ docker run -d -e OLLAMA_BASE_URL=http://127.0.0.1:8000 -v open-webui:/app/backend/data --name open-webui --network=host --restart always ghcr.io/open-webui/open-webui:main
```

3. 监视容器启动。容器最多可能需要一分钟初始化。要查看进度和日志，请运行以下命令，然后等待日志表明服务器已运行并准备好接受连接。

```sh
$ docker logs open-webui -f
```

4. 在网页浏览器中访问 Open WebUI，输入以下 URL：<http://127.0.0.1:8080>。这会打开一个聊天界面，你可以选择模型并开始与 LLM 交互。

更详细的说明，请参阅 Open WebUI 文档中的[快速入门](https://docs.openwebui.com/getting-started/quick-start/)指南。
