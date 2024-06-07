# 系统配置



## `raspi-config`

>**技巧**
>
>树莓派桌面用户可以在“首选项”>“树莓派配置”中访问此应用程序的图形版本。但是，一些高级配置仅在 raspi-config 中可用。 

raspi-config 可帮助您配置您的树莓派。不同树莓派型号之间的可用选项可能有所不同。要打开配置工具，请运行以下命令：

```
$ sudo raspi-config
```

您应该看到在灰色框中出现了一个带有选项的蓝色屏幕：


![raspi-config main screen](../.gitbook/assets/raspi-config.png)

使用上下箭头键在可用选项之间移动突出显示的选择。

按右箭头键或按 Tab 键选择 `<Select>` 和 `<Finish>` 按钮。按左箭头键或按 Tab 键返回选项。

raspi-config 可自动编辑 /boot/firmware/config.txt 和各种 Linux 配置文件。某些选项需要重新启动才能生效。如果您更改了其中任何一个， raspi-config 在退出时会要求您重新启动。

>**技巧**
>
>在选项值的长列表中（比如时区城市列表），输入单个字母会跳转到列表的相应部分。例如，输入 L 可跳转到里斯本。 

### 系统选项

系统选项子菜单可让您对引导、登录和网络过程的各个部分进行配置更改，以及一些其他系统级别的更改。

![raspi-config system options](../.gitbook/assets/raspi-system.png)

#### 无线局域网

配置 Wi-Fi SSID 和密码。

#### 音频

指定音频输出位置。

#### 密码

 更改您的密码。

获取更多信息，请参阅更改用户密码。

#### 主机名

在网络上为树莓派设置可见的 mDNS 域名。

#### 启动/自动登录

选择是启动到控制台还是桌面，以及在打开电源时是否自动登录到当前用户帐户。

#### 启动时的网络

在启动前等待网络连接。

#### 启动画面

启用或禁用启动时显示的启动画面。

#### 电源 LED

如果您的树莓派型号支持，可以更改电源 LED 的行为。

#### 浏览器

更改默认的网络浏览器。

### 显示选项

![raspi-config display options](../.gitbook/assets/raspi-display.png)

#### Underscan（欠扫描）

>**注意**
>
>Wayland 下不可用。 

如果屏幕上显示的初始文本消失在边缘，启用过扫描（overscan）以调整边框。在某些显示器上，特别是监视器上，禁用过扫描将使图像填满整个屏幕并去除黑边。

#### Screen blanking（屏幕空白）

启用或禁用屏幕空白。

#### VNC resolution（VNC 分辨率）

定义在无头设置中使用的视频分辨率。

#### Composite（复合）

启用或禁用复合视频。

#### 4Kp60 HDMI

启用或禁用 HDMI 的 4Kp60 分辨率输出。

### 接口参数

启用和禁用各种物理和虚拟接口。

![raspi-config interface options](../.gitbook/assets/raspi-interface.png)

#### SSH

启用或禁用使用 SSH 远程访问您的树莓派的终端。

SSH 允许您从另一台计算机远程访问树莓派的命令行。默认情况下，SSH 处于禁用状态。在 SSH 文档页面上阅读更多关于使用 SSH 的信息。如果将您的树莓派直接连接到公共网络，请不要启用 SSH，除非您为所有用户设置了安全密码。

#### VNC

启用或禁用 WayVNC 或 RealVNC 虚拟网络计算服务器。

#### SPI

启用或禁用 SPI 接口和自动加载 SPI 内核模块。

#### I2C

启用或禁用 I2C 接口和自动加载 I2C 内核模块。

#### 串行端口

在串行连接上启用或禁用 shell 和内核消息。

#### 1-Wire

启用或禁用 Dallas 1-wire 接口，通常用于 DS18B20 温度传感器。

#### 远程 GPIO

启用或禁用对 GPIO 引脚的远程访问。

### 性能选项

![raspi-config performance options](../.gitbook/assets/raspi-perf.png)

#### 超频

如果您的树莓派型号支持，可以对 CPU 进行超频。超频潜力因个别树莓派设备而异，即使是同一型号也会有所不同。超频过高可能会导致不稳定。

>**警告**
>
>**超频可能会缩短您树莓派的使用寿命。** 如果在某个特定级别超频导致系统不稳定，请尝试降低超频的程度。在启动过程中按住 Shift 键可临时禁用超频。 

#### GPU 内存

更改向 GPU 提供的内存量。

#### Overlay file system（堆叠文件系统）

启用或禁用只读文件系统。

#### 风扇

可自定义 GPIO 连接的树莓派 4 机箱风扇的行为。这不影响树莓派 5 机箱中的风扇或使用特殊四针风扇头连接的树莓派 5 主动散热器。

### 本地化选项

配置位置和与国家相关的选项。

![raspi-config localisation options](../.gitbook/assets/raspi-l18n.png)

#### 语言环境

选择一个语言环境，例如 en_GB.UTF-8 UTF-8 。

#### 时区

设置您的本地时区，从地区开始，然后选择一个城市，例如"Europe/London"。键入一个字母以跳转到列表中的该字母。

#### 键盘

打开一个菜单，您可以在其中选择您的键盘布局。更改通常会立即生效，但可能需要重新启动。键入一个字母以跳转到列表中的该字母。

#### 无线局域网国家

为您的无线网络设置国家代码。

### 高级选项

![raspi-config advanced options](../.gitbook/assets/raspi-adv.png)

#### 扩展文件系统

将您的操作系统分区扩展到填满整个存储设备，为您提供更多用于文件的空间。重新启动您的树莓派以完成此操作。通常，Raspberry Pi OS 在首次启动时运行此操作。如果您将您的操作系统克隆到容量大于原始设备的独立存储设备上，则此选项可能会很有用。

>**警告**
>
>它没有再确认的步骤。选择该选项将立即开始分区扩展。 

#### 网络接口名称

启用或禁用可预测的网络接口名称。

#### 网络代理设置

配置网络的代理设置。

#### 启动顺序

在树莓派 4 及更高版本上，如果未插入 SD 卡，指定是否从 USB 或网络引导。有关更多信息，请参阅引导加载程序配置。

#### 引导加载程序版本

在树莓派 4 及更高版本上，切换到最新的引导 ROM 软件。或者，如果最新版本引起问题，您可以恢复到出厂默认设置。

#### Wayland

在 X11 和 Wayland 后端之间切换。树莓派 4 及更高版本默认使用 Wayland；其他型号的树莓派默认使用 X11。

>**注意**
>
>要在树莓派 4 先前的型号上使用 Wayland，您还必须将 wayland=on 添加到 /boot/firmware/cmdline.txt 。 

#### 音频配置

在 Bookworm 之前，Raspberry Pi OS 使用 PulseAudio，现在可以在 PulseAudio 和 PipeWire 音频后端之间切换。

### 更新

将此工具更新到最新版本。

### 关于 raspi-config

显示 raspi-config 的描述。

### 完成

退出 raspi-config 。如果您进行了需要重新启动的更改， raspi-config 会提示您重新启动。首次实施更改时，最好重新启动。如果选择调整 SD 卡大小，重新启动可能需要比平常更长的时间。

## 非交互式 raspi-config

raspi-config 工具还支持非交互式选项和标志，可以在命令行上完全更改选项，没有可视化组件。可用选项在树莓派型号之间可能有所不同。

```
$ sudo raspi-config nonint <command> <arguments> [optional-argument]
```

>**注意**
>
>`0` 和 `1` 的含义在选项之间有所不同。在将值传递给选项之前，请始终参照文档。 

### 系统选项

#### 无线局域网

配置 Wi-Fi SSID 和密码。

```
$ sudo raspi-config nonint do_wifi_ssid_passphrase <ssid> <passphrase> [hidden] [plain]
```

传递无线网络名称（SSID）和密码（如果需要）。以下参数是可选的：

`<hidden>` 选项表示 SSID 的可见性。如果网络广播开放的 SSID，请传递 0 或省略该选项。如果您的 SSID 是隐藏的，请传递 1 。默认为 0 。

`<plain>` 选项指示您是否打算将密码作为明文传递。如果您的密码包含空格或类似 ! 的特殊字符，则必须传递 0 并在密码周围使用引号。否则，您可以传递 1 或省略该选项。默认为 1 。要传递此选项，您必须为 `<hidden>` 指定一个值。

例如，运行以下命令以连接到 a：

* 名为 myssid 的非隐藏网络，密码为 mypassphrase ：

  ```
  $ sudo raspi-config nonint do_wifi_ssid_passphrase myssid mypassphrase
  ```
* 使用密码 mypassphrase 的隐藏网络 myssid ：

  ```
  $ sudo raspi-config nonint do_wifi_ssid_passphrase myssid mypassphrase 1
  ```
* 使用密码 my passphrase 的非隐藏网络 myssid ：

  ```
  $ sudo raspi-config nonint do_wifi_ssid_passphrase myssid "my passphrase" 0 0
  ```

#### 音频

指定音频输出位置。

```
$ sudo raspi-config nonint do_audio <N>
```

在树莓派 4B 上，您可以使用以下选项：

* 0 ：bcm2835 headphone jack（耳机插孔）
* 1 ：vc4-hdmi-0
* 2 ：vc4-hdmi-1

要查看此选项的交互式 raspi-config 版本中使用的数字列表，请参阅可能的 `<N>` 值的完整列表。

#### 密码

 更改您的密码。

有关更改用户密码的更多信息，请参阅更改用户密码。

```
$ sudo raspi-config nonint do_change_pass
```

>**注意**
>
>此功能使用全屏交互式界面，即使从命令行参数运行也是如此。 

#### 主机名

在网络上为此树莓派设置可见的 mDNS 域名。

```
$ sudo raspi-config nonint do_hostname <hostname>
```

#### 启动/自动登录

选择是启动到控制台还是桌面，并且在打开电源时是否自动登录到当前用户帐户。

```
$ sudo raspi-config nonint do_boot_behaviour <B1/B2/B3/B4>
```

* B1 ：启动到控制台，需要登录
* B2 ：启动到控制台，自动登录
* B3 ：启动到桌面，需要登录
* B4 ：启动到桌面，自动登录

#### 启动时的网络

在允许启动继续之前等待网络连接。

```
$ sudo raspi-config nonint do_boot_wait <0/1>
```

* 0 ：在不等待网络连接的情况下启动
* 1 ：等待网络连接后启动

#### 启动画面

启用或禁用启动时显示的启动画面。

```
$ sudo raspi-config nonint do_boot_splash <0/1>
```

* 0 ：启用启动画面
* 1 ：禁用启动画面

#### 电源 LED

如果您的树莓派允许的话，可以更改电源 LED 的行为。

```
$ sudo raspi-config nonint do_leds <0/1>
```

* 0 ：闪烁以表示磁盘活动
* 1 ：始终点亮电源 LED

#### 浏览器

更改默认的网络浏览器。选择一个当前未安装的网络浏览器将无法工作。

```
$ sudo raspi-config nonint do_browser <chromium-browser/firefox>
```

### 显示选项

#### Underscan（欠扫描）

>在 Wayland 下不可用。 

如果屏幕上显示的初始文本消失在边缘，启用过扫描以调整边框。在某些显示器上，特别是监视器上，禁用过扫描将使图像填满整个屏幕并去除黑色边框。

```
$ sudo raspi-config nonint do_overscan_kms <device> <enabled>
```

 设备:

* `1`: HDMI-1
* `2`: HDMI-2

 启用：

* 0 ：启用过扫描
* 1 ：禁用过扫描

#### 屏幕空白

启用或禁用屏幕空白。

```
$ sudo raspi-config nonint do_blanking <0/1>
```

* 0 ：启用屏幕空白
* 1 ：禁用屏幕空白

#### VNC 分辨率

在无显示器设置中为 VNC 定义要使用的视频分辨率。

```
$ sudo raspi-config nonint do_vnc_resolution <width>x<height>
```

#### 复合

启用或禁用复合视频输出。

在树莓派 4 上：

```
$ sudo raspi-config nonint do_pi4video <V1/V2/V3>
```

* V1 ：启用 4Kp60 HDMI 输出
* V2 ：启用复合视频输出
* V3 ：禁用 4Kp60 和复合输出

 在其他型号上：

```
$ sudo raspi-config nonint do_composite <0/1>
```

* 0 ：启用复合视频
* 1 ：禁用复合视频

### 接口选项

#### SSH

使用 SSH 启用或禁用对树莓派的远程终端访问。

SSH 允许您从另一台计算机远程访问树莓派的命令行。有关 SSH 的更多信息，请参阅 SSH 文档。

```
$ sudo raspi-config nonint do_ssh <0/1>
```

* 0 ：启用 SSH
* 1 ：禁用 SSH

#### VNC

启用或禁用虚拟网络计算（VNC）服务器。有关 VNC 的更多信息，请参阅 VNC 文档。

```
$ sudo raspi-config nonint do_vnc <0/1>
```

* 0 ：启用 VNC
* 1 ：禁用 VNC

#### SPI

启用或禁用 SPI 接口和 SPI 内核模块的自动加载。

```
$ sudo raspi-config nonint do_spi <0/1>
```

* 0 ：启用 SPI
* 1 ：禁用 SPI

#### I2C

启用或禁用 I2C 接口和 I2C 内核模块的自动加载。

```
$ sudo raspi-config nonint do_i2c <0/1>
```

* 0 ：启用 I2C
* 1 ：禁用 I2C

#### 串行端口

启用或禁用串行连接硬件。

```
$ sudo raspi-config nonint do_serial_hw <0/1/2>
```

* 0 ：启用串行端口
* 1 ：禁用串行端口

#### 串行控制台

在串行连接上启用或禁用 shell 和内核消息。

```
$ sudo raspi-config nonint do_serial_cons <0/1/2>
```

* 0 ：启用串行端口上的控制台
* 1 ：禁用串行端口上的控制台

#### 1-wire

启用或禁用达拉斯 1-wire 接口。这通常用于 DS18B20 温度传感器。

```
$ sudo raspi-config nonint do_onewire <0/1>
```

* 0 ：启用 1-wire
* 1 ：禁用 1-wire

#### 远程 GPIO

启用或禁用对 GPIO 引脚的远程访问。

```
$ sudo raspi-config nonint do_rgpio <0/1>
```

* 0 ：启用远程 GPIO
* 1 ：禁用远程 GPIO

### 性能选项

#### 超频

如果您的树莓派型号允许，可以对 CPU 进行超频。即使是相同型号的树莓派设备，超频潜力也会有所不同。超频过高可能会导致不稳定。


>**警告**
>
>超频可能会缩短您树莓派的使用寿命。如果在某个水平上超频导致系统不稳定，请尝试更温和的超频。在启动时按住 Shift 键可临时禁用超频。

```
$ sudo raspi-config nonint do_overclock <setting>
```

此命令接受以下 <setting> 值：

* None ：无超频（默认）
* Modest ：超频至最大值的 50%
* Medium ：超频至最大值的 75%
* High ：超频至最大值的 100%
* Turbo ：超频至最大值的 125%

#### GPU 内存

更改向 GPU 提供的内存量。

```
$ sudo raspi-config nonint do_memory_split <megabytes>
```

#### 堆叠文件系统

启用或禁用只读文件系统。

```
$ sudo raspi-config nonint do_overlayfs <0/1>
```

* 0 ：启用覆盖文件系统
* 1 ：禁用覆盖文件系统

#### 风扇

自定义 GPIO 连接的树莓派 4 机箱风扇的行为。不影响树莓派 5 机箱中的风扇或使用特殊四针风扇头连接的树莓派 5 主动散热器。

```
$ sudo raspi-config nonint do_fan <0/1> [gpio] [onTemp]
```

* 0 ：启用风扇
* 1 ：禁用风扇

gpio 默认为 14 。

onTemp 默认为 80 摄氏度。

### 本地化选项

#### 语言环境

选择语言环境，例如 en_GB.UTF-8 UTF-8 。

```
$ sudo raspi-config nonint do_change_locale <locale>
```

要查看所有可用的 `<locale>` 值列表，请参阅此选项交互式 raspi-config 版本中使用的缩写。

#### 时区

设置您的本地时区，从地区开始，然后选择一个城市，例如"Europe/London"。

```
$ sudo raspi-config nonint do_change_timezone <timezone>
```

要查看此选项交互式 `<timezone>` 版本中使用的缩写的完整列表，请参见。

#### 键盘

设置键盘布局。更改通常会立即生效，但可能需要重新启动。

```
$ sudo raspi-config nonint do_configure_keyboard <keymap>
```

要查看可用的 `<keymap>` 值的完整列表，请参阅此选项交互 raspi-config 版本中使用的缩写。

#### 无线局域网国家

设置无线网络的国家代码。

```
$ sudo raspi-config nonint do_wifi_country <country>
```

要查看此选项交互式 raspi-config 版本中使用的缩写的可用 `<country>` 值的完整列表。

### 高级选项

#### 扩展文件系统

将您的操作系统分区扩展到填满整个存储设备，为您提供更多用于文件的空间。重启树莓派以完成此操作。通常，Raspberry Pi OS 在第一次启动时运行此操作。如果您将操作系统克隆到容量大于原始设备的独立存储设备上，则此选项可能很有用。

>**警告**
>
>没有再确认步骤。选择该选项将立即开始分区扩展。

```
$ sudo raspi-config nonint do_expand_rootfs
```

#### 网络接口名称

启用或禁用可预测的网络接口名称。

```
$ sudo raspi-config nonint do_net_names <0/1>
```

* 0 ：启用可预测的网络接口名称
* 1 ：禁用可预测的网络接口名称

#### 网络代理设置

配置网络代理设置。

```
$ sudo raspi-config nonint do_proxy <SCHEMES> <ADDRESS>
```

#### 启动顺序

在树莓派 4 及更高型号上，如果未插入 SD 卡，指定是否从 USB 或网络引导。有关更多信息，请参阅引导加载程序配置部分。

```
$ sudo raspi-config nonint do_boot_order <B1/B2/B3>
```

根据您的设备，您可以从以下选项中选择：

* B1 ：SD 卡启动 - 如果可用，则从 SD 卡启动，否则从 NVMe 启动，否则从 USB 启动
* B2 ：NVMe/USB 启动 - 如果可用，则从 NVMe 启动，否则从 USB 启动，否则从 SD 卡启动
* B3 ：网络引导 - 如果插入 SD 卡，则从 SD 卡引导，否则从网络引导

#### 引导加载程序版本

在树莓派 4 及更新型号上，切换到最新的引导 ROM 软件。或者，如果最新版本导致问题，可以恢复到出厂默认设置。

```
$ sudo raspi-config nonint do_boot_rom <E1/E2>
```

* E1 ：使用最新的引导 ROM
* E2 ：使用出厂默认设置

#### Wayland

在 X11 和 Wayland 后端之间切换。树莓派 4 及更新型号默认使用 Wayland；其他型号的树莓派默认使用 X11。

```
$ sudo raspi-config nonint do_wayland <W1/W2>
```

* W1 ：使用 X11 后端
* W2 ：使用 Wayland 后端

>**注意**
>
>在树莓派 4 之前的树莓派型号上使用 Wayland，您还必须将 wayland=on 添加到 /boot/firmware/cmdline.txt 。 

#### 音频配置

使用此选项在 PulseAudio 和 PipeWire 音频后端之间切换。在树莓派 OS Bookworm 之前，树莓派 OS 使用了 PulseAudio。

```
$ sudo raspi-config nonint do_audioconf <1/2>
```

* 1 ：使用 PulseAudio 后端
* 2 ：使用 PipeWire 后端

### 更新

将此工具更新到最新版本。

```
$ sudo raspi-config nonint do_update
```

## 显示

要配置您的树莓派使用非默认显示模式，请手动设置分辨率或旋转。

### 支持 HDMI 显示器

大多数 HDMI 显示器上，Raspberry Pi OS 使用显示器支持的最高分辨率和刷新率。

树莓派 Zero、Zero W 和 Zero 2 W 配备迷你 HDMI 端口，因此您需要迷你 HDMI 转全尺寸 HDMI 电缆或适配器。

树莓派 4、树莓派 5 和树莓派 400 都有两个 micro HDMI，因此您需要为每个您希望连接的显示器准备 micro HDMI 转标准 HDMI 的线缆或适配器。在打开树莓派之前连接这些线缆。

树莓派 4 和 400 可以驱动高达 1080p 分辨率、60Hz 刷新率的两个显示器。或者支持两个 30Hz 刷新率的 4K 显示器。如果您将显示器连接到 HDMI0 端口并在 /boot/firmware/config.txt 中设置 hdmi_enable_4kp60=1 参数，还可以以 60Hz 刷新率驱动单个 4K 显示器。

树莓派 5 可以在无需额外配置的情况下以 60Hz 的刷新率驱动两个 4K 分辨率的显示器。

### 设置分辨率和旋转

#### 通过桌面

在树莓派桌面上，打开“首选项”菜单，然后选择“屏幕配置”实用程序。您应该看到连接到树莓派的显示器的图形表示。右键单击要修改的显示器，然后选择一个选项。单击“应用”并关闭“屏幕配置”以保存更改。

#### 通过 CLI

使用以下命令打开屏幕配置实用程序：

```
$ arandr
```

您应该看到连接到树莓派的显示器的图形表示。右键单击要修改的显示器，然后选择一个选项。单击“应用”并关闭屏幕配置以保存更改。

### 手动设置分辨率和旋转

#### 确定显示设备名称

要手动配置分辨率和旋转，您需要知道显示设备的名称。要确定设备名称，请运行以下命令以显示有关连接设备的信息：

```
$ kmsprint | grep Connector
```

#### 设置自定义分辨率

如果您运行 Wayland 桌面合成器，您可以通过编辑您的主目录中的 .config/wayfire.ini 文件来设置自定义显示分辨率。编辑现有的 [output:<device>] 部分，或者如果不存在，则添加一个新的 [output:<device>] 部分以适用于您的显示设备。要更改显示分辨率，请添加一行 mode 。例如，以下示例显示了名为 HDMI-A-1 的设备以 1080p 60Hz 分辨率的配置：

```
[output:HDMI-A-1]
mode = 1920x1080@60
```

有关支持的模式和 mode 语法的信息，请参阅 Wayfire 文档。

将相同的配置块添加到 /usr/share/greeter.ini 以配置登录屏幕分辨率。

#### 设置自定义旋转

如果您运行 Wayland 桌面合成器，可以使用 wlr-randr 设置自定义显示旋转。以下命令将显示旋转为 0°、90°、180°和 270°：

```
$ wlr-randr --output HDMI-A-1 --transform normal
$ wlr-randr --output HDMI-A-1 --transform 90
$ wlr-randr --output HDMI-A-1 --transform 180
$ wlr-randr --output HDMI-A-1 --transform 270
```

--output 选项指定要旋转的设备。

>**注意**
>
>要通过 SSH 运行此命令，请添加以下前缀： WAYLAND_DISPLAY=wayland-1 ，例如 WAYLAND_DISPLAY=wayland-1 wlr-randr --output HDMI-A-1 --transform 90 。


您还可以使用以下 --transform 选项之一，同时镜像显示器并旋转它： flipped ， flipped-90 ， flipped-180 ， flipped-270 。

或者，您可以通过编辑您的家目录中的 .config/wayfire.ini 文件来旋转显示。编辑现有的 `[output:<device>]` 部分，或者如果不存在，则添加一个新的 `[output:<device>]` 部分以适配您的显示设备。要旋转您的显示，添加一个 transform 行。例如，以下示例显示了一个名为 HDMI-A-1 的设备的配置，分辨率为 1080p，刷新率为 60Hz，旋转角度为 270°：

```
[output:HDMI-A-1]
mode = 1920x1080@60
transform = 270
```

Wayland 支持以下 transform 选项：

* `normal`
* `90`
* `180`
* `270`

将相同的配置块添加到 /usr/share/greeter.ini 以配置登录屏幕旋转。

### 控制台分辨率和旋转

要在树莓派控制台模式下更改分辨率和旋转，请使用 KMS 设置。有关更多信息，请参阅配置内核命令行。

>**注意**
>
>
>在使用多个显示器的控制台模式时，所有连接的显示器共享相同的旋转设置。 

## 音频

Raspberry Pi OS 具有多种音频输出模式：HDMI 1、耳机插孔（如果您的设备有）和 USB 音频。

默认情况下，Raspberry Pi OS 将音频输出到 HDMI 1。如果没有 HDMI 输出可用，Raspberry Pi OS 将音频输出到耳机插孔或连接的 USB 音频设备。

### 更改音频输出

本节介绍了在 Raspberry Pi OS 中配置音频输出的不同方法。

#### 通过桌面音量控制

单击系统托盘上的音量图标以打开音频输出选择器。该界面可让您选择音频输出设备。单击音频输出设备以切换音频输出到该设备。

##### 专业音频配置文件

在音频输出选择器中查看音频设备时，您可能会看到一个名为专业音频的设备配置文件。该配置文件在每个音频设备上公开了最大数量的通道，使您能够更好地控制信号的路由。除非您需要对音频输出进行精细调整控制，否则请使用其他设备配置文件。

有关专业音频配置文件的更多信息，请访问 PipeWire 的常见问题解答。

#### 通过 raspi-config

要更改音频输出，请使用 raspi-config ，运行以下命令：

```
$ sudo raspi-config
```

您应该看到一个配置屏幕。完成以下步骤以更改您的音频输出：

1. 选择 System options 并按 Enter 。
2. 选择 Audio 选项并按 Enter 。
3. 选择所需模式，然后按 Enter 选择该模式。
4. 按右箭头键退出选项列表。选择 Finish 退出配置工具。

## 网络

Raspberry Pi OS 为设置无线连接提供了图形用户界面（GUI）。Raspberry Pi OS Lite 的用户和无头机器的用户可以使用 APT 从命令行设置无线网络连接。

>**注意**
>
>从 Raspberry Pi OS Bookworm 开始，Network Manager 是默认的网络配置工具。早期版本的 Raspberry Pi OS 使用 APT 和其他工具进行网络配置。 

### 连接到无线网络

#### 通过桌面

通过菜单栏右端的网络图标访问网络管理器。如果您使用带有内置无线连接功能的树莓派，或者插入了无线适配器，则单击此图标即可显示可用无线网络列表。如果看到消息“未找到 AP - 正在扫描...”，请等待几秒钟，网络管理器应该会找到您的网络。

>**注意**
>
>支持双频无线的树莓派设备（树莓派 3B+、树莓派 4、计算模块 4、树莓派 400 和树莓派 5）会自动禁用网络，直到您分配一个无线局域网国家。要设置无线局域网国家，请从“首选项”菜单中打开树莓派配置应用程序，选择本地化，然后从菜单中选择您的国家。

![wifi2](https://www.raspberrypi.com/documentation/computers/images/wifi2.png)

右侧的图标显示网络是否已安全，并指示信号强度。单击要连接的网络。如果网络已安全，对话框将提示您输入网络密钥：

![key](https://www.raspberrypi.com/documentation/computers/images/key.png)

输入密钥，然后单击“确定”，然后等待几秒钟。网络图标会闪烁一下，表示正在建立连接。连接成功后，图标将停止闪烁并显示信号强度。

##### 连接到隐藏网络

使用隐藏网络，请在网络菜单中导航到高级选项 > 连接到隐藏的 Wi-Fi 网络：

![the connect to a hidden wi-fi network option in advanced options](https://www.raspberrypi.com/documentation/computers/images/network-hidden.png)

然后，输入隐藏网络的 SSID。询问您的网络管理员您的网络使用哪种安全类型；大多数家庭网络目前使用 WPA 和 WPA2 个人安全，公共网络有时使用 WPA 和 WPA2 企业安全。选择您的网络的安全类型，并输入您的凭据：

![hidden wi-fi network authentication](https://www.raspberrypi.com/documentation/computers/images/network-hidden-authentication.png)

单击“连接”按钮以启动网络连接。

#### 通过命令行

本指南将帮助您在树莓派上配置无线连接，而无需使用图形工具。不需要额外的软件。

>**注意**
>
>本指南适用于 WEP、WPA、WPA2 或 WPA3 网络，但可能不适用于企业网络。

##### 启用无线网络

在全新安装时，您必须指定您使用设备的国家/地区。这样可以使您的设备选择正确的 5GHz 网络频段。在您指定了无线局域网国家/地区后，您就可以使用树莓派内置的无线网络模块。

要做到这一点，请使用命令行 raspi-config 工具设置您的无线局域网国家/地区。运行以下命令：

```
$ sudo raspi-config
```

使用箭头键选择“本地化选项”菜单项。选择 WLAN 国家选项。使用箭头键从下拉菜单中选择您的国家。按 Enter 键选择您的国家。

您现在应该可以访问无线网络。运行以下命令以检查您的无线电是否已启用：

```
$ nmcli radio wifi
```

如果此命令返回文本“已启用”，则可以准备配置连接。如果此命令返回“已禁用”，请尝试使用以下命令启用 Wi-Fi：

```
$ nmcli radio wifi on
```

##### 查找网络

要扫描无线网络，请运行以下命令：

```
$ nmcli dev wifi list
```

您应该看到类似以下的输出：

```
IN-USE  BSSID              SSID            MODE   CHAN  RATE        SIGNAL  BARS  SECURITY
        90:72:40:1B:42:05  myNetwork       Infra  132   405 Mbit/s  89      ****  WPA2
        90:72:42:1B:78:04  myNetwork5G     Infra  11    195 Mbit/s  79      ***   WPA2
        9C:AB:F8:88:EB:0D  Pi Towers       Infra  1     260 Mbit/s  75      ***   WPA2 802.1X
        B4:2A:0E:64:BD:BE  Example         Infra  6     195 Mbit/s  37      **    WPA1 WPA2
```

在“SSID”列中查找要连接的网络名称。使用 SSID 和密码连接到网络。

##### 连接到网络

运行以下命令来配置网络连接，将 <example_ssid> 占位符替换为您要配置的网络名称：

```
$ sudo nmcli --ask dev wifi connect <example_ssid>
```

在提示时输入您的网络密码。

您输入密码后，您的树莓派应该会自动连接到网络。

如果您看到错误输出，声称“需要密码，但未提供密码”，则表示您输入了错误的密码。请再次运行上述命令，仔细输入您的密码。

检查是否已连接到网络，请运行以下命令：

```
$ nmcli dev wifi list
```

应该看到类似以下的输出：

```
IN-USE  BSSID              SSID            MODE   CHAN  RATE        SIGNAL  BARS  SECURITY
*       90:72:40:1B:42:05  myNetwork       Infra  132   405 Mbit/s  89      ****  WPA2
        90:72:42:1B:78:04  myNetwork5G     Infra  11    195 Mbit/s  79      ***   WPA2
        9C:AB:F8:88:EB:0D  Pi Towers       Infra  1     260 Mbit/s  75      ***   WPA2 802.1X
        B4:2A:0E:64:BD:BE  Example         Infra  6     195 Mbit/s  37      **    WPA1 WPA2
```

在“IN-USE”列中查找星号（ `*` ）；它应该出现在您打算连接到的网络的 SSID 所在的同一行。

>**注意**
>
>您可以在目录 /etc/NetworkManager/system-connections/ 中手动编辑您的连接配置。 

##### 连接到一个未加密的网络

如果您要连接的网络没有使用密码，请运行以下命令：

```
$ sudo nmcli dev wifi connect <example_ssid>
```

>**警告**
>
>未加密的无线网络可能会将您的个人信息置于风险之中。在可能的情况下，请使用安全的无线网络或 VPN。

##### 连接到隐藏网络

如果您正在使用隐藏网络，请在运行 nmcli 时指定"hidden"选项，其值为"yes"。

```
$ sudo nmcli --ask dev wifi connect <example_ssid> hidden yes
```

##### 设置网络优先级

如果您的设备同时检测到多个已知网络，它可能会连接任何一个已检测到的已知网络。可使用优先级选项来强制让您的树莓派优先连接某些网络。您的设备将连接到具有最高优先级的范围内的网络。运行以下命令查看已知网络的优先级：

```
$ nmcli --fields autoconnect-priority,name connection
```

您应该看到类似以下的输出：

```
AUTOCONNECT-PRIORITY  NAME
0                     myNetwork
0                     lo
0                     Pi Towers
0                     Example
-999                  Wired connection 1
```

使用 nmcli connection modify 命令设置网络的优先级。以下示例命令将名为 "Pi Towers" 的网络的优先级设置为 10 ：

```
$ nmcli connection modify "Pi Towers" connection.autoconnect-priority 10
```

您的设备将始终尝试连接到具有最高非负优先级值的在范围内的网络。您还可以为网络分配负优先级；只有在范围内没有其他已知网络时，您的设备才会尝试连接到负优先级网络。例如，假设有三个网络：

```
AUTOCONNECT-PRIORITY  NAME
-1                    snake
0                     rabbit
1                     cat
1000                  dog
```

* 如果所有这些网络都在范围内，您的设备将首先尝试连接到 "dog" 网络。
* 如果连接到"dog"网络失败，您的设备将尝试连接到"cat"网络。
* 如果连接到"cat"网络失败，您的设备将尝试连接到"rabbit"网络。
* 如果连接到"rabbit"网络失败，并且您的设备未检测到其他已知网络，您的设备将尝试连接到"snake"网络。

### 配置 DHCP

默认情况下，Raspberry Pi OS 尝试通过 DHCP 自动配置所有网络接口，如果 DHCP 失败，则回退到 169.254.0.0/16 范围内的自动私有地址。

### 分配静态 IP 地址

为了为您的树莓派分配静态 IP 地址，请在路由器上为其保留一个地址。您的树莓派将继续通过 DHCP 分配其地址，但每次都将收到相同的地址。可以通过在 DHCP 服务器中将树莓派的 MAC 地址与静态 IP 地址关联来分配“固定”地址。

## 屏幕空白

您可以配置您的树莓派在一段时间内的不活动后将屏幕变暗。在默认情况下，当启用屏幕空白时，Raspberry Pi OS 在不活动十分钟后将屏幕变暗。

### 桌面

您可以使用树莓派配置菜单中的屏幕空白选项来控制屏幕空白。

#### 配置树莓派

单击菜单栏中的 Raspberry Pi 按钮。导航到首选项 > Raspberry Pi 配置。

![opening the Raspberry Pi Configuration menu from the desktop](https://www.raspberrypi.com/documentation/computers/images/pi-configuration.png)

选择显示选项卡。将屏幕空白选项单选按钮切换到打开位置。按下确定以确认您的选择。

![toggle Screen Blanking on in the Raspberry Pi Configuration menu](https://www.raspberrypi.com/documentation/computers/images/blanking.png)

#### CLI

您可以使用 raspi-config 命令行工具启用和禁用屏幕空白。运行以下命令打开该工具：

```
$ sudo raspi-config
```

使用箭头键导航，使用回车键选择。选择 Display Options > Screen Blanking 。使用箭头键选择 yes 以启用屏幕空白，或选择 no 以禁用屏幕空白。

或者，您可以添加或编辑以下行到 ~/.config/wayfire.ini ：

```
[idle]
dpms_timeout=600
```

dpms_timeout 变量控制了在 Raspberry Pi OS 在屏幕空白之前需要的不活动秒数。例如，值为 600 会在 600 秒后，或者十分钟后使屏幕空白。将值设置为 0 可以永远不让屏幕空白。

### 控制台

Raspberry Pi Configuration 使用的 dpms_timeout 屏幕空白配置仅影响桌面会话。在控制台模式下，当您的树莓派连接到仅有终端输入的监视器和键盘时，请在内核命令行中使用 consoleblank 设置。

#### 设置控制台模式屏幕空白

要更改控制台模式屏幕空白配置，请在文本编辑器中以管理员身份打开 /boot/firmware/cmdline.txt ：

```
$ sudo nano /boot/firmware/cmdline.txt
```

您可以在这里调整 Raspberry Pi OS 在空白控制台之前等待的秒数。例如，添加 consoleblank=600 以在 600 秒的不活动后禁用显示输出。将值设置为 0 以永远不要空白屏幕。

更改 cmdline.txt 后，只有在重启后才会生效。使用以下命令重启您的树莓派：

```
$ sudo reboot
```

#### 查看当前屏幕空白设置

您可以使用以下命令显示当前控制台空白时间（以秒为单位）：

```
$ cat /sys/module/kernel/parameters/consoleblank
```

## 用户

### 更改用户密码

您可以通过 raspi-config 应用程序或命令行更改当前用户帐户的密码：

```
$ sudo raspi-config
```

选择选项 2，并按照说明更改密码。

或者，使用 passwd 应用程序：

```
$ passwd
```

### 添加用户

要添加新用户，请输入以下命令，将 `<username>` 占位符替换为新用户的用户名：

```
$ sudo adduser <username>
```

在提示时，为新用户输入密码。

您可以在 `/home/<username>/` 找到新用户的主目录。

为了授予新用户必要的权限，比如 sudo ，运行以下命令将用户添加到相关用户组，将 `<username>` 占位符替换为新用户的用户名：

```
$ sudo usermod -a -G adm,dialout,cdrom,sudo,audio,video,plugdev,games,users,input,netdev,gpio,i2c,spi <username>
```

要检查权限是否已成功授予，请运行以下命令，将 `<username>` 占位符替换为新用户的用户名：

```
$ sudo su - <username>
```

如果上述命令成功运行，则已成功为用户配置权限。

### 删除用户

要删除用户，请运行以下命令，将 `<username>` 占位符替换为要删除的用户名：

```
$ sudo deluser -remove-home <username>
```

此命令将删除用户以及其主目录。如果您想保留用户的主目录，请运行不带 -remove-home 选项的命令。

### 更改默认用户

要更改在启动时自动登录到您树莓派的用户，请运行以下命令：

```
$ sudo raspi-config
```

选择选项 1 ， Boot/Auto login 。重新启动以使更改生效。

## 外部存储

您可以将外部硬盘、固态硬盘或 USB 闪存连接到树莓派上的任何 USB 端口，并挂载文件系统以访问其中存储的数据。

默认情况下，您的树莓派会自动挂载一些流行的文件系统，如 FAT、NTFS 和 HFS+，位于 /media/pi/<HARD-DRIVE-LABEL> 位置。

>**注意**
>
>Raspberry Pi OS Lite 不会自动挂载。

要设置存储设备，使其始终挂载到您选择的特定位置，必须手动挂载。

### 挂载存储设备

您可以将存储设备挂载到特定文件夹位置。通常在 /mnt 文件夹中执行此操作，例如 /mnt/mydisk 。请注意，文件夹必须为空。

将存储设备插入树莓派上的 USB，并使用以下命令列出树莓派上的所有磁盘分区：

```
$ sudo lsblk -o UUID,NAME,FSTYPE,SIZE,MOUNTPOINT,LABEL,MODEL
```

树莓派使用挂载点 / 和 /boot/firmware/ 。您的存储设备将显示在此列表中，以及任何其他连接的存储设备。

使用 SIZE、LABEL 和 MODEL 列来识别指向存储设备的磁盘分区的名称。例如， sda1 。FSTYPE 列包含了文件系统类型。如果您的存储设备使用 exFAT 文件系统，请安装 exFAT 驱动程序：

```
$ sudo apt update
$ sudo apt install exfat-fuse
```

如果您的存储设备使用 NTFS 文件系统，您将只能以只读方式访问它。如果您想要对设备进行写操作，可以安装 ntfs-3g 驱动程序：

```
$ sudo apt update
$ sudo apt install ntfs-3g
```

运行以下命令以获取磁盘分区的位置：

```
$ sudo blkid
```

 例如， /dev/sda1 。

创建一个目标文件夹，用作存储设备的挂载点。在这种情况下使用的挂载点名称是 mydisk 。您可以指定自己喜欢的名称：

```
$ sudo mkdir /mnt/mydisk
```

将存储设备挂载到您创建的挂载点上：

```
$ sudo mount /dev/sda1 /mnt/mydisk
```

验证存储设备已成功挂载，通过列出内容来确认：

```
$ ls /mnt/mydisk
```

### 自动挂载存储设备

您可以修改 fstab 文件，定义树莓派启动时存储设备将自动挂载的位置。在 fstab 文件中，磁盘分区由通用唯一标识符（UUID）标识。

获取磁盘分区的 UUID：

```
$ sudo blkid
```

从列表中找到磁盘分区并记录 UUID。（例如， 5C24-1453 。）使用诸如 nano 之类的命令行编辑器打开 fstab 文件：

```
$ sudo nano /etc/fstab
```

在 fstab 文件中添加以下行：

```
UUID=5C24-1453 /mnt/mydisk fstype defaults,auto,users,rw,nofail 0 0
```

用您在上述步骤中找到的文件系统类型替换 fstype ，例如： ntfs 。

如果文件系统类型为 FAT 或 NTFS，请在 nofail 之后立即添加 ,umask=000 - 这将允许所有用户完全读写存储设备上的每个文件。

现在您已在 fstab 中设置了一个条目，您可以启动带有或不带有存储设备的树莓派。在拔下设备之前，您必须关闭树莓派或手动卸载它。

>**注意**
>
>如果在树莓派启动时未连接存储设备，启动时间将额外需要 90 秒。您可以通过在 nofail 后立即添加 ,x-systemd.device-timeout=30 来缩短这个时间。这将把超时时间更改为 30 秒，这意味着系统只会等待 30 秒，然后放弃尝试挂载磁盘。


要获取有关每个 Linux 命令的更多信息，请使用 man 命令查阅特定的手册页。例如， man fstab 。

### 卸载存储设备

当树莓派关机时，系统会负责卸载存储设备，以便安全拔下。如果您想手动卸载设备，可以使用以下命令：

```
$ sudo umount /mnt/mydisk
```

如果收到“目标正忙”的错误消息，这意味着存储设备未被卸载。如果没有显示错误，现在可以安全地拔下设备。

#### 处理“目标正忙”

“目标正忙”消息意味着存储设备上有被程序使用的文件。要关闭这些文件，请使用以下步骤。

关闭在存储设备上有打开文件的任何程序。如果您有一个终端打开，请确保您不在存储设备挂载的文件夹中，或者在其子文件夹中。

如果您仍然无法卸载存储设备，您可以使用 lsof 工具检查哪个程序在设备上打开了文件。您需要首先安装 lsof ，使用 apt ：

```
$ sudo apt update
$ sudo apt install lsof
```

 使用 lsof 命令：

```
$ lsof /mnt/mydisk
```

## 内核命令行（ cmdline.txt ）

Linux 内核在启动时接受一组命令行参数。在树莓派上，这个命令行在引导分区中的一个文件中定义，称为 cmdline.txt 。您可以使用任何文本编辑器编辑此文本文件。

```
$ sudo nano /boot/firmware/cmdline.txt
```

>**重要**
>
>将所有参数放在同一行的 cmdline.txt 中。不要使用换行符。


要查看在启动时传递给内核的命令行，请运行以下命令：

```
$ cat /proc/cmdline
```

因为树莓派固件在启动内核之前对命令行进行更改，所以此命令的输出将不完全匹配 cmdline.txt 的内容。

### 命令行选项

许多内核命令行参数，其中一些由内核本身定义。其他由内核可能正在使用的代码定义，比如 Plymouth 闪屏系统。

#### 标准条目

console 定义了串行控制台。通常有两个条目：

* `console=serial0,115200`
* `console=tty1`

root 定义了根文件系统的位置。例如， root=/dev/mmcblk0p2 表示多媒体卡块 0 分区 2。

rootfstype 定义了根文件系统使用的文件系统类型，例如， rootfstype=ext4 。

quiet 将默认内核日志级别设置为 KERN_WARNING ，在启动过程中抑制除非非常严重的日志消息之外的所有消息。

#### 设置 KMS 显示模式

早期版本的 Raspberry Pi OS 中使用的传统固件和 FKMS 显示模式不再受支持。取而代之的是，最近的 OS 版本使用 KMS（内核模式设置）。

如果在 Raspberry Pi OS 中不存在 video 条目，则树莓派操作系统将使用 HDMI 连接的显示器的 EDID 自动选择基于 Linux 内核信息的显示器支持的最佳分辨率。在 Raspberry Pi OS Lite 或控制台模式中，您必须自定义 video 条目以控制分辨率和旋转。

```
video=HDMI-A-1:1920x1080M@60
```

另外，可以添加旋转和反射参数，如标准 Linux 帧缓冲文档中所述。以下示例定义了一个名为 HDMI-A- 的显示器，分辨率为 1080p，刷新率为 60Hz，旋转 90 度，并在 X 轴上反射：

```
video=HDMI-A-1:1920x1080M@60,rotate=90,reflect_x
```

在指定旋转和反射参数时，必须明确指定分辨率。

显示类型的可能选项 - video= 条目的第一部分 - 包括：

| 视频选项 | 显示                                                                   |
| ---------- | ------------------------------------------------------------------------ |
| `HDMI-A-1`         | HDMI 1（树莓派 4B 板子上标注为 HDMI 0，单 HDMI 板上标注为 HDMI） |
| `HDMI-A-2`         | HDMI 2（树莓派 4B 板子上标注为 HDMI 1）                          |
| `DSI-1`         | DSI 或 DPI                                                             |
| `Composite-1`         | 复合                                                                   |

#### 其他条目

此部分包含了您可以在内核命令行中使用的其他条目。此列表不是详尽的。

splash 告诉引导使用 Plymouth 模块显示启动画面。

plymouth.ignore-serial-consoles 通常，如果启用了 Plymouth 模块，它将阻止任何串行控制台上出现启动消息。此标志告诉 Plymouth 忽略所有串行控制台，使启动消息再次可见，就像没有运行 Plymouth 时一样。

dwc_otg.lpm_enable=0 关闭 Link Power Management（LPM）在 dwc_otg 驱动程序中的设置，该驱动程序驱动着嵌入在用于树莓派计算机的处理器中的 USB 控制器。在树莓派 4 上，默认情况下禁用此控制器，并且仅连接到 USB Type C 电源输入连接器。树莓派 4 上的 USB-A 端口由另一个不受此设置影响的 USB 控制器驱动。

dwc_otg.speed 设置了树莓派计算机上内置处理器的 USB 控制器的速度。 dwc_otg.speed=1 将其设置为全速（USB 1.0），比高速（USB 2.0）慢。除非在解决 USB 设备问题时，否则不应设置此选项。

smsc95xx.turbo_mode 启用/禁用有线网络驱动程序的 Turbo 模式。 smsc95xx.turbo_mode=N 关闭 Turbo 模式。

usbhid.mousepoll 指定鼠标轮询间隔。如果您遇到无线鼠标运行缓慢或不稳定的问题，将其设置为 0 可能会有所帮助。

使用 drm.edid_firmware=HDMI-A-1:edid/your_edid.bin 覆盖您的显示器内置的 EDID 内容。

## 本地化您的树莓派 Pi

您可以使用 raspi-config 工具配置 Raspberry Pi OS 的 UI 语言、键盘布局和时区。

## 保护您的树莓派

在这里，我们描述了一些提高您树莓派安全性的常见方法。

### 设置 sudo 命令要求密码

使用 sudo 前缀运行命令将其作为超级用户运行。默认情况下，这不需要密码。但是，您可以通过要求为所有使用 sudo 运行的命令输入密码来使您的树莓派更安全。

要强制 sudo 需要密码，请编辑您的用户帐户的 nopasswd sudoers 文件，将文件名中的 `<username>` 占位符替换为您的用户名：

```
$ sudo visudo /etc/sudoers.d/010_<username>-nopasswd
```

将 `<username>` 条目更改为以下内容，并将 <username> 替换为您的用户名：

```
<username> ALL=(ALL) PASSWD: ALL
```

保存文件。您的新偏好应立即生效。

### 更新 Raspberry Pi OS

只有最新的操作系统发行版包含所有最新的安全补丁。始终将您的设备更新到最新版本的 Raspberry Pi OS。

### 自动更新您的 SSH 服务器

如果您使用 SSH 连接到您的树莓派，添加 cron 工作可能是值得的，专门更新 SSH 服务器。 以下命令，可能作为每日 cron 工作运行，确保您及时获得最新的 SSH 安全修复程序，独立于您的正常更新过程。

```
$ apt install openssh-server
```

### 改善 SSH 安全

SSH 是远程访问树莓派 的常用方式。默认情况下，SSH 需要用户名和密码。为了使 SSH 更加安全，请使用基于密钥的身份验证。

#### 启用和禁用 SSH 用户

您还可以通过更改 sshd 配置来允许或拒绝特定用户。

```
$ sudo nano /etc/ssh/sshd_config
```

将以下行添加、编辑或追加到文件末尾，其中包含您希望允许登录的用户名：

```
AllowUsers alice bob
```

您还可以使用 DenyUsers 来明确阻止某些用户名登录：

```
DenyUsers jane john
```

更改后，请使用以下命令重新启动 sshd 服务，以使更改生效：

```
$ sudo systemctl restart ssh
```

### 使用防火墙

Linux 有许多防火墙解决方案可用。大多数使用底层的 iptables 项目来提供数据包过滤。该项目位于 Linux netfiltering 系统之上。默认情况下，Raspberry Pi OS 上安装了 iptables，但未设置。设置它可能是一项复杂的任务，一个比 iptables 提供更简单界面的项目是 Uncomplicated Firewall (UFW)。这是 Ubuntu 中的默认防火墙工具，可以安装到您的树莓派上：

```
$ sudo apt install ufw
```

ufw 是一个命令行工具，尽管有一些 GUI 可用。请注意， ufw 需要以 root 权限运行，因此所有命令都以 sudo 开头。还可以使用选项 --dry-run 任何 ufw 命令，这表示显示命令的操作结果，而不实际进行任何更改。

启用防火墙，这也将确保它在启动时启动：

```
$ sudo ufw enable
```

要禁用防火墙，并禁用启动时启动，请使用：

```
$ sudo ufw disable
```

允许特定端口访问（我们在示例中使用了端口 22）：

```
$ sudo ufw allow 22
```

拒绝访问端口也非常简单（再次，我们以端口 22 为例）：

```
$ sudo ufw deny 22
```

您还可以指定在端口上允许或拒绝哪种服务。在此示例中，我们拒绝了端口 22 上的 TCP：

```
$ sudo ufw deny 22/tcp
```

即使您不知道服务使用哪个端口，也可以指定服务。此示例允许 ssh 服务通过防火墙访问：

```
$ sudo ufw allow ssh
```

状态命令列出防火墙的所有当前设置：

```
$ sudo ufw status
```

规则可能相当复杂，允许阻止特定 IP 地址，指定允许流量的方向，或限制连接尝试的次数（例如，以帮助击败 DDoS 攻击）。您还可以指定要应用规则的设备（例如，eth0，wlan0）。请参阅 ufw 手册页（ man ufw ）以获取除下面命令之外的完整详细信息。

使用 TCP 在 ssh 端口上限制登录尝试。如果 IP 地址在过去 30 秒内尝试连接六次或更多次，则拒绝连接：

```
$ sudo ufw limit ssh/tcp
```

拒绝从 IP 地址 192.168.2.1 访问端口 30

```
$ sudo ufw deny from 192.168.2.1 port 30
```

### 使用 fail2ban 阻止可疑活动

当将树莓派用作服务器时，您必须在防火墙中创建有意的漏洞以允许服务器流量。Fail2ban 可以帮助保护您的服务器。Fail2ban 检查日志文件并检查可疑活动，如多次暴力登录尝试。它可以帮助您避免手动检查入侵尝试的日志文件，然后通过 iptables 更新防火墙以阻止它们。

运行以下命令安装 fail2ban ：

```
$ sudo apt install fail2ban
```

安装后，Fail2ban 会创建 /etc/fail2ban/jail.conf 。要启用 Fail2ban，请将 jail.conf 复制到 jail.local ：

```
$ sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
```

在此配置文件中包含一组默认选项，以及用于检查特定服务异常的选项。要查看用于 ssh 的规则，请在编辑器中打开 jail.local ：

```
$ sudo nano /etc/fail2ban/jail.local
```

如果不存在，则创建 `[ssh]` 部分，并向该部分添加以下行：

```
[ssh]
enabled  = true
port     = ssh
filter   = sshd
backend  = systemd
maxretry = 6
```

这将启用对可疑 ssh 活动的 Fail2ban 检查，包括系统日志检查，并允许在阻止活动之前进行六次重试。

在同一文件中，此 `[default]` 部分定义了默认的封禁操作 iptables-multiport ，当达到检测阈值时运行 /etc/fail2ban/action.d/iptables-multiport.conf 文件：

```
# Default banning action (e.g. iptables, iptables-new,
# iptables-multiport, shorewall, etc) It is used to define
# action_* variables. Can be overridden globally or per
# section within jail.local file
banaction = iptables-multiport
```

多端口禁止所有端口上的所有访问。 action.d 文件夹包含许多可用于自定义服务器响应可疑活动的替代操作配置文件。

例如，如果要在三次失败尝试后永久禁止 IP 地址，请将 `[ssh]` 部分中的 maxretry 值更改为 3 ，并将 bantime 设置为负数：

```
[ssh]
enabled  = true
port     = ssh
filter   = sshd
backend  = systemd
maxretry = 3
bantime  = -1
```

## 设置无头树莓派

无头树莓派在没有显示器、键盘或鼠标的情况下运行。要无头运行树莓派，您需要一种从另一台计算机访问它的方式。要远程访问您的树莓派，您需要将树莓派连接到网络，并找到一种通过该网络访问树莓派的方式。

要将树莓派连接到网络，您可以通过以太网将设备插入有线连接，或配置无线网络。

要通过该网络访问树莓派，请使用 SSH。通过 SSH 连接，您就可以使用 raspi-config 来启用 VNC（如果您更喜欢图形桌面环境）。

如果您从头开始设置您的树莓派，请在刻录过程中设置无线网络和 SSH。如果您已经设置好了树莓派，您可以使用 raspi-config 配置 SSH。

>**警告**
>
>取决于您使用的树莓派型号和 SD 卡型号，您的树莓派可能需要长达五分钟的时间来启动并首次连接到无线网络。 

### 连接到有线网络

首次启动时，要连接到有线网络，请通过以太网将您的无头树莓派连接，或者如果您的树莓派没有以太网接口，则需使用以太网转换器。您的树莓派将自动连接到网络。

### 连接到无线网络

要在无头树莓派首次启动时配置无线网络访问，请使用 Raspberry Pi Imager 中的高级设置菜单。输入您首选无线网络的 SSID 和密码。您的树莓派将使用这些凭据在首次启动时连接到网络。某些无线适配器和某些树莓派开发板不支持 5GHz 网络；请查阅您的无线模块文档，以确保与您首选网络的兼容性。

>**注意**
>
>旧版的 Raspberry Pi OS 使用一个 wpa_supplicant.conf 文件，该文件可以放入 boot 文件夹中以配置无线网络设置。从 Raspberry Pi OS Bookworm 版本开始，不再提供该功能。


### 远程访问

如果没有键盘或显示器，您需要一种方法来远程控制您的无头树莓派。在首次启动时，唯一的选项是 SSH。要在全新安装的 Raspberry Pi OS 上启用 SSH，请选择以下方法之一：

* 在 Raspberry Pi Imager 的 OS 自定义菜单中启用 SSH，然后输入用户名和密码
* 在 SD 卡的根目录下创建一个名为 ssh 的文件，然后按照下面部分的说明手动配置一个用户 userconf.txt

欲了解更多信息，请参阅设置 SSH 服务器。通过 SSH 连接，您就可以使用 raspi-config 来启用 VNC，如果您更喜欢图形桌面环境。

#### 手动配置用户

在您的 SD 卡根目录下，创建一个名为 userconf.txt 的文件。

该文件应包含一行文本，由 `<username>:<password>` 组成：您想要使用的用户名，紧接着是一个冒号，然后是您想要使用的密码的加密表示。

>**注意**
>
>`<username>`必须只包含小写字母，数字和连字符，并且必须以字母开头。长度不得超过 31 个字符。 

要生成加密密码，请在另一台计算机上使用 OpenSSL。打开终端并输入以下内容：

```
$ openssl passwd -6
```

在提示时输入密码并进行验证。然后，该命令将输出所提供密码的加密版本。

## 从您的树莓派主机一个无线网络

您的树莓派可以使用无线模块主机自己的无线网络。如果您通过以太网端口（或第二个无线模块）将您的树莓派连接到互联网，连接到无线网络的其他设备可以通过您的树莓派访问互联网。

假如使用 10.x.x.x IP 块的有线网络。您可以将您的树莓派连接到该网络，并在使用另一个 IP 块的独立网络上为无线客户端提供服务，例如 192.168.x.x 。

在下面的图表中，请注意笔记本电脑存在于与路由器和有线客户端分开的 IP 块中：

![host a network](../.gitbook/assets/host-a-network.png)

在这种网络配置下，无线客户端可以通过树莓派路由器彼此通信。但是，无线网络上的客户端不能直接与有线网络上的客户端进行交互，除了树莓派之外；无线客户端存在于一个与为有线客户端提供服务的网络分开的私有网络中。

>**注意**
>
>树莓派 5、4、3、Zero W 和 Zero 2 W 可以使用内置无线模块托管无线网络。没有内置无线网卡的树莓派型号可以使用单独的无线适配器以支持此功能。

### 启用热点

要在命令行上创建托管的无线网络，请运行以下命令，将 `<example-network-name>` 和 `<example-password>` 占位符替换为您自己的值：

```
$ sudo nmcli device wifi hotspot ssid <example-network-name> password <example-password>
```

使用另一个无线客户端，如笔记本电脑或智能手机，连接到网络。查找一个 SSID 与 `<example-network-name>` 匹配的网络。输入您的网络密码，您应该成功连接到网络。如果您的树莓派通过以太网连接或第二个无线适配器访问互联网，您应该能够访问互联网。

### 禁用热点

要禁用热点网络并恢复将您的 Pi 用作无线客户端，请运行以下命令：

```
$ sudo nmcli device disconnect wlan0
```

在禁用网络后，运行以下命令可重新连接到另一个 Wi-Fi 网络：

```
$ sudo nmcli device up wlan0
```

>**技巧**
>
>有关连接到无线网络的更多信息，请参阅配置网络。

### 将您的树莓派用作网络桥接器

默认情况下，从您的树莓派托管的无线网络与通过以太网连接的父网络分开存在。在这种安排中，连接到父网络的设备无法直接与连接到您的树莓派托管的无线网络上的设备通信。如果您希望连接的无线设备能够与父网络上的设备通信，您可以将您的树莓派配置为网络桥接器。有了网络桥接器，连接到 Pi 托管的无线网络的每个设备都被分配一个父网络中的 IP 地址。

在下面的图表中，笔记本电脑存在于与路由器和有线客户端相同的 IP 块中：

![bridge network](../.gitbook/assets/bridge-network.png)

以下步骤描述了如何在您的树莓派上设置网络桥接，以实现无线客户端和父网络之间的通信。

首先，创建一个网络桥接口：

```
$ sudo nmcli connection add type bridge con-name 'Bridge' ifname bridge0
```

接下来，将您设备的以太网连接添加到父网络桥接中：

```
$ sudo nmcli connection add type ethernet slave-type bridge \
    con-name 'Ethernet' ifname eth0 master bridge0
```

最后，将您的无线热点连接添加到桥接中。您可以添加现有的热点接口或创建一个新的：

* 如果您已经按照上述说明创建了无线热点连接，请使用以下命令将现有接口添加到桥接中：

  ```
  $ sudo nmcli connection modify 'Hotspot' master bridge0
  ```
* 如果您尚未创建无线热点连接，请使用单个命令创建新接口并将其添加到桥接中，将 `<hotspot-password>` 占位符替换为您选择的密码：

  ```
  $ sudo nmcli connection add con-name 'Hotspot' \
      ifname wlan0 type wifi slave-type bridge master bridge0 \
      wifi.mode ap wifi.ssid Hotspot wifi-sec.key-mgmt wpa-psk \
      wifi-sec.proto rsn wifi-sec.pairwise ccmp \
      wifi-sec.psk <hotspot-password>
  ```

现在您已配置好桥接，是时候激活它了。运行以下命令以激活桥接：

```
$ sudo nmcli connection up Bridge
```

运行以下命令开始托管您的无线网络：

```
$ sudo nmcli connection up Hotspot
```

您可以使用 nmcli device 命令来验证桥接、以太网接口和无线热点接口是否都处于活动状态。

>**技巧**
>
>使用诸如 arp-scan 之类的工具，检查如果连接到热点，父网络上的设备是否可访问。

## 使用代理服务器

代理服务器充当客户端设备和互联网之间的中介。要将您的树莓派配置为代理服务器客户端，请按照本节中的说明操作。

 您将需要：

* 代理服务器的 IP 地址或主机名和端口
* 如果需要，为您的代理设置用户名和密码

### 配置您的树莓派

您需要设置三个环境变量（ http_proxy ， https_proxy 和 no_proxy ），以便您的树莓派知道如何访问代理服务器。

打开终端窗口，并使用 nano 打开文件 /etc/environment ：

```
$ sudo nano /etc/environment
```

将以下内容添加到 /etc/environment 文件中以创建 http_proxy 变量：

```
export http_proxy="http://<proxy_ip_address>:<proxy_port>"
```

用代理的 IP 地址和端口替换 `<proxy_ip_address>` 和 `<proxy_port>` 占位符。

```
export http_proxy="http://<username>:<password>@proxyipaddress:proxyport"
```

用您用于验证代理的用户名和密码替换 `<username>` 和 `<password>` 占位符。

为环境变量 https_proxy 输入相同的信息：

```
export https_proxy="http://username:password@proxyipaddress:proxyport"
```

创建 no_proxy 环境变量，这是一个逗号分隔的地址列表，您的树莓派不应该使用代理。

```
export no_proxy="localhost, 127.0.0.1"
```

您的 /etc/environment 文件现在应该如下所示：

```
export http_proxy="http://username:password@proxyipaddress:proxyport"
export https_proxy="http://username:password@proxyipaddress:proxyport"
export no_proxy="localhost, 127.0.0.1"
```

按下 Ctrl + X 保存并退出。

### 更新 sudoers 文件

使用代理环境变量来运行作为 sudo 的操作，比如下载和安装软件，更新 sudoers 。

使用以下命令打开 sudoers ：

```
$ sudo visudo
```

将以下行添加到文件中，这样 sudo 将使用您刚刚创建的环境变量：

```
Defaults	env_keep+="http_proxy https_proxy no_proxy"
```

按下 Ctrl + X 保存并退出。

### 重启您的树莓派

重启您的树莓派以使更改生效。现在您应该能够通过代理服务器访问互联网。

## boot 文件夹内容

Raspberry Pi OS 将引导文件存储在 SD 卡的第一个分区上，使用 FAT 文件系统格式化。

在启动时，每个树莓派从引导分区加载各种文件，以便在 Linux 内核启动之前启动各个处理器。

在启动时，Linux 将引导分区挂载为 /boot/firmware/ 。

>**注意**
>
>在 Bookworm 之前，Raspberry Pi OS 将引导分区存储在 /boot/。自从 Bookworm 以来，引导分区位于 /boot/firmware/。 

### `bootcode.bin`

引导加载程序由 SoC 在启动时加载。它执行一些非常基本的设置，然后加载 start*.elf 文件之一。

树莓派 4 和 5 不使用 bootcode.bin 。它已被内置 EEPROM 中的引导代码取代。

### `start*.elf`

加载到 SoC 中 VideoCore GPU 上的二进制固件块，然后接管引导过程。

start.elf 基本固件。

start_x.elf 包含额外的编解码器。

start_db.elf 用于调试。

start_cd.elf 是精简版本的固件，移除了对硬件块（如编解码器和 3D）以及调试日志支持的支持；它还施加了初始帧缓冲区限制。当在 config.txt 中指定 gpu_mem=16 时，将自动使用精简固件。

start4.elf ， start4x.elf ， start4db.elf 和 start4cd.elf 是针对树莓派 4 系列（4B 型号，Pi 400，计算模块 4 和计算模块 4S）特定固件文件。

要了解如何使用这些文件的更多信息，请参阅 config.txt 文档。

树莓派 5 不使用 elf 文件。固件被包含在引导加载程序 EEPROM 中。

### `fixup*.dat`

在匹配的情况下找到链接器文件与前一节中列出的 start*.elf 文件。

### `cmdline.txt`

内核命令行传递到引导时的内核。

### `config.txt`

包含许多用于设置树莓派的配置参数。有关更多信息，请参阅 config.txt 文档。

>**重要**
>
>树莓派 5 需要在启动分区中有一个非空 config.txt 文件。 

### `issue.txt`

包含发行版日期和 git 提交 ID 的文本化维护信息。

### `initramfs*`

初始 RAM 磁盘的内容。这会在真正的根文件系统被挂载之前将临时根文件系统加载到内存中。

自从 Bookworm 版本开始，Raspberry Pi OS 默认包含一个 initramfs 文件。要启用初始 ramdisk，请在 config.txt 中使用 auto_initramfs 关键字进行配置。

### ssh 或 ssh.txt

当此文件存在时，会在启动时启用 SSH。否则，默认情况下禁用 SSH。内容无关紧要。即使是空文件也会启用 SSH。

### 设备树 blob 文件（ *.dtb ）

设备树 blob 文件包含各种型号的树莓派的硬件定义。这些文件根据检测到的树莓派型号在启动时设置内核。

### 内核文件（ *.img ）

相应于树莓派型号的各种内核映像文件：

| 文件名 | 处理器                    | 树莓派型号                                                                     | 注解                                           |
| -------- | --------------------------- | -------------------------------------------------------------------------------- | -------------------------------------------------- |
| `kernel.img`       | BCM2835                   | Pi Zero，Pi 1                                                                  |                                                  |
| `kernel7.img`       | BCM2836，BCM2837          | 树莓派 Zero 2 W，树莓派 2，树莓派 3                                            | 后来的树莓派 2 使用 BCM2837                      |
| `kernel7l.img`       | BCM2711                   | Pi 4，Pi 400，CM4，CM4S                                                        | 大物理地址扩展（LPAE）                           |
| `kernel8.img`       | BCM2837，BCM2711，BCM2712 | 树莓派 Zero 2 W，树莓派 2，树莓派 3，树莓派 4，树莓派 400，CM4，CM4S，树莓派 5 | 64 位内核。基于 BCM2836 的树莓派 2 不支持 64 位内核。 |
| `kernel_2712.img`       | BCM2712                   | 树莓派 5                                                                       | 为 Pi 5 优化的 64 位内核。                          |

>**注意**
>
>在运行 32 位内核系统上，lscpu 会报告其 CPU 架构为 armv7l ，在运行 64 位内核系统上，lscpu 会报告其 CPU 架构为 aarch64 。在 armv7l 情况下， l 指的是小端 CPU 架构，而不是 LPAE ，如 kernel7l.img 文件名所示。

### overlays 文件夹

包含设备树叠加。这些用于配置各种硬件设备，如第三方声卡。 config.txt 中的条目选择这些叠加层。有关更多信息，请参阅设备树、叠加和参数。

## LED 警告闪烁代码

如果树莓派由于某种原因无法启动，或者必须关闭，在许多情况下，LED 将闪烁特定次数以指示发生了什么。LED 将闪烁一定数量的长闪烁（0 或更多次），然后产生短闪烁，以指示确切状态。在大多数情况下，该模式将在两秒间隔后重复。

| 长闪烁 | 短闪烁 | 状态                               |
| -------- | -------- | ------------------------------------ |
| 0      | 3      | 无法启动的通用故障                 |
| 0      | 4      | 未找到 start*.elf                  |
| 0      | 7      | 未找到内核映像                     |
| 0      | 8      | SDRAM 故障                         |
| 0      | 9      | SDRAM 不足                         |
| 0      | 10     | 处于停止状态                       |
| 2      | 1      | 分区不是 FAT                       |
| 2      | 2      | 无法从分区读取                     |
| 2      | 3      | 扩展分区不是 FAT                   |
| 2      | 4      | 文件签名/哈希不匹配 - Pi 4 和 Pi 5 |
| 3      | 1      | SPI EEPROM 错误 - Pi 4 和 Pi 5     |
| 3      | 2      | SPI EEPROM 已写保护 - Pi 4 和 Pi 5 |
| 3      | 3      | I2C 错误 - Pi 4 和 Pi 5            |
| 3      | 4      | 安全启动配置无效                   |
| 4      | 3      | 未找到 RP1                         |
| 4      | 4      | 不支持的板类型                     |
| 4      | 5      | 致命固件错误                       |
| 4      | 6      | 电源故障类型 A                     |
| 4      | 7      | 电源故障类型 B                     |

## 配置 UART

树莓派上有两种可用的 UART - PL011 和 mini UART。PL011 是一种功能强大、广泛兼容 16550 的 UART，而 mini UART 具有较少的功能集。

树莓派上的所有 UART 仅支持 3.3V（如果连接到 5V 系统，将会损坏）。可以使用适配器连接到 5V 系统。另外，也可以 用各种第三方提供的低成本 USB 至 3.3V 串行适配器。

### 树莓派 Zero、1、2 和 3

树莓派 Zero、1、2 和 3 各自包含两个 UART，如下：

| 名称  | 类型      |
| ------- | ----------- |
| UART0 | PL011     |
| UART1 | mini UART |

### 树莓派 4 和 400

树莓派 4 Model B 和 400 默认情况下有额外的四个 PL011，但它们是被禁用的：

| 名称  | 类型      |
| ------- | ----------- |
| UART0 | PL011     |
| UART1 | mini UART |
| UART2 | PL011     |
| UART3 | PL011     |
| UART4 | PL011     |
| UART5 | PL011     |

### 树莓派 5

树莓派 5 有额外的四个 PL011，这些在默认情况下是禁用的：

| 名称  | 类型  |
| ------- | ------- |
| UART0 | PL011 |
| UART1 | PL011 |
| UART2 | PL011 |
| UART3 | PL011 |
| UART4 | PL011 |

树莓派 5 没有 mini UART。

### CM1、CM3、CM3+ 和 CM4

第一代计算模块，与计算模块 3 和计算模块 3+ 一起，都有两个 UART，而计算模块 4 如上所述有六个 UART。

在所有的计算模块型号上，默认情况下禁用了 UART，并可以通过使用设备树叠加来显式启用。您还可以指定要使用的 GPIO 引脚，例如：

```
dtoverlay=uart1,txd1_pin=32,rxd1_pin=33
```

### 主 UART

在树莓派上，选择一个 UART 位于 GPIO 14（发送）和 15（接收） - 这是主 UART。默认情况下，这也将是 Linux 控制台可能存在的 UART。请注意，GPIO 14 是 GPIO 引脚上的引脚 8，而 GPIO 15 是引脚 10。

在树莓派 5 上，主 UART 出现在调试标头上。

### 次要 UART

次要 UART 通常不出现在 GPIO 连接器上。默认情况下，次要 UART 连接到组合无线局域网/蓝牙控制器的蓝牙侧，在包含此控制器的型号上。

### 主要和次要 UART

以下表格总结了各种树莓派设备上 UART 的分配：

| 型号                            | 主/控制台 | 次要/蓝牙 |
| --------------------------------- | ----------- | ----------- |
| 树莓派 Zero                     | UART0     | UART1     |
| 树莓派 Zero W / 树莓派 Zero 2 W | UART1     | UART0     |
| 树莓派 1                        | UART0     | UART1     |
| 树莓派 2                        | UART0     | UART1     |
| 树莓派 3                        | UART1     | UART0     |
| 计算模块 3 & 3+                 | UART0     | UART1     |
| 树莓派 4                        | UART1     | UART0     |
| 树莓派 5                        | UART10    |           |

Raspberry Pi OS 上的 Linux 设备：

| Linux 设备 | 说明                  |
| ------------ | ----------------------- |
| `/dev/ttyS0`           | mini UART             |
| `/dev/ttyAMA0`           | 第一个 PL011（UART0） |
| `/dev/serial0`           | 主 UART               |
| `/dev/serial1`           | 次 UART               |
| `/dev/ttyAMA10`           | 树莓派 5 调试 UART    |

/dev/serial0 和 /dev/serial1 是指向 /dev/ttyS0 或 /dev/ttyAMA0 的符号链接。

在树莓派 5 上， /dev/serial0 是一个指向 /dev/ttyAMA10 的符号链接。

由于 Bookworm 的变化， /dev/serial1 在默认情况下不存在。您可以通过在 config.txt 中设置以下值来重新启用 serial1 ：

```
dtparam=krnbt=off
```

>**技巧**
>
>该选项将来可能不适用于所有型号。应只有在您的用例没有其他替代方案时才使用该选项。 

### mini UART 和 CPU 核心频率

>**注意**
>
> 如果迷你 UART 是主要的，或者蓝牙被禁用，则默认情况下禁用迷你 UART。 

为了使用迷你 UART，您需要配置树莓派以使用固定的 VPU 核心时钟频率。这是因为迷你 UART 时钟与 VPU 核心时钟相连，因此当核心时钟频率发生变化时，UART 波特率也会发生变化。可以将 enable_uart 和 core_freq 设置添加到 config.txt 中，以更改迷你 UART 的行为。以下表总结了可能的组合：

| 迷你 UART 设置为 | 核心时钟                      | 结果                                                                                 |
| ------------------ | ------------------------------- | -------------------------------------------------------------------------------------- |
| 主 UART          | 变量                          | 迷你 UART 已禁用                                                                     |
| 主 UART          | 通过设置 enable_uart=1 来修复 | 启用迷你 UART，核心时钟固定为 250MHz，或者如果 force_turbo=1 设置，则为 VPU 超频频率 |
| 次要 UART        | 可变                          | 迷你 UART 已禁用                                                                     |
| 二级 UART        | 通过设置 core_freq=250 来修复 | 迷你 UART 已启用                                                                     |

enable_uart 标志的默认状态取决于哪个 UART 是主 UART：

| 主 UART               | 启用 `_uart` 参数的默认状态 |
| ----------------------- | -------------------------- |
| 迷你 UART             | 0                        |
| 第一个 PL011（UART0） | 1                        |

### 禁用 Linux 串行控制台

默认情况下，主 UART 被分配给 Linux 控制台。如果您希望将主 UART 用于其他目的，您必须重新配置 Raspberry Pi OS。这可以通过使用 raspi-config 来实现：

* 启动 raspi-config: sudo raspi-config
* 选择选项 3 - 接口选项
* 选择选项 P6 - 串行端口
* 在提示符 Would you like a login shell to be accessible over serial? 处，回答'否'
* 在提示符 Would you like the serial port hardware to be enabled? 处，回答“是”
* 退出 raspi-config 并重启树莓派以使更改生效

### 启用 Linux 的早期控制台

尽管 Linux 内核在引导过程中相对较早地启动了 UART，但仍然比一些关键基础设施设置晚得多。在这些早期阶段出现故障可能很难诊断，如果没有访问那个时间段的内核日志消息。要为其中一个 UART 启用 earlycon 支持，请根据主要 UART 是哪个，向 cmdline.txt 添加以下选项之一：

对于树莓派 5， earlycon 输出仅出现在具有以下配置的 3 针调试连接器上：

```
earlycon=pl011,0x107d001000,115200n8
```

对于树莓派 4、400 和计算模块 4：

```
earlycon=uart8250,mmio32,0xfe215040
earlycon=pl011,mmio32,0xfe201000
```

对于树莓派 2、Pi 3 和计算模块 3：

```
earlycon=uart8250,mmio32,0x3f215040
earlycon=pl011,mmio32,0x3f201000
```

对于树莓派 1、Pi Zero 和 Compute Module 1：

```
earlycon=uart8250,mmio32,0x20215040
earlycon=pl011,mmio32,0x20201000
```

默认波特率为 115200bps。

>**注意**
>
>选择错误的早期控制台可能会妨碍树莓派启动。 

### UART 和设备树

内核 GitHub 中可以找到各种 UART 设备树叠加定义。最有用的两个叠加是 disable-bt 和 miniuart-bt 。

disable-bt 禁用蓝牙设备，并将第一个 PL011（UART0）设置为主 UART。您还必须禁用初始化调制解调器的系统服务，以防它连接到 UART，使用 sudo systemctl disable hciuart 。

miniuart-bt 将蓝牙功能切换到使用迷你 UART，并将第一个 PL011（UART0）设置为主 UART。请注意，这可能会降低最大可用波特率（请参阅下文有关迷你 UART 限制的内容）。您还必须使用 force_turbo=1 或 core_freq=250 将 VPU 核心时钟设置为固定频率。

叠加层 uart2 、 uart3 、 uart4 和 uart5 用于在树莓派 4 上启用四个额外的 UART。在文件夹中还有其他特定于 UART 的叠加层。有关设备树叠加层的详细信息，请参考 /boot/firmware/overlays/README ，或运行 dtoverlay -h overlay-name 查看描述和使用信息。

向 config.txt 文件添加一行以应用设备树叠加。请注意，文件名的 -overlay.dts 部分将被移除。例如：

```
dtoverlay=disable-bt
```

### PL011 和 mini-UART

PL011 UART 和 mini-UART 之间存在一些差异。

迷你 UART 具有较小的 FIFO。加上缺乏流量控制，这使得在更高的波特率下更容易丢失字符。它也通常比 PL011 功能更弱，主要是因为其波特率与 VPU 时钟速度的关联。

与 PL011 相比，迷你 UART 的特定缺陷包括：

* 没有中断检测
* 没有帧错误检测
* 没有奇偶校验位
* 没有接收超时中断

迷你 UART 和 BCM2835 的 PL011 实现均没有 DCD、DSR、DTR 或 RI 信号。

可在 SoC 外设文档中找到进一步的迷你 UART 文档。

## 设备树、叠加和参数

树莓派内核和固件使用设备树（DT）来描述硬件。这些设备树可能包括用于控制板载功能的 DT 参数。DT 叠加层允许描述和配置可选外部硬件，并支持更多控制参数。

固件加载程序（ start.elf 及其变体）负责加载 DTB（设备树块 - 一种机器可读的 DT 文件）。它根据板的修订号选择要加载的 DTB，并进行修改以进一步定制。这种运行时定制避免了许多只有细微差异的 DTB 的需求。

用户提供的参数在 config.txt 中被扫描，以及任何叠加层及其参数，然后应用。加载程序检查结果以了解（例如）要用于控制台的任何 UART。最后，它启动内核，传递指向合并 DTB 的指针。

### 设备树

设备树（DT）是系统中硬件的描述。它应包括基本 CPU 的名称、其内存配置以及任何外部和内部的外围设备。DT 不应用于描述软件，尽管通过列出硬件模块，通常会导致驱动程序模块被加载。

>**注意**
>
>切记，DT 应该是与操作系统无关的，因此任何与 Linux 特定的内容都不应出现在其中。

设备树表示硬件配置，以节点层次结构的形式呈现。每个节点可以包含属性和子节点。属性是命名的字节数组，可以包含字符串、数字（大端序）、任意字节序列以及二者的任意组合。类比于文件系统，节点是目录，属性是文件。树中节点和属性的位置可以用路径描述，使用斜杠作为分隔符，单个斜杠（ `/` ）表示根。

#### DTS 基本语法

设备树通常以一种称为设备树源（DTS）的文本形式编写，并存储在具有 .dts 后缀的文件中。DTS 语法类似于 C 语言，使用大括号进行分组，并在每行末尾使用分号。请注意，DTS 在关闭大括号后需要分号：将其视为 C struct 而非函数。编译后的二进制格式称为扁平设备树（FDT）或设备树 Blob（DTB），存储在 .dtb 文件中。

以下是 .dts 格式中的简单树：

```
/dts-v1/;
/include/ "common.dtsi";

/ {
    node1 {
        a-string-property = "A string";
        a-string-list-property = "first string", "second string";
        a-byte-data-property = [0x01 0x23 0x34 0x56];
        cousin: child-node1 {
            first-child-property;
            second-child-property = <1>;
            a-string-property = "Hello, world";
        };
        child-node2 {
        };
    };
    node2 {
        an-empty-property;
        a-cell-property = <1 2 3 4>; /* each number (cell) is a uint32 */
        child-node1 {
            my-cousin = <&cousin>;
        };
    };
};

/node2 {
    another-property-for-node2;
};
```

 此树包含：

* 必需的标题： `/dts-v1/`
* 包含另一个 DTS 文件，传统上命名为 `*.dtsi` ，类似于 C 中的 .h 头文件
* 单个根节点： `/`
* 一对子节点： node1 和 node2
* 一些节点的子节点： child-node1 和 child-node2
* 一个标签（ cousin ）和对该标签的引用（ `&cousin` ）
* 散布在树中的几个属性
* 一个重复的节点 ( /node2 )

属性是简单的键值对，其中值可以是空的，也可以包含任意字节流。虽然数据类型没有编码在数据结构中，但在设备树源文件中可以表达一些基本数据表示。

文本字符串（以 NUL 结尾）用双引号表示：

```
string-property = "a string";
```

单元格是由尖括号分隔的 32 位无符号整数：

```
cell-property = <0xbeef 123 0xabcd1234>;
```

任意字节数据用方括号分隔，并以十六进制输入：

```
binary-property = [01 23 45 67 89 ab cd ef];
```

不同表示形式的数据可以使用逗号连接起来：

```
mixed-property = "a string", [01 23 45 67], <0x12345678>;
```

逗号也用于创建字符串列表：

```
string-list = "red fish", "blue fish";
```

#### 有关 `/include/` 的一则说明

`/include/` 指令实现了简单的文本包含，类似于 C 的 #include 指令，但是设备树编译器的一个特性导致不同的使用模式。鉴于节点是命名的，可能带有绝对路径，因此在 DTS 文件（及其包含文件）中可能会出现相同的节点两次。当这种情况发生时，节点和属性被合并，根据需要交错和覆盖属性（后续值会覆盖先前的值）。

在上面的示例中， `/node2` 的第二次出现会导致将新属性添加到原始属性中：

```
/node2 {
    an-empty-property;
    a-cell-property = <1 2 3 4>; /* each number (cell) is a uint32 */
    another-property-for-node2;
    child-node1 {
        my-cousin = <&cousin>;
    };
};
```

因此，一个 .dtsi 可以覆盖或为树中的多个位置提供默认值。

#### 标签和引用

树的一部分经常需要引用另一部分，有四种方法可以做到这一点：

路径字符串类似于文件系统路径，例如 `/soc/i2s@7e203000` 是 BCM2835 和 BCM2836 中 I2S 设备的完整路径。标准 API 不会创建到属性的路径，例如 `/soc/i2s@7e203000/status` ：所以，您应首先找到一个节点，然后选择该节点的属性。

Phandles 是分配给节点的唯一 32 位整数，在其 phandle 属性中。出于历史原因，您可能还会看到一个多余的匹配 linux,phandle 。Phandles 按顺序编号，从 1 开始；0 不是有效的 phandle。它们通常由 DT 编译器分配，当它在整数上下文中遇到对节点的引用时，通常以标签的形式。使用 phandles 引用节点的引用仅被编码为相应的整数（单元）值；没有标记表明它们应被解释为 phandles，因为这是应用程序定义的。

标签就像 C 中的标签为代码中的位置命名一样，DT 标签为层次结构中的节点分配名称。编译器获取标签的引用，并在字符串上下文（ `&node` ）中将其转换为路径，在整数上下文（ `<&node>` ）中将其转换为 phandle；原始标签不会出现在编译输出中。请注意，标签不包含结构；它们只是一个扁平的全局命名空间中的标记。

别名类似于标签，不同之处在于它们作为索引形式出现在 FDT 输出中。它们作为 `/aliases` 节点的属性存储，每个属性将别名名称映射到路径字符串。尽管别名节点出现在源中，但路径字符串通常显示为对标签的引用（ `&node` ），而不是完全写出。解析路径字符串为节点的 DT API 通常查看路径的第一个字符，将不以斜杠开头的路径视为必须首先使用 `/aliases` 表转换为路径的别名。

#### 设备树语义

如何构建设备树，以及如何最好地使用它来捕获一些硬件的配置，是一个庞大而复杂的主题。有许多可用资源，其中一些列在下面，但有几点值得强调：

* compatible 属性是硬件描述和驱动软件之间的链接。当操作系统遇到具有 compatible 属性的节点时，它会在其设备驱动程序数据库中查找最佳匹配项。在 Linux 中，这通常会导致驱动程序模块被自动加载，前提是它已经被适当标记并且没有被列入黑名单。
* status 属性指示设备是启用还是禁用。如果 status 是 ok ， okay 或不存在，则设备已启用。否则， status 应该是 disabled ，以便禁用设备。将设备放置在一个 .dtsi 文件中并将状态设置为 disabled 可以很有用。然后，派生配置可以包括该 .dtsi 并设置所需设备的状态为 okay 。

### 设备树叠加

现代片上系统（SoC）是一个非常复杂的设备；完整的设备树可能长达数百行。进一步将 SoC 放置在带有其他组件的板上只会使情况变得更加复杂。为了保持可管理性，特别是如果有共享组件的相关设备，将共同元素放入 .dtsi 文件中，以便从可能的多个 .dts 文件中包含，这是有道理的。

当像树莓派这样的系统还支持可选的插件配件，如 HATs 时，问题就变得更加复杂。最终，每种可能的配置都需要一个设备树来描述它，但假如考虑到所有不同的基本型号和大量可用的配件，组合的数量开始迅速增加。

需要的是一种方法来描述这些可选组件，使用部分设备树，然后通过采用基本 DT 并添加一些可选元素来构建完整的树。您可以这样做，这些可选元素称为"叠加"。

除非您想要学习如何为树莓派编写叠加，否则您可能更喜欢跳转到使用设备树。

#### 片段

DT 叠加层包含多个片段，每个片段都针对一个节点及其子节点。尽管概念听起来很简单，但语法一开始似乎相当奇怪：

```
// Enable the i2s interface
/dts-v1/;
/plugin/;

/ {
    compatible = "brcm,bcm2835";

    fragment@0 {
        target = <&i2s>;
        __overlay__ {
            status = "okay";
            test_ref = <&test_label>;
            test_label: test_subnode {
                dummy;
            };
        };
    };
};
```

字符串 compatible 标识这是为 BCM2835 设计的，这是树莓派 SoC 的基本架构；如果叠加层使用了树莓派 4 的功能，则 brcm,bcm2711 是正确的值，否则 brcm,bcm2835 可用于所有树莓派叠加层。然后是第一个（在这种情况下是唯一的）片段。片段应从零开始编号。不遵守这一点可能导致一些或所有片段被忽略。

每个片段由两部分组成：一个 target 属性，用于标识要应用叠加层的节点；以及 **overlay** 本身，其主体将添加到目标节点。上面的示例可以解释为如果它是这样编写的：

```
/dts-v1/;
/plugin/;

/ {
    compatible = "brcm,bcm2835";
};

&i2s {
    status = "okay";
    test_ref = <&test_label>;
    test_label: test_subnode {
        dummy;
    };
};
```

使用足够新版本的 dtc ，您可以按照上述示例编写并获得相同的输出，但一些自制工具尚不理解这种格式。目前，应将希望包含在标准 Raspberry Pi OS 内核中的任何叠加层以旧格式编写。

将该叠加层与标准树莓派基础设备树（例如 bcm2708-rpi-b-plus.dtb ）合并的效果，前提是叠加层在之后加载，将启用 I2S 接口，将其状态更改为 okay 。但是，如果尝试使用以下方式编译此叠加层：

```
$ dtc -I dts -O dtb -o 2nd.dtbo 2nd-overlay.dts
```

...您将收到错误消息：

```
Label or path i2s not found
```

这并不太意外，因为没有提及基础 .dtb 或 .dts 文件，以便编译器找到 i2s 标签。

再试一次，这次使用原始示例并添加 `-@` 选项以允许未解决的引用（和 -Hepapr 以去除一些混乱）：

```
$ dtc -@ -Hepapr -I dts -O dtb -o 1st.dtbo 1st-overlay.dts
```

如果 dtc 返回关于第三行的错误，则它没有覆盖工作所需的扩展。运行 sudo apt install device-tree-compiler ，然后再试一次 - 这次，编译应该成功完成。请注意，适当的编译器也可在内核树中作为 scripts/dtc/dtc 使用，当使用 dtbs make 目标时构建：

```
$ make ARCH=arm dtbs
```

转储 DTB 文件的内容以查看编译器生成了什么：

```
$ fdtdump 1st.dtbo
```

这应该输出类似于以下内容：

```
/dts-v1/;
// magic:		0xd00dfeed
// totalsize:		0x207 (519)
// off_dt_struct:	0x38
// off_dt_strings:	0x1c8
// off_mem_rsvmap:	0x28
// version:		17
// last_comp_version:	16
// boot_cpuid_phys:	0x0
// size_dt_strings:	0x3f
// size_dt_struct:	0x190

/ {
    compatible = "brcm,bcm2835";
    fragment@0 {
        target = <0xffffffff>;
        __overlay__ {
            status = "okay";
            test_ref = <0x00000001>;
            test_subnode {
                dummy;
                phandle = <0x00000001>;
            };
        };
    };
    __symbols__ {
        test_label = "/fragment@0/__overlay__/test_subnode";
    };
    __fixups__ {
        i2s = "/fragment@0:target:0";
    };
    __local_fixups__ {
        fragment@0 {
            __overlay__ {
                test_ref = <0x00000000>;
            };
        };
    };
};
```

在文件结构的详细描述之后，有我们的片段。但请仔细观察 - 我们在 `&i2s` 处写了什么，现在却写成了 `0xffffffff` ，这表明发生了一些奇怪的事情（较旧版本的 dtc 可能会写成 0xdeadbeef ）。编译器还添加了一个包含唯一（对于此叠加层而言）的小整数的 phandle 属性，以指示该节点具有标签，并用相同的小整数替换了对标签的所有引用。

在片段之后有三个新节点：

* **symbols** 列出了覆盖中使用的标签（ test_label 在这里），以及带有标签节点的路径。这个节点是如何处理未解析符号的关键。
* **fixups** 包含一个属性映射列表，将未解析符号的名称映射到需要使用目标节点的 phandle 进行修补的片段内单元格路径列表。在这种情况下，路径是到 target 的 0xffffffff 值，但片段可能包含其他未解析引用，这将需要额外的修复。
* **local_fixups** 保存了存在于叠加层内的标签引用的位置 - test_ref 属性。这是必需的，因为执行合并的程序必须确保 phandle 编号是连续且唯一的。

在 1.3 节中提到“原始标签不会出现在编译输出中”，但是当使用 `-@` 开关时，情况并非如此。相反，每个标签都会导致 **symbols** 节点中的一个属性，将标签映射到路径，就像 aliases 节点一样。实际上，机制如此相似，以至于在解析符号时，树莓派加载程序会在没有 **symbols** 节点的情况下搜索“别名”节点。曾经这非常有用，因为提供足够的别名允许使用非常旧的 dtc 版本来构建基本的 DTB 文件，但幸运的是，那已经是远古历史了。

#### 设备树参数

为了避免需要大量的设备树叠加，减少外围设备用户修改 DTS 文件的需要，树莓派加载程序支持一项新功能 - 设备树参数。这允许使用命名参数对 DT 进行小的更改，类似于内核模块从 modprobe 和内核命令行接收参数的方式。参数可以由基本 DTBs 和叠加暴露，包括 HAT 叠加。

通过在根节点添加一个 **overrides** 节点来定义参数。它包含属性，其名称是选择的参数名称，其值是一个序列，包括目标节点的 phandle（对标签的引用）和指示目标属性的字符串；支持字符串、整数（单元）和布尔属性。

##### 字符串参数

字符串参数的声明方式如下：

```
name = <&label>,"property";
```

其中 label 和 property 将被适当的值替换。字符串参数可能导致它们的目标属性增长、缩小或被创建。

请注意，名为 status 的属性被特殊对待；`非零/true/yes/on` 值将被转换为字符串 "okay" ，而`零/false/no/off` 将变为 "disabled" 。

##### 整数参数

整数参数是这样声明的：

```
name = <&label>,"property.offset"; // 8-bit
name = <&label>,"property;offset"; // 16-bit
name = <&label>,"property:offset"; // 32-bit
name = <&label>,"property#offset"; // 64-bit
```

在这里， label ， property 和 offset 将被适当的值替换；偏移量以字节为单位相对于属性的起始位置指定（默认为十进制），前面的分隔符指定参数的大小。与早期实现不同，整数参数可以引用不存在的属性或超出现有属性末尾的偏移量。

##### 布尔参数

设备树将布尔值编码为零长度属性；如果存在，则该属性为真，否则为假。它们的定义如下：

```
boolean_property; // Set 'boolean_property' to true
```

通过不定义属性将其分配值 false 。布尔参数的声明如下，用适当的值替换 label 和 property 占位符：

```
name = <&label>,"property?";
```

倒置布尔在应用相同方式之前反转输入值，就像常规布尔一样；它们的声明方式类似，但使用 ! 表示反转：

```
name = <&label>,"<property>!";
```

布尔参数可以导致属性被创建或删除，但它们不能删除基本 DTB 中已经存在的属性。

##### 字节字符串参数

字节字符串属性是任意字节序列，例如 MAC 地址。它们接受十六进制字节的字符串，字节之间可以有冒号，也可以没有。

```
mac_address = <&ethernet0>,"local_mac_address[";
```

选择 [ 是为了与声明字节字符串的 DT 语法匹配：

```
local_mac_address = [aa bb cc dd ee ff];
```

##### 具有多个目标的参数

在设备树中的某些情况下，能够在多个位置设置相同的值是很方便的。与创建多个参数的笨拙方法不同，可以通过将它们连接起来，将多个目标添加到单个参数中，就像这样：

```
__overrides__ {
    gpiopin = <&w1>,"gpios:4",
              <&w1_pins>,"brcm,pins:0";
    ...
};
```

（示例取自 w1-gpio 叠加层）

>**注意**
>
>甚至可以使用单个参数针对不同类型的属性。您可以合理地将“启用”参数连接到 status 字符串、包含零或一的单元格以及适当的布尔属性。

##### 文本分配

DT 参数机制允许从同一参数中修补多个目标，但其效用受到限制，因为必须将相同的值写入所有位置（除了格式转换和从反转布尔值中获得的否定）。嵌入式文字分配的添加允许参数写入任意值，而不管用户提供的参数值如何。

分配出现在声明的末尾，并由 = 表示：

```
str_val  = <&target>,"strprop=value";              // 1
int_val  = <&target>,"intprop:0=42"                // 2
int_val2 = <&target>,"intprop:0=",<42>;            // 3
bytes    = <&target>,"bytestr[=b8:27:eb:01:23:45"; // 4
```

第 1、2 和 4 行相当明显，但第 3 行更有趣，因为该值显示为整数（单元）值。DT 编译器在编译时评估整数表达式，这可能很方便（特别是如果使用宏值），但该单元也可以包含对标签的引用：

```
// Force an LED to use a GPIO on the internal GPIO controller.
exp_led = <&led1>,"gpios:0=",<&gpio>,
          <&led1>,"gpios:4";
```

应用叠加时，标签将按照通常的方式针对基本 DTB 进行解析。最好将多部分参数拆分到多行，以便更容易阅读 - 随着单元值分配的增加，这变得更加必要。

请记住，除非应用了参数，否则参数不起作用 - 查找表中的默认值将被忽略，除非使用参数名称而不指定值。

##### 查找表

查找表允许在使用之前转换参数输入值。它们充当关联数组，有点像 switch/case 语句：

```
phonetic = <&node>,"letter{a=alpha,b=bravo,c=charlie,d,e,='tango uniform'}";
bus      = <&fragment>,"target:0{0=",<&i2c0>,"1=",<&i2c1>,"}";
```

没有 =value 的键意味着将键用作值，没有键的 = 表示在没有匹配项的情况下是默认值，并且以逗号开始或结束列表（或在任何地方使用空键=值对）表示未匹配的输入值应该保持不变；否则，找不到匹配项将会报错。

>**注意**
>
>在单元格整数值后的表字符串中，逗号分隔符是隐式的 - 明确添加一个会创建一个空对（见上文）。 

>**注意**
>
>由于查找表操作的是输入值，而文字赋值会忽略它们，因此不可能将两者结合在一起 - 查找声明中 } 结束后的字符被视为错误。 

##### 叠加/片段参数

描述中所述的 DT 参数机制存在许多限制，包括缺乏创建整数数组的简便方法，以及无法创建新节点。克服其中一些限制的方法是有条件地包含或排除某些片段。

通过将 **overlay** 节点重命名为 **dormant** ，可以将片段从最终合并过程中排除（禁用）。参数声明语法已扩展，以允许否则非法的零目标 phandle 指示以下字符串包含片段或叠加范围的操作。到目前为止，已实现了四种操作：

```
+<n>    // Enable fragment <n>
-<n>    // Disable fragment <n>
=<n>    // Enable fragment <n> if the assigned parameter value is true, otherwise disable it
!<n>    // Enable fragment <n> if the assigned parameter value is false, otherwise disable it
```

 例子：

```
just_one    = <0>,"+1-2"; // Enable 1, disable 2
conditional = <0>,"=3!4"; // Enable 3, disable 4 if value is true,
                          // otherwise disable 3, enable 4.
```

i2c-rtc 叠加使用这种技术。

##### 特殊属性

一些属性名称，在被参数定位时，会得到特殊处理。您可能已经注意到的一个 - status - 将布尔值转换为 okay 表示 true， disabled 表示 false。

分配给 bootargs 属性会将其附加到其末尾，而不是覆盖它 - 这是如何向内核命令行添加设置的方式。

reg 属性用于指定设备地址 - 内存映射硬件块的位置，I2C 总线上的地址等。子节点的名称应该用十六进制地址加以限定，使用 @ 作为分隔符：

```
bmp280@76 {
    reg = <0x77>;
    ...
};
```

当分配给 reg 属性时，父节点名称的地址部分将被替换为分配的值。这可用于在多次使用相同叠加时防止节点名称冲突 - 这是 i2c-gpio 叠加使用的技术。

name 属性是一个伪属性 - 它不应出现在 DT 中，但是对其赋值会导致其父节点的名称更改为分配的值。与 reg 属性一样，这可以用于给节点提供唯一的名称。

##### 叠加地图文件

树莓派 4 的推出，围绕 BCM2711 SoC 构建，带来了许多变化；其中一些变化是额外的接口，另一些是对现有接口进行的修改（或删除）。有一些新的叠加层专为树莓派 4 设计，这些叠加层在旧硬件上没有意义，例如启用新的 SPI、I2C 和 UART 接口的叠加层，但其他叠加层即使控制着新设备上仍然相关的功能，也不能正确应用。

因此，有必要针对具有不同硬件的多个平台定制叠加方法。在单个 .dtbo 文件中支持它们将需要大量使用隐藏的（“休眠”）片段，并切换到按需符号解析机制，以便不需要的丢失符号不会导致失败。一个更简单的解决方案是添加一个功能，根据当前平台将叠加名称映射到几个实现文件中的一个。

叠加映射是固件在引导时加载的文件。它以 DTS 源格式编写 - overlay_map.dts ，编译为 overlay_map.dtb 并存储在叠加目录中。

这是当前地图文件的摘录（请参阅完整版本）:

```
/ {
    disable-bt {
        bcm2835;
        bcm2711;
        bcm2712 = "disable-bt-pi5";
    };

    disable-bt-pi5 {
        bcm2712;
    };

    uart5 {
        bcm2711;
    };

    pi3-disable-bt {
        renamed = "disable-bt";
    };

    lirc-rpi {
        deprecated = "use gpio-ir";
    };
};
```

每个节点都有一个需要特殊处理的叠加名称。每个节点的属性要么是平台名称，要么是少数几个特殊指令之一。当前支持的平台有 bcm2835 ，其中包括所有围绕 BCM2835、BCM2836 和 BCM2837 SoCs 构建的树莓派， bcm2711 适用于树莓派 4B、400 和 CM4， bcm2712 适用于树莓派 5 和 CM5。

没有值的平台名称（空属性）表示当前叠加与该平台兼容；例如， uart5 与 bcm2711 平台兼容。对于平台的非空值是要使用的替代叠加的名称，请求在 BCM2712 上使用 disable-bt 会导致加载 disable-bt-pi5 。未在叠加节点中包含的任何平台都与该叠加不兼容。未在映射中提到的任何叠加都假定与所有平台兼容。

第二个示例节点 - disable-bt-pi5 - 可以从 disable-bt 的内容中推断出，但这种智能是用于文件的构建，而不是用于其解释。

仅在 BCM2711 上使用 uart5 叠加才有意义。

如果未为叠加列出平台，则可能适用其中一个特殊指令：

* renamed 指令表示叠加的新名称（应与原始名称基本兼容），但也会记录有关更名的警告。
* deprecated 指令包含一个简要的解释性错误消息，在通用前缀 overlay '...' is deprecated: 之后将被记录。

链接重命名和特定于平台的实现是可能的，但要小心避免循环！

记住：只有异常需要列出 - 覆盖的节点缺失意味着应该为所有平台使用默认文件。

从固件中访问诊断消息已在调试中介绍。

dtoverlay 和 dtmerge 实用程序已扩展以支持映射文件：

* dtmerge 从基础 DTB 中的兼容字符串中提取平台名称。
* dtoverlay 从 live 设备树中读取兼容字符串位于 /proc/device-tree 处，但您可以使用 -p 选项提供替代平台名称（在不同平台上进行干扰运行时很有用）。

它们都将错误、警告和任何调试输出发送到 STDERR。

##### 例子

这里有一些不同类型的属性示例，带有修改它们的参数：

```
/ {
    fragment@0 {
        target-path = "/";
        __overlay__ {

            test: test_node {
                string = "hello";
                status = "disabled";
                bytes = /bits/ 8 <0x67 0x89>;
                u16s = /bits/ 16 <0xabcd 0xef01>;
                u32s = /bits/ 32 <0xfedcba98 0x76543210>;
                u64s = /bits/ 64 < 0xaaaaa5a55a5a5555 0x0000111122223333>;
                bool1; // Defaults to true
                       // bool2 defaults to false
                mac = [01 23 45 67 89 ab];
                spi = <&spi0>;
            };
        };
    };

    fragment@1 {
        target-path = "/";
        __overlay__ {
            frag1;
        };
    };

    fragment@2 {
        target-path = "/";
        __dormant__ {
            frag2;
        };
    };

    __overrides__ {
        string =      <&test>,"string";
        enable =      <&test>,"status";
        byte_0 =      <&test>,"bytes.0";
        byte_1 =      <&test>,"bytes.1";
        u16_0 =       <&test>,"u16s;0";
        u16_1 =       <&test>,"u16s;2";
        u32_0 =       <&test>,"u32s:0";
        u32_1 =       <&test>,"u32s:4";
        u64_0 =       <&test>,"u64s#0";
        u64_1 =       <&test>,"u64s#8";
        bool1 =       <&test>,"bool1!";
        bool2 =       <&test>,"bool2?";
        entofr =      <&test>,"english",
                      <&test>,"french{hello=bonjour,goodbye='au revoir',weekend}";
        pi_mac =      <&test>,"mac[{1=b8273bfedcba,2=b8273b987654}";
        spibus =      <&test>,"spi:0[0=",<&spi0>,"1=",<&spi1>,"2=",<&spi2>;

        only1 =       <0>,"+1-2";
        only2 =       <0>,"-1+2";
        enable1 =     <0>,"=1";
        disable2 =    <0>,"!2";
    };
};
```

对于更多示例，请查看树莓派 Linux GitHub 存储库中托管的大量叠加源文件。

#### 导出标签

固件中的叠加处理和使用 dtoverlay 实用程序的运行时叠加应用将在叠加中定义的标签视为私有于该叠加。这样可以避免为标签发明全局唯一名称（使它们保持简短），并且允许同一叠加多次使用而不发生冲突（前提是使用一些技巧 - 请参阅特殊属性）。

有时，创建一个标签并从另一个叠加中使用它非常有用。自 2020 年 2 月 14 日发布的固件具有将某些标签声明为全局的能力 - **exports** 节点：

```
    ...
    public: ...

    __exports__ {
        public; // Export the label 'public' to the base DT
    };
};
```

当应用此叠加时，加载程序会剥离除了已导出的符号之外的所有符号，在本例中为 public ，并重新编写路径，使其相对于包含标签的片段的目标。然后加载在此之后的叠加可以引用 `&public` 。

#### 叠加应用程序顺序

在大多数情况下，片段应用的顺序并不重要，但对于自身打补丁的叠加（其中片段的目标是叠加中的标签，称为叠加内部片段），这变得重要。在旧固件中，片段严格按顺序从上到下应用。自 2020 年 2 月 14 日发布的固件起，片段分两次应用：

* 首先应用并隐藏目标其他片段的片段。
* 然后应用常规片段。

这种拆分对于运行时叠加特别重要，因为第一步发生在 dtoverlay 实用程序中，第二步由内核执行（无法处理内部叠加片段）。

### 在树莓派上使用设备树

#### DTBs，叠加和 config.txt

在树莓派上，加载程序（其中之一是 start.elf 图像）的工作是将叠加与适当的基础设备树结合，然后将完全解析的设备树传递给内核。基础设备树位于 FAT 分区中与 start.elf 相邻（从 Linux /boot/firmware/ ），命名为 bcm2711-rpi-4-b.dtb ， bcm2710-rpi-3-b-plus.dtb ，等等。请注意，一些型号（3A+，A，A+）将使用“b” 等效型号（3B+，B，B+），分别。此选择是自动的，并允许在各种设备中使用相同的 SD 卡映像。

>**注意**
>
>DT 和 ATAGs 是互斥的，将 DT blob 传递给不理解它的内核将导致启动失败。固件将始终尝试加载 DT 并将其传递给内核，因为自 rpi-4.4.y 以来的所有内核都没有 DTB 将无法正常工作。您可以通过在 config.txt 中添加 device_tree= 来覆盖此设置，这将强制使用 ATAGs，对于简单的裸机内核可能很有用。

现在的加载程序支持使用 bcm2835_defconfig 进行构建，该配置选择了上游 BCM2835 支持。这个配置将导致 bcm2835-rpi-b.dtb 和 bcm2835-rpi-b-plus.dtb 被构建。如果这些文件与内核一起复制，那么加载程序将尝试默认加载其中一个 DTB。

为了管理设备树和叠加层，加载程序支持一些 config.txt 指令：

```
dtoverlay=acme-board
dtparam=foo=bar,level=42
```

这将导致加载程序在固件分区中查找 overlays/acme-board.dtbo ，Raspberry Pi OS 挂载在 /boot/firmware/ 上。然后它将搜索参数 foo 和 level ，并将指定的值分配给它们。

加载程序还将搜索带有已编程 EEPROM 的附加 HAT，并从那里加载支持的叠加层 - 直接或通过“overlays”目录中的名称; 这一切都在没有任何用户干预的情况下发生。

有多种方法可以告诉内核正在使用设备树：

* 在引导过程中，“Machine model:”内核消息具有特定于板的值，例如“Raspberry Pi 2 Model B”，而不是“BCM2709”。
* /proc/device-tree 存在，并包含与 DT 的节点和属性完全相同的子目录和文件。

使用设备树，内核将自动搜索并加载支持指示启用设备的模块。因此，通过为设备创建适当的 DT 叠加，您可以使设备的用户无需编辑 /etc/modules ；所有配置都在 config.txt 中进行，在 HAT 的情况下，甚至这一步也是不必要的。但是，请注意，诸如 i2c-dev 之类的分层模块仍然需要显式加载。

反过来，由于平台设备只有在 DTB 请求时才会被创建，因此不再需要黑名单模块，这些模块过去是由板支持代码中定义的平台设备加载的结果。实际上，当前的 Raspberry Pi OS 映像不包含黑名单文件（除了一些 WLAN 设备，其中有多个可用驱动程序）。

#### DT 参数

如上所述，DT 参数是一种方便的方式，可以对设备的配置进行小的更改。当前的基本 DTB 支持用于启用和控制板载音频、I2C、I2S 和 SPI 接口的参数，而无需使用专用叠加。在使用中，参数看起来像这样：

```
dtparam=audio=on,i2c_arm=on,i2c_arm_baudrate=400000,spi=on
```

>**注意**
>
>多个赋值可以放在同一行，但确保不要超过 80 个字符的限制。


如果您有一个定义一些参数的叠加层，可以在后续行上指定这些参数，就像这样：

```
dtoverlay=lirc-rpi
dtparam=gpio_out_pin=16
dtparam=gpio_in_pin=17
dtparam=gpio_in_pull=down
```

…或者像这样将参数附加到叠加层行：

```
dtoverlay=lirc-rpi,gpio_out_pin=16,gpio_in_pin=17,gpio_in_pull=down
```

叠加层参数仅在加载下一个叠加层之前有效。如果同名参数同时被叠加层和基础导出，叠加层中的参数优先；建议避免这样做。要暴露基础 DTB 导出的参数，可以结束当前叠加层范围：

```
dtoverlay=
```

#### 特定于板的标签和参数

树莓派开发板有两个 I2C 接口。这些通常分为：一个用于 ARM，一个用于 VideoCore（GPU）。在几乎所有型号上， i2c1 属于 ARM， i2c0 属于 VC，用于控制摄像头并读取 HAT EEPROM。然而，有两个早期版本的 Model B 角色相反。

为了使所有树莓派都能使用一组叠加和参数，固件创建了一些特定于板的 DT 参数。这些是：

```
i2c/i2c_arm
i2c_vc
i2c_baudrate/i2c_arm_baudrate
i2c_vc_baudrate
```

这些是 i2c0 ， i2c1 ， i2c0_baudrate 和 i2c1_baudrate 的别名。建议仅在确实需要时使用 i2c_vc 和 i2c_vc_baudrate - 例如，如果您正在编程 HAT EEPROM（最好使用 i2c-gpio 叠加层使用软件 I2C 总线）。启用 i2c_vc 可能会导致树莓派相机或树莓派触摸显示屏无法正常工作。

对于编写叠加层的人，相同的别名已应用于 I2C DT 节点上的标签。因此，您应该编写：

```
fragment@0 {
    target = <&i2c_arm>;
    __overlay__ {
        status = "okay";
    };
};
```

使用数字变体的任何叠加层将被修改为使用新的别名。

#### HATs 和设备树

树莓派 HAT 是一个带有嵌入式 EEPROM 的附加板，专为具有 40 针引脚头的树莓派设计。EEPROM 包括启用板（或要从文件系统加载的叠加的名称）所需的任何 DT 叠加层，此叠加层还可以公开参数。

HAT 叠加层在基本 DTB 之后由固件自动加载，因此其参数可在加载任何其他叠加层之前访问，或者在使用 dtoverlay= 结束叠加层范围之前访问。如果出于某种原因您想要抑制 HAT 叠加层的加载，请在任何其他 dtoverlay 或 dtparam 指令之前放置 dtoverlay= 。

#### 动态设备树

从 Linux 4.4 开始，树莓派内核支持动态加载叠加和参数。兼容内核管理一个叠加的堆栈，这些叠加叠加在基本 DTB 之上。更改立即反映在 /proc/device-tree 中，可能导致模块被加载和平台设备被创建和销毁。

上面提到的“堆栈”一词很重要 - 叠加只能在堆栈顶部添加和移除；更改堆栈中较低位置的内容需要首先移除其顶部的任何内容。

有一些用于管理叠加的新命令：

##### dtoverlay 命令

dtoverlay 是一个命令行实用程序，可在系统运行时加载和移除叠加层，同时列出可用的叠加层并显示其帮助信息。

使用 `dtoverlay -h` 获取使用信息：

```
Usage:
  dtoverlay <overlay> [<param>=<val>...]
                           Add an overlay (with parameters)
  dtoverlay -D [<idx>]     Dry-run (prepare overlay, but don't apply -
                           save it as dry-run.dtbo)
  dtoverlay -r [<overlay>] Remove an overlay (by name, index or the last)
  dtoverlay -R [<overlay>] Remove from an overlay (by name, index or all)
  dtoverlay -l             List active overlays/params
  dtoverlay -a             List all overlays (marking the active)
  dtoverlay -h             Show this usage message
  dtoverlay -h <overlay>   Display help on an overlay
  dtoverlay -h <overlay> <param>..  Or its parameters
    where <overlay> is the name of an overlay or 'dtparam' for dtparams
Options applicable to most variants:
    -d <dir>    Specify an alternate location for the overlays
                (defaults to /boot/firmware/overlays or /flash/overlays)
    -v          Verbose operation
```

与 config.txt 等效不同，所有叠加的参数必须包含在同一条命令行中 - dtparam 命令仅用于基本 DTB 的参数。

更改内核状态的命令变体（添加和移除内容）需要 root 权限，因此您可能需要在命令前加上 sudo 。只有在运行时应用的叠加和参数可以被卸载 - 固件应用的叠加或参数会被“烘焙”，因此不会被 dtoverlay 列出，也无法移除。

##### dtparam 命令

dtparam 创建并加载一个覆盖层，其效果基本与在 config.txt 中使用 dtparam 指令相同。在使用上，它与具有 - 的覆盖层名称的 dtoverlay 基本等效，但存在一些差异： dtparam 将列出基础 DTB 的所有已知参数的帮助信息。仍然可以使用 dtparam -h 获取有关 dtparam 命令的帮助。在指示要移除的参数时，只能使用索引号（而非名称）。并非所有 Linux 子系统都会在运行时响应设备的添加 - I2C、SPI 和声音设备可以工作，但有些则不行。

##### 撰写运行时可用覆盖层的指南

创建或删除设备对象是由添加或移除节点，或节点状态从禁用变为启用或反之触发的。"status"属性的缺失意味着节点已启用。

不要在将覆盖基础 DTB 中现有节点的片段内创建节点 - 内核将重命名新节点以使其唯一。如果要更改现有节点的属性，请创建一个针对它的片段。

ALSA 不会阻止其编解码器和其他组件在使用中被卸载。在使用中删除叠加可能会导致内核异常，如果删除的编解码器仍在声卡中使用。实验发现设备在叠加中以片段顺序的相反顺序被删除，因此将卡的节点放在组件节点之后允许有序关闭。

##### 注意事项

在运行时加载叠加层是内核的一个最新功能，截至撰写本文时，尚无一种被接受的方法可以从用户空间执行此操作。通过将此机制的细节隐藏在命令背后，用户可以在不同内核接口标准化的情况下免受影响。

* 一些叠加层在运行时的效果比其他叠加层更好。设备树的某些部分仅在引导时使用 - 使用叠加层更改它们不会产生任何效果。
* 应用或移除一些叠加层可能会导致意外行为，因此应谨慎进行。这就是需要 sudo 的原因之一。
* 卸载 ALSA 卡的叠加层可能会因为某些正在使用 ALSA 的活动而停滞不前 - LXPanel 音量滑块插件展示了这种效果。为了使声卡的叠加层能够被移除， lxpanelctl 实用程序已被赋予两个新选项 - alsastop 和 alsastart - 并且这些选项在加载或卸载叠加层之前和之后分别从辅助脚本 dtoverlay-pre 和 dtoverlay-post 中调用。
* 移除叠加层不会导致已加载的模块被卸载，但可能会导致一些模块的引用计数降至零。运行 rmmod -a 两次将导致未使用的模块被卸载。
* 覆盖必须按相反顺序移除。这些命令将允许您移除较早的覆盖，但所有中间的覆盖将被移除并重新应用，这可能会产生意想不到的后果。
* 仅会探测树顶层和总线节点的子级的设备树节点。对于运行时添加的节点，进一步的限制是总线必须注册通知以添加和移除子级。但是，有一些例外情况会打破这个规则并引起混淆：内核明确扫描整个树以寻找某些设备类型 - 时钟和中断控制器是主要的两种 - 以便（对于时钟）早期初始化它们和/或（对于中断控制器）按特定顺序初始化。这种搜索机制仅在引导过程中发生，因此对于运行时由覆盖添加的节点不起作用。因此，建议将固定时钟节点放在树的根部，除非保证覆盖不会在运行时使用。

#### 支持的覆盖和参数

请参考 /boot/firmware/overlays 中找到的叠加 .dtbo 文件旁边的 README 文件。它会随着添加和更改而保持最新。

### 固件参数

固件使用特殊的 `/chosen` 节点在引导加载程序和/或固件与操作系统之间传递参数。除非另有说明，否则每个属性都存储为 32 位整数。

overlay_prefix （字符串）由 config.txt 选择的 overlay_prefix 字符串。

os_prefix （字符串）由 config.txt 选择的 os_prefix 字符串。

rpi-boardrev-ext 来自 OTP 行 33 的扩展板修订代码。

rpi-country-code PiWiz 使用的国家代码。仅适用于树莓派 400。

rpi-duid （字符串）仅适用于树莓派 5。PCB 上 QR 码的字符串表示。

#### 通用引导加载程序属性 `/chosen/bootloader`

除非另有说明，否则每个属性都存储为 32 位整数。

boot-mode 用于加载内核的引导模式。请参阅 BOOT_ORDER。

partition 引导过程中使用的分区号。如果加载了 boot.img ramdisk，则此引用的是 ramdisk 中加载的分区，而不是 ramdisk 内部的分区号。

pm_rsts 引导过程中 PM_RSTS 寄存器的值。

tryboot 如果在启动时设置了 tryboot 标志，则设置为 1 。

#### 电源供应属性 `/chosen/power`

仅适用于树莓派5。除非另有说明，否则每个属性均存储为 32 位整数。

max_current 电源供应器可以提供的最大电流（以毫安为单位）。固件报告由 USB-C、USB-PD 或 PoE 接口指示的值。对于台式电源供应器（例如连接到 GPIO 标头），请在引导加载程序配置中定义 PSU_MAX_CURRENT 以指示电源供应器的电流能力。

power_reset 仅适用于树莓派 5。一个位字段，指示 PMIC 被重置的原因。

| 位 | 原因     |
| ---- | ---------- |
| 0  | 过压     |
| 1  | 低电压   |
| 2  | 高温     |
| 3  | 启用信号 |
| 4  | 看门狗   |

rpi_power_supply （两个 32 位整数）官方树莓派 27W 电源适配器的 USB VID 和 Product VDO（如果连接）。

usb_max_current_enable 如果 USB 端口电流限制器在启动时设置为低限，则为零；如果启用了高限，则为非零。如果电源适配器声称最大电流为 5A 或者在 config.txt 中强制使用 usb_max_current_enable=1 ，则自动启用高电平。

usb_over_current_detected 如果在 USB 启动期间发生 USB 过流事件，则为非零值。

usbpd_power_data_objects （包含多个 32 位整数的二进制数据块）引导加载程序在 USB-PD 协商期间接收到的原始二进制 USB-PD 对象（仅限固定供电）。要为错误报告捕获此内容，请运行 hexdump -C /proc/device-tree/chosen/power/usbpd_power_data_objects 。

格式由 USB 供电规范定义。

#### BCM2711 和 BCM2712 特定的引导加载程序属性 /chosen/bootloader

以下属性特定于 BCM2711 和 BCM2712 SPI EEPROM 引导加载程序。除非另有说明，否则每个属性都存储为 32 位整数。

build_timestamp EEPROM 引导加载程序的 UTC 构建时间。

capabilities 这个位字段描述了当前引导加载程序支持的功能。这可以用来在引导加载程序 EEPROM 配置中启用功能（例如 USB 启动）之前检查是否支持。

| 位 | 功能                                     |
| ---- | ------------------------------------------ |
| 0  | 使用 VLI USB 主机控制器进行 USB 引导     |
| 1  | [ 网络引导](https://www.raspberrypi.com/documentation/computers/remote-access.html#network-boot-your-raspberry-pi)                                         |
| 2  | TRYBOOT_A_B 模式                         |
| 3  | [TRYBOOT](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#fail-safe-os-updates-tryboot)                                         |
| 4  | 使用 BCM2711 USB 主机控制器进行 USB 引导 |
| 5  | [RAM 磁盘 - boot.img](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#boot_ramdisk)                                         |
| 6  | [ NVMe 引导](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#nvme-ssd-boot)                                         |
| 7  | [ 安全启动](https://github.com/raspberrypi/usbboot/blob/master/Readme.md#secure-boot)                                         |

update_timestamp 由 rpi-eeprom-update 设置的 UTC 更新时间戳。

signed 如果启用了安全启动，则此位字段将为非零。各个位指示当前的安全启动配置。

| 位    | 说明                                            |
| ------- | ------------------------------------------------- |
| 0     | SIGNED_BOOT 已在 EEPROM 配置文件中定义。        |
| 1     | 保留                                            |
| 2     | ROM 开发密钥已被吊销。请参阅 revoke_devkey。    |
| 3     | 客户公钥摘要已写入 OTP。请参阅 program_pubkey。 |
| 4…31 | 保留                                            |

version (字符串) 用于引导加载程序的 Git 版本字符串。

#### BCM2711 和 BCM2712 USB 引导属性 /chosen/bootloader/usb

如果系统是从 USB 引导的，则定义以下属性。这些属性可用于唯一标识 USB 引导设备。每个属性存储为 32 位整数。

usb-version USB 主协议版本（2 或 3）。

route-string 由 USB 3.0 规范定义的设备的 USB 路由字符串标识符。

root-hub-port-number 引导设备连接到的根集线器端口号 - 可能通过其他 USB 集线器连接。

lun 用于大容量存储设备的逻辑单元号。

#### NVMEM 节点

固件通过 NVMEM 子系统提供引导加载程序 EEPROM 部分的只读内存副本。

每个区域在 /sys/bus/nvmem/devices/ 下显示为一个 NVMEM 设备，在 /sys/firmware/devicetree/base/aliases 下显示为一个命名别名。

从 rpi-eeprom-update 读取 NVMEM 模式的示例 shell 脚本代码。

```
blconfig_alias="/sys/firmware/devicetree/base/aliases/blconfig"
blconfig_nvmem_path=""

if [ -f "${blconfig_alias}" ]; then
   blconfig_ofnode_path="/sys/firmware/devicetree/base"$(strings "${blconfig_alias}")""
   blconfig_ofnode_link=$(find -L /sys/bus/nvmem -samefile "${blconfig_ofnode_path}" 2>/dev/null)
   if [ -e "${blconfig_ofnode_link}" ]; then
      blconfig_nvmem_path=$(dirname "${blconfig_ofnode_link}")
      fi
   fi
fi
```

blconfig 别名，指向存储引导加载程序 EEPROM 配置文件副本的 NVMEM 设备。

blpubkey 别名，指向以二进制格式存储引导加载程序 EEPROM 公钥副本（如果已定义）的 NVMEM 设备。可以使用 rpi-bootloader-key-convert 实用程序将数据转换为 PEM 格式，以便与 OpenSSL 一起使用。

有关更多信息，请参阅安全启动。

### 故障排除

#### 调试

加载程序将跳过缺少的叠加和错误参数，但如果存在严重错误，比如缺少或损坏的基本 DTB 或失败的叠加合并，那么加载程序将退回到非 DT 引导。如果发生这种情况，或者如果您的设置不符合您的期望，值得检查加载程序的警告或错误：

```
$ sudo vclog --msg
```

通过将 dtdebug=1 添加到 config.txt 可以启用额外的调试。

您可以这样创建当前 DT 状态的人类可读表示：

```
$ dtc -I fs /proc/device-tree
```

这对于查看将叠加层合并到基础树上的效果可能很有用。

如果内核模块未按预期加载，请检查它们是否在 /etc/modprobe.d/raspi-blacklist.conf 中被列入黑名单；在使用设备树时，不应该需要列入黑名单。如果没有发现任何异常，您还可以通过在 /lib/modules/<version>/modules.alias 中搜索 compatible 值来检查模块是否导出了正确的别名。否则，您的驱动程序可能缺少以下内容之一：

```
.of_match_table = xxx_of_match,
```

 要么：

```
MODULE_DEVICE_TABLE(of, xxx_of_match);
```

如果失败， depmod 失败了，或者更新的模块尚未安装在目标文件系统上。

#### 使用 dtmerge 、 dtdiff 和 ovmerge 测试叠加。

除了 dtoverlay 和 dtparam 命令之外，还有一个用于将叠加应用到 DTB 的实用程序 - dtmerge 。要使用它，您首先需要获取基本的 DTB，可以通过以下两种方式之一获取：

从 /proc/device-tree 中的实时 DT 状态生成它：

```
$ dtc -I fs -O dtb -o base.dtb /proc/device-tree
```

这将包括您迄今为止在 config.txt 中应用的任何叠加和参数，或者通过在运行时加载它们，这可能是您想要的，也可能不是。或者：

从 /boot/firmware/ 中的源 DTB 复制它。这不会包括叠加和参数，但也不会包括固件的任何其他修改。为了允许测试所有叠加， dtmerge 实用程序将创建一些特定于板的别名（"i2c_arm" 等），但这意味着合并的结果将与原始 DTB 有更多差异。您可能期望的不同。解决此问题的方法是使用 dtmerge 进行复制：

```
$ dtmerge /boot/firmware/bcm2710-rpi-3-b.dtb base.dtb -
```

( - 表示不存在的叠加名称)。

您现在可以尝试应用叠加或参数：

```
$ dtmerge base.dtb merged.dtb - sd_overclock=62
$ dtdiff base.dtb merged.dtb
```

 这将返回：

```
--- /dev/fd/63  2016-05-16 14:48:26.396024813 +0100
+++ /dev/fd/62  2016-05-16 14:48:26.396024813 +0100
@@ -594,7 +594,7 @@
                };

                sdhost@7e202000 {
-                       brcm,overclock-50 = <0x0>;
+                       brcm,overclock-50 = <0x3e>;
                        brcm,pio-limit = <0x1>;
                        bus-width = <0x4>;
                        clocks = <0x8>;
```

您还可以比较不同的叠加或参数。

```
$ dtmerge base.dtb merged1.dtb /boot/firmware/overlays/spi1-1cs.dtbo
$ dtmerge base.dtb merged2.dtb /boot/firmware/overlays/spi1-2cs.dtbo
$ dtdiff merged1.dtb merged2.dtb
```

 要获得：

```
--- /dev/fd/63  2016-05-16 14:18:56.189634286 +0100
+++ /dev/fd/62  2016-05-16 14:18:56.189634286 +0100
@@ -453,7 +453,7 @@

                        spi1_cs_pins {
                                brcm,function = <0x1>;
-                               brcm,pins = <0x12>;
+                               brcm,pins = <0x12 0x11>;
                                phandle = <0x3e>;
                        };

@@ -725,7 +725,7 @@
                        #size-cells = <0x0>;
                        clocks = <0x13 0x1>;
                        compatible = "brcm,bcm2835-aux-spi";
-                       cs-gpios = <0xc 0x12 0x1>;
+                       cs-gpios = <0xc 0x12 0x1 0xc 0x11 0x1>;
                        interrupts = <0x1 0x1d>;
                        linux,phandle = <0x30>;
                        phandle = <0x30>;
@@ -743,6 +743,16 @@
                                spi-max-frequency = <0x7a120>;
                                status = "okay";
                        };
+
+                       spidev@1 {
+                               #address-cells = <0x1>;
+                               #size-cells = <0x0>;
+                               compatible = "spidev";
+                               phandle = <0x41>;
+                               reg = <0x1>;
+                               spi-max-frequency = <0x7a120>;
+                               status = "okay";
+                       };
                };

                spi@7e2150C0 {
```

Utils 存储库包含另一个 DT 实用程序 - ovmerge 。与 dtmerge 不同， ovmerge 结合了文件并以源形式应用叠加。由于叠加从未被编译，标签得以保留，结果通常更易读。它还具有许多其他技巧，例如能够列出文件包含的顺序。

#### 强制使用特定的设备树

如果您有非常特定的需求，而默认的 DTB 不支持这些需求，或者您只是想尝试编写自己的 DT，请告诉加载程序加载替代的 DTB 文件，就像这样：

```
device_tree=my-pi.dtb
```

#### 禁用设备树使用

树莓派 Linux 内核中需要使用设备树。对于裸机和其他操作系统，可以通过添加以下内容来禁用设备树使用：

```
device_tree=
```

 到 config.txt 。

#### 快捷方式和语法变体

加载程序理解一些快捷方式：

```
dtparam=i2c_arm=on
dtparam=i2s=on
```

可以缩短为：

```
dtparam=i2c,i2s
```

（ i2c 是 i2c_arm 的别名， =on 被假定）。它仍然接受长形式版本： device_tree_overlay 和 device_tree_param 。

#### config.txt 中可用的其他 DT 命令

device_tree_address 这用于覆盖固件加载设备树的地址（不是 dt-blob）。默认情况下，固件将选择一个合适的位置。

device_tree_end 这将对加载的设备树设置（独占）限制。默认情况下，设备树可以增长到可用内存的末尾，这几乎肯定是所需的。

dtdebug 如果非零，则打开固件的设备树处理的一些额外日志记录。

enable_uart 启用主/控制台 UART（在树莓派 3、4、400、Zero W 和 Zero 2 W 上为 ttyS0，在其他情况下为 ttyAMA0 - 除非与诸如 miniuart-bt 的叠加交换）。如果主 UART 是 ttyAMA0，则 enable_uart 默认为 1（已启用），否则默认为 0（已禁用）。这是因为有必要阻止核心频率的变化，否则会使 ttyS0 无法使用，因此 enable_uart=1 意味着 core_freq=250 （除非 force_turbo=1 ）。在某些情况下，这会影响性能，因此默认情况下关闭。

overlay_prefix 指定要从中加载叠加的子目录/前缀 - 默认为 "overlays/"。请注意末尾的“/”。如果需要，您可以在最后一个“/”后添加内容以向每个文件添加前缀，尽管这可能不是必要的。

进一步的端口可以通过 DT 进行控制。有关更多详细信息，请参阅第 3 节。

#### 进一步帮助

如果您阅读了本文档但未找到解决设备树问题的答案，可以获得帮助。作者通常可以在 Raspberry Pi 论坛上找到，特别是设备树论坛。

## 更改默认引脚配置

>**注意**
>
>通过用户提供的设备树 blob 自定义默认引脚配置已被弃用。 

### 引导序列期间的设备引脚

在引导序列期间，GPIO 引脚经历各种操作。

* 上电 - 引脚默认为具有默认拉电阻的输入，这些电阻在数据表中有描述
* 由 bootrom 设置
* 通过 bootcode.bin 设置
* 通过 dt-blob.bin 设置（本页）
* 通过 GPIO 命令在 config.txt 中设置
* 附加固件引脚（例如 UARTS）
* 内核/设备树

在软复位时，相同的过程适用，除了默认拉引脚，这些只在上电复位时应用。

通过过程可能需要几秒钟。在此期间，GPIO 引脚可能不处于附加外围设备期望的状态（如 dt-blob.bin 或 config.txt 中定义）。由于不同的 GPIO 引脚具有不同的默认拉电阻，您应该针对您的外围设备执行以下操作之一：

* 选择一个在复位时默认为外围设备所需拉电阻的 GPIO 引脚
* 推迟外围设备的启动，直到操作完成
* 添加适当的上拉/下拉电阻

### 提供自定义设备树 blob

为了将设备树源（ .dts ）文件编译成设备树 blob（ .dtb ）文件，必须安装设备树编译器，方法是运行 sudo apt install device-tree-compiler 。然后可以使用 dtc 命令如下：

```
$ sudo dtc -I dts -O dtb -o /boot/firmware/dt-blob.bin dt-blob.dts
```

同样，如果需要，可以将 .dtb 文件转换回 .dts 文件。

```
$ dtc -I dtb -O dts -o dt-blob.dts /boot/firmware/dt-blob.bin
```

### dt-blob 的各个部分

dt-blob.bin 用于在启动时配置二进制块（VideoCore）。Linux 内核目前不使用它。dt-blob 可以配置所有版本的树莓派，包括计算模块，以使用替代设置。dt-blob 中以下部分有效：

#### `videocore`

本部分包含所有 VideoCore blob 信息。所有后续部分必须包含在此部分内。

#### `pins_*`

有许多单独的 pins_* 部分，基于特定的树莓派型号，即：

* pins_rev1 ：Rev1 引脚设置。由于移动的 I2C 引脚，存在一些差异。
* pins_rev2 ：Rev2 引脚设置。这包括 P5 上的附加编解码器引脚。
* pins_bplus1 ：树莓派 1 型 B+ rev 1.1，包括完整的 40 针连接器。
* pins_bplus2 ：树莓派 1 型 B+ rev 1.2，交换低功耗和 lan-run 引脚。
* pins_aplus ：树莓派 1 型 A+，无以太网。
* pins_2b1 ：树莓派 2 型 B rev 1.0；通过 I2C0 控制开关电源管理系统。
* pins_2b2 ：树莓派 2 型 B rev 1.1；通过软件 I2C 在 42 和 43 上控制开关电源管理系统。
* pins_3b1 ：树莓派 3 型 B 型修订版 1.0
* pins_3b2 ：树莓派 3 型 B 型修订版 1.2
* pins_3bplus ：树莓派 3 型 B+
* pins_3aplus ：树莓派 3 型 A+
* pins_pi0 ：树莓派 Zero
* pins_pi0w ：树莓派 Zero W
* pins_pi02w ：树莓派 Zero 2 W
* pins_cm ：树莓派计算模块 1。默认情况下，这是芯片的默认设置，因此它是关于芯片上默认上拉/下拉的有用信息来源。
* pins_cm3 ：树莓派计算模块 3
* pins_cm3plus ：树莓派计算模块 3+
* pins_cm4s ：树莓派计算模块 4S
* pins_cm4 ：树莓派计算模块 4

每个 pins_* 部分都可以包含 pin_config 和 pin_defines 部分。

#### `pin_config`

pin_config 部分用于配置各个引脚。该部分中的每个项目必须是一个命名的引脚部分，例如 pin@p32 ，表示 GPIO32。还有一个特殊部分 pin@default ，其中包含未在 pin_config 部分中明确命名的任何内容的默认设置。

#### `pin@pinname`

该部分可以包含以下项目的任意组合：

* `polarity`

  * `active_high`
  * `active_low`
* `termination`

  * `pull_up`
  * `pull_down`
  * `no_pulling`
* `startup_state`

  * `active`
  * `inactive`
* `function`

  * `input`
  * `output`
  * `sdcard`
  * `i2c0`
  * `i2c1`
  * `spi`
  * `spi1`
  * `spi2`
  * `smi`
  * `dpi`
  * `pcm`
  * `pwm`
  * `uart0`
  * `uart1`
  * `gp_clk`
  * `emmc`
  * `arm_jtag`
* 驱动强度用于设置引脚的强度。请注意，您只能为该银行指定单个驱动强度。 <8> 和 <16> 是有效值。

#### `pin_defines`

此部分用于将特定的 VideoCore 功能设置为特定的引脚。这使用户可以将摄像头电源使能引脚移动到其他位置，或将 HDMI 热插拔位置移动：这些是 Linux 无法控制的事情。请参考下面的示例 DTS 文件。

### 时钟配置

通过这个界面可以改变时钟的配置，尽管很难预测结果！时钟系统的配置非常复杂。有五个单独的 PLL，每个 PLL 都有自己固定（或可变，对于 PLLC 的情况）的 VCO 频率。然后，每个 VCO 都有许多不同的通道，可以使用不同的 VCO 频率分频。每个时钟目的地都可以配置为来自其中一个时钟通道，尽管源到目的地的映射受到限制，因此并非所有通道都可以路由到所有时钟目的地。

这里有一些示例配置，您可以用来更改特定的时钟。当请求时钟配置时，我们将添加到此资源。

```
clock_routing {
   vco@PLLA  {    freq = <1966080000>; };
   chan@APER {    div  = <4>; };
   clock@GPCLK0 { pll = "PLLA"; chan = "APER"; };
};

clock_setup {
   clock@PWM { freq = <2400000>; };
   clock@GPCLK0 { freq = <12288000>; };
   clock@GPCLK1 { freq = <25000000>; };
};
```

以上内容将把 PLLA 设置为运行在 1.96608GHz 的源 VCO（此 VCO 的限制为 600MHz - 2.4GHz），将 APER 通道更改为/4，并配置 GPCLK0 从 PLLA 通过 APER 进行源控制。这用于为音频编解码器提供所需的 12288000Hz，以产生 48000 范围的频率。

### 样本设备树源文件

固件存储库包含一个主 Raspberry Pi blob，通常从中派生其他内容。
