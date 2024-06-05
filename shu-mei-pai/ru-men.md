# 入门

## 开始使用您的树莓派

 在 GitHub 上编辑此内容

要开始使用您的树莓派，您需要以下内容：

* 电源供应
* 引导介质（例如，具有充足存储空间和速度的 microSD 卡）

您可以将树莓派设置为带有桌面的交互式计算机，也可以将其设置为仅通过网络访问的无头计算机。要无头设置您的树莓派，您不需要任何额外的外围设备：您可以在安装操作系统时预先配置主机名、用户帐户、网络连接和 SSH。如果要直接使用您的树莓派，您将需要以下额外配件：

* 一个显示器
* 用于将树莓派连接到显示器的电缆
* 键盘
* 鼠标

### 电源供应

以下表格显示了为各种树莓派模型提供电源所需的 USB-PD 电源模式。您可以使用任何提供正确电源模式的高质量电源。

| 型号                    | 推荐的电源适配器（电压/电流）     | 树莓派电源适配器 |
| ------------------------- | ----------------------------------- | ------------------ |
| 树莓派 5                | 5V/5A，5V/3A 限制外围设备为 600mA | [27W USB-C 电源适配器](https://www.raspberrypi.com/products/27w-power-supply/)                 |
| 树莓派 4 型 B           | 5V/3A                             | [15W USB-C 电源适配器](https://www.raspberrypi.com/products/type-c-power-supply/)                 |
| 树莓派 3（所有型号）    | 5V/2.5A                           | [12.5W 微型 USB 电源适配器](https://www.raspberrypi.com/products/micro-usb-power-supply/)                 |
| 树莓派 2（所有型号）    | 5V/2.5A                           | [12.5W 微型 USB 电源适配器](https://www.raspberrypi.com/products/micro-usb-power-supply/)                 |
| 树莓派 1（所有型号）    | 5V/2.5A                           | [12.5W 微型 USB 电源适配器](https://www.raspberrypi.com/products/micro-usb-power-supply/)                 |
| 树莓派 Zero（所有型号） | 5V/2.5A                           | [12.5W 微型 USB 电源适配器](https://www.raspberrypi.com/products/micro-usb-power-supply/)                 |

![Plugging a power supply into a Raspberry Pi.](https://www.raspberrypi.com/documentation/computers/images/peripherals/cable-power.png)

将电源适配器插入标有 "POWER IN"、"PWR IN" 或 "PWR" 的端口。一些树莓派型号，如 Zero 系列，具有与电源端口相同外形尺寸的输出 USB 端口。请确保在树莓派上使用正确的端口！

### 引导介质

树莓派型号缺乏内置存储，因此您需要提供它。您可以从安装在任何支持的介质上的操作系统映像引导您的树莓派：通常使用 microSD 卡，但也可以使用 USB 存储、网络存储和通过 PCIe HAT 连接的存储。然而，只有最近的树莓派型号支持所有这些介质类型。

自树莓派 1 Model A+ 以来的所有树莓派消费者型号都配备了 microSD 插槽。当插槽中插入卡片时，您的树莓派会自动从 microSD 插槽引导。

![Inserting a microSD card into a Raspberry Pi.](https://www.raspberrypi.com/documentation/computers/images/peripherals/sd-card.png)

#### 推荐的 SD 卡

我们建议在树莓派 OS 安装时使用至少 32GB 存储空间的 SD 卡。对于树莓派 OS Lite，我们建议至少 16GB。您可以使用任何容量小于 2TB 的 SD 卡。由于 MBR 的限制，目前不支持超过 2TB 的容量。与任何其他启动介质一样，读写速度更快的 SD 卡将提供更好的性能。

由于硬件限制，以下设备只能从 256GB 或更小的引导分区启动：

* 树莓派 Zero
* 树莓派 1
* BCM2836 SoC 的早期树莓派 2 型号

其他操作系统有不同的要求。检查您操作系统的文档以获取容量要求。

### 键盘

您可以使用树莓派上的任何 USB 端口连接有线键盘或 USB 蓝牙接收器。

![Plugging a keyboard into a Raspberry Pi.](https://www.raspberrypi.com/documentation/computers/images/peripherals/cable-key.png)

### 鼠标

您可以使用树莓派上的任何 USB 端口连接有线鼠标或 USB 蓝牙接收器。

![Plugging a mouse into a Raspberry Pi.](https://www.raspberrypi.com/documentation/computers/images/peripherals/cable-mouse.png)

### 显示器

树莓派型号具有以下显示连接功能：

| 型号                    | 显示输出                                             |
| ------------------------- | ------------------------------------------------------ |
| 树莓派 5                | 2× 微型 HDMI                                        |
| 树莓派 4（所有型号）    | 2× 微型 HDMI，音频和复合输出通过 3.5 毫米 TRRS 插孔 |
| 树莓派 3（所有型号）    | HDMI，音频和复合输出通过 3.5 毫米 TRRS 插孔          |
| 树莓派 2 (所有型号)     | 通过 3.5 毫米 TRRS 插孔进行 HDMI、音频和复合输出     |
| 树莓派 1 Model B+       | 通过 3.5 毫米 TRRS 插孔进行 HDMI、音频和复合输出     |
| 树莓派 1 型 A+          | 通过 3.5 毫米 TRRS 插孔进行 HDMI、音频和复合输出     |
| 树莓派 Zero（所有型号） | 迷你 HDMI                                            |

| NOTE | 没有树莓派型号支持通过 USB-C 进行视频传输（DisplayPort 替代模式）。 |
| ------ | --------------------------------------------------------------------- |

如果您的树莓派有多个 HDMI 端口，请将主显示器插入标有 HDMI0 的端口。

大多数显示器没有 micro 或 mini HDMI 端口。但是，您可以使用 micro-HDMI 至 HDMI 电缆或 mini-HDMI 至 HDMI 电缆将树莓派上的这些端口连接到任何 HDMI 显示器。对于不支持 HDMI 的显示器，请考虑使用将 HDMI 显示输出转换为显示器支持的端口的适配器。

![Plugging a micro HDMI cable into a Raspberry Pi.](https://www.raspberrypi.com/documentation/computers/images/peripherals/cable-hdmi.png)

### 音频

所有树莓派型号都支持通过 HDMI、micro HDMI 或 mini HDMI 输出音频。所有树莓派型号都支持通过 USB 输出音频。所有配备蓝牙的树莓派型号支持蓝牙音频。树莓派 1、2、3 和 4 的所有变种都包括一个 3.5 毫米的 TRRS 耳机插孔，可能需要放大才能获得足够的输出音量。

### 网络

以下树莓派型号配备了 Wi-Fi 和蓝牙连接功能：

* 树莓派 5
* 树莓派 4
* 树莓派 3B+
* 树莓派 3
* 树莓派 Zero W
* Rsapberry Pi Zero 2 W

“Model B”后缀表示带以太网端口的变体；“Model A”表示没有以太网端口。如果您的树莓派没有以太网端口，您仍然可以使用 USB 转以太网适配器连接有线互联网。

![Plugging an Ethernet cable into a Raspberry Pi.](https://www.raspberrypi.com/documentation/computers/images/peripherals/cable-net.png)

## 安装操作系统

 在 GitHub 上编辑

要使用您的树莓派，您需要一个操作系统。默认情况下，树莓派会检查插入 SD 卡槽中的任何 SD 卡上是否有操作系统。

根据您的树莓派型号，您还可以从其他存储设备引导操作系统，包括 USB 驱动器、通过 HAT 连接的存储和网络存储。

要为您的树莓派在存储设备上安装操作系统，您需要：

* 一个可以用来将存储设备镜像到引导设备中的计算机
* 将您的存储设备插入该计算机的一种方式

大多数树莓派用户选择 microSD 卡作为他们的引导设备。

我们建议使用树莓派镜像工具安装操作系统。

树莓派镜像工具是一个帮助您在 macOS、Windows 和 Linux 上下载和写入镜像的工具。镜像工具包含许多流行的树莓派操作系统镜像。镜像工具还支持加载直接从树莓派或第三方供应商（如 Ubuntu）下载的镜像。您可以使用镜像工具预配置树莓派的凭据和远程访问设置。

镜像工具支持打包在 .img 格式中的镜像，以及像 .zip 这样的容器格式。

如果您没有其他计算机来将映像写入启动设备，您可以直接从互联网在您的树莓派上安装操作系统。

### 使用 Imager 安装

您可以通过以下方式安装 Imager：

* 从树莓派官网/raspberrypi.com/software 下载最新版本并运行安装程序。
* 通过终端使用您的软件包管理器安装，例如 sudo apt install rpi-imager 。

安装 Imager 后，通过单击树莓派 Imager 图标或运行 rpi-imager 启动应用程序。

![Raspberry Pi Imager main window.](https://www.raspberrypi.com/documentation/computers/images/imager/welcome.png)

单击“选择设备”，然后从列表中选择您的树莓派型号。

![Raspberry Pi model selections in Imager.](https://www.raspberrypi.com/documentation/computers/images/imager/choose-model.png)

接下来，单击“选择操作系统”，然后选择要安装的操作系统。Imager 始终在列表顶部显示推荐的树莓派 OS 版本供您的型号选择。

![Operating system selections in Imager.](https://www.raspberrypi.com/documentation/computers/images/imager/choose-os.png)

将首选存储设备连接到计算机。例如，使用外部或内置 SD 卡读卡器插入 microSD 卡。然后，单击“选择存储”，选择您的存储设备。

| WARNING | 如果您的计算机连接了多个存储设备，请务必选择正确的设备！通常可以通过大小识别存储设备。如果不确定，请断开其他设备，直到确定要制作映像的设备。 |
| --------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |

![Storage selection options in Imager.](https://www.raspberrypi.com/documentation/computers/images/imager/choose-storage.png)

 接下来，点击“下一步”。

![Imager prompt to open OS customisation menu.](https://www.raspberrypi.com/documentation/computers/images/imager/os-customisation-prompt.png)

在弹出窗口中，Imager 将要求您应用操作系统定制。我们强烈建议通过操作系统定制设置配置您的树莓派。单击“编辑设置”按钮打开操作系统定制。

如果您不通过操作系统定制设置配置您的树莓派，树莓派 OS 将在首次启动期间的配置向导中要求您提供相同的信息。您可以单击“否”按钮跳过操作系统定制。

#### 操作系统定制

操作系统定制菜单允许您在首次启动之前设置您的树莓派。您可以预先配置：

* 用户名和密码
* Wi-Fi 凭据
* 设备主机名
* 时区
* 键盘布局
* 远程连接

当您首次打开 OS 自定义菜单时，您可能会看到一个提示，询问是否允许从主机计算机加载 Wi-Fi 凭据。如果您回答“是”，Imager 将从您当前连接的网络预填 Wi-Fi 凭据。如果您回答“否”，您可以手动输入 Wi-Fi 凭据。

主机名选项定义了您的树莓派使用 mDNS 在网络上广播的主机名。当您将树莓派连接到网络时，网络上的其他设备可以使用 <hostname>.local 或 <hostname>.lan 与您的计算机通信。

用户名和密码选项定义了树莓派上管理员用户帐户的用户名和密码。

无线局域网选项允许您输入无线网络的 SSID（名称）和密码。如果您的网络不公开广播 SSID，则应启用“隐藏 SSID”设置。默认情况下，Imager 使用您当前所在的国家作为“无线局域网国家”。此设置控制树莓派使用的 Wi-Fi 广播频率。如果您计划运行无头树莓派，请为无线局域网选项输入凭据。

区域设置选项允许您为您的树莓派定义时区和默认键盘布局。

![General settings in the OS customisation menu.](https://www.raspberrypi.com/documentation/computers/images/imager/os-customisation-general.png)

服务选项卡包括帮助您远程连接到树莓派的设置。

如果您计划通过网络远程使用您的树莓派，请勾选“启用 SSH”旁边的复选框。如果您计划运行一个无显示器的树莓派，您应该启用此选项。

* 选择密码验证选项，使用您在 OS 定制的常规选项卡中提供的用户名和密码通过网络 SSH 到您的树莓派。
* 选择仅允许公钥验证，为您的树莓派预配置无密码公钥 SSH 验证，使用您当前使用的计算机上的私钥。如果您的 SSH 配置中已经有 RSA 密钥，Imager 将使用该公钥。如果没有，您可以单击“运行 SSH-keygen”生成公/私钥对。Imager 将使用新生成的公钥。

![Services settings in the OS customisation menu.](https://www.raspberrypi.com/documentation/computers/images/imager/os-customisation-services.png)

OS 定制还包括一个“选项”菜单，允许您在写入过程中配置 Imager 的行为。这些选项允许您在 Imager 完成验证图像时播放声音，自动在验证后卸载存储介质，并禁用遥测。

![Options in the OS customisation menu.](https://www.raspberrypi.com/documentation/computers/images/imager/os-customisation-options.png)

#### 写入

当您完成输入 OS 定制设置后，请单击“保存”以保存您的定制。

然后，在将映像写入存储设备时，单击“是”应用 OS 自定义设置。

最后，回答“您确定要继续吗？”弹出窗口中的“是”，开始向存储设备写入数据。

![Confirming a reimage of a storage device in Imager.](https://www.raspberrypi.com/documentation/computers/images/imager/are-you-sure.png)

如果看到一个要求权限以读取和写入存储介质的管理员提示，请授予 Imager 权限以继续。

![Writing an image to a device in Imager.](https://www.raspberrypi.com/documentation/computers/images/imager/writing.png)

去喝杯咖啡或散散步。这可能需要几分钟。

![Verifying an image on a device in Imager.](https://www.raspberrypi.com/documentation/computers/images/imager/stop-ask-verify.png)

如果你想要冒险一下，可以点击取消验证来跳过验证过程。

当你看到“写入成功”弹出窗口时，表示镜像已完全写入和验证。现在你可以从存储设备启动树莓派了！

![The screen Imager shows when it finishes writing an image to a storage device.](https://www.raspberrypi.com/documentation/computers/images/imager/finished.png)

接下来，继续进行第一次启动配置说明，让您的树莓派运行起来。

### 通过网络安装

网络安装使树莓派能够使用通过网络下载的树莓派 Imager 版本在存储设备上安装操作系统。通过网络安装，您可以在树莓派上安装操作系统，无需单独的 SD 卡阅读器，也无需除树莓派之外的计算机。您可以在任何兼容的存储设备上运行网络安装，包括 SD 卡和 USB 存储设备。

仅适用于树莓派 4、400 和 5 的网络安装。如果您的树莓派使用较旧的引导加载程序，您可能需要更新引导加载程序以使用网络安装。

网络安装需要以下内容：

* 支持网络安装的固件运行的兼容树莓派型号
* 一个显示器
* 一个键盘
* 一个有线网络连接

要启动网络安装，请在以下配置中按住 SHIFT 键并打开您的树莓派电源：

* 没有可引导的存储设备
* 连接的键盘
* 连接兼容的存储设备，如 SD 卡或 USB 存储

![The Network Install screen.](https://www.raspberrypi.com/documentation/computers/images/network-install-1.png)

如果您尚未将树莓派连接到互联网，请使用以太网电缆连接。

![Starting Network Install.](https://www.raspberrypi.com/documentation/computers/images/network-install-2.png)

一旦连接到互联网，您的树莓派将下载树莓派安装程序。如果下载失败，您可以重复该过程再试一次。

![Downloading Imager using Network Install.](https://www.raspberrypi.com/documentation/computers/images/network-install-3.png)

一旦您完成下载树莓派安装程序，您的树莓派将自动启动树莓派镜像工具。有关运行树莓派镜像工具的更多信息，请参阅安装操作系统。

![Choose a storage device.](https://www.raspberrypi.com/documentation/computers/images/network-install-4.png)

有关网络安装配置的更多信息，请参阅 HTTP 引导。

## 设置您的树莓派

 在 GitHub 上编辑此内容

安装操作系统映像后，将存储设备连接到您的树莓派。

首先，拔掉树莓派的电源适配器，确保在连接外围设备时树莓派已关机。如果您在 microSD 卡上安装了操作系统，现在可以将其插入树莓派的卡槽。如果您在其他任何存储设备上安装了操作系统，现在可以将其连接到树莓派。

![Inserting a microSD card into a Raspberry Pi.](https://www.raspberrypi.com/documentation/computers/images/peripherals/sd-card.png)

然后，插入任何其他外围设备，如鼠标、键盘和显示器。

![Attaching the power supply to a Raspberry Pi.](https://www.raspberrypi.com/documentation/computers/images/peripherals/cable-all.png)

最后，将电源连接到您的树莓派。当您的树莓派开机时，您应该看到状态 LED 亮起。如果您的树莓派连接到显示器，您应该在几分钟内看到启动屏幕。

## 首次启动配置

如果您在 Imager 中使用了 OS 自定义来预配置您的树莓派，恭喜！您的设备已经准备就绪。继续下一步，了解如何充分利用您的树莓派。

如果您的树莓派在 5 分钟内无法启动，请检查状态 LED。如果 LED 在闪烁，请查看 LED 警告闪烁代码以获取更多信息。如果您的树莓派拒绝启动，请尝试以下缓解措施：

* 如果您使用的是除 SD 卡以外的启动设备，请尝试从 SD 卡启动
* 重新为您的 SD 卡重新映像; 确保在 Imager 中完成整个验证步骤
* 更新您的树莓派上的引导加载程序，然后重新为您的 SD 卡重新映像

如果您选择在 Imager 中跳过 OS 定制，则您的树莓派将在首次启动时运行配置向导。您需要一个显示器和键盘来浏览向导; 鼠标是可选的。

![Click Next to get started with configuration.](https://www.raspberrypi.com/documentation/computers/images/initial-setup/start.png)

### 蓝牙

如果您正在使用蓝牙键盘或鼠标，此步骤将引导您完成设备配对。您的树莓派将扫描可配对的设备，并连接到找到的第一个设备。

此过程适用于内置或外部 USB 蓝牙适配器。如果您使用 USB 适配器，请在启动树莓派之前插入它。

### 语言环境

此页面可帮助您配置国家、语言、时区和键盘布局。

![Adjust country, language, time zone, and keyboard layout.](https://www.raspberrypi.com/documentation/computers/images/initial-setup/locale.png)

### 用户

此页面可帮助您配置默认用户帐户的用户名和密码。

默认情况下，旧版本的树莓派 OS 将用户名设置为"pi"。如果您使用用户名"pi"，请避免使用旧的默认密码"raspberry"，以保持您的树莓派安全。

![Create your username and password.](https://www.raspberrypi.com/documentation/computers/images/initial-setup/user.png)

### 无线网络

这个页面可以帮助您连接到 Wi-Fi 网络。从列表中选择您喜欢的网络。

![Selecting a wireless network.](https://www.raspberrypi.com/documentation/computers/images/initial-setup/network.png)

如果您的网络需要密码，您可以在这里输入。

![Entering a password for a wireless network.](https://www.raspberrypi.com/documentation/computers/images/initial-setup/network_password.png)

### 浏览器

此页面允许您选择将 Firefox 或 Chromium 作为默认的互联网浏览器。您可以选择卸载您未设置为默认的浏览器。

![The Choose Browser page.](https://www.raspberrypi.com/documentation/computers/images/initial-setup/browser.png)

### 软件更新

一旦您的树莓派连接到互联网，此页面将帮助您将操作系统和软件更新到最新版本。在软件更新过程中，向导将删除非默认浏览器（如果您选择在浏览器选择步骤中卸载它）。更新可能需要几分钟时间。

![You can download the latest software updates during the wizard before you boot for the first time.](https://www.raspberrypi.com/documentation/computers/images/initial-setup/update.png)

![You can download the latest software updates during the wizard before you boot for the first time.](https://www.raspberrypi.com/documentation/computers/images/initial-setup/download.png)

当您看到弹出窗口指示系统已经更新，请点击“确定”继续下一步。

### 完成

在配置向导结束时，点击“重新启动”来重启您的树莓派。您的树莓派将应用您的配置并启动到桌面。

![The Setup Complete dialogue prompts to restart your Raspberry Pi.](https://www.raspberrypi.com/documentation/computers/images/initial-setup/restart.png)

## 下一步

 在 GitHub 上编辑此内容

树莓派已设置并准备就绪，接下来做什么？

### 推荐软件

树莓派操作系统预装许多基本应用程序，因此您可以立即开始使用它们。如果您想利用我们认为有用的其他应用程序，请单击屏幕左上角的树莓图标。选择首选项 > 推荐软件，您将找到软件包管理器。您可以在此免费安装各种推荐软件。

![Opening the package manager GUI in Raspberry Pi OS](https://www.raspberrypi.com/documentation/computers/images/recommended-software.png)

例如，如果您计划将树莓派用作家用电脑，您可能会发现 LibreOffice 用于编写和编辑文档和电子表格非常有用。您还可以通过诸如屏幕放大器和 Orca 屏幕阅读器之类的应用程序使树莓派更易于访问，这些应用程序位于通用访问下。

### 教程

我们的教程展示了您可以如何使用您的新计算机的各种方式。您可以通过跟随激发您兴趣的教程来学习编码、控制外部设备，并构建令人兴奋的新项目。

### 支持

对于官方树莓派产品的支持，或者与其他树莓派用户联系，请访问树莓派论坛。

### 进一步阅读

![](https://www.raspberrypi.com/documentation/computers/images/fifth-editon-cover.png)[https://store.rpipress.cc/products/the-official-raspberry-pi-beginners-guide-5th-edition](https://store.rpipress.cc/products/the-official-raspberry-pi-beginners-guide-5th-edition)

您可以在 Gareth Halfacree 的最新版《官方树莓派初学者指南》中找到有关如何开始使用树莓派的更多信息。

 学习如何：

* 设置您的树莓派，安装其操作系统，并开始使用这台功能齐全的计算机。
* 使用 Scratch 3、Python 和 MicroPython 编程语言，通过逐步指南开始编码项目。
* 尝试连接电子元件，并乐在其中创造令人惊叹的项目。

第五版的新内容：

* 针对最新的树莓派计算机进行更新：树莓派 5 和树莓派 Zero 2 W。
* 包括最新的树莓派操作系统。
* 包含了关于树莓派 Pico 的新章节！

您可以在树莓派出版社网站上购买这本书。
