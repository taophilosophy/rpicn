# config.txt

## 什么是 config.txt ？

>**注意**
>
>在 Bookworm 之前，Raspberry Pi OS 将引导分区存储在 /boot/。自从 Bookworm 以来，引导分区位于 /boot/firmware/。 

树莓派使用一个配置文件，而不是您在传统 PC 上期望找到的 BIOS。在传统上会使用 BIOS 对系统配置参数进行编辑和存储，而现在存储在一个名为 config.txt 的可选文本文件中。这个文件在 ARM CPU 和 Linux 初始化之前由 GPU 读取。因此，它必须位于 SD 卡的第一个（引导）分区上，与 bootcode.bin 和 start.elf 一起。这个文件通常在 Linux 中作为 /boot/firmware/config.txt 访问，并且必须作为 root 用户进行编辑。在 Windows 或 OS X 中，它显示为卡片上唯一可访问部分中的一个文件。如果您需要应用下面的一些配置设置，但是您的引导分区上还没有 config.txt ，请将其创建为一个新的文本文件。

任何更改只有在重启树莓派后才会生效。Linux 启动后，您可以使用以下命令查看当前的活动设置：

* `vcgencmd get_config <config>` ：显示特定的配置值，例如 vcgencmd get_config arm_freq
* vcgencmd get_config int ：列出所有已设置的整数配置选项（非零）
* vcgencmd get_config str ：列出所有已设置的字符串配置选项（非空）

>**注意**
>
>有一些配置设置无法使用 vcgencmd 查看。

### 文件格式

config.txt 文件由早期引导固件读取，因此它具有非常简单的文件格式。格式是每行一个 property=value 语句，其中 value 可以是整数或字符串。可以添加注释，或通过以 # 字符开头的行来注释和禁用现有配置值。

条目的行长度限制为 98 个字符-超过此限制的任何字符都将被忽略。

这是一个示例文件：

```
# Enable audio (loads snd_bcm2835)
dtparam=audio=on

# Automatically load overlays for detected cameras
camera_auto_detect=1

# Automatically load overlays for detected DSI displays
display_auto_detect=1

# Enable DRM VC4 V3D driver
dtoverlay=vc4-kms-v3d
```

### 高级功能

#### `include`

导致将指定文件的内容插入到当前文件中。

例如，将行 include extraconfig.txt 添加到 config.txt 将在 config.txt 文件中包含 extraconfig.txt 文件的内容。

>**注意**
>
>引用指令不受 bootcode.bin 或 EEPROM 引导加载程序支持。<br /><br /> 由引导加载程序处理的设置只有在 config.txt 中指定（而不是任何其他包含的文件）时才会生效：<br />*`bootcode_delay`,*`gpu_mem`, `gpu_mem_256`, `gpu_mem_512`, `gpu_mem_1024`,*`total_mem`,*`sdram_freq`,*`start_x`, `start_debug`, `start_file`, `fixup_file`,*`uart_2ndstage`. 

#### 条件过滤

条件过滤器在条件部分中有详细介绍。

## `autoboot.txt`

autoboot.txt 是一个可选的配置文件，可用于指定 boot_partition 编号。

这也可以与 tryboot 功能一起使用，实现用于 OS 升级的 A/B 引导。

autoboot.txt 限制为 512 字节，并支持 [all] ， [none] 和 [tryboot] 条件过滤器。

查看 TRYBOOT 引导流程。

### `boot_partition`

指定用于引导的分区号，除非分区号已作为 reboot 命令的参数指定（例如 sudo reboot 2 ）。

分区号从 1 开始，MBR 分区为 1 到 4 。指定分区 0 意味着从 default 分区引导，该分区是第一个可引导的 FAT 分区。

可引导的分区必须格式化为 FAT12、FAT16 或 FAT32，并包含一个 start.elf 文件（或者在树莓派 5 上包含一个 config.txt 文件），以便被引导加载程序分类为可引导。

### [tryboot] 过滤器

如果系统是使用 tryboot 参数引导的，则此过滤器通过。

```
sudo reboot "0 tryboot"
```

### `tryboot_a_b`

将此属性设置为 1 ，以便在设置 tryboot 标志时加载普通 config.txt 和 boot.img 文件，而不是 tryboot.txt 和 tryboot.img 。

这使得可以在分区级别而不是文件级别上进行 tryboot 开关，而无需修改 A/B 分区中的配置文件。

### A/B 启动的示例更新流程

以下伪代码显示了一个假设的操作系统 Update service 如何使用 tryboot + autoboot.txt 执行安全的操作系统升级。

 初始 autoboot.txt

```
[all]
tryboot_a_b=1
boot_partition=2
[tryboot]
boot_partition=3
```

** 安装更新**

* 系统已启动并默认引导到分区 2
* 一个 Update service 将下一个 OS 版本下载到分区 3
* 通过重新启动到 tryboot 模式 reboot "0 tryboot" 来测试更新，其中 0 表示默认分区

**提交或取消更新**

* 系统从分区 3 启动，因为 `[tryboot]` 过滤器在 tryboot mode 中评估为 true
* 如果 tryboot 处于活动状态（ /proc/device-tree/chosen/bootloader/tryboot == 1 ）
  * 如果当前的引导分区 ( /proc/device-tree/chosen/bootloader/partition ) 与 autoboot.txt 的 `[tryboot]` 部分中的 boot_partition 匹配
    * Update Service 验证系统以验证更新是否成功
    * 如果更新成功
      * 替换 autoboot.txt 交换 boot_partition 配置
      * 正常重启 - 分区 3 现在是默认启动分区
    * 其他
      * Update Service 标记更新失败，例如删除更新文件。
      * 正常重启 - 分区 2 仍然是默认引导分区，因为 tryboot 标志会自动清除。
    * 结束如果
  * 结束 如果
* 结束 如果

 更新 autoboot.txt

```
[all]
tryboot_a_b=1
boot_partition=3
[tryboot]
boot_partition=2
```

>**注意**
>
>更新 autoboot.txt 后不必重新启动。但是，Update Service 必须小心，以避免覆盖当前分区，因为 autoboot.txt 已经被修改以提交最后的更新。另请参阅：设备树参数。 

## 常见选项

### 常见显示选项

#### hdmi_enable_4kp60 （仅适用于树莓派 4）

默认情况下，连接到 4K 显示器时，树莓派 4B、400 和 CM4 将选择 30Hz 的刷新率。使用该参数可允许选择 60Hz 的刷新率。

>**重要**
>
>您树莓派 4 上的两个 micro HDMI 端口无法做到同时输出 4Kp60。 


>**警告**
>
>设置 hdmi_enable_4kp60 将增加树莓派的功耗和温度。 

### 常见硬件配置选项

#### `camera_auto_detect`

启用此设置（在 Raspberry Pi OS 中默认启用），固件将自动为其识别的 CSI 摄像头加载叠加层。设置 camera_auto_detect=0 可禁用该设置。

#### `display_auto_detect`

启用此设置（在 Raspberry Pi OS 中默认启用），固件将自动加载识别的 DSI 显示器的叠加层。将 display_auto_detect=0 可设置禁用。

#### `dtoverlay`

dtoverlay 选项请求固件加载一个命名的设备树叠加层 - 一个可以启用内置和外部硬件内核支持的配置文件。例如， dtoverlay=vc4-kms-v3d 加载一个启用内核图形驱动程序的叠加层。

作为特例，如果不带任何值调用 - dtoverlay= - 该选项标记着叠加参数列表的结束。如果在任何其他 dtoverlay 或 dtparam 设置之前使用，它会阻止加载任何 HAT 叠加层。

有关更多详细信息，请参阅 DTBs、叠加和 config.txt。

#### `dtparam`

树莓派设备树配置文件支持许多参数，例如启用 I2C 和 SPI 接口。许多 DT 叠加可以通过参数的使用进行配置。这两种类型的参数都可以使用 dtparam 设置提供。此外，叠加参数可以附加到 dtoverlay 选项上，用逗号分隔，但请记住 98 个字符的行长度限制。

有关更多详细信息，请参阅 DTBs、叠加和 config.txt。

#### arm_boost （仅适用于树莓派 4）

所有树莓派 400 和更新版本的树莓派 4B 都配备有第二个开关模式电源，用于 SoC 电压轨，这使得默认的 turbo 模式时钟可以从 1.5GHz 增加到 1.8GHz。此更改在 Raspberry Pi OS 中默认启用。将 arm_boost=0 设置为禁用。

#### power_force_3v3_pwm （仅适用于树莓派 5）

使用 3V3 电源时强制 PWM。将 power_force_3v3_pwm=0 设置为禁用。

## 机载模拟音频（3.5 毫米插孔）

机载音频输出使用配置选项来改变模拟音频驱动方式，以及是否启用一些固件功能。

### `audio_pwm_mode`

audio_pwm_mode=1 从 3.5 毫米 AV 插孔选择传统的低质量模拟音频。

audio_pwm_mode=2 （默认）使用先进的调制方案选择高质量模拟音频。

>**注意**
>
>此选项使用更多 GPU 计算资源，可能会干扰某些型号上的某些用例。 

### `disable_audio_dither`

默认情况下，如果音频流被路由到模拟音频输出，则会应用 1.0LSB 抖动。在某些情况下，例如当 ALSA 音量设置为低水平时，这可能会产生可听见的背景噪音。将 disable_audio_dither 设置为 1 以禁用抖动应用。

### `enable_audio_dither`

当音频样本大于 16 位时，通常会禁用音频抖动（请参阅上面的 disable_audio_dither）。将此选项设置为 1 以强制对所有位深度使用抖动。

### `pwm_sample_bits`

pwm_sample_bits 命令调整模拟音频输出的位深度。默认位深度为 11 。选择低于 8 的位深度将导致音频无法正常工作，因为低于 8 的设置会导致 PLL 频率过低而无法支持。这通常只用作演示位深度如何影响量化噪声。

## HDMI 音频

默认情况下，所有带 HDMI 输出的树莓派都启用了 HDMI 音频输出。

要禁用 HDMI 音频输出，请在 /boot/firmware/config.txt 的 dtoverlay=vc4-kms-v3d 行末尾添加 `,noaudio` ：

```
dtoverlay=vc4-kms-v3d,noaudio
```

## 引导选项

### `start_file`, `fixup_file`

这些选项指定在引导之前传输到 VideoCore GPU 的固件文件。

start_file 指定要使用的 VideoCore 固件文件。 fixup_file 指定用于修复与 GPU 内存分配匹配的内存位置的文件。

start_file 和 fixup_file 是一对匹配的组件 - 使用不匹配的文件将阻止板子启动。这是一个高级选项，因此我们建议您使用 start_x 和 start_debug 而不是这个选项。

>**注意**
>
>精简固件（ start*cd.elf 和 fixup*cd.dat ）无法通过这种方式选择 - 系统将无法启动。启用精简固件的唯一方法是指定 gpu_mem=16 。精简固件删除了对编解码器、3D 和调试日志的支持，并将初始的早期引导帧缓冲区限制为 1080p @16bpp - 尽管 KMS 可以在以后的阶段用高达 32bpp 的 4K 帧缓冲区替换这一点，就像任何固件一样。 

>**注意**
>
>树莓派 5 固件包含在引导加载程序 EEPROM 中。 

### `cmdline`

cmdline 是在引导分区上用于读取内核命令行字符串的替代文件名；默认值为 cmdline.txt 。

### `kernel`

kernel 是用于加载内核的引导分区上的替代文件名。在树莓派 1、Zero 和 Zero W 以及树莓派计算模块 1 上，默认值为 kernel.img 。在树莓派 2、3、3+ 和 Zero 2 W 以及树莓派计算模块 3 和 3+ 上，默认值为 kernel7.img 。在树莓派 4 和 400 以及树莓派计算模块 4 上，默认值为 kernel8.img（如 arm_64bit 设置为 0，则为 kernel7l.img ）。

树莓派 5 固件默认加载 kernel_2712.img ，因为该映像包含了针对树莓派 5 的优化（例如 16K 页大小）。如果不存在此文件，则将加载通用的 64 位内核（ kernel8.img ）。

### `arm_64bit`

如果设置为 1，则内核将以 64 位模式启动。将其设置为 0 会选择 32 位模式。

在 64 位模式下，固件将选择适当的内核（例如 kernel8.img ），除非定义了显式的 kernel 选项，此时将使用该选项。

在 Pi 4s（Pi 4B、Pi 400、CM4 和 CM4S）上默认为 1，在所有其他平台上默认为 0。但是，如果显式 kernel 选项中给定的名称与已知内核之一匹配，则 arm_64bit 将相应设置。

>**注意**
>
>64 位内核可以是未压缩的映像文件，也可以是 gzip 压缩的映像文件（仍然可以命名为 kernel8.img；引导加载程序将通过开头的签名字节识别压缩文件）。64 位内核仅适用于树莓派 3、3+、4、400、Zero 2 W 和 2B rev 1.2，以及树莓派计算模块 3、3+和 4。树莓派 5 仅支持 64 位内核，因此该参数已被移除。 

### `ramfsfile`

ramfsfile 是在 ramfs 的引导分区上加载的可选文件名。

>**注意**
>
>较新的固件支持加载多个 ramfs 文件。您应用逗号分隔多个文件名，注意不要超过 80 个字符的行长限制。所有加载的文件都会在内存中连接在一起，并被视为单个 ramfs blob。更多信息请参考论坛。

### `ramfsaddr`

ramfsaddr 是应加载到的内存地址。

### `initramfs`

initramfs 命令指定 ramfs 文件名和要加载到的内存地址。它在一个参数中执行 ramfsfile 和 ramfsaddr 的操作。地址也可以是 followkernel （或 0 ），将其放置在内核映像之后的内存中。示例值为： initramfs initramf.gz 0x00800000 或 initramfs init.gz followkernel 。与 ramfsfile 一样，更新的固件允许通过逗号分隔它们的名称加载多个文件。

>**注意**
>
>此选项使用与所有其他选项不同的语法，不应在此处使用 = 字符。

### `auto_initramfs`

如果 auto_initramfs 设置为 1 ，则按照与内核选择相同的规则查找 initramfs 文件。

### `disable_poe_fan`

默认情况下，启动时将在 I2C 总线上进行探测，即使未连接 PoE HAT 也会发生。将此选项设置为 1 会通过 I2C（在 ID_SD 和 ID_SC 引脚上）禁用对 PoE HAT 风扇的控制。如果您不打算使用 PoE HAT，则这是最小化启动时间的有用方式。

### `disable_splash`

如果 disable_splash 设置为 1 ，则启动时将不显示彩虹闪屏。默认值为 0 。

### `enable_uart`

enable_uart=1 （与 console=serial0 一起在 cmdline.txt 中）请求内核创建串行控制台，可使用 GPIO 14 和 15（40 针排针上的 8 和 10 引脚）。编辑 cmdline.txt 以删除 quiet 行，使内核的引导消息也显示在那里。另请参阅 uart_2ndstage 。

### `force_eeprom_read`

将此选项设置为 0 可防止固件在上电时尝试读取连接到 ID_SD 和 ID_SC 引脚的 I2C HAT EEPROM。另请参阅 disable_poe_fan 。

### `os_prefix`

os_prefix 是一个可选设置，允许您在同一卡上选择多个内核和设备树文件的版本。 os_prefix 中的任何值都会被添加到固件加载的任何操作系统文件的名称之前，其中“操作系统文件”被定义为内核、initramfs、cmdline.txt、.dtbs 和叠加。前缀通常是目录名称，但也可以是文件名的一部分，例如“test-”。因此，目录前缀必须包括结尾的 / 字符。

为了减少系统无法启动的几率，固件首先会测试提供的前缀值的可行性 - 除非新位置/名称中可以找到预期的内核和 .dtb，否则将忽略前缀（设置为“”）。这种可行性测试的特殊情况适用于叠加层，只有在存在 `${os_prefix}${overlay_prefix}README` 时，叠加层才会从 |${os_prefix}${overlay_prefix}` （默认值为 overlay_prefix 为“overlays/”）加载，否则将忽略 os_prefix 并将叠加层视为共享。

（固件在检查前缀时检查关键文件的存在而不是目录的原因有两个：前缀可能不是目录，并且并非所有引导方法都支持检查目录的存在。）

>**注意**
>
>任何用户指定的操作系统文件都可以通过使用绝对路径（相对于引导分区）绕过所有前缀 - 只需以 / 开头的文件路径，例如 kernel=/my_common_kernel.img 。 

请参见 overlay_prefix 和 upstream_kernel 。

### otg_mode （仅适用于树莓派 4）

USB On-The-Go（通常缩写为 OTG）是一项功能，允许使用适当的 OTG 电缆支持 USB 设备，将其配置为 USB 主机。在较旧的树莓派 上，单个 USB 2 控制器同时用于 USB 主机和设备模式。

树莓派 4B 和 树莓派 400（非 CM4 或 CM4IO）添加了一个高性能的 USB 3 控制器（通过 PCIe 连接）用于驱动主 USB 端口。传统的 USB 2 控制器仍然可用于 USB-C 电源连接器，用作设备（ otg_mode=0 ，默认）。

otg_mode=1 请求使用更强大的 XHCI USB 2 控制器作为 USB-C 连接器上的另一个主机控制器。

>**注意**
>
>由于 CM4 和 CM4IO 不包含外部 USB 3 控制器，Raspberry Pi OS 镜像在 CM4 上设置 otg_mode=1 可获得更好的性能。

### `overlay_prefix`

指定从中加载叠加层的子目录/前缀，默认为 overlays/ （请注意末尾的 / ）。如果与 os_prefix 结合使用，则 os_prefix 在 overlay_prefix 之前出现，即 dtoverlay=disable-bt 将尝试加载 `${os_prefix}${overlay_prefix}disable-bt.dtbo` 。

>**注意**
>
>除非存在 `${os_prefix}${overlay_prefix}README` ，否则叠加层将与主操作系统共享（即 os_prefix 将被忽略）。 

## GPIO 控制

### `gpio`

gpio 指令允许在引导时将 GPIO 引脚设置为特定模式和值，以前需要自定义 dt-blob.bin 文件。每行将相同的设置应用于一组引脚（或至少对一组引脚进行相同的更改），可以是单个引脚（ 3 ），引脚范围（ 3-4 ）或逗号分隔的列表（ 3-4,6,8 ）。引脚集之后是一个 = 和来自此列表的一个或多个逗号分隔的属性：

* ip - 输入
* op - 输出
* `a0-a5` - Alt0-Alt5
* dh - 高电平驱动（用于输出）
* dl - 低电平驱动（用于输出）
* pu - 上拉
* pd - 下拉
* pn/np - 无上拉

gpio 设置是按顺序应用的，因此后面出现的设置会覆盖先前出现的设置。

 例子：

```
# Select Alt2 for GPIO pins 0 to 27 (for DPI24)
gpio=0-27=a2

# Set GPIO12 to be an output set to 1
gpio=12=op,dh

# Change the pull on (input) pins 18 and 20
gpio=18,20=pu

# Make pins 17 to 21 inputs
gpio=17-21=ip
```

gpio 指令遵循 config.txt 中的"`[...]`"条件过滤器，因此可以根据型号、序列号和 EDID 使用不同的设置。

通过这种机制进行的 GPIO 更改不会直接影响内核。它们不会导致 GPIO 引脚导出到 sysfs 接口，并且可以被设备树中的 pinctrl 条目以及 pinctrl 等实用程序覆盖。

还要注意，应用电源和更改生效之间会有几秒钟的延迟 - 如果通过网络引导或从 USB 大容量存储设备引导，则延迟会更长。

## 超频选项

内核具有默认启用节能管理器的 CPUFreq 驱动程序，在安装 raspi-config 时默认切换到 ondemand。使用 ondemand 管理器，CPU 频率将随处理器负载变化。您可以通过 `*_min` 配置选项调整最小值，或者通过应用静态缩放管理器（powersave 或 performance）或 force_turbo=1 来禁用动态时钟调整。

当 SoC 达到 temp_limit （见下文）时，超频和超电压将在运行时禁用，默认值为 85°C，以降低 SoC 温度。使用树莓派 1 和树莓派 2 不太可能达到此限制，但在使用树莓派 3 及更新型号时更有可能。当检测到欠压情况时，也会禁用超频和超电压。

>**注意**
>
>有关频率管理和热控制的更多信息，请参阅相关部分。 

>**警告**
>
>将任何超频参数设置为非 raspi-config 使用的值可能会在 SoC 内设置一个永久位，从而可能检测到您的树莓派已被超频。设置超频位的具体情况是，如果 force_turbo 设置为 `1` ，且任何 `over_voltage_*` 选项设置为大于 `0` 的值。有关更多信息，请参阅有关 Turbo 模式的博文。 

### 超频

| 选项                                                                                                | 说明                                                                                                                                                                                                                                                                                                                                                                                         |
| ----------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| arm_freq                                                                                            | ARM CPU 的频率（MHz）。                                                                                                                                                                                                                                                                                                                                                                      |
| ARM 增强                                                                                            | 将 arm_freq 增加到板型和固件支持的最高频率。设置为 1 以启用。                                                                                                                                                                                                                                                                                                                                |
| GPU 频率                                                                                            | 将 core_freq 、 h264_freq 、 isp_freq 、 v3d_freq 和 hevc_freq 放在一起。                                                                                                                                                                                                                                                                                                                    |
| core_freq                                                                                           | GPU 处理器核心的频率，单位为 MHz。影响 CPU 性能，因为它驱动 L2 缓存和内存总线；L2 缓存仅适用于树莓派 Zero/树莓派 Zero W/树莓派 1；对于树莓派 2 和树莓派 3，SDRAM 也有一些好处。有关在树莓派 4 上使用的详细信息，请参阅下面的部分。                                                                                                                   |
| h264_freq                                                                                           | 硬件视频块的频率，以 MHz 为单位； gpu_freq 设置的个别覆盖。                                                                                                                                                                                                                                                                                                                                  |
| isp_freq                                                                                            | 图像传感器管线块的频率，单位为 MHz； gpu_freq 设置的个别覆盖。                                                                                                                                                                                                                                                                                                                               |
| v3d_freq                                                                                            | 3D 块的频率，单位为 MHz； gpu_freq 设置的个别覆盖。在树莓派 5 上，V3D 与 core_freq 、 isp_freq 和 hevc_freq 独立。                                                                                                                                                                                                                                                                    |
| 高效视频编解码器块的频率（MHz）；{{0}}设置的个别覆盖。仅适用于树莓派 4。                     | sdram 频率                                                                                                                                                                                                                                                                                                                                                                                   |
| sdram_freq                                                                                          | SDRAM 的频率（MHz）。不支持在树莓派 4 或更新版本上超频 SDRAM。                                                                                                                                                                                                                                                                                                                        |
| 过压                                                                                                | CPU/GPU 核心的最高电压限制。该值应在范围[-16,8]内，相当于范围[0.95V,1.55V]（树莓派 1 上为[0.8,1.4V]），步长为 0.025V。换句话说，指定-16 将给出 0.95V（树莓派 1 上为 0.8V）作为最大 CPU/GPU 核心电压，指定 8 将允许高达 1.55V（树莓派 1 上为 1.4V）。有关默认值，请参见下表。仅当指定 force_turbo=1 时才允许超过 6 的值：如果还设置了 over_voltage_* > 0 ，则会设置保修位。 |
| 内存过压                                                                                            | 设置 over_voltage_sdram_c ， over_voltage_sdram_i 和 over_voltage_sdram_p 一起。                                                                                                                                                                                                                                                                                                             |
| 内存过压_c                                                                                          | SDRAM 控制器电压调整。[-16,8] 相当于 [0.8V,1.4V]，步长为 0.025V。不支持树莓派 4 或更高版本设备。                                                                                                                                                                                                                                                                                      |
| over_voltage_sdram_i                                                                                | SDRAM I/O 电压调整。[-16,8] 相当于 [0.8V,1.4V]，步长为 0.025V。不支持树莓派 4 或更高版本设备。                                                                                                                                                                                                                                                                                        |
| SDRAM phy 电压调整。[-16,8]等同于[0.8V,1.4V]，步长为 0.025V。不支持树莓派 4 或更高版本设备。 | 强制高性能模式                                                                                                                                                                                                                                                                                                                                                                               |
| force_turbo                                                                                         | 即使 ARM 核心不忙时，也会强制使用 turbo 模式频率。如果 over_voltage_* 也设置了，启用此功能可能会设置保修位。                                                                                                                                                                                                                                                                                 |
| 初始 turbo                                                                                          | 从启动时启用给定秒数的 turbo 模式，或直到 cpufreq 设置频率。最大值为 60 。                                                                                                                                                                                                                                                                                                                   |
| arm_freq_min                                                                                        | 用于动态频率时钟的最小值 arm_freq 。请注意，将此值降低到默认值以下不会导致任何显著的节能，并且目前不受支持。                                                                                                                                                                                                                                                                                 |
| core_freq_min                                                                                       | 用于动态频率调节的最小值 core_freq 。                                                                                                                                                                                                                                                                                                                                                        |
| gpu_freq_min                                                                                        | 用于动态频率调节的最小值 gpu_freq 。                                                                                                                                                                                                                                                                                                                                                         |
| h264_freq_min                                                                                       | 用于动态频率调节的最小值 h264_freq 。                                                                                                                                                                                                                                                                                                                                                        |
| isp_freq_min                                                                                        | 用于动态频率时钟的最小值 isp_freq 。                                                                                                                                                                                                                                                                                                                                                         |
| v3d_freq_min                                                                                        | 用于动态频率时钟的最小值 v3d_freq 。                                                                                                                                                                                                                                                                                                                                                         |
| hevc_freq_min                                                                                       | 用于动态频率调节的最小值 hevc_freq 。                                                                                                                                                                                                                                                                                                                                                        |
| sdram_freq_min                                                                                      | 用于动态频率时钟的最小值 sdram_freq 。                                                                                                                                                                                                                                                                                                                                                       |
| over_voltage_min                                                                                    | 用于动态频率时钟的最小值 over_voltage 。该值应在[-16,8]范围内，相当于[0.8V,1.4V]范围，步长为 0.025V。换句话说，指定-16 将给出 0.8V 作为 CPU/GPU 核心空闲电压，指定 8 将给出最低 1.4V。此设置在树莓派 4 和树莓派 5 上已弃用。                                                                                                                                                   |
| 过压偏移                                                                                            | 在树莓派 4 和树莓派 5 上，over_voltage_delta 参数会将微伏数计算结果添加给定的偏移量。                                                                                                                                                                                                                                                                                          |
| 温度限制                                                                                            | 过热保护。当 SoC 达到摄氏度时，将时钟和电压设置为默认值。超过 85 的值将被限制为 85。                                                                                                                                                                                                                                                                                                         |
| temp_soft_limit                                                                                     | 仅适用于 3A+/3B+。CPU 速度节流控制。这将设置 CPU 时钟速度节流系统激活的温度。在此温度下，时钟速度从 1400MHz 降至 1200MHz。默认为 60 ，最高可提高至 70 ，但这可能会导致不稳定性。                                                                                                                                                                                                             |

该表列出了各种型号的树莓派上各选项的默认值，所有频率均以 MHz 表示。

| 选项           | Pi 0/W | 树莓派 1 | 树莓派 2 | 树莓派 3 | Pi3A+/Pi3B+ | CM4 和 Pi4B ⇐ R1.3 | Pi4B R1.4                           | 树莓派 400 | 树莓派 Zero 2 W | 树莓派 5 |
| ---------------- | -------- | ---------- | ---------- | ---------- | ------------- | --------------------- | ------------------------------------- | ------------ | ----------------- | ---------- |
| arm_freq       | 1000   | 700      | 900      | 1200     | 1400        | 1500                | 如果 arm_boost=1，则为 1500 或 1800 | 1800       | 1000            | 2400     |
| core_freq      | 400    | 250      | 250      | 400      | 400         | 500                 | 500                                 | 500        | 400             | 910      |
| h264 频率      | 300    | 250      | 250      | 400      | 400         | 500                 | 500                                 | 500        | 300             | 不适用   |
| isp 频率       | 300    | 250      | 250      | 400      | 400         | 500                 | 500                                 | 500        | 300             | 910      |
| v3d_freq       | 300    | 250      | 250      | 400      | 400         | 500                 | 500                                 | 500        | 300             | 910      |
| hevc_freq      | 不适用 | 不适用   | 不适用   | 不适用   | 不适用      | 500                 | 500                                 | 500        | 不适用          | 910      |
| sdram_freq     | 450    | 400      | 450      | 450      | 500         | 3200                | 3200                                | 3200       | 450             | 4267     |
| arm_freq_min   | 700    | 700      | 600      | 600      | 600         | 600                 | 600                                 | 600        | 600             | 1500     |
| core_freq_min  | 250    | 250      | 250      | 250      | 250         | 200                 | 200                                 | 200        | 250             | 500      |
| gpu_freq_min   | 250    | 250      | 250      | 250      | 250         | 250                 | 250                                 | 250        | 250             | 500      |
| h264_freq_min  | 250    | 250      | 250      | 250      | 250         | 250                 | 250                                 | 250        | 250             | 不适用   |
| isp_freq_min   | 250    | 250      | 250      | 250      | 250         | 250                 | 250                                 | 250        | 250             | 500      |
| v3d_freq_min   | 250    | 250      | 250      | 250      | 250         | 250                 | 250                                 | 250        | 250             | 500      |
| sdram_freq_min | 400    | 400      | 400      | 400      | 400         | 3200                | 3200                                | 3200       | 400             | 4267     |

此表提供了所有型号通用选项的默认值。

| 选项                 | 默认                                  |
| ---------------------- | --------------------------------------- |
| 初始_turbo           | 0（秒）                               |
| 温度限制             | 85（°C）                             |
| 过压                 | 0（1.35V，1.2V 在树莓派 1 上） |
| 过压最小值           | 0（1.2 伏特）                         |
| over_voltage_sdram   | 0（1.2 伏特）                         |
| 内存超压_c           | 0 (1.2V)                              |
| 内存超压_i           | 0（1.2 伏特）                         |
| over_voltage_sdram_p | 0（1.2 伏特）                         |

固件使用自适应电压调节（AVS）来确定在 over_voltage 和 over_voltage_min 定义的范围内的最佳 CPU/GPU 核电压。

#### 专为树莓派 4、树莓派 400 和 CM4 设计

当系统处于空闲状态时，最低核心频率必须足够快，以支持显示器的最高像素时钟（忽略空白）。因此，如果显示模式为 4Kp60，则 core_freq 将被提升至 500 MHz 以上。

| 显示选项          | 最大 core_freq |
| ------------------- | ---------------- |
| 默认              | 500            |
| hdmi_enable_4kp60 | 550            |

>**注意**
>
>树莓派 5 支持双 4Kp60 显示器，使用空闲时钟设置，因此 hdmi_enable_4kp60 是多余的。


* 超频需要最新的固件版本。
* 最新的固件在系统超频时会自动增加电压。手动设置 over_voltage 会禁用超频的自动电压调节。
* 推荐在超频时使用单独的频率设置（ isp_freq ， v3d_freq 等），而不是 gpu_freq ，因为 ISP、V3D、HEVC 等的最大稳定频率会有所不同。
* 树莓派 4 或更新设备上的 SDRAM 频率不可配置。

#### `force_turbo`

默认情况下（ force_turbo=0 ），按需 CPU 频率驱动程序会在 ARM 核心繁忙时将时钟提升到最大频率，并在 ARM 核心空闲时将其降低到最低频率。

force_turbo=1 覆盖了这种行为，即使 ARM 核心使用率不高，也会强制使用最大频率。

### 时钟关系

#### 树莓派 4

GPU 核心、CPU、SDRAM 和 GPU 每个都有自己的 PLL，并且可以具有不相关的频率。h264、v3d 和 ISP 块共享一个 PLL。

要查看树莓派当前的频率（以千赫为单位），请输入： cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_cur_freq 。将结果除以 1000 以找到以兆赫为单位的值。请注意，此频率是内核请求的频率，可能会出现任何节流（例如在高温下）可能意味着 CPU 实际运行速度比报告的更慢。可以使用 vcgencmd vcgencmd measure_clock arm 检索实际 ARM CPU 频率的瞬时测量。这显示为赫兹。

### 监控核心温度

##### [冷却树莓派设备](https://pip.raspberrypi.com/categories/685-whitepapers-app-notes/documents/RP-003608-WP/Cooling-a-Raspberry-Pi-device.pdf)

冷却树莓派设备

这份白皮书详细介绍了为什么您的树莓派可能会发热以及为什么您可能希望降温，提供了关于冷却过程的选项。

要查看树莓派的温度，请键入 cat /sys/class/thermal/thermal_zone0/temp 。将结果除以 1000 以找到摄氏度的值。或者，还有一个 vcgencmd， vcgencmd measure_temp ，可以直接查询 GPU 的温度。

达到温度限制对 SoC 不会造成伤害，但会导致 CPU 降频。散热片可以帮助控制核心温度，从而提高性能。如果树莓派安装在机箱内，这将特别有用。散热片上的空气流动将使散热更加有效。

当核心温度在 80°C 和 85°C 之间时，ARM 核心将被降频。如果温度超过 85°C，ARM 核心和 GPU 将被降频。

对于树莓派 3 Model B+，PCB 技术已经改变，以提供更好的散热和增加热量。此外，引入了软温度限制，旨在最大限度地延长设备在达到 85°C 硬限制之前的“冲刺”时间。当达到软限制时，时钟速度从 1.4GHz 降至 1.2GHz，并略微降低操作电压。这降低了温度增加的速度：我们以 1.4GHz 的短暂时期换取了 1.2GHz 的较长时期。默认情况下，软限制为 60°C。这可以通过 temp_soft_limit 设置中的 config.txt 进行更改。

### 监测电压

保持供电电压高于 4.8V 以确保可靠性能。请注意，一些 USB 充电器/电源的电压可能会降至 4.2V。这是因为它们通常设计用于给 3.7V 的锂聚合物电池充电，而不是为计算机提供 5V 的电压。

要监测树莓派的电源电压，您需要使用万用表在 GPIO 的 VCC 和 GND 引脚之间进行测量。更多信息请参阅文档中的电源部分。

如果电压降至 4.63V 以下（±5%），ARM 核心和 GPU 将被降频，并且会向内核日志添加指示低电压状态的消息。

树莓派 5 PMIC 集成了内置 ADC，可用于测量供电电压。要执行此操作，请运行 vcgencmd pmic_read_adc EXT5V_V

### 超频问题

大多数超频问题会立即出现，导致无法启动。如果出现这种情况，请在下次启动时按住 shift 键。这将临时禁用所有超频，使您能够成功启动，然后编辑您的设置。

## 条件过滤器

当 SD 卡（或卡片镜像）与树莓派和显示器一起使用时，很容易将 config.txt 设置为该特定组合所需的方式，并保持不变，只有在发生变化时才进行修改。

然而，如果一个树莓派在不同的显示器之间交换，或者如果 SD 卡（或存储卡镜像）在多个开发板之间交换，单一的设置可能不再足够。条件过滤器允许您定义配置文件的某些部分仅在特定情况下使用，允许单个 config.txt 在不同硬件读取时创建不同的配置。

### `[all]` 过滤器

`[all]` 过滤器是最基本的过滤器。它重置所有先前设置的过滤器，并允许下面列出的任何设置应用于所有硬件。通常最好在过滤设置组的末尾添加一个 `[all]` 过滤器，以避免意外组合过滤器（见下文）。

### 模型过滤器

条件模型过滤器根据以下表格应用。

| 过滤器 | 适用型号                                                                          |
| -------- | --------------------------------------------------------------------------------------- |
| `[pi1]`       | 1A 型号，1B 型号，1A+型号，1B+型号，计算模块 1                                        |
| `[pi2]`       | 2B 型号（基于 BCM2836 或 BCM2837）                                                    |
| `[pi3]`       | 3B 型号，3B+型号，3A+型号，计算模块 3，计算模块 3+                                    |
| `[pi3+]`       | 3A+型号，3B+型号（也识别 [pi3] 的内容）                                                 |
| `[pi4]`       | 4B 型号，Pi 400，计算模块 4，计算模块 4S                                              |
| `[pi5]`       | 树莓派 5                                                                              |
| `[pi400]`       | Pi 400（也识别 [pi4] 的内容）                                                           |
| `[cm4]`       | 计算模块 4（也识别 [pi4] 的内容）                                                       |
| `[cm4s]`       | 计算模块 4S（也识别 [pi4] 的内容）                                                      |
| `[pi0]`       | 零，零 W，零 2 W                                                                      |
| `[pi0w]`       | 零 W（也识别 [pi0] 的内容）                                                             |
| `[pi02]`       | 零 2 W（也识别 [pi0w] 和 [pi0] 的内容）                                                 |
| `[board-type=Type]`       | 通过 Type 号进行筛选 - 查看树莓派修订代码 例如 `[board-type=0x14]` 将匹配 CM4。 |

这些对于定义不同的 kernel 、 initramfs 和 cmdline 设置特别有用，因为树莓派 1 和树莓派 2 需要不同的内核。它们还可以用于定义不同的超频设置，因为树莓派 1 和树莓派 2 有不同的默认速度。例如，为每个定义单独的 initramfs 映像：

```
 [pi1]
 initramfs initrd.img-3.18.7+ followkernel
 [pi2]
 initramfs initrd.img-3.18.7-v7+ followkernel
 [all]
```

记得在最后使用 `[all]` 过滤器，这样任何后续设置不仅限于仅限于树莓派 2 硬件。

>**注意**
>
>一些型号的树莓派（Zero W、Zero 2 W、Model 3B+、Pi 400、计算模块 4 和计算模块 4S）可以查看多个滤波器的设置（如上表所列）。这意味着，如果您希望某个设置仅适用于（例如）Model 4B，而不希望将该设置应用于 Pi 400，则需要通过后续 `[pi400]` 部分中的替代设置来恢复 `[pi4]` 部分中的设置 - 此类部分的排序很重要。或者，您可以使用一个与不同硬件产品具有一对一映射的 `[board-type=0x11]` 滤波器。

### `[none]` 滤波器

`[none]` 滤波器会阻止后续的任何设置应用于任何硬件。虽然没有什么是您不能在没有 `[none]` 的情况下做的，但这可以是一种在 config.txt 中保留未使用设置组的有用方式，而无需注释掉每一行。

### `[tryboot]` 过滤器

如果设置了 tryboot 重启标志，则此过滤器成功。

旨在用于 autoboot.txt 中，以选择故障安全 OS 更新的不同 boot_partition 模式。

### `[EDID=*]` 过滤器

当在树莓派上使用单个 SD 卡在多个显示器之间切换时，并且空白配置不足以自动选择每个显示器所需的分辨率时，可以根据显示器的 EDID 名称选择特定设置。

要查看连接的显示器的 EDID 名称，您需要按照一些步骤进行操作。运行以下命令以查看您在树莓派上拥有哪些输出设备：

```
ls -1 /sys/class/drm/card?-HDMI-A-?/edid
```

在树莓派 4 上，这将打印类似于：

```
/sys/class/drm/card1-HDMI-A-1/edid
/sys/class/drm/card1-HDMI-A-2/edid
```

然后，您需要针对每个这些文件名运行 edid-decode ，例如：

```
edid-decode /sys/class/drm/card1-HDMI-A-1/edid
```

如果没有连接到特定输出设备的监视器，它会告诉您 EDID 为空；否则，它将为您提供有关您的监视器功能的大量信息。您需要查找指定 Manufacturer 和 Display Product Name 的行。然后，“EDID 名称” 是 `<Manufacturer>-<Display Product Name>` ，其中任一字符串中的空格都将替换为下划线。例如，如果您的 edid-decode 输出包括：

```
....
  Vendor & Product Identification:
    Manufacturer: DEL
....
    Display Product Name: 'DELL U2422H'
....
```

该显示器的 EDID 名称将是 DEL-DELL_U2422H 。

然后，您可以将其用作条件过滤器，指定仅当连接了此特定显示器时才适用的设置：

```
[EDID=DEL-DELL_U2422H]
cmdline=cmdline_U2422H.txt
[all]
```

这些设置仅在启动时应用。显示器必须在启动时连接，并且树莓派必须能够读取其 EDID 信息以找到正确的名称。在启动后将不同的显示器热插拔到树莓派上将不会选择不同的设置。

在树莓派 4 上，如果两个 HDMI 都在使用中，则将针对两个端口检查 EDID 过滤器，并将应用所有匹配条件过滤器的配置。

>**注意**
>
>在树莓派 5 上不提供此设置。


### 序列号过滤器

有时候设置应该只应用于单个特定的树莓派，即使您将 SD 卡更换到另一个树莓派。示例包括许可密钥和超频设置（尽管许可密钥已以不同方式支持 SD 卡更换）。您还可以使用此功能选择不同的显示设置，即使上面的 EDID 识别不可能，只要您不在树莓派之间更换显示器。例如，如果您的显示器没有提供可用的 EDID 名称，或者如果您正在使用复合输出（无法读取 EDID）。

要查看您树莓派的序列号，请运行以下命令：

```
cat /proc/cpuinfo
```

序列号将显示在输出底部附近的一个 16 位十六进制值。您树莓派的序列号是最后的八位十六进制数字。例如，如果您看到：

```
Serial          : 0000000012345678
```

序列号为 `12345678` 。

>**注意**
>
>在某些型号的树莓派上，前 8 个十六进制数字包含除 0 之外的值。即使在这种情况下，也只使用最后八个十六进制数字作为序列号。 

您可以定义仅适用于此特定树莓派的设置：

```
[0x12345678]
# settings here are applied only to the Raspberry Pi with this serial
[all]
# settings here are applied to all hardware
```

### GPIO 过滤器

您还可以根据 GPIO 的状态进行过滤。例如：

```
[gpio4=1]
# Settings here are applied if GPIO 4 is high

[gpio2=0]
# Settings here are applied if GPIO 2 is low

[all]
# settings here are applied to all hardware
```

### 结合条件过滤器

相同类型的过滤器会相互替换，所以 `[pi2]` 会覆盖 `[pi1]` ，因为两者不可能同时为真。

不同类型的过滤器可以通过依次列出它们来组合，例如：

```
 # settings here are applied to all hardware
 [EDID=VSC-TD2220]
 # settings here are applied only if monitor VSC-TD2220 is connected
 [pi2]
 # settings here are applied only if monitor VSC-TD2220 is connected *and* on a Raspberry Pi 2
 [all]
 # settings here are applied to all hardware
```

使用 `[all]` 过滤器重置所有先前的过滤器，避免意外地组合不同类型的过滤器。

## 内存选项

### `total_mem`

此参数可用于强制树莓派限制其内存容量：指定您希望树莓派使用的总 RAM 量（以 MB 为单位）。例如，要使 4GB 的树莓派 4B 表现得像 1GB 型号一样，请使用以下设置：

```
total_mem=1024
```

此值可设置为最小值 128MB 至开发板上安装的总内存的最大值之间。

## 许可密钥和编解码器选项

可通过购买绑定到您的树莓派 CPU 序列号的许可证来启用树莓派 3 和早期型号的上附加编解码器来硬件解码。

树莓派 4 已永久禁用了 MPEG2 和 VC1 的硬件解码器。这些编解码器无法启用，因此不需要硬件编解码器许可密钥。 MPEG2 和 VC1 文件的软件解码对于典型用例表现良好。

树莓派 5 具有 H.265（HEVC）硬件解码功能。此解码默认启用，因此也不需要硬件编解码器许可密钥。

### `decode_MPG2`

decode_MPG2 是用于允许硬件 MPEG-2 解码的许可密钥，例如 decode_MPG2=0x12345678 。

### `decode_WVC1`

decode_WVC1 是用于允许硬件 VC-1 解码的许可密钥，例如 decode_WVC1=0x12345678 。

如果您有多个树莓派并为每个树莓派都购买了编解码器许可证，您可以在单个 config.txt 中列出最多八个许可证密钥，例如 decode_MPG2=0x12345678,0xabcdabcd,0x87654321 。这使您可以在不必每次编辑 config.txt 的情况下在不同的树莓派之间交换相同的 SD 卡。

## 视频选项

### HDMI 模式

使用屏幕配置实用程序或 KMS 视频设置来控制 HDMI 设置。

#### 树莓派 4 和 5 的 HDMI 管道

为了支持双显示器和高达 4k60 的模式，树莓派 4 和 5 为每个时钟周期生成 2 个输出像素。

每个 HDMI 模式都有一个定时列表，控制所有关于同步脉冲持续时间的参数。这些通常是通过像素时钟定义的，然后是每个水平和垂直方向的活动像素数量，前廊，同步脉冲和后廊。

以每个时钟 2 个像素的速度运行意味着树莓派 4 和 5 不支持任何水平定时不可被 2 整除的定时。固件和 Linux 内核会过滤掉任何不符合此标准的模式。

CEA 和 DMT 标准中只有一个不兼容的模式：DMT 模式 81，1366x768 @ 60Hz。该模式具有水平同步和后廊定时的奇数值，以及宽度不可被 8 整除。

如果您的显示器具有此分辨率，树莓派 4 或 5 会自动降级到显示器广告的下一个模式，通常为 1280x720。

### 复合视频模式

所有型号的树莓派计算机上都可以找到复合视频输出：

| 型号              | 复合输出                |
| ------------------- | ------------------------- |
| 树莓派 1 A 和 B   | RCA 插孔                |
| 树莓派 Zero | 未焊接 TV 头部          |
| 树莓派 Zero 2 W   | 板的底部测试点          |
| 树莓派 5          | HDMI 插座旁的 J7 电路板 |
| 所有其他型号      | 3.5 毫米 AV 插孔        |

>**注意**
>
>树莓派 400 不支持复合视频输出。


#### `enable_tvout`

设置为 1 以启用复合视频输出，设置为 0 以禁用。在树莓派 4 和 5 上，只有在将其设置为 1 时才能使用复合输出，这也会禁用 HDMI 输出。树莓派 400 不支持复合输出。

| 型号           | 默认 |
| ---------------- | ------ |
| Pi 4，5 和 400 | 0    |
| 所有其他型号   | 1    |

除了树莓派 4 和 5 之外的所有型号，都需要禁用 HDMI 输出才能启用复合输出。 当未连接/检测到 HDMI 显示器时，HDMI 输出被禁用。 设置 enable_tvout=0 以防止在禁用 HDMI 时启用复合输出。

要启用复合输出，请在 /boot/firmware/config.txt 的末尾附加 `,composite` 到 dtoverlay=vc4-kms-v3d 这一行：

```
dtoverlay=vc4-kms-v3d,composite
```

默认情况下，这会输出复合 NTSC 视频。 要选择不同的模式，请在 /boot/firmware/cmdline.txt 的单行末尾附加以下内容：

```
vc4.tv_norm=<video_mode>
```

用以下值之一替换 `<video_mode>` 占位符：

* `NTSC`
* `NTSC-J`
* `NTSC-443`
* `PAL`
* `PAL-M`
* `PAL-N`
* `PAL60`
* `SECAM`

### 液晶显示屏和触摸屏

#### `ignore_lcd`

默认情况下，在 I2C 总线上检测到树莓派触摸显示屏时会使用它。 ignore_lcd=1 会跳过此检测阶段。这会阻止使用液晶显示屏。

#### `disable_touchscreen`

启用和禁用触摸屏。

disable_touchscreen=1 禁用官方树莓派触摸显示屏的触摸屏组件。

### 通用显示选项

#### `disable_fw_kms_setup`

默认情况下，固件会解析任何连接的 HDMI 显示器的 EDID，选择适当的视频模式，然后通过内核命令行上的设置将模式的分辨率和帧速率（以及超扫描参数）传递给 Linux 内核。在罕见情况下，固件可能会选择一个不在 EDID 中的模式，这可能与设备不兼容。使用 disable_fw_kms_setup=1 可以禁用传递视频模式参数，从而避免此问题。Linux 视频模式系统（KMS）会自行解析 EDID 并选择适当的模式。

>**注意**
>
>在树莓派 5 上，该参数默认为 1 。 

## 摄像头设置

### `disable_camera_led`

当将 disable_camera_led 设置为 1 时，录制视频或拍摄静态图片时防止红色相机 LED 灯亮起。这对于防止反射很有用，例如当相机面向窗户时。

### `awb_auto_is_greyworld`

当将 awb_auto_is_greyworld 设置为 1 时，允许不支持内部灰世界选项的库或应用程序使用 NoIR 相机捕获有效的图像和视频。它将自动 awb 模式切换为使用灰世界算法。这仅在需要 NoIR 相机时或高质量相机已移除红外滤光片时才需要。
