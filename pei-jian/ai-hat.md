# AI HAT+（AI HATs）

AI HAT 是树莓派 5 的附加板，内置 AI 加速芯片：Hailo 神经处理单元（NPU）。Hailo NPU 使树莓派 5 能够在本地运行硬件加速的 AI 模型，无需将数据发送到远程云服务器进行处理。这种边缘 AI 方法可提升性能、降低延迟，并有助于保护数据隐私。有关 AI HAT 如何与树莓派 5 集成以提供硬件加速 AI 推理的信息，请参阅[工作原理](#工作原理)。

AI HAT 采用较新的树莓派 HAT 规范，以加号（**+**）表示。AI HAT 有两种型号：**AI HAT+** 和 **AI HAT+ 2**。更多信息请参阅[型号](#型号)。这些 AI HAT 提供不同的性能变体，以推理性能的每秒万亿次运算（TOPS）衡量。AI HAT+ 提供 **13 TOPS** 或 **26 TOPS** 变体；AI HAT+ 2 提供单一的 **40 TOPS** 变体。更多信息请参阅[性能（TOPS）变体](#性能tops变体)。

![26 每秒万亿次运算（TOPS）的树莓派 AI HAT+](https://www.raspberrypi.com/documentation/accessories/images/ai-hat-plus-hero.jpg)

26 每秒万亿次运算（TOPS）的树莓派 AI HAT+

![40 每秒万亿次运算（TOPS）的树莓派 AI HAT+ 2](https://www.raspberrypi.com/documentation/accessories/images/ai-hat-plus-2-hero.jpg)

40 每秒万亿次运算（TOPS）的树莓派 AI HAT+ 2

## 工作原理

AI HAT 与树莓派 5 集成，利用板载 Hailo NPU（加速芯片）提供硬件加速的 AI 推理。

当 AI HAT+ 或 AI HAT+ 2 连接到树莓派 5 时，树莓派系统会自动检测板载加速器，并将受支持的 AI 工作负载卸载到它上面。这包括使用我们现有的摄像头和视觉框架在 NPU 上运行基于视觉的神经网络模型。有关将 AI HAT+ 或 AI HAT+ 2 连接到树莓派 5 的说明，请参阅[硬件组装](#硬件组装)。

树莓派系统自带的摄像头应用框架 `rpicam-apps` 和 `Picamera2` 可自动使用 Hailo NPU 执行受支持的 AI 计算任务，例如图像识别和目标检测。更多信息请参阅[人工智能软件](../shu-mei-pai/ren-gong-zhi-neng-ruan-jian.md)。

虽然检测和基本集成是自动的，但你还必须安装其他软件组件和受支持的 AI 模型才能使用硬件加速推理。更多信息请参阅[人工智能软件](../shu-mei-pai/ren-gong-zhi-neng-ruan-jian.md)。

## 型号

下表列出了 AI HAT+ 与 AI HAT+ 2 之间的主要能力差异。有关每种型号可用的加速芯片具体性能变体的信息，请参阅[性能（TOPS）变体](#性能tops变体)。

>**注意**
>
> **AI 套件**的规格与 AI HAT+ 的 Hailo-8L 变体相同，功能上也等效。但是，AI 套件已停产，我们建议使用本页介绍的 AI HAT 之一。

| 功能 | AI HAT+ | AI HAT+ 2 |
| ---- | ---- | ---- |
| **加速芯片（Hailo NPU）** | Hailo-8L（13 TOPS，INT8）或 Hailo-8（26 TOPS，INT8） | Hailo-10H（40 TOPS，INT4） |
| **内存（RAM）** | 使用树莓派 5 上的内存 | 自带 8 GB 板载内存，可运行最多约 60 亿参数的大语言模型（LLM）和视觉语言模型（VLM） |
| **大语言模型（LLM）支持** | 不支持 | 支持 |
| **视觉语言模型（VLM）支持** | 不支持 | 支持 |
| **用例** | 目标检测、摄像头后处理、机器人、中等神经网络工作负载 | AI HAT+ 上所有可用功能，外加生成式 AI 工作负载，包括本地 LLM 和 VLM |

## 性能（TOPS）变体

**AI HAT+** 提供以下每秒万亿次运算（TOPS）推理性能变体：

- **13 TOPS**，基于 **Hailo-8L** 神经网络加速器构建。适用于中等工作负载，性能与 [AI 套件](ren-gong-zhi-neng-tao-jian-ai-kit.md)相似。
- **26 TOPS**，基于 **Hailo-8** 神经网络加速器构建。支持更大的网络、更高的吞吐量和并行 AI 模型。

**AI HAT+ 2** 提供 **40 TOPS** 推理性能，基于 **Hailo-10H** 神经网络推理加速器构建。它支持所有 AI HAT+ 工作负载，并增加了本地 LLM 和 VLM 能力，可实现本地文档问答等应用。

## 物理规格

下图展示了 AI HAT+、AI HAT+ 2 以及 AI HAT+ 2 附带散热器的物理尺寸。AI HAT+ 和 AI HAT+ 2 的尺寸相同；主要的视觉差异是 AI HAT+ 2 上增加了 SDRAM。有关此差异的更多信息，请参阅[型号](#型号)。

### AI HAT+ 规格

下图展示了 AI HAT+ 的大致物理尺寸，单位为毫米（mm）。AI HAT+ 约为 66 mm × 56.5 mm。Hailo NPU 周围有金属外壳，使其约为 17 mm × 17 mm。

![AI HAT+ 的机械图；所有测量值均为近似值，单位为毫米](https://www.raspberrypi.com/documentation/accessories/images/aihat-plus-mechanical.png)

### AI HAT+ 2 与散热器规格

下图展示了 AI HAT+ 2 的大致物理尺寸，单位为毫米（mm）。AI HAT+ 约为 66 mm × 56.5 mm。Hailo NPU 约为 15 mm × 15 mm，SDRAM 约为 14.5 mm × 10 mm。

![AI HAT+ 2 的机械图；所有测量值均为近似值，单位为毫米](https://www.raspberrypi.com/documentation/accessories/images/aihat-plus-2-mechanical.png)

下图展示了 AI HAT+ 2 散热器的大致物理尺寸，单位为毫米（mm）。考虑到用于将散热器固定到 AI HAT+ 2 的两个带有推入式销钉孔的角，散热器约为 42.5 mm × 64 mm。安装推入式销钉后，AI HAT+ 2 的高度约为 14 mm；不安装推入式销钉时，AI HAT+ 2 的高度约为 3.2 mm。

![AI HAT+ 2 散热器的机械图；所有测量值均为近似值，单位为毫米](https://www.raspberrypi.com/documentation/accessories/images/aihat-plus-2-heatsink-mechanical.png)

## 硬件组装

请检查你拥有所需的硬件，然后按照步骤在树莓派 5 上安装 AI HAT+ 或 AI HAT+ 2，开始前请确保树莓派 5 已断开电源。

### 准备工作

AI HAT+ 和 AI HAT+ 2 均附带以下安装硬件：

- 四个螺纹间隔柱。
- 四颗长螺丝，用于将间隔柱固定到树莓派 5。
- 四颗短螺丝，用于将 AI HAT+ 或 AI HAT+ 2 固定到树莓派 5 上的间隔柱。
- 一个 GPIO 堆叠排针。
- 一根排线。

![AI HAT 的安装硬件](https://www.raspberrypi.com/documentation/accessories/images/ai-hat-plus-installation-02.png)

此外，你还需要：

- 一台树莓派 5。
- 一把十字螺丝刀。
- 可选：树莓派主动散热器（推荐）。这是一个带风扇的铝制散热器，有助于散发树莓派 5 的热量，使其保持在安全的工作温度。

AI HAT+ 2 附带一个额外的散热器，需安装在 HAT 顶部。我们建议同时安装主动散热器（在树莓派 5 上）和散热器（在 AI HAT+ 2 上）。

当你备齐所有必需硬件后，请完成以下步骤。

### 第 1 步：安装主动散热器（推荐）

我们建议在树莓派 5 上安装主动散热器。如果你想跳过此步骤，或者你的树莓派 5 已经安装了主动散热器，请继续下一步。

![将主动散热器安装到树莓派 5 上](https://www.raspberrypi.com/documentation/accessories/images/ai-hat-plus-installation-01.png)

首先，确保树莓派 5 已断开电源。然后：

1. **准备散热器。** 移除散热器底部导热垫上的保护纸。这会露出每个导热垫上的粘性表面。
2. **放置散热器。** 将两个白色推入式销钉与树莓派 5 上两个专用的散热器孔对齐。在此位置，导热垫与无线模块、片上系统（SoC）和电源管理集成电路（PMIC）对齐。
3. **固定散热器。** 将散热器轻轻压到树莓派 5 上。然后，均匀地将两个白色推入式销钉向下压入树莓派 5 上的两个专用散热器孔，直到它们咔嗒一声卡入。
4. **连接风扇。** 将风扇的 JST 接头插入树莓派 5 上的风扇插座。

>**注意**
>
> 使用前请确保推入式销钉完好无损，并牢固地卡在树莓派 5 上。

我们建议散热器安装到树莓派 5 后不要拆卸。这是因为拆卸散热器可能导致推入式销钉和导热垫退化，从而造成产品损坏。

### 第 2 步：安装 AI HAT+ 2 散热器（推荐）

AI HAT+ 2 附带一个额外的散热器。如果你安装的是 AI HAT+ 而不是 AI HAT+ 2，可以跳过此步骤。

虽然 AI HAT+ 2 随附的散热器是可选的，但我们建议将其安装到 AI HAT+ 2 上，尤其是在运行基准测试或密集型 AI 工作负载时。这可以防止 AI HAT+ 2 因过热而降速。

要将 AI HAT+ 2 散热器安装到 AI HAT+ 2 上（在将其安装到树莓派 5 之前）：

1. **准备散热器。** 移除散热器底部导热垫上的保护纸。这会露出每个导热垫上的粘性表面。
2. **放置散热器。** 将散热器上的两个黑色推入式销钉与 AI HAT+ 2 上对角两个专用散热器孔对齐。在此位置，导热垫与电源稳压器、Hailo NPU 和 SDRAM 芯片对齐。
3. **固定散热器。** 均匀地将两个黑色推入式销钉向下压入 AI HAT+ 2 上的散热器孔，直到它们咔嗒一声卡入。

>**注意**
>
> 使用前请确保推入式销钉完好无损，并牢固地卡在 AI HAT+ 2 上。

我们建议散热器安装到树莓派 AI HAT+ 2 后不要拆卸。这是因为拆卸散热器可能导致推入式销钉和导热垫退化，从而造成产品损坏。

### 第 3 步：安装 AI HAT

AI HAT+ 和 AI HAT+ 2 均通过树莓派 5 的 PCIe 接口连接，这是一个用于连接硬件组件的高速接口。

首先，确保树莓派 5 已断开电源，然后：

1. **安装间隔柱。** 使用十字螺丝刀和四颗较长的螺丝，将四个间隔柱固定到树莓派 5 上的黄色孔位。
2. **连接 GPIO 堆叠排针。** 将 GPIO 堆叠排针与树莓派 5 上的 GPIO 引脚对齐。用力按下，直到排针完全就位。只要所有 GPIO 引脚都正确对齐并插入，排针的方向无关紧要。
3. **从 AI HAT 上断开 PCIe 排线。** 将 AI HAT 上 PCIe 接口两侧的固定夹向外滑出，然后轻轻拉出排线。
4. **将 PCIe 排线插入树莓派。** 将排线的另一端插入树莓派 5 上的 PCIe 接口。为此，首先将树莓派 5 上 PCIe 接口的固定夹从两侧向上滑出。然后，将排线插入 PCIe 接口。确保金属触点朝向内部（朝向 USB 接口）。
5. **将 PCIe 排线固定到树莓派。** 在保持排线不动的同时，从两侧将固定夹推回接口，确保排线均匀插入。
6. **安装 AI HAT。** 使 AI HAT 的主要组件朝上，将 AI HAT 上的安装孔与树莓派 5 上的间隔柱对齐。使用剩余的四颗（较短的）螺丝将 AI HAT 固定到位。
7. **将 PCIe 排线插入 AI HAT。** 将排线未连接的一端插入 AI HAT 上的 PCIe 接口。为此，首先将 AI HAT 上 PCIe 接口的固定夹从两侧向外滑出。然后，将排线插入 PCIe 接口。
8. **将 PCIe 排线固定到 AI HAT。** 在保持排线不动的同时，从两侧将固定夹推回接口，确保排线均匀插入。

## 后续步骤：运行 AI 模型

AI HAT 既支持 Hailo 提供的示例模型，也支持为你的特定应用训练的自定义模型，例如语音转文本、翻译或视觉场景分析。有关可用示例模型的列表，请参阅 Hailo 的 [Model Explorer](https://hailo.ai/products/hailo-software/model-explorer/generative-ai/)。

要开始在树莓派 5 上运行 AI 模型，请参阅[人工智能软件](../shu-mei-pai/ren-gong-zhi-neng-ruan-jian.md)，其中提供了有关以下内容的信息和指导：

- 在树莓派 5 上运行 AI 加速的视觉模型。
- 与 AI HAT+ 2 相关的生成式 AI 模型。
