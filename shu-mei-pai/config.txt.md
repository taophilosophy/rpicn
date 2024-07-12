# config.txt

## 什么是 config.txt ?

 在 GitHub 上编辑此内容

树莓派设备使用一个名为 config.txt 的配置文件，而不是常规 PC 上的 BIOS。GPU 在 Arm CPU 和 Linux 初始化之前读取 config.txt。树莓派 OS 在引导分区中查找此文件，该分区位于 /boot/firmware/ 处。

| NOTE | 在树莓派 OS Bookworm 之前，树莓派 OS 将引导分区存储在 /boot/ 处。|
| ------ | ------------------------------------------------------------------- |

你可以直接从你的树莓派系统安装中编辑 config.txt。你还可以移除存储设备并从另一台计算机编辑启动分区中的文件，包括 config.txt。

对 config.txt 的更改只有在重启后才会生效。你可以使用以下命令查看当前活动设置：

vcgencmd get_config <config> 显示特定的配置数值，例如 vcgencmd get_config arm_freq

vcgencmd get_config int 列出所有非零整数配置选项（非零）

vcgencmd get_config str 列出所有非空字符串配置选项

| NOTE | 并非所有配置设置都可以使用 vcgencmd 进行检索。|
| ------ | ------------------------------------------------ |

### 文件格式

config.txt 文件由早期启动固件读取，因此使用非常简单的文件格式：每行一个 property=value 语句，其中 value 可以是整数或字符串。可以添加注释，或通过以 # 字符开头的行来注释掉和禁用现有配置值。

条目的最大长度为 98 个字符。树莓派操作系统会忽略超出此限制的任何字符。

这里是一个示例文件：

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

使指定文件的内容插入到当前文件中。

例如，添加行 include extraconfig.txt 到 config.txt 将在 config.txt 文件中包含 extraconfig.txt 文件的内容。

| NOTE | bootcode.bin 或 EEPROM 引导加载程序不支持 include 指令。<br /><br />只有在 config.txt 中指定（而不是任何其他包含文件中），由引导加载程序处理的设置才会生效：<br />\* `bootcode_delay`,\* `gpu_mem`, `gpu_mem_256`, `gpu_mem_512`, `gpu_mem_1024`,\* `total_mem`,\* `sdram_freq`,\* `start_x`, `start_debug`, `start_file`, `fixup_file`,\* `uart_2ndstage`. |
| ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

#### 条件过滤

条件过滤器包含在条件部分中。

## `autoboot.txt`

 在 GitHub 上编辑此内容

autoboot.txt 是一个可选的配置文件，可用于指定 boot_partition 数量。

这也可以与 tryboot 功能一起使用，实现用于 OS 升级的 A/B 引导。

autoboot.txt 限制为 512 字节，支持 [all]、[none] 和 [tryboot] 条件过滤器。

查看 TRYBOOT 启动流程。

### `boot_partition`

指定引导的分区号，除非分区号已作为 reboot 命令的参数指定（例如 sudo reboot 2 ）。

分区号从 1 开始，MBR 分区为 1 到 4。指定分区 0 意味着从第一个可引导的 FAT 分区 default 引导。

可引导的分区必须以 FAT12、FAT16 或 FAT32 格式进行格式化，并包含一个 start.elf 文件（或者在树莓派 5 上包含一个 config.txt 文件），以便引导程序将其视为可引导。

### [tryboot] 过滤器

如果系统启动时设置了 tryboot 标志，则此过滤器将通过。

```
$ sudo reboot "0 tryboot"
```

### `tryboot_a_b`

当设置此属性为 1 时，会加载普通 config.txt 和 boot.img 文件，而不加载 tryboot.txt 和 tryboot.img 文件，当 tryboot 标志设置时。

这样可以在分区级别而不是文件级别上进行 tryboot 开关，并且无需修改 A/B 分区中的配置文件。

### A/B 启动的示例更新流程

以下伪代码显示了一个假设的操作系统 Update service 如何在 autoboot.txt 中使用 tryboot 执行安全的操作系统升级。

 初始 autoboot.txt :

```
[all]
tryboot_a_b=1
boot_partition=2
[tryboot]
boot_partition=3
```

** 安装更新**

* 系统已启动并默认引导到分区 2
* Update service 下载 OS 的下一个版本到分区 3
* 通过重启到 tryboot 模式 reboot "0 tryboot" 来测试更新，其中 0 表示默认分区

**提交或取消更新**

* 系统从第 3 分区引导，因为 [tryboot] 过滤器在 tryboot mode 中评估为 true
* 如果 tryboot 处于活动状态 ( /proc/device-tree/chosen/bootloader/tryboot == 1 )

  * 如果当前的引导分区（ /proc/device-tree/chosen/bootloader/partition ）与 autoboot.txt 部分的 [tryboot] 匹配

    * Update Service 验证系统以确保更新成功
    * 如果更新成功

      * 替换 autoboot.txt 交换 boot_partition 配置
      * 正常重启 - 分区 3 现在是默认启动分区
    * 否则

      * Update Service 将更新标记为失败，例如删除更新文件。
      * 正常重启 - 分区 2 仍然是默认的启动分区，因为 tryboot 标志会自动清除。
    * 结束如果。
  * 结束 如果
* 结束 如果

 更新 autoboot.txt ：

```
[all]
tryboot_a_b=1
boot_partition=3
[tryboot]
boot_partition=2
```

| NOTE | 更新完 autoboot.txt 后不是必须重启。然而，Update Service 必须小心，以避免覆盖当前分区，因为已经修改了 autoboot.txt 以提交最后的更新。有关更多信息，请参阅设备树参数。|
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

## 常见选项

 在 GitHub 上编辑

### 常见显示选项

#### hdmi_enable_4kp60 （仅适用于 Raspberry Pi 4）

默认情况下，连接到 4K 显示器时，Raspberry Pi 4B、400 和 CM4 将选择 30Hz 刷新率。使用此选项可允许选择 60Hz 的刷新率。Raspberry Pi 4 不支持同时在两个微型 HDMI ports 上输出 4Kp60。设置 hdmi_enable_4kp60 会增加功耗和温度。

### 常见硬件配置选项

#### `camera_auto_detect`

启用此设置（在树莓派系统中，默认启用），固件将自动加载识别的 CSI 摄像头的叠加层。将 camera_auto_detect=0 设置为禁用该设置。

#### `display_auto_detect`

启用此设置（在树莓派系统中默认启用），固件将自动加载识别的 DSI 显示屏的叠加层。将 display_auto_detect=0 设置为禁用。

#### `dtoverlay`

dtoverlay 选项请求固件加载一个命名的设备树叠加层 - 一个可以启用内置和外部硬件内核支持的配置文件。例如，dtoverlay=vc4-kms-v3d 加载一个启用内核图形驱动程序的叠加层。

作为一个特殊情况，如果没有值调用 - dtoverlay= - 该选项标记着叠加参数列表的结束。如果在任何其他 dtoverlay 或 dtparam 设置之前使用，它会阻止加载任何 HAT 叠加层。

有关更多详细信息，请参阅 DTB、叠加和 config.txt。

#### `dtparam`

为 Raspberry Pi 的设备树配置文件支持许多参数，例如启用 I2C 和 SPI 接口。许多 DT 叠加层可通过参数配置。这两种类型的参数都可以使用 dtparam 设置。此外，叠加层参数可以附加到 dtoverlay 选项，用逗号分隔，但请注意字符长度限制为 98 个字符。

欲了解更多详情，请查阅 DTB、叠加层和 config.txt。

#### arm_boost （仅适用于 Raspberry Pi 4）

所有 Raspberry Pi 400s 和更新版本的 Raspberry Pi 4B 都配备了第二个开关模式电源供应，用于 SoC 电压轨，这使得默认的 turbo 模式时钟可从 1.5GHz 增加到 1.8GHz。此更改在树莓派系统中默认启用。设置 arm_boost=0 以禁用。

#### power_force_3v3_pwm （仅适用于 Raspberry Pi 5）

使用 3V3 电源时强制 PWM。设置 power_force_3v3_pwm=0 以禁用。

## 在板载模拟音频（3.5 毫米插孔）

 在 GitHub 上编辑此内容

板载音频输出使用配置选项来改变模拟音频驱动的方式，以及是否启用某些固件功能。

### `audio_pwm_mode`

audio_pwm_mode=1 选择来自 3.5 毫米 AV 插孔的传统低质量模拟音频。

audio_pwm_mode=2 （默认）使用先进的调制方案选择高质量模拟音频。

| NOTE | 此选项使用更多 GPU 计算资源，可能会对某些型号的某些用例产生干扰。|
| ------ | ------------------------------------------------------------------- |

### `disable_audio_dither`

默认情况下，如果音频流被路由到模拟音频输出，则会应用 1.0LSB 抖动。在某些情况下，例如当 ALSA 音量设置为低水平时，这可能会产生可听见的背景噪音。将 disable_audio_dither 设置为 1 以禁用抖动应用。

### `enable_audio_dither`

音频抖动（请参阅上述 disable_audio_dither）通常在音频样本大于 16 位时被禁用。将此选项设置为 1 可强制对所有位深度使用抖动。

### `pwm_sample_bits`

pwm_sample_bits 命令调整模拟音频输出的位深度。默认位深度为 11。选择低于 8 的位深度将导致音频无法正常工作，因为低于 8 的设置会导致 PLL 频率过低而无法支持。这通常仅用作演示位深度如何影响量化噪声。

## HDMI 音频

默认情况下，所有带 HDMI 输出的 Raspberry Pi 型号都启用 HDMI 音频输出。

要禁用 HDMI 音频输出，请在 /boot/firmware/config.txt 中的 dtoverlay=vc4-kms-v3d 行末尾添加 ,noaudio ：

```
dtoverlay=vc4-kms-v3d,noaudio
```

## 启动选项

 在 GitHub 上编辑此内容

### `start_file`, `fixup_file`

这些选项指定在启动前传输到 VideoCore GPU 的固件文件。

start_file 指定要使用的 VideoCore 固件文件。fixup_file 指定用于修正 start_file 中使用的内存位置，以匹配 GPU 内存分配。

start_file 和 fixup_file 是一对匹配的文件 - 使用不匹配的文件将阻止板子启动。这是一个高级选项，因此我们建议你使用 start_x 和 start_debug，而不是此选项。

| NOTE | 精简固件（ start*cd.elf 和 fixup*cd.dat ）不能通过这种方式选择 - 系统将无法启动。启用精简固件的唯一方法是指定 gpu_mem=16。精简固件删除对编解码器、3D 和调试日志的支持，以及将初始早期引导帧缓冲区限制为 1080p @16bpp - 尽管 KMS 可以在后续阶段用高达 32bpp 4K 帧缓冲区代替这一点，就像任何固件一样。|
| ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

| NOTE | 树莓派 5 固件包含在引导加载程序 EEPROM 中。|
| ------ | --------------------------------------------- |

### `cmdline`

cmdline 是启动分区上的备用文件名，用于读取内核命令行字符串；默认值为 cmdline.txt。

### `kernel`

kernel 是用于加载内核的启动分区上的备用文件名。树莓派 1、Zero 和 Zero W 以及树莓派计算模块 1 的默认值为 kernel.img。树莓派 2、3、3+ 和 Zero 2 W 以及树莓派计算模块 3 和 3+ 的默认值为 kernel7.img。树莓派 4 和 400 以及树莓派计算模块 4 的默认值为 kernel8.img，或者如果设置了 arm_64bit 为 0，则默认值为 kernel7l.img。

Raspberry Pi 5 固件默认加载 kernel_2712.img，因为此镜像针对 Raspberry Pi 5 进行了优化（例如 16K 页面大小）。如果此文件不存在，则会加载通用的 64 位内核（ kernel8.img ）。

### `arm_64bit`

如果设置为 1，则内核将以 64 位模式启动。设置为 0 会选择 32 位模式。

在 64 位模式下，固件将选择适当的内核（例如 kernel8.img ），除非存在明确的 kernel 选项，那么将使用该选项。

在 Pi 4s（Pi 4B、Pi 400、CM4 和 CM4S）上默认为 1，在所有其他平台上默认为 0。但是，如果显式 kernel 选项中给定的名称与已知的内核之一匹配，则 arm_64bit 将相应设置。

| NOTE | 64 位内核可以是未压缩的镜像文件或图像的 gzip 存档（仍可称为 kernel8.img；引导加载程序将从开头的签名字节识别存档）。64 位内核仅适用于树莓派 3、3+、4、400、Zero 2 W 和 2B rev 1.2，以及树莓派计算模块 3、3+ 和 4。树莓派 5 仅支持 64 位内核，因此对于该设备已删除此参数。|
| ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

### `ramfsfile`

ramfsfile 是引导分区上的 ramfs 的可选文件名。

| NOTE | 新固件支持加载多个 ramfs 文件。应注意使用逗号分隔多个文件名，不要超过 80 个字符的行长限制。所有加载的文件在内存中连接在一起，被视为单个 ramfs blob。有关更多信息，请参阅论坛。|
| ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

### `ramfsaddr`

ramfsaddr 是应将 ramfsfile 加载到的内存地址。

### `initramfs`

initramfs 命令同时指定 ramfs 文件名和需要加载到的内存地址。它在一个参数中执行了 ramfsfile 和 ramfsaddr 的操作。地址也可以是 followkernel （或 0 ），将其放在内核映像后的内存中。示例值为： initramfs initramf.gz 0x00800000 或 initramfs init.gz followkernel。与 ramfsfile 一样，更新的固件允许通过逗号分隔它们的名称加载多个文件。

| NOTE | 此选项使用与所有其他选项不同的语法，你不应在此处使用 = 字符。|
| ------ | --------------------------------------------------------------- |

### `auto_initramfs`

如果 auto_initramfs 设置为 1，请按照内核选择的相同规则查找 initramfs 文件。

### `disable_poe_fan`

默认情况下，I2C 总线上的探测将在启动时发生，即使未连接 PoE HAT。将此选项设置为 1 可禁用通过 I2C 控制 PoE HAT 风扇（在 ID_SD＆ID_SC 引脚上）。如果你不打算使用 PoE HAT，则这是最大化启动时间的有用方式。

### `disable_splash`

如果将 disable_splash 设置为 1，则启动时不会显示彩虹闪屏。默认值为 0。

### `enable_uart`

enable_uart=1 （与 console=serial0 结合在 cmdline.txt 中）要求内核创建一个串行控制台，可使用 GPIO 14 和 15（40 引脚排针上的 8 和 10 引脚）访问。编辑 cmdline.txt 以删除 quiet 行，从而使内核的启动消息也显示在那里。另请参阅 uart_2ndstage。

### `force_eeprom_read`

将此选项设置为 0 可防止固件在上电时尝试读取连接到 ID_SD 和 ID_SC 引脚的 I2C HAT EEPROM。另请参阅 disable_poe_fan。

### `os_prefix`

os_prefix 是一个可选设置，允许你在同一卡上安装的内核和设备树文件的多个版本之间进行选择。os_prefix 中的任何值都会被前置到固件加载的任何操作系统文件的名称之前，其中“操作系统文件”的定义是指内核、initramfs、cmdline.txt、.dtbs 和叠加层。该前缀通常是目录名称，但也可以是文件名的一部分，比如“test-”。因此，目录前缀必须包含尾随的 / 字符。

为了减少系统无法启动的几率，固件首先测试所提供的前缀值是否可行 - 除非新位置/名称能够找到预期的内核和.dtb 文件，否则前缀将被忽略（设为“”）。此可行性测试的一个特例应用于叠加层，只有从 ${os_prefix}${overlay_prefix} （其中 overlay_prefix 的默认值为“overlays/”）才会加载叠加层，否则它会忽略 os_prefix 并将叠加层视为共享项。

（固件在检查前缀时检查关键文件的存在而不是目录的原因有二：前缀可能不是目录，并非所有启动方法都支持测试目录的存在。）

| NOTE | 任何用户指定的操作系统文件都可以通过使用绝对路径（相对于启动分区）来绕过所有前缀-只需以 / 开头，例如 kernel=/my_common_kernel.img。|
| ------ | -------------------------------------------------------------------------------------------------------------------------------------- |

另请参阅 overlay_prefix 和 upstream_kernel。

### otg_mode （仅适用于树莓派 4）。

USB On-The-Go（通常缩写为 OTG）是一项功能，它允许支持 USB 设备使用适当的 OTG 电缆将自己配置为 USB 主机。在旧版的 Raspberry Pis 上，一个 USB2 控制器同时用于 USB 主机和设备模式。

Raspberry Pi 4B 和 Raspberry Pi 400（不包括 CM4 或 CM4IO）添加了一个高性能 USB 3 控制器，通过 PCIe 连接，以驱动主 USB ports。传统的 USB 2 控制器仍然可以在 USB-C 电源连接器上使用为设备（ otg_mode=0，默认情况下）。

otg_mode=1 请求使用更具能力的 XHCI USB 2 控制器作为 USB-C 连接器上的另一个主机控制器。

| NOTE | 由于 CM4 和 CM4IO 不包括外部 USB 3 控制器，树莓派操作系统镜像在 CM4 上设置 otg_mode=1 以获得更好的性能。|
| ------ | ---------------------------------------------------------------------------------------------------------- |

### `overlay_prefix`

指定从哪个子目录/前缀加载叠加层，默认为 overlays/ （注意末尾的 / ）。如果与 os_prefix 一起使用，则 os_prefix 位于 overlay_prefix 之前，即 dtoverlay=disable-bt 将尝试加载 ${os_prefix}${overlay_prefix}disable-bt.dtbo。

| NOTE | 除非 ${os_prefix}${overlay_prefix}README 存在，否则叠加层与主操作系统共享（即 os_prefix 将被忽略）。|
| ------ | ------------------------------------------------------------------------------------------------------ |

### 配置属性

树莓派 5 需要一个 config.txt 文件表示分区可引导。

#### `boot_ramdisk`

如果此属性设置为 1，则引导程序将尝试加载一个名为 boot.img 的 ramdisk 文件，其中包含引导文件系统。随后的文件（例如 start4.elf ）从 ramdisk 中读取，而不是原始引导文件系统。

boot_ramdisk 的主要目的是支持 secure-boot，但未签名的 boot.img 文件也可用于网络引导或 RPIBOOT 配置。

* RAM 磁盘文件的最大大小为 96MB。
* boot.img 文件是原始磁盘 .img 文件。建议的格式是一个没有 MBR 的普通 FAT32 分区。
* RAM 磁盘文件系统的内存在操作系统启动之前被释放。
* 如果选择了 TRYBOOT，则引导加载程序将搜索 tryboot.img 而不是 boot.img。
* 也请参阅 autoboot.txt。

有关 secure-boot 和创建 boot.img 文件的更多信息，请参阅 USBBOOT。

 默认： 0

#### `boot_load_flags`

自定义固件（裸金属）的实验性属性。

位 0 (0x1) 表示 .elf 文件为定制固件。这将禁用任何兼容性检查（例如 USB MSD 启动是否受支持），并在启动可执行文件之前重置 PCIe。

树莓派 5 上无关紧要，因为没有 start.elf 文件。

 默认： 0x0

#### `pciex4_reset`

仅适用于 Raspberry Pi 5。

默认情况下，RP1 使用的 PCIe x4 控制器在启动操作系统之前会被复位。如果此参数设置为 0，则复位将被禁用，允许操作系统或裸金属代码继承来自引导加载程序的 PCIe 配置设置。

 默认值： 1

#### `uart_2ndstage`

如果 uart_2ndstage 是 1，则启用 UART 调试日志记录。此选项还会自动启用 start.elf 中的 UART 日志记录。这也在启动选项页面上有描述。

BOOT_UART 属性还会启用引导加载程序 UART 日志记录，但不会在 start.elf 中启用 UART 日志记录，除非也设置了 uart_2ndstage=1。

 默认： 0

#### `erase_eeprom`

如果 erase_eeprom 设置为 1，那么 recovery.bin 将擦除整个 SPI EEPROM 而不是刷新引导加载程序镜像。此属性在正常启动期间没有任何效果。

 默认: 0

#### `eeprom_write_protect`

配置 EEPROM write status register。这可以设置为将整个 EEPROM 标记为写保护，或清除写保护。

这个选项必须与控制 EEPROM 更新的 EEPROM /WP 引脚一起使用。拉低 /WP （CM4 EEPROM_nWP 或者在树莓派 4 TP5 上）不会写保护 EEPROM，除非 Write Status Register 也已配置。

查看 Winbond W25x40cl 或 Winbond W25Q16JV 数据手册以获取更多详细信息。

config.txt 中的 eeprom_write_protect 设置为 recovery.bin。

| 值 | 描述                              |
| ---- | ----------------------------------- |
| 1  | 配置写保护区域以覆盖整个 EEPROM。|
| 0  | 清除写保护区域。        |
| -1 | 什么也不做。            |

| NOTE | flashrom 不支持清除写保护区域，如果定义了写保护区域，将无法更新 EEPROM。|
| ------ | -------------------------------------------------------------------------- |

在树莓派 5 上，默认情况下，/WP 被拉低，因此一旦配置 Write Status Register，写保护就会启用。要清除写保护，请通过连接 TP14 和 TP1 将 /WP 拉高。

 默认值: -1

#### `os_check`

在树莓派 5 上，固件会自动在尝试从当前分区引导之前检查兼容的设备树文件。否则，将加载旧的不兼容内核，然后挂起。要禁用此检查（例如用于裸机开发），请在 config.txt 中设置 os_check=0。

 默认： 1

#### `bootloader_update`

可将此选项设置为 0 以阻止自更新，而无需更新 EEPROM 配置。在通过网络引导更新多个 Raspberry Pi 时，有时会很有用，因为可以针对每个 Raspberry Pi 控制此选项（例如，通过 config.txt 中的串行号过滤器）。

 默认： 1

### 安全引导配置属性

##### [如何使用树莓派安全引导](https://pip.raspberrypi.com/categories/685-whitepapers-app-notes/documents/RP-003466-WP/Boot-Security-Howto.pdf)

如何使用树莓派安全引导

本白皮书描述了如何在基于 Raspberry Pi 4 的设备上实现安全启动。有关我们实施安全启动方法的概述，请参阅 Raspberry Pi 4 启动安全白皮书。安全启动系统旨在与 buildroot -based OS 镜像一起使用；不建议或支持将其与树莓派系统一起使用。

以下 config.txt 属性用于编程 secure-boot OTP 设置。这些更改是不可逆的，只能在刷写引导加载程序 EEPROM 镜像时通过 RPIBOOT 进行编程。这确保了 secure-boot 无法远程设置或通过意外插入陈旧的 SD 卡映像。

有关启用 secure-boot 的更多信息，请参阅 Secure Boot 自述文件和 USBBOOT 存储库中的 Secure Boot 教程。

#### `program_pubkey`

如果将此属性设置为 1，则 recovery.bin 将哈希公钥的散列值写入 EEPROM 镜像到 OTP。设置后，引导加载程序将拒绝使用不同 RSA 密钥签名的 EEPROM 镜像或未签名镜像。

 默认： 0

#### `revoke_devkey`

如果将此属性设置为 1，则 recovery.bin 将写入一个值到 OTP，防止 ROM 加载不支持 secure-boot 的旧第二阶段引导加载程序版本。这可以防止通过回滚到旧版本的引导加载程序释放 secure-boot 被关闭。

 默认: 0

#### `program_rpiboot_gpio`

由于 树莓派 4B 或 树莓派 400 上没有专用 GPIO 跳线帽，必须使用其他 GPIO 来选择 RPIBOOT 模式，将 GPIO 拉低。从以下选项中选择一个单个 GPIO:

* `2`
* `4`
* `5`
* `6`
* `7`
* `8`

此属性不依赖于 secure-boot，但请验证此 GPIO 配置不会与在引导过程中拉低 GPIO 的任何 HAT 发生冲突。

由于出于安全考虑，此属性只能通过 RPIBOOT 进行编程，因此必须首先使用 erase_eeprom 清除引导加载程序 EEPROM。这将导致 BCM2711 ROM 切换到 RPIBOOT 模式，然后允许设置此选项。

 默认值：

#### `program_jtag_lock`

如果此属性设置为 1，则 recovery.bin 将编程防止使用 VideoCore JTAG 的 OTP 值。此选项要求还设置 program_pubkey 和 revoke_devkey。此选项可以防止故障分析，应仅在设备完全测试后设置。

 默认: 0

## GPIO 控制

 在 GitHub 上编辑

### `gpio`

gpio 指示允许在引导时将 GPIO 引脚设置为特定模式和值，以一种以前需要定制 dt-blob.bin 文件的方式进行设置。每行将相同的设置应用于一组引脚，或者至少对一组引脚进行相同的更改，可以处理单个引脚（ 3 ），一系列引脚（ 3-4 ）或者以逗号分隔的列表（ 3-4,6,8 ）。

引脚设置后跟一个 = 和此列表中的一个或多个逗号分隔属性：

* ip - 输入
* op - 输出
* `a0-a5` - Alt0-Alt5
* dh - 驱动高（用于输出）
* dl - 驱动低电平（用于输出）
* pu - 上拉
* pd - 下拉
* pn/np - 没有拉取

gpio 设置按顺序应用，因此后面出现的设置会覆盖先前出现的设置。

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

该 gpio 指令尊重 "[...]" 条件过滤器，因此可以根据型号、序列号和 EDID 使用不同的设置。

通过该机制进行的 GPIO 更改不会直接影响内核。它们不会导致 GPIO 引脚被导出到 sysfs 接口，并且可以被设备树中的 pinctrl 条目以及像 pinctrl 这样的实用工具覆盖。

还要注意，应用电源并使更改生效之间会有几秒钟的延迟-如果通过网络引导或从 USB 大容量存储设备引导，则延迟会更长。

## 超频选项

 在 GitHub 上编辑此内容

内核默认启用了 CPUFreq 驱动程序，并在启动时将 powersave 调度程序切换为 ondemand，安装 raspi-config 后。使用 ondemand 调度程序，CPU 频率将随处理器负载变化。你可以通过 *_min 配置选项调整最小值，或者通过应用静态缩放调度程序（powersave 或 performance）或使用 force_turbo=1 来禁用动态时钟调整。

当 SoC 达到 temp_limit （见下文）时，运行时会禁用超频和过压功能，默认为 85°C，以便降低 SoC 温度。你不应该在 树莓派 1 和 树莓派 2 上达到这个限制，但在 树莓派 3 和更新版本上更有可能。当检测到欠电压情况时，也会禁用超频和过压功能。

| NOTE | 更多信息请参阅频率管理和热控制部分。|
| ------ | -------------------------------------- |

| WARNING | 将任何超频参数设置为非 raspi-config 使用的值可能会在 SoC 内部设置一个永久比特。这将使你的 树莓派 曾经超频的情况变得可检测。当将 force_turbo 设置为 1 且任一 over_voltage_* 选项设为大于 0 的值时，超频位会设置。详细信息请查看有关 Turbo 模式的博文。|
| --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

### 超频

| 选项 | 描述                                                                                                                                                                                                                                                                                                                                                                           |
| ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `arm_freq`     | ARM CPU 的频率，以 MHz 为单位。                                                                                                                                                                                                                                                                                                                                      |
| `arm_boost`     | 将 arm_freq 增加到板型和固件支持的最高频率。设置为 1 以启用。                                                                                                                                                                                                                                                                                                        |
| `gpu_freq`     | 将 core_freq、h264_freq、isp_freq、v3d_freq 和 hevc_freq 一起设置。                                                                                                                                                                                                                                                                                            |
| `core_freq`     | GPU 处理器核心的频率，以兆赫为单位。影响 CPU 性能，因为它驱动 L2 缓存和内存总线；只有树莓派 Zero / 树莓派 Zero W / 树莓派 1 受益于 L2 缓存；对树莓派 2 和树莓派 3 上的 SDRAM 有一点益处。请参见下面关于在树莓派 4 上使用的部分。                                                                                                                                     |
| `h264_freq`     | 硬件视频块的频率，以兆赫为单位；对 gpu_freq 设置的个别覆盖。                                                                                                                                                                                                                                                                                                         |
| `isp_freq`     | 图像传感器管道块的频率，以兆赫为单位；对 gpu_freq 设置的个别覆盖。                                                                                                                                                                                                                                                                                                   |
| `v3d_freq`     | 在 MHz 中的 3D 块的频率；gpu_freq 设置的个别覆盖。在 Raspberry Pi 5 上，V3D 与 core_freq、isp_freq 和 hevc_freq 独立。                                                                                                                                                                                                                                            |
| `hevc_freq`     | 高效视频编解码器块的频率，单位为 MHz；gpu_freq 设置的个别覆盖。仅适用于 Raspberry Pi 4。                                                                                                                                                                                                                                                                            |
| `sdram_freq`     | SDRAM 的频率，单位为 MHz。不支持在 Raspberry Pi 4 或更新版本上超频 SDRAM。                                                                                                                                                                                                                                                                                           |
| `over_voltage`     | CPU/GPU 核心上限电压。值应在范围[-16,8]内，这相当于范围[0.95V,1.55V]（在树莓派 1 上为 [0.8V,1.4V]），步长为 0.025V。换句话说，指定-16 将使 CPU/GPU 核心电压的最大值为 0.95V（在树莓派 1 上为 0.8V），指定 8 将允许高达 1.55V（在树莓派 1 上为 1.4V）。有关默认值，请参见下表。仅当指定了 force_turbo=1 时才允许高于 6 的值：如果还设置了 over_voltage_* > 0，则会设置保修位。|
| `over_voltage_sdram`     | 一起设置 over_voltage_sdram_c，over_voltage_sdram_i 和 over_voltage_sdram_p。                                                                                                                                                                                                                                                                                     |
| `over_voltage_sdram_c`     | SDRAM 控制器电压调整。[-16,8]相当于[0.8V,1.4V]，步长为 0.025V。不支持树莓派 4 或更高版本设备。                                                                                                                                                                                                                                                                       |
| `over_voltage_sdram_i`     | SDRAM I/O 电压调整。[-16,8] 相当于[0.8V,1.4V]，步长为 0.025V。不支持树莓派 4 或更高版本的设备。                                                                                                                                                                                                                                                                      |
| `over_voltage_sdram_p`     | SDRAM 物理电压调整。[-16,8] 相当于[0.8V,1.4V]，步长为 0.025V。不支持树莓派 4 或更高版本的设备。                                                                                                                                                                                                                                                                      |
| `force_turbo`     | 即使 ARM 核心空闲时也强制进入 Turbo 模式频率。启用此选项可能设置保修位，如果 over_voltage_* 也设置的话。                                                                                                                                                                                                                                                             |
| `initial_turbo`     | 从引导启用提速模式，持续给定的秒数，或直到 cpufreq 设置频率。最大值为 60。                                                                                                                                                                                                                                                                                          |
| `arm_freq_min`     | 用于动态频率时钟的最小值为 arm_freq。请注意，将该值降低到低于默认值并不会导致任何显著的节能，并且当前不受支持。                                                                                                                                                                                                                                                     |
| `core_freq_min`     | 用于动态频率时钟的最小值为 core_freq。                                                                                                                                                                                                                                                                                                                              |
| `gpu_freq_min`     | 用于动态频率调节的最小值 gpu_freq。                                                                                                                                                                                                                                                                                                                                 |
| `h264_freq_min`     | 用于动态频率调节的最小值 h264_freq。                                                                                                                                                                                                                                                                                                                                |
| `isp_freq_min`     | 用于动态频率调节的最小值 isp_freq。                                                                                                                                                                                                                                                                                                                                 |
| `v3d_freq_min`     | 用于动态频率时钟的最小值 v3d_freq。                                                                                                                                                                                                                                                                                                                                 |
| `hevc_freq_min`     | 用于动态频率时钟的最小值 hevc_freq。                                                                                                                                                                                                                                                                                                                                |
| `sdram_freq_min`     | 用于动态频率时钟的最小值 sdram_freq。                                                                                                                                                                                                                                                                                                                               |
| `over_voltage_min`     | 动态频率时钟的最小值 over_voltage。该值应在[-16,8]范围内，等同于[0.8V,1.4V]范围，每 0.025V 一步。换句话说，指定-16 将使 CPU/GPU 核心空闲电压为 0.8V，指定 8 将使最低电压为 1.4V。在树莓派 4 和树莓派 5 上，此设置已被弃用。                                                                                                                                         |
| `over_voltage_delta`     | 在树莓派 4 和树莓派 5 上，over_voltage_delta 参数会将给定的偏移量（以微伏计算）添加到 DVFS 算法计算的数字中。                                                                                                                                                                                                                                                        |
| `temp_limit`     | 过热保护。当 SoC 达到摄氏度设定值时，将时钟和电压设置为默认值。超过 85 的值将被限制为 85。                                                                                                                                                                                                                                                                           |
| `temp_soft_limit`     | 仅适用于 3A+/3B+. CPU 速度节流控制。这将设置 CPU 时钟速度节流系统激活的温度。在此温度下，时钟速度从 1400MHz 降至 1200MHz。默认为 60，最多可提高至 70，但这可能会导致不稳定。                                                                                                                                                                                       |

该表提供了各种树莓派型号选项的默认值，所有频率均以 MHz 表示。

| 选项 | 树莓派 0/W | 树莓派 1 | 树莓派 2 | 树莓派 3 | 树莓派 3A+/树莓派 3B+ | CM4 和 树莓派 4B ⇐ R1.3 | 树莓派 4B R1.4                   | 树莓派 400 | 树莓派 Zero 2 W | Pi 5   |
| ------ | ------------ | ---------- | ---------- | ---------- | ----------------------- | -------------------------- | ---------------------------------- | ------------ | ----------------- | -------- |
| `arm_freq`     | 1000       | 700      | 900      | 1200     | 1400                  | 1500                     | 1500 或 1800（如果 arm_boost = 1 | 1800       | 1000            | 2400   |
| `core_freq`     | 400        | 250      | 250      | 400      | 400                   | 500                      | 500                              | 500        | 400             | 910    |
| `h264_freq`     | 300        | 250      | 250      | 400      | 400                   | 500                      | 500                              | 500        | 300             | 不适用 |
| `isp_freq`     | 300        | 250      | 250      | 400      | 400                   | 500                      | 500                              | 500        | 300             | 910    |
| `v3d_freq`     | 300        | 250      | 250      | 400      | 400                   | 500                      | 500                              | 500        | 300             | 910    |
| `hevc_freq`     | 无         | 无       | 无       | 无       | 无                    | 500                      | 500                              | 500        | 无              | 910    |
| `sdram_freq`     | 450        | 400      | 450      | 450      | 500                   | 3200                     | 3200                             | 3200       | 450             | 4267   |
| `arm_freq_min`     | 700        | 700      | 600      | 600      | 600                   | 600                      | 600                              | 600        | 600             | 1500   |
| `core_freq_min`     | 250        | 250      | 250      | 250      | 250                   | 200                      | 200                              | 200        | 250             | 500    |
| `gpu_freq_min`     | 250        | 250      | 250      | 250      | 250                   | 250                      | 250                              | 250        | 250             | 500    |
| `h264_freq_min`     | 250        | 250      | 250      | 250      | 250                   | 250                      | 250                              | 250        | 250             | 不适用 |
| `isp_freq_min`     | 250        | 250      | 250      | 250      | 250                   | 250                      | 250                              | 250        | 250             | 500    |
| `v3d_freq_min`     | 250        | 250      | 250      | 250      | 250                   | 250                      | 250                              | 250        | 250             | 500    |
| `sdram_freq_min`     | 400        | 400      | 400      | 400      | 400                   | 3200                     | 3200                             | 3200       | 400             | 4267   |

此表提供了所有通用的选项默认值。

| 选项 | 默认                           |
| ------ | -------------------------------- |
| `initial_turbo`     | 0（秒）                        |
| `temp_limit`     | 85（°C）                      |
| `over_voltage`     | 0（1.35V，树莓派 1 上的 1.2V） |
| `over_voltage_min`     | 0（1.2V）                      |
| `over_voltage_sdram`     | 0（1.2V）                      |
| `over_voltage_sdram_c`     | 0 (1.2 伏特)                   |
| `over_voltage_sdram_i`     | 0 (1.2 伏特)                   |
| `over_voltage_sdram_p`     | 0 (1.2 伏特)                   |

固件使用自适应电压调整（AVS）来确定在 over_voltage 和 over_voltage_min 定义的范围内的最佳 CPU/GPU 核心电压。

#### 适用于 Raspberry Pi 4，Raspberry Pi 400 和 CM4

当系统处于空闲状态时，最小核心频率必须足够快，以支持显示器的最高像素时钟（忽略消隐）。因此，如果显示模式为 4Kp60，则 core_freq 将被提升到 500 MHz 以上。

| 显示选项 | 最大 core_freq |
| ---------- | ---------------- |
| 默认     | 500            |
| `hdmi_enable_4kp60`         | 550            |

| NOTE | 树莓派 5 上默认支持双 4Kp60 显示屏，无需使用 hdmi_enable_4kp60。|
| ------ | ------------------------------------------------------------------- |

* 超频需要最新的固件版本。
* 最新的固件在系统超频时会自动提高电压。手动设置 over_voltage 会禁用超频时的自动电压调节。
* 在超频时建议使用单独的频率设置（ isp_freq，v3d_freq 等），而不是 gpu_freq，因为 ISP、V3D、HEVC 等的最大稳定频率不同。
* Raspberry Pi 4 或更高版本设备上的 SDRAM 频率不可配置。

#### `force_turbo`

默认情况下（ force_turbo=0 ），按需的 CPU 频率驱动程序会在 ARM 核心繁忙时将时钟提升到最大频率，并在 ARM 核心空闲时将其降至最低频率。

force_turbo=1 覆盖了这种行为，即使 ARM 核心不忙，也会强制使用最大频率。

### 时钟关系

#### 树莓派 4

GPU 核心、CPU、SDRAM 和 GPU 各自拥有自己的 PLL，并且可以具有不相关的频率。h264、v3d 和 ISP 模块共享一个 PLL。

要查看树莓派当前的频率（以 KHz 为单位），请输入： cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_cur_freq。将结果除以 1000 以找到以 MHz 为单位的值。请注意，此频率是内核请求的频率，可能在任何限制情况下（例如在高温下）CPU 实际运行速度可能比报告的要慢。可以使用 vcgencmd 获取实际 ARM CPU 频率的瞬时测量 vcgencmd measure_clock arm。该频率以赫兹为单位显示。

### 监控核心温度

##### [冷却 Raspberry Pi 设备](https://pip.raspberrypi.com/categories/685-whitepapers-app-notes/documents/RP-003608-WP/Cooling-a-Raspberry-Pi-device.pdf)

冷却 Raspberry Pi 设备

本白皮书详细介绍了你的 Raspberry Pi 可能会发热的原因，以及为什么你可能希望对其进行降温，并提供了有关冷却过程的选项。

要查看树莓派的温度，请运行以下命令：

```
$ cat /sys/class/thermal/thermal_zone0/temp
```

通过将结果除以 1000 来找到摄氏度的值。或者，你可以使用 vcgencmd measure_temp 来报告 GPU 温度。

达到温度极限对 SoC 并不有害，但会导致 CPU 降频。散热器可以帮助控制核心温度，从而提高性能。如果树莓派安装在外壳内，则特别有用。散热器上的空气流动会使冷却效果更好。

当核心温度在 80°C 和 85°C 之间时，ARM 核心将被调整。如果温度超过 85°C，ARM 核心和 GPU 将被调整。

对于 Raspberry Pi 3B+，PCB 技术已经改变，提供更好的散热和增加热量。此外，引入了一个软温度限制，旨在最大限度地延长设备在达到 85°C 硬限制之前的“冲刺”时间。当达到软限制时，时钟速度从 1.4GHz 降至 1.2GHz，并稍微降低操作电压。这减少了温度的上升速度：我们用 1.4GHz 的短暂时间换取了 1.2GHz 的长时间。默认情况下，软限制为 60°C。可以通过 temp_soft_limit 设置中的 config.txt 更改此设置。

### 监控电压

保持供电电压高于 4.8V 以确保可靠性能。请注意，一些 USB 充电器/电源的电压可能会降至 4.2V。这是因为它们通常设计用于为 3.7V 的锂聚合物电池充电，而不是为计算机提供 5V 的电压。

要监测树莓派的电源供电电压，你需要使用万用表在 GPIO 引脚的 VCC 和 GND 之间进行测量。有关更多信息，请查看文档的电源部分。

如果电压降至 4.63V 以下（±5％），ARM 核心和 GPU 将被降频，并将在内核日志中增加指示低电压状态的消息。

树莓派 5 的 PMIC 具有内置的 ADC，可测量供电电压。要查看当前的供电电压，请运行以下命令：

```
$ vcgencmd pmic_read_adc EXT5V_V
```

### 超频问题

大多数超频问题会立即出现在启动失败时。如果出现这种情况，请在下次启动时按住 shift 键。这将临时禁用所有超频，让你成功启动，然后编辑你的设置。

## 条件过滤器

 在 GitHub 上编辑此内容

当一个 Raspberry Pi 和一台显示器使用单个 SD 卡（或卡镜像）时，很容易将 config.txt 设置为该特定组合所需的方式，并仅在发生更改时进行修改。

但是，如果一个 Raspberry Pi 在不同的显示器之间交换，或者 SD 卡（或卡镜像）在多个板之间交换，单一的设置可能不再足够。条件过滤器允许你定义配置文件的某些部分仅在特定情况下使用，从而使单个 config.txt 在不同硬件读取时创建不同的配置。

### [all] 过滤器

[all] 过滤器是最基本的过滤器。它重置所有先前设置的过滤器，并允许将下面列出的任何设置应用于所有硬件。通常最好在过滤设置组的末尾添加一个 [all] 过滤器，以避免意外组合过滤器（请参见下文）。

### 过滤器

根据以下表格应用条件过滤器。

| 过滤器 | 适用型号                                                                 |
| -------- | -------------------------------------------------------------------------- |
| `[pi1]`       | 1A 型号，1B 型号，1A+型号，1B+型号，计算模块 1                           |
| `[pi2]`       | 2B 型号（基于 BCM2836 或 BCM2837）                                       |
| `[pi3]`       | Model 3B, Model 3B+, Model 3A+, Compute Module 3, Compute Module 3+      |
| `[pi3+]`       | Model 3A+, Model 3B+（还可以看到 [pi3] 内容）                            |
| `[pi4]`       | Model 4B, Pi 400, Compute Module 4, Compute Module 4S                    |
| `[pi5]`       | 树莓派 5                                                                 |
| `[pi400]`       | Pi 400（也看到 [pi4] 内容）                                              |
| `[cm4]`       | 计算模块 4（也看到 [pi4] 内容）                                          |
| `[cm4s]`       | 计算模块 4S（也查看 [pi4] 内容）                                         |
| `[pi0]`       | Zero，Zero W，Zero 2 W                                                   |
| `[pi0w]`       | Zero W（也查看 [pi0] 内容）                                              |
| `[pi02]`       | 零 2W（还可以查看 [pi0w] 和 [pi0] 的内容）                               |
| `[board-type=Type]`       | 按 Type 号筛选 - 查看树莓派修订代码，例如 [board-type=0x14] 将匹配 CM4。|

这些对于定义不同的 kernel、initramfs 和 cmdline 设置特别有用，因为树莓派 1 和树莓派 2 需要不同的内核。它们还可以用于定义不同的超频设置，因为树莓派 1 和树莓派 2 有不同的默认速度。例如，为每个定义单独的 initramfs 镜像：

```
[pi1]
initramfs initrd.img-3.18.7+ followkernel
[pi2]
initramfs initrd.img-3.18.7-v7+ followkernel
[all]
```

记得在最后使用 [all] 过滤器，这样任何后续设置不仅限于 Raspberry Pi 2 硬件。

| NOTE | 一些 Raspberry Pi 的型号（Zero W，Zero 2 W，Model 3B+，Pi 400，Compute Module 4 和 Compute Module 4S）查看多个过滤器的设置（如上表所列）。这意味着如果你想让一个设置只适用于（例如）4B 型号，而不会将该设置应用于 Pi 400，那么 [pi4] 部分中的设置需要在随后的 [pi400] 部分中通过替代设置来恢复 - 这些部分的顺序很重要。或者，你可以使用 [board-type=0x11] 过滤器，这个过滤器与不同的硬件产品之间有一对一的映射关系。|
| ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

### [none] 过滤器

该 [none] 过滤器阻止任何随后的设置应用于任何硬件。尽管没有什么是你不能没有 [none] 做的，但它可以是一个有用的方法，可以在不必注释掉每一行的情况下，在 config.txt 中保留未使用设置的组。

### 该 [tryboot] 过滤器

如果设置了 tryboot 重新引导标志，则此过滤器成功。

用于 autoboot.txt 中，以在故障安全的 OS 更新模式下选择不同的 boot_partition。

### [EDID=*] 过滤器

在 Raspberry Pi 上使用单个 SD 卡切换多个显示器时，并且空白配置不足以自动为每个显示器选择所需的分辨率时，可以根据显示器的 EDID 名称选择特定设置。

要查看已连接显示器的 EDID 名称，你需要按照以下步骤操作。运行以下命令，查看你的树莓派上有哪些输出设备：

```
$ ls -1 /sys/class/drm/card?-HDMI-A-?/edid
```

在树莓派 4 上，这将打印类似于：

```
/sys/class/drm/card1-HDMI-A-1/edid
/sys/class/drm/card1-HDMI-A-2/edid
```

然后，你需要对每个这些文件名运行 edid-decode，例如：

```
$ edid-decode /sys/class/drm/card1-HDMI-A-1/edid
```

如果没有显示器连接到特定输出设备，它将告诉你 EDID 为空；否则，它会为你提供有关显示器功能的大量信息。你需要查找指定 Manufacturer 和 Display Product Name 的行。然后，“EDID 名称”为 <Manufacturer>-<Display Product Name>，其中任一字符串中的空格都将替换为下划线。例如，如果你的 edid-decode 输出包括：

```
....
  Vendor & Product Identification:
    Manufacturer: DEL
....
    Display Product Name: 'DELL U2422H'
....
```

此显示器的 EDID 名称将是 DEL-DELL_U2422H。

然后，你可以将其用作条件过滤器，指定仅在连接此特定显示器时适用的设置：

```
[EDID=DEL-DELL_U2422H]
cmdline=cmdline_U2422H.txt
[all]
```

这些设置仅适用于启动时。监视器必须在启动时连接，并且树莓派必须能够读取其 EDID 信息以找到正确的名称。在启动后将不同的监视器热插拔到树莓派上将不会选择不同的设置。

在树莓派 4 上，如果两个 HDMI ports同时使用，则 EDID 过滤器将与两者进行匹配，并将应用所有匹配条件过滤器的配置。

| NOTE | 在树莓派 5 上不提供此设置。|
| ------ | ----------------------------- |

### 串行号码过滤器

有时候设置应仅适用于单个特定的树莓派，即使你将 SD 卡更换为另一个。示例包括许可证密钥和超频设置（虽然许可证密钥已以不同方式支持 SD 卡更换）。你还可以使用此功能选择不同的显示设置，即使上述的 EDID 识别不可能，只要你不在树莓派之间切换监视器。例如，如果你的显示器没有提供可用的 EDID 名称，或者如果你正在使用复合输出（其中无法读取 EDID）。

要查看你的树莓派的串行号码，请运行以下命令：

```
$ cat /proc/cpuinfo
```

输出的底部附近将显示一个 16 位十六进制值。你的 Raspberry Pi 串行号是最后八位十六进制数字。例如，如果你看到：

```
Serial          : 0000000012345678
```

串行号是 12345678。

| NOTE | 在某些 Raspberry Pi 型号上，前 8 位十六进制数字包含除 0 之外的其他值。即使在这种情况下，也只使用最后八位十六进制数字作为串行号。|
| ------ | ----------------------------------------------------------------------------------------------------------------------------------- |

你可以定义仅应用于此特定树莓派的设置：

```
[0x12345678]
# settings here apply only to the Raspberry Pi with this serial

[all]
# settings here apply to all hardware
```

### GPIO 过滤器

你还可以根据 GPIO 的状态进行过滤。例如：

```
[gpio4=1]
# Settings here apply if GPIO 4 is high

[gpio2=0]
# Settings here apply if GPIO 2 is low

[all]
# settings here apply to all hardware
```

### 合并条件过滤器

相同类型的过滤器互相取代，因此 [pi2] 会覆盖 [pi1]，因为两者不可能同时为真。

不同类型的过滤器可以通过依次列出它们来组合，例如:

```
# settings here apply to all hardware

[EDID=VSC-TD2220]
# settings here apply only if monitor VSC-TD2220 is connected

[pi2]
# settings here apply only if monitor VSC-TD2220 is connected *and* on a Raspberry Pi 2

[all]
# settings here apply to all hardware
```

使用 [all] 过滤器重置所有先前的过滤器，避免意外地组合不同类型的过滤器。

## 存储器选项

 在 GitHub 上编辑此项

### `total_mem`

此参数可用于强制限制树莓派的内存容量：指定你希望树莓派使用的总 RAM 量（以兆字节为单位）。例如，要使 4GB 的树莓派 4B 表现为 1GB 型号，请使用以下内容：

```
total_mem=1024
```

此值将被夹在 128MB 的最小值和板载安装的总内存的最大值之间。

## 许可证密钥和编解码器选项

 在 GitHub 上编辑此内容

可以通过购买一个许可证来激活树莓派 3 及其早期型号上的额外编解码器的硬件解码，该许可证将锁定到你的树莓派的 CPU 序列号。

树莓派 4 已永久禁用了 MPEG2 和 VC1 的硬件解码器。这些编解码器无法启用，因此不需要硬件编解码器许可证密钥。对于典型用例，MPEG2 和 VC1 文件的软件解码性能已经足够。

Raspberry Pi 5 具有 H.265（HEVC）硬件解码。该解码默认启用，因此不需要硬件解码许可密钥。

### `decode_MPG2`

decode_MPG2 是一个许可密钥，用于允许硬件 MPEG-2 解码，例如 decode_MPG2=0x12345678。

### `decode_WVC1`

decode_WVC1 是一个许可密钥，用于允许硬件 VC-1 解码，例如 decode_WVC1=0x12345678。

如果你有多个树莓派，并为每个树莓派购买了编解码器许可证，你可以在单个 config.txt 中列出多达八个许可证密钥，例如 decode_MPG2=0x12345678,0xabcdabcd,0x87654321。这使你可以在不必每次都编辑 config.txt 的情况下，在不同的树莓派之间交换同一张 SD 卡。

## 视频选项

 在 GitHub 上编辑此内容

### HDMI 模式

要控制 HDMI 设置，请使用屏幕配置实用程序或 KMS 视频设置中的 cmdline.txt。

#### 用于树莓派 4 的 HDMI 管道

为了支持双显示器和高达 4Kp60 的模式，Raspberry Pi 4 生成每个时钟周期的 2 个输出像素。

每个 HDMI 模式都有一组控制所有关于同步脉冲持续时间的参数的定时列表。这些通常是通过像素时钟定义的，然后是水平和垂直方向的一系列活动像素，前廊、同步脉冲和后廊。

将所有内容都设置为每个时钟 2 个像素意味着 Raspberry Pi 4 无法支持水平定时不是 2 的倍数的模式。固件和 Linux 内核会过滤掉不符合此标准的任何模式。

CEA 和 DMT 标准中只有一个不兼容模式：DMT 模式 81，1366x768 @ 60Hz。该模式具有水平同步和后廊定时的奇数值，并且宽度不能被 8 整除。

如果你的显示器具有此分辨率，树莓派 4 将自动降至显示器下一个广告模式；通常是 1280x720。

#### 树莓派 5 的 HDMI 管道

虽然 Raspberry Pi 5 也以每个时钟周期 2 个输出像素的速度运行，但它对奇数定时有特殊处理，并可以直接处理这些模式。

### 复合视频模式

每个 Raspberry Pi 计算机型号都可以找到复合视频输出。

| model           | 复合输出              |
| ----------------- | ----------------------- |
| 树莓派 1 A 和 B | RCA 接头              |
| 树莓派 Zero     | 未焊接的 TV 接头      |
| 树莓派 Zero 2 W | 板卡底部的测试垫      |
| 树莓派 5        | HDMI 插口旁边的 J7 垫 |
| 所有其他型号    | 3.5 毫米 AV 插孔      |

| NOTE | 树莓派 400 上不提供复合视频输出。|
| ------ | ----------------------------------- |

#### `enable_tvout`

将 1 设置为启用复合视频输出，将 0 设置为禁用。在树莓派 4 和 5 上，仅当你将其设置为 1 时，才可使用复合输出，这也会禁用 HDMI 输出。树莓派 400 上不支持复合输出。

| Model          | 默认 |
| ---------------- | ------ |
| Pi 4, 5 和 400 | 0    |
| 所有其他   | 1    |

除了树莓派 4 和 5 之外的所有，需要禁用 HDMI 输出才能启用复合输出。当未连接/检测到 HDMI 显示器时，HDMI 输出被禁用。设置 enable_tvout=0 以防止在禁用 HDMI 时启用复合输出。

要启用复合输出，请在 /boot/firmware/config.txt 的 dtoverlay=vc4-kms-v3d 行末尾附加 ,composite ：

```
dtoverlay=vc4-kms-v3d,composite
```

默认情况下，这将输出复合 NTSC 视频。要选择不同模式，请将以下内容添加到 /boot/firmware/cmdline.txt 中的单行中：

```
vc4.tv_norm=<video_mode>
```

用以下值替换 <video_mode> 占位符：

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

默认情况下，在检测到 I2C 总线上的树莓派触摸显示屏时使用。ignore_lcd=1 跳过此检测阶段。这可以防止使用 LCD 显示屏。

#### `disable_touchscreen`

启用和禁用触摸屏。

disable_touchscreen=1 禁用官方树莓派触摸显示屏的触摸屏组件。

### 一般显示选项

#### `disable_fw_kms_setup`

默认情况下，固件会解析任何连接的 HDMI 显示器的 EDID，选择适当的视频模式，然后通过内核命令行上的设置将模式的分辨率和帧率（以及超扫描参数）传递给 Linux 内核。在罕见情况下，固件可能会选择一个 EDID 中不存在的模式，这可能与设备不兼容。使用 disable_fw_kms_setup=1 可以禁用传递视频模式参数，从而避免此问题。Linux 视频模式系统（KMS）会自己解析 EDID 并选择适当的模式。

| NOTE | 在 Raspberry Pi 5 上，此参数默认为 1。|
| ------ | ----------------------------------------- |

## 相机设置

 在 GitHub 上编辑此内容

### `disable_camera_led`

将 disable_camera_led 设置为 1 可以防止录制视频或拍摄静态图片时红色相机 LED 灯亮起。例如，当相机面向窗户时，这对防止反光很有用。

### `awb_auto_is_greyworld`

将 awb_auto_is_greyworld 设置为 1 允许那些不内部支持灰色世界选项的库或应用程序捕捉使用 NoIR 相机拍摄的有效图像和视频。它将自动 awb 模式切换为使用灰色世界算法。这仅在 NoIR 相机需要时，或者高质量相机已经移除了红外滤镜，才需要这样做。
