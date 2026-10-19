# 软件来源

在树莓派，我们尽可能多地开源代码，以便使用和适配你的用途。树莓派专门为我们的产品开发和维护软件，并将精力集中在能提供最佳用户体验的软件上。例如，优化多媒体加速的驱动，如 3D、HEVC 解码、摄像头成像流水线、AI 加速、双 HDMI 和音频。

## 在树莓派系统中查找软件源代码

在查找随树莓派系统分发的软件时，通常存在上游软件源，我们对其打补丁以创建下游软件包（带有 `+rpt` 标签的软件包）。要查看这些软件包的源代码，通过 apt 获取通常更方便。为此，你首先需要编辑 apt 列表以包含源代码包。编辑以下文件，将每个“Types: deb”行改为“Types: deb deb-src”：

* `/etc/apt/sources.list.d/debian.sources`（在 64 位镜像上）
或
* `/etc/apt/sources.list.d/raspbian.sources`（在 32 位镜像上）
以及
* `/etc/apt/sources.list.d/raspi.sources`

接下来必须更新软件包列表：

```sh
$ sudo apt update
```

现在你可以获取软件包源代码，例如：

```sh
$ apt source labwc
```

接下来，你需要安装一个辅助软件包：

```sh
$ sudo apt install devscripts
```

最后，你可以使用标准的 Debian 构建流程构建软件包：

```sh
$ sudo apt build-dep labwc
$ cd labwc-0.8.4
$ debuild -uc -us
```

## 我们的 GitHub 组织

你还可以在 GitHub 仓库中以更标准的形式找到我们的软件；我们使用三个 GitHub 组织发布源代码：

* <https://github.com/raspberrypi>
* <https://github.com/raspberrypi-ui>
* <https://github.com/RPi-Distro>

我们还在以下组织发布与我们的图书和杂志相关的内容：

* <https://github.com/raspberrypipress>
* <https://github.com/themagpimag>

## 分类源代码列表

以下是大多数人感兴趣的精编仓库列表：

### 主要源代码

**[raspberrypi/linux](https://github.com/raspberrypi/linux)**：此仓库包含下游 Linux 内核的源代码，支持并运行于树莓派 1 到 5 的所有版本。

**[raspberrypi/firmware](https://github.com/raspberrypi/firmware)**：此仓库包含闭源固件，不过以下两个链接很有用：

* [固件的变更日志](https://github.com/raspberrypi/firmware/commits/master/)
* [设备树覆盖层 README](https://github.com/raspberrypi/firmware/blob/master/boot/overlays/README)

**[raspberrypi/rpi-eeprom](https://github.com/raspberrypi/rpi-eeprom)**：树莓派 4 和树莓派 5 引导加载程序 EEPROM 的安装脚本和二进制文件，包括[发布版本](https://github.com/raspberrypi/rpi-eeprom/releases)和[发行说明](https://github.com/raspberrypi/rpi-eeprom/blob/master/releases.md)。

### 库和应用程序

**[raspberrypi/utils](https://github.com/raspberrypi/utils)**：实用工具集合，如 pinctrl、piolib 和 raspinfo，以及 gpiolib——树莓派支持的直接访问 GPIO 引脚的方法。

**[raspberrypi/libcamera](https://github.com/raspberrypi/libcamera)**：用于控制树莓派设备 ISP 和摄像头的 libcamera 库实现。

**[raspberrypi/rpicam-apps](https://github.com/raspberrypi/rpicam-apps)**：使用 libcamera 通过树莓派摄像头进行图像/视频处理和编码的 C++ 库与应用程序套件。

**[raspberrypi/picamera2](https://github.com/raspberrypi/picamera2)**：用于使用和控制树莓派摄像头的 Python 库。

**[raspberrypi/drmu](https://github.com/raspberrypi/drmu)**：用于直接控制和访问多媒体接口的库。

### 桌面

**[raspberrypi-ui/rpd-metas](https://github.com/raspberrypi-ui/rpd-metas)**：用于创建桌面的元软件包。

**[raspberrypi-ui/wf-panel-pi](https://github.com/raspberrypi-ui/wf-panel-pi)**：运行基于 Wayland 的桌面时显示在屏幕上的任务栏或程序坞。

**[raspberrypi-ui/lxpanel-pi](https://github.com/raspberrypi-ui/lxpanel-pi)**：运行旧版基于 X 的桌面时显示在屏幕上方的任务栏。

以下组件显示在任务栏上：

* [pplug-batt](https://github.com/raspberrypi-ui/pplug-batt)
* [pplug-bluetooth](https://github.com/raspberrypi-ui/pplug-bluetooth)
* [pplug-clock](https://github.com/raspberrypi-ui/pplug-clock)
* [pplug-cpu](https://github.com/raspberrypi-ui/pplug-cpu)
* [pplug-cputemp](https://github.com/raspberrypi-ui/pplug-cputemp)
* [pplug-ejecter](https://github.com/raspberrypi-ui/pplug-ejecter)
* [pplug-gpu](https://github.com/raspberrypi-ui/pplug-gpu)
* [pplug-menu](https://github.com/raspberrypi-ui/pplug-menu)
* [pplug-netman](https://github.com/raspberrypi-ui/pplug-netman)
* [pplug-power](https://github.com/raspberrypi-ui/pplug-power)
* [pplug-updater](https://github.com/raspberrypi-ui/pplug-updater)
* [pplug-volumepulse](https://github.com/raspberrypi-ui/pplug-volumepulse)

**[raspberrypi-ui/pcmanfm](https://github.com/raspberrypi-ui/pcmanfm)** 和 **[raspberrypi-ui/libfm](https://github.com/raspberrypi-ui/libfm)**：桌面使用的文件管理器，它还负责显示桌面背景。

**[raspberrypi-ui/rpcc](https://github.com/raspberrypi-ui/rpcc)**：控制中心应用程序。

**[raspberrypi-ui/rc_gui](https://github.com/raspberrypi-ui/rc_gui)**：控制中心的树莓派配置插件。

**[raspberrypi-ui/appset](https://github.com/raspberrypi-ui/appset)**：控制中心的外观设置插件。

**[raspberrypi-ui/rasputin](https://github.com/raspberrypi-ui/rasputin)**：控制中心的鼠标和键盘设置插件。

**[raspberrypi-ui/raindrop](https://github.com/raspberrypi-ui/raindrop)**：控制中心的屏幕配置插件。

**[raspberrypi-ui/rpinters](https://github.com/raspberrypi-ui/rpinters)**：控制中心的打印机设置插件。

### 应用程序

**[raspberrypi-ui/agnostics](https://github.com/raspberrypi-ui/agnostics)**：用于检查 SD 卡的诊断应用程序。

**[raspberrypi-ui/bookshelf](https://github.com/raspberrypi-ui/bookshelf)**：Bookshelf 应用程序的代码，可让你下载和阅读电子书以及《树莓派官方杂志》的过期期刊。

**[raspberrypi-ui/piclone](https://github.com/raspberrypi-ui/piclone)**：SD 卡复制器应用程序，可克隆卡和驱动器。

**[raspberrypi-ui/rp-prefapps](https://github.com/raspberrypi-ui/rp-prefapps)**：推荐软件应用程序，可安装或移除选定的程序。

### 调试

**[raspberrypi/rpi-analyse-boot](https://github.com/raspberrypi/rpi-analyse-boot)**：启动分析服务，从各种不同来源收集启动耗时指标。

### 工具

**[raspberrypi/rpi-imager](https://github.com/raspberrypi/rpi-imager)**：树莓派启动盘制作工具应用程序的代码，用于将操作系统刷写到 SD 卡。

**[raspberrypi/rpi-image-gen](https://github.com/raspberrypi/rpi-image-gen)**：用于为嵌入式树莓派系统开发操作系统的构建系统。

**[raspberrypi/usbboot](https://github.com/raspberrypi/usbboot)**：通过 USB 启动树莓派以配置计算模块和树莓派设备的工具。

**[raspberrypi/rpi-sb-provisioner](https://github.com/raspberrypi/rpi-sb-provisioner)**：大规模配置树莓派设备的工具，包括安全启动和加密文件系统。（支持树莓派 5、计算模块 4 和计算模块 5。）

### 反馈

**[raspberrypi/trixie-feedback](https://github.com/raspberrypi/trixie-feedback)**：专门用于当前树莓派系统版本问题反馈的仓库。

### 树莓派 Pico

**[Microsoft Visual Studio Code 的树莓派 Pico 扩展](https://marketplace.visualstudio.com/items?itemName=raspberry-pi.raspberry-pi-pico)**：可在此下载并安装树莓派 Pico SDK 的 VS Code 扩展。

**[raspberrypi/pico-setup](https://github.com/raspberrypi/pico-setup)**：用于命令行使用的树莓派 Pico SDK 快速安装工具。

**[raspberrypi/pico-sdk](https://github.com/raspberrypi/pico-sdk)**：树莓派 Pico SDK 源代码。

**[raspberrypi/debugprobe](https://github.com/raspberrypi/debugprobe)**：树莓派调试套件的源代码，可轻松提供 SWD 和 UART。

**[raspberrypi/openocd](https://github.com/raspberrypi/openocd)**：树莓派下游 OpenOCD 源代码。

**[raspberrypi/pico-examples](https://github.com/raspberrypi/pico-examples)**：树莓派 Pico 示例。

**[raspberrypi/picotool](https://github.com/raspberrypi/picotool)**：用于在 BOOTSEL 模式下与 RP 系列设备交互的工具。
