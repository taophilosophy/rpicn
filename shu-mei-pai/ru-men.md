# 入门

## 开始使用你的树莓派

{% embed url="https://www.bilibili.com/video/BV1TS411N7Fs" %}

 
要开始使用你的树莓派，你须准备以下物品：

* [电源适配器](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#power-supply)
* 启动介质（如[大容量高速内存卡](https://www.raspberrypi.com/documentation/computers/getting-started.html#recommended-sd-cards)）

你可以把树莓派配置成带桌面的交互式计算机，也可以将其配置为仅通过网络访问的无头设备（headless）。不需要其他外部设备，你就能无头设置树莓派：你可以[在安装操作系统](https://www.raspberrypi.com/documentation/computers/getting-started.html#installing-the-operating-system)时预先设置主机名、用户账户、网络连接和 SSH。但如果你要直接使用树莓派，还需以下其余配件：

* 显示器
* 用于将树莓派接入显示器的连接线
* 键盘
* 鼠标

### 电源适配器

下表列出了用于各种型号的树莓派供电所需的 USB-PD 电源适配器款式。你可使用其他能提供符合供电功率要求的高品质电源适配器来代替。

| 型号                    | 供电建议（电压/电流）     | 树莓派官方电源适配器 |
| :-------------------------: | :-----------------------------------: | :------------------: |
| 树莓派 5                | 5V/5A、5V/3A（将外部设备限制至 600mA） | [27W USB Type-C 电源适配器](https://www.raspberrypi.com/products/27w-power-supply/)                 |
| 树莓派 4B        | 5V/3A                             | [15W USB Type-C 电源适配器](https://www.raspberrypi.com/products/type-c-power-supply/)                 |
| 树莓派 3（所有型号）    | 5V/2.5A                           | [12.5W Mirco USB 电源适配器](https://www.raspberrypi.com/products/micro-usb-power-supply/)                 |
| 树莓派 2（所有型号）    | 5V/2.5A                           | [12.5W Mirco USB 电源适配器](https://www.raspberrypi.com/products/micro-usb-power-supply/)                 |
| 树莓派 1（所有型号）    | 5V/2.5A                           | [12.5W Mirco USB 电源适配器](https://www.raspberrypi.com/products/micro-usb-power-supply/)                 |
| 树莓派 Zero（所有型号） | 5V/2.5A                           | [12.5W Mirco USB 电源适配器](https://www.raspberrypi.com/products/micro-usb-power-supply/)                 |

![将电源接入树莓派](../.gitbook/assets/cable-power.png)

请将电源适配器接入树莓派（接口标有“POWER IN”、“PWR IN”或“PWR”）。某些型号的树莓派（如 Zero 系列），其 USB 输出接口的规格与电源接口相同。请确保你在树莓派上所使用的接口是正确的！

### 启动介质

树莓派不带内置存储，故需要你来提供启动介质。你可以用在受支持的介质上安装的操作系统，来启动你的树莓派：一般用内存卡，亦可用 USB 存储设备、网络存储设备及用 PCIe 扩展板转接的存储设备。但是，只有最新款的树莓派才能支持上述所有类型。

自树莓派 1A+ 以降，所有消费者型号的树莓派都搭载了内存卡槽。在卡槽中插入内存后，你的树莓派就能自动从内存卡启动。

![将内存卡卡插入树莓派](../.gitbook/assets/sd-card.png)

#### 推荐的内存卡

我们建议，用于安装树莓派系统（Raspberry Pi OS）的内存卡，存储容量至少为 32GB（对于精简版树莓派系统（Raspberry Pi OS Lite），建议至少为 16GB）。你可以使用任何容量不大于 2TB 的内存卡。由于 MBR 的限制，目前不支持大于 2TB 的容量。同所有其他启动介质一样，读写速度更快的内存卡性能也更佳。

由于硬件所限，以下设备仅可从 256GB（及更小）的启动分区上启动：

* 树莓派 Zero
* 树莓派 1
* 基于 BCM2836 SoC 的早期树莓派 2 

其他操作系统需求可能各异。请查阅你使用的操作系统文档来了解容量需求。

### 键盘

你可以使用树莓派上的任一 USB 接口来连接[有线键盘](https://www.raspberrypi.com/products/raspberry-pi-keyboard-and-hub/)及 USB 蓝牙接收器。

![将键盘插入树莓派](../.gitbook/assets/cable-key.png)

### 鼠标

你可以使用树莓派上的任一 USB 接口来连接[有线鼠标](https://www.raspberrypi.com/products/raspberry-pi-mouse/)及 USB 蓝牙接收器。

![将鼠标插入树莓派](../.gitbook/assets/cable-mouse.png)

### 显示器

树莓派支持以下显示输出功能：

| 型号                    | 显示输出                                             |
| :-------------------------: | :------------------------------------------------------: |
| 树莓派 5                | micro HDMI ×2                                       |
| 树莓派 4（所有型号）    | micro HDMI ×2，可使用 3.5 mm [TRRS 插孔](http://en.wikipedia.org/wiki/Phone_connector_(audio)#TRRS_standards)进行音频和复合输出 |
| 树莓派 3（所有型号）    | HDMI，可使用 3.5 mm [TRRS 插孔](http://en.wikipedia.org/wiki/Phone_connector_(audio)#TRRS_standards)进行音频和复合输出          |
| 树莓派 2 (所有型号)     | 可使用 3.5 mm [TRRS 插孔](http://en.wikipedia.org/wiki/Phone_connector_(audio)#TRRS_standards)进行 HDMI、音频和复合输出     |
| 树莓派 1B+       | 可使用 3.5 mm [TRRS 插孔](http://en.wikipedia.org/wiki/Phone_connector_(audio)#TRRS_standards)进行 HDMI、音频和复合输出     |
| 树莓派 1A+          | 可使用 3.5 mm [TRRS 插孔](http://en.wikipedia.org/wiki/Phone_connector_(audio)#TRRS_standards)进行 HDMI、音频和复合输出     |
| 树莓派 Zero（所有型号） | mini HDMI                                            |

>**注意**
>
>所有型号的树莓派都不支持 USB-C 视频传输（DisplayPort alt mode）。

如果你的树莓派有多个 HDMI 接口，请将主显示器插入到标有 `HDMI0` 的那个口。

常见的显示器都不支持 micro HDMI，亦不支持 mini HDMI。但是，你可以用 [micro-HDMI-to-HDMI 转换线](https://www.raspberrypi.com/products/micro-hdmi-to-standard-hdmi-a-cable/) 和 [mini-HDMI-to-HDMI 转换线](https://www.raspberrypi.com/products/standard-hdmi-a-male-to-mini-hdmi-c-male-cable/)来把树莓派上的这些接口转接至 HDMI 显示器。如果显示器不支持 HDMI，请考虑用转换器将 HDMI 输出转为该设备所支持的类型。

![把 micro HDMI 线插入树莓派](../.gitbook/assets/cable-hdmi.png)

### 音频

所有型号的树莓派都能通过 HDMI、micro HDMI（或 mini HDMI）进行音频输出，且都支持通过 USB 进行音频输出。所有搭载了蓝牙的树莓派都支持蓝牙音频。所有基于树莓派 1、2、3 和 4 的型号都有一个 3.5 mm 的 [TRRS](http://en.wikipedia.org/wiki/Phone_connector_(audio)#TRRS_standards) AUX 耳机插孔，但可能需要用放大器才能得到足够大的音量输出。

### 网络

如下型号的树莓派配备了 WiFi 和蓝牙连接功能：

* 树莓派 5
* 树莓派 4
* 树莓派 3B+
* 树莓派 3
* 树莓派 Zero W
* 树莓派 Zero 2 W

后缀“B”代表带以太网接口的版本；而 “A”代表不带以太网接口。如果你的树莓派没有以太网接口，你还可以用 USB 转以太网转换器来连接有线互联网。

![把以太网线接入树莓派](../.gitbook/assets/cable-net.png)

## 安装操作系统

如果你要使用树莓派，还需要操作系统。在默认情况下，树莓派会在卡槽里的内存卡中进行查找，看是否有操作系统。

视你的树莓派型号而定，也许你还能用别的存储设备来启动操作系统，比如 USB 设备、网络存储及与扩展板连接的存储设备。

要让存储设备提供树莓派操作系统，你需要：

* 能把镜像写入到该存储设备的计算机
* 把你的存储设备连接到该计算机的方法

大多数树莓派用户会选择把存储卡用作他们的启动设备。

我们建议用树莓派启动盘制作工具来安装操作系统。

树莓派启动盘制作工具是一款帮助你在 macOS、Windows 和 Linux 上下载和写入镜像的软件。树莓派启动盘制作工具涉及了许多常见的树莓派操作系统镜像。树莓派启动盘制作工具还能直接加载已下载的镜像，比如[树莓派](https://ubuntu.com/download/raspberry-pi)和第三方供应商（如 [Ubuntu](https://ubuntu.com/download/raspberry-pi)）。你可以使用树莓派启动盘制作工具预配置树莓派的凭据，设定远程访问。

树莓派启动盘制作工具亦兼容打包为 `.img` 格式的镜像，以及像 `.zip` 这样的压缩文件。

如果你没有能把镜像写入到存储设备的计算机，你可以通过互联网直接在你的树莓派上安装操作系统。

### 使用树莓派启动盘制作工具

你可以通过以下方式安装树莓派启动盘制作工具：

* 从树莓派官网 [raspberrypi.com/software](https://www.raspberrypi.com/software/) 下载最新版本并运行安装程序。
* 通过终端使用包管理器安装，如 `sudo apt install rpi-imager`。

树莓派启动盘制作工具安装完成后，通过单击树莓派启动盘制作工具图标或执行 `rpi-imager` 来启动应用程序。

![树莓派启动盘制作工具主窗口](https://www.raspberrypi.com/documentation/computers/images/imager/welcome.png)

单击“**选择设备（Choose device）**”，然后从列表中选择你的树莓派型号。

![在树莓派启动盘制作工具中选择树莓派的型号](https://www.raspberrypi.com/documentation/computers/images/imager/choose-model.png)

接下来，单击“**选择操作系统（Choose OS）**”，然后选择要安装的操作系统。树莓派启动盘制作工具将始终在列表最上方显示树莓派系统（树莓派系统），那是适用于你树莓派型号的推荐版本。

![在树莓派启动盘制作工具中选择操作系统](https://www.raspberrypi.com/documentation/computers/images/imager/choose-os.png)

将所选存储设备接入计算机。如果使用外部或内置 SD 卡读卡器，请插入 microSD 卡。然后，单击“**选择存储设备（Choose storage）**”，选择你的存储设备。

>**警告**
>
>如果你的计算机接入了多个存储设备，**请务必选择那个正确的设备！** 通常可以用大小来识别存储设备。如不确定，请断开其他设备，直到能确定要刻录镜像的设备。

![在树莓派启动盘制作工具中选择存储设备](https://www.raspberrypi.com/documentation/computers/images/imager/choose-storage.png)

 接下来，点击“**下一步（Next）**。

![在树莓派启动盘制作工具中打开操作系统定制](https://www.raspberrypi.com/documentation/computers/images/imager/os-customisation-prompt.png)

在弹出窗口中，树莓派启动盘制作工具将要求你应用操作系统设置。我们强烈建议通过操作系统定制设置配置你的树莓派。单击“编辑设置（Edit Settings）”按钮打开操作系统定制（ OS customisation）。

如果你没有用操作系统定制这个功能来配置你的树莓派，树莓派系统会在首次启动时的配置向导中，要求你再次提供。你可以单击选项“否（No）”来跳过操作系统自定义。

#### 操作系统定制

操作系统定制菜单能让你在首次开机之前，对你的树莓派进行设置。你可以预先配置：

* 用户名和密码
* Wi-Fi 凭据
* 设备主机名
* 时区
* 键盘布局
* 远程连接

当你首次打开系统自定义菜单时，你可能会看到一个提示，询问你是否允许从计算机加载 Wi-Fi 凭据。如果你回答“确认”，启动盘制作工具将从你当前连接的网络预填 Wi-Fi 凭据。如果你回答“否”，你可手动输入 Wi-Fi 凭据。

**主机名（hostname）** 参数设定了你的树莓派在网络上广播的主机名（使用 [mDNS](https://en.wikipedia.org/wiki/Multicast_DNS)）。当你把树莓派接入网络后，网络上的其他设备就可以使用 `<你的主机名>.local` 或 `<你的主机名>.lan` 与你的树莓派进行通信。

**用户名（username）和密码（password）** 参数设定了树莓派上管理员用户账户的用户名和密码。

**无线局域网（wireless LAN）** 参数能让你输入无线网络的 SSID（网络名称）和密码。如果你的网络不公开广播 SSID，则应启用“隐藏 SSID”设置。默认情况下，制作工具使用你当前所在的国家作为“无线局域网国家/区域”。此设置控制树莓派使用的 Wi-Fi 广播频率。如果你打算运行无头树莓派，请为无线局域网选项输入凭据。

**区域设置（ locale settings）** 参数能为你的树莓派设定时区和默认键盘布局。

![操作系统自定义菜单的常规设置](https://www.raspberrypi.com/documentation/computers/images/imager/os-customisation-general.png)

选项 **服务（Services）** 涉及帮助你远程连接到树莓派的设置。

如果你打算用网络远程使用你的树莓派，请勾选“启用 SSH（Enable SSH）”旁边的方框。或者说，如果你想要不依赖显示器直接运行树莓派，请启用该功能。

* 选择 **密码验证（password authentication）** 参数，可使用你在 OS 定制的常规选项卡中提供的用户名和密码通过网络 SSH 到你的树莓派。
* 选择 **仅允许公钥验证（Allow public-key authentication only ）**，可为你的树莓派预配置无密码，仅公钥的 SSH 验证，默认会使用你当前计算机上的私钥。如果你的 SSH 配置中已经有 RSA 密钥，制作工具将使用该公钥。如果没有，你可以单击“**运行 SSH-keygen（Run SSH-keygen）**”来生成公、私钥对。制作工具会使用新生成的公钥。

![操作系统定制菜单中的服务设置](https://www.raspberrypi.com/documentation/computers/images/imager/os-customisation-services.png)

系统定制还包括“**选项（Options）**”菜单，能让你在写入过程中配置制作工具的操作。这些选项能让你在制作工具完成镜像校验时播放声音，在校验后自动卸载存储介质，及禁用遥测。

![操作系统自定义菜单选项](https://www.raspberrypi.com/documentation/computers/images/imager/os-customisation-options.png)

#### 写入

当你完成输入系统定制设置后，可单击“**保存（Save）**”来保存你的定制选项。

然后，在将镜像写入存储设备时，可单击“**确认（Yes）**”应用系统自定义设置。

最后，回答“你确定要继续吗？（`Are you sure you want to continue?`）”弹出窗口中的“**确认（Yes）**”，开始向存储设备写入数据。

![在启动盘制作工具中再次确认要写入镜像的存储设备](https://www.raspberrypi.com/documentation/computers/images/imager/are-you-sure.png)

如果看到要求管理员权限以读取和写入存储介质的提示，要继续，请授予制作工具权限。

![在启动盘制作工具中向设备写入镜像](https://www.raspberrypi.com/documentation/computers/images/imager/writing.png)

>这可能需要几分钟。去喝杯咖啡，散散步吧。

![在启动盘制作工具中校验设备上的镜像](https://www.raspberrypi.com/documentation/computers/images/imager/stop-ask-verify.png)

>如果你想要找刺激，可以点击 **取消校验（cancel verify）** 来跳过校验过程。

当你看到“写入成功”弹出窗口时，表示镜像已完全写入和验证。现在你可以从存储设备启动树莓派了！

![当向存储设备的镜像写入完成时，屏幕上会显示制作工具。](https://www.raspberrypi.com/documentation/computers/images/imager/finished.png)

接下来，继续进行[首次启动配置说明](https://www.raspberrypi.com/documentation/computers/getting-started.html#configuration-on-first-boot)，让你的树莓派跑起来。

### 网络安装

网络安装能让树莓派使用来自树莓派制作工具以网络下载，并存储在设备上面的镜像，进行操作系统的安装。使用网络安装，你可以在树莓派上安装操作系统，从而无需任何 SD 卡读卡器及除树莓派之外的计算机。你可以在所有受支持的存储设备上运行网络安装——比如 SD 卡和 USB 存储设备。

网络安装仅适用于树莓派 4、400 和 5。如果你的树莓派的引导加载程序比较旧，你可能需要[更新引导加载程序](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#bootloader_update_stable)才能使用网络安装。

网络安装需要满足以下条件：

* 受支持的树莓派型号且安装了支持网络安装的固件
* 显示器
* 键盘
* 有线网络连接

要启动网络安装，请在以下配置的基础上，按住 ***SHIFT*** 键，同时打开你的树莓派电源：

* 存储设备尚未被写入镜像
* 已接入键盘
* 已接入兼容的存储设备，如 SD 卡、USB 存储设备

![网络安装界面](../.gitbook/assets/network-install-1.png)

如果你尚未将树莓派连接到互联网，请使用网线进行连接。

![开始网络安装](../.gitbook/assets/network-install-2.png)

连接到互联网后，你的树莓派会下载树莓派安装程序。如果下载失败，你可以重复该过程，再试一次。

![使用网络安装进行下载树莓派启动盘制作工具](../.gitbook/assets/network-install-3.png)

在树莓派启动盘制作工具下载完成后，你的树莓派将自动运行启动盘制作工具。有关运行启动盘制作工具的更多信息，请参阅[安装操作系统](https://www.raspberrypi.com/documentation/computers/getting-started.html#installing-the-operating-system)。

![选择存储设备](https://www.raspberrypi.com/documentation/computers/images/network-install-4.png)

有关网络安装配置的更多信息，请参阅 [HTTP 引导](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#http-boot)。

## 设置你的树莓派


操作系统镜像写入完成后，将存储设备接入至你的树莓派。

首先，拔掉树莓派的电源适配器插头，确保在连接外部设备时树莓派已关机。如果你在 microSD 卡上安装了操作系统，现在就可以将其插入树莓派的卡槽。如果你在其他存储设备上安装了操作系统，现在可以将其接入树莓派。

![将 microSD 卡插入树莓派](../.gitbook/assets/sd-card.png)

然后，插入所需的其他外部设备，如鼠标、键盘和显示器。

![将电源连接到树莓派](../.gitbook/assets/cable-all.png)

最后，把电源连接到你的树莓派。当你的树莓派开机时，你应该看到 LED 状态亮起。如果你的树莓派接入了显示器，你应该在几分钟内就能看到启动屏幕。

## 首次启动配置

如果你在启动盘制作工具中使用了系统自定义来预配置你的树莓派，**恭喜！** 你的设备已经准备就绪。可继续[下一步](https://www.raspberrypi.com/documentation/computers/getting-started.html#next-steps)，了解如何充分发挥你的树莓派。

如果你的树莓派在 5 分钟内仍无法启动，请检查 LED 状态灯。如果 LED 在闪烁，请查看 [LED 告警闪烁的代码以获取更多信息](https://www.raspberrypi.com/documentation/computers/configuration.html#led-warning-flash-codes)。如果你的树莓派不能启动，请尝试以下解决方案：

* 如果你的启动设备使用的不是 SD 卡，请先试试用 SD 卡启动
* [重新为你的 SD 卡写入镜像](https://www.raspberrypi.com/documentation/computers/getting-started.html#installing-the-operating-system); 确保在启动盘制作工具中进行了完整的校验步骤
* [更新你的树莓派上的引导加载程序](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#bootloader_update_stable)，然后[为你的 SD 卡再次写入镜像](https://www.raspberrypi.com/documentation/computers/getting-started.html#installing-the-operating-system)

如果你选择在启动盘制作工具中跳过了系统定制，则你的树莓派会在首次启动时运行配置向导。你需要显示器和键盘来设置向导（没有鼠标也能完成）。

![单击“下一步”开始配置](../.gitbook/assets/start.png)

### 蓝牙

如果你正在使用蓝牙键盘、蓝牙鼠标，此步骤将引导你完成设备配对。你的树莓派将扫描可配对的设备，并连接至第一个被扫描到的设备。

此过程适用于内、外置 USB 蓝牙适配器。如果你使用 USB 适配器，请在启动树莓派之前插入。

### 语言环境

此页可帮助你配置国家、语言、时区和键盘布局。

![调整国家/地区、语言、时区和键盘布局](https://www.raspberrypi.com/documentation/computers/images/initial-setup/locale.png)

### 用户

此页可帮助你配置默认用户账户的用户名和密码。

在默认情况下，旧版的树莓派系统会把用户名设置为“pi”。如果你使用的用户名是“pi”，请不要使用在旧系统中的默认密码，即“raspberry”，以确保你的树莓派是安全的。

![配置你的用户名和密码](https://www.raspberrypi.com/documentation/computers/images/initial-setup/user.png)

### 无线网络

该页可以帮助你连接到 Wi-Fi 网络。从列表中选择你需要的网络。

![选择你的网络](https://www.raspberrypi.com/documentation/computers/images/initial-setup/network.png)

如果你的网络需要密码验证，你可以在这里输入。

![输入无线网络密码](https://www.raspberrypi.com/documentation/computers/images/initial-setup/network_password.png)

### 浏览器

此页面能让你选择把默认互联网浏览器设置为 Firefox（火狐浏览器）还是 Chromium（开源的 Chrome）。对于不是你默认设置的那个浏览器，你可以选择卸载。

![选择浏览器](https://www.raspberrypi.com/documentation/computers/images/initial-setup/browser.png)

### 软件更新

在你的树莓派接入互联网后，此页能帮助你把操作系统和软件更新到最新版本。在软件更新过程中，向导会删除非默认浏览器（如果你选择了在浏览器步骤中卸载它）。可能需要几分钟时间才能完成更新。

![在首次启动前，你可以通过向导下载最新的软件更新](https://www.raspberrypi.com/documentation/computers/images/initial-setup/update.png)

![在首次启动前，你可以通过向导下载最新的软件更新](https://www.raspberrypi.com/documentation/computers/images/initial-setup/download.png)

当你看到弹出窗口指示系统已经更新，请点击“**确定（OK）**”继续下一步。

### 完成

在配置向导结束时，点击“**重启（Restart）**”来重启你的树莓派。你的树莓派将应用个性化并启动至桌面。

![设置完成对话框，提示重启树莓派](https://www.raspberrypi.com/documentation/computers/images/initial-setup/restart.png)

## 下一步
 

树莓派已设置并准备就绪，接下来做什么？

### 软件推荐

树莓派操作系统预装了许多基本应用程序，因此可以开箱即用。如果你想使用我们认为有用的其他软件，请单击屏幕左上角的树莓派图标。选择 **首选项（Preferences）** > **推荐软件（Recommended Software）**，你将找到软件包管理器。你可以在此免费安装各种推荐软件。

![在树莓派系统中打开图形界面的软件包管理器](../.gitbook/assets/recommended-software.png)

具体来说，如果你打算把树莓派当家用电脑用，你可能会需要 LibreOffice，它对于撰写和编辑文档和电子表格非常有用。你还可以通过诸如屏幕放大器和 Orca 屏幕阅读器之类的应用程序使树莓派更易于使用，这些应用程序位于通用访问下。

### 教程

[我们的教程](https://www.raspberrypi.com/tutorials/)向你介绍了各种方式，都是有关你的新树莓派如何使用的。你可以跟随那些能激发你兴趣的教程，来学习编程、控制外部设备，并构建令人兴奋的新项目。

### 支持

对于官方树莓派产品的支持，及与其他树莓派用户交流，请访问[树莓派论坛](https://forums.raspberrypi.com/?_gl=1*j1etrl*_ga*ODAwMTM3MTg4LjE3MTc1NzY1NTQ.*_ga_22FD70LWDS*MTcyMDY5NTU5OC4xOC4wLjE3MjA2OTU1OTguMC4wLjA.)。

### 进一步阅读

![树莓派官方初学者指南](https://www.raspberrypi.com/documentation/computers/images/fifth-editon-cover.png)

你可以在由 Gareth Halfacree 撰写的最新版《[树莓派官方初学者指南](https://store.rpipress.cc/collections/latest-releases/products/the-official-raspberry-pi-beginners-guide-5th-edition)》中找到有关如何开始使用树莓派的更多信息。

 可学习如何：

* 配置你的树莓派，为其安装操作系统，并开始使用这台功能齐全的计算机。
* 使用编程语言 Scratch 3、Python 和 MicroPython，通过逐步指南开始编程项目。
* 尝试连接电子元件，并乐在其中创造令人惊叹的项目。

第五版的新增内容：

* 针对最新的树莓派计算机进行更新：树莓派 5 和树莓派 Zero 2 W。
* 涉及最新的树莓派系统。
* 涉及树莓派 Pico 的新章节！

你可以在树莓派出版社的网站上[购买这本书](https://store.rpipress.cc/products/the-official-raspberry-pi-beginners-guide-5th-edition)。
