# 树莓派音频扩展板（Raspberry Pi Audio Board）

## 概述

树莓派音频扩展板可为您现有的高保真音响设备或基于树莓派的设备和项目提供高质量音频。我们提供了四种不同硬件的扩展板。适用于使用 40 针 GPIO 引脚的树莓派型号。

每块板都有特定的用途和一组功能。 DAC PRO，DAC+ 和 DigiAMP+ 扩展板支持高达全高清音频（192kHz）的最高音质播放；而 Codec Zero 支持高达高清音频（96kHz），并包括内置麦克风，非常适合迷你项目。

### 参数对比

|               | **线路输出（Line out）** | **平衡输出（Balanced out）** | **立体声扬声器** | **单声道扬声器** | **耳机** | **AUX 输入** | **AUX 输出** | **外接麦克风** | **内置麦克风** |
| --------------- | --------------- | --------------- | ------------------- | ------------------- | ----------- | --------------- | --------------- | ----------------- | ----------------- |
| DAC Pro       | ✓            | ✓            |                   |                   | ✓        |               |               |                 |                 |
| DAC+          | ✓            |               |                   |                   | ✓        |               |               |                 |                 |
| 数字放大器+   |               |               | ✓                |                   |           |               |               |                 |                 |
| 编解码器 Zero |               |               |                   | ✓                |           | ✓            | ✓            | ✓              | ✓              |

线路输出 A 双声道 RCA 连接器，通常为红色和白色。此输出是可变模拟信号（0-2V RMS），可连接到您现有的高保真系统（前置放大器或功放），或用于驱动具有自己内置功放的有源音箱。

平衡输出 XLR 连接器，通常是三针公连接器。这在工作室设置中使用，在一些高端高保真系统中也使用。它也可以用于驱动像那些在俱乐部或舞台上对着 DJ 或表演者的主动监听扬声器。

立体声扬声器两组 2×25W 扬声器的螺钉端子。这些是传统的没有内置放大的高保真扬声器。这些被称为被动扬声器。

单声道扬声器一个单独的 1.2W 扬声器的螺钉端子，如晶体管收音机或类似产品中所找到的。

一个 3.5 毫米插孔插座，为一副耳机提供立体声音频。树莓派 DAC 板上的耳机放大器可驱动高达 80/90Ω 的阻抗耳机。

Aux in 双 Phono/RCA 连接器或 3.5 毫米插孔。可接受高达 1V RMS 的模拟音频输入。这可用于从可变模拟源（如手机，MP3 播放器或类似设备）录制音频。

Aux out 双 Phono/RCA 连接器或 3.5 毫米插孔。提供高达 1V RMS 的模拟音频输出。这可用于将音频馈送到放大器中，与 Line out 相比音量降低。

用于与外部电容麦克风配合使用的外部麦克风 3.5 毫米插孔。当使用外部麦克风插座时，会自动禁用 Codec Zero 上的内置 MEMS 麦克风。

### 树莓派 DAC Pro

树莓派 DAC Pro HAT 是我们最高保真度的数字模拟转换器（DAC）。

![DAC Pro Board Diagram](https://www.raspberrypi.com/documentation/accessories/images/DAC_Pro_Board_Diagram.jpg)

使用 Texas Instruments PCM5242，DAC Pro 提供出色的信噪比（SNR），支持平衡/差分输出，并与留声机/RCA 线级输出并行。它还包括专用耳机放大器。DAC Pro 由树莓派通过 GPIO 标头供电。

作为 DAC Pro 的一部分，两个三针标头（P7/P9）位于树莓派的 USB 和以太网接口上方，供可选的 XLR 板使用，允许差分/平衡输出。

#### 引脚分配

| **P1** | 模拟输出（0-2V RMS），携带 GPIO27，静音信号（耳机检测），左右音频和左右地线。 |
| -- | ------------------------------------------------------------------------------- |
| **P6** | 耳机插孔信号（1：左，2：地线，3：右，4：地线，5：检测）。                     |
| **P7/9** | 差分（0-4V RMS）输出（P7：左，P9：右）。                                      |
| **P10** | 替代 5V 输入，与树莓派并联供电。                                              |

#### 可选的 XLR 板

Pi-DAC PRO 通过一个 6 针头连接器暴露出一个可选的 XLR 板，通过 XLR 插座提供差分/平衡输出，位于树莓派的 USB/以太网接口上方。

![optional xlr board](https://www.raspberrypi.com/documentation/accessories/images/optional_xlr_board.jpg)

XLR 连接器用于工作室和一些高端 hifi 系统。它也可用于驱动在迪斯科或舞台上使用的主动“监视器”扬声器。

### 树莓派 DAC+

树莓派 DAC+ 是一款可提供 24 位 192kHz 数字音频输出的高分辨率音频输出 HAT。

![DAC+ Board Diagram](https://www.raspberrypi.com/documentation/accessories/images/DAC+_Board_Diagram.jpg)

DAC+ 中使用了德州仪器 PCM5122，将模拟音频传输到设备的音频插座。它还支持专用耳机放大器，并通过树莓派 GPIO 引脚头取电。

#### 引脚分配

| **P1** | 模拟输出（0-2V RMS），携带 GPIO27，静音信号（耳机检测），左右音频和左右地线。 |
| -- | ------------------------------------------------------------------------------- |
| **P6** | 耳机插孔信号（引脚 1：左，2：地线，3：右，4：地线，5：检测）。                |

### 树莓派 DigiAMP+

使用树莓派 DigiAMP+，您可连接 2 个无源立体声扬声器，输出功率高达 35W，可变输出，非常适合用于基于树莓派的高保真系统。

DigiAMP+ 使用德州仪器 TAS5756M PowerDAC，必须由外部电源供电。它需要 12-24V 直流电源（建议使用 XP Power VEC65US19 电源适配器）。

![DigiAMP+ Board Diagram](https://www.raspberrypi.com/documentation/accessories/images/DigiAMP+_Board_Diagram.jpg)

DigiAMP+ 的电源桶连接器尺寸为 5.5mm x 2.5mm。

在上电时，默认情况下放大器会被静音（静音 LED 灯亮起）。软件负责静音状态和 LED 控制（树莓派 GPIO22）。

DigiAMP+ 旨在同时并联为树莓派和 DigiAMP+ 提供电源，通过 GPIO 接口为树莓派提供 5.1V 2.5A 的电流。

>**警告**
>
>在使用 DigiAMP+ 时，请勿向树莓派的电源输入接口供电。


#### 引脚分配

| **P5** | 用于硬线安装的备用电源输入（必须遵守极性）。 |
| -- | ---------------------------------------------- |
| **P8** | TAS5756m 内部 GPIO1/2/3                      |

### 树莓派 Codec Zero

树莓派 Codec Zero 是一款树莓派 Zero 尺寸的音频 HAT。它在树莓派和 Codec Zero 的内置 Dialog Semiconductor DA7212 编解码器之间传递双向数字音频信号（I2S）。Codec Zero 支持各种输入和输出设备。

* 高性能 24 位音频编解码器
* 支持 8-96kHz 之间的常见音频采样率
* 内置微机电（MEMS）麦克风（Mic2）
* 单声道电容式麦克风（Mic2 左）
* 在检测到 Mic2 插入时自动禁用 MEMS
* 支持额外的（不适合）单声道电容麦克风（Mic1 右）
* 立体声辅助输入通道（AUX IN）- PHONO/RCA 连接器
* 立体声辅助输出通道（耳机/AUX OUT）
* 灵活的模拟和数字混音路径
* 自动电平控制（ALC）的数字信号处理器（DSP）
* 五段均衡器
* 单声道线路输出/迷你扬声器驱动器：1.2 W @ 5V，THD<10%，R=8Ω

![Codec Zero Board Diagram](https://www.raspberrypi.com/documentation/accessories/images/Codec_Zero_Board_Diagram.jpg)

Codec Zero 内置了 EEPROM，必要时可用于自动配置 Linux 环境。它具有集成的 MEMS 麦克风，并可通过 3.5 毫米插孔与立体声麦克风输入和单声道扬声器（1.2 W/8Ω）一起使用。

除了绿色（GPIO23）和红色（GPIO24）LED 灯外，还提供了一个可编程的触觉按钮（GPIO27）。

#### 引脚排列

| **P1/2** | 如果需要，支持外部 PHONO/RCA 插座。P1：AUX IN，P2：AUX OUT。 |
| -- | -------------------------------------------------------------- |
| **P1** | 第 1 针是方形的。                                            |

![CODEC ZERO ZOOMED IN DIAGRAM](https://www.raspberrypi.com/documentation/accessories/images/CODEC_ZERO_ZOOMED_IN_DIAGRAM.jpg)

Codec Zero 是小型项目的理想设计起点，如对讲机、智能门铃、复古收音机改装或智能音箱。

## 配置

所有树莓派音频扩展板上都包含了预编程的 EEPROM。树莓派音频扩展板设计为即插即用；Raspberry Pi OS 可自动检测并配置。在 Raspberry Pi OS 中，用右键单击屏幕右上角的音频设置，可以在板载音频设置和 HAT 音频设置之间切换：

![gui](https://www.raspberrypi.com/documentation/accessories/images/gui.png)

有许多第三方音频软件应用程序适用于树莓派，支持我们音频扩展板的即插即用功能。他们通常无需屏幕。它们可以通过 PC 或 Mac 应用程序控制，也可以通过安装在树莓派上的 Web 服务器控制，并通过网页进行交互。

如果您需要自行配置 Raspberry Pi OS（也许是因为您正在运行自己的无头系统，无法通过 GUI 进行控制）那么您需要将树莓派音频扩展板设置为 Raspberry Pi OS 的主要音频设备，并禁用树莓派的板载音频设备。这可以通过编辑 /boot/firmware/config.txt 文件来实现。通过 SSH 连接到您的树莓派的终端会话，运行以下命令来编辑文件：

```
$ sudo nano /boot/firmware/config.txt
```

在文件中找到 dtparam=audio=on 行，并通过在该行开头放置 `#` 符号来注释掉它。任何给定行中 `#` 符号之后的内容将被程序忽略。您的 /boot/firmware/config.txt 文件现在应包含以下条目：

```
#dtparam=audio=on
```

按下 Ctrl+X 键，然后按 Y 键，最后按 Enter 保存。最后，重新启动您的树莓派以使设置生效。

```
$ sudo reboot
```

或者，可以直接在树莓派的 microSD 卡上编辑 /boot/firmware/config.txt 文件，然后将其插入您通常使用的计算机。使用默认文件管理器，在卡上打开 /boot/firmware/ 卷，并使用适当的文本编辑器编辑 config.txt 文件，然后保存文件，弹出 microSD 卡，重新插入到树莓派中。

### 安装 HAT

树莓派音频扩展板连接到树莓派的 40 针引脚头上。它们设计为使用提供的电路板支架和螺丝支撑在树莓派上。除非您在 DAC Pro 上使用硬连线连接器（如 XLR（外部线路返回）连接）需要对树莓派音频扩展板进行常规操作，否则无需焊接。

所提供的全部必要安装硬件包含了间隔柱、螺丝和连接器。在添加音频扩展板之前，应仅用手指将 PCB 间隔柱拧紧到树莓派上。然后，应将剩余的螺丝从上方拧入间隔柱中。

### 硬件版本

音频卡有多个版本，您拥有的版本决定了所需的配置操作。较老的 IQaudIO 标记的板（黑色 PCB）在电气上等同于树莓派品牌的板（绿色 PCB），但具有不同的 EEPROM 内容。可以使用以下命令确认您拥有的版本：

```
$ grep -a . /proc/device-tree/hat/*
```

如果供应商字符串显示为"Raspberry Pi Ltd."，则无需采取进一步操作（但请参阅下文以获取额外的 Codec Zero 配置）。如果显示为"IQaudIO Limited www.iqaudio.com"，则需要以下所述的额外 config.txt 设置。如果显示为"找不到文件或目录"，则表示 HAT 未被检测到，但这些 config.txt 设置可能仍然使其正常工作。

```
# Some magic to prevent the normal HAT overlay from being loaded
dtoverlay=
# And then choose one of the following, according to the model:
dtoverlay=rpi-codeczero
dtoverlay=rpi-dacplus
dtoverlay=rpi-dacpro
dtoverlay=rpi-digiampplus
```

### 额外的 Codec Zero 配置

树莓派 Codec Zero 板使用 Dialog Semiconductor DA7212 编解码器。这允许从内置 MEMS 麦克风、立体声磁头插座（AUX IN）或两个单声道外部电容麦克风录制音频。播放通过立体声磁头插座（AUX OUT）或单声道扬声器连接器进行。

每个输入和输出设备都有自己的混音器，允许独立调整音频级别和音量。在编解码器本身内部，还存在其他混音器和开关，允许将输出混合到单声道以用于单扬声器输出。信号也可以被反转；有一个五段均衡器来调整特定频段。这些设置可以通过交互方式使用 AlsaMixer 进行控制，也可以通过编程方式进行控制。

AUX IN 和 AUX OUT 都是 1V RMS。可能需要调整 AUX IN 的混音器，以确保输入信号不会使 ADC 饱和。同样，可以调整输出混音器以获得最佳输出。

在 GitHub 上提供了预配置的脚本（可加载的 ALSA 设置），提供了：

* 单声道 MEMS 麦克风录制，单声道扬声器播放
* 单声道 MEMS 麦克风录制，单声道 AUX OUT 播放
* 立体声 AUX IN 录制，立体声 AUX OUT 播放
* 立体声 MIC1/MIC2 录音，立体声 AUX OUT 播放

Codec Zero 需要在每次树莓派上电时知道正在使用哪些输入和输出设置。在树莓派上的终端会话中，运行以下命令下载脚本：

```
$ git clone https://github.com/raspberrypi/Pi-Codec.git
```

如果未安装 `git`，请运行以下命令进行安装：

```
$ sudo apt install git
```

以下命令将设置您的设备使用板载 MEMS 麦克风和扬声器进行播放：

```
$ sudo alsactl restore -f /home/<username>/Pi-Codec/Codec_Zero_OnboardMIC_record_and_SPK_playback.state
```

为了在项目上电时使用所需的设置，请编辑 /etc/rc.local 文件。该文件的内容在每次引导过程结束时运行，因此非常适合此目的。编辑文件：

```
$ sudo nano /etc/rc.local
```

在 exit 0 行上方添加所选脚本命令，然后按 Ctrl X，Y 和 Enter 保存。根据您选择的设置，文件现在应该看起来类似于这样：

```
#!/bin/sh -e
#
# rc.local
#
# This script is executed at the end of each multiuser runlevel.
# Make sure that the script will "exit 0" on success or any other
# value on error.
#
# In order to enable or disable this script just change the execution
# bits.
#
# By default this script does nothing.

sudo alsactl restore -f /home/<username>/Pi-Codec/Codec_Zero_OnboardMIC_record_and_SPK_playback.state

exit 0
```

按 Ctrl+X ，然后按 Y 键，然后按 Enter 键保存。重新启动以使设置生效：

```
$ sudo reboot
```

如果您在无头环境中使用您的树莓派和 Codec Zero，则需要执行一个最后步骤，以使 Codec Zero 成为默认音频设备，而无需访问桌面上的 GUI 音频设置。我们需要在您的主文件夹中创建一个小文件：

```
$ sudo nano .asoundrc
```

将以下内容添加到文件中：

```
pcm.!default {
        type hw
        card Zero
}
```

按 Ctrl+X ，然后按 Y 键，然后按 Enter 键保存。重新启动一次以完成配置：

```
$ sudo reboot
```

### 静音和取消静音 DigiAMP+

树莓派上的 GPIO22 切换 DigiAMP+ 静音状态。最新的音频设备树通过附加参数支持取消 DigiAMP+ 的静音。

首先，在内核模块加载时进行“一次性”静音。

对于树莓派板：

```
dtoverlay=rpi-digiampplus,unmute_amp
```

 对于 IQaudIO 板：

```
dtoverlay=iqaudio-digiampplus,unmute_amp
```

当 ALSA 设备被客户端打开时取消静音。当 ALSA 设备关闭时，延迟五秒后静音。（在五秒关闭窗口内重新打开设备将取消静音。）

对于树莓派板：

```
dtoverlay=rpi-digiampplus,auto_mute_amp
```

 对于 IQaudIO 板：

```
dtoverlay=iqaudio-digiampplus,auto_mute_amp
```

如果您不想通过设备树控制静音状态，也可以编写自己的脚本解决方案。

放大器将以静音状态启动。要取消静音放大器：

```
$ sudo sh -c "echo 22 > /sys/class/gpio/export"
$ sudo sh -c "echo out >/sys/class/gpio/gpio22/direction"
$ sudo sh -c "echo 1 >/sys/class/gpio/gpio22/value"
```

再次将放大器静音：

```
$ sudo sh -c "echo 0 >/sys/class/gpio/gpio22/value"
```

## 入门指南

### 创建玩具聊天盒

作为树莓派音频扩展板的一个示例，让我们一起来制作一个玩具聊天盒。其内置麦克风、可编程按钮和扬声器驱动器使 Codec Zero 成为此应用的理想选择。

![Chatter Box](https://www.raspberrypi.com/documentation/accessories/images/Chatter_Box.jpg)

当按下按钮时，将播放一个随机的预先录制的五秒音频片段。按住十秒后，将发出通知的打嗝声，然后录制一个新的五秒片段。按住按钮超过 20 秒将播放第二个打嗝声，并删除所有先前的录音。

### 硬件和接线

对于这个项目，任何小型被动扬声器都应该足够。我们使用了一个在这里可用的扬声器，它在 4Ω 时承载 5W 功率。我们还使用了一个发光的瞬时按键和一个激光切割的盒子来容纳所有组件；但这两者都是完全可选的。这个示例将仅使用 Codec Zero 的板载按钮，该按钮预先连接到 GPIO 27。（或者，您可以使用任何瞬时按键，比如这里提供的。）

![Chatterbox Labels](https://www.raspberrypi.com/documentation/accessories/images/Chatterbox_Labels.png)

使用小型扁头螺丝刀将扬声器连接到螺丝端子。对于额外的按钮，根据指示将按钮线焊接到 Codec Zero 垫片上，使用 GPIO 引脚 27 和地线作为开关，如果需要，使用 +3.3V 和地线作为 LED。

### 设置您的树莓派

在此示例中，我们使用 Raspberry Pi OS Lite。有关更多详细信息，请参考我们的安装 Raspberry Pi OS 指南。

在继续之前，请确保更新您的操作系统，并按照提供的 Codec Zero 配置说明进行操作，包括启用板载麦克风和扬声器输出的命令。

### 编程您的树莓派

在您的树莓派上打开一个 shell — 例如通过 SSH 连接 — 并运行以下内容来创建我们的 Python 脚本：

```
$ sudo nano chatter_box.py
```

将以下内容添加到文件中，将 `<username>` 替换为您的用户名：

```
#!/usr/bin/env python3
from gpiozero import Button
from signal import pause
import time
import random
import os
from datetime import datetime

# Print current date

date = datetime.now().strftime("%d_%m_%Y-%H:%M:%S")
print(f"{date}")

# Make sure that the 'sounds' folder exists, and if it does not, create it

path = '/home/<username>/sounds'

isExist = os.path.exists(path)

if not isExist:
  os.makedirs(path)
  print("The new directory is created!")
  os.system('chmod 777 -R /home/<username>/sounds')

# Download a 'burp' sound if it does not already exist

burp = '/home/<username>/burp.wav'

isExist = os.path.exists(burp)
if not isExist:
  os.system('wget http://rpf.io/burp -O burp.wav')
  print("Burp sound downloaded!")

# Setup button functions - Pin 27 = Button hold time 10 seconds.

button = Button(27, hold_time=10)

def pressed():
    global press_time
    press_time = time.time()
    print("Pressed at %s" % (press_time));

def released():
    release_time = time.time()
    pressed_for = release_time - press_time
    print("Released at %s after %.2f seconds" % (release_time, pressed_for))
    if pressed_for < button.hold_time:
        print("This is a short press")
        randomfile = random.choice(os.listdir("/home/<username>/sounds/"))
        file = '/home/<username>/sounds/' + randomfile
        os.system('aplay ' + file)
    elif pressed_for > 20:
        os.system('aplay ' + burp)
        print("Erasing all recorded sounds")
        os.system('rm /home/<username>/sounds/*');

def held():
    print("This is a long press")
    os.system('aplay ' + burp)
    os.system('arecord --format S16_LE --duration=5 --rate 48000 -c2 /home/<username>/sounds/$(date +"%d_%m_%Y-%H_%M_%S")_voice.m4a');

button.when_pressed = pressed
button.when_released = released
button.when_held = held

pause()
```

按 Ctrl+X 键，然后按 Y 键，然后按 Enter 键保存。要使脚本可执行，请输入以下内容：

```
$ sudo chmod +x chatter_box.py
```

输入以下内容以创建一个 crontab 守护程序，每次设备启动时都会自动启动脚本：

```
$ crontab -e
```

您将被要求选择一个编辑器；我们建议您使用 nano 。通过输入相应的数字进行选择，然后按 Enter 键继续。应将以下行添加到文件底部，将 `<username>` 替换为您的用户名：

```
@reboot python /home/<username>/chatter_box.py
```

按 Ctrl X、Y 和 Enter 保存，然后重新启动您的设备。

### 操作您的设备

最后一步是确保一切都按预期运行。按下按钮，当听到打嗝声时松开按钮。录音现在将开始，持续五秒钟。一旦您松开按钮，请再次简短按下按钮以听取录音。您可以根据需要重复此过程，您的声音将随机播放。您可以通过按住按钮并在第一次打嗝声和录音过程期间保持按钮按下，然后在至少 20 秒后释放按钮来删除所有录音，此时您将听到另一个打嗝声，确认已删除录音。

### 下一步

升级！升级项目总是很有趣，为什么不添加一些额外功能，比如录音时会亮起的 LED？此项目具有制作自己版本的谷歌智能扬声器系统所需的所有零件，或者您可能考虑构建第二个设备，可用于创建一对能够通过 SSH 通过网络传输音频文件的对讲机。

## 硬件信息

 硬件信息：

* PCB 螺丝全部为 M2.5。
* PCB 支架（用于机箱）为 5mm 公/母。
* PCB 支架（用于树莓派到音频扩展板）为 9mm 母/母。
* PCB 支架（用于 XLR 到 DAC PRO）为 8mm 母/公。
* PCB 支架（用于官方树莓派 7 英寸显示屏）为 5 毫米公母。
* 我们使用和测试过的旋转编码器包括 Alpha 三针旋转编码器 RE160F-40E3-20A-24P，ALPS EC12E2430804（RS：729-5848），和 Bourns ECW0JB24-AC0006L（RS：263-2839）。
* 用于为 DigiAMP+ 供电的圆筒连接器为 2.5mm 内径，5.5mm 外径，11mm。
* DigiAMP+ 设计为与 12V 至 24V、3A 供应配合使用，例如 XPPower VEC65US19 或类似产品。
* DigiAMP+ 使用 CamdenBoss 的两部分连接器。安装在 PCB 上的是 CTBP9350/2AO。
* Codec Zero 上使用的扬声器端子可接受 14~26 AWG（直径最大为 1.6mm）之间的线缆。

### GPIO 使用

树莓派音频扩展板利用 GPIO 头上的许多引脚才能正常运行。其中一些引脚仅供扩展板使用，而另一些可与其他外设、传感器等共享。

音频扩展板使用以下树莓派 GPIO 引脚：

* 所有电源引脚
* 所有地线引脚
* GPIO 2/3 (I2C)
* GPIO 18/19/20/21 (I2S)

如果可用，还将使用以下硬件：

* GPIO 22（DigiAMP+ 静音/取消静音支持）
* 用于旋转编码器（物理音量控制）或状态 LED（Codec Zero）的 GPIO 23/24
* 用于红外传感器的 GPIO 25
* 用于旋转编码器按键开关/Codec Zero 开关的 GPIO 27

### DAC PRO，DAC+，DigiAMP+，Codec Zero

![pin table new](https://www.raspberrypi.com/documentation/accessories/images/pin_table_new.jpg)

DAC PRO，DAC+ 和 DigiAMP+ 重新公开了树莓派信号，可以轻松添加其他传感器和外围设备。请注意，一些信号是一些我们的主板专用的（如 I2S 和 EEPROM）；其他信号如 I2C 可以在多个主板之间共享。

![pin out new](https://www.raspberrypi.com/documentation/accessories/images/pin_out_new.jpg)

### 保存 AlsaMixer 设置

存储 AlsaMixer 设置，请在命令行中添加以下内容：

```
$ sudo alsactl store
```

您可以将当前状态保存到文件，然后在启动时重新加载该状态。

要保存，请运行以下命令，将 `<username>` 替换为您的用户名：

```
$ sudo alsactl store -f /home/<username>/usecase.state
```

要恢复保存的文件，请运行以下命令，将 <username> 替换为您的用户名：

```
$ sudo alsactl restore -f /home/<username>/usecase.state
```

### 基于 MPD 的音频与音量控制

要允许基于音乐播放器守护程序（MPD）的音频软件控制音频扩展板的内置音量，可能需要更改文件 /etc/mpd.conf 以支持正确的 AlsaMixer 名称。

通过确保 /etc/mpd.conf 的“音频输出”部分具有“混音器控制”行，可以实现这一点。以下是德州仪器基于的板卡（DAC PRO/DAC+/DigiAMP+）的示例：

```
audio_output {
    type "alsa"
    name "ALSA Device"
    mixer_control "Digital"
}
```

## 更新固件

树莓派音频板使用包含信息的 EEPROM，该信息由主机树莓派设备在启动时选择适当的驱动程序时使用。此信息在制造过程中编程到 EEPROM 中。在某些情况下，最终用户可能希望更新 EEPROM 内容：可以通过命令行完成。

>**重要**
>
>在继续之前，您应该将运行在您的树莓派上的 Raspberry Pi OS 更新到最新版本。

### EEPROM 写保护链接

在编程过程中，您需要用导线连接红色框中显示的两个焊盘，以拉低 EEPROM 写保护链接。

![write protect tabs](https://www.raspberrypi.com/documentation/accessories/images/write_protect_tabs.jpg)

>**注意**
>
>在某些情况下，两个焊盘上可能已经焊接了一个 0Ω 电阻，用于连接写保护链接，就像上面 Codec Zero 板的图片中所示。

### EEPROM 编程

在写保护线被拉低后，EEPROM 就可以被编程。

您应该首先安装实用程序，然后运行管理员权限。打开终端，输入以下内容：

```
$ sudo apt update
$ sudo apt install rpi-audio-utils
$ sudo rpi-audio-flash
```

启动后，您将看到一个警告信息。

![warning](https://www.raspberrypi.com/documentation/accessories/images/firmware-update/warning.png)

选择“是”继续，将显示一个菜单，允许您选择您的硬件。

![select](https://www.raspberrypi.com/documentation/accessories/images/firmware-update/select.png)

>**注意**
>
>如果没有扩展板，或者连接的扩展板并非树莓派音频扩展板，则会显示错误信息。如果已经更新了主板上的固件，将显示一条消息，告知您无需继续操作。

选择正确的硬件后，屏幕将显示，同时将新固件刷入扩展板。

![flashing](https://www.raspberrypi.com/documentation/accessories/images/firmware-update/flashing.png)

稍后将显示信息，告诉您已安装新固件。

![flashed](https://www.raspberrypi.com/documentation/accessories/images/firmware-update/flashed.png)

>**注意**
>
>如果固件安装失败，将在屏幕上显示错误。首先，您应该拔下来并重新插入扩展板，然后尝试重新刷写固件。 
