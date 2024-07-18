# 系统配置

## `raspi-config`

>**技巧**
>
>树莓派桌面用户可以使用这款软件的图形化版本，位于“**首选项（Preferences）**”>“**树莓派配置（Raspberry Pi Configuration）**”。但是，某些高级配置仅存在于 `raspi-config`。

`raspi-config` 能帮助你配置树莓派。在不同型号的树莓派间，能进行配置的选项也不尽相同。若要打开这个配置工具，请执行以下命令：

```
$ sudo raspi-config
```

你应该会在灰色窗口内，看到蓝色背景的界面，并附带了各种选项：

![raspi-config 主菜单](../.gitbook/assets/raspi-config.png)

你用 **上箭头（↑）**、**下箭头（↓）** 就能在可选条目之间自由切换，并对当前所选高亮显示。

按 **右箭头（→）**、**Tab 键** 可选择按钮 `<Select>` 和 `<Finish>`。按 **左箭头（←）**、**Tab 键** 可返回上一级菜单。

`raspi-config` 会自动编辑 [`/boot/firmware/config.txt`](https://www.raspberrypi.com/documentation/computers/config_txt.html#what-is-config-txt)，以及相关 Linux 配置文件。某些选项可能需要重启才能生效：如果你修改了他们当中任何一个，在退出时，`raspi-config` 会要求你重启。

>**技巧**
>
>在选项值所提供的长长的列表中（如时区城市列表），输入单个字母即可跳转到列表中的对应部分。例如，输入 `L` 会跳转至 Lisbon（里斯本）。

### System options——系统选项

系统选项（System options）的子菜单：能让你对启动、登录和网络过程的相关部分进行配置修改，以及某些其他系统级的修改。

![raspi-config system options（系统选项）](../.gitbook/assets/raspi-system.png)

#### Wireless LAN——无线局域网（WLAN）

可配置 WiFi 网络名称（SSID）和密码。

#### Audio——音频

指定音频输出位置。

#### Password——密码

修改你的密码。

获取更多信息，请参阅[修改用户密码](https://www.raspberrypi.com/documentation/computers/configuration.html#change-user-password)。

#### Hostname——主机名

在网络上为树莓派设置可见的 [mDNS](https://www.raspberrypi.com/documentation/computers/remote-access.html#resolve-raspberrypi-local-with-mdns) 域名。

#### Boot/auto login——启动/自动登录

选择是启动到控制台，还是桌面。以及在接通电源时，是否自动登录到当前用户账户。

#### Network at boot——启动时联网

在启动前等待网络连接。

#### Splash screen——启动画面

启用或禁用：开机时显示的启动画面。

#### Power LED——电源灯

如果你的树莓派型号支持，可以修改电源灯的行为。

#### Browser——浏览器

修改默认的网络浏览器。

### Display options——显示选项

![raspi-config display options（显示选项）](../.gitbook/assets/raspi-display.png)

#### Underscan——欠扫描

>**注意**
>
>在 Wayland 下不可用。

如果屏幕上显示的文本开端消失在屏幕边缘，可启用 overscan（过扫描）调整边框。在某些显示器上，特别是监控器上，禁用过扫描会使镜像充满整个屏幕，且不带黑边。

#### Screen blanking——屏幕节能（无操作时关闭屏幕）

启用或禁用：Screen blanking——屏幕节能（无操作时关闭屏幕）。

#### VNC resolution——VNC 分辨率

用于[无头](https://www.raspberrypi.com/documentation/computers/configuration.html#setting-up-a-headless-raspberry-pi)设置所使用的显示分辨率。

#### Composite——复合视频

启用或禁用复合视频（composite video）。

#### 4Kp60 HDMI

启用或禁用：HDMI 的 4K 60p 分辨率输出。

### Interface options——接口选项

启用和禁用各种物理、虚拟接口。

![raspi-config interface options（接口选项）](../.gitbook/assets//raspi-interface.png)

#### SSH

启用或禁用：树莓派终端 SSH 远程访问。

SSH 能让你在另一台计算机上，远程访问树莓派的命令行。在默认情况下，SSH 处于禁用状态。在 [SSH 文档页](https://www.raspberrypi.com/documentation/computers/remote-access.html#ssh)上能阅读更多关于 SSH 的使用信息。如果你将树莓派直接接入到了公共网络，请不要启用 SSH，除非你为所有用户都设置了安全的密码。

#### VNC

启用或禁用：WayVNC、RealVNC 虚拟网络计算服务（virtual network computing，VNC）。

#### SPI

启用或禁用：SPI 接口，是否自动加载 SPI 内核模块。

#### I2C——I²C

启用或禁用：I²C 接口，是否自动加载 I²C 内核模块。

#### Serial port——串口

启用或禁用：串口上的 shell 及内核信息输出。

#### 1-Wire——单总线

启用或禁用：单总线（Dallas 1-wire）接口，通常用于 DS18B20 温度传感器。

#### Remote GPIO——GPIO 远程访问

启用或禁用：GPIO 引脚的远程访问。

### Performance options——性能选项

![raspi-config performance options（性能选项）](../.gitbook/assets//raspi-perf.png)

#### Overclock——超频

如果你的树莓派型号支持，就能对 CPU 超频。超频能力因树莓派设备个体体质而异，即使是相同型号也会有所不同。超频过高可能会导致不稳定。

>**警告**
>
>**超频可能会缩短你树莓派的使用寿命。** 如果因某个特定级别的超频导致系统不稳定，可以试试较为保守的超频。在启动过程中按住 **Shift** 键可临时禁用超频。

#### GPU memory——GPU 显存

修改向 GPU 提供的内存大小。①

#### Overlay file system——堆叠文件系统（OverlayFS）

启用或禁用：只读文件系统。

#### Fan——风扇

可自定义接入 GPIO 的风扇行为（[树莓派 4 外壳](https://www.raspberrypi.com/products/raspberry-pi-4-case-fan/)自带）。对[树莓派 5 外壳自带风扇](https://www.raspberrypi.com/products/raspberry-pi-5-case/)、[树莓派 5 主动散热器](https://www.raspberrypi.com/products/active-cooler/)（使用特殊四针风扇头）无效。

### Localisation options——本地化选项

配置位置、国家/地区相关选项。

![raspi-config localisation options（本地化选项）](../.gitbook/assets//raspi-l18n.png)

#### Locale——语言环境

可选择语言环境，如 `zh_CN.UTF-8 UTF-8`（中文）或 `en_GB.UTF-8 UTF-8`（英语）。

#### Time zone——时区

设置你的本地时区，从地区（Asia，亚洲）开始，然后选择城市（北京时间为 Shanghai）②，例如"Asia/Shanghai"。键入单个字母可跳转到列表中的该字母。

#### Keyboard——键盘

将打开菜单，你可以在其中选择你的键盘布局（中国使用标准美式键盘布局）。通常修改会立即生效，但可能需要重启。键入单个字母会跳转到列表中的该字母。

#### WLAN country——无线局域网区域

为你的无线网络设置区域码。

### Advanced options——高级选项

![raspi-config advanced options（高级选项）](../.gitbook/assets//raspi-adv.png)

#### Expand filesystem——扩大文件系统

扩大你的操作系统分区，以便利用整个存储设备，从而带来更大的文件存储空间。要完成此操作，你需重启树莓派。通常，在首次启开机时，树莓派系统会执行此操作。如果你把你的操作系统克隆到了容量大于旧设备的其他存储设备上，该功能可能会极其有用。

>**警告**
>
>没有再确认的步骤。选择该选项将立即开始分区扩展操作。

#### Network interface names——网络接口名称

启用或禁用：可预测的网络接口名称。

#### Network proxy settings——设置网络代理

配置网络代理。

#### Boot order——启动顺序

在树莓派 4 及后续新款设备上，设定：在未插入 SD 卡的情况下，是否从 USB、网络进行启动。有关更多信息，请参阅[启动加载程序配置](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#raspberry-pi-bootloader-configuration)。

#### Bootloader version——引导加载程序版本

在树莓派 4 及后续新款设备上，更新到最新的 ROM 引导软件。或者，倘若最新版本引发了故障，你可以在此恢复出厂默认设置。

#### Wayland

在 X11 后端和 Wayland 后端间进行切换。在树莓派 4 及后续新款设备上，默认使用 Wayland。其他型号的树莓派默认使用 X11。

>**注意**
>
>要在树莓派 4 先前的型号上使用 Wayland，你还必须把 `wayland=on` 添加至 `/boot/firmware/cmdline.txt`。

#### Audio config——音频配置

在 Bookworm 以前，树莓派系统使用 PulseAudio，现在则可以在音频后端 PulseAudio 和 PipeWire 之间进行切换。

### Update——更新

把 `raspi-config` 更新到最新版本。

### About raspi-config——关于 raspi-config

`raspi-config` 相关说明。

### Finish——完成

退出 `raspi-config`。如果你进行的修改需要重启，`raspi-config` 会提示你重启。首次进行修改时，最好重启。如果选择了调整 SD 卡大小，重启可能会花比平时更久的时间。

## 非交互式 raspi-config

工具 `raspi-config` 还支持非交互式选项及参数，无需可视化组件，就可以用命令行修改所有选项。可用选项可能因树莓派型号而异。

```
$ sudo raspi-config nonint <命令> <参数> [可选参数]
```

>**注意**
>
> 对于不同选项来说，`0` 和 `1` 的含义也不尽相同。在将值赋给参数之前，请始终参照文档。

### System options——系统选项

#### Wireless LAN——无线局域网（WLAN）

配置 WiFi 网络名称（SSID）和密码。

```
$ sudo raspi-config nonint do_wifi_ssid_passphrase <网络名称> <密码> [隐藏的网络] [明文]
```

填入无线网络名称（SSID）和密码（如需要）。以下是可选参数：

参数 `<隐藏的网络>` 代表网络名称可见性。如果网络名称开放广播，请使用 `0` 或者省略该参数。如果你的网络名称是隐藏的，请填 `1`。默认为 `0`。

参数 `<明文>` 代表你是否打算明文传输密码。如果你的密码包含空格、特殊字符（如 `!`)，则必须使用 `0`，并在密码两头加上英文双引号 `"`。如无以上情形，你可以传递 `1` 或者省略该参数。默认为 `1`。但若要使用此参数，你必须同时赋值给 `<隐藏的网络>`。

例如，通过执行以下命令，可以连接至：

* 未隐藏的网络 `myssid`，密码为 `mypassphrase`：

  ```
  $ sudo raspi-config nonint do_wifi_ssid_passphrase myssid mypassphrase
  ```
* 隐藏的网络 `myssid`，密码为 `mypassphrase`：

  ```
  $ sudo raspi-config nonint do_wifi_ssid_passphrase myssid mypassphrase 1
  ```
* 未隐藏的网络 `myssid`，密码为 `my passphrase`：

  ```
  $ sudo raspi-config nonint do_wifi_ssid_passphrase myssid "my passphrase" 0 0
  ```

#### Audio——音频

指定音频输出位置。

```
$ sudo raspi-config nonint do_audio <数字>
```

在树莓派 4B 上，你可以使用以下参数：

* `0`：bcm2835 headphone jack（耳机插孔）
* `1`：vc4-hdmi-0
* `2`：vc4-hdmi-1

要查看此参数 `<数字>` 所有可用值的列表，请参阅交互版 `raspi-config` 中所使用的缩写。

#### Password——密码

修改你的密码。

有关修改用户密码的更多信息，请参阅[修改用户密码](https://www.raspberrypi.com/documentation/computers/configuration.html#change-user-password)。

```
$ sudo raspi-config nonint do_change_pass
```

>**注意**
>
>此功能会使用全屏界面进行交互，即使在命令行执行参数也是一样的。

#### Hostname——主机名

在网络上为此树莓派设置可见的 [mDNS](https://www.raspberrypi.com/documentation/computers/remote-access.html#resolve-raspberrypi-local-with-mdns) 域名。

```
$ sudo raspi-config nonint do_hostname <主机名>
```

#### Boot/auto login——启动/自动登录

选择：启动到控制台，还是桌面；在接通电源时，是否自动登录到当前用户账户。

```
$ sudo raspi-config nonint do_boot_behaviour <B1/B2/B3/B4>
```

* `B1`：启动到控制台，需要登录
* `B2`：启动到控制台，自动登录
* `B3`：启动到桌面，需要登录
* `B4`：启动到桌面，自动登录

#### Network at boot——启动时联网

是否在启动前等待网络连接。

```
$ sudo raspi-config nonint do_boot_wait <0/1>
```

* `0`：启动前不等待网络连接
* `1`：启动前等待网络连接

#### Splash screen——启动画面

启用或禁用：启动时显示的启动画面。

```
$ sudo raspi-config nonint do_boot_splash <0/1>
```

* `0`：启用启动画面
* `1`：禁用启动画面

#### Power LED——电源灯

如果你的树莓派型号支持，可以修改电源灯的行为。

```
$ sudo raspi-config nonint do_leds <0/1>
```

* `0`：用闪烁代表磁盘活动状态
* `1`：电源灯常亮


#### Browser——浏览器

修改默认的网络浏览器。如所选的网络浏览器在当前并未安装，将不生效。

```
$ sudo raspi-config nonint do_browser <chromium-browser/firefox>
```

### Display options——显示选项

#### Underscan——欠扫描

>**注意**
>
>在 Wayland 下不可用。

如果屏幕上显示的文本开端在屏幕边缘消失，可启用 overscan（过扫描）调整边框。在某些显示器上，特别是监控器上，禁用过扫描会把镜像填充到整个屏幕，且不带黑边。

```
$ sudo raspi-config nonint do_overscan_kms <device> <enabled>
```

设备:

* `1`: HDMI-1
* `2`: HDMI-2

启用：

* `0`：启用过扫描
* `1`：禁用过扫描

#### Screen blanking——屏幕节能

启用或禁用：屏幕节能（无操作时关闭屏幕）。

```
$ sudo raspi-config nonint do_blanking <0/1>
```

* `0`：启用屏幕节能（无操作时关闭屏幕）
* `1`：禁用屏幕节能（无操作时不会关闭屏幕）

#### VNC resolution——VNC 分辨率

用于[无头](https://www.raspberrypi.com/documentation/computers/configuration.html#setting-up-a-headless-raspberry-pi)设置所使用的显示分辨率。

```
$ sudo raspi-config nonint do_vnc_resolution <宽>x<高>
```

#### Composite——复合视频

启用或禁用复合视频（composite video）。

在树莓派 4 上：

```
$ sudo raspi-config nonint do_pi4video <V1/V2/V3>
```

* `V1`：启用 HDMI 4K 60p 输出
* `V2`：启用复合视频输出
* `V3`：禁用 4K 60p 和复合输出

对于其他型号：

```
$ sudo raspi-config nonint do_composite <0/1>
```

* `0`：启用复合视频
* `1`：禁用复合视频

### Interface options——接口选项

#### SSH

启用或禁用：树莓派终端 SSH 远程访问。

SSH 能让你在另一台计算机远程访问树莓派的命令行。有关 SSH 的更多信息，请参阅 [SSH 文档](https://www.raspberrypi.com/documentation/computers/remote-access.html#ssh)。

```
$ sudo raspi-config nonint do_ssh <0/1>
```

* `0`：启用 SSH
* `1`：禁用 SSH

#### VNC

启用或禁用：虚拟网络计算服务（virtual network computing，VNC）。有关 VNC 的更多信息，请参阅 [VNC 文档](https://www.raspberrypi.com/documentation/computers/remote-access.html#vnc)。

```
$ sudo raspi-config nonint do_vnc <0/1>
```

* `0`：启用 VNC
* `1`：禁用 VNC

#### SPI

启用或禁用：SPI 接口，是否自动加载 SPI 内核模块。

```
$ sudo raspi-config nonint do_spi <0/1>
```

* `0`：启用 SPI
* `1`：禁用 SPI

#### I2C——I²C

启用或禁用：I²C 接口，是否自动加载 I²C 内核模块。

```
$ sudo raspi-config nonint do_i2c <0/1>
```

* `0`：启用 I²C
* `1`：禁用 I²C

#### Serial port——串口

启用或禁用：串口硬件。

```
$ sudo raspi-config nonint do_serial_hw <0/1/2>
```

* `0`：启用串口
* `1`：禁用串口

#### Serial console——串口控制台

启用或禁用： shell 及内核信息的串口输出。

```
$ sudo raspi-config nonint do_serial_cons <0/1/2>
```

* `0`：启用串口控制台
* `1`：禁用串口控制台

#### 1-wire——单总线

启用或禁用：Dallas 1-wire（单总线）接口，通常用于 DS18B20 温度传感器。

```
$ sudo raspi-config nonint do_onewire <0/1>
```

* `0`：启用 1-wire
* `1`：禁用 1-wire

#### Remote GPIO——GPIO 远程访问

启用或禁用：GPIO 引脚的远程访问。

```
$ sudo raspi-config nonint do_rgpio <0/1>
```

* `0`：启用 GPIO 远程访问
* `1`：禁用 GPIO 远程访问

### Performance options——性能选项

#### Overclock——超频

如果你的树莓派型号支持，就能对 CPU 超频。超频潜力因树莓派设备个体体质而异，即使是相同型号也会有所不同。超频过高可能会导致不稳定。


>**警告**
>
>**超频可能会缩短你树莓派的使用寿命。** 如因某个特定级别的超频造成系统不稳定，可尝试更为保守的超频。在启动过程中按住 **Shift** 键可暂时禁用超频。

```
$ sudo raspi-config nonint do_overclock <设置>
```

此命令接受以下 `<设置>` 值：

* `None`：不超频（默认）
* `Modest`：超频至最大值 50%
* `Medium`：超频至最大值 75%
* `High`：超频至最大值 100%
* `Turbo`：超频至最大值 125%

#### GPU memory——GPU 显存

修改向 GPU 提供的内存量。

```
$ sudo raspi-config nonint do_memory_split <megabytes>
```

#### Overlay file system——堆叠文件系统（OverlayFS）

启用或禁用：只读文件系统。

```
$ sudo raspi-config nonint do_overlayfs <0/1>
```

* `0`：启用堆叠文件系统（OverlayFS）
* `1`：禁用堆叠文件系统（OverlayFS）

#### Fan——风扇

可自定义接入 GPIO 的风扇行为（[树莓派 4 外壳](https://www.raspberrypi.com/products/raspberry-pi-4-case-fan/)自带）。对[树莓派 5 外壳自带风扇](https://www.raspberrypi.com/products/raspberry-pi-5-case/)、[树莓派 5 主动散热器](https://www.raspberrypi.com/products/active-cooler/)（使用特殊四针风扇头连接）无效。

```
$ sudo raspi-config nonint do_fan <0/1> [gpio] [onTemp]
```

* `0`：启用风扇
* `1`：禁用风扇

默认 `gpio` 为 14。

`onTemp` 默认为 80 °C。

### Localisation options——本地化选项

#### Locale——语言环境

选择语言环境，如 `zh_CN.UTF-8 UTF-8`（中文）或 `en_GB.UTF-8 UTF-8`（英语）。

```
$ sudo raspi-config nonint do_change_locale <语言环境>
```

要查看参数 `<语言环境>` 的所有可用值列表，请参阅交互版 `raspi-config` 中所使用的缩写。

#### Time zone——时区

设置你的本地时区，从地区开始，然后选择城市，如"Asia/Shanghai"。

```
$ sudo raspi-config nonint do_change_timezone <时区>
```

要查看参数 `<时区>` 的所有缩写值列表，请参见交互版 `raspi-config`。

#### Keyboard——键盘

设置键盘布局。一般来说，修改会立即生效，但也可能需重启才能生效。

```
$ sudo raspi-config nonint do_configure_keyboard <键盘布局>
```

要查看该参数 `<键盘布局>` 的所有可用值列表，请参阅交互版 `raspi-config` 中所使用的缩写。

#### WLAN country——无线局域网区域

设置无线网络的区域码。

```
$ sudo raspi-config nonint do_wifi_country <区域>
```

要查看此参数 `<区域>` 的所有可用值列表，请参阅交互版 `raspi-config` 中所使用的缩写。

### Advanced options——高级选项

#### Expand filesystem——扩展文件系统

将你的操作系统分区进行扩展，以利用整个存储设备，能为你带来更大的文件存储空间。需要需重启你的树莓派才能完成该。通常，树莓派系统会在首次开机时执行此操作。如果你将你的操作系统克隆到了容量大于旧设备的其他存储设备上，该功能可能会极其有用。

>**警告**
>
>没有再确认的步骤。选择该选项将立即执行分区扩展操作。

```
$ sudo raspi-config nonint do_expand_rootfs
```

#### Network interface names——网络接口名称

启用或禁用：可预测的网络接口名称。

```
$ sudo raspi-config nonint do_net_names <0/1>
```

* `0`：启用可预测的网络接口名称
* `1`：禁用可预测的网络接口名称

#### Network proxy settings——设置网络代理

配置网络代理。


```
$ sudo raspi-config nonint do_proxy <SCHEMES> <ADDRESS>
```

#### Boot order——启动顺序

在树莓派 4 及后续新款设备上，在未插入 SD 卡的情况下，指定：是否从 USB、网络进行启动。有关更多信息，请参阅[引导加载程序配置](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#raspberry-pi-bootloader-configuration)。


```
$ sudo raspi-config nonint do_boot_order <B1/B2/B3>
```

视你的设备而定，你可以在以下选项中进行选择：

* B1 ：SD 卡启动 - 如果 SD 卡可用，则优先从 SD 卡启动；如 SD 卡不可用，再从 NVMe 启动；如果 SD 卡、NVMe 均不可用，那么从 USB 启动
* B2 ：NVMe/USB 启动 - 如果 NVMe 可用，则优先从 NVMe 启动；如果 NVMe 不可用，再从 USB 启动；如果 NVMe、USB 均不可用，那么从 SD 卡启动
* B3 ：网络启动 - **如果 SD 卡可用**，则优先从 SD 卡启动；如果 SD 卡不可用，则从网络启动

#### Bootloader version——引导加载程序版本

在树莓派 4 及后续新款设备上，更新到最新版的 ROM 引导软件。或者，倘若最新版本引发了故障，你也可以在此恢复出厂默认设置。

```
$ sudo raspi-config nonint do_boot_rom <E1/E2>
```

* `E1`：使用最新的引导 ROM
* `E2`：使用出厂默认设置

#### Wayland

在 X11 后端和 Wayland 后端间进行切换。在树莓派 4 及后续新款设备上，默认使用 Wayland。其他型号的树莓派默认使用 X11。

```
$ sudo raspi-config nonint do_wayland <W1/W2>
```

* `W1`：使用 X11 后端
* `W2`：使用 Wayland 后端

>**注意**
>
>要在树莓派 4 先前的型号上使用 Wayland，你还必须把 `wayland=on` 添加到 `/boot/firmware/cmdline.txt`。

#### Audio config——音频配置

使用此参数在 PulseAudio 和 PipeWire 音频后端间进行切换。在树莓派系统 Bookworm 之前，树莓派系统使用 PulseAudio。

```
$ sudo raspi-config nonint do_audioconf <1/2>
```

* `1`：使用 PulseAudio 后端
* `2`：使用 PipeWire 后端

### Update——更新

将 `raspi-config` 更新至最新版本。

```
$ sudo raspi-config nonint do_update
```

## 显示

要配置你的树莓派，使用非默认显示模式，请手动设置分辨率和方向。

### HDMI 显示器支持

对于大部分 HDMI 显示器来说，树莓派系统都能使其达到最高分辨率和刷新率。

树莓派 Zero、Zero W 和 Zero 2 W 搭载了 mini HDMI 接口，因此你需要 mini HDMI 转全尺寸 HDMI 转接线（转接头）。

树莓派 4、5 和 400 搭载了两个 micro HDMI，因此你需要为每台你想使用的显示器，都各准备一份 micro HDMI 转标准 HDMI 转接线（转接头）。请在树莓派开机之前接入上述适配器。

树莓派 4 和 400 可以同时输出两个显示器，高达 1080p 分辨率、60Hz 刷新率；或输出两个 4K 30Hz 刷新率的显示器。如果你把显示器接入了 `HDMI0` 口，并在 [`/boot/firmware/config.txt`](https://www.raspberrypi.com/documentation/computers/config_txt.html#what-is-config-txt) 设置了参数 `hdmi_enable_4kp60=1`，还可以用 60Hz 刷新率输出单个 4K 显示器。

树莓派 5 无需任何额外配置，就可以 4K 分辨率、60Hz 刷新率，输出两个显示器。

### 设置分辨率和方向

#### 在桌面设置

在树莓派桌面上，打开菜单“**首选项（Preferences）**”，然后选择工具“**屏幕配置（Screen Configuration）**”。你应该会看到当前树莓派已接入的显示器（以图画代表）。右键单击要修改的显示器，然后选择一个选项。单击“**应用（Apply）**”并退出“**屏幕配置（Screen Configuration）**”以保存修改。

#### 在命令行设置

使用以下命令能打开 **屏幕配置（Screen Configuration）** 工具：

```
$ arandr
```

你应该会看到当前树莓派已接入的显示器（以图画代表）。右键单击要修改的显示器，然后选择一个选项。单击“**应用(Apply)**”并退出 **屏幕配置（Screen Configuration）** 以保存修改。

### 手动设置分辨率和屏幕方向

#### 确定显示设备名称

要手动配置分辨率和方向，你得知道显示设备的名称。要确定设备名称，请运行以下命令，来显示已接入设备的信息：

```
$ kmsprint | grep Connector
```

#### 设置自定义分辨率

如果你正在使用 Wayland 桌面混成器，你可以通过编辑你主目录中的文件来，设置自定义显示分辨率：`.config/wayfire.ini`。可编辑现有的 `[output:<device>]` 部分。倘若没有，则添加一个新部分 `[output:<device>]`，以适配你的显示设备。要修改显示分辨率，请添加 `mode` 这行。例如，对于以下示例，配置为：设备名称是 `HDMI-A-1`、分辨率是 1080p 60Hz：

```
[output:HDMI-A-1]
mode = 1920x1080@60
```

有关可支持的分辨率和 `mode` 语法的信息，请参阅 [Wayfire 文档](https://github.com/WayfireWM/wayfire-wiki/blob/master/Configuration.md#output-configuration)。

将相同的配置段落添加到 `/usr/share/greeter.ini`，可以配置登录屏幕分辨率。

#### 设置自定义屏幕方向

如果你正在运行 Wayland 桌面混成器，可以通过设置 `wlr-randr` 自定义屏幕显示方向。以下命令分别将屏幕方向配置为 0°、90°、180° 和 270°：

```
$ wlr-randr --output HDMI-A-1 --transform normal
$ wlr-randr --output HDMI-A-1 --transform 90
$ wlr-randr --output HDMI-A-1 --transform 180
$ wlr-randr --output HDMI-A-1 --transform 270
```

参数 `--output` 可指定要修改屏幕方向的设备。

>**注意**
>
>如要通过 SSH 运行此命令，请添加如下前缀： `WAYLAND_DISPLAY=wayland-1`。比如 `WAYLAND_DISPLAY=wayland-1 wlr-randr --output HDMI-A-1 --transform 90`。


你还可以使用以下某 `--transform` 参数，来同时镜像屏幕并修改其显示方向：`flipped`、`flipped-90`、`flipped-180`、`flipped-270`。

或者，你还可以通过编辑你主目录（home）中的文件，来旋转屏幕方向：`.config/wayfire.ini`。请编辑现有的 `[output:<device>]` 部分。倘若没有，则添加一个新的 `[output:<device>]` 部分以适配你的[显示设备](https://www.raspberrypi.com/documentation/computers/configuration.html#determine-display-device-name)。要旋转屏幕方向，需添加 `transform` 这一行。如，以下示例配置：设备名称是 `HDMI-A-1`、分辨率是 1080p 60Hz，旋转角度是 270°：


```
[output:HDMI-A-1]
mode = 1920x1080@60
transform = 270
```

Wayland 支持以下 `transform` 参数：

* `normal`
* `90`
* `180`
* `270`

将相同的配置内容添加到 `/usr/share/greeter.ini`，来改变登录界面的屏幕方向。

### Console resolution and rotation——控制台分辨率和屏幕旋转方向

要修改树莓派控制台模式下的分辨率和方向，请使用 KMS 设置。有关更多信息，请参阅[配置内核命令行](https://www.raspberrypi.com/documentation/computers/configuration.html#kernel-command-line-cmdline-txt)。

>**注意**
>
>
>如控制台模式同时输出至多个显示器，所有接入的显示器将使用相同的屏幕方向。

## Audio——音频

树莓派系统支持多种音频输出模式：HDMI 1、耳机插孔（如果你的设备有）和 USB 音频。

在默认情况下，树莓派系统将音频输出到 HDMI 1。如果 HDMI 输出不可用，树莓派系统会将音频输出到耳机插孔、已接入的 USB 音频设备。

### 修改音频输出

本节介绍了在树莓派系统中，多种配置音频输出的方法。

#### 通过桌面音量控制

单击系统托盘上的音量图标，打开音频输出选择器。该界面可让你选择音频输出设备。单击音频输出设备，能切换音频输出到该设备。

##### 专业音频配置文件

在 **音频输出选择器（audio output selector）** 中查看音频设备时，你也许会看到一个名为专业音频的设备配置文件。该配置文件在每个音频设备上公开了最大数量的通道，使你能够更好地控制信号的路由。除非你要对音频输出进行细粒度调整控制，否则请使用其他设备配置文件。

更多有关专业音频配置文件的内容，请访问 [PipeWire 常见问题解答](https://gitlab.freedesktop.org/pipewire/pipewire/-/wikis/FAQ#what-is-the-pro-audio-profile)。

#### 使用 raspi-config

要修改音频输出，请使用 [`raspi-config`](https://www.raspberrypi.com/documentation/computers/configuration.html#raspi-config)，运行以下命令：

```
$ sudo raspi-config
```

你将看到配置界面。完成以下步骤，可修改你的音频输出：

1. 选择 `System options` 并按  **回车键**。
2. 选择 `Audio options` 并按  **回车键**。
3. 选择所需模式，然后按 **回车键** 选择该模式。
4. 按 **右、方向键** 退出选项列表。选择 `Finish` 退出配置工具。

## 网络

可以用图形化用户界面（GUI）对树莓派系统上的无线连接进行配置。精简版树莓派系统和无头机器的用户可以用 [nmcli](https://networkmanager.dev/docs/api/latest/nmcli.html)，在命令行设置无线网络连接。

>**注意**
>
>自树莓派系统 *Bookworm* 以降，默认的网络配置工具变成了 Network Manager。旧版的树莓派系统使用 dhcpd 和其他工具进行网络配置。

### 连接到无线网络

#### 通过桌面

通过菜单栏右端的网络图标打开网络管理器。如果你使用的树莓派搭载了内置无线连接功能（或插入了无线适配器），则单击此图标即可显示可用无线网络列表。如果看到信息“未找到 AP——正在扫描……（No APs found - scanning…​）”，请等待几秒，网络管理器应该就能搜到你的网络。

>**注意**
>
>搭载双频无线的树莓派设备（树莓派 3B+、4、计算模块 4、树莓派 400、5）会自动禁用网络，直到你分配无线局域网区域。要设置无线局域网区域，请在“首选项”菜单里打开树莓派配置应用程序，选择 **本地化（Localisation）**，然后从菜单中选择你的区域。

![WiFi](../.gitbook/assets/wifi2.png)

右侧的图标会提示网络是否加密，并指示其信号强度。单击要连接的网络。如果是加密网络，对话框将让你输入网络密钥：

![密码](../.gitbook/assets/key.png)

输入密钥，然后单击“**确定（OK）**”，再等待几秒钟。网络图标会闪烁一下，表示正在建立连接。连接成功后，图标将停止闪烁并显示信号强度。

##### 连接到隐藏的网络

要使用隐藏的网络，请在网络菜单中导航到 **高级选项（Advanced options）** > **连接到隐藏的 WiFi 网络（Connect to a hidden Wi-Fi network）**：

![高级选项中连接到隐藏的网络](../.gitbook/assets/network-hidden.png)

然后，输入隐藏网络的网络名称（SSID）。询问你的网络管理员：你所用的网络使用哪种加密方式。目前，大多数家用网络使用的是 WPA 和 WPA2 个人加密，公共网络有时使用 WPA 和 WPA2 企业加密。选择你网络的加密方式，并输入你的凭据：

![隐藏的 WiFi 网络认证](../.gitbook/assets/network-hidden-authentication.png)

单击按钮“**连接（Connect）**”可启动网络连接。

#### 通过命令行

本指南将帮助你：在不使用图形化工具（且无需额外软件）的情况下，在树莓派上配置使用无线连接。

>**注意**
>
>本指南适用于 WEP、WPA、WPA2 和 WPA3 网络，但可能不适用于企业网络。

##### 启用无线网络

在全新安装时，你必须指定你设备的使用位置。这样可以使你的设备选择正确的 5GHz 网络频段。在你指定无线局域网区域后，你就可以使用树莓派内置的无线网络模块了。

要做到这一点，请使用命令行工具 `raspi-config`，设置你的无线局域网区域。运行以下命令：

```
$ sudo raspi-config
```

使用方向键选择菜单项“**本地化选项（Localisation options）**”。选择选项 **WLAN 区域（WLAN country）**。使用 **方向键** 从下拉菜单中选择你的区域。按 **回车键** 确认选择。

现在，你应该已经可以访问无线网络了。运行以下命令来检查你的 WiFi 无线电是否已启用：

```
$ nmcli radio wifi
```

如果此命令返回文本“enabled（已启用）”，则可以继续准备配置连接。如果此命令返回“disabled（已禁用）”，请尝试使用以下命令启用 WiFi：

```
$ nmcli radio wifi on
```

##### 搜索网络

要扫描无线网络，请运行以下命令：

```
$ nmcli dev wifi list
```

你应看到类似输出如下：

```
IN-USE  BSSID              SSID            MODE   CHAN  RATE        SIGNAL  BARS  SECURITY
        90:72:40:1B:42:05  myNetwork       Infra  132   405 Mbit/s  89      ****  WPA2
        90:72:42:1B:78:04  myNetwork5G     Infra  11    195 Mbit/s  79      ***   WPA2
        9C:AB:F8:88:EB:0D  Pi Towers       Infra  1     260 Mbit/s  75      ***   WPA2 802.1X
        B4:2A:0E:64:BD:BE  Example         Infra  6     195 Mbit/s  37      **    WPA1 WPA2
```

在“SSID”这一列下，查找要连接的网络名称。使用网络名称（SSID）和密码连接到网络。

##### 连接到网络

运行以下命令来配置网络连接，将占位符 `<网络名称>` 替换为你要配置的网络名称：

```
$ sudo nmcli --ask dev wifi connect <网络名称>
```

在有提示时输入你的网络密码。

在你输入密码后，你的树莓派应该会自动接入网络。

如果你看到错误输出，提示你“需要密码，但未提供密码”，则意味着你输入的密码错误。请再次运行上述命令，仔细检查你输入的密码。

要检查是否已接入网络，请运行以下命令：

```
$ nmcli dev wifi list
```

应该看到类似输出如下：

```
IN-USE  BSSID              SSID            MODE   CHAN  RATE        SIGNAL  BARS  SECURITY
*       90:72:40:1B:42:05  myNetwork       Infra  132   405 Mbit/s  89      ****  WPA2
        90:72:42:1B:78:04  myNetwork5G     Infra  11    195 Mbit/s  79      ***   WPA2
        9C:AB:F8:88:EB:0D  Pi Towers       Infra  1     260 Mbit/s  75      ***   WPA2 802.1X
        B4:2A:0E:64:BD:BE  Example         Infra  6     195 Mbit/s  37      **    WPA1 WPA2
```

在“IN-USE”列中查找星号(`*`)；它应该出现在你打算接入网络的网络名称（SSID）所在的同一行。

>**注意**
>
>你可以手动编辑你的连接，配置文件位于目录 `/etc/NetworkManager/system-connections/` 下。

##### 连接到未加密的网络

如果你要连接的网络未使用密码，请运行以下命令：

```
$ sudo nmcli dev wifi connect <网络名称>
```

>**警告**
>
>未加密的无线网络可能会将你的个人信息暴露在风险之中。应尽可能请使用安全的无线网络（或 VPN）。

##### 连接到隐藏的网络

如果你正在使用着隐藏的网络，请在运行 `nmcli` 时指定参数 “hidden”，并赋值为“yes”。

```
$ sudo nmcli --ask dev wifi connect <网络名称> hidden yes
```

##### 设置网络优先级

如果你的设备同时检测到了多个已知网络，它可能会随机接入到任意某个被检测到的已知网络。可使用优先级参数，强制让你的树莓派优先连接到某些网络。在范围内，你的设备将连接到具有最高优先级的网络。运行以下命令，查看已知网络的优先级：

```
$ nmcli --fields autoconnect-priority,name connection
```

你应该看到类似输出如下：

```
AUTOCONNECT-PRIORITY  NAME
0                     myNetwork
0                     lo
0                     Pi Towers
0                     Example
-999                  Wired connection 1
```

使用命令 `nmcli connection modify` 可设置网络的优先级。以下示例命令：把叫做 "Pi Towers" 的网络的优先级设置为 `10`：

```
$ nmcli connection modify "Pi Towers" connection.autoconnect-priority 10
```

在范围内，你的设备将始终尝试连接到具有最高非负优先级值的网络。你还可以为网络分配负优先级；只有在范围内，没有其他已知网络时，你的设备才会尝试连接到负优先级网络。例如，现在有三个网络：

```
AUTOCONNECT-PRIORITY  NAME
-1                    snake
0                     rabbit
1                     cat
1000                  dog
```

* 在范围内，如果所有这些网络都存在，你的设备将首先尝试连接到网络“dog”。
* 如果网络“dog”连接失败，你的设备将尝试连接到网络“cat”。
* 如果网络“cat”连接失败，你的设备将尝试连接到网络“rabbit”。
* 如果网络“rabbit”连接失败，并且你的设备未检测到其他已知网络，你的设备将尝试连接到网络“snake”。

### 配置 DHCP

在默认情况下，树莓派系统会尝试用 DHCP 自动配置所有网络接口。如果 DHCP 失败，则回滚至自动私有地址，范围是 `169.254.0.0/16`。

### 分配静态 IP 地址

如果要给你的树莓派分配静态 IP 地址，请在路由器上为其设置一个保留地址。你的树莓派仍将通过 DHCP 分配其地址，但每次都会收到相同的地址。可以在 DHCP 服务器中，将树莓派的 MAC 地址绑定到静态 IP 地址，来实现“静态”地址的分配。

## Screen Blanking 屏幕节能（无操作时关闭屏幕）

你可以配置你的树莓派使用 **屏幕节能（Screen Blanking）**：在一段时间内无操作后，把屏幕关闭。在默认情况下，在启用屏幕节能后，树莓派系统将在无操作十分钟后关闭屏幕。

### 桌面

你可以使用树莓派配置菜单中的屏幕节能选项来控制屏幕节能（无操作时关闭屏幕）。

#### 配置树莓派

单击菜单栏中的树莓派按钮。导航到 **首选项（Preferences）** > **树莓派配置（Raspberry Pi Configuration）**。

![从桌面打开菜单“树莓派配置”](https://www.raspberrypi.com/documentation/computers/images/pi-configuration.png)

选择选项卡显示（**Display**）。将选项按钮切换到屏幕节能（**Screen Blanking**）。按下 **完成（OK）**，确认你的选择。

![toggle Screen Blanking on in the Raspberry Pi Configuration menu](https://www.raspberrypi.com/documentation/computers/images/blanking.png)

#### 命令行

你可以使用命令行工具 `raspi-config`，来启用和禁用屏幕节能。运行以下命令打开该工具：

```
$ sudo raspi-config
```

使用 **方向键** 导航，使用 **回车键** 选择。选择 `Display Options` > 。使用  **方向键**：选择 `yes` 启用屏幕节能；选择 `no` 禁用屏幕节能。

你还可以编辑添加以下行到 `~/.config/wayfire.ini`：

```
[idle]
dpms_timeout=600
```

变量 `dpms_timeout` 控制了在树莓派系统在屏幕关闭之前所需的无操作秒数。如，值若为 `600`，则意味着会在 600 秒（十分钟）后关闭屏幕。将值置 `0`，屏幕将永不熄灭。

### 控制台

树莓派配置使用的屏幕节能配置 `dpms_timeout` 仅涉及桌面会话。在 **控制台模式** 下，即当你的树莓派仅接入至带有终端输入的监控器和键盘时，请在内核命令行下，使用设置 `consoleblank`。

#### 设置控制台模式下的屏幕节能（screen blanking）

要修改控制台模式下的屏幕节能配置，请以管理员身份，在文本编辑器中打开 `/boot/firmware/cmdline.txt`：

```
$ sudo nano /boot/firmware/cmdline.txt
```

你可以在这儿调整树莓派系统，在关闭屏幕之前，所等待控制台的秒数。例如，添加 `consoleblank=600` 可在其无操作 600 秒后关闭显示信号输出。将值置 `0`，屏幕将永不熄灭。

修改 `cmdline.txt` 后，只有在重启后才会生效。使用以下命令重启你的树莓派：

```
$ sudo reboot
```

#### 查看当前屏幕节能设置

你可以使用以下命令，显示当前控制台屏幕关闭时间（以秒为单位）：

```
$ cat /sys/module/kernel/parameters/consoleblank
```

## 用户

### 修改用户密码

你可以用工具 `raspi-config`，在命令行来修改当前用户账户的密码：

```
$ sudo raspi-config
```

选择 option 2，并按照说明修改密码。

或者，使用工具 `passwd`：

```
$ passwd
```

### 添加用户

要添加新用户，请输入以下命令：把占位符 `<用户名>` 换成新用户的用户名：

```
$ sudo adduser <用户名>
```

在出现提示时，为新用户输入密码。

新用户的主目录位于 `/home/<用户名>/`。

为了授予新用户必要的权限，比如 `sudo`，运行以下命令将该用户添加到相关用户组，请把占位符 `<用户名>` 换成新用户的用户名：

```
$ sudo usermod -a -G adm,dialout,cdrom,sudo,audio,video,plugdev,games,users,input,netdev,gpio,i2c,spi <用户名>
```

要检查权限是否成功授予，请运行以下命令，请将占位符 `<用户名>` 换成新用户的用户名：

```
$ sudo su - <用户名>
```

如果上述命令成功运行，则已成功为该用户配置了权限。

### 删除用户

要删除用户，请运行以下命令，请将占位符 `<用户名>` 换成要删除的用户名：

```
$ sudo deluser -remove-home <用户名>
```

此命令将删除用户及其主目录。如果你想保留该用户的主目录，请在执行命令时，把参数 `-remove-home` 去掉。

### 修改默认用户

要修改在启动时自动登录到你树莓派的用户，请运行以下命令：

```
$ sudo raspi-config
```

选择 option `1`, `Boot/Auto login`。重启以使修改生效。

## 外部存储

你可以将外置硬盘、固态硬盘和 USB 闪存接入树莓派上的任意 USB 口，然后挂载文件系统，访问里面存储的数据。

在默认情况下，对于常见的文件系统（FAT、NTFS 和 HFS+），你的树莓派会自动挂载，挂载位置在 `/media/pi/<HARD-DRIVE-LABEL>`。

>**注意**
>
>精简版树莓派系统没有实现自动挂载这个功能。

要设置存储设备，必须手动挂载，使其挂载到你选择的特定位置。

### 挂载存储设备

你可以将存储设备挂载到特定文件夹位置。通常挂载到文件夹 `/mnt` 下，例如 `/mnt/mydisk`。请注意，文件夹必须为空。

将存储设备插入树莓派上的 USB 口，并使用以下命令列出树莓派上的所有磁盘分区：

```
$ sudo lsblk -o UUID,NAME,FSTYPE,SIZE,MOUNTPOINT,LABEL,MODEL
```

树莓派自身使用挂载点 `/` 和 `/boot/firmware/`。你的存储设备将显示在此列表中，以及所有其他已接入的存储设备。

使用 SIZE、LABEL 和 MODEL 这几列来辨别指向存储设备的磁盘分区的名称（如 `sda1`）。FSTYPE 这列包含了文件系统类型。如果你的存储设备使用的是 exFAT 文件系统，请安装 exFAT 驱动程序：

```
$ sudo apt update
$ sudo apt install exfat-fuse
```

如果你的存储设备使用 NTFS 文件系统，你将只能以只读方式使用它。如果你想要对设备进行写操作，可以安装驱动程序 ntfs-3g：

```
$ sudo apt update
$ sudo apt install ntfs-3g
```

运行以下命令以获取磁盘分区的位置：

```
$ sudo blkid
```

比如，`/dev/sda1`。

创建一个目标文件夹，用作存储设备的挂载点。在这种情况下，使用的挂载点名称是 `mydisk`。你可以指定成自己想要的名称：

```
$ sudo mkdir /mnt/mydisk
```

将存储设备挂载到你创建的挂载点上：

```
$ sudo mount /dev/sda1 /mnt/mydisk
```

要检查存储设备是否挂载成功，可通过列出内容来确认：

```
$ ls /mnt/mydisk
```

### 自动挂载存储设备

你可以修改 `fstab` 文件，定义树莓派在启动时，存储设备自动挂载的位置。在 `fstab` 文件中，磁盘分区由通用唯一标识符（UUID）标识。

获取磁盘分区的 UUID：

```
$ sudo blkid
```

从列表中找到磁盘分区并记录 UUID。（如 `5C24-1453`）使用诸如 nano 之类的命令行编辑器打开 fstab 文件：

```
$ sudo nano /etc/fstab
```

在 `fstab` 文件中添加以下几行：

```
UUID=5C24-1453 /mnt/mydisk fstype defaults,auto,users,rw,nofail 0 0
```

用你在上述步骤中找到的文件系统类型（如 `ntfs`）替换 `fstyp`。

如果文件系统类型为 FAT 和 NTFS，请在紧跟 `nofail` 之后，添加 `,umask=000` - 这将让所有用户完全读写存储设备上的任意文件。

现在你已在 `fstab` 中设置了一个条目。在启动树莓派时，该存储设备是否接入均可开机。在拔下存储设备之前，你必须先将树莓派关机，或者手动卸载该存储设备。

>**注意**
>
>如果在树莓派启动时，未接入存储设备，启动时将再多等 90 秒。你可以通过在紧跟 `nofail` 之后，添加 `,x-systemd.device-timeout=30` 来缩短时间。这将把超时时间修改为 30 秒，这意味着系统只会等待 30 秒，然后放弃挂载磁盘。


要获取有关每个 Linux 命令的更多信息，请使用 `man` 命令查阅特定的手册页。例如，`man fstab`。

### 卸载存储设备

当树莓派关机时，系统会负责卸载存储设备，以便安全拔出。如果你想手动卸载设备，可以使用以下命令：

```
$ sudo umount /mnt/mydisk
```

如果收到报错“device is busy”，这意味着存储设备未被卸载。如果没有显示错误，现在可以安全地拔出设备。

#### 解决“device is busy”

信息“device is busy”意味在着存储设备上，有被程序占用的文件。要关闭这些文件，请执行以下步骤。

关闭任何打开了存储设备上的文件的软件。如果你打开了一个终端，请确保你未处于存储设备所挂载的文件夹（及其子文件夹）下。

如果你仍然无法卸载存储设备，你可以使用工具 lsof 检查是哪个程序在设备上打开了文件。首先你要用 apt 安装 lsof：

```
$ sudo apt update
$ sudo apt install lsof
```

 使用 lsof 命令：

```
$ lsof /mnt/mydisk
```

## 内核命令行（ cmdline.txt ）

Linux 内核在启动时可接受一组命令行参数。在树莓派上，这个命令行定义在引导分区中的一个文件中，名为 `cmdline.txt`。你可以使用任意文本编辑器编辑该文本文件。

```
$ sudo nano /boot/firmware/cmdline.txt
```

>**重要**
>
>请把所有参数放在 `cmdline.txt` 中的一行里。**不要** 用换行符。


要查看在启动时传递给内核的命令行，请运行以下命令：

```
$ cat /proc/cmdline
```

因为树莓派固件会在启动内核之前对命令行进行修改，所以此命令行的输出不会与 `cmdline.txt` 的内容完全吻合。

### 命令行参数

有许多内核命令行参数，其中某些由内核本身定义。其他的可能由内核正在使用的代码定义，如 Plymouth 闪屏系统。

#### 标准条目

`console`

　　定义了串口控制台。通常有两个条目：

* `console=serial0,115200`
* `console=tty1`

`root` 

　　定义了根文件系统的位置。例如，`root=/dev/mmcblk0p2` 表示多媒体卡区块 0 分区 2。

`rootfstype`

　　定义了根文件系统使用的文件系统类型，例如 `rootfstype=ext4`。

`quiet` 

　　将默认内核日志级别设置为 `KERN_WARNING`，在启动过程中屏蔽任何不是非常严重级别的内核信息。

#### 设置 KMS 显示模式

早期版本的树莓派系统中使用的传统固件和 FKMS 显示模式，已不再支持。作为代替，最新版本的操作系统使用 KMS（内核模式设置）。

如果在 `cmdline.txt` 中没有 `video` 这个条目，树莓派操作系统将根据 HDMI 接入显示器的 [EDID](https://en.wikipedia.org/wiki/Extended_Display_Identification_Data)，自动选择（基于 Linux 内核信息）显示器支持最佳分辨率。在精简版树莓派系统、控制台模式中，你必须自己手动修改 `video` 这个条目，才能修改分辨率和屏幕方向。

```
video=HDMI-A-1:1920x1080M@60
```

另外，可以添加旋转和翻转（屏幕镜像）参数，请参考标准 [Linux 帧缓冲文档](https://github.com/raspberrypi/linux/blob/rpi-6.1.y/Documentation/fb/modedb.rst)。以下示例定义了一台显示器：名为 `HDMI-A-`、分辨率为 1080p、刷新率为 60Hz、屏幕旋转 90 度、并在 X 轴上翻转屏幕（屏幕镜像）：

```
video=HDMI-A-1:1920x1080M@60,rotate=90,reflect_x
```

在指定屏幕旋转和翻转参数时，必须明确指定分辨率。

显示类型的支持选项——`video=` 条目的开头部分，包括：

| 视频选项 | 显示                                                                   |
| :----------: | :------------------------------------------------------------------------: |
| `HDMI-A-1`         | HDMI 1（树莓派 4B 主板上标为 HDMI 0、单个 HDMI 主板上标为 HDMI） |
| `HDMI-A-2`         | HDMI 2（树莓派 4B 主板上标为 HDMI 1）                          |
| `DSI-1`         | DSI 或 DPI                                                             |
| `Composite-1`         | 复合                                                                   |

#### 其他条目

此部分是可以在内核命令行中使用的其他条目。此列表不是完整无遗的。

`splash`

  启动时使用 Plymouth 模块显示启动画面。

`plymouth.ignore-serial-consoles` 

  通常如启用 Plymouth 模块，它会屏蔽掉所有串口控制台上出现的启动信息。此参数能让 Plymouth 忽略所有串口控制台，使启动消息再次重现，就像没有运行 Plymouth 一样。

`dwc_otg.lpm_enable=0` 

  关闭链接状态电源管理（Link Power Management，LPM）在 `dwc_otg` 驱动程序中的设置。该驱动程序驱动着 USB 控制器（嵌入在树莓派计算机的处理器中）。在树莓派 4 上，默认已禁用此控制器，且它仅连接至 USB Type C 电源输入接口。树莓派 4 上的 USB-A 接口由另外的，与此设置无关的 USB 控制器驱动。

`dwc_otg.speed` 

  可设置树莓派计算机 USB 控制器的速率（内置于处理器）。将其设置 `dwc_otg.speed=1` 则为全速（USB 1.0），低于高速（USB 2.0）。除非要解决 USB 设备问题，否则不应设置此参数。

`smsc95xx.turbo_mode` 

  启用或禁用：有线网络驱动程序 Turbo 模式。`smsc95xx.turbo_mode=N` 则关闭 Turbo 模式。

`usbhid.mousepoll` 

  指定鼠标轮询间隔。如果你遇到了无线鼠标移动缓慢、不稳定的问题，将其置 `0` 也许有用。

`drm.edid_firmware=HDMI-A-1:edid/your_edid.bin`

  使用它能覆盖你显示器内置的 EDID 信息。

## 本地化你的树莓派

你可以使用工具 [`raspi-config`](https://www.raspberrypi.com/documentation/computers/configuration.html#raspi-config) 配置树莓派系统的界面语言、键盘布局和时区。

## 保护你的树莓派

在这儿，我们介绍了一些常见方法，能提高你树莓派的安全性。

### 设置 sudo 命令要求密码

使用前缀 `sudo` 运行命令，会将其以超级用户执行。在默认情况下，不需要密码。但是你可以要求，所有以 `sudo` 运行的命令均需输入密码，来使你的树莓派更安全。

要强制 `sudo` 需要密码，请编辑你用户账户的 `nopasswd` sudoers 文件，将文件名中的占位符 `<用户名>` 换成你的用户名：

```
$ sudo visudo /etc/sudoers.d/010_<用户名>-nopasswd
```

将条目 `<用户名>` 修改为如下内容，并把 `<用户名>` 换成你的用户名：

```
<用户名> ALL=(ALL) PASSWD: ALL
```

保存文件。你的新设置会立即生效。

### 更新树莓派系统

只有最新版本的操作系统包含了所有最新的安全补丁。请始终将你设备中的树莓派系统[更新](https://www.raspberrypi.com/documentation/computers/os.html#update-software)至最新版本。

### 自动更新你的 SSH 服务器

如果你通过 SSH 连接至树莓派，通过添加 `cron` 作业，专门更新 SSH 服务器可能是值得的。可把以下命令，作为每日 `cron` 作业运行，确保你能及时获得最新的 SSH 安全修复程序。它独立于你的正常更新流程。

```
$ apt install openssh-server
```

### 提高 SSH 安全性

远程访问树莓派的常用方式是 SSH。在默认情况下，SSH 需要用户名和密码。为了提高 SSH 的安全性，请[使用基于密钥的身份验证](https://www.raspberrypi.com/documentation/computers/remote-access.html#configure-ssh-without-a-password)。

#### 启用和禁用 SSH 用户

你还可以通过修改 sshd 配置，**允许（allow）** 和 **拒绝（deny）** 特定用户。

```
$ sudo nano /etc/ssh/sshd_config
```

将以下行添加、编辑或追加到文件末尾，其中包含了你希望允许登录的用户名：

```
AllowUsers alice bob
```

你还可以使用 `DenyUsers` 来明确禁止某些用户名的登录：

```
DenyUsers jane john
```

修改后，请使用以下命令重启 `sshd` 服务，以使修改生效：

```
$ sudo systemctl restart ssh
```

### 使用防火墙

Linux 上有许多防火墙解决方案可用。大多数通过底层的 [iptables](http://www.netfilter.org/projects/iptables/index.html) 项目来进行数据包过滤。该项目基于 Linux netfiltering 系统。在默认情况下，树莓派系统上预装了 `iptables`，但未设置。设置它可能是一件非常麻烦的事情。[Uncomplicated Firewall (UFW) ](https://www.linux.com/learn/introduction-uncomplicated-firewall-ufw)项目提供了比 `iptables` 更易用的界面。UFW 是 Ubuntu 中默认的防火墙工具，也可以安装到你的树莓派上：

```
$ sudo apt install ufw
```

`ufw` 是个命令行工具，然而也有图形界面可用。请注意，`ufw` 需以 root 权限运行，因此所有命令都以 `sudo` 开头。还可以使用参数 `--dry-run` 执行所有 `ufw` 命令，这表示仅输出命令的执行结果，而不进行任何实质性修改。

启用防火墙，同时也会让它开机自启：

```
$ sudo ufw enable
```

要禁用防火墙，同时禁用开机自启，请使用：

```
$ sudo ufw disable
```

允许特定端口访问（我们在示例中使用了 22 端口）：

```
$ sudo ufw allow 22
```

拒绝访问端口也非常简单（我们再次以 22 端口为例）：

```
$ sudo ufw deny 22
```

你还可以指定在端口上允许和拒绝哪种服务。在此示例中，我们拒绝了 22 端口上的 TCP：

```
$ sudo ufw deny 22/tcp
```

如果你不知道服务会使用哪个端口，那么可以指定服务。此示例允许 ssh 服务通过防火墙访问：

```
$ sudo ufw allow ssh
```

命令 status 可列出当前防火墙的所有设置：

```
$ sudo ufw status
```

规则可能相当复杂：允许阻止特定 IP 地址、指定允许流量的方向、限制连接尝试的次数（如有助于缓解 DDoS 攻击）。你还可以指定要应用规则的设备（如 eth0、wlan0）。请参阅 `ufw` 手册页（`man ufw`）以获取除下面命令之外的完整详细信息。

在 ssh 端口上（TCP）限制登录尝试。如果 IP 地址在过往 30 秒内有过六次及更多次连接尝试，则拒绝连接：

```
$ sudo ufw limit ssh/tcp
```

拒绝从 IP 地址 192.168.2.1 访问端口 30

```
$ sudo ufw deny from 192.168.2.1 port 30
```

### 使用 `fail2ban` 阻止可疑活动

在树莓派作为服务器时，你必须在防火墙中创建有意的漏洞以允许服务器流量通过。[Fail2ban](http://www.fail2ban.org/) 可以帮助保护你的服务器。Fail2ban 会检查日志文件中的检查可疑活动，如多次暴力登录尝试。它可以帮助你避免：手动检查入侵尝试的日志文件，然后再通过 `iptables` 更新防火墙来阻止它们。

运行以下命令安装 `fail2ban`：

```
$ sudo apt install fail2ban
```

安装后，Fail2ban 会创建 `/etc/fail2ban/jail.conf`。要启用 Fail2ban，请将 `jail.conf` 复制到 `jail.local`：

```
$ sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
```

在此配置文件中包含了一组默认选项，以及用于检查特定服务异常的选项。要查看用于 `ssh` 的规则，请用编辑器打开 `jail.local`：

```
$ sudo nano /etc/fail2ban/jail.local
```

如果不存在，则创建 `[ssh]` 部分，并向该部分添加以下数行：

```
[ssh]
enabled  = true
port     = ssh
filter   = sshd
backend  = systemd
maxretry = 6
```

这将启用对 ssh 可疑活动的 Fail2ban 检查，包括检查系统日志，并在阻止活动之前给予进行六次重试机会。

在同一文件中，此 `[default]` 部分定义了默认的封禁操作 iptables-multiport，当达到检测阈值时运行 `/etc/fail2ban/action.d/iptables-multiport.conf` 文件：

```
# Default banning action (e.g. iptables, iptables-new,
# iptables-multiport, shorewall, etc) It is used to define
# action_* variables. Can be overridden globally or per
# section within jail.local file
banaction = iptables-multiport
```

multiport（多端口）会禁止全部端口上的一切访问。`action.d` 文件夹包含许多可用于自定义服务器响应可疑活动的替代操作配置文件。

例如，如果要在三次失败尝试后永久拉黑 IP 地址，请将 `[ssh]` 部分中的 `maxretry` 值修改为 `3`，并将 `bantime` 设置为负数：

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

无头（**headless**）是指在没有显示器、键盘、鼠标的情况下运行树莓派。要运行无头树莓派，你需要一种在其他计算机上访问它的方法。要远程访问你的树莓派，你需要将树莓派接入网络，并找到一种使用该网络访问树莓派的方法。

要把树莓派连接到网络，你可以通过以太网，把设备进行有线连接，或者配置无线网络。

要通过该网络访问树莓派，请使用 SSH。通过 SSH 连接，你就可以使用 `raspi-config` 来[启用 VNC](https://www.raspberrypi.com/documentation/computers/remote-access.html#vnc)（如果你更喜欢图形化桌面环境）。

如果你从头开始设置你的树莓派，请在[启动盘制作过程中](https://www.raspberrypi.com/documentation/computers/getting-started.html#installing-the-operating-system)设置无线网络和 SSH。如果你已经设置好了树莓派，你可以使用 `raspi-config` 配置 SSH。

>**警告**
>
>取决于你使用的树莓派型号和 SD 卡型号，你的树莓派首次可能需要长达五分钟的时间来启动并接入无线网络。

### 连接到有线网络

首次启动时，若要连接到有线网络，请把你的树莓派接入以太网。如果说你的树莓派没有以太网接口，则需使用以太网转换器。你的树莓派将自动连接到网络。

### 连接到无线网络

要在无头树莓派首次启动时配置无线网络访问，请使用树莓派启动盘制作工具中的高级设置菜单。输入你首选无线网络的网络名称（SSID）和密码。你的树莓派在首次启动时，将用这些凭据接入网络。某些无线适配器和某些树莓派开发板并不支持 5GHz 网络；请查阅你的无线模块文档，以确保与你首选网络的兼容性。

>**注意**
>
>旧版的树莓派系统会使用一个叫 `wpa_supplicant.conf` 的文件，把该文件放入 boot 文件夹就可以配置无线网络设置。从树莓派系统 Bookworm 版本开始，该功能不再可用。



### 远程访问

如果没有键盘和显示器，你需要某种方法来[远程控制](https://www.raspberrypi.com/documentation/computers/remote-access.html)你的无头树莓派。在首次启动时，唯一的办法是 SSH。要在全新安装的树莓派系统上启用 SSH，请选择以下某种方法：

* 在树莓派启动盘制作工具的操作系统自定义菜单中启用 SSH，然后输入用户名和密码
* 在 SD 卡的根目录下创建一个名为 `ssh` 的文件，然后按照下面部分的说明手动配置用户 `userconf.txt`

欲了解更多信息，请参阅[设置 SSH 服务器](https://www.raspberrypi.com/documentation/computers/remote-access.html#ssh)。通过 SSH 连接，你就可以使用 `raspi-config` 来启[用 VNC](https://www.raspberrypi.com/documentation/computers/remote-access.html#vnc)，如果你更喜欢图形桌面环境。

#### 手动配置用户

在你 SD 卡的根目录下，创建一个名为 `userconf.txt` 的文件。

该文件需包含一行文本，由 `<用户明>:<密码>` 构成：你想要使用的用户名，紧接着是一个英文冒号，然后是你想要用的密码的 **加密** 形式。

>**注意**
>
>`<用户名>` 仅支持小写英语字母，数字和 `-`。且必须以字母开头。长度不大于 31 个字符。

要生成加密密码，请在其他计算机上使用 [OpenSSL](https://www.openssl.org/)。打开终端并输入以下内容：

```
$ openssl passwd -6
```

在有提示时输入密码并进行验证。然后，该命令将输出所提供密码的加密形式。

## 从你的树莓派发射无线网络

你的树莓派可以用无线模块发射自己的无线网络。如果你用以太网口（或其他的无线模块）把你的树莓派接入互联网，那么接入无线网络的其他设备就可以用你的树莓派来上网。

假如使用的有线网络 IP 段是 `10.x.x.x`。你可将你的树莓派连接到该网络，并在使用另一个 IP 段（如 `192.168.x.x`）的独立网络上，为无线客户端提供服务。

在以下拓扑中，请注意笔记本电脑与路由器和有线客户端的 IP 段是分离的：

![主网络](../.gitbook/assets/host-a-network.png)

在这种网络配置下，无线客户端可以通过树莓派路由器彼此通信。但是，无线网络上的客户端不能直接与有线网络上的客户端进行通信（除了树莓派）。无线客户端位于私有网络中，与为有线客户端提供服务的网络相分离。

>**注意**
>
>树莓派 5、4、3，Zero W、2 W 可使用内置无线模块托管无线网络。未搭载内置无线网卡的树莓派型号可以使用外置无线模块来实现此功能。

### 启用热点

要在命令行上创建托管的无线网络，请运行以下命令，把占位符 `<网络名称>` 和 `<密码>` 改成你自己的值：

```
$ sudo nmcli device wifi hotspot ssid <网络名称> password <密码>
```

使用其他的无线客户端（如笔记本电脑和智能手机）连接至网络。查找与网络名称（SSID）与 `<网络名称>` 一致的网络。输入你的网络密码，你应成功连接至网络。如果你的树莓派用以太网连接和另外的无线适配器接入互联网，你也应该能上网。

### 禁用热点

要禁用热点网络，并将你的树莓派还原成无线客户端，请运行以下命令：

```
$ sudo nmcli device disconnect wlan0
```

在禁用热点后，运行以下命令，可重新连接到其他 WiFi 网络：

```
$ sudo nmcli device up wlan0
```

>**技巧**
>
>有关连接到无线网络的更多信息，请参阅[配置网络](https://www.raspberrypi.com/documentation/computers/configuration.html#networking)。

### 将你的树莓派用作网桥

在默认情况下，从你的树莓派托管的无线网络与通过以太网连接的父网络分相分离。在这种拓扑下，连接到父网络的设备无法直接与树莓派托管的无线网络所接入的设备进行通信。如果你希望连接的无线设备能够与父网络上的设备通信，你可以将你的树莓派配置为[网桥](https://en.wikipedia.org/wiki/Network_bridge)。有了网桥，所有接入树莓派托管的无线网络的设备都会被分配一个父网络中的 IP 地址。

在以下拓扑中，笔记本电脑、路由器和有线客户端位于相同的 IP 段：

![桥接网络](../.gitbook/assets/bridge-network.png)

以下步骤记录了如何在你的树莓派上设置网桥，以实现无线客户端和父网络之间的通信。

首先，创建一个网桥接口：

```
$ sudo nmcli connection add type bridge con-name 'Bridge' ifname bridge0
```

接下来，把你设备的以太网连接添加到父网桥：

```
$ sudo nmcli connection add type ethernet slave-type bridge \
    con-name 'Ethernet' ifname eth0 master bridge0
```

最后，把你的无线热点连接添加到桥接中。你可以添加现有的热点接口，亦可创建新的：

* 如果你已经按照上述说明创建了无线热点连接，请使用以下命令将现有接口添加至桥接中：

  ```
  $ sudo nmcli connection modify 'Hotspot' master bridge0
  ```
* 如果你尚未创建无线热点连接，请使用单个命令（所有内容是一个命令）来创建新接口并将其添加到桥接中，把占位符 `<热点密码>` 改成你选择的密码：

  ```
  $ sudo nmcli connection add con-name 'Hotspot' \
      ifname wlan0 type wifi slave-type bridge master bridge0 \
      wifi.mode ap wifi.ssid Hotspot wifi-sec.key-mgmt wpa-psk \
      wifi-sec.proto rsn wifi-sec.pairwise ccmp \
      wifi-sec.psk <热点密码>
  ```

现在你已配置好桥接，是时候激活它了。运行以下命令以激活桥接：

```
$ sudo nmcli connection up Bridge
```

运行以下命令，开始托管你的无线网络：

```
$ sudo nmcli connection up Hotspot
```

你可以使用命令 `nmcli device` 来验证桥接、以太网接口和无线热点接口是否均处于活动状态。

>**技巧**
>
>可使用诸如 [arp-scan](https://github.com/royhills/arp-scan) 之类的工具，检查接入热点后，是否可访问父网络上的设备。

## 使用代理服务器

代理服务器是客户端设备和互联网之间的中介。要将你的树莓派配置为代理服务器客户端，请按照本节中的说明操作。

 你将需要：

* 代理服务器的 IP 地址或者主机名和端口
* 如果需要，为你的代理设置用户名和密码

### 配置你的树莓派

你需要设置三个环境变量（`http_proxy`、`https_proxy`、`no_proxy`），以便你的树莓派知道如何访问代理服务器。

打开终端，并使用 nano 打开文件 `/etc/environment`：

```
$ sudo nano /etc/environment
```

将以下内容添加到文件 `/etc/environment`，以创建变量 `http_proxy`：

```
export http_proxy="http://<代理IP地址>:<代理端口>"
```

用代理的 IP 地址和端口分别替换占位符 `<代理IP地址>` 和 `<代理端口>`。

>**注意**
>
>如果你使用的代理需要用户名和密码，请使用以下格式：
>
>```
>export http_proxy="http://<用户名>:<密码>@代理IP地址:代理端口"
>```
>
>把你用于验证代理的用户名和密码分别替换占位符 `<用户名>` 和 `<密码>`。


为环境变量 `https_proxy` 输入相同的信息：

```
export https_proxy="http://<用户名>:<密码>@代理IP地址:代理端口"
```

创建环境变量 `no_proxy`，这是一个由逗号分隔的地址列表，你的树莓派不应该使用代理。

```
export no_proxy="localhost, 127.0.0.1"
```

你的 `/etc/environment` 文件现在应该如下所示：

```
export http_proxy="http://<用户名>:<密码>@代理IP地址:代理端口"
export https_proxy="http://<用户名>:<密码>@代理IP地址:代理端口"
export no_proxy="localhost, 127.0.0.1"
```

按 **Ctrl** + **X** 保存并退出。

### 更新 `sudoers` 文件

要在下载和安装软件等以 `sudo` 方式运行的操作中，使用代理环境变量，请更新 sudoers。

使用以下命令打开 `sudoers`：

```
$ sudo visudo
```

将以下行添加到文件中，这样 `sudo` 将使用你刚刚创建的环境变量：

```
Defaults	env_keep+="http_proxy https_proxy no_proxy"
```

按 **Ctrl** + **X** 保存并退出。

### 重启你的树莓派

重启你的树莓派以使修改生效。现在你应该能够通过代理服务器访问互联网了。

## boot 文件夹内容

树莓派系统把引导文件放在 SD 卡的首个分区上，分区被格式化成 FAT 文件系统。

在启动时，每种树莓派都会从引导分区加载所有文件，以便在 Linux 内核启动之前启动各个处理器。

在启动时，Linux 把引导分区挂载到 `/boot/firmware/`。

>**注意**
>
>在 Bookworm 之前，树莓派系统将引导分区放在 `/boot/`。自 Bookworm 以降，引导分区位于 `/boot/firmware/`。

### `bootcode.bin`

SoC 在启动时会加载引导加载程序。它会执行一些非常基本的设置，然后再加载某个 `start*.elf` 文件。

树莓派 4、5 不使用 `bootcode.bin`。它们使用板载 EEPROM 中的引导代码。

### `start*.elf`

加载 SoC 中 VideoCore GPU 上的二进制固件，然后接管引导过程。

`start.elf`

　　基本固件

`start_x.elf` 

　　包含额外的编解码器

`start_db.elf`

　　用于调试

`start_cd.elf`
　　
　　精简版本的固件，移除了对硬件区域（如编解码器和 3D）以及调试日志支持的支持；它还施加了对初始帧缓冲区限制。当在 `config.txt` 中指定 `gpu_mem=16` 时，将自动调用精简固件。

`start4.elf`、`start4x.elf`、`start4db.elf` 和 `start4cd.elf` 是树莓派 4 系列（树莓派 4B、400，计算模块 4、4S）的专用固件文件。

要了解如何使用这些文件的更多信息，请参阅 [config.txt 文档](https://www.raspberrypi.com/documentation/computers/config_txt.html#boot-options)。

树莓派 5 不再使用 `elf` 文件。固件内置于引导加载程序 EEPROM。

### `fixup*.dat`

在匹配的情况下找到链接器文件与前一节中列出的 `start*.elf` 文件。

### `cmdline.txt`

[内核命令行](https://www.raspberrypi.com/documentation/computers/configuration.html#kernel-command-line-cmdline-txt)，将传递给引导时的内核。

### `config.txt`

涉及许多用于设置树莓派的配置参数。有关更多信息，请参阅 [config.txt 文档](https://www.raspberrypi.com/documentation/computers/config_txt.html)。

>**重要**
>
>树莓派 5 要求在启动分区中，有一个非空的 `config.txt` 文件存在。

### `issue.txt`

包含发行版日期和 git 提交 ID 的文本化维护信息。

### `initramfs*`

初始内存盘的内容。将在真实的根文件系统挂载之前，把临时根文件系统加载到内存。

自 Bookworm 版本以降，树莓派系统默认内置了一个 `initramfs` 文件。要启用初始内存盘，请在 [`config.txt`](https://www.raspberrypi.com/documentation/computers/config_txt.html) 中使用关键字 [`auto_initramfs`](https://www.raspberrypi.com/documentation/computers/config_txt.html#auto_initramfs) 进行配置。

### ssh（ssh.txt）

若存在此文件，会在启动时启用 SSH。否则，默认情况下会禁用 SSH。内容无关紧要，即使是空文件也会启用 SSH。

### DTB 文件(`*.dtb`)

DTB 文件涉及各种树莓派型号的硬件定义。这些文件根据[检测到的树莓派型号](https://www.raspberrypi.com/documentation/computers/configuration.html#part3.1)，在启动时设置内核。

### 内核文件(`*.img`)

适用于各种树莓派型号的内核镜像文件：

| 文件名 | 处理器                    | 树莓派型号                                                                     | 注解                                           |
| :--------: | :---------------------------: | :--------------------------------------------------------------------------------: | -------------------------------------------------- |
| `kernel.img`       | BCM2835                   | 树莓派 Zero，树莓派 1                                                                  |                                                  |
| `kernel7.img`       | BCM2836，BCM2837          | 树莓派 Zero 2 W，树莓派 2、3                                            | 基于 BCM2837 的新版树莓派 2                     |
| `kernel7l.img`       | BCM2711                   | 树莓派 4、400，CM4，CM4S                                                        | 大物理地址扩展（LPAE）                           |
| `kernel8.img`       | BCM2837，BCM2711，BCM2712 | 树莓派 Zero 2 W，树莓派 2、3、4、400，CM4、CM4S、5 | [64 位内核](https://www.raspberrypi.com/documentation/computers/config_txt.html#boot-options)。基于 BCM2836 的树莓派 2 不支持 64 位内核。|
| `kernel_2712.img`       | BCM2712                   | 树莓派 5                                                                       | 为树莓派 5 优化的 [64 位内核](https://www.raspberrypi.com/documentation/computers/config_txt.html#boot-options)。                |

>**注意**
>
>在运行 32 位内核系统上，`lscpu` 会把 CPU 架构报告成 `armv7l`；在运行 64 位内核系统上，lscpu 会把 CPU 架构报告成 `aarch64`。对于 `armv7l` 来说，`l` 指的是小端 CPU 架构（如 `kernel7l.img` 文件名所示），而非指 `LPAE`。

### 文件夹 `overlays` 

涉及设备树叠加层。这些用于配置各种硬件设备（如第三方声卡）。可使用 `config.txt` 中的条对这些叠加层进行选择。更多有关信息，请参阅[设备树、叠加层和参数](https://www.raspberrypi.com/documentation/computers/configuration.html#part2)。

## LED 警告闪烁代码

在大多数情况下，如果树莓派由于某种原因无法启动（或必须关闭），LED 将闪烁特定次数以指示问题。LED 将发出一定数量的长闪烁（0 或更多次），然后发出短闪烁，以指示确切状态。在大多数情况下，该模式以两秒间隔重复。

| 长闪 | 短闪 | 状态                               |
| :--------: | :--------: | ------------------------------------ |
| 0      | 3      | 无法启动的一般故障                 |
| 0      | 4      | 未找到 start*.elf                  |
| 0      | 7      | 未找到内核镜像                     |
| 0      | 8      | 内存故障                         |
| 0      | 9      | 内部不足                         |
| 0      | 10     | 处于停止状态                       |
| 2      | 1      | 分区不是 FAT                       |
| 2      | 2      | 无法读取分区                 |
| 2      | 3      | 扩展分区不是 FAT                   |
| 2      | 4      | 文件签名或哈希不匹配 - 树莓派 4、5 |
| 3      | 1      | SPI EEPROM 错误 - 树莓派 4、5     |
| 3      | 2      | SPI EEPROM 写保护 - 树莓派 4、5 |
| 3      | 3      | I²C 错误 - 树莓派 4、5            |
| 3      | 4      | 安全启动配置无效                   |
| 4      | 3      | 未找到 RP1                         |
| 4      | 4      | 主板类型不受支持                     |
| 4      | 5      | 致命性固件错误                       |
| 4      | 6      | 电源故障类型 A                     |
| 4      | 7      | 电源故障类型 B                     |

## 配置 UART

树莓派上有两种 UART 可用- [PL011](http://infocenter.arm.com/help/index.jsp?topic=/com.arm.doc.ddi0183g/index.html) 和 mini UART。PL011 是一款功能强大、兼容性好的 16550 UART，而 mini UART 功能较少。

树莓派上所有的 UART 仅支持 3.3V（如接入 5V 设备，将损坏）。可使用适配器转接到 5V 设备。此外，也可以使用各种第三方渠道的廉价 USB 转 3.3V 串口转换器。

### 树莓派 Zero，树莓派 1、2、3

如下，树莓派 Zero，树莓派 1、2、3 各搭载了两个 UART：

| 名称  | 类型      |
| :-------: | :-----------: |
| UART0 | PL011     |
| UART1 | mini UART |

### 树莓派 4 和 400

在默认情况下，树莓派 4B 和 400 搭载了四个另外的 PL011，但它们是被禁用的：

| 名称  | 类型      |
| :-------: | :-----------: |
| UART0 | PL011     |
| UART1 | mini UART |
| UART2 | PL011     |
| UART3 | PL011     |
| UART4 | PL011     |
| UART5 | PL011     |

### 树莓派 5

树莓派 5 搭载着四个另外的 PL011，这些在默认情况下也是被禁用的：

| 名称  | 类型  |
| :-------: | :-------: |
| UART0 | PL011 |
| UART1 | PL011 |
| UART2 | PL011 |
| UART3 | PL011 |
| UART4 | PL011 |

树莓派 5 没有 mini UART。

### CM1、CM3、CM3+ 和 CM4

计算模块 1、3、3+ 各搭载了两个 UART，而计算模块 4 有六个 UART（如上所述）。

在所有型号的计算模块上，默认情况下均禁用了 UART，并可以通过使用设备树叠加层来显式启用。你还可以指定要使用的 GPIO 引脚，例如：

```
dtoverlay=uart1,txd1_pin=32,rxd1_pin=33
```

### 主 UART

在树莓派上，使用 GPIO 14（发送）和 15（接收）的 UART - 就是主 UART。在默认情况下，大概率也会把 Linux 控制台输出至该 UART。请注意，GPIO 14 是 GPIO 引脚上的引脚 8，而 GPIO 15 是引脚 10。

在树莓派 5 上，主 UART 出现在调试标头上。

### 次要 UART

次要 UART 通常并不接入 GPIO 连接器。在默认情况下，次要 UART 连接到了无线局域网和蓝牙控制器（复合）的蓝牙一侧，如果该型号搭载了此控制器。

### 主次 UART

以下表格总结了各种树莓派设备上 UART 的分配：

| 型号                            | 主/控制台 | 次/蓝牙 |
| :---------------------------------: | :-----------: | :-----------: |
| 树莓派 Zero                     | UART0     | UART1     |
| 树莓派 Zero W、Zero 2 W | UART1     | UART0     |
| 树莓派 1                        | UART0     | UART1     |
| 树莓派 2                        | UART0     | UART1     |
| 树莓派 3                        | UART1     | UART0     |
|计算模块 3 & 3+                 | UART0     | UART1     |
| 树莓派 4                        | UART1     | UART0     |
| 树莓派 5                        | UART10    |           |

树莓派系统上的 Linux 设备：

| Linux 设备 | 说明                  |
| :------------: | :-----------------------: |
| `/dev/ttyS0`           | mini UART             |
| `/dev/ttyAMA0`           | 第一个 PL011（UART0） |
| `/dev/serial0`           | 主 UART               |
| `/dev/serial1`           | 次 UART               |
| `/dev/ttyAMA10`           | 树莓派 5 调试 UART    |

`/dev/serial0` 是指向 `/dev/ttyS0` 的符号链接、`/dev/serial1` 是指向 `/dev/ttyAMA0` 的符号链接。

在树莓派 5 上，`/dev/serial0` 是指向 `/dev/ttyAMA10` 的符号链接。

由于 Bookworm 的变更，在默认情况，`/dev/serial1` 并下不存在。你可以通过在 config.txt 中，设置以下值再次启用 serial1 ：

```
dtparam=krnbt=off
```

>**技巧**
>
>该参数可能不会兼容将来的所有型号。应仅在你的用例无其他替代方案时，才使用该选项。

### mini UART 和 CPU 核心频率

>**注意**
>
> 如果 mini UART 是主要的（蓝牙被禁用），则默认情况下会禁用 mini UART。

为了使用 mini UART，你需要配置树莓派以使用固定的 VPU 核心时钟频率。这是因为 mini UART 时钟与 VPU 核心时钟关联，因此当核心时钟频率发生变化时，UART 波特率也会发生变化。可以将 `enable_uart` 和 `core_freq` 设置添加到 `config.txt` 中，以修改 mini UART 的行为。以下表总结了可能的情况：

| mini UART 的设置 | 核心时钟                      | 结果                                                                                 |
| :------------------: | :-------------------------------: | -------------------------------------------------------------------------------------- |
| 主 UART          | 变量                          | mini UART 已禁用                                                                     |
| 主 UART          | 通过设置 `enable_uart=1` 来修复 | 启用 mini UART，核心时钟固定为 250MHz；如设置 `force_turbo=1`，则为 VPU 超频频率 |
| 次要 UART        | 可变                          | mini UART 已禁用                                                                     |
| 二级 UART        | 通过设置 `core_freq=250` 修复 | mini UART 已启用                                                                     |

参数 `enable_uart` 的默认状态取决于哪个 UART 是主 UART：

| 主 UART               |   参数 `enable_uart` 的默认状态 |
| :-----------------------: | :--------------------------: |
| mini UART             | 0                        |
| 第一个 PL011（UART0） | 1                        |

### 禁用 Linux 串口控制台

在默认情况下，主 UART 被分配给 Linux 控制台。如果你希望将主 UART 用于其他目的，你必须重新配置树莓派系统。这可以通过使用 [`raspi-config`](https://www.raspberrypi.com/documentation/computers/configuration.html#raspi-config) 来实现：

* 启动 raspi-config：`sudo raspi-config`
* 选择  option 3 - Interface Options
* 选择 option P6 - Serial Port
* 在提示符 `Would you like a login shell to be accessible over serial?` 处，回答“No”
* 在提示符 `Would you like the serial port hardware to be enabled?` 处，回答“Yes”
* 退出 `raspi-config` 并重启树莓派，以使修改生效

### 启用 Linux 的早期控制台

尽管在 Linux 内核引导过程中，相对较早地启动了 UART，但仍然比一些关键基础设施设置晚得多。如果无法得到这些早期阶段的内核日志信息，可能很难诊断在那个时间段出现的故障。要为其中某个 UART 启用 `earlycon` 支持，请根据所选的主 UART，向 cmdline.txt 中添加以下某选项：

以下配置，对于树莓派 5，`earlycon` 仅输出到调试连接器（3 针）：

```
earlycon=pl011,0x107d001000,115200n8
```

对于树莓派 4、400 和计算模块 4：

```
earlycon=uart8250,mmio32,0xfe215040
earlycon=pl011,mmio32,0xfe201000
```

对于树莓派 2、3 和计算模块 3：

```
earlycon=uart8250,mmio32,0x3f215040
earlycon=pl011,mmio32,0x3f201000
```

对于树莓派 1，树莓派 Zero 和计算模块 1：

```
earlycon=uart8250,mmio32,0x20215040
earlycon=pl011,mmio32,0x20201000
```

默认波特率为 115200bps。

>**注意**
>
>选择错误的早期控制台可能会妨碍树莓派启动。

### UART 和设备树

在[内核 GitHub](https://github.com/raspberrypi/linux) 中，可以找到各种 UART 设备树叠加层定义。最有用的两个叠加层是 [`disable-bt`](https://github.com/raspberrypi/linux/blob/rpi-6.1.y/arch/arm/boot/dts/overlays/disable-bt-overlay.dts) 和 [`miniuart-bt`](https://github.com/raspberrypi/linux/blob/rpi-6.1.y/arch/arm/boot/dts/overlays/miniuart-bt-overlay.dts)。

`disable-bt` 禁用蓝牙设备，并将第一个 PL011（UART0）设置为主 UART。你还必须禁用初始化调制解调器的系统服务，以防它连接到 UART：可使用 `sudo systemctl disable hciuart`。

`miniuart-bt` 将蓝牙功能切换到使用 mini UART，并将第一个 PL011（UART0）设置为主 UART。请注意，这可能会降低最大可用波特率（请参阅下文有关 mini UART 限制的内容）。你还必须使用 `force_turbo=1` 或 `core_freq=250` 将 VPU 核心时钟设置为固定频率。

叠加层 `uart2`、`uart3`、`uart4` 和 `uart5` 用于在树莓派 4 上启用四个另外的 UART。在文件夹中还有其他特定于 UART 的叠加层。有关设备树叠加层的详细信息，请参考 `/boot/firmware/overlays/README`，或运行 `dtoverlay -h overlay-name` 查看描述和使用信息。

向 `config.txt` 文件添加一行以应用[设备树叠加层](https://www.raspberrypi.com/documentation/computers/configuration.html#device-trees-overlays-and-parameters)。请注意，请去掉文件名中的 `-overlay.dts` 部分。例如：

```
dtoverlay=disable-bt
```

### PL011 和 mini-UART

PL011 UART 和 mini-UART 有若干差异。

mini UART 的 FIFO 比较小。加上缺乏流量控制，导致在较高的波特率下更易丢失字符。它的功能通常也少于 PL011，主要是因为其波特率与 VPU 时钟速度相关联。

与 PL011 相比，mini UART 的不足包括：

* 没有中断检测
* 没有帧错误检测
* 没有奇偶校验位
* 没有接收超时中断

mini UART 和 BCM2835 的 PL011 实现均不带 DCD、DSR、DTR 和 RI 信号。

可在 [SoC 外设文档](https://datasheets.raspberrypi.com/bcm2835/bcm2835-peripherals.pdf?_gl=1*oiqbws*_ga*ODAwMTM3MTg4LjE3MTc1NzY1NTQ.*_ga_22FD70LWDS*MTcyMDk3MjM3Ni4zNi4wLjE3MjA5NzIzNzYuMC4wLjA.)中找到进一步的 mini UART 文档。

## 设备树、叠加层和参数

树莓派内核和固件使用设备树（DT）来描述硬件。这些设备树可能包括用于控制板载功能的 DT 参数。DT 叠加层能描述和配置可选外部硬件，可支持更多控制参数。

固件加载程序（`start.elf` 及其变体）负责加载 DTB（设备树块 - 一种机器可读的 DT 文件）。它根据主板的修订版本选择要加载的 DTB，并进行修改以进一步定制。这种运行时定制避免了许多只有细微差异的 DTB 的需求。

在 `config.txt` 中扫描用户提供的参数，以及所有叠加层及其参数，然后应用。加载程序检查结果来了解（例如）要用于控制台的所有 UART。最后，启动内核，传递指向合并 DTB 的指针。

### 设备树

设备树（DT）是对设备硬件的描述。它应涉及基本 CPU 的名称、其内存配置以及所有外部和内部的外围设备。DT 不应用于描述软件，尽管通过列出硬件模块，通常会触发驱动程序模块的加载。

>**注意**
>
>切记，DT 应与操作系统无关，因此任何 Linux 的特定内容都不应出现在里面。

设备树代表硬件配置，以节点层次结构的形式呈现。每个节点可以包含属性和子节点。属性是命名的字节数组，可以包含字符串、数字（大端序）、任意字节序列以及二者的任意组合。类比于文件系统，节点是目录，属性是文件。树中节点和属性的位置可以用路径描述，使用斜杠作为分隔符，单个斜杠(`/`)表示 root。

#### DTS 基础语法

设备树通常用一种被称为设备树源（DTS）的文本形式编写，并存储在后缀为 `.dts` 的文件中。DTS 语法类似于 C 语言，使用大括号进行分组，并在每行末尾使用分号。请注意，DTS 在封闭大括号后需要英文分号：将其视为 C `struct` 而非函数。编译后的二进制格式称为扁平设备树（FDT）和 DTB，存储在文件 `.dtb` 中。

以下是一个 `.dts` 格式的简单树：

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
* 对另一个 DTS 文件的包含，传统上命名成 `*.dtsi`，类似于 C 中的头文件 `.h` 
* 单个根节点： `/`
* 一对子节点：`node1` 和 `node2`
* 一些节点的子节点：`child-node1` 和 `child-node2`
* 一个标签（`cousin`）和对该标签的引用(`&cousin`)
* 散布在树中的几个属性
* 一个重复的节点 (`/node2`)

属性是简单的键值对，其中值可以为空，也可包含任意字限流。虽然在数据结构中数据类型没有编码，但在设备树源文件中可以表达一些基本数据表示。

文本字符串（以 NUL 结尾）用英文双引号表示：

```
string-property = "a string";
```

单元格是由尖括号分隔的 32 位无符号整数：

```
cell-property = <0xbeef 123 0xabcd1234>;
```

所有字节数据用方括号分隔，并以十六进制输入：

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

`/include/` 指令实现了简单的文本包含，类似于 C 的 `#include` 指令，但是设备树编译器的一个特性会导致不同的使用模式。鉴于节点是被命名的，可能带有绝对路径，因此在 DTS 文件（及其包含文件）中相同的节点可能会出现两次。当发生这种情况时，节点和属性将被合并，根据需要交错和覆盖属性（后续值会覆盖先前的值）。

在以上示例中，`/node2` 的第二次出现会导致把新属性添加到原始属性中：

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

因此，一个 `.dtsi` 可以被覆盖，或为树中的多个位置提供默认值。

#### 标签和引用

树的一部分经常需要引用另一部分，有四种方法可以做到这一点：

**Path strings**

　　类似于文件系统路径，如 `/soc/i2s@7e203000` 是 BCM2835、BCM2836 中 I²S 设备的完整路径。标准 API 不会创建到属性的路径，例如 `/soc/i2s@7e203000/status`：所以，你首先应找到一个节点，然后选择该节点的属性。

**Phandles**

　　是分配给节点的唯一 32 位整数，在其 `phandle` 属性中。出于历史原因，你可能还会看到一个多余的匹配 `linux,phandle`。Phandles 按顺序编号，从 1 开始；0 不是有效的 phandle。它们通常由 DT 编译器分配，当它在整数上下文中遇到对节点的引用时，通常以标签的形式。使用 phandles 引用节点的引用仅被编码为相应的整数（单元）值；没有标记表明它们应被解释为 phandles，因为这是应用程序定义的。

**Labels**

　　就像 C 中的标签为代码中的位置命名一样，DT 标签为层次结构中的节点分配名称。编译器获取标签的引用，并在字符串上下文(`&node`)中将其转换为路径，在整数上下文(`<&node>`)中将其转换为 phandle；原始标签不会出现在编译输出中。请注意，标签不包含结构；它们只是一个扁平的全局命名空间中的标记。

**Aliases**

　　类似于标签，不同之处在于，它们以索引形式出现在 FDT 输出。它们作为 `/aliases` 节点的属性存储，每个属性将别名名称映射到路径字符串。尽管别名节点出现在源中，但路径字符串通常显示为对标签的引用(`&node`)，而不是完全写出。解析路径字符串为节点的 DT API 通常查看路径的第一个字符，将不以斜杠开头的路径视为必须首先使用 `/aliases` 表转换为路径的别名。

#### 设备树语义

如何构建设备树，以及如何最好地使用它来捕获一些硬件的配置，是一个庞大而复杂的主题。有许多可用资源，其中一些列在下面，但有几点值得强调：

* `compatible`

　　属性是硬件描述和驱动软件之间的链接。当操作系统遇到具有 compatible 属性的节点时，它会在其设备驱动程序数据库中查找最佳匹配项。在 Linux 中，这通常会触发驱动程序模块的自动加载，前提是它已经被适当标记并且未被列入黑名单。
  
* `status`

　　属性指示启用还是禁用设备。如果 status 是 ok，okay 和不存在，则设备已启用。否则，status 应是 disabled，以便禁用设备。将设备放置在某个 .dtsi 文件中，并将状态设置为 disabled 可能很有用。然后，派生配置可以包括该 .dtsi，并把所需设备的状态设置为 okay。

### 设备树叠加层

现代片上系统（SoC）是一个非常复杂的设备；完整的设备树可能长达数百行。再进一步，将 SoC 放置在带有其他组件的主板上，只会使情况变得更加复杂。为了保持可管理性，特别是如果有共享组件的相关设备，将共同元素放入 `.dtsi` 文件，以便从可能的多个 `.dts` 文件中包含，这是有道理的。

像树莓派这样的系统，如果还能支持可选的插件配件（如 HAT），问题就会变得更加复杂。最终，每种可能的配置都需要一个设备树来描述它，但假如考虑到所有不同的基本型号和大量可用的配件，组合的数量开始迅速增加。

需要一种方法来描述这些可选组件：使用部分设备树，然后通过采用基本 DT，并添加一些可选元素来构建完整的树。你可以这样做，这些可选元素称为"叠加层"。

除非你想要学习如何为树莓派编写叠加层，否则你可能更喜欢跳转到[使用设备树](https://www.raspberrypi.com/documentation/computers/configuration.html#part3)。

#### 片段

DT 叠加层包含多个片段，每个片段都针对一个节点及其子节点。尽管概念听起来很简单，但刚开始的语法似乎相当奇怪：

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

字符串 `compatible` 标识是为 BCM2835 设计的，这是树莓派 SoC 的基本架构；如果叠加层使用了树莓派 4 的功能，则正确的值为 `brcm,bcm2711`。除此外，brcm,bcm2835 可用于所有树莓派叠加层。然后是第一个（在这种情况下是唯一的）片段。片段应从零开始编号。不遵守这点可能导致某些片断或全部片段被忽视。

每个片段都由两部分组成：一个 `target` 属性，用于标识要应用叠加层的节点；以及 `__overlay__` 本身，其主体将添加到目标节点。如果它是这样编写的，上面的示例可以解释为：

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

使用版本够新的 `dtc`，你可以按照上述示例编写并获得相同的输出，但一些自制工具尚不支持这种格式。目前，应以旧格式编写所有你希望其包含在标准树莓派系统内核的叠加层。

将该叠加层与标准树莓派基础设备树（例如 `bcm2708-rpi-b-plus.dtb`）合并的效果，前提是叠加层在之后加载，将启用 I²S 接口，将其状态修改为 `okay`。但是，如果尝试使用以下方式编译此叠加层：

```
$ dtc -I dts -O dtb -o 2nd.dtbo 2nd-overlay.dts
```

...你将收到错误消息：

```
Label or path i2s not found
```

这并不怎么意外，因为没有提及基础 `.dtb`、`.dts` 文件，编译器找不到标签 `i2s`。

再试一次，这次使用原始示例并添加选项 `-@` 以允许未解决的引用（和 `-Hepapr` 以解决一些麻烦）：

```
$ dtc -@ -Hepapr -I dts -O dtb -o 1st.dtbo 1st-overlay.dts
```

如果 `dtc` 返回的报错有关第三行，则它没有工作所需的扩展工具。请运行 `sudo apt install device-tree-compiler`，然后重试一次。这次，编译应该成功完成。请注意，适当的编译器也可在内核树中作为 `scripts/dtc/dtc` 使用，当使用 `dtbs` make target 时构建：

```
$ make ARCH=arm dtbs
```

转储 DTB 文件的内容，查看编译器生成了什么：

```
$ fdtdump 1st.dtbo
```

输出应类似如下：

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

在文件结构的详细描述之后，我们有了一个片段。但请仔细观察 - 我们在 `&i2s` 处写了什么，现在却写成了 `0xffffffff`，这表明发生了一些奇怪的事情（较旧版本的 dtc 可能会写成 `0xdeadbeef`）。编译器还添加了一个包含唯一（对于此叠加层而言）的小整数的 `phandle` 属性，以指示该节点具有标签，并用相同的小整数替换了对标签的所有引用。

在片段之后有三个新节点：

* `__symbols__` 列出了覆盖中使用的标签（ `test_label` 在这里），以及带有标签节点的路径。这个节点是如何处理未解析符号的关键。
* `__fixups__` 包含一个属性映射列表，将未解析符号的名称映射到需要使用目标节点的 phandle 进行修补的片段内单元格路径列表。在这种情况下，路径是到 `target` 的 `0xffffffff` 值，但片段可能包含其他未解析引用，这将需要额外的修复。
* `__local_fixups__` 保存了存在于叠加层内的标签引用的位置 - `test_ref` 属性。这是必需的，因为执行合并的程序必须确保 phandle 编号是连续且唯一的。

在 [1.3 节](https://www.raspberrypi.com/documentation/computers/configuration.html#part1.3)中提到“原始标签不会出现在编译输出中”，但是当使用 `-@` 开关时，情况并非如此。相反，每个标签都会导致节点 `__symbols__` 中的一个属性，将标签映射到路径，就像节点 `aliases` 一样。实际上，机制如此相似，以至于在解析符号时，树莓派加载程序会在没有 `__symbols__` 节点的情况下搜索“别名”节点。曾经，这非常有用，因为提供足够的别名可允许使用非常老版本的 `dtc` 来构建基本的 DTB 文件，但幸运的是，那已经是远古历史了。

#### 设备树参数

为了避免需要大量的设备树叠加层，减少外围设备用户修改 DTS 文件的需要，树莓派加载程序支持一项新功能 - 设备树参数。这允许使用命名参数对 DT 进行小修改，类似于内核模块从 `modprobe` 和内核命令行接收参数的方式。参数可以由基本 DTB 和叠加层暴露，包括 HAT 叠加层。

通过在根节点添加一个 `__overrides__` 节点来定义参数。它包含属性，其名称是选择的参数名称，其值是一个序列，包括目标节点的 phandle（对标签的引用）和指示目标属性的字符串；支持字符串、整数（单元）和布尔属性。

##### 字符串参数

字符串参数的声明方式如下：

```
name = <&label>,"property";
```

其中 `label` 和 `property` 将被适当的值替换。字符串参数可能导致它们的目标属性增长、缩小或被创建。

请注意，名为 `status` 的属性被特殊对待；非零/true/yes/on 值将被转换为字符串 `"okay"`，而 零/false/no/off 将变为 `"disabled"`。

##### 整数参数

整数参数是这样声明的：

```
name = <&label>,"property.offset"; // 8-bit
name = <&label>,"property;offset"; // 16-bit
name = <&label>,"property:offset"; // 32-bit
name = <&label>,"property#offset"; // 64-bit
```

在这里，`label`、`property` 和 `offset` 将被适当的值替换；偏移量以字节为单位相对于属性的起始位置指定（默认为十进制），前面的分隔符指定参数的大小。与早期实现不同，整数参数可以引用不存在的属性或超出现有属性末尾的偏移量。

##### 布尔参数

设备树将布尔值编码为零长度属性；如果存在，则该属性为真；如果不存在，则该属性为假。它们的定义如下：

```
boolean_property; // 设置 'boolean_property' 为 true
```

通过不定义属性将其分配值 `false`。布尔参数的声明如下，用适当的值替换占位符 `label` 和 `property` ：

```
name = <&label>,"property?";
```

倒置布尔在应用相同方式之前反转输入值，就像常规布尔一样；它们的声明方式类似，但使用 `!` 表示反转：

```
name = <&label>,"<property>!";
```

布尔参数可以触发属性创建或删除，但它们不能删除基本 DTB 中已经存在的属性。

##### 字节字符串参数

字节字符串属性是任意字节序列（如 MAC 地址）。它们接受十六进制字节的字符串，字节之间可以有英文冒号，也可以没有。

```
mac_address = <&ethernet0>,"local_mac_address[";
```

选择 `[` 是为了与声明字节字符串的 DT 语法匹配：

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

（示例来自 w1-gpio 叠加层）

>**注意**
>
>甚至可以使用单个参数针对不同类型的属性。你可以合理地将“启用”参数连接到字符串 `status`、包含零或一的单元格以及适当的布尔属性。

##### 文本分配

DT 参数机制允许从同一参数中修补多个目标，但其效用受到限制，因为必须将相同的值写入所有位置（除了格式转换和从反转布尔值中获得的否定）。嵌入式文字分配的添加允许参数写入任意值，而不管用户提供的参数值如何。

分配出现在声明的末尾，并由 `=` 表示：

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

应用叠加层时，标签将按照通常的方式针对基本 DTB 进行解析。最好将多部分参数拆分到多行，以便更容易阅读 - 随着单元值分配的增加，这变得更加必要。

请记住，除非应用了参数，否则参数不起作用 - 查找表中的默认值将被忽略，除非使用参数名称而不指定值。

##### 查找表

查找表允许在使用之前转换参数输入值。它们充当关联数组，有点像 switch/case 语句：

```
phonetic = <&node>,"letter{a=alpha,b=bravo,c=charlie,d,e,='tango uniform'}";
bus      = <&fragment>,"target:0{0=",<&i2c0>,"1=",<&i2c1>,"}";
```

没有 `=value` 的键意味着将键用作值，没有键的 = 表示在没有匹配项的情况下是默认值，并且以逗号开始或结束列表（或在任何地方使用空键=值对）表示未匹配的输入值应该保持不变；否则，找不到匹配项将会报错。

>**注意**
>
>在单元格整数值后的表字符串中，逗号分隔符是隐式的 - 明确添加一个会创建一个空对（见上文）。

>**注意**
>
>由于查找表操作的是输入值，而文字赋值会忽略它们，因此不可能将两者结合在一起 - 查找声明中 `}` 结束后的字符被视为错误。

##### 叠加层/片段参数

描述中所述的 DT 参数机制存在许多限制，包括缺乏创建整数数组的简便方法，以及无法创建新节点。克服其中一些限制的方法是有条件地包含或排除某些片段。

通过将 `__overlay__` 节点重命名为 `__dormant__`，可以将片段从最终合并过程中排除（禁用）。参数声明语法已扩展，以允许否则非法的零目标 phandle 指示以下字符串包含片段或叠加层范围的操作。到目前为止，已实现了四种操作：

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

叠加层 `i2c-rtc` 使用这种技术。

##### 特殊属性

一些属性名称，在被参数定位时，会得到特殊处理。你可能已经注意到的一个 - `status` - 将布尔值转换为 `okay` 表示 true，`disabled` 表示 false。

分配给 `bootargs` 属性会将其附加到其末尾，而不是覆盖它 - 这是如何向内核命令行添加设置的方式。

`reg` 属性用于指定设备地址 - 内存映射硬件块的位置，I²C 总线上的地址等。子节点的名称应该用十六进制地址加以限定，使用 `@` 作为分隔符：

```
bmp280@76 {
    reg = <0x77>;
    ...
};
```

当分配给 `reg` 属性时，父节点名称的地址部分将被替换为分配的值。这可用于在多次使用相同叠加层时防止节点名称冲突 - 这是 `i2c-gpio` 叠加层使用的技术。

`name` 属性是一个伪属性 - 它不应出现在 DT 中，但是对其赋值会导致其父节点的名称修改为分配的值。与 `reg` 属性一样，这可以用于给节点提供唯一的名称。

##### 叠加层映射文件

随着树莓派 4（围绕 BCM2711 SoC 构建）的推出，带来了许多变化；其中一些变化是额外的接口，另一些是对现有接口进行的修改（删除）。有一些新的叠加层专为树莓派 4 设计，这些叠加层在旧硬件上无意义，如启用新的 SPI、I²C 和 UART 接口的叠加层，但其他叠加层即使控制着新设备上仍然相关的功能，也不能正确应用。

因此，有必要针对具有不同硬件的多个平台定制叠加层方法。在单个 .dtbo 文件中支持它们将需要大量使用隐藏的（“休眠”）片段，并切换到按需符号解析机制，以便不需要的丢失符号不会导致失败。一个更简单的解决方案是添加一个功能，根据当前平台将叠加层名称映射到几个实现文件中的一个。

叠加层映射是固件在引导时加载的文件。它以 DTS 源格式编写 - `overlay_map.dts`，编译为 `overlay_map.dtb` 并存储在叠加层目录中。

这是当前映射文件的摘录（请参阅[完整版本](https://github.com/raspberrypi/linux/blob/rpi-6.6.y/arch/arm/boot/dts/overlays/overlay_map.dts)）:

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

每个节点都有一个需要特殊处理的叠加层名称。每个节点的属性要么是平台名称，要么是少数几个特殊指令之一。当前支持的平台有 `bcm2835`，其中包括所有围绕 BCM2835、BCM2836 和 BCM2837 SoC 构建的树莓派，`bcm2711` 适用于树莓派 4B、400 和 CM4，`bcm2712` 适用于树莓派 5 和 CM5。

没有值的平台名称（空属性）表示当前叠加层与该平台兼容；例如，`uart5` 与 `bcm2711` 平台兼容。对于平台的非空值是要使用的替代叠加层的名称，请求在 BCM2712 上使用 `disable-bt` 会导致加载 `disable-bt-pi5`。未在叠加层节点中包含的任何平台都与该叠加层不兼容。未在映射中提到的任何叠加层都假定与所有平台兼容。

第二个示例节点 - `disable-bt-pi5` - 可以从 `disable-bt` 的内容中推断出，但这种智能是用于文件的构建，而不是用于其解释。

仅在 BCM2711 上使用 `uart5` 叠加层才有意义。

如果未为叠加层列出平台，则可能适用其中一个特殊指令：

* `renamed` 指令表示叠加层的新名称（应与原始名称基本兼容），但也会记录有关更名的警告。
* `deprecated` 指令包含一个简要的解释性错误消息，在通用前缀 `overlay '...' is deprecated:` 之后将被记录。

链接重命名和特定于平台的实现是可能的，但要小心避免循环！

记住：只有异常需要列出 - 覆盖的节点缺失意味着应该为所有平台使用默认文件。

从固件中访问诊断消息已在[调试](https://www.raspberrypi.com/documentation/computers/configuration.html#part5.1)中介绍。

`dtoverlay` 和 `dtmerge` 工具已增补，可支持映射文件：

* `dtmerge` 从基础 DTB 中的兼容字符串中提取平台名称。
* `dtoverlay` 从 live 设备树中读取兼容字符串位于 `/proc/device-tree` 处，但你可以使用选项 `-p` 提供替代平台名称（在不同平台上进行干扰运行时很有用）。

它们都将错误、警告和任何调试输出发送到 STDERR。

##### 示例

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
                bool1; // 默认为 true
                       // bool2 默认为 false
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

更多示例，请查看[树莓派 Linux GitHub 存储库](https://github.com/raspberrypi/linux/tree/rpi-6.1.y/arch/arm/boot/dts/overlays)中托管的大量叠加层源文件。

#### 导出标签

固件中的叠加层处理和使用 `dtoverlay` 工具的运行时叠加层应用将在叠加层中定义的标签视为私有于该叠加层。这样可以避免为标签发明全局唯一名称（使它们保持简短），并且允许同一叠加层多次使用而不发生冲突（前提是使用一些技巧 - 请参阅[特殊属性](https://www.raspberrypi.com/documentation/computers/configuration.html#part2.2.9)）。

有时，创建一个标签并从另一个叠加层中使用它非常有用。自 2020 年 2 月 14 日发布的固件具有将某些标签声明为全局的能力 - `__exports__` 节点：

```
    ...
    public: ...

    __exports__ {
        public; // Export the label 'public' to the base DT
    };
};
```

当应用此叠加层时，加载程序会剥离除了已导出的符号之外的所有符号，在本例中为 `public`，并重新编写路径，使其相对于包含标签的片段的目标。然后加载在此之后的叠加层可以引用 `&public`。

#### 叠加层应用程序顺序

在大多数情况下，片段应用的顺序并不重要，但对于自身打补丁的叠加层（其中片段的目标是叠加层中的标签，称为叠加层内部片段），这变得重要。在旧固件中，片段严格按顺序从上到下应用。自 2020 年 2 月 14 日发布的固件起，片段分两次应用：

* 首先应用并隐藏目标其他片段的片段。
* 然后应用常规片段。

这种拆分对于运行时叠加层特别重要，因为第一步发生在 `dtoverlay` 工具中，第二步由内核执行（无法处理内部叠加层片段）。

### 在树莓派上使用设备树

#### DTB，叠加层和 `config.txt`

在树莓派上，加载程序（其中之一是镜像 `start.elf` ）的工作是将叠加层与适当的基础设备树结合，然后将完全解析的设备树传递给内核。基础设备树位于 FAT 分区（Linux 在 `/boot/firmware/`）中与 `start.elf` 相邻，命名为 `bcm2711-rpi-4-b.dtb`，`bcm2710-rpi-3-b-plus.dtb` 等等。请注意，某些型号（3A+，A，A+）将使用“b” 等效型号（3B+，B，B+），分别。此选择是自动的，并允许在各种设备中使用相同的 SD 卡镜像。

>**注意**
>
>DT 和 ATAG 互斥，将 DT blob 传给不支持它的内核将导致启动失败。固件将始终尝试加载 DT，并将其传递给内核，因为自 rpi-4.4.y 以降，若没有 DTB，所有的内核都无法正常工作。你可以通过在 config.txt 中添加 `device_tree=` 来覆盖此设置，这将强制使用 ATAG，对于简单的裸机内核可能很有用。

现在的加载程序支持使用 bcm2835_defconfig 进行构建，该配置选择了上游 BCM2835 支持。这个配置将导致 `bcm2835-rpi-b.dtb` 和 `bcm2835-rpi-b-plus.dtb` 被构建。如果这些文件与内核一起复制，那么加载程序将尝试默认加载其中一个 DTB。

为了管理设备树和叠加层，加载程序支持一些 `config.txt` 指令：

```
dtoverlay=acme-board
dtparam=foo=bar,level=42
```

这将导致加载程序在固件分区中查找 `overlays/acme-board.dtbo`，树莓派系统挂载在 `/boot/firmware/` 上。然后它将搜索参数 `foo` 和 `level`，并将指定的值分配给它们。

加载程序还将搜索带有已编程 EEPROM 的附加 HAT，并从那里加载支持的叠加层 - 直接或通过“overlays”目录中的名称; 这一切都在没有任何用户干预的情况下发生。

有多种方法可以告诉内核正在使用设备树：

* 在引导过程中，“Machine model:”内核信息具有特定于板的值，如“Raspberry Pi 2 Model B”，而非“BCM2709”。
* `/proc/device-tree` 存在，并包含与 DT 的节点和属性完全相同的子目录和文件。

使用设备树，内核将自动搜索并加载支持指示启用设备的模块。因此，通过为设备创建适当的 DT 叠加层，你可以使设备的用户无需编辑 `/etc/modules`；所有配置都在 `config.txt` 中进行，在 HAT 的情况下，甚至这一步也是不必要的。但是，请注意，诸如 `i2c-dev` 之类的分层模块仍然需要显式加载。

反过来，由于平台设备只有在 DTB 请求时才会被创建，因此不再需要黑名单模块，这些模块过去是由板支持代码中定义的平台设备加载的结果。实际上，当前的树莓派系统镜像不包含黑名单文件（除了一些 WLAN 设备，其中有多个可用驱动程序）。

#### DT 参数

如上所述，DT 参数是一种方便的方式，可以对设备的配置进行小的修改。当前的基本 DTB 支持用于启用和控制板载音频、I²C、I²S 和 SPI 接口的参数，而无需使用专用叠加层。在使用中，参数看起来像这样：

```
dtparam=audio=on,i2c_arm=on,i2c_arm_baudrate=400000,spi=on
```

>**注意**
>
>多个赋值可以放在同一行，但要确保不超过 80 个字符的限制。


如果你有一个定义一些参数的叠加层，可以在后续行上指定这些参数，就像这样：

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

#### 特定于主板的标签和参数

树莓派开发板有两个 I²C 接口。这些通常分为：一个用于 ARM，一个用于 VideoCore（GPU）。几乎在所有型号上，`i2c1` 属于 ARM，`i2c0` 属于 VC，用于控制摄像头并读取 HAT EEPROM。然而，两个早期版本的 B 型树莓派设定相反。

为了使所有树莓派都能使用一组叠加层和参数，固件创建了一些特定于主板的 DT 参数。这些是：

```
i2c/i2c_arm
i2c_vc
i2c_baudrate/i2c_arm_baudrate
i2c_vc_baudrate
```

这些分别是 `i2c0`，`i2c1`，`i2c0_baudrate` 和 `i2c1_baudrate` 的别名。建议仅在确实需要时使用 `i2c_vc` 和 `i2c_vc_baudrate` - 例如，如果你正在编程 HAT EEPROM（最好使用 `i2c-gpio` 叠加层使用软件 I²C 总线）。启用 `i2c_vc` 可能会导致树莓派相机、树莓派触摸显示屏无法正常工作。

对于编写叠加层的人，相同的别名已应用于 I²C DT 节点上的标签。因此，你应该编写：

```
fragment@0 {
    target = <&i2c_arm>;
    __overlay__ {
        status = "okay";
    };
};
```

使用数字变体的任何叠加层将被修改为使用新的别名。

#### 扩展板（HAT）和设备树

树莓派扩展板是搭载了嵌入式 EEPROM 的附加板，专为具有 40 针引脚头的树莓派设计。EEPROM 包括启用板（或要从文件系统加载的叠加层的名称）所需的任何 DT 叠加层，此叠加层还可以公开参数。

HAT 叠加层在基本 DTB 之后由固件自动加载，因此其参数可在加载任何其他叠加层之前访问，或者在使用 `dtoverlay=` 结束叠加层范围之前访问。如果出于某种原因你想要抑制 HAT 叠加层的加载，请在任何其他 `dtoverlay` 或 `dtparam` 指令之前放置 `dtoverlay=`。

#### 动态设备树

从 Linux 4.4 开始，树莓派内核支持动态加载叠加层和参数。兼容内核管理一个叠加层的堆栈，这些叠加层叠加层在基本 DTB 之上。修改立即反映在 `/proc/device-tree` 中，可能导致模块被加载和平台设备被创建和销毁。

上面提到的“堆栈”一词很重要 - 叠加层只能在堆栈顶部添加和移除；修改堆栈中较低位置的内容需要首先移除其顶部的任何内容。

有一些用于管理叠加层的新命令：

##### 命令 `dtoverlay` 

`dtoverlay` 是一个命令行工具，可在系统运行时加载和移除叠加层，同时列出可用的叠加层并显示其帮助信息。

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

与 `config.txt` 等效不同，所有叠加层的参数必须包含在同一条命令行中 - [dtparam](https://www.raspberrypi.com/documentation/computers/configuration.html#part3.5.2) 命令仅用于基本 DTB 的参数。

修改内核状态的命令变体（添加和移除内容）需要 root 权限，因此你可能需要在命令前加上 `sudo`。只有在运行时应用的叠加层和参数可以被卸载 - 固件应用的叠加层或参数会被“烘焙”，因此不会被 `dtoverlay` 列出，也无法移除。

##### 命令 `dtparam` 

`dtparam` 创建并加载一个覆盖层，其效果基本与在 `config.txt` 中使用 `dtparam` 指令相同。在使用上，它与具有 - 的覆盖层名称的 `dtoverlay` 基本等效，但存在一些差异： `dtparam` 将列出基础 DTB 的所有已知参数的帮助信息。仍然可以使用 `dtparam -h` 获取有关 dtparam 命令的帮助。在指示要移除的参数时，只能使用索引号（而非名称）。并非所有 Linux 子系统都会在运行时响应设备的添加 - I²C、SPI 和声音设备可以工作，但有些则不行。

##### 撰写运行时可用覆盖层的指南

创建或删除设备对象是由添加或移除节点，或节点状态从禁用变为启用或反之触发的。"status"属性的缺失意味着节点已启用。

不要在将覆盖基础 DTB 中现有节点的片段内创建节点 - 内核将重命名新节点以使其唯一。如果要修改现有节点的属性，请创建一个针对它的片段。

ALSA 不会阻止其编解码器和其他组件在使用中被卸载。在使用中删除叠加层可能会导致内核异常，如果删除的编解码器仍在声卡中使用。实验发现设备在叠加层中以片段顺序的相反顺序被删除，因此将卡的节点放在组件节点之后允许有序关闭。

##### 注意事项

在运行时加载叠加层是内核的一个最新功能，截至撰写本文时，尚无一种被接受的方法可以从用户空间执行此操作。通过将此机制的细节隐藏在命令背后，用户可以在不同内核接口标准化的情况下免受影响。

* 一些叠加层在运行时的效果比其他叠加层更好。设备树的某些部分仅在引导时使用 - 使用叠加层修改它们不会产生任何效果。
* 应用或移除一些叠加层可能会导致意外行为，因此应谨慎进行。这就是需要 `sudo` 的原因之一。
* 卸载 ALSA 卡的叠加层可能会因为某些正在使用 ALSA 的活动而停滞不前 - LXPanel 音量滑块插件展示了这种效果。为了使声卡的叠加层能够被移除，`lxpanelctl` 工具已被赋予两个新选项 - `alsastop` 和 `alsastart` - 并且这些选项在加载或卸载叠加层之前和之后分别从辅助脚本 `dtoverlay-pre` 和 `dtoverlay-post` 中调用。
* 移除叠加层不会导致已加载的模块被卸载，但可能会导致一些模块的引用计数降至零。运行 `rmmod -a` 两次将导致未使用的模块被卸载。
* 覆盖必须按相反顺序移除。这些命令将允许你移除较早的覆盖，但所有中间的覆盖将被移除并重新应用，这可能会产生意想不到的后果。
* 仅会探测树顶层和总线节点的子级的设备树节点。对于运行时添加的节点，进一步的限制是总线必须注册通知以添加和移除子级。但是，有一些例外情况会打破这个规则并引起混淆：内核明确扫描整个树以寻找某些设备类型 - 时钟和中断控制器是主要的两种 - 以便（对于时钟）早期初始化它们和/或（对于中断控制器）按特定顺序初始化。这种搜索机制仅在引导过程中发生，因此对于运行时由覆盖添加的节点不起作用。因此，建议将固定时钟节点放在树的根部，除非保证覆盖不会在运行时使用。

#### 支持的覆盖和参数

请参考 `/boot/firmware/overlays` 中找到的叠加层 `.dtbo` 文件旁边的 [README](https://github.com/raspberrypi/firmware/blob/master/boot/firmware/overlays/README) 文件。它会随着添加和修改而保持最新。

### 固件参数

固件使用特殊的 [`/chosen`](https://www.kernel.org/doc/html/latest/devicetree/usage-model.html#runtime-configuration) 节点在引导加载程序及固件与操作系统之间传递参数。除非另有说明，否则每个属性都存储为 32 位整数。

`overlay_prefix`

　　（**字符串**）由 `config.txt` 选择的 [`overlay_prefix`](https://www.raspberrypi.com/documentation/computers/config_txt.html#overlay_prefix) 字符串。

`os_prefix` 

　　（**字符串**）由 `config.txt` 选择的 [os_prefix](https://www.raspberrypi.com/documentation/computers/config_txt.html#os_prefix) 字符串。

`rpi-boardrev-ext`

　　来自 [OTP 第 33 行](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#otp-register-and-bit-definitions) 的扩展板修订代码。

`rpi-country-code`

　　[PiWiz](https://github.com/raspberrypi-ui/piwiz) 使用的区域代码。仅适用于树莓派 400。

`rpi-duid` 

　　（**字符串**）仅适用于树莓派 5。PCB 上二维码的字符串表示。

#### 通用引导加载程序属性 `/chosen/bootloader`

除非另有说明，否则每个属性都存储为 32 位整数。

`boot-mode`

　　用于加载内核的引导模式。请参阅 [BOOT_ORDER](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#BOOT_ORDER)。

`partition`

　　引导过程中使用的分区号。如果加载了 `boot.img` ramdisk，则此引用的是 ramdisk 中加载的分区，而不是 ramdisk 内部的分区号。

`pm_rsts` 

　　引导过程中 `PM_RSTS` 寄存器的值。

`tryboot`

　　如果在启动时设置了参数 `tryboot` ，则设置为 1。

#### 电源适配器属性 `/chosen/power`

仅适用于树莓派 5。除非另有说明，否则每个属性均被存储为 32 位整数。

`max_current`

　　电源适配器可以提供的最大电流（以 mA 为单位）。固件报告由 USB-C、USB-PD 或 PoE 接口指示的值。对于台式电源适配器（例如连接到 GPIO 排针），请在引导加载程序配置中定义 `PSU_MAX_CURRENT` 以指示电源适配器的电流能力。

`power_reset` 

　　仅适用于树莓派 5。一个位字段，指示 PMIC 被重置的原因。

| 位 | 原因     |
| :----: | :----------: |
| 0  | 过压     |
| 1  | 低压   |
| 2  | 高温     |
| 3  | 启用信号 |
| 4  | Watchdog   |

`rpi_power_supply` 

　　（**两个 32 位整数**）官方树莓派 27W 电源适配器的 USB VID 和 Product VDO（如已接入）。

`usb_max_current_enable` 

　　如果 USB 接口电流限制器在启动时设置为低限，则为 0；如果启用了高限，则为非 0 值。如果电源适配器报告其最大电流为 5A 或在 `config.txt` 中强制使用 `usb_max_current_enable=1`，则自动启用高电平。

`usb_over_current_detected` 

　　如果在 USB 启动期间发生 USB 过流事件，则为非 0 值。

`usbpd_power_data_objects`

　　（**包含多个 32 位整数的二进制数据块**）引导加载程序在 USB-PD 协商期间接收到的原始二进制 USB-PD 对象（仅限固定供电）。要为错误报告捕获此内容，请运行 `hexdump -C /proc/device-tree/chosen/power/usbpd_power_data_objects`。

格式由 [USB PD](https://usb.org/document-library/usb-power-delivery)规范定义。

#### BCM2711 和 BCM2712 特定的引导加载程序属性 /chosen/bootloader

以下属性特定于 BCM2711 和 BCM2712 SPI EEPROM 引导加载程序。除非另有说明，否则每个属性都存储为 32 位整数。

`build_timestamp`

　　EEPROM 引导加载程序的 UTC 构建时间。

`capabilities` 

　　这个位字段描述了当前引导加载程序支持的功能。这可以用来在引导加载程序 EEPROM 配置中启用功能（例如 USB 启动）之前检查是否支持。

| 位 | 功能                                     |
| :----: | :------------------------------------------: |
| 0  | 使用 VLI USB 主机控制器进行 [USB 引导](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#usb-mass-storage-boot)     |
| 1  | [ 网络引导](https://www.raspberrypi.com/documentation/computers/remote-access.html#network-boot-your-raspberry-pi)                                         |
| 2  | [TRYBOOT_A_B](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#fail-safe-os-updates-tryboot) 模式                         |
| 3  | [TRYBOOT](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#fail-safe-os-updates-tryboot)                                         |
| 4  | 使用 BCM2711 USB 主机控制器进行 [USB 引导](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#usb-mass-storage-boot) |
| 5  | [RAM 磁盘 - boot.img](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#boot_ramdisk)                                         |
| 6  | [ NVMe 引导](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#nvme-ssd-boot)                                         |
| 7  | [ 安全启动](https://github.com/raspberrypi/usbboot/blob/master/Readme.md#secure-boot)                                         |

`update_timestamp` 

　　由 `rpi-eeprom-update` 设置的 UTC 更新时间戳。

`signed` 

　　如果启用了安全启动，则此位字段将为非 0。各个位指示当前的安全启动配置。

| 位    | 说明                                            |
| :-------: | ------------------------------------------------- |
| 0     | `SIGNED_BOOT` 已在 EEPROM 配置文件中定义。  |
| 1     | 保留                                            |
| 2     | ROM 开发密钥已被吊销。请参阅 [revoke_devkey](https://www.raspberrypi.com/documentation/computers/config_txt.html#revoke_devkey)。 |
| 3     | 客户公钥摘要已写入 OTP。请参阅 [program_pubkey](https://www.raspberrypi.com/documentation/computers/config_txt.html#program_pubkey)。|
| 4…31 | 保留                                            |

`version` 

  （**字符串**）用于引导加载程序的 Git 版本字符串。

#### BCM2711 和 BCM2712 USB 引导属性 `/chosen/bootloader/usb`

如果系统是从 USB 引导的，则定义以下属性。这些属性可用于唯一标识 USB 引导设备。每个属性存储为 32 位整数。

`usb-version`

　　USB 主协议版本（2 或 3）。

`route-string`

　　由 USB 3.0 规范定义的设备的 USB 路由字符串标识符。

`root-hub-port-number` 

　　引导设备连接到的根集线器端口号 - 可能通过其他 USB 集线器连接。

`lun` 

　　用于大容量存储设备的逻辑单元号。

#### NVMEM 节点

固件通过 NVMEM 子系统提供引导加载程序 EEPROM 部分的只读内存映射。

每个区域在 `/sys/bus/nvmem/devices/` 下显示为一个 NVMEM 设备，在 `/sys/firmware/devicetree/base/aliases` 下显示为一个命名别名。

从 [rpi-eeprom-update](https://github.com/raspberrypi/rpi-eeprom/blob/master/rpi-eeprom-update) 读取 NVMEM 模式的示例 shell 脚本代码。

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

`blconfig`

　　别名，指向存储引导加载程序 EEPROM 配置文件副本的 NVMEM 设备。

`blpubkey` 

　　别名，指向以二进制格式存储引导加载程序 EEPROM 公钥副本（如果已定义）的 NVMEM 设备。可以使用 [rpi-bootloader-key-convert](https://github.com/raspberrypi/usbboot/blob/master/tools/rpi-bootloader-key-convert) 工具将数据转换为 PEM 格式，以便与 OpenSSL 一起使用。

有关更多信息，请参阅[安全启动](https://github.com/raspberrypi/usbboot#secure-boot)。

### 故障排除

#### 调试

加载程序将跳过缺少的叠加层和错误参数，但如果存在严重错误，比如缺少或损坏的基本 DTB 或失败的叠加层合并，那么加载程序将退回到非 DT 引导。如果发生这种情况，或者如果你的设置不符合你的期望，值得检查加载程序的警告或错误：

```
$ sudo vclog --msg
```

通过将 `dtdebug=1` 添加到 `config.txt` 可以启用额外的调试。

你可以这样创建当前 DT 状态，以人类可读的形式表示：

```
$ dtc -I fs /proc/device-tree
```

这对于查看将叠加层合并到基础树上的效果可能很有用。

如果内核模块未按预期加载，请检查它们是否在 `/etc/modprobe.d/raspi-blacklist.conf` 中被列入黑名单；在使用设备树时，不应该需要列入黑名单。如果没有发现任何异常，你还可以通过在 `/lib/modules/<version>/modules.alias` 中搜索 `compatible` 值来检查模块是否导出了正确的别名。否则，你的驱动程序可能缺少以下内容之一：

```
.of_match_table = xxx_of_match,
```

 要么：

```
MODULE_DEVICE_TABLE(of, xxx_of_match);
```

如果失败，那么因为 `depmod` 失败，或者更新的模块尚未安装在目标文件系统上。

#### 使用 dtmerge、dtdiff 和 ovmerge 测试叠加层。

除了命令 `dtoverlay` 和 `dtparam` 之外，还有一个用于将叠加层应用到 DTB 的工具 - `dtmerge`。要使用它，你首先需要获取基本的 DTB，可以通过以下两种方式之一获取：

从 `/proc/device-tree` 中的实时 DT 状态生成它：

```
$ dtc -I fs -O dtb -o base.dtb /proc/device-tree
```

这将包括你迄今为止在 `config.txt` 中应用的任何叠加层和参数，或者通过在运行时加载它们，这可能是你想要的，也可能不是。或者：

从 `/boot/firmware/` 中的源 DTB 复制它。这不会包括叠加层和参数，但也不会包括固件的任何其他修改。为了允许测试所有叠加层，`dtmerge` 工具将创建一些特定于板的别名（"i2c_arm" 等），但这意味着合并的结果将与原始 DTB 有更多差异。你可能期望的不同。解决此问题的方法是使用 dtmerge 进行复制：

```
$ dtmerge /boot/firmware/bcm2710-rpi-3-b.dtb base.dtb -
```

( - 表示不存在的叠加层名称)。

你现在可以尝试应用叠加层或参数：

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

你还可以比较不同的叠加层或参数。

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

[Utils](https://github.com/raspberrypi/utils) 存储库包含了另一个 DT 工具 - `ovmerge`。与 `dtmerge` 不同，`ovmerge` 结合了文件并以源形式应用叠加层。由于叠加层从未被编译，标签得以保留，结果通常更易读。它还具有许多其他技巧，例如能够列出文件包含的顺序。

#### 强制使用特定的设备树

如果你有非常特定的需求，而默认的 DTB 不能满足他们，或者你只是想尝试编写自己的 DT，请让加载程序加载指定的 DTB 文件，就像这样：

```
device_tree=my-pi.dtb
```

#### 禁用设备树使用

树莓派的 Linux 内核需要使用设备树。对于裸机和其他操作系统，可以通过添加以下内容来禁用设备树加载：

```
device_tree=
```

到 `config.txt`。

#### 快捷方式和语法变体

加载程序使用的一些快捷方式：

```
dtparam=i2c_arm=on
dtparam=i2s=on
```

可以简写成：

```
dtparam=i2c,i2s
```

（ `i2c` 是 `i2c_arm` 的别名，`=on` 为默认）。它仍然接受长形式版本： `device_tree_overlay` 和 `device_tree_param`。

#### `config.txt` 中可用的其他 DT 命令

`device_tree_address` 

　　这用于覆盖固件加载设备树的地址（不是 dt-blob）。默认情况下，固件将选择一个合适的位置。

`device_tree_end` 

　　这将对加载的设备树设置（独占）限制。默认情况下，设备树可以增长到可用内存的末尾，这几乎肯定是所需的。

`dtdebug` 

　　如果非 0，则打开固件的设备树处理的一些额外日志记录。

`enable_uart` 

　　启用主/控制台 [UART](https://www.raspberrypi.com/documentation/computers/configuration.html#configure-uarts)（在树莓派 3、4、400、Zero W 和 Zero 2 W 上为 ttyS0，在其他情况下为 ttyAMA0 - 除非与诸如 miniuart-bt 的叠加层交换）。如果主 UART 是 ttyAMA0，则 `enable_uart` 默认为 1（已启用），否则默认为 0（已禁用）。这是因为有必要阻止核心频率的变化，否则会使 ttyS0 无法使用，因此 `enable_uart=1` 意味着 `core_freq=250` （除非 `force_turbo=1`）。在某些情况下，这会影响性能，因此默认情况下关闭。

`overlay_prefix` 

　　指定要从中加载叠加层的子目录/前缀 - 默认为 "overlays/"。请注意末尾的“/”。如果需要，你可以在最后一个“/”后添加内容以向每个文件添加前缀，尽管这可能不是必要的。

可以用 DT 对端口进行进一步的控制。有关更多详细信息，请参阅[第 3 节](https://www.raspberrypi.com/documentation/computers/configuration.html#part3)。

#### 更多帮助

如果你在阅读本文档后，仍未找到解决设备树问题的答案，也能得到帮助。通常可在树莓派文档论坛找到答案，特别是[设备树](https://forums.raspberrypi.com/viewforum.php?f=107&_gl=1*ud7pvi*_ga*ODAwMTM3MTg4LjE3MTc1NzY1NTQ.*_ga_22FD70LWDS*MTcyMDk3NDM1MC4zNy4xLjE3MjA5NzU3MzQuMC4wLjA.)论坛。

## 修改默认引脚配置

>**注意**
>
>通过用户提供的DTB 自定义默认引脚配置的方法，已被弃用。

### 引导序列期间的设备引脚

在引导序列期间，GPIO 引脚经历各种操作。

* 上电 - 引脚默认为具有默认拉电阻的输入，这些电阻在[数据表](https://datasheets.raspberrypi.com/bcm2835/bcm2835-peripherals.pdf?_gl=1*ud7pvi*_ga*ODAwMTM3MTg4LjE3MTc1NzY1NTQ.*_ga_22FD70LWDS*MTcyMDk3NDM1MC4zNy4xLjE3MjA5NzU3MzQuMC4wLjA.)中有说明
* 由 bootrom 设置
* 通过 `bootcode.bin` 设置
* 通过 `dt-blob.bin` 设置（本页）
* 通过 [GPIO 命令](https://www.raspberrypi.com/documentation/computers/config_txt.html#gpio-control)在 `config.txt` 中设置
* 附加固件引脚（例如 UART）
* 内核/设备树

在软复位时，相同的过程适用，除了默认拉引脚，这些只在上电复位时应用。

通过过程可能需要几秒钟。在此期间，GPIO 引脚可能不处于附加外围设备期望的状态（如 `dt-blob.bin` 或 `config.txt` 中定义）。由于不同的 GPIO 引脚具有不同的默认拉电阻，你应该针对你的外围设备执行以下 **某个操作**：

* 选择一个在复位时默认为外围设备所需拉电阻的 GPIO 引脚
* 推迟外围设备的启动，直到操作完成
* 添加适当的上拉/下拉电阻

### 提供自定义DTB

为了将设备树源（ `.dts` ）文件编译成 DTB（ `.dtb`）文件，必须安装设备树编译器，方法是运行 `sudo apt install device-tree-compiler`。然后可以使用 `dtc` 命令如下：

```
$ sudo dtc -I dts -O dtb -o /boot/firmware/dt-blob.bin dt-blob.dts
```

同样，如有需要，可将 .dtb 文件转换回 .dts 文件。

```
$ dtc -I dtb -O dts -o dt-blob.dts /boot/firmware/dt-blob.bin
```

### `dt-blob` 的各个部分

`dt-blob.bin` 用于在启动时配置二进制区块（VideoCore）。Linux 内核目前不使用它。dt-blob 可以配置所有型号的树莓派，包括计算模块，以使用替代设置。dt-blob 中以下部分有效：

#### `videocore`

本部分包含所有 VideoCore blob 信息。所有后续部分必须被包含在此部分内。

#### `pins_*`

有许多单独的 `pins_*` 部分，基于特定的树莓派型号，即：

* `pins_rev1`：Rev1 引脚设置。由于移动的 I²C 引脚，存在一些差异。
* `pins_rev2`：Rev2 引脚设置。这包括 P5 上的附加编解码器引脚。
* `pins_bplus1`：树莓派 1B+ 修订版 1.1，包括完整的 40 针连接器。
* `pins_bplus2`：树莓派 1B+ 修订版 1.2，交换低功耗和 lan-run 引脚。
* `pins_aplus`：树莓派 1A+，无以太网。
* `pins_2b1`：树莓派 2B 修订版 1.0；通过 I²C0 控制开关电源管理系统。
* `pins_2b2`：树莓派 2B 修订版 1.1；通过软件 I²C 在 42 和 43 上控制开关电源管理系统。
* `pins_3b1`：树莓派 3B 修订版 1.0
* `pins_3b2`：树莓派 3B 修订版 1.2
* `pins_3bplus` ：树莓派 3B+
* `pins_3aplus` ：树莓派 3A+
* `pins_pi0` ：树莓派 Zero
* `pins_pi0w` ：树莓派 Zero W
* `pins_pi02w` ：树莓派 Zero 2 W
* `pins_cm` ：树莓派计算模块 1。默认情况下，这是芯片的默认设置，因此它是关于芯片上默认上拉/下拉的有用信息来源。
* `pins_cm3` ：树莓派计算模块 3
* `pins_cm3plus` ：树莓派计算模块 3+
* `pins_cm4s` ：树莓派计算模块 4S
* `pins_cm4` ：树莓派计算模块 4

每个 `pins_*` 部分都可以包含 `pin_config` 和 `pin_defines` 部分。

#### `pin_config`

`pin_config` 部分用于配置各个引脚。该部分中的每个项目必须是一个命名的引脚部分，例如 `pin@p32`，表示 GPIO32。还有一个特殊部分 `pin@default`，其中包含未在 pin_config 部分中明确命名的任何内容的默认设置。

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
* `drive_strength_mA`
　　驱动强度用于设置引脚的强度。请注意，你只能为该参数指定单个驱动强度。有效值为 `<8>`、`<16>`。

#### `pin_defines`

此部分用于将特定的 VideoCore 功能设置为特定的引脚。这使用户可以将摄像头电源使能引脚移动到其他位置，或将 HDMI 热插拔位置移动：这些是 Linux 无法控制的事情。请参考以下 DTS 示例文件。

### 时钟配置

通过这个界面可以修改时钟配置，哪怕结果很难预测！时钟系统的配置异常复杂。有 5 个独立的 PLL，每个 PLL 都有自己固定（或可变，如 PLLC）的 VCO 频率。然后，每个 VCO 都有许多不同的通道，可以使用不同的 VCO 频率分频。每个时钟目的地都可以配置为来自其中一个时钟通道，尽管源到目的地的映射受到限制，因此并非所有通道都可以路由到所有时钟目的地。

这里有一些示例配置，你可以用来修改特定的时钟。当请求时钟配置时，我们将添加到此资源。

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

以上内容将把 PLLA 设置为运行在 1.96608GHz 的源 VCO（此 VCO 的限制为 600MHz - 2.4GHz），将 APER 通道修改为/4，并配置 GPCLK0 从 PLLA 通过 APER 进行源控制。这用于为音频编解码器提供所需的 12288000Hz，以产生 48000 范围的频率。

### 设备树源文件实例

固件存储库包含一个[主 Raspberry Pi blob](https://github.com/raspberrypi/firmware/blob/master/extra/dt-blob.dts)，通常从中派生其他内容。


>**译者注**
>
>- ① 树莓派 GPU 显存来自内存。
>- ② 根据 IANA（互联网名称与数字地址分配机构）规范，中国标准时区（北京时间）使用的是 Asia/Shanghai（上海）而非北京。
