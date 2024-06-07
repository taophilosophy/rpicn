# 旧版 config.txt 参数

## 旧版参数

这里所说的 config.txt 的参数被视为旧版参数，不再被Raspberry Pi OS Bookworm 使用，且没有官方支持。它们要么涉及旧版软件（如固件图形驱动程序）、要么已被弃用、或要么只有极少数人才可能会使用到。然而，它们仍然记录在此，因为它们对于使用旧版操作系统的用户或进行裸机开发的人仍然可能有用。

## 旧版启动参数

(另请参阅 config.txt 启动选项。)

### `start_x`, `start_debug`

这些提供了一些替代 start_file 和 fixup_file 设置的快捷方式，是选择固件配置的推荐方法。

  start_x=1 意味着

```
  start_file=start_x.elf
  fixup_file=fixup_x.dat
```

在树莓派 4 上，如果存在文件 start4x.elf 和 fixup4x.dat ，则将使用这些文件。

  start_debug=1 意味着

```
  start_file=start_db.elf
  fixup_file=fixup_db.dat
```

### `disable_commandline_tags`

将 disable_commandline_tags 命令设置为 1 ，以阻止 start.elf 在启动内核之前填充 ATAGS（来自 0x100 的内存）。

### `arm_control`

>**警告**
>
>此设置已弃用。请改用 arm_64bit 以启用 64 位内核。


设置特定于板的控制位。

### `armstub`

armstub 是从中加载 ARM 存根的引导分区上的文件名。默认的 ARM 存根存储在固件中，并根据树莓派型号和各种设置自动选择。

存根是在内核之前运行的一小段 ARM 代码。其工作是在将控制权传递给内核之前设置低级硬件，如中断控制器。

### `arm_peri_high`

将 arm_peri_high 设置为 1 可以在树莓派 4 上启用高外设模式。如果加载了适当的 DTB，则会自动设置。


>**注意**
>
>在没有兼容的设备树的情况下启用高外设模式会导致系统无法启动。目前缺少 ARM 存根支持，因此您还需要使用 armstub 加载适当的文件。


### `kernel_address`

kernel_address 是内核映像应加载到的内存地址。默认情况下，32 位内核加载到地址 0x8000 ，64 位内核加载到地址 0x200000 。如果设置了 kernel_old ，内核将加载到地址 0x0 。

### `kernel_old`

将 kernel_old 设置为 1 以将内核加载到内存地址 0x0 。

### `init_uart_baud`

init_uart_baud 是初始 UART 波特率。默认值为 115200 。

### `init_uart_clock`

init_uart_clock 是初始 UART 时钟频率。默认值为 48000000 （48MHz）。请注意，此时钟仅适用于 UART0（Linux 中的 ttyAMA0），且 UART 的最大波特率受限于时钟的 1/16。树莓派 3 和树莓派 Zero 上的默认 UART 是 UART1（Linux 中的 ttyS0），其时钟为核心 VPU 时钟 - 至少 250MHz。

### `bootcode_delay`

bootcode_delay 命令在 bootcode.bin 秒内延迟，然后加载 start.elf ：默认值为 0 。

这在在读取显示器的 EDID 之前插入延迟特别有用，例如，如果树莓派和显示器来自同一电源，但显示器启动时间比树莓派更长。如果在初始启动时显示检测错误，但在不断电的情况下重新启动树莓派时正确，请尝试设置此值。

### `boot_delay`

boot_delay 命令会在加载内核之前在 start.elf 中强制等待给定的秒数：默认值为 0 。毫秒中的总延迟计算为 (1000 x boot_delay) + boot_delay_ms 。如果您的 SD 卡需要一段时间才能准备好，然后 Linux 才能从中引导，这可能很有用。

### `boot_delay_ms`

boot_delay_ms 命令意味着在加载内核之前在 start.elf 中等待给定的毫秒数，以及 boot_delay 。默认值为 0 。

### enable_gic （仅适用于树莓派 4）

在树莓派 4B 上，如果将此值设置为 0 ，则中断将通过旧版中断控制器路由到 Arm 内核，而不是通过 GIC-400。默认值为 1 。

### `sha256`

如果设置为非零，则启用为加载的文件（内核、initramfs、设备树 .dtb 文件和叠加层）记录 SHA256 哈希的日志，该哈希由 sha256sum 实用程序生成。如果启用，记录输出将发送到 UART，并且也可通过 sudo vclog --msg 访问。在调试启动问题时，此选项可能很有用，但可能会增加启动时间数秒。在所有平台上，默认值为 0。

### `uart_2ndstage`

设置 uart_2ndstage=1 会导致第二阶段加载程序（在树莓派 4 之前的设备上为 bootcode.bin ，在树莓派 4 设备上为 EEPROM 中的引导代码）和主固件（ start*.elf ）将诊断信息输出到 UART0。

请注意，输出可能会干扰蓝牙操作，除非将其禁用（ dtoverlay=disable-bt ）或切换到另一个 UART（ dtoverlay=miniuart-bt ），如果 UART 同时访问 Linux 输出，则可能会导致数据丢失，从而导致输出损坏。只有在尝试诊断早期引导加载问题时才应该需要此功能。

### `upstream_kernel`

如果使用 upstream_kernel=1 ，固件会将 os_prefix 设置为"upstream/"，除非已明确设置为其他内容，但与其他 os_prefix 值一样，如果在使用前缀时找不到所需的内核和.dtb 文件，则会被忽略。

固件还会更喜欢 DTBs 的上游 Linux 名称（ bcm2837-rpi-3-b.dtb 而不是 bcm2710-rpi-3-b.dtb ，例如）。如果找不到上游文件，则固件将加载下游变体，并自动应用"upstream"叠加以进行一些调整。请注意，此过程发生在 os_prefix 最终确定之后。

## 旧版 GPIO 控制

(另请参阅 config.txt GPIO 控制。)

### `enable_jtag_gpio`

设置 enable_jtag_gpio=1 选择 GPIO 引脚 22-27 的 Alt4 模式，并设置一些内部 SoC 连接，启用 Arm CPU 的 JTAG 接口。它适用于所有型号的树莓派。

| 引脚号 | 功能     |
| -------- | ---------- |
| GPIO22 | ARM_TRST |
| GPIO23 | ARM_RTCK |
| GPIO24 | ARM_TDO  |
| GPIO25 | ARM_TCK  |
| GPIO26 | ARM_TDI  |
| GPIO27 | ARM_TMS  |

## 旧版超频选项

（另请参阅 config.txt 超频选项。）

### 超频

#### `never_over_voltage`

在一次性可编程（OTP）存储器中设置一个位，防止设备过电压。这旨在锁定树莓派，以防止无意或恶意地使用无效过电压设置保修位。

#### `disable_auto_turbo`

在树莓派 2 和 3 上，设置此标志将禁用 GPU 进入 turbo 模式，该模式在特定负载下可以启用。

## 旧版条件过滤器

（另请参阅 config.txt 条件过滤器。）

### `[HDMI:*]` 过滤器

>**注意**
>
>此过滤器仅适用于树莓派 4。 

树莓派 4 有两个 HDMI，对于许多与 HDMI 相关的 config.txt 命令，有必要指定所指的 HDMI 接口。HDMI 条件过滤器将后续 HDMI 配置限制到特定接口。

```
 [HDMI:0]
   hdmi_group=2
   hdmi_mode=45
 [HDMI:1]
   hdmi_group=2
   hdmi_mode=67
```

所有特定端口 HDMI 命令都提供了另一种 variable:index 语法。您可以使用以下内容，这与前面的示例相同：

```
 hdmi_group:0=2
 hdmi_mode:0=45
 hdmi_group:1=2
 hdmi_mode:1=67
```

## 旧版内存选项

（另请参阅 config.txt 内存选项）

>**注意**
>
>树莓派 5 不会代表操作系统分配 GPU 内存，因此以下设置不起作用。 

### `gpu_mem`

指定要为 GPU 专用保留多少兆字节的内存：剩余内存分配给 Arm CPU 供操作系统使用。对于内存少于 1GB 的树莓派，默认值为 64 ；对于内存为 1GB 或更多的树莓派，默认值为 76 。

>**重要**
>
>与 x86 机器上的 GPU 不同，增加显存并不能提高 3D 性能，VideoCore 的架构意味着指定比必要值更大的值不会带来性能优势，事实上可能会损害性能。

为了确保 Linux 的最佳性能，您应将 gpu_mem 设置为可能的最低值。如果某个特定的图形功能无法正常工作，请尝试增加 gpu_mem 的值，注意下面显示的推荐最大值。

在树莓派 4 上，GPU 的 3D 组件具有自己的内存管理单元（MMU），不使用 gpu_mem 分配的内存。取而代之的是在 Linux 内动态分配内存。这使得在树莓派 4 上可以指定比以前型号更小的 gpu_mem 值。

在旧版内核上，分配给 GPU 的内存用于显示、3D、编解码器和摄像头等用途，以及一些基本固件管理。下面指定的最大值假定您正在使用所有这些功能。如果没有使用，则应使用较小的 gpu_mem 值。

建议的最大值如下：

| 总内存     |  推荐的 gpu_mem 最大值             |
| ------------ | ---------------------------------- |
| 256MB      | `128`                                 |
| 512MB      | `384`                                 |
| 1GB 或更大 | 在树莓派 4 上， 512 ， 76 |

>**重要**
>
>Raspberry Pi OS 上的相机堆栈（libcamera）使用 Linux CMA 内存来分配缓冲区，而非 GPU 显存，因此增加 GPU 显存大小没有任何好处。


可以将 gpu_mem 设置为较大的值，但应避免这样做，因为可能会导致问题，比如妨碍 Linux 启动。gpu_mem 的最小值为 16 ，但这会禁用某些 GPU 功能。

您还可以使用 gpu_mem_256 ， gpu_mem_512 和 gpu_mem_1024 ，以便在不同内存量的树莓派之间交换相同的 SD 卡，而无需每次都编辑 config.txt ：

### `gpu_mem_256`

gpu_mem_256 命令为具有 256MB 内存的树莓派设置以兆字节为单位的 GPU 内存。如果内存大小不是 256MB，则会被忽略。这会覆盖 gpu_mem 。

### `gpu_mem_512`

gpu_mem_512 命令设置树莓派内存为 512MB 时的 GPU 内存（以兆字节为单位）。如果内存大小不是 512MB，则会被忽略。这将覆盖 gpu_mem 。

### `gpu_mem_1024`

gpu_mem_1024 命令设置树莓派内存为 1GB 或更多时的 GPU 内存（以兆字节为单位）。如果内存大小小于 1GB，则会被忽略。这将覆盖 gpu_mem 。

### `disable_l2cache`

将此设置为 1 会禁用 CPU 对 GPU 的 L2 缓存的访问，并需要相应的禁用 L2 缓存的内核。在 BCM2835 上的默认值为 0 。在 BCM2836、BCM2837、BCM2711 和 BCM2712 上，ARM 有自己的 L2 缓存，因此默认值为 1 。标准的树莓派 kernel.img 和 kernel7.img 版本反映了缓存设置的差异。

## 旧版视频选项

(另请参阅 config.txt 视频选项)

### HDMI 模式

>**注意**
>
>因为树莓派 4 和树莓派 400 有两个 HDMI 接口，一些 HDMI 命令可以应用于任一接口。您可以使用语法 `<command>:<port>` ，其中端口为 0 或 1，以指定设置应适用于哪个端口。如果未指定端口，则默认为 0。如果在不需要端口号的命令上指定端口号，则端口将被忽略。有关语法和替代机制的更多详细信息，请参阅文档的条件部分中 HDMI 子部分。 

#### `hdmi_safe`

将 hdmi_safe 设置为 1 将导致使用“安全模式”设置尝试以最大 HDMI 兼容性启动。这与设置以下参数相同：

```
hdmi_force_hotplug=1
hdmi_ignore_edid=0xa5000080
config_hdmi_boost=4
hdmi_group=2
hdmi_mode=4
disable_overscan=0
overscan_left=24
overscan_right=24
overscan_top=24
overscan_bottom=24
```

#### `hdmi_ignore_edid`

将 hdmi_ignore_edid 设置为 0xa5000080 可以启用忽略 EDID/显示数据，如果您的显示器没有准确的 EDID。它需要这个不寻常的值来确保不会意外触发。

#### `hdmi_edid_file`

将 hdmi_edid_file 设置为 1 将导致 GPU 从引导分区中的 edid.dat 文件读取 EDID 数据，而不是从显示器读取。

#### `hdmi_edid_filename`

在树莓派 4B 上，您可以使用 hdmi_edid_filename 命令指定要使用的 EDID 文件的文件名，并指定要应用文件的端口。这还需要 hdmi_edid_file=1 来启用 EDID 文件。

 例如：

```
hdmi_edid_file=1
hdmi_edid_filename:0=FileForPortZero.edid
hdmi_edid_filename:1=FileForPortOne.edid
```

#### `hdmi_force_edid_audio`

将 hdmi_force_edid_audio 设置为 1 会假装显示器支持所有音频格式，即使实际上不支持 DTS/AC3，也允许进行音频透传。

#### `hdmi_ignore_edid_audio`

将 hdmi_ignore_edid_audio 设置为 1 会假装显示器不支持任何音频格式。这意味着 ALSA 会默认使用模拟音频（耳机）插孔。

#### `hdmi_force_edid_3d`

将 hdmi_force_edid_3d 设置为 1 会假装所有 CEA 模式都支持 3D，即使 EDID 没有指示支持。

#### `hdmi_ignore_cec_init`

将 hdmi_ignore_cec_init 设置为 1 将阻止在启动过程中发送初始活动源消息。这可以防止在重新启动树莓派时，CEC 启用的电视机从待机状态中唤醒并切换频道。

#### `hdmi_ignore_cec`

将 hdmi_ignore_cec 设置为 1 会假装显示器根本不支持 CEC。将不支持任何 CEC 功能。

#### `cec_osd_name`

cec_osd_name 命令设置设备的初始 CEC 名称。默认为 `Raspberry Pi`.

#### `hdmi_pixel_encoding`

hdmi_pixel_encoding 命令强制使用像素编码模式。默认情况下，它将使用从 EDID 请求的模式，因此您不应该需要更改它。

| hdmi_pixel_encoding | 结果                                     |
| --------------------- | ------------------------------------------ |
| 0                   | 默认值（CEA 为 RGB 有限，DMT 为 RGB 全） |
| 1                   | RGB 有限（16-235）                       |
| 2                   | RGB 全（0-255）                          |
| 3                   | YCbCr 有限 (16-235)                      |
| 4                   | YCbCr 全范围 (0-255)                     |

#### `hdmi_max_pixel_freq`

固件和 KMS 使用像素频率来过滤 HDMI 模式。请注意，这与帧率不同。它指定了有效模式可以具有的最大频率，从而剔除更高频率的模式。因此，例如，如果您希望禁用所有 4K 模式，您可以指定最大频率为 200000000，因为所有 4K 模式的频率都大于此值。

#### `hdmi_blanking`

当操作系统要求将显示器置于待机模式以节省电源时， hdmi_blanking 命令控制发生的情况。如果未设置此选项或将其设置为 0，则 HDMI 输出将被清空但不会关闭。为了模仿其他计算机的行为，您可以将 HDMI 输出也设置为关闭，方法是将此选项设置为 1：连接的显示器将进入低功耗待机模式。

>**注意**
>
>在树莓派 4 上，设置 hdmi_blanking=1 不会导致 HDMI 输出停止，因为此功能尚未实现。当使用不使用 framebuffer 的应用程序时，此功能可能会导致问题，例如 omxplayer 。

| hdmi_blanking | 结果                    |
| --------------- | ------------------------- |
| 0             | HDMI 输出将被屏蔽       |
| 1             | HDMI 输出将被关闭并屏蔽 |

#### `hdmi_drive`

hdmi_drive 命令允许您在 HDMI 和 DVI 输出模式之间进行选择。

| hdmi_drive | 结果                                             |
| ------------ | -------------------------------------------------- |
| 1          | 正常的 DVI 模式（无声音）                        |
| 2          | 正常的 HDMI 模式（如果支持且已启用，将发送声音） |

#### `config_hdmi_boost`

配置 HDMI 接口的信号强度。最小值为 0 ，最大值为 11 。

原始 Model B 和 A 的默认值为 2 。Model B+ 和所有后续型号的默认值为 5 。

如果您遇到 HDMI 问题（斑点，干扰），请尝试 7 。非常长的 HDMI 电缆可能需要高达 11 才行，但除非绝对必要，否则不应使用这么高的值。

在旧版树莓派 4 上会忽略此选项。

#### `hdmi_group`

hdmi_group 命令定义 HDMI 输出组，可以是 CEA（消费类电子协会，通常由电视使用的标准）或 DMT（显示器定时，通常由显示器使用的标准）。此设置应与 hdmi_mode 一起使用。

| HDMI 组 | 结果             |
| --------- | ------------------ |
| 0       | 从 EDID 自动检测 |
| 1       | CEA              |
| 2       | DMT              |

#### `hdmi_mode`

与 hdmi_group 一起， hdmi_mode 定义 HDMI 输出格式。格式模式编号源自 CTA 规范。

>**注意**
>
>并非所有模式在所有型号上都可用。

这些值仅在 hdmi_group=1 (CEA) 有效：

| hdmi_mode | 分辨率         | 频率     | 屏幕比例 | 注释               |
| ----------- | ---------------- | ---------- | ---------- | -------------------- |
| 1         | VGA（640x480） | 60Hz  | 4:3      |                    |
| 2         | 480p           | 60Hz  | 4:3      |                    |
| 3         | 480p           | 60Hz  | 16:9     |                    |
| 4         | 720p           | 60Hz     | 16:9     |                    |
| 5         | 1080i          | 60Hz  | 16:9     |                    |
| 6         | 480i           | 60Hz  | 4:3      |                    |
| 7         | 480i           | 60Hz     | 16:9     |                    |
| 8         | 240p           | 60Hz  | 4:3      |                    |
| 9         | 240p           | 60Hz  | 16:9     |                    |
| 10        | 480i           | 60Hz     | 4:3      | 像素四倍化         |
| 11        | 480i           | 60Hz     | 16:9     | 像素四倍化         |
| 12        | 240p           | 60Hz     | 4:3      | 像素四倍化         |
| 13        | 240p           | 60Hz     | 16:9     | 像素四倍化         |
| 14        | 480p           | 60Hz     | 4:3      | 像素加倍           |
| 15        | 480p           | 60Hz     | 16:9     | 像素加倍           |
| 16        | 1080p          | 60Hz     | 16:9     |                    |
| 17        | 576p           | 50Hz  | 4:3      |                    |
| 18        | 576p           | 50Hz  | 16:9     |                    |
| 19        | 720p           | 50Hz     | 16:9     |                    |
| 20        | 1080i          | 50Hz     | 16:9     |                    |
| 21        | 576i           | 50Hz  | 4:3      |                    |
| 22        | 576i           | 50Hz     | 16:9     |                    |
| 23        | 288p           | 50Hz  | 4:3      |                    |
| 24        | 288p           | 50Hz  | 16:9     |                    |
| 25        | 576i           | 50Hz     | 4:3      | 像素四倍化         |
| 26        | 576i           | 50Hz     | 16:9     | 像素四倍化         |
| 27        | 288p           | 50Hz     | 4:3      | 像素四倍增         |
| 28        | 288p           | 50Hz     | 16:9     | 像素四倍化         |
| 29        | 576p           | 50Hz     | 4:3      | 像素加倍           |
| 30        | 576p           | 50Hz     | 16:9     | 像素加倍           |
| 31        | 1080p          | 50Hz     | 16:9     |                    |
| 32        | 1080p          | 24Hz     | 16:9     |                    |
| 33        | 1080p          | 25Hz     | 16:9     |                    |
| 34        | 1080p          | 30Hz     | 16:9     |                    |
| 35        | 480p           | 60Hz     | 4:3      | 像素四倍化         |
| 36        | 480p           | 60Hz     | 16:9     | 像素四倍化         |
| 37        | 576p           | 50Hz     | 4:3      | 像素四倍化         |
| 38        | 576p           | 50Hz     | 16:9     | 像素四倍化         |
| 39        | 1080i          | 50Hz     | 16:9     | 降低清屏时间（reduced blanking）           |
| 40        | 1080i          | 100Hz | 16:9     |                    |
| 41        | 720p           | 100Hz | 16:9     |                    |
| 42        | 576p           | 100Hz    | 4:3      |                    |
| 43        | 576p           | 100Hz | 16:9     |                    |
| 44        | 576i           | 100Hz | 4:3      |                    |
| 45        | 576i           | 100Hz    | 16:9     |                    |
| 46        | 1080i          | 120Hz    | 16:9     |                    |
| 47        | 720p           | 120Hz | 16:9     |                    |
| 48        | 480p           | 120Hz    | 4:3      |                    |
| 49        | 480p           | 120Hz    | 16:9     |                    |
| 50        | 480i           | 120Hz    | 4:3      |                    |
| 51        | 480i           | 120Hz    | 16:9     |                    |
| 52        | 576p           | 200Hz | 4:3      |                    |
| 53        | 576p           | 200Hz | 16:9     |                    |
| 54        | 576i           | 200Hz    | 4:3      |                    |
| 55        | 576i           | 200Hz | 16:9     |                    |
| 56        | 480p           | 240Hz | 4:3      |                    |
| 57        | 480p           | 240Hz    | 16:9     |                    |
| 58        | 480i           | 240Hz    | 4:3      |                    |
| 59        | 480i           | 240Hz | 16:9     |                    |
| 60        | 720p           | 24Hz     | 16:9     |                    |
| 61        | 720p           | 25Hz     | 16:9     |                    |
| 62        | 720p           | 30Hz     | 16:9     |                    |
| 63        | 1080p          | 120Hz    | 16:9     |                    |
| 64        | 1080p          | 100Hz    | 16:9     |                    |
| 65        | 自定义         |          |          |                    |
| 66        | 720p           | 25Hz     | 64:27    | 树莓派 4           |
| 67        | 720p           | 30Hz     | 64:27    | 树莓派 4           |
| 68        | 720p           | 50Hz  | 64:27    | 树莓派 4           |
| 69        | 720p           | 60Hz     | 64:27    | 树莓派 4           |
| 70        | 720p           | 100Hz | 64:27    | 树莓派 4           |
| 71        | 720p           | 120Hz    | 64:27    | 树莓派 4           |
| 72        | 1080p          | 24Hz     | 64:27    | 树莓派 4           |
| 73        | 1080p          | 25Hz     | 64:27    | 树莓派 4           |
| 74        | 1080p          | 30Hz     | 64:27    | 树莓派 4           |
| 75        | 1080p          | 50Hz     | 64:27    | 树莓派 4           |
| 76        | 1080p          | 60Hz     | 64:27    | 树莓派 4           |
| 77        | 1080p          | 100Hz    | 64:27    | 树莓派 4           |
| 78        | 1080p          | 120Hz    | 64:27    | 树莓派 4           |
| 79        | 1680x720       | 24Hz     | 64:27    | 树莓派 4           |
| 80        | 1680x720       | 25z      | 64:27    | 树莓派 4           |
| 81        | 1680x720       | 30Hz     | 64:27    | 树莓派 4           |
| 82        | 1680x720       | 50Hz     | 64:27    | 树莓派 4           |
| 83        | 1680x720       | 60Hz     | 64:27    | 树莓派 4           |
| 84        | 1680x720       | 100Hz    | 64:27    | 树莓派 4           |
| 85        | 1680x720       | 120Hz    | 64:27    | 树莓派 4           |
| 86        | 2560x720       | 24Hz     | 64:27    | 树莓派 4           |
| 87        | 2560x720       | 25Hz     | 64:27    | 树莓派 4           |
| 88        | 2560x720       | 30Hz     | 64:27    | 树莓派 4           |
| 89        | 2560x720       | 50Hz     | 64:27    | 树莓派 4           |
| 90        | 2560x720       | 60Hz     | 64:27    | 树莓派 4           |
| 91        | 2560x720       | 100Hz    | 64:27    | 树莓派 4           |
| 92        | 2560x720       | 120Hz    | 64:27    | 树莓派 4           |
| 93        | 2160p          | 24Hz     | 16:9     | 树莓派 4           |
| 94        | 2160p          | 25Hz     | 16:9     | 树莓派 4           |
| 95        | 2160p          | 30Hz     | 16:9     | 树莓派 4           |
| 96        | 2160p          | 50Hz     | 16:9     | 树莓派 4           |
| 97        | 2160p          | 60Hz     | 16:9     | 树莓派 4           |
| 98        | 4096x2160      | 24Hz     | 256:135  | 树莓派 4           |
| 99        | 4096x2160      | 25Hz     | 256:135  | 树莓派 4           |
| 100       | 4096x2160      | 30Hz     | 256:135  | 树莓派 4           |
| 101       | 4096x2160      | 50Hz     | 256:135  | 树莓派 4 ^**1**^ |
| 102       | 4096x2160      | 60Hz     | 256:135  | 树莓派 4 ^**1**^ |
| 103       | 2160p          | 24Hz     | 64:27    | 树莓派 4           |
| 104       | 2160p          | 25Hz     | 64:27    | 树莓派 4           |
| 105       | 2160p          | 30Hz     | 64:27    | 树莓派 4           |
| 106       | 2160p          | 50Hz     | 64:27    | 树莓派 4           |
| 107       | 2160p          | 60Hz     | 64:27    | 树莓派 4           |

1. 仅在超频核心频率下可用：设置 core_freq_min=600 和 core_freq=600 。请参阅超频。

像素加倍和四倍表示更高的时钟速率，每个像素分别重复两次或四次。

如果 hdmi_group=2 （DMT）有效，则这些值有效：

| hdmi_mode | 分辨率    | 频率     | 屏幕宽高比 | 笔记                   |
| ----------- | ----------- | ---------- | ------------ | ------------------------ |
| 1         | 640x350   | 85Hz     |            |                        |
| 2         | 640x400   | 85Hz     | 16:10      |                        |
| 3         | 720x400   | 85Hz     |            |                        |
| 4         | 640x480   | 60Hz     | 4:3        |                        |
| 5         | 640x480   | 72Hz     | 4:3        |                        |
| 6         | 640x480   | 75Hz     | 4:3        |                        |
| 7         | 640x480   | 85Hz     | 4:3        |                        |
| 8         | 800x600   | 56Hz     | 4:3        |                        |
| 9         | 800x600   | 60Hz     | 4:3        |                        |
| 10        | 800x600   | 72Hz     | 4:3        |                        |
| 11        | 800x600   | 75Hz     | 4:3        |                        |
| 12        | 800x600   | 85Hz     | 4:3        |                        |
| 13        | 800x600   | 120Hz    | 4:3        |                        |
| 14        | 848x480   | 60Hz     | 16:9       |                        |
| 15        | 1024x768  | 43Hz     | 4:3        | 与树莓派不兼容 |
| 16        | 1024x768  | 60Hz  | 4:3        |                        |
| 17        | 1024x768  | 70Hz  | 4:3        |                        |
| 18        | 1024x768  | 75Hz     | 4:3        |                        |
| 19        | 1024x768  | 85Hz  | 4:3        |                        |
| 20        | 1024x768  | 120Hz | 4:3        |                        |
| 21        | 1152x864  | 75Hz     | 4:3        |                        |
| 22        | 1280x768  | 60Hz     | 15:9       | 降低清屏时间（reduced blanking）               |
| 23        | 1280x768  | 60Hz  | 15:9       |                        |
| 24        | 1280x768  | 75Hz | 15:9       |                        |
| 25        | 1280x768  | 85Hz     | 15:9       |                        |
| 26        | 1280x768  | 120Hz    | 15:9       | 降低清屏时间（reduced blanking）               |
| 27        | 1280x800  | 60       | 16:10      | 降低清屏时间（reduced blanking）               |
| 28        | 1280x800  | 60Hz     | 16:10      |                        |
| 29        | 1280x800  | 75Hz     | 16:10      |                        |
| 30        | 1280x800  | 85Hz     | 16:10      |                        |
| 31        | 1280x800  | 120Hz    | 16:10      | 降低清屏时间（reduced blanking）               |
| 32        | 1280x960  | 60Hz     | 4:3        |                        |
| 33        | 1280x960  | 85Hz     | 4:3        |                        |
| 34        | 1280x960  | 120Hz    | 4:3        | 降低清屏时间（reduced blanking）               |
| 35        | 1280x1024 | 60Hz     | 5:4        |                        |
| 36        | 1280x1024 | 75Hz     | 5:4        |                        |
| 37        | 1280x1024 | 85Hz     | 5:4        |                        |
| 38        | 1280x1024 | 120Hz    | 5:4        | 降低清屏时间（reduced blanking）               |
| 39        | 1360x768  | 60Hz  | 16:9       |                        |
| 40        | 1360x768  | 120Hz | 16:9       | 降低清屏时间（reduced blanking）               |
| 41        | 1400x1050 | 60Hz     | 4:3        | 降低清屏时间（reduced blanking）               |
| 42        | 1400x1050 | 60Hz     | 4:3        |                        |
| 43        | 1400x1050 | 75Hz     | 4:3        |                        |
| 44        | 1400x1050 | 85Hz  | 4:3        |                        |
| 45        | 1400x1050 | 120Hz | 4:3        | 降低清屏时间（reduced blanking）               |
| 46        | 1440x900  | 60Hz     | 16:10      | 降低清屏时间（reduced blanking）               |
| 47        | 1440x900  | 60Hz     | 16:10      |                        |
| 48        | 1440x900  | 75Hz     | 16:10      |                        |
| 49        | 1440x900  | 85Hz     | 16:10      |                        |
| 50        | 1440x900  | 120Hz    | 16:10      | 降低清屏时间（reduced blanking）               |
| 51        | 1600x1200 | 60Hz     | 4:3        |                        |
| 52        | 1600x1200 | 65Hz     | 4:3        |                        |
| 53        | 1600x1200 | 70Hz     | 4:3        |                        |
| 54        | 1600x1200 | 75Hz     | 4:3        |                        |
| 55        | 1600x1200 | 85Hz     | 4:3        |                        |
| 56        | 1600x1200 | 120Hz    | 4:3        | 降低清屏时间（reduced blanking）               |
| 57        | 1680x1050 | 60Hz     | 16:10      | 降低清屏时间（reduced blanking）               |
| 58        | 1680x1050 | 60Hz     | 16:10      |                        |
| 59        | 1680x1050 | 75Hz     | 16:10      |                        |
| 60        | 1680x1050 | 85Hz     | 16:10      |                        |
| 61        | 1680x1050 | 120Hz    | 16:10      | 降低清屏时间（reduced blanking）               |
| 62        | 1792x1344 | 60Hz     | 4:3        |                        |
| 63        | 1792x1344 | 75Hz     | 4:3        |                        |
| 64        | 1792x1344 | 120Hz    | 4:3        | 降低清屏时间（reduced blanking）               |
| 65        | 1856x1392 | 60Hz     | 4:3        |                        |
| 66        | 1856x1392 | 75Hz     | 4:3        |                        |
| 67        | 1856x1392 | 120Hz    | 4:3        | 降低清屏时间（reduced blanking）               |
| 68        | 1920x1200 | 60Hz     | 16:10      | 降低清屏时间（reduced blanking）               |
| 69        | 1920x1200 | 60Hz     | 16:10      |                        |
| 70        | 1920x1200 | 75Hz     | 16:10      |                        |
| 71        | 1920x1200 | 85Hz     | 16:10      |                        |
| 72        | 1920x1200 | 120Hz    | 16:10      | 降低清屏时间（reduced blanking）               |
| 73        | 1920x1440 | 60Hz     | 4:3        |                        |
| 74        | 1920x1440 | 75Hz     | 4:3        |                        |
| 75        | 1920x1440 | 120Hz    | 4:3        | 降低清屏时间（reduced blanking）               |
| 76        | 2560x1600 | 60Hz     | 16:10      | 降低清屏时间（reduced blanking）               |
| 77        | 2560x1600 | 60Hz     | 16:10      |                        |
| 78        | 2560x1600 | 75Hz     | 16:10      |                        |
| 79        | 2560x1600 | 85Hz     | 16:10      |                        |
| 80        | 2560x1600 | 120Hz    | 16:10      | 降低清屏时间（reduced blanking）               |
| 81        | 1366x768  | 60Hz     | 16:9       | [不适用于树莓派 4 和 5](https://www.raspberrypi.com/documentation/computers/config_txt.html#hdmi-pipeline-for-raspberry-pi-4-and-5)                       |
| 82        | 1920x1080 | 60Hz     | 16:9       | 1080p                  |
| 83        | 1600x900  | 60Hz     | 16:9       | 降低清屏时间（reduced blanking）               |
| 84        | 2048x1152 | 60Hz     | 16:9       | 降低清屏时间（reduced blanking）               |
| 85        | 1280x720  | 60Hz     | 16:9       | 720p                   |
| 86        | 1366x768  | 60Hz     | 16:9       | 降低清屏时间（reduced blanking）               |

>**注意**
>
>旧版树莓派 4 之前的型号支持的最高模式为 1920×1200，带有降低清屏时间（reduced blanking）的 60Hz，而树莓派 4 可以支持高达 4096×2160（口语上称为 4k）的 60Hz。还请注意，如果您正在使用树莓派 4 的两个 HDMI 端口进行 4k 输出，则两者的输出都将限制在 30Hz。


#### `hdmi_timings`

允许设置原始 HDMI 定时值，用 hdmi_group=2 和 hdmi_mode=87 选择自定义模式。

```
hdmi_timings=<h_active_pixels> <h_sync_polarity> <h_front_porch> <h_sync_pulse> <h_back_porch> <v_active_lines> <v_sync_polarity> <v_front_porch> <v_sync_pulse> <v_back_porch> <v_sync_offset_a> <v_sync_offset_b> <pixel_rep> <frame_rate> <interlaced> <pixel_freq> <aspect_ratio>
```

```
<h_active_pixels> = horizontal pixels (width)
<h_sync_polarity> = invert hsync polarity
<h_front_porch>   = horizontal forward padding from DE active edge
<h_sync_pulse>    = hsync pulse width in pixel clocks
<h_back_porch>    = vertical back padding from DE active edge
<v_active_lines>  = vertical pixels height (lines)
<v_sync_polarity> = invert vsync polarity
<v_front_porch>   = vertical forward padding from DE active edge
<v_sync_pulse>    = vsync pulse width in pixel clocks
<v_back_porch>    = vertical back padding from DE active edge
<v_sync_offset_a> = leave at zero
<v_sync_offset_b> = leave at zero
<pixel_rep>       = leave at zero
<frame_rate>      = screen refresh rate in Hz
<interlaced>      = leave at zero
<pixel_freq>      = clock frequency (h_active_pixels + h_front_porch + h_sync_pulse + h_back_porch)
                                    * (v_active_lines + v_front_porch + v_sync_pulse + v_back_porch)
                                    * framerate
<aspect_ratio>    = [see footnote]
```

可将宽高比设置为八个值之一。从以下内容中选择一个代表与您屏幕最相似的宽高比的值：

| 宽高比 | 名称              | 值 |
| -------- | ------------------- | ---- |
| 4:3    | HDMI_ASPECT_4_3   | 1  |
| 14:9   | HDMI_ASPECT_14_9  | 2  |
| 16:9   | HDMI_ASPECT_16_9  | 3  |
| 5:4    | HDMI_ASPECT_5_4   | 4  |
| 16:10  | HDMI_ASPECT_16_10 | 5  |
| 15:9   | HDMI_ASPECT_15_9  | 6  |
| 21:9   | HDMI_ASPECT_21_9  | 7  |
| 64:27  | HDMI_ASPECT_64_27 | 8  |

#### `hdmi_force_mode`

将设置为 1 将从内部列表中删除除 hdmi_mode 和 hdmi_group 指定的模式之外的所有其他模式，这意味着它们不会出现在任何模式的枚举列表中。如果显示似乎忽略 hdmi_mode 和 hdmi_group 设置，此选项可能有所帮助。

#### `edid_content_type`

强制将 EDID 内容类型设置为特定值。

 选项如下：

* 0 = EDID_ContentType_NODATA ，内容类型为 none
* 1 = EDID_ContentType_Graphics ，内容类型为图形，ITC 必须设置为 1
* 2 = EDID_ContentType_Photo ，内容类型为照片
* 3 = EDID_ContentType_Cinema ，内容类型为电影
* 4 = EDID_ContentType_Game ，内容类型游戏

### 我的显示器可以使用哪些值？

您的 HDMI 显示器可能仅支持有限的格式。要找出支持的格式，请使用以下方法：

* 将输出格式设置为 VGA 60Hz ( hdmi_group=1 和 hdmi_mode=1 ) 并启动您的树莓派
* 输入以下命令以列出支持的 CEA 模式: /opt/vc/bin/tvservice -m CEA
* 输入以下命令以列出支持的 DMT 模式: /opt/vc/bin/tvservice -m DMT
* 输入以下命令以显示当前状态： /opt/vc/bin/tvservice -s
* 输入以下命令以从您的监视器中获取更详细的信息： /opt/vc/bin/tvservice -d edid.dat; /opt/vc/bin/edidparser edid.dat

在故障排除默认 HDMI 模式问题时，还应提供 edid.dat 。

### 自定义模式

如果您的显示器需要的模式不在上述表格中，那么可以为其定义一个自定义 CVT 模式：

```
hdmi_cvt=<width> <height> <framerate> <aspect> <margins> <interlace> <rb>
```

| 值     | 默认   | 说明                                               |
| -------- | -------- | ------------------------------------------------------ |
| 宽度   | (必填) | 像素宽度                                             |
| 高度   | (必填) | 像素高度                                             |
| 帧速率 | (必填) | 每秒帧数                                             |
| 宽高比 | 3      | 宽高比 1=4:3, 2=14:9, 3=16:9, 4=5:4, 5=16:10, 6=15:9 |
| 边距   | 0      | 0=边距禁用, 1=边距启用                               |
| 交错   | 0      | 0=逐行扫描，1=隔行扫描                               |
| rb     | 0      | 0=正常，1=降低清屏时间（reduced blanking）                                   |

结尾处的字段可以省略以使用默认值。

请注意，这只是创建模式（第 2 组模式 87）。要使树莓派默认使用此模式，您必须添加一些附加设置。例如，要选择 800×480 分辨率并启用音频驱动：

```
hdmi_cvt=800 480 60 6
hdmi_group=2
hdmi_mode=87
hdmi_drive=2
```

如果您的显示器不支持标准 CVT 时序，则可能无法正常工作。

### 复合视频模式

#### `sdtv_mode`

sdtv_mode 命令定义了用于复合视频输出的电视标准。

| 标准电视模式 | 结果                                              |
| -------------- | --------------------------------------------------- |
| 0（默认）    | 正常的 NTSC                                       |
| 1            | NTSC 的日本版本-没有基座                          |
| 2            | 正常的 PAL                                        |
| 3            | PAL 的巴西版本-525/60 而不是 625/50，不同的子载波 |
| 16           | 逐行扫描 NTSC                                     |
| 18           | 逐行扫描 PAL                                      |

#### `sdtv_aspect`

sdtv_aspect 命令定义了复合视频输出的纵横比。默认值为 1 。

| sdtv_aspect | 结果 |
| ------------- | -------- |
| 1           | 4:3    |
| 2           | 14:9   |
| 3           | 16:9   |

#### `sdtv_disable_colourburst`

将 sdtv_disable_colourburst 设置为 1 会禁用复合视频输出上的彩色爆发。图片将以单色显示，但可能会更清晰。

### 液晶显示屏和触摸屏

#### `display_default_lcd`

如果检测到树莓派触摸显示屏，它将被用作默认显示器，并显示帧缓冲区。设置 display_default_lcd=0 将确保液晶显示屏不是默认显示器，这通常意味着 HDMI 输出将是默认的。仍然可以通过从支持的应用程序中选择其显示编号来使用液晶显示屏，例如，omxplayer。

#### `lcd_framerate`

指定树莓派触摸显示屏的帧率，单位为 Hz/fps。默认为 60Hz。

#### `lcd_rotate`

这会使用 LCD 内置的翻转功能翻转显示，这比使用基于 GPU 的旋转操作更省计算资源。

例如， lcd_rotate=2 将补偿倒置显示。

#### `enable_dpi_lcd`

启用连接到 DPI GPIO 的 LCD 显示器。这是为了允许使用并行显示接口的第三方 LCD 显示器。

#### `dpi_group`, `dpi_mode`, `dpi_output_format`

dpi_group 和 dpi_mode config.txt 参数用于设置预定模式（DMT 或 CEA 模式，与 HDMI 上使用的相同）。用户可以以与 HDMI 相同的方式生成自定义模式（请参阅 dpi_timings 部分）。

dpi_output_format 是一个位掩码，指定用于设置显示格式的各种参数。

#### `dpi_timings`

允许设置原始 DPI 定时值，用于自定义模式，通过 dpi_group=2 和 dpi_mode=87 选择。

```
dpi_timings=<h_active_pixels> <h_sync_polarity> <h_front_porch> <h_sync_pulse> <h_back_porch> <v_active_lines> <v_sync_polarity> <v_front_porch> <v_sync_pulse> <v_back_porch> <v_sync_offset_a> <v_sync_offset_b> <pixel_rep> <frame_rate> <interlaced> <pixel_freq> <aspect_ratio>
```

```
<h_active_pixels> = horizontal pixels (width)
<h_sync_polarity> = invert hsync polarity
<h_front_porch>   = horizontal forward padding from DE active edge
<h_sync_pulse>    = hsync pulse width in pixel clocks
<h_back_porch>    = vertical back padding from DE active edge
<v_active_lines>  = vertical pixels height (lines)
<v_sync_polarity> = invert vsync polarity
<v_front_porch>   = vertical forward padding from DE active edge
<v_sync_pulse>    = vsync pulse width in pixel clocks
<v_back_porch>    = vertical back padding from DE active edge
<v_sync_offset_a> = leave at zero
<v_sync_offset_b> = leave at zero
<pixel_rep>       = leave at zero
<frame_rate>      = screen refresh rate in Hz
<interlaced>      = leave at zero
<pixel_freq>      = clock frequency (h_active_pixels + h_front_porch + h_sync_pulse + h_back_porch)
                                    * (v_active_lines + v_front_porch + v_sync_pulse + v_back_porch)
                                    * framerate
<aspect_ratio>    = [see footnote]
```

可将宽高比设置为八个值之一。从以下选项中选择一个代表与您屏幕最相似的宽高比的值：

| 宽高比 | 名称              | 值 |
| -------- | ------------------- | ---- |
| 4:3    | HDMI_ASPECT_4_3   | 1  |
| 14:9   | HDMI_ASPECT_14_9  | 2  |
| 16:9   | HDMI_ASPECT_16_9  | 3  |
| 5:4    | HDMI_ASPECT_5_4   | 4  |
| 16:10  | HDMI_ASPECT_16_10 | 5  |
| 15:9   | HDMI_ASPECT_15_9  | 6  |
| 21:9   | HDMI_ASPECT_21_9  | 7  |
| 64:27  | HDMI_ASPECT_64_27 | 8  |

### 通用显示选项

#### `hdmi_force_hotplug`

将 hdmi_force_hotplug 设置为 1 会假装 HDMI 热插拔信号已被断开，因此看起来好像没有连接 HDMI 显示器。换句话说，即使没有检测到 HDMI 监视器，也会使用 HDMI 输出模式。

#### `hdmi_ignore_hotplug`

将 hdmi_ignore_hotplug 设置为 1 会假装 HDMI 热插拔信号已被断开，因此看起来好像没有连接 HDMI 显示器。因此，即使连接了监视器，HDMI 输出也将被禁用。

#### `disable_overscan`

disable_overscan 的默认值为 0 ，这为 HD CEA 模式的左、右、上和下边缘以及 SD CEA 模式的 32 和 DMT 模式的 0 提供了默认的过扫描值。

将 disable_overscan 设置为 1 以禁用固件设置的超扫描的默认值。

#### `overscan_left`

overscan_left 命令指定要添加到屏幕左边缘的固件默认超扫描值的像素数。默认值为 0 。

如果文本超出屏幕左边缘，请增加此值；如果屏幕左边缘和文本之间有黑色边框，请减少此值。

#### `overscan_right`

overscan_right 命令指定要添加到屏幕右边缘超扫描的固件默认值的像素数。默认值为 0 。

如果文本超出屏幕右边缘，请增加此值；如果屏幕右边缘和文本之间有黑色边框，请减小此值。

#### `overscan_top`

overscan_top 命令指定要添加到屏幕顶部超扫描的固件默认值的像素数。默认值为 0 。

如果文本超出屏幕顶部边缘，请增加此值；如果屏幕顶部边缘和文本之间有黑色边框，请减小此值。

#### `overscan_bottom`

overscan_bottom 命令指定要添加到屏幕底部边缘超扫描的像素数。默认值为 0 。

如果文本超出屏幕底部边缘，请增加此值；如果屏幕底部边缘和文本之间有黑色边框，请减小此值。

#### `overscan_scale`

将 overscan_scale 设置为 1 以强制任何非帧缓冲层符合超扫描设置。默认值为 0 。

注意：通常不建议使用此功能：因为显示器上的所有图层都将由 GPU 缩放，这可能会降低图像质量。建议在显示器本身上禁用超扫描，以避免图像被 GPU 和显示器两次缩放。

#### `framebuffer_width`

framebuffer_width 命令指定像素中的控制台帧缓冲区宽度。默认值为显示宽度减去总水平超扫描量。

#### `framebuffer_height`

framebuffer_height 命令指定控制台帧缓冲区的像素高度。默认值为显示高度减去总垂直过扫描。

#### `max_framebuffer_height`, `max_framebuffer_width`

指定内部帧缓冲区的最大尺寸。

#### `framebuffer_depth`

使用 framebuffer_depth 来指定每像素位的控制台帧缓冲区深度。默认值为 16 。

| 帧缓冲深度 | 结果          | 注解                                           |
| ------------ | --------------- | ------------------------------------------------ |
| 8          | 8 位帧缓冲区  | 默认 RGB 调色板使屏幕难以阅读                  |
| 16         | 16 位帧缓冲区 |                                                |
| 24         | 24 位帧缓冲区 | 可能导致显示损坏                               |
| 32         | 32 位帧缓冲区 | 可能需要与 framebuffer_ignore_alpha=1 一起使用 |

#### `framebuffer_ignore_alpha`

将 framebuffer_ignore_alpha 设置为 1 以禁用 alpha 通道。可以改善 32 位 framebuffer_depth 的显示。

#### `framebuffer_priority`

在具有多个显示器的系统中，使用旧版（KMS 之前）图形驱动程序，这将强制特定的内部显示设备成为第一个 Linux 帧缓冲区（即 /dev/fb0 ）。

可设置的选项有：

| 显示           | ID |
| ---------------- | ---- |
| 主 LCD         | 0  |
| 次要液晶显示器 | 1  |
| HDMI 0         | 2  |
| 复合视频       | 3  |
| HDMI 1         | 7  |

#### `max_framebuffers`

此配置条目设置可创建的固件帧缓冲区的最大数量。有效选项为 0、1 和 2。在旧版的设备上，默认设置为 1，因此在使用多个显示器时（例如 HDMI 和 DSI 或 DPI 显示器），需要将其增加到 2。树莓派 4 的配置将此默认设置为 2，因为它有两个 HDMI 端口。

在大多数情况下将其设置为 2 是安全的，因为只有在实际检测到连接的设备时才会创建帧缓冲区。

将此值设置为 0 可用于在无头模式下减少内存需求，因为这将阻止分配任何帧缓冲区。

#### `test_mode`

test_mode 命令在启动过程中显示测试图像和声音（仅通过复合视频和模拟音频输出），持续给定的秒数，然后继续正常启动操作系统。这用作制造测试；默认值为 0 。

#### `display_hdmi_rotate`

使用 display_hdmi_rotate 旋转或翻转 HDMI 显示方向。默认值为 0 。

| 显示 _hdmi_ 旋转 | 结果              |
| ---------------- | ------------------- |
| 0              | 无旋转            |
| 1              | 顺时针旋转 90 度  |
| 2              | 顺时针旋转 180 度 |
| 3              | 顺时针旋转 270 度 |
| 65536          | 水平翻转          |
| 131072         | 垂直翻转          |

请注意，90 度和 270 度旋转选项需要 GPU 上额外的内存，因此这些选项在 16MB GPU 分配下无法使用。

您可以通过将旋转设置与翻转相结合来将它们相加。您也可以以相同的方式同时进行水平和垂直翻转。例如，180 度旋转与垂直和水平翻转将为 0x20000 + 0x10000 + 2 = 0x30002。

#### `display_lcd_rotate`

对于旧版图形驱动程序（适用于早于树莓派 4 的型号），请使用 display_lcd_rotate 旋转或翻转 LCD 方向。参数与 display_hdmi_rotate 相同。另请参阅 lcd_rotate 。

#### `display_rotate`

在最新固件中， display_rotate 已被弃用。仅保留以确保向后兼容性。请改用 display_lcd_rotate 和 display_hdmi_rotate 。

使用 display_rotate 旋转或翻转屏幕方向。参数与 display_hdmi_rotate 相同。

### 其他选项

#### `dispmanx_offline`

强制 dispmanx 组合在两个离屏帧缓冲区中离线完成。这样可以允许更多的 dispmanx 元素进行合成，但速度较慢，可能会将屏幕帧速率限制在大约 30fps 左右。

## 旧版树莓派 4 HDMI 管道


>**重要**
>
>当使用 VC4 KMS 图形驱动程序时，完整的显示管道由 Linux 管理 - 包括 HDMI 输出。这些设置仅适用于旧版 FKMS 和基于固件的图形驱动程序。

树莓派 4 无法在 HDMI 上输出 1366×768 @ 60Hz。在某些显示器上，可以配置它们使用 1360×768 @ 60Hz。它们通常不通过 EDID 广告此模式，因此无法自动进行选择，但可以通过手动添加来选择：

```
hdmi_group=2
hdmi_mode=87
hdmi_cvt=1360 768 60
```

 …到 config.txt。

通过 hdmi_timings= 行手动指定的时间也需要遵守所有水平定时参数必须是 2 的倍数的限制。

dpi_timings= 不受相同限制，因为该管道仍然每个时钟周期仅运行一个像素。

## 旧版杂项选项

### `avoid_warnings`

avoid_warnings=2 即使低电压存在也允许使用 turbo 模式。

### `logging_level`

设置 VideoCore 日志级别。该值是一个 VideoCore 特定的位掩码。
