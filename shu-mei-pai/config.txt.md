# `config.txt`

## `config.txt` 是什么？

树莓派设备没有使用传统 PC 上的 [BIOS](https://en.wikipedia.org/wiki/BIOS)，而是使用名为 `config.txt` 的配置文件。GPU 会在 Arm CPU 和 Linux 初始化之前读取 `config.txt`。树莓派系统（Raspberry Pi OS）会在位于 `/boot/firmware/` 的**启动分区**中查找此文件。

你可以直接在树莓派系统上编辑 `config.txt`。你也可以取下存储设备，在另一台计算机上编辑启动分区中的文件（包括 `config.txt`）。

对 `config.txt` 的修改只有在重启后才会生效。你可以使用以下命令查看当前生效的设置：

* `vcgencmd get_config <参数>`：显示指定的配置值，例如 `vcgencmd get_config arm_freq`
* `vcgencmd get_config int`：列出所有非零整数配置项
* `vcgencmd get_config str`：列出所有非空字符串配置项

>**注意**
>
>并非所有配置设置都能通过 `vcgencmd` 获取。

部分旧版 `config.txt` 参数已不再受官方支持。这些参数记录在[旧版 config.txt 参数](https://www.raspberrypi.com/documentation/computers/legacy_config_txt.html)中，未包含在本文中。

### 文件格式

`config.txt` 文件会由早期启动固件读取，因此所采取的文件格式非常简单：**每行一条语句：`属性=值`，其中 `值` 可以是整数或字符串。** 可以在行首添加字符 `#` 来插入注释，或注释掉现有配置值以禁用。

每行条目的最大长度为 98 个字符。树莓派系统会忽略掉所有溢出此限制的字符。

示例文件如下：

```bash
# 开启音频（加载 snd_bcm2835）
dtparam=audio=on

# 自动为检测到的摄像头加载叠加层
camera_auto_detect=1

# 自动为检测到的 DSI 显示屏加载叠加层
display_auto_detect=1

# 开启 DRM VC4 V3D 驱动
dtoverlay=vc4-kms-v3d
```

### 高级功能

#### `include`

在当前文件中插入指定文件的内容。

比如：把 `include extraconfig.txt` 这行添加到 `config.txt`，就会在 `config.txt` 文件中引用 `extraconfig.txt` 文件的内容。

>**注意**
>
>`bootcode.bin`、EEPROM 引导加载程序均不支持 `include` 指令。
>
>以下由引导加载程序处理的设置，只有在 `config.txt`（而非任何其他被引用的文件）中指定时才会生效：
>
>* `bootcode_delay`、
>* `gpu_mem`、`gpu_mem_256`、`gpu_mem_512`、`gpu_mem_1024`、
>* `total_mem`、
>* `sdram_freq`、
>* `start_x`、`start_debug`、`start_file`、`fixup_file`、
>* `uart_2ndstage`。

#### 条件筛选器

条件筛选器见[条件筛选器](https://www.raspberrypi.com/documentation/computers/config_txt.html#conditional-filters)一节。

## `autoboot.txt`

`autoboot.txt` 是一个可选的配置文件，放在初始启动分区中，用于指定 `boot_partition` 的编号。

该文件可与 `tryboot` 功能配合使用，为故障安全的操作系统升级实现 A/B 启动。这是引导加载程序和固件的原生能力，独立于第三方多系统启动管理器运行。

>**注意**
>
>`autoboot.txt` 只控制引导加载程序选择哪个启动分区。要构建一个有弹性、可用于生产环境的 A/B 更新系统，需要专门的分区布局（如冗余的启动分区和根文件系统）以及配套的更新工具。有关自动化方案，请参阅 [A/B Boot Update](https://www.raspberrypi.com/documentation/services/connect.html#remoteupdate-intro) 和 [rpi-image-gen](https://github.com/raspberrypi/rpi-image-gen) 工具。

`autoboot.txt` 支持 `[all]`、`[none]` 和 `[tryboot]` [条件筛选器](https://www.raspberrypi.com/documentation/computers/config_txt.html#conditional-filters)。

另见 [TRYBOOT](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#fail-safe-os-updates-tryboot) 启动流程。

### `boot_partition`

指定用于启动的分区号，除非分区号已经作为 `reboot` 命令的参数指定过（例如 `sudo reboot 2`）。

分区号从 `1` 开始。指定分区 `0` 会指示引导加载程序选择默认分区，默认分区解析为第一个可引导的 FAT 分区（通常是分区 1）。

可引导分区必须格式化为 FAT12、FAT16 或 FAT32，并包含 `start.elf` 文件（树莓派 5 上为 `config.txt` 文件），引导加载程序才会将其归类为可引导。

### 与 `cmdline.txt` 的关系及根文件系统选择

引导加载程序只读取 `autoboot.txt` 来定位目标启动分区。它不会解析 `cmdline.txt`，也不会对其做任何处理，只是把其中的参数传递给操作系统内核。

根分区选择（`root=...`）由内核通过 `cmdline.txt` 处理。在双槽位 A/B 系统中，每个启动分区通常包含各自独立的 `cmdline.txt` 文件，指向对应的根分区。或者，如果每个启动分区使用相同的文件，你可以在 `config.txt` 中使用 `[boot_partition=N]` 条件筛选器来选择备用的 `cmdline.txt`：

```bash
[boot_partition=2]
cmdline=cmdline_rootfs_a.txt

[boot_partition=3]
cmdline=cmdline_rootfs_b.txt
```

### `tryboot_a_b`

将此属性置为 `1`，当设置了 `tryboot` 标志时，会加载正常的 `config.txt` 和 `boot.img` 文件，而不是 `tryboot.txt` 和 `tryboot.img`。

这样就可以在分区级（而非文件级）进行 `tryboot` 切换，无需修改 A/B 分区中的配置文件。

### A/B 启动的更新流程示例

考虑如下的 A/B 分区布局：

* **分区 1（FAT）：** 包含 `autoboot.txt` 的初始引导加载程序分区。
* **分区 2（FAT）：** 槽位 A 启动分区（`boot_partition=2`），包含固件、内核，以及指向根 A 的 `cmdline.txt`。
* **分区 3（FAT）：** 槽位 B 启动分区（`boot_partition=3`），包含固件、内核，以及指向根 B 的 `cmdline.txt`。
* **分区 4：** 槽位 A 根文件系统分区（根 A）。
* **分区 5：** 槽位 B 根文件系统分区（根 B）。
* **分区 6：** 可选的持久化数据分区。

初始 `autoboot.txt`：

```bash
[all]
tryboot_a_b=1
boot_partition=2
[tryboot]
boot_partition=3
```

#### 安装更新

系统默认从分区 2 启动。然后，假想的更新服务会：

1. 把下一版操作系统安装到分区 3（及其对应的根分区）。
2. 通过执行 tryboot 重启来测试更新：

```bash
$ sudo reboot "0 tryboot"
```

#### 提交或取消更新

系统会从分区 3 启动，因为 `autoboot.txt` 中的 `[tryboot]` 筛选器求值为真。

如果 `tryboot` 处于激活状态（`/proc/device-tree/chosen/bootloader/tryboot` 等于 `1`），并且我们从 tryboot 分区启动（`/proc/device-tree/chosen/bootloader/partition` 与 `autoboot.txt` 的 `[tryboot]` 部分中设置的 `boot_partition` 匹配）：
   * 假想的更新服务随后会验证系统健康状况。
     * **如果成功：** 更新 `autoboot.txt`，交换默认分区和 tryboot 分区，提交更新。
     * **如果失败：** 执行正常重启，不修改 `autoboot.txt`。`tryboot` 标志会被自动清除，系统将恢复为从分区 2 启动。

提交更新后的 `autoboot.txt`：

```bash
[all]
tryboot_a_b=1
boot_partition=3
[tryboot]
boot_partition=2
```

>**技巧**
>
>位于 `/proc/device-tree/chosen/bootloader/` 下的属性（如 `tryboot` 和 `partition`）以原始的 32 位大端二进制整数存储。用 `cat` 之类的工具查看时会出现不可打印字符，或者看起来是空白的。要在 shell 脚本中读取这些整数值，请使用：
>
>```bash
>printf "%d\n" "0x$(od /proc/device-tree/chosen/bootloader/tryboot -v -An -t x1 | tr -d ' ')"
>```

## 常见参数

### 常见显示参数

#### `hdmi_enable_4kp60`

>**注意**
>
>此参数仅适用于树莓派 4B、计算模块 4、计算模块 4S 和树莓派 400。

默认情况下，接入 4K 显示器时，受影响的型号会选择 30 Hz 刷新率。使用此参数可允许选择 60 Hz 刷新率。受此设置影响的型号仅在 HDMI0 上支持 4Kp60 输出。启用此设置会增加功耗和温度。

### 常见硬件配置参数

#### `camera_auto_detect`

默认情况下，树莓派系统会在 `/boot/firmware/config.txt` 中包含一行启用此设置的配置。

启用后，固件会自动为识别到的 CSI 摄像头加载叠加层。

要禁用，请设置 `camera_auto_detect=0`（或删除 `camera_auto_detect=1`）。

#### `display_auto_detect`

默认情况下，树莓派系统会在 `/boot/firmware/config.txt` 中包含一行启用此设置的配置。

启用后，固件会自动为识别到的 DSI 显示屏加载叠加层。

要禁用，请设置 `display_auto_detect=0`（或删除 `display_auto_detect=1`）。

#### `dtoverlay`

`dtoverlay` 参数会要求固件加载指定的设备树覆盖层——这是一个配置文件，可启用内核对内置和外部硬件的支持。例如，`dtoverlay=vc4-kms-v3d` 会加载叠加层，启用内核图形驱动程序。

作为特例，如果在调用时不带值（即 `dtoverlay=`），该参数会标记叠加层参数列表的结束。如果用在任何其他 `dtoverlay` 或 `dtparam` 设置之前，它会阻止加载任何扩展板叠加层。

更多信息请参阅 [DTB、叠加层和 `config.txt`](https://www.raspberrypi.com/documentation/computers/configuration.html#part3.1)。

#### `dtparam`

树莓派设备的设备树配置文件支持多种参数，例如启用 I²C、SPI 接口。许多 DT 叠加层也都能用参数进行配置。这两类参数都可以通过 `dtparam` 设置提供。此外，还可以把叠加层参数以逗号分隔追加到 `dtoverlay` 参数之后，但请注意 98 个字符的行长限制。

欲了解更多详情，请查阅 [DTB、叠加层和 `config.txt`](https://www.raspberrypi.com/documentation/computers/configuration.html#part3.1)。

#### `arm_boost`

>**注意**
>
>此参数仅适用于搭载两相供电的较新树莓派 4B 修订版，以及所有修订版的树莓派 400。

默认情况下，树莓派系统会在 `/boot/firmware/config.txt` 中包含一行配置，在受支持的设备上启用此设置。

部分树莓派设备的 SoC 电压轨配有第二个开关电源。启用后，默认超频模式的主频会从 1.5 GHz 提升到 1.8 GHz。

要禁用，请设置 `arm_boost=0`。

#### `power_force_3v3_pwm`

>**注意**
>
>此参数仅适用于树莓派 5、500、500+ 和计算模块 5。

强制 GPIO 排针或 CSI 连接器输出的 3.3V 使用 PWM。

要禁用，请设置 `power_force_3v3_pwm=0`。

## 板载模拟音频（3.5 mm 插孔）

使用配置参数可以修改板载音频输出的模拟音频驱动方式，以及是否启用某些固件功能。

### `audio_pwm_mode`

`audio_pwm_mode=1` 选择传统低质量模拟音频，基于 3.5 mm AV 端子。

`audio_pwm_mode=2` 选择使用高级调制方案的高质量模拟音频。（默认）

>**注意**
>
>此参数将占用更多的 GPU 计算资源，可能会对某些型号的特定用例造成影响。

### `disable_audio_dither`

在默认情况下，如果音频流路由输出到了模拟音频，则会应用 1.0LSB 抖动。在某些情况下（如 ALSA 音量处于较低水平），就有可能产生可闻的背景嘶声。将 `disable_audio_dither` 置为 `1` 可禁用抖动功能。

### `enable_audio_dither`

当音频样本大于 16 位时，通常就会禁用音频抖动（请参阅上述 `disable_audio_dither`）。将此参数置为 `1` 可强制对所有位深度都应用抖动。

### `pwm_sample_bits`

命令 `pwm_sample_bits` 能调整模拟音频输出的位深度。默认位深度为 `11`。位深度设置低于 `8` 会导致音频无法工作，因为低于 `8` 的设置会导致 PLL 频率过低，无法支持。该参数通常仅用于演示位深度对量化噪声的影响。

## HDMI 音频

在默认情况下，所有搭载 HDMI 输出接口的树莓派型号均启用了 HDMI 音频输出。

要禁用 HDMI 音频输出，请在 `/boot/firmware/config.txt` 中的 `dtoverlay=vc4-kms-v3d` 这行末尾添加 `,noaudio`：

```bash
dtoverlay=vc4-kms-v3d,noaudio
```

## 启动参数

### `start_file`、`fixup_file`

这些参数可指定：在启动前传给 VideoCore GPU 的固件文件。

`start_file` 指定要使用的 VideoCore 固件文件。`fixup_file` 用于修正 `start_file` 所使用的内存位置，以匹配 GPU 内存分配。

`start_file` 和 `fixup_file` 是一对必须匹配的文件：搭配错误将导致开发板无法启动。这是个高级参数，因此我们建议你使用 `start_x` 和 `start_debug`，而不是此参数。

>**注意**
>
>无法以这种方式选择精简固件（`start*cd.elf` 和 `fixup*cd.dat`）——系统将无法启动。启用精简固件的唯一方法是指定 `gpu_mem=16`。精简固件移除了对编解码器、3D 和调试日志的支持，并把初始早期引导帧缓冲区限制为 1080p @16bpp——不过与其他固件一样，KMS 可以在后续阶段用最高 32bpp 的 4K 帧缓冲区取而代之。

>**注意**
>
>树莓派 5、500、500+ 和计算模块 5 的固件内置于引导加载程序 EEPROM 中。

### `cmdline`

`cmdline` 是启动分区上的一个备用文件名，用于从中读取内核命令行字符串；默认值为 `cmdline.txt`。

### `kernel`

`kernel` 是用于加载内核的启动分区上的一个备用文件名。树莓派 1、Zero、Zero W 和计算模块 1 的默认值为 `kernel.img`。树莓派 2、3、3+、Zero 2 W 和计算模块 3、3+ 的默认值为 `kernel7.img`。树莓派 4、400 和计算模块 4 的默认值为 `kernel8.img`；如将 `arm_64bit` 置为 0，则默认值为 `kernel7l.img`。

树莓派 5、500、500+ 和计算模块 5 的固件默认加载 `kernel_2712.img`，因为此镜像包含针对这些机型的优化（例如 16K 页大小）。如果此文件不存在，则会改为加载通用 64 位内核（`kernel8.img`）。

### `arm_64bit`

如果置为 1，内核将以 64 位模式启动。置为 0 则选择 32 位模式。

在 64 位模式下，固件会选择合适的内核（例如 `kernel8.img`），除非显式定义了 `kernel` 参数——此时将使用显式指定的内核。

在树莓派 4、400 和计算模块 4、4S 平台上默认值为 1；在所有其他平台上默认值为 0。但是，如果显式设置的 `kernel` 参数中给定的名称与已知的任一内核匹配，`arm_64bit` 会相应设置。

64 位内核有以下两种形式：

* 未压缩的镜像文件
* 镜像的 gzip 压缩包

两种形式都可以使用 `img` 文件扩展名；引导加载程序通过文件开头的签名字节识别压缩包。

以下树莓派型号支持此标志：

* 2B rev 1.2
* 3B
* 3A+
* 3B+
* 4B
* 400
* Zero 2 W
* 计算模块 3
* 计算模块 3+
* 计算模块 4
* 计算模块 4S

自树莓派 5 起的旗舰机型、自 CM5 起的计算模块以及自树莓派 500 起的键盘系列机型_仅_支持 64 位内核。仅支持 64 位内核的型号会忽略此标志。

### `armstub`

`armstub` 是启动分区上用于加载 Arm stub 的文件名。默认的 Arm stub 存储在固件中，会根据树莓派型号和各种设置自动选择。

stub 是在内核之前运行的一小段 Arm 代码。它的职责是设置中断控制器等底层硬件，然后将控制权交给内核。

### `ramfsfile`

`ramfsfile` 是启动分区上的 `ramfs` 的一个可选文件名。

>**注意**
>
>新版固件可加载多个 `ramfs` 文件。请注意：多个文件名需以逗号分隔，不要超过 80 个字符的行长限制。所有已加载的文件在内存中拼接在一起，被视为单个 `ramfs` 二进制块。有关更多信息，请参阅[论坛](https://forums.raspberrypi.com/viewtopic.php?f=63&t=10532)。

### `ramfsaddr`

`ramfsaddr` 指定 `ramfsfile` 将加载到的内存地址。

### `initramfs`

>**注意**
>
>构建和更新 `initramfs` 被视为只有经验丰富的用户才会尝试的高级技术。树莓派官方不对其提供支持，因此我们也不提供相关说明。

命令 `initramfs` 同时指定了 ramfs 的文件名**和**它将加载到的内存地址。它在一个参数中同时执行了 `ramfsfile` 和 `ramfsaddr` 的操作。地址也可以是 `followkernel`（或 `0`），将其放置在内核镜像之后的内存中。示例值为：`initramfs initramf.gz 0x00800000`、`initramfs init.gz followkernel`。同 `ramfsfile` 一样，新版固件可加载多个文件，多个文件名以逗号分隔。

>**注意**
>
>参数 `initramfs` 使用的语法与其他所有参数不同，你不能在此处使用字符 `=`。

### `auto_initramfs`

如果将 `auto_initramfs` 置为 `1`，固件会查找与内核匹配的 `initramfs` 文件。该文件必须与内核镜像位于同一位置，名称由内核名派生：把 `kernel` 前缀替换为 `initramfs`，并去掉 `.img` 之类的扩展名。例如，`kernel8.img` 需要 `initramfs8`。只要自定义内核名分别以 `kernel` 和 `initramfs` 开头且其余部分一致（除了 initramfs 不带文件扩展名），你也可以在自定义内核名下使用 `auto_initramfs`。否则，就需要显式的 [`initramfs`](https://www.raspberrypi.com/documentation/computers/config_txt.html#initramfs) 语句。

### `disable_poe_fan`

在默认情况下，即使并未接入 PoE 扩展板，启动时也会在 I²C 总线上进行探测。将此参数置为 1，可禁用通过 I²C（在 `ID_SD` 和 `ID_SC` 引脚上）对 PoE 扩展板风扇的控制。如果你不打算使用 PoE 扩展板，那么这是缩短启动时间的有效方式。

### `disable_splash`

如果将 `disable_splash` 置为 `1`，启动时将不会显示彩虹屏。默认值为 `0`。

### `enable_uart`

`enable_uart=1`（与 `cmdline.txt` 中的 `console=serial0,115200` 配合使用）能让内核创建一个串口控制台，可使用 GPIO 14 和 15（40 针排针上的引脚 8 和引脚 10）访问。编辑 `cmdline.txt`，删除 `quiet` 字段，就能把内核的启动消息也输出到这个串口上。另请参阅 `uart_2ndstage`。

### `force_eeprom_read`

将此参数置为 `0`，可阻止固件在上电时读取 I²C 扩展板 EEPROM（连接至 `ID_SD` 和 `ID_SC` 引脚）。另请参阅 [`disable_poe_fan`](https://www.raspberrypi.com/documentation/computers/config_txt.html#disable_poe_fan)。

### `os_prefix`

`os_prefix` 是可选配置，能让你在同一张卡上安装的多个内核和设备树文件版本之间进行选择。`os_prefix` 中的任何值都会前置到固件加载的所有操作系统文件名之前，其中“操作系统文件”是指内核、`initramfs`、`cmdline.txt`、`.dtbs` 和叠加层。该前缀通常是目录名，但也可以是文件名的一部分，比如 “test-”。因此，目录前缀必须以字符 `/` 结尾。

为了降低系统无法启动的概率，固件会先测试所提供的前缀值是否可行——除非能在新位置/新名称下找到所需的内核和 .dtb 文件，否则前缀会被忽略（置为 “”）。对叠加层有一个特殊的可行性测试：只有当 `${os_prefix}${overlay_prefix}README` 存在时，才会从 `${os_prefix}${overlay_prefix}` 加载叠加层（其中 [`overlay_prefix`](https://www.raspberrypi.com/documentation/computers/config_txt.html#overlay_prefix) 的默认值为 “overlays/”）；否则固件会忽略 `os_prefix`，把叠加层当作共享的。

（固件在检查前缀时判断的是关键文件（而非目录）是否存在，原因有二：前缀可能不是目录，而且并非所有启动方式都支持测试目录是否存在。）

>**注意**
>
>任何用户指定的操作系统文件都可以使用绝对路径（相对于启动分区）绕过所有前缀——只需让文件路径以 `/` 开头，例如 `kernel=/my_common_kernel.img`。

另请参阅 [`overlay_prefix`](https://www.raspberrypi.com/documentation/computers/config_txt.html#overlay_prefix) 和 [`upstream_kernel`](https://www.raspberrypi.com/documentation/computers/legacy_config_txt.html#upstream_kernel)。

### `otg_mode`（仅适用于树莓派 4）

USB On-The-Go（通常缩写为 OTG）是一项功能，让支持的 USB 设备通过相应的 OTG 线把自己配置成 USB 主机。在较旧的树莓派设备上，一个 USB 2.0 控制器同时用于 USB 主机模式和设备模式。

树莓派 4B 及后续机型、树莓派 400 及后续机型的主 USB 端口由一个通过 PCIe 连接的高性能 USB 3.0 控制器驱动。旧版 USB 2.0 控制器在 USB-C 电源接口上仍然可用，作设备模式使用（`otg_mode=0`，默认值）。树莓派计算模块 4 及更早的型号没有 USB 3.0 控制器。

`otg_mode=1` 要求在该 USB-C 连接器上使用能力更强的 XHCI USB 2.0 控制器作为替代主机控制器。

>**注意**
>
>默认情况下，树莓派系统在 `/boot/firmware/config.txt` 中包含一行配置，在计算模块 4 上启用此设置。

### `overlay_prefix`

指定从哪个子目录/前缀加载叠加层，默认为 `overlays/`（注意末尾的 `/`）。如果与 [`os_prefix`](https://www.raspberrypi.com/documentation/computers/config_txt.html#os_prefix) 同时使用，则 `os_prefix` 位于 `overlay_prefix` 之前；例如 `dtoverlay=disable-bt` 会尝试加载 `${os_prefix}${overlay_prefix}disable-bt.dtbo`。

>**注意**
>
>除非存在 `${os_prefix}${overlay_prefix}README`，否则叠加层将与主操作系统共享（即忽略 `os_prefix`）。

### 配置属性

树莓派 5 需要存在一个 `config.txt` 文件来标识分区可启动。

#### `boot_ramdisk`

如果此属性置为 `1`，则引导加载程序会尝试加载名为 `boot.img` 的 ramdisk 文件，其中包含[引导文件系统](https://www.raspberrypi.com/documentation/computers/configuration.html#boot-folder-contents)。随后的文件（例如 `start4.elf`）将从 ramdisk 中读取，而非原始引导文件系统。

`boot_ramdisk` 的主要目的是支持安全启动（`secure-boot`），但未签名的 `boot.img` 文件也可用于网络引导或 `RPIBOOT` 配置。

* 对于树莓派 4 及后续机型，ramdisk 文件的最大尺寸为 180 MB；更早的设备为 128 MB。不过，在内存有限的设备（例如 256 MB）上，我们建议使用较小的 ramdisk 文件，例如 32 MB。
* `boot.img` 文件是裸磁盘 `.img` 文件。推荐格式是不带 MBR 的普通 FAT32 分区。
* ramdisk 文件系统的内存在操作系统启动之前释放。
* 如果选择了 [TRYBOOT](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#fail-safe-os-updates-tryboot)，则引导加载程序将搜索 `tryboot.img` 而非 `boot.img`。
* 另请参阅 [autoboot.txt](https://www.raspberrypi.com/documentation/computers/config_txt.html#autoboot-txt)。

更多有关安全启动（`secure-boot`）和创建 `boot.img` 文件的信息，请参阅 [USBBOOT](https://github.com/raspberrypi/usbboot/blob/master/Readme.md)。

默认值：`0`

#### `boot_load_flags`

定制固件（裸机）的实验性属性。

位 0（0x1）表示 `.elf` 文件为定制固件。这会禁用所有兼容性检查（例如是否支持 USB MSD 启动），并在启动可执行文件之前复位 PCIe。

对树莓派 5 无关紧要，因为它没有 `start.elf` 文件。

默认值：`0x0`

#### `enable_rp1_uart`

仅适用于树莓派 5。

置为 `1` 时，固件会将 RP1 UART0 初始化为 115200 bps，并且在启动操作系统之前不复位 RP1（可通过 `pciex4_reset=1` 单独配置）。这使得在早期启动代码中（例如裸机调试期间）更容易从 40 针排针获取 UART 输出。

默认值：`0x0`

#### `pciex4_reset`

仅适用于树莓派 5。

默认情况下，在启动操作系统之前，会对 `RP1` 使用的 PCIe x4 控制器进行复位。如果此参数置为 `0`，则禁用复位，让操作系统或裸机代码继承来自引导加载程序的 PCIe 配置设置。

默认值：`1`

#### `sha256`

如果置为非零值，则启用对已加载文件（内核、initramfs、设备树 .dtb 文件和叠加层）的 SHA256 哈希日志记录，格式与 `sha256sum` 工具生成的相同。如果启用了 UART，日志输出到 UART，也可以通过 `sudo vclog --msg` 查看。此参数在调试启动问题时很有用，但代价是可能给启动时间增加_许多_秒。在所有平台上默认值为 0。

#### `uart_2ndstage`

如果 `uart_2ndstage` 为 `1`，则启用到 UART 的调试日志记录。此参数还会自动启用 `start.elf` 中的 UART 日志记录。这也在[启动参数](https://www.raspberrypi.com/documentation/computers/config_txt.html#boot-options)页上有描述。

属性 `BOOT_UART` 也会启用引导加载程序的 UART 日志记录，但不会启用 `start.elf` 的 UART 日志记录——除非同时设置了 `uart_2ndstage=1`。

默认值：`0`

#### `erase_eeprom`

如果 `erase_eeprom` 置为 `1`，那么 `recovery.bin` 将擦除整个 SPI EEPROM，而非刷写引导加载程序镜像。此属性在正常启动期间无效。

默认值：`0`

#### `set_reboot_arg1`

仅适用于树莓派 5。

设置 `boot_arg1` 的值，在重启后通过防复位寄存器传递给引导加载程序。更多详情请参阅 [`boot_arg1`](https://www.raspberrypi.com/documentation/computers/config_txt.html#boot_arg1)。

要在运行时设置重启参数而不编辑 `config.txt`，可以使用 `vcmailbox`。例如，在下次重启时把 `boot_arg1` 设置为 `42`：

```bash
$ sudo vcmailbox 0x0003808c 8 8 1 42
```

默认值：（空）

#### `set_reboot_order`

仅适用于树莓派 5。

设置 [BOOT_ORDER](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#BOOT_ORDER) 的值，在重启后通过防复位寄存器传递给引导加载程序。与 `tryboot` 一样，这是一次性设置，使用后会自动清除。

此属性可用于调试不同的 [BOOT_ORDER](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#BOOT_ORDER) 设置。或者，在同时控制电源和 `nRPIBOOT` GPIO 的配置系统中，可用它来覆盖启动模式，而无需在 EEPROM 配置中指定[条件筛选器](https://www.raspberrypi.com/documentation/computers/config_txt.html#conditional-filters)语句。

要在运行时设置重启顺序而不编辑 `config.txt`，可以使用 `vcmailbox`。例如，测试下次重启时的网络启动：

```bash
$ sudo vcmailbox 0x0003808b 4 4 0xf4612
$ sudo reboot
```

默认值：（空）

#### `kernel_watchdog_timeout`

如果置为非零值（单位为秒），此属性会启用一个硬件看门狗定时器，并在启动时移交给操作系统（OS）。如果操作系统不定期“喂狗”（kick）或重置看门狗，系统将在指定的超时时间后复位。

此属性设置 `systemd` 的 `watchdog.open_timeout` 参数，该参数控制操作系统有多少时间来完成初始化并开始服务看门狗。该值通过内核命令行传递给操作系统。对于持续运行，操作系统还必须定期重置看门狗，这通常由 `systemd` 中的 `RuntimeWatchdogSec` 参数控制。更多信息请参阅 [systemd 看门狗文档](https://www.freedesktop.org/software/systemd/man/latest/systemd-system.conf.html#RuntimeWatchdogSec=)。

>**注意**
>
>在树莓派系统 _Bookworm_ 上，`RuntimeWatchdogSec` 参数**默认未启用**，必须先在 `/etc/systemd/system.conf` 中配置，固件内核看门狗才能使用。
>
>如果 `BOOT_WATCHDOG_TIMEOUT`（EEPROM/引导加载程序设置，仅在树莓派 4 和 5 上支持）和 `kernel_watchdog_timeout` 都已设置，引导加载程序会在操作系统启动时无缝地从引导加载程序看门狗切换到内核看门狗。这提供了从上电到操作系统运行时的连续看门狗覆盖。
>
>建议使用 `kernel_watchdog_timeout` 而不是 `dtparam=watchdog`，因为 `kernel_watchdog_timeout` 会显式设置 `open_timeout` 参数，确保看门狗在 systemd 接管之前保持激活。

这有助于确保系统在启动过程完成后，能够从操作系统的挂起或崩溃中恢复。

默认值：`0`（禁用）

#### `kernel_watchdog_partition`

如果内核看门狗触发（即操作系统未能在超时时间内重置看门狗），此属性指定复位后从哪个分区启动。这样可以自动故障转移到恢复分区或备用分区。

你可以将它与[表达式筛选器](https://www.raspberrypi.com/documentation/computers/config_txt.html#the-expression-filter)结合使用，在看门狗触发重启到特定分区时，应用不同的设置或选择不同的启动流程。

另请参阅 [PARTITION](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#PARTITION) 属性，了解如何使用高分区号来检测看门狗触发。

默认值：`0`（默认分区）

#### `eeprom_write_protect`

配置 EEPROM 写状态寄存器（`write status register`）。可将整个 EEPROM 标记为写保护，或清除写保护。

该参数必须与控制 EEPROM 写状态寄存器更新的 EEPROM `/WP` 引脚配合使用。将 `/WP` 引脚拉低（CM4 上为 `EEPROM_nWP`，树莓派 4 上为 `TP5`）并不会对 EEPROM 写保护，除非写状态寄存器也进行了配置。

可查看 [Winbond W25x40cl](https://www.winbond.com/resource-files/w25x40cl_f%2020140325.pdf)、[Winbond W25Q16JV](https://www.winbond.com/hq/product/code-storage-flash-memory/serial-nor-flash/?__locale=en&partNo=W25Q16JV) 的数据手册以获取更多详细信息。

`config.txt` 中的 `eeprom_write_protect` 设置用于 `recovery.bin`。

| 值 | 说明 |
| :----: | :-----------------------------------: |
| `1` | 将写保护区域配置为覆盖整个 EEPROM。 |
| `0` | 清除写保护区域。 |
| `-1` | 什么也不做。 |

>**注意**
>
>`flashrom` 不能清除写保护区域，如果定义了写保护区域，它将无法更新 EEPROM。

对于树莓派 5，在默认情况下 `/WP` 已拉低，因此只要配置了写状态寄存器，就会启用写保护。要清除写保护，请将 `/WP` 引脚拉高，方法是连接 `TP14` 和 `TP1`。

默认值：`-1`

#### `os_check`

对于树莓派 5，在尝试从当前分区引导之前，固件会自动检查是否存在兼容的设备树文件。否则，较旧的不兼容内核会被加载，然后卡死。要禁用此检查（例如用于裸机开发），请在 `config.txt` 中设置 `os_check=0`。

默认值：`1`

#### `bootloader_update`

可将此参数置为 0，在不更新 EEPROM 配置的情况下阻止自更新。在通过网络引导更新多个树莓派设备时，这有时很有用，因为可以针对每个树莓派单独控制此参数（例如，通过 `config.txt` 中的串号筛选器）。

默认值：`1`

### 安全启动的配置属性

##### 白皮书

>[如何使用树莓派安全启动（How to use Raspberry Pi Secure Boot）](https://pip.raspberrypi.com/documents/RP-003466-WP)
>
>本白皮书介绍如何在基于树莓派 4 的设备上实现安全启动。有关我们实施安全启动方法的概述，请参阅[树莓派 4 启动安全（Raspberry Pi 4 Boot Security）](https://pip.raspberrypi.com/documents/RP-004651-WP)白皮书。安全启动系统旨在与自定义操作系统镜像搭配使用，例如用 `rpi-image-gen` 或 `buildroot` 生成的镜像。不建议将其与树莓派系统搭配使用。

以下 `config.txt` 属性用于编程安全启动的 OTP 设置。这些更改不可逆，只能在刷写引导加载程序 EEPROM 镜像时通过 `RPIBOOT` 进行编程。这确保了安全启动无法被远程设置，也不会因意外插入旧的存储卡镜像而被设置。

更多有关启用安全启动的信息，请参阅以下资源：

* [USBBOOT](https://github.com/raspberrypi/usbboot) 存储库中的[安全启动 readme 文件](https://github.com/raspberrypi/usbboot/blob/master/Readme.md#secure-boot)和[安全启动教程](https://github.com/raspberrypi/usbboot/blob/master/secure-boot-example/README.md)。
* [安全启动信任链](https://www.raspberrypi.com/documentation/security/security-architecture.html#secure-boot-chain-of-trust)。
* [安全启动配置器（`rpi-sb-provisioner`）](https://www.raspberrypi.com/documentation/security/secure-boot-provisioner.html)。

#### `program_pubkey`

如果将此属性置为 `1`，则 `recovery.bin` 将把 EEPROM 镜像中的公钥哈希值写入 OTP。设置后，引导加载程序将拒绝使用不同 RSA 密钥签名的 EEPROM 镜像及未签名的镜像。

默认值：`0`

#### `revoke_devkey`

仅适用于树莓派 4。

如果将此属性置为 `1`，则 `recovery.bin` 将向 OTP 写入一个值，阻止 ROM 加载不支持安全启动的旧版本二级引导加载程序。这可以防止通过回滚到旧版引导加载程序来关闭安全启动。因此，在生产设备上启用安全启动时必须设置此属性。

自 `recovery.bin` 发布版本 `2025/05/16` 及更高版本起，若设置了 `program_pubkey=1`，此属性会被自动设置。

默认值：`0`

#### `program_rpiboot_gpio`

仅适用于树莓派 4B 和树莓派 400。

计算模块 4 和 4S 有专用的 `nRPIBOOT` 跳线用于选择 `RPIBOOT` 模式。树莓派 4B 和树莓派 400 没有专用的 `nRPIBOOT` 跳线，因此必须从以下 GPIO 中选择一个用作 `nRPIBOOT`：

* `2`
* `4`
* `5`
* `6`
* `7`
* `8`

操作系统启动后，你可以将该 GPIO 用作通用 I/O 引脚。但是，你应当确认该 GPIO 配置不会与可能在启动期间把该 GPIO 拉低的扩展板冲突。

虽然 `secure-boot` 要求在树莓派 4B 和树莓派 400 上设置此属性，但它并不依赖 `secure-boot`。例如，`RPIBOOT` 对自动化测试很有用。

出于安全考虑，此 OTP 值_只能_通过 `RPIBOOT` 编程。因此，你必须先使用 `erase_eeprom` 清空引导加载程序 EEPROM。空白的 EEPROM 会让 ROM 故障转移到 `RPIBOOT` 模式，随后才能设置此参数。

默认值：（空）

#### `program_jtag_lock`

如果将此属性置为 `1`，则 `recovery.bin` 将编程一个 OTP 值，阻止 VideoCore JTAG 被使用。此参数要求同时设置 `program_pubkey` 和 `revoke_devkey`。此参数会妨碍故障分析，应仅在设备经过全面测试后设置。

默认值：`0`

## GPIO 控制

### `gpio`

`gpio` 指令能在启动时把 GPIO 引脚设置为特定模式和特定值，这种方式在以前需要一个自定义的 `dt-blob.bin` 文件。每一行都会把相同的设置（或至少做出相同的更改）应用到一组引脚，可以指定单个引脚（`3`）、一段引脚区间（`3-4`），或以逗号分隔的列表（`3-4,6,8`）。

引脚设置后跟一个 `=` 和此列表中的一个或多个以逗号分隔的属性：

* `ip`——输入
* `op`——输出
* `a0-a5`——Alt0-Alt5
* `dh`——驱动高电平（用于输出）
* `dl`——驱动低电平（用于输出）
* `pu`——上拉
* `pd`——下拉
* `pn/np`——无拉取

`gpio` 设置将按顺序应用，因此后面出现的设置会覆盖先前出现的设置。

示例：

```bash
# 将 GPIO 引脚 0-27 配置成 Alt2 模式（用于 DPI24）
gpio=0-27=a2

# 将 GPIO12 设置为输出模式，并将其状态设为 1
gpio=12=op,dh

# 更改引脚 18、引脚 20 的上拉、下拉配置（引脚为输入）。
gpio=18,20=pu

# 将引脚 17-21 设置为输入。
gpio=17-21=ip
```

`config.txt` 中的条件筛选器“\[...\]”兼容该 `gpio` 指令，因此可以根据型号、序列号和 EDID 使用不同的设置。

通过该机制进行的 GPIO 修改不会直接影响内核。它们不会把 GPIO 引脚暴露到 `sysfs` 接口，并且可被设备树中的 `pinctrl` 条目以及 `pinctrl` 之类的工具覆盖。

还请注意，从上电到修改生效会有几秒钟的延迟——如果通过网络启动或从 USB 大容量存储设备启动，延迟会更长。

### `enable_jtag_gpio`

设置 `enable_jtag_gpio=1` 会为 GPIO 引脚 22-27 选择 Alt4 模式，并建立一些 SoC 内部连接，为 Arm CPU 启用 JTAG 接口。它适用于所有型号的树莓派。

| 引脚号 | 功能 |
| :----: | :----: |
| GPIO22 | `ARM_TRST` |
| GPIO23 | `ARM_RTCK` |
| GPIO24 | `ARM_TDO` |
| GPIO25 | `ARM_TCK` |
| GPIO26 | `ARM_TDI` |
| GPIO27 | `ARM_TMS` |

## 超频参数

内核带有 [CPUFreq](https://www.kernel.org/doc/html/latest/admin-guide/pm/cpufreq.html) 驱动程序，默认启用 powersave 调度器；安装 [raspi-config](https://www.raspberrypi.com/documentation/computers/configuration.html#raspi-config) 后，启动时会切换为按需（on-demand）调度。在按需调度下，CPU 频率会随处理器负载变化。你可以用 `*_min` 配置参数调整最小值，也可以通过应用静态调频调度器（powersave 或 performance）或设置 `force_turbo=1` 来禁用动态调频。

当 SoC 运行时达到 `temp_limit`（见下文，默认为 85°C）时，超频和过压会被禁用，以便给 SoC 降温。在树莓派 1 和树莓派 2 上你不太可能触及这个限制，但在树莓派 3 及更新机型上更容易遇到。检测到欠压情况时，超频和过压也会被禁用。

>**注意**
>
>更多信息请参阅[频率管理和热控制部分](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#frequency-management-and-thermal-control)。

>**警告**
>
>将任意超频参数设置为非 [raspi-config](https://www.raspberrypi.com/documentation/computers/configuration.html#overclock) 所用的值，可能会导致在 SoC 内部置一个永久位。这将使你的树莓派曾经超频过这一事实变得可检测。当 `force_turbo` 置为 `1` 且任一 `over_voltage_*` 参数置为大于 `0` 的值时，就会设置超频位。详细信息请查看有关[超频模式的博客文章](https://www.raspberrypi.com/news/introducing-turbo-mode-up-to-50-more-performance-for-free/)。

### 超频

| 参数 | 说明 |
| :------: | ---------------------------------------------------------------------------- |
| `arm_freq` | Arm CPU 的频率（MHz）。 |
| `arm_boost` | 将 `arm_freq` 提升到该主板类型和固件所支持的最高频率。置为 `1` 启用。 |
| `gpu_freq` | 一并设置 `core_freq`、`h264_freq`、`isp_freq`、`v3d_freq` 和 `hevc_freq`。 |
| `core_freq` | GPU 处理器核心的频率（MHz）。会影响 CPU 性能，因为它驱动着 L2 缓存和内存总线；L2 缓存只让树莓派 Zero/Zero W/树莓派 1 受益；对树莓派 2、3 上的 SDRAM 也有小幅好处。关于在树莓派 4 上的使用，请参见下文小节。 |
| `h264_freq` | 硬件视频模块的频率（MHz）；单独覆盖 `gpu_freq` 设置。 |
| `isp_freq` | 图像传感器管道模块的频率（MHz）；单独覆盖 `gpu_freq` 设置。 |
| `v3d_freq` | 3D 模块的频率（MHz）；单独覆盖 `gpu_freq` 设置。在树莓派 5 上，V3D 独立于 `core_freq`、`isp_freq` 和 `hevc_freq`。 |
| `hevc_freq` | 高效视频编解码器模块的频率（MHz）；单独覆盖 `gpu_freq` 设置。仅适用于树莓派 4。 |
| `sdram_freq` | SDRAM 的频率（MHz）。不支持在树莓派 4 及更新机型上对 SDRAM 超频。 |
| `over_voltage` | CPU/GPU 核心电压上限。数值应位于区间 [-16,8]，相当于区间 [0.95V,1.55V]（树莓派 1 为 [0.8,1.4V]），步长为 0.025V。换言之，设定 -16 将把 CPU/GPU 核心电压的最大值变为 0.95V（树莓派 1 为 0.8V）；设定 8 将允许高达 1.55V（树莓派 1 为 1.4V）。默认值见下表。只有指定 `force_turbo=1` 时才允许高于 6 的值：如果同时设定 `over_voltage_*` > `0`，则会设置保修位。 |
| `over_voltage_sdram` | 一并设置 `over_voltage_sdram_c`、`over_voltage_sdram_i` 和 `over_voltage_sdram_p`。 |
| `over_voltage_sdram_c` | 调整 SDRAM 控制器电压。[-16,8] 等同于 [0.8V,1.4V]，步长为 0.025V。不支持树莓派 4 及更新设备。 |
| `over_voltage_sdram_i` | 调整 SDRAM I/O 电压。[-16,8] 等同于 [0.8V,1.4V]，步长为 0.025V。不支持树莓派 4 及更新设备。 |
| `over_voltage_sdram_p` | 调整 SDRAM phy 电压。[-16,8] 等同于 [0.8V,1.4V]，步长为 0.025V。不支持树莓派 4 及更新设备。 |
| `force_turbo` | 即使 Arm 核心不忙，也强制使用超频模式的频率。如果同时设置了 `over_voltage_*`，启用此参数可能会设置保修位。 |
| `initial_turbo` | 启用[启动加速模式](https://forums.raspberrypi.com/viewtopic.php?f=29&t=6201&start=425#p180099)，持续给定的秒数，或直至 `cpufreq` 设定频率。最大值为 `60`。2024 年 11 月的固件更新做出了以下更改：将默认值从 `0` 改为 `60` 以缩短启动时间；将内核 CPU 性能调度器从 `powersave` 切换为 `ondemand`。 |
| `arm_freq_min` | 动态频率调节所用的 `arm_freq` 最小值。请注意，把该值降到默认值以下并不会带来明显的节能效果，且目前不受支持。 |
| `core_freq_min` | 动态频率调节所用的 `core_freq` 最小值。 |
| `gpu_freq_min` | 动态频率调节所用的 `gpu_freq` 最小值。 |
| `h264_freq_min` | 动态频率调节所用的 `h264_freq` 最小值。 |
| `isp_freq_min` | 动态频率调节所用的 `isp_freq` 最小值。 |
| `v3d_freq_min` | 动态频率调节所用的 `v3d_freq` 最小值。 |
| `hevc_freq_min` | 动态频率调节所用的 `hevc_freq` 最小值。 |
| `sdram_freq_min` | 动态频率调节所用的 `sdram_freq` 最小值。 |
| `over_voltage_min` | 动态频率调节所用的 `over_voltage` 最小值。该值应位于区间 [-16,8]，等同于 [0.8V,1.4V]，步长为 0.025V。换言之，设定 -16 将把 CPU/GPU 核心空闲电压变为 0.8V；设定 8 将把最低电压变为 1.4V。该设置在树莓派 4 和树莓派 5 上已被弃用。 |
| `over_voltage_delta` | 在树莓派 4 和树莓派 5 上，参数 `over_voltage_delta` 会把给定的偏移量（以微伏计）加到 DVFS 算法计算出的数值上。 |
| `temp_limit` | 过热保护。当 SoC 达到此设定值（摄氏度）时，会将时钟和电压恢复为默认值。超过 85 的值会被钳制到 85。 |
| `temp_soft_limit` | **仅适用于 3A+/3B+。** CPU 降频控制。它设定 CPU 时钟速度节流系统激活时的温度。在此温度下，时钟速度将从 1400 MHz 降至 1200 MHz。默认值为 `60`，最大可升至 `70`，但可能会引起不稳定。 |
| `core_freq_fixed` | 置为 1 将停用核心时钟频率的主动调节，确保使用核心时钟的外设保持恒定的速度。固定的时钟频率是所用平台上较高的/超频频率。请优先使用此参数而不是设定特定的核心时钟频率，因为它能让配置文件在不同平台之间通用。 |

下表给出了各树莓派型号参数的默认值，所有频率均以 MHz 表示。

| 参数 | Pi Zero W | Pi 1 | Pi 2 | Pi 3 | Pi 3A+/Pi 3B+ | CM4 和 Pi 4B <= R1.3 | Pi 4B R1.4 | Pi 400 | Pi Zero 2 W | Pi 5/500/500+ |
| :------: | :------------: | :----------: | :----------: | :----------: | :-----------------------: | :--------------------------: | :----------------------------------: | :------------: | :-----------------: | :--------: |
| `arm_freq` | 1000 | 700 | 900 | 1200 | 1400 | 1500 | 1500 或 1800（若 `arm_boost`=1） | 1800 | 1000 | 2400 |
| `core_freq` | 400 | 250 | 250 | 400 | 400 | 500 | 500 | 500 | 400 | 910 |
| `h264_freq` | 300 | 250 | 250 | 400 | 400 | 500 | 500 | 500 | 300 | 不适用 |
| `isp_freq` | 300 | 250 | 250 | 400 | 400 | 500 | 500 | 500 | 300 | 910 |
| `v3d_freq` | 300 | 250 | 250 | 400 | 400 | 500 | 500 | 500 | 300 | 960 |
| `hevc_freq` | 不适用 | 不适用 | 不适用 | 不适用 | 不适用 | 500 | 500 | 500 | 不适用 | 910 |
| `sdram_freq` | 450 | 400 | 450 | 450 | 500 | 3200 | 3200 | 3200 | 450 | 4267 |
| `arm_freq_min` | 700 | 700 | 600 | 600 | 600 | 600 | 600 | 600 | 600 | 1500 |
| `core_freq_min` | 250 | 250 | 250 | 250 | 250 | 200 | 200 | 200 | 250 | 500 |
| `gpu_freq_min` | 250 | 250 | 250 | 250 | 250 | 250 | 250 | 250 | 250 | 500 |
| `h264_freq_min` | 250 | 250 | 250 | 250 | 250 | 250 | 250 | 250 | 250 | 不适用 |
| `isp_freq_min` | 250 | 250 | 250 | 250 | 250 | 250 | 250 | 250 | 250 | 500 |
| `v3d_freq_min` | 250 | 250 | 250 | 250 | 250 | 250 | 250 | 250 | 250 | 500 |
| `sdram_freq_min` | 400 | 400 | 400 | 400 | 400 | 3200 | 3200 | 3200 | 400 | 4267 |

下表给出了在所有型号上取值相同的参数的默认值。

| 参数 | 默认值 |
| :------: | :--------------------------------: |
| `initial_turbo` | 0（秒） |
| `temp_limit` | 85（°C） |
| `over_voltage` | 0（1.35V，树莓派 1 为 1.2V） |
| `over_voltage_min` | 0（1.2V） |
| `over_voltage_sdram` | 0（1.2V） |
| `over_voltage_sdram_c` | 0（1.2V） |
| `over_voltage_sdram_i` | 0（1.2V） |
| `over_voltage_sdram_p` | 0（1.2V） |

固件使用自适应电压调节（AVS），在 `over_voltage` 和 `over_voltage_min` 定义的区间内确定最佳的 CPU/GPU 核心电压。

#### 适用于树莓派 4、树莓派 400 和 CM4

系统空闲时的最低核心频率必须足够快，以支持显示器最高的像素时钟（忽略消隐期）。因此，如果显示模式为 4Kp60，`core_freq` 将被提升到 500 MHz 以上。

| 显示参数 | `core_freq` 最大值 |
| :----------: | :----------------: |
| 默认 | 500 |
| `hdmi_enable_4kp60` | 550 |

>**注意**
>
>自树莓派 5 起的旗舰机型、自 CM5 起的计算模块以及自树莓派 500 起的键盘系列机型无需使用 `hdmi_enable_4kp60`，它们默认支持双 4Kp60 显示屏。

* 超频需要最新版本的固件。
* 最新的固件在系统超频时会自动提升电压。手动设定 `over_voltage` 会禁用超频时的自动电压调节。
* 建议超频时使用单个频率设置（`isp_freq`、`v3d_freq` 等）而不是 `gpu_freq`，因为 ISP、V3D、HEVC 等的最大稳定频率各不相同。
* 树莓派 4 及更新设备上的 SDRAM 频率不可配置。

#### `force_turbo`

在默认情况下（`force_turbo=0`），按需的 CPU 频率驱动程序会在 Arm 核心繁忙时把时钟提升到最大频率，并在 Arm 核心空闲时将其降至最低频率。

`force_turbo=1` 会覆盖上述行为，即使 Arm 核心不忙也强制使用最大频率。

### 时钟关系

#### 树莓派 4

GPU 核心、CPU、SDRAM 和 GPU 各自拥有自己的 PLL，频率可相互独立。h264、v3d 和 ISP 模块共享一个 PLL。

要查看树莓派设备当前的频率（KHz），请输入：`cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_cur_freq`。将结果除以 1000 可得到以 MHz 为单位的值。请注意，此频率是内核_请求_的频率，任何降频（例如高温时）都可能意味着 CPU 的实际运行速度比报告的要慢。使用 vcgencmd 命令 `vcgencmd measure_clock arm` 可以获取 Arm CPU 实际频率的瞬时测量值。该值以赫兹为单位显示。

### 监控核心温度

##### 白皮书

>[树莓派设备散热（Cooling a Raspberry Pi device）](https://pip.raspberrypi.com/documents/RP-003608-WP)
>
>本白皮书详述了你的树莓派可能发热的原因，以及你可能想为它降温的理由，并提供了冷却过程的多种选择。

要查看树莓派的温度，请运行以下命令：

```bash
$ cat /sys/class/thermal/thermal_zone0/temp
```

将结果除以 1000 可得到摄氏度的值。或者，你可以使用 `vcgencmd measure_temp` 来报告 GPU 温度。

达到温度极限不会对 SoC 造成伤害，但会导致 CPU 降频。散热器可以帮助控制核心温度，从而保障性能。如果树莓派装在外壳里运行，散热器尤其有用。散热器上的空气流动会让冷却更有效率。

当核心温度处于 80°C 到 85°C 之间时，Arm 核心将被降频。如果温度超过 85°C，Arm 核心和 GPU 都将被降频。

对于树莓派 3B+ 来说，其印刷电路板（PCB）工艺有所改进，提供了更好的散热性能和更大的热容。此外，还引入了软温度限制，目标是在设备达到 85°C 硬限制之前，尽可能延长其“冲刺”时间。达到软限制时，时钟速度会从 1.4 GHz 降至 1.2 GHz，工作电压也会略微降低。这降低了温度上升的速率：我们用更长时间的 1.2 GHz 换取短时间的 1.4 GHz。默认情况下，软限制为 60°C。可以通过 `config.txt` 中的 `temp_soft_limit` 设置更改此值。

### 监控电压

要保证可靠运行，供电电压必须保持在 4.8 V 以上。请注意，某些 USB 充电器/电源的电压可能低至 4.2 V。这是因为它们通常设计用来给 3.7 V 锂聚合物电池充电，而不是为计算机提供 5 V 电源。

要监测树莓派设备的电源电压，你需要用万用表测量 GPIO 排针的 VCC 引脚和 GND 引脚之间的电压。更多信息请参阅文档的[电源](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#power-supply)部分。

如果电压降至 4.63 V（±5%）以下，Arm 核心和 GPU 将被降频，并且内核日志中会记录一条指示低电压状态的消息。

树莓派 5 的 PMIC 内置了 ADC，可测量供电电压。要查看当前供电电压，请运行以下命令：

```bash
$ vcgencmd pmic_read_adc EXT5V_V
```

### 超频问题

大多数超频问题会立即显现，表现为设备无法启动。如果你的设备因超频配置更改而无法启动，请按以下步骤将其恢复到可启动的状态：

1. 移除 `config.txt` 中所有时钟频率覆盖设置。
2. 使用 `over_voltage_delta` 提高核心电压。
3. 重新应用超频参数，注意避开之前已知有问题的超频参数。

## 条件筛选器

当单张存储卡（或卡镜像）只与一台树莓派和一台显示器搭配使用时，很容易针对这个特定组合把 `config.txt` 设置好并保持不变，只在情况变化时才修改。

但是，如果一台树莓派要在不同显示器之间换用，或者一张存储卡（或卡镜像）要在多块开发板之间换用，那么单一的一套设置可能就不够用了。条件筛选器允许你定义配置文件的某些部分只在特定情况下使用，让同一份 `config.txt` 在被不同硬件读取时生成不同的配置。

### 筛选器 `[all]`

筛选器 `[all]` 是最基本的筛选器。它会重置所有先前设置的筛选器，让其下方列出的任意设置应用于所有硬件。通常，最好在每组筛选设置的末尾添加筛选器 `[all]`，以避免意外组合筛选器（见下文）。

### 型号筛选器

型号条件筛选器的适用型号如下表所示。

| 筛选器 | 适用型号 |
| :--------: | :--------------------------------------------------------------------------: |
| `[pi1]` | 1A、1B、1A+、1B+，计算模块 1 |
| `[pi2]` | 2B（基于 BCM2836 或 BCM2837） |
| `[pi3]` | 3B、3B+、3A+，计算模块 3、3+ |
| `[pi3+]` | 3A+、3B+（同时引用 `[pi3]` 的内容） |
| `[pi4]` | 4B、400，计算模块 4、4S |
| `[pi5]` | 5、500、500+，计算模块 5 |
| `[pi400]` | 400（同时引用 `[pi4]` 的内容） |
| `[pi500]` | 500/500+（同时引用 `[pi5]` 的内容） |
| `[cm0]` | 计算模块 0（同时引用 `[pi02]` 的内容） |
| `[cm1]` | 计算模块 1（同时引用 `[pi1]` 的内容） |
| `[cm3]` | 计算模块 3（同时引用 `[pi3]` 的内容） |
| `[cm3+]` | 计算模块 3+（同时引用 `[pi3+]` 的内容） |
| `[cm4]` | 计算模块 4（同时引用 `[pi4]` 的内容） |
| `[cm4s]` | 计算模块 4S（同时引用 `[pi4]` 的内容） |
| `[cm5]` | 计算模块 5（同时引用 `[pi5]` 的内容） |
| `[pi0]` | Zero、Zero W、Zero 2 W |
| `[pi0w]` | Zero W（同时引用 `[pi0]` 的内容） |
| `[pi02]` | Zero 2 W（同时引用 `[pi0w]` 和 `[pi0]` 的内容） |
| `[board-type=Type]` | 按 `Type` 编号筛选——参见[树莓派修订代码](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#raspberry-pi-revision-codes)。例如 `[board-type=0x14]` 匹配 CM4。 |

这些筛选器对定义不同的 `kernel`、`initramfs` 和 `cmdline` 设置特别有用，因为树莓派 1 和树莓派 2 需要不同的内核。它们也有助于定义不同的超频设置，因为树莓派 1 和树莓派 2 的默认频率不同。比如，为每个型号定义不同的 `initramfs` 镜像：

```bash
[pi1]
initramfs initrd.img-3.18.7+ followkernel
[pi2]
initramfs initrd.img-3.18.7-v7+ followkernel
[all]
```

记得在最后使用筛选器 `[all]`，这样后续设置就不会仅限于树莓派 2 硬件。

>**注意**
>
>某些型号的树莓派（包括 Zero、计算模块和键盘系列机型）会读取多个筛选器的设置。要让某个设置只应用于一个型号：
>
>* 先将该设置应用于基础型号（例如 `[pi4]`），然后为所有会读取基础型号筛选器的型号还原该设置（例如 `[pi400]`、`[cm4]`、`[cm4s]`）
>* 使用带修订代码的 `board-type` 筛选器来锁定单个型号（例如 `[board-type=0x11]`）

### 筛选器 `[none]`

筛选器 `[none]` 会阻止其后的任何设置应用于任何硬件。虽然没有 `[none]` 也没有什么做不到的，但它是一种有用的方式，可以在不必注释掉每一行的情况下，把成组的未使用设置保留在 `config.txt` 中。

```bash
# 引导加载程序 EEPROM 配置。
# 若 PM_RSTS 为分区 62，则设置引导加载程序属性：
# 禁用 SD 高速模式，并显示 HDMI 诊断信息
# 从分区 2 启动，带调试选项。
[partition=62]
# 只有高编号（>31）分区才能被重映射。
PARTITION=2
SD_QUIRKS=0x1
HDMI_DELAY=0
```

示例 `config.txt`——（目前适用于树莓派 5 及后续机型）

```bash
# config.txt——若 PM_RSTS 中最初请求的分区号是
# 一个特殊数字，则使用备用的 cmdline.txt
[partition=62]
cmdline=cmdline-recovery.txt
```

`PM_RSTS` 寄存器在启动时的原始值可通过 `/proc/device-tree/chosen/bootloader/rsts` 获取，用于启动的最终分区号可通过 `/proc/device-tree/chosen/bootloader/partition` 获取。这些都是大端二进制值。

### 表达式筛选器

表达式筛选器支持使用一组简单的运算符，把无符号整数“启动变量”与常量进行比较。它旨在支持 OTA 更新机制、调试和测试。

* “启动变量”是 `boot_arg1`、`cust_otpN`、`bootvar0`、`boot_count`、`boot_partition` 和 `partition`。
* 启动变量始终为小写。
* 整数常量可以写成十进制或十六进制。
* 表达式条件筛选器没有副作用，例如没有赋值运算符。
* 与其他筛选器类型一样，表达式筛选器不能嵌套。
* 使用 `[all]` 筛选器可重置表达式和所有其他条件筛选器类型。

语法：

```bash
# ARG 是启动变量
# VALUE 和 MASK 是无符号整数常量
[ARG=VALUE]      # 当 (ARG == VALUE) 时选中
[ARG&MASK]       # 当 ((ARG & VALUE) != 0) 时选中
[ARG&MASK=VALUE] # 当 ((ARG & MASK) == VALUE) 时选中
[ARG<VALUE]      # 当 (ARG < VALUE) 时选中
[ARG>VALUE]      # 当 (ARG > VALUE) 时选中
```

#### `boot_arg1`

仅适用于树莓派 5 及更新的设备。

`boot_arg1` 变量是一个 32 位用户自定义值，存储在防复位寄存器中，允许参数跨重启传递。

在 `config.txt` 中把 `boot_arg1` 设置为 42：

```bash
set_reboot_arg1=42
```

属性 `set_reboot_arg1` 为下一次启动设置该值。它不会改变配置解析器当前看到的值。

使用 `vcmailbox` 把 `boot_arg1` 设置为 42：

```bash
sudo vcmailbox 0x0003808c 8 8 1 42
```

使用 `vcmailbox` 读取 `boot_arg1`：

```bash
sudo vcmailbox 0x0003008c 8 8 1 0
# 示例输出——boot_arg1 为 42
# 0x00000020 0x80000000 0x0003008c 0x00000008 0x80000008 0x00000001 0x0000002a 0x0000000
```

操作系统启动时 `boot_arg1` 变量的值可以从[设备树](https://www.raspberrypi.com/documentation/computers/configuration.html#part4)的 `/proc/device-tree/chosen/bootloader/arg1` 读取。

#### `cust_otpN`

`cust_otpN` 启动变量（其中 `N` 的范围是 0–7）对应八行客户 OTP。这让你能够基于存储在客户 OTP 中的持久值选择不同的配置。

下面的 `config.txt` 代码片段仅在客户 OTP 第 0 行的位 0 被置位时更改 `cmdline` 文件：

```bash
[cust_otp0&0x1]
cmdline=cmdline_product1.txt
```

有关编程客户 OTP 行的更多信息，请参阅[写入和读取客户 OTP 值](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#write-and-read-customer-otp-values)。

#### `bootvar0`

仅适用于树莓派 4 及更新的设备。

`bootvar0` 变量是一个 32 位用户自定义值，通过 `rpi-eeprom-config` 设置，然后可以在 `config.txt` 中用作条件变量。

例如，在 `rpi-eeprom-config` 中把 `bootvar0` 设置为 42：

```bash
BOOTVAR0=42
```

在 `config.txt` 中按条件使用 `bootvar0`：

```bash
[bootvar0=42]
arm_freq=1000
```

这让同一个镜像（即使用相同的 `config.txt` 文件）能够基于 `rpi-eeprom-config` 的持久设置支持不同的配置。

#### `boot_count`

仅适用于树莓派 5 及更新的设备。

`boot_count` 变量是一个 8 位值，存储在防复位寄存器中，每次启动时递增（到 256 后回绕为零）。断电后会被清除。

使用 `vcmailbox` 读取 `boot_count`：

```bash
sudo vcmailbox 0x0003008d 4 4 0
# 示例——启动计数为 3
# 0x0000001c 0x80000000 0x0003008d 0x00000004 0x80000004 0x00000003 0x00000000
```

使用 `vcmailbox` 设置/清除 `boot_count`：

```bash
# 通过置零清除 boot_count。
sudo vcmailbox 0x0003808d 4 4 0
```

操作系统启动时 `boot_count` 的值可以从[设备树](https://www.raspberrypi.com/documentation/computers/configuration.html#part4)的 `/proc/device-tree/chosen/bootloader/count` 读取。

#### `boot_partition`

`boot_partition` 变量可用于选择要加载的备用操作系统文件（例如 `cmdline.txt`），具体取决于处理 [autoboot.txt](https://www.raspberrypi.com/documentation/computers/config_txt.html#autoboot-txt) 后 `config.txt` 是从哪个分区加载的。它适用于使用 `autoboot.txt` 的 `A/B` 启动系统：在这种情况下，A、B 两个镜像的启动分区中最好安装完全相同的文件。

如果在 [autoboot.txt](https://www.raspberrypi.com/documentation/computers/config_txt.html#autoboot-txt) 中设置的 `boot_partition` 覆盖了它的值，或者指定的分区不可引导且 EEPROM 配置中启用了 [PARTITION_WALK](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#PARTITION_WALK)，那么 `boot_partition` 的值可能与请求的 `partition` 变量不同。

示例 `config.txt`——为 `A/B` 启动文件系统选择匹配的根文件系统：

```bash
# 使用不同的 cmdline 文件，根据系统从哪个分区启动来指向不同的根文件系统。
[boot_partition=1]
cmdline=cmdline_rootfs_a.txt  # 指向根文件系统 A

[boot_partition=2]
cmdline=cmdline_rootfs_b.txt  # 指向根文件系统 B
```

`boot_partition` 的值——即用于启动操作系统的分区——可以从[设备树](https://www.raspberrypi.com/documentation/computers/configuration.html#part4)的 `/proc/device-tree/chosen/bootloader/partition` 读取。

#### `partition`

`partition` 变量可根据请求的分区号（`sudo reboot N`）或直接使用 `PM_RSTS` 看门狗寄存器，选择备用的启动流程。

### 筛选器 `[tryboot]`

如果设置了 `tryboot` 重启标志，此筛选器生效。

它适用于 [autoboot.txt](https://www.raspberrypi.com/documentation/computers/config_txt.html#autoboot-txt)，以便在 `tryboot` 模式下选择不同的 `boot_partition`，实现故障安全的操作系统更新。

启动开始时 `tryboot` 的值可以从[设备树](https://www.raspberrypi.com/documentation/computers/configuration.html#part4)的 `/proc/device-tree/chosen/bootloader/tryboot` 读取。

### 筛选器 `[EDID=*]`

在树莓派上使用单张存储卡在多台显示器之间切换，而空白配置不足以自动为每台显示器选择所需分辨率时，可以根据显示器的 EDID 名称来选择特定设置。

要查看已接入显示器的 EDID 名称，你需要按以下几步操作。运行以下命令，查看你的树莓派上有哪些输出设备：

```bash
$ ls -1 /sys/class/drm/card?-HDMI-A-?/edid
```

在树莓派 4 上，会打印类似如下的输出：

```
/sys/class/drm/card1-HDMI-A-1/edid
/sys/class/drm/card1-HDMI-A-2/edid
```

然后，你需要对每个文件名运行 `edid-decode`，比如：

```bash
$ edid-decode /sys/class/drm/card1-HDMI-A-1/edid
```

如果该输出设备上没有连接显示器，它会告诉你 EDID 为空；否则它会给你提供_大量_关于显示器能力的信息。你需要查找指定 `Manufacturer` 和 `Display Product Name` 的行。“EDID 名称”就是 `<Manufacturer>-<Display Product Name>`，两个字符串中的空格都替换为下划线。比如，如果你的 `edid-decode` 输出包含：

```
  Vendor & Product Identification:
    Manufacturer: DEL
    Display Product Name: 'DELL U2422H'
```

这台显示器的 EDID 名称就是 `DEL-DELL_U2422H`。

然后，你可以把它用作条件筛选器，指定仅在连接这台特定显示器时才适用的设置：

```bash
[EDID=DEL-DELL_U2422H]
cmdline=cmdline_U2422H.txt
[all]
```

这些设置仅在启动时应用。显示器必须在启动时连接，而且树莓派必须能够读取其 EDID 信息以找到正确的名称。启动后热插拔不同的显示器，不会选择不同的设置。

在树莓派 4 上，如果同时使用两个 HDMI 端口，则会对两者都检查 EDID 筛选器，并且所有匹配的条件筛选器的配置都会被应用。

>**注意**
>
>树莓派 5 不提供此设置。

### 串号筛选器

有时，某些设置应该只应用于一台特定的树莓派，即使你把存储卡换到另一台上也一样。例子包括许可证密钥和超频设置（尽管许可证密钥已经通过另一种方式支持存储卡交换）。即使无法使用上述 EDID 识别，你也可以用它来选择不同的显示设置，只要你不把显示器在树莓派设备之间换来换去即可。例如，显示器没有提供可用的 EDID 名称，或者你正在使用复合输出（无法从中读取 EDID）。

要查看你树莓派的串号，请运行以下命令：

```bash
$ cat /proc/cpuinfo
```

输出末尾附近会显示一个 16 位十六进制值。你树莓派的串号就是最后八位十六进制数字。比如，如果你看到：

```bash
Serial          : 0000000012345678
```

则串号为 `12345678`。

>**注意**
>
>在某些树莓派型号上，前 8 位十六进制数字包含的可能是 `0` 以外的值。即使在这种情况下，也只使用最后八位十六进制数字作为串号。

你可以定义仅应用于这台特定树莓派的设置：

```bash
[0x12345678]
# 此处设置仅适用于具有该序列号的树莓派

[all]
# 此处设置适用于所有硬件
```

### GPIO 筛选器

你还可以根据 GPIO 的状态进行筛选。例如：

```bash
[gpio4=1]
# 当 GPIO 4 为高电平时，此处设置生效

[gpio2=0]
# 当 GPIO 2 为低电平时，此处设置生效

[all]
# 此处设置适用于所有硬件
```

### 组合条件筛选器

相同类型的筛选器会互相取代，因此 `[pi2]` 会覆盖 `[pi1]`，因为两者不可能同时为真。

不同类型的筛选器可以通过逐个列出的方式组合，例如：

```bash
# 此处设置适用于所有硬件

[EDID=VSC-TD2220]
# 仅当接入 VSC-TD2220 显示器时，此处设置生效

[pi2]
# 仅当接入 VSC-TD2220 显示器且使用树莓派 2 时，此处设置生效

[all]
# 此处设置适用于所有硬件
```

使用筛选器 `[all]` 可重置先前所有筛选器，避免意外组合不同类型的筛选器。

## 内存参数

### `total_mem`

此参数可用于强制限制树莓派的内存容量：指定你想要让树莓派使用的内存总量（以 MB 为单位）。比如，要让 4 GB 的树莓派 4B 表现得像 1 GB 的型号，请使用以下配置：

```bash
total_mem=1024
```

该值会被钳制在最小 128 MB 与板上实际安装的总内存量之间。

## 许可证密钥和编解码器参数

对于树莓派 3 及更早的型号，可以通过[购买许可证](https://codecs.raspberrypi.com/license-keys/)来启用附加编解码器的硬件解码，许可证与你树莓派的 CPU 序列号绑定。

树莓派 4 的 MPEG2 和 VC1 硬件解码器已被永久禁用。这些编解码器无法启用，因此不需要硬件编解码器许可证密钥。对典型用例来说，MPEG2 和 VC1 文件的软件解码性能已经足够好。

树莓派 5 具备 H.265（HEVC）硬件解码。该解码默认启用，因此不需要硬件编解码器许可证密钥。

### `decode_MPG2`

`decode_MPG2` 是启用 MPEG-2 硬件解码的许可证密钥，例如 `decode_MPG2=0x12345678`。

### `decode_WVC1`

`decode_WVC1` 是启用 VC-1 硬件解码的许可证密钥，例如 `decode_WVC1=0x12345678`。

如果你有多台树莓派设备，并且为每台都购买了编解码器许可证，你可以在一份 `config.txt` 中列出最多八个许可证密钥，例如 `decode_MPG2=0x12345678,0xabcdabcd,0x87654321`。这让你可以在不同树莓派设备之间交换同一张存储卡，而不必每次都编辑 `config.txt`。

## 视频参数

### HDMI 信号格式

要控制 HDMI 设置，请按照《配置》页中[显示设置](https://www.raspberrypi.com/documentation/computers/configuration.html#display-settings)的说明操作。

#### 4 系列设备的 HDMI 管道

为了支持双显示器和最高 4Kp60 的模式，树莓派 4B、计算模块 4、计算模块 4S 和树莓派 400 每个时钟周期生成两个输出像素。

每种 HDMI 模式都有一份时序列表，控制同步脉冲持续时间相关的所有参数。这些时序通常由一个像素时钟定义，然后是水平方向和垂直方向各自的有效像素数、前肩（front porch）、同步脉冲和后肩（back porch）。

由于一切都在每时钟 2 像素下运行，4 系列设备无法支持_任何_水平时序不能被 2 整除的模式。固件和 Linux 内核会过滤掉任何不满足此条件的模式。

CEA 和 DMT 标准中只有一种不兼容的模式：DMT 模式 81，1366x768 @ 60Hz。该模式的水平同步和后肩时序为奇数，宽度不能被 8 整除。

如果你的显示器使用这种分辨率，4 系列设备会自动降到显示器通告的下一个模式，通常是 1280x720。

#### 5 系列设备的 HDMI 管道

树莓派 5 及后续机型、计算模块 5 及后续机型、树莓派 500 及后续机型同样以每时钟两个输出像素工作。这些型号对奇数时序有特殊处理，可以直接处理这些模式。

### 复合视频模式

每款树莓派计算机上都能找到复合视频输出。

| 型号 | 复合输出 |
| :-----------------: | :-----------------------: |
| 树莓派 1 A 和 B | RCA 端子 |
| 树莓派 Zero | 未焊接的 `TV` 接口 |
| 树莓派 Zero 2 W | 主板底部的测试点 |
| 树莓派 5 | HDMI 插口旁的 J7 触点 |
| 所有其他型号 | 3.5 mm AV 端子 |

>**注意**
>
>键盘系列机型不提供复合视频输出。

#### `enable_tvout`

置为 `1` 启用复合视频输出，置为 `0` 禁用。自树莓派 4 起的旗舰机型、自 CM4 起的计算模块以及 Zero 系列机型，只有将此参数置为 `1` 时才提供复合输出，置为 `1` 同时也会禁用 HDMI 输出。键盘系列机型不提供复合输出。

| 型号 | 默认值 |
| :----------------: | :------: |
| 自树莓派 4B 起的旗舰机型、自 CM4 起的计算模块、键盘系列机型 | 0 |
| 所有其他型号 | 1 |

在受支持的机型上，必须禁用 HDMI 输出才能启用复合输出。未检测到 HDMI 显示器时，HDMI 输出会被禁用。设置 `enable_tvout=0` 可防止在 HDMI 被禁用时启用复合输出。

要启用复合输出，请在 `/boot/firmware/config.txt` 的 `dtoverlay=vc4-kms-v3d` 这行末尾添加 `,composite`：

```bash
dtoverlay=vc4-kms-v3d,composite
```

在默认情况下，会输出复合视频 NTSC。要选择其他模式，请改为在 `/boot/firmware/cmdline.txt` 的单行内容末尾追加以下内容：

```bash
vc4.tv_norm=<video_mode>
```

请将 `<video_mode>` 占位符替换为以下值之一：

* `NTSC`
* `NTSC-J`
* `NTSC-443`
* `PAL`
* `PAL-M`
* `PAL-N`
* `PAL60`
* `SECAM`

### LCD 显示器和触摸屏

#### `ignore_lcd`

在默认情况下，会在 I²C 总线上检测树莓派触摸显示屏，检测到即使用。`ignore_lcd=1` 可跳过这个检测阶段。这会阻止 LCD 显示屏被使用。

#### `disable_touchscreen`

启用和禁用触摸屏。

`disable_touchscreen=1` 可禁用树莓派官方触摸显示屏的触摸屏组件。

### 通用显示参数

#### `disable_fw_kms_setup`

在默认情况下，固件会解析所有通过 HDMI 接入的显示器的 EDID，选择合适的视频模式，然后通过内核命令行上的设置把该模式的分辨率和帧率（以及过扫描参数）传给 Linux 内核。在极少数情况下，固件可能会选择 EDID 中不存在的模式，该模式可能与设备不兼容。使用 `disable_fw_kms_setup=1` 可以禁用视频模式参数的传递，从而避免此问题。Linux 视频模式系统（KMS）会自己解析 EDID 并选择合适的模式。

>**注意**
>
>在树莓派 5 上，此参数默认为 `1`。

## 相机设置

### `disable_camera_led`

将 `disable_camera_led` 置为 `1`，可在录制视频或拍摄照片时阻止摄像机的红色 LED 点亮。这对于防止反光（例如摄像机正对着窗户时）很有用。

### `awb_auto_is_greyworld`

将 `awb_auto_is_greyworld` 置为 `1`，可以让内部不支持灰度世界（greyworld）选项的库或应用程序使用 NoIR 摄像头捕捉到有效的图像和视频。它会把自动 awb 模式切换为使用灰度世界算法。这应该只在 NoIR 摄像头，或[移除了红外滤光片](https://www.raspberrypi.com/documentation/accessories/camera.html#filter-removal)的高质量（HQ）摄像头上才需要。
