# config.txt

## `config.txt` 是什么？

树莓派设备采用配置文件——`config.txt`，来代替普通 PC 上的 [BIOS](https://en.wikipedia.org/wiki/BIOS) 。GPU 会先读取 `config.txt`，然后再初始化 Arm CPU 和 Linux。树莓派系统会在 **启动分区**（`/boot/firmware/`）中查找 `config.txt`。

>**注意**
>
>树莓派 *Bookworm* 之前的系统，会把启动分区放在 `/boot/`。

你可以直接在你当前的树莓派系统上编辑 `config.txt`。你也可弹出存储设备，在其他计算机上，编辑启动分区中的文件（如 `config.txt`）。

所有对 `config.txt` 的修改，仅在重启后生效。你可使用以下命令，查看当下使用的设置：

`vcgencmd get_config <选项>` 

　　显示指定选项的值，如 `vcgencmd get_config arm_freq`

`vcgencmd get_config int` 

　　列出所有非零整数选项（非 0）

`vcgencmd get_config str`

　　列出所有非空字符串选项

>**注意**
>
>`vcgencmd` 并不能检索全部的选项。

### 文件格式

文件 `config.txt` 由早期启动固件读取，因此采用的文件格式非常简单：**每行一个语句：`属性=值`，其中 `值` 可以是整数或字符串。** 可以通过在行首添加字符 `#` 来插入注释，或注释掉现有配置值以禁用。

每行条目的最大长度为 98 个字符。树莓派系统会忽略掉任何超出此限制的字符。

此处是示例文件：

```
# 开启音频（加载 snd_bcm2835）
dtparam=audio=on

# 自动检测新加摄像头叠加层
camera_auto_detect=1

# 自动检测新加 DSI 显示器
display_auto_detect=1

# 开启 DRM VC4 V3D 驱动
dtoverlay=vc4-kms-v3d
```

### 高级功能

#### `include`

引用指定文件的内容到当前文件。

比如：把 `include extraconfig.txt` 这行添加到 `config.txt`——将在 `config.txt` 文件中引用文件 `extraconfig.txt` 的内容。

>**注意**
>
>`bootcode.bin`、EEPROM 引导加载程序均不支持 include 指令。
>
>由引导加载程序控制的设置，只有在 `config.txt`（而非其他附带文件）中指定时才会生效：
>
>* `bootcode_delay`、
>* `gpu_mem`、`gpu_mem_256`、`gpu_mem_512`、`gpu_mem_1024`、
>* `total_mem`、
>* `sdram_freq`、
>* `start_x`、`start_debug`、`start_file`、`fixup_file`、
>* `uart_2ndstage`。

#### 条件筛选

条件筛选器位于[条件部分](https://www.raspberrypi.com/documentation/computers/config_txt.html#conditional-filters)。

## `autoboot.txt`

`autoboot.txt` 是可选配置文件，可用于指定 `boot_partition` 的编号。

也可与功能 `tryboot` 一同使用，实现系统更新的 A/B 启动。

`autoboot.txt` 被限制为 512 字节，支持[条件](https://www.raspberrypi.com/documentation/computers/config_txt.html#conditional-filters)筛选器 `[all]`、`[none]` 和 `[tryboot]` 。

另见 [TRYBOOT](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#fail-safe-os-updates-tryboot) 启动流程。

### `boot_partition`

指定启动的分区号。也可以直接把分区号作为参数传给命令 `reboot`（如 `sudo reboot 2`）来实现。

分区号从 `1` 开始，MBR 分区为 `1` 到 `4`。指定分区 `0` 表示从 **默认** 分区启动，默认分区是首个可引导的 FAT 分区。

作为启动分区，其文件系统仅支持 FAT12、FAT16 和 FAT32，并包含一个 `start.elf` 文件（若为树莓派 5，则改为文件 `config.txt`），以便引导程序将其视为可引导。

### 筛选器 `[tryboot]` 

如果系统在启动时设置了标志位 `tryboot`，则此筛选器将被激活。

```
$ sudo reboot "0 tryboot"
```

### `tryboot_a_b`

当标志位 `tryboot` 被激活后，若将属性 `tryboot_a_b` 置为 `1`，会加载普通文件 `config.txt` 和 `boot.img`，而不会加载文件 `tryboot.txt` 和 `tryboot.img`，。

这样就可以在分区级（而非在文件级）上控制 `tryboot` 的开关，且无需修改 A/B 分区中的配置文件。

### A/B 启动更新流程示例

以下伪代码：假设操作系统更新服务在 `autoboot.txt` 中使用 `tryboot` 执行安全的操作系统更新。

简单的 `autoboot.txt` :

```
[all]
tryboot_a_b=1
boot_partition=2
[tryboot]
boot_partition=3
```

**安装更新**

* 设备上电，然后从默认分区 2 启动
* `Update service（更新服务）`下载新版操作系统到分区 3
* 重启到 `tryboot` 模式：用 `reboot "0 tryboot"` 来测试更新，其中 `0` 代表默认分区

**进行、取消更新**

* 系统将从分区 3 启动，因为在 `tryboot mode` 中，筛选器 `[tryboot]` 的结果为 true
* 如果 `tryboot` 处于激活状态 ( `/proc/device-tree/chosen/bootloader/tryboot == 1` )
  * 如果当前的启动分区（ `/proc/device-tree/chosen/bootloader/partition` ）与 `autoboot.txt` 部分的 `[tryboot]`（`boot_partition`）相匹配
    * `Update service（更新服务）`验证系统以确保更新成功
    * 如果更新成功
      * 替换 `autoboot.txt` 以交换 `boot_partition` 配置
      * 正常重启：现在默认启动分区是分区 3
    * 如果更新失败
      * `Update service（更新服务）`将更新标记为失败（如删除更新文件）。
      * 正常重启：默认的启动分区仍是分区 2，因为标志位 `tryboot` 会被自动清除
    * 结束更新
  * 结束更新
* 结束更新

 更新 `autoboot.txt`：

```
[all]
tryboot_a_b=1
boot_partition=3
[tryboot]
boot_partition=2
```

>**注意**
>
>更新 `autoboot.txt` 后并不必须重启。然而，必须小心 `Update service（更新服务）`，谨防覆盖当前分区：因为已经修改了 `autoboot.txt`，执行了最后的更新。有关更多信息，请参阅[设备树参数](https://www.raspberrypi.com/documentation/computers/configuration.html#device-trees-overlays-and-parameters)。

## 常见选项
 

### 常见显示选项

#### `hdmi_enable_4kp60`（仅适用于树莓派 4）

在默认情况下，当接入 4K 显示器时，树莓派 4B、400 和 CM4 将输出 30Hz 刷新率。使用此选项可输出 60Hz 刷新率。树莓派 4 无法同时在两个 micro HDMI 接口上输出 4Kp60。设置 `hdmi_enable_4kp60` 会增加功耗和温度。

### 常见硬件配置选项

#### `camera_auto_detect`

启用此设置（树莓派系统默认已启用），固件将自动加载所识别的 CSI 摄像头叠加层。如 `camera_auto_detect=0` 则表示禁用该设置。

#### `display_auto_detect`

启用此设置（树莓派系统默认已启用），固件将自动加载所识别的 DSI 显示屏的叠加层。设置 `display_auto_detect=0` 可禁用。

#### `dtoverlay`

`dtoverlay` 选项将要求固件加载指定的设备树覆盖层——这是个配置文件，可启用内、外围硬件的内核支持。例如，`dtoverlay=vc4-kms-v3d` 会加载叠加层，启用内核图形驱动程序。

作为例外，如果在调用时未赋值（即 `dtoverlay=`），则表示直接覆盖至参数列表的末尾。如果定义在一切 `dtoverlay`、`dtparam` 参数之前，那么所有的扩展板叠加层均不会加载。

更多有关信息，请参阅 [DTB、叠加层和 `config.txt`](https://www.raspberrypi.com/documentation/computers/configuration.html#part3.1)。

#### `dtparam`

树莓派的设备树配置文件支持多种参数，如启用 I²C、SPI 接口。大部分 DT 叠加层也都能用参数进行配置。这两类的参数都可以用 `dtparam` 进行配置。此外，还可以把叠加层参数添加到选项 `dtoverlay` 里：以逗号分隔，但请注意，字符长度限制为 98 个字符。

欲了解更多详情，请查阅 DTB、叠加层和 `config.txt`。

#### `arm_boost`（仅适用于树莓派 4）

所有树莓派 400 系列和修订版树莓派 4B 均搭载了额外的开关电源（SMPS）（用于 SoC 电压轨），这使默认超频状态下的主频，从 1.5GHz 提升到 1.8GHz。此更改在树莓派系统下默认已生效。设置 `arm_boost=0` 可禁用。

#### `power_force_3v3_pwm`（仅适用于树莓派 5）

使用 3.3V 电源时强制 PWM。设置 `power_force_3v3_pwm=0` 可禁用。

## 板载模拟音频（3.5 mm 插孔）
 
使用配置选项可以修改板载音频输出的模拟音频驱动方式，以及是否启用某些固件功能。

### `audio_pwm_mode`

`audio_pwm_mode=1` 选择传统低质量模拟音频，基于 3.5 mm AV 接口。

`audio_pwm_mode=2` 选择使用高级调制方案的高质量模拟音频。（默认）

>**注意**
>
>此选项将占用更多的 GPU 计算资源，可能会对某些型号的特定用例造成影响。

### `disable_audio_dither`

在默认情况下，如果音频流路由输出到了模拟音频，则会应用 1.0LSB 抖动。在某些情况下（如 ALSA 音量处于较低水平），就有可能产生可感的背景噪音。将 `disable_audio_dither` 置为 `1` 可禁用抖动功能。

### `enable_audio_dither`

当音频样本大于 16 位时，通常就会禁用音频抖动（请参阅上述 `disable_audio_dither`）。将此选项置为 `1` 可强制对所有位深度都应用抖动。

### `pwm_sample_bits`

命令 `pwm_sample_bits` 能调整模拟音频输出的位深度。默认位深度为 `11`。如果位深度设置低于 `8`，音频将无法正常工作。因为低于 `8` 的值会导致 PLL 频率过低：对于设备来说，是不可能的。该参数通常仅用于演示位深度对量化噪声的影响。

## HDMI 音频

在默认情况下，所有搭载了 HDMI 输出接口的树莓派型号，均启用了 HDMI 音频输出。

要禁用 HDMI 音频输出，请在 `/boot/firmware/config.txt` 中的 `dtoverlay=vc4-kms-v3d` 这行末尾添加 `,noaudio` ：

```
dtoverlay=vc4-kms-v3d,noaudio
```

## 启动选项

### `start_file`、`fixup_file`

这些选项指可指定：在启动前传给 VideoCore GPU 的固件文件。

`start_file` 指定要使用的 VideoCore 固件文件。`fixup_file` 用于修正 `start_file` 所使用的内存位置，以匹配 GPU 内存分配。

`start_file` 和 `fixup_file` 是一对关联文件：错误搭配将导致开发板无法启动。这是个专业选项，因此我们不建议你使用，你应该用 `start_x` 和 `start_debug`。

>**注意**
>
>使用配置参数 `start*cd.elf`、`fixup*cd.dat` 无法调用精简固件，只会导致系统无法启动。唯一能启用精简固件的方法是指定 `gpu_mem=16`。精简固件删除了对编解码器、3D 和调试日志的支持，以及把初始早期引导帧缓冲区限制成 1080p @16bpp——正如同其他固件，KMS 在后续阶段可使用高达 32bpp 4K 帧缓冲区代替之。


>**注意**
>
>树莓派 5 的固件内置在引导加载程序 EEPROM 中。

### `cmdline`

`cmdline` 是启动分区中的一个可选文件名（默认值为 `cmdline.txt`），用于读取内核命令行字符串。

### `kernel`

`kernel` 是用于加载内核的启动分区上的一个可选文件名。树莓派 1，树莓派 Zero、Zero W 和计算模块 1 的默认值为 `kernel.img`。树莓派 2、3、3+，树莓派 Zero 2 W，计算模块 3、3+ 的默认值为 `kernel7.img`。树莓派 4、400 和计算模块 4 的默认值为 `kernel8.img`；如将 `arm_64bit` 设置为 0，则默认值为 `kernel7l.img`。

树莓派 5 固件默认加载 `kernel_2712.img`，因为此镜像为树莓派 5 进行了优化（例如 16K 页面大小）。如果此文件不存在，则会加载 64 位通用内核（ `kernel8.img`）。

### `arm_64bit`

如果置为 1，则内核将以 64 位模式启动。设置为 0 会选择 32 位模式。

在 64 位模式下，固件将选择合适的内核（例如 `kernel8.img`）。如未显式设置参数 `kernel`，则将使用该选项。

在树莓派 4 系列（4B、400、CM4 和 CM4S）上默认值为 1，在其他所有平台上默认值为 0。但是，如果显式设置的选项 `kernel` 中给定的名称与已知的任一内核匹配，则 `arm_64bit` 将应用相应设置。

>**注意**
>
>64 位内核可以是未压缩的镜像文件，也可以是 gzip 压缩的镜像文件（仍可称为作 kernel8.img。引导加载程序能从开头的签名字节识别压缩文件）。64 位内核仅适用于树莓派 3、3+、4、400，树莓派 Zero 2 W，树莓派 2B 修订版 1.2，树莓派计算模块 3、3+、4。树莓派 5 仅支持 64 位内核，因此对树莓派 5 来说，此参数无效。

### `ramfsfile`

`ramfsfile` 是引导分区上的 `ramfs` 的一个可选文件名。

>**注意**
>
>新版固件可加载多个 `ramfs` 文件。请注意：多个文件名需以逗号分隔，不要超过 80 个字符的行长限制。所有已加载的文件在内存中拼接在一起，被视为单个 `ramfs` 二进制块。有关更多信息，请参阅[论坛](https://forums.raspberrypi.com/viewtopic.php?f=63&t=10532&_gl=1*1f9jjcx*_ga*ODAwMTM3MTg4LjE3MTc1NzY1NTQ.*_ga_22FD70LWDS*MTcyMTU1MzIwNy41MS4xLjE3MjE1NTMyMjIuMC4wLjA.)。

### `ramfsaddr`

`ramfsaddr` 指定 `ramfsfile` 将加载的内存地址。

### `initramfs`

命令 `initramfs` 同时指定了 ramfs 的文件名 **和** ramfs 将加载的内存地址。它在一个参数中同时执行了操作 `ramfsfile` 和 `ramfsaddr`。地址也可以是 `followkernel` （或 `0`），将其放在内核镜像之后的内存中。示例值为：`initramfs initramf.gz 0x00800000`、`initramfs init.gz followkernel`。同 `ramfsfile` 一样，新版固件可加载多个文件，多个文件名以逗号分隔。

>**注意**
>
>选项 `initramfs` 使用的语法与其他选项有所不同，你不能在此处使用字符 `=`。

### `auto_initramfs`

如果把 `auto_initramfs` 置为 `1`，将按照所选内核的匹配规则查找文件 `initramfs`。

### `disable_poe_fan`

在默认情况下，启动时，会在 I²C 总线上进行探测（哪怕并未接入 PoE 扩展板）。将此参数置为 1，可禁用在 I²C（在 `ID_SD＆ID_SC` 引脚）上对 PoE 扩展板风扇的检测行为。如果你不打算使用 PoE 扩展板，那么这是最大程度上缩短启动时间的有效方式。

### `disable_splash`

如果将 `disable_splash` 置为 1，启动时将不会出现彩虹屏。默认值为 `0`。

### `enable_uart`

`enable_uart=1` （与 `console=serial0` 在 `cmdline.txt` 中联合使用）能让内核创建串口控制台——可使用 GPIO 14 和 15（40 脚排针上的引脚 8 和引脚 10）访问。编辑 `cmdline.txt`，删除 `quiet` 字段，就能把内核的启动消息也输出到这个串口上。另请参阅 `uart_2ndstage`。

### `force_eeprom_read`

将此选项置为 `0` 可禁止：固件在上电时读取 I²C 扩展板的 EEPROM（连接至 `ID_SD` 和 `ID_SC` 引脚）。另请参阅 [`disable_poe_fan`](https://www.raspberrypi.com/documentation/computers/config_txt.html#disable_poe_fan)。

### `os_prefix`

`os_prefix` 是可选配置，能让你在同一张卡上，安装多个版本的内核和设备树文件，并进行切换。`os_prefix` 中的任何值都会被前置到固件加载的所有操作系统文件的名称之前，其中“操作系统文件”的定义是指内核、`initramfs`、`cmdline.txt`、`.dtbs` 和叠加层。该前缀通常是目录名称，但也可以是文件名的一部分，比如“test-”。因此，目录前缀必须以字符 `/` 结尾。

为了提高系统启动的几率，固件首先会测试所提供的前缀值是否可行——除非在新位置/新名称下能够找到对应的内核和文件 .dtb，否则将忽略前缀（置为“”）。对叠加层可行性测试的特例是：如果存在 `${os_prefix}${overlay_prefix}README`，将仅从 `${os_prefix}${overlay_prefix}` （其中 [`overlay_prefix`](https://www.raspberrypi.com/documentation/computers/config_txt.html#overlay_prefix) 的默认值为 "overlays/"）加载覆盖层；否则，它将忽略 `os_prefix`，并将叠加层视为共享。

（固件在检查前缀时，是判断关键文件（而非目录）的存在与否。原因有二：前缀可能不是目录，并非所有启动方法都支持使用测试目录。）

>**注意**
>
>所有操作系统文件都可以通过用户指定使用的绝对路径（相对于启动分区）来修改前缀——只需以 `/` 开头：如 `kernel=/my_common_kernel.img`。

另请参阅 [`overlay_prefix`](https://www.raspberrypi.com/documentation/computers/config_txt.html#overlay_prefix) 和 [`upstream_kernel`](https://www.raspberrypi.com/documentation/computers/legacy_config_txt.html#upstream_kernel)。

### `otg_mode`（仅适用于树莓派 4）。

USB On-The-Go（通常缩写为 OTG）是一项功能，它能让受支持的 USB 设备通过相应的 OTG 线把自己配置成 USB 主机。在旧款树莓派系列上，单个 USB2 控制器可同时作为 USB 主机模式和 USB 设备模式。

树莓派 4B 和 400（不含 CM4、CM4IO）添加了一个连接至 PCIe 的高性能 USB 3 控制器，用于驱动主要的 USB 端口。传统的 USB 2 控制器仍然可用：它通过 Type-C 电源接口，以设备模式进行连接。（`otg_mode=0` 为默认）。

`otg_mode=1` 可将 Type-C 接口的主控制器切换成更为强大的 XHCI USB 2 控制器。

>**注意**
>
>由于 CM4 和 CM4IO 未搭载单独的 USB 3 控制器，在树莓派操作系统镜像上，为 CM4 上设置了 `otg_mode=1`，以实现最佳性能。

### `overlay_prefix`

指定从哪个子目录/前缀加载叠加层，默认为 `overlays/` （注意末尾的 `/`）。如果同时使用了 [`os_prefix`](https://www.raspberrypi.com/documentation/computers/config_txt.html#os_prefix) ，则 `os_prefix` 将位于 `overlay_prefix` 之前。即 `dtoverlay=disable-bt` 将会加载 `${os_prefix}${overlay_prefix}disable-bt.dtbo`。

>**注意**
>
>除非存在 `${os_prefix}${overlay_prefix}README`，否则叠加层将与主操作系统复用（即无视 `os_prefix`）。

### 配置属性

树莓派 5 需要一个文件 `config.txt` 来标识分区可启动。

#### `boot_ramdisk`

如果此属性置为 `1`，则引导程序将尝试加载名为 `boot.img` 的 ramdisk 文件（其中包含[引导文件系统](https://www.raspberrypi.com/documentation/computers/configuration.html#boot-folder-contents)）。随后的文件（例如 `start4.elf` ）将从 ramdisk 中读取，而非原始引导文件系统。

`boot_ramdisk` 的主要目的是支持安全启动（`secure-boot`），但未签名的 `boot.img` 文件也可用于网络引导或配置 `RPIBOOT`。

* RAM 磁盘文件的最大值为 96MB。
* `boot.img` 文件是裸磁盘 `.img` 文件。推荐的格式是不带 MBR 的普通 FAT32 分区。
* 在操作系统启动之前从内存中释放 RAM 磁盘文件系统。
* 如果触发 [TRYBOOT](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#fail-safe-os-updates-tryboot)，则引导加载程序将搜索 `tryboot.img` 而非 `boot.img`。
* 另请参阅 [autoboot.txt](https://www.raspberrypi.com/documentation/computers/config_txt.html#autoboot-txt)。

更多有关安全启动（`secure-boot`）和创建 `boot.img` 文件的信息，请参阅 [USBBOOT](https://github.com/raspberrypi/usbboot/blob/master/Readme.md)。

默认值： `0`

#### `boot_load_flags`

定制固件（裸金属）的实验性属性。

位 0 (0x1) 表示 `.elf` 文件为定制固件。这将禁用一切兼容性检查（如是否支持 USB MSD 启动），并在启动可执行文件之前重置 PCIe。

对于树莓派 5 无关紧要，因为它就没有 `start.elf` 这个文件。

默认值： `0x0`

#### `pciex4_reset`

仅适用于树莓派 5。

默认情况下，在启动操作系统之前，会对 `RP1` 使用的 PCIe x4 控制器进行复位。如果此参数置为 `0`，则将禁用复位，以实现操作系统或裸金属代码继承来自引导加载程序的 PCIe 配置设置。

默认值： `1`

#### `uart_2ndstage`

如果 `uart_2ndstage` 为 `1`，则将启用串口调试日志记录。此选项还会自动启用 `start.elf` 中的串口日志记录。这也在[启动选项](https://www.raspberrypi.com/documentation/computers/config_txt.html#boot-options)页上有描述。

属性 `BOOT_UART` 也会启用引导加载程序的串口日志记录，但不会启用 `start.elf` 的串口日志记录——除非同时设置了 `uart_2ndstage=1`。

默认值： `0`

#### `erase_eeprom`

如果 `erase_eeprom` 置为 `1`，那么 `recovery.bin` 将擦除整个 SPI EEPROM，而非刷新引导加载程序镜像。此属性在正常启动期间无效。

默认值：`0`

#### `eeprom_write_protect`

配置 EEPROM 写状态寄存器（`write status register`）。可将整个 EEPROM 标记为写保护，或清除写保护。

该选项必须与控制 EEPROM 写入状态寄存器更新的 EEPROM `/WP` 引脚一同使用。将 `/WP` 的引脚拉低（CM4 为 `EEPROM_nWP`、树莓派 4 为 `TP5`）——但若仅如此，并不会对 EEPROM 写保护，除非同时对写入状态寄存器进行了配置。

可查看 [Winbond W25x40cl](https://www.winbond.com/resource-files/w25x40cl_f%2020140325.pdf)、[Winbond W25Q16JV](https://www.winbond.com/hq/product/code-storage-flash-memory/serial-nor-flash/?__locale=en&partNo=W25Q16JV) 的数据手册以获取更多详细信息。

`config.txt` 中的 `eeprom_write_protect` 设置用于 `recovery.bin`。

| 值 | 说明                              |
| :----: | ----------------------------------- |
| `1`  | 把整个 EEPROM 配置写保护区域。|
| `0`  | 清除写保护区域。        |
| `-1` | 什么也不做。            |

>**注意**
>
>flashrom 不能清除写保护区域，如果定义了写保护区域，将无法更新 EEPROM。

对于树莓派 5，在默认情况下，`/WP` 已拉低，因此只要配置了写状态寄存器，就会启用写保护。要清除写保护，请将 `/WP` 引脚拉高，方法是连接 `TP14` 和 `TP1`。

默认值: `-1`

#### `os_check`

在树莓派 5 上，固件默认会在从当前分区引导之前，自动检查适配的设备树文件。如果没有找到，将加载旧的不兼容的内核，然后可能会卡住。要禁用此检查（如用于裸机开发），请在 `config.txt` 中设置 `os_check=0`。

默认值： `1`

#### `bootloader_update`

可将此选项置为 `0` 以关闭自动更新（无需刷新 EEPROM 配置）。在通过网络引导更新多个树莓派时，有时会很有用，因为可以针对不同的树莓派控制此选项（例如，通过 `config.txt` 中的串号筛选器）。

默认值： `1`

### 安全启动配置属性

##### 白皮书

>[如何使用树莓派安全启动](https://pip.raspberrypi.com/categories/685-whitepapers-app-notes/documents/RP-003466-WP/Boot-Security-Howto.pdf)
>
>本白皮书介了如何在基于树莓派 4 的设备上实现安全启动。有关我们实施安全启动方法的概述，请参阅[树莓派 4 启动安全](https://pip.raspberrypi.com/categories/685-whitepapers-app-notes/documents/RP-004651-WP/Raspberry-Pi-4-Boot-Security.pdf?_gl=1*3s582g*_ga*ODAwMTM3MTg4LjE3MTc1NzY1NTQ.*_ga_22FD70LWDS*MTcyMjI0NDk0Mi43My4xLjE3MjIyNDQ5NDcuMC4wLjA.)白皮书。安全启动系统被设计成与基于 `buildroot` 的操作系统镜像搭配使用；不建议、或者说不支持将其与树莓派系统（Raspberry Pi O）一同使用。

以下 `config.txt` 属性用于编程安全启动的 OTP 设置。这些更改是不可逆的，只能在刷写引导加载程序 EEPROM 镜像时通过 `RPIBOOT` 进行编程。这阻止了使用远程设置或通过意外插入陈旧的 SD 卡镜像进行安全启动。

更多有关启用安全启动的信息，请参阅[安全启动 readme 文件](https://github.com/raspberrypi/usbboot/blob/master/Readme.md#secure-boot)和 [USBBOOT](https://github.com/raspberrypi/usbboot) 存储库中的[安全启动教程](https://github.com/raspberrypi/usbboot/blob/master/secure-boot-example/README.md)。

#### `program_pubkey`

如果将此属性置为 1，则 `recovery.bin` 将把 EEPROM 镜像中的公钥哈希值写入 OTP。一旦设置，启动加载程序将拒绝使用其他 RSA 密钥签名的 EEPROM 镜像及未签名的镜像。

默认值： `0`

#### `revoke_devkey`

如果将此属性置为 1，则 `recovery.bin` 将向 OTP 写入一个值，以阻止 ROM 加载不支持安全启动的旧版第二阶段的启动加载程序。这可以阻止通过回滚到旧版启动加载程序以绕过安全启动的行为。

默认值： `0`

#### `program_rpiboot_gpio`

由于树莓派 4B 和树莓派 400 上没有专用的 `nRPIBOOT` 跳线，因此必须使用别的 GPIO 配置 `RPIBOOT` 模式，可通过拉低 GPIO 来实现。请从以下选项中选择这个 GPIO：

* `2`
* `4`
* `5`
* `6`
* `7`
* `8`

此属性不要求安全启动，但要确认该 GPIO 配置不会与其他扩展板冲突，因为扩展板可能会在启动期间将 GPIO 拉低。

出于安全考量，此属性仅可通过 `RPIBOOT` 进行编程，因此必须首先用 `erase_eeprom` 擦除引导加载程序 EEPROM。这将触发 BCM2711 ROM 故障转移到 `RPIBOOT` 模式，然后才能设置此选项。

默认值：` `

#### `program_jtag_lock`

如果将此属性置为 `1`，则 `recovery.bin` 将编程一个 OTP 值，来禁用 VideoCore JTAG（调试接口）。此选项必须与 `program_pubkey` 和 `revoke_devkey` 同时使用。启用此选项可禁用故障诊断，应仅在设备经过全面测试后设置此选项。

默认值： `0`

## GPIO 控制

### `gpio`

`gpio` 指令能在启动时把 GPIO 引脚设置为特定模式、特定值，这种方式在以前需要一个自定义文件 `dt-blob.bin`。每一行都将相同的设置（或至少相同的更改）应用到一组引脚，可处理单个引脚（`3`）、某区间内的引脚（`3-4`）或以逗号分隔的列表（`3-4,6,8`）。

引脚设置后跟一个 `=` 和此列表中的一个或多个逗号分隔属性：

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

```
# 将 GPIO 引脚 0-27 配置成 Alt2 模式（用于 DPI24）
gpio=0-27=a2

# 将 GPIO12 设置为输出模式，并将其状态设为 1
gpio=12=op,dh

# 更改引脚 18、引脚 20 的上拉、下拉电阻配置（引脚为输入）。
gpio=18,20=pu

# 将引脚 17-21 设置为输入。
gpio=17-21=ip
```

该 gpio 指令兼容 `config.txt` 中的条件筛选器“\[...\]”，因此可以根据型号、序列号和 EDID 使用不同的设置。

通过该机制进行的 GPIO 修改不会直接干预内核。它们不会把 GPIO 引脚暴露到 `sysfs` 接口，并且可被设备树中的 `pinctrl` 条目以及像 `pinctrl` 这样的工具所覆盖。

还请注意，从上电到修改生效会有几秒钟的延迟——如果通过网络启动或从 USB 大容量存储设备启动，那么延迟会更大。

## 超频选项

内核会默认启用驱动程序 [CPUFreq](https://www.kernel.org/doc/html/latest/admin-guide/pm/cpufreq.html)：安装 [raspi-config](https://www.raspberrypi.com/documentation/computers/configuration.html#raspi-config) 后，在启动时会把调度程序从 powersave 切换到 ondemand。通过调度程序 ondemand，CPU 频率将随处理器负载而变化。如果你把配置参数 `*_min` 调整为最小值、使用了静态缩放调度程序（powersave、performance），亦或使用 `force_turbo=1`——他们都会禁用动态频率调整。

当 SoC 在运行时达到 `temp_limit`（见下文，默认为 85°C）时，就会禁用超频和过压功能，以降低 SoC 温度。你不大可能在树莓派 1、2 上受到此限制。在树莓派 3 及更新款上才有可能。当检测到欠电压时，也会禁用超频和过压功能。

>**注意**
>
>更多信息请参阅[频率管理和热控制部分](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#frequency-management-and-thermal-control)。

>**警告**
>
>将任意超频参数设置为非 `raspi-config` 使用的值可能会导致在 SoC 内部置一个永久位。这将使你的树莓派以往的超频情况变得可检测。当将 `force_turbo` 置为 `1` 且任一 `over_voltage_*` 参数置为大于 `0` 的值时，就会应用超频位设置。详细信息请查看有关[超频模式的博客文章](https://www.raspberrypi.com/news/introducing-turbo-mode-up-to-50-more-performance-for-free/)。

### 超频

| 参数 | 说明                                  |
| :------: | ---------------------------------------------------------------------------- |
| `arm_freq`     | ARM CPU 的频率（MHz）。                                                                                                                                                                                                                                                                                                                                      |
| `arm_boost`     | 将 `arm_freq` 提升到主板和固件所支持的最高主频。置为 1 启用。                                                                                                                                                                                                                                                                                                        |
| `gpu_freq`     | 与 `core_freq`、`h264_freq`、`isp_freq`、`v3d_freq` 和 `hevc_freq` 一同设置。                                                                                                                                                                                                                                                                                            |
| `core_freq`     | GPU 处理器主频（MHz）。将影响 CPU 性能，因为它驱动着 L2 缓存和内存总线；只有树莓派 Zero、Zero W，树莓派 1 能从 L2 缓存中受益；对树莓派 2、3 上的内存（SDRAM）来说，有好处但不大。请参见下文关于在树莓派 4 上如何使用的章节。                                                                                                                                     |
| `h264_freq`     | 硬件视频模块的频率（MHz）；对个别 `gpu_freq` 设置的覆盖。                                                                                                                                                                                                                                                                                                         |
| `isp_freq`     | 图像传感器管道模块的频率（MHz）；对个别 `gpu_freq` 设置的覆盖。                                                                                                                                                                                                                                                                                                   |
| `v3d_freq`     | 3D 模块的频率（MHz）；对个别 `gpu_freq` 设置的覆盖。在树莓派 5 上，V3D 独立于 `core_freq`、`isp_freq` 和 `hevc_freq`。                                                                                                                                                                                                                                            |
| `hevc_freq`     | 高效视频编解码器模块的频率（MHz）；对个别 `gpu_freq` 设置的覆盖。仅适用于树莓派 4。                                                                                                                                                                                                                                                                            |
| `sdram_freq`     | 内存（SDRAM）的频率（MHz）。在树莓派 4 及后续新款设备上无法对内存（SDRAM）超频。                                                                                                                                                                                                                                                                                           |
| `over_voltage`     | CPU/GPU 核心的电压上限。数值应位于区间 \[-16,8\]，这相当于区间 \[0.95V,1.55V\]（树莓派 1 为 \[0.8V,1.4V\]），步长为 0.025V。换言之，设定 -16 将把 CPU/GPU 核心电压的最大值变成为 0.95V（树莓派 1 为 0.8V）；设定为 8 将高达 1.55V（树莓派 1 为 1.4V）。有关默认值，请参见下表。仅当指定 `force_turbo=1` 时，才能允许高于 6 的值：如果同时设定 `over_voltage_*` 大于 `0`，则会设置保修位。|
| `over_voltage_sdram`     | 与 `over_voltage_sdram_c`，`over_voltage_sdram_i` 和 `over_voltage_sdram_p` 一同设置。                                                                                                                                                                                                                                                                                     |
| `over_voltage_sdram_c`     | 调整内存（SDRAM）控制器电压。\[-16,8\] 等同于 \[0.8V,1.4V\]，步长为 0.025V。不支持树莓派 4 及后续新款设备。                                                                                                                                                                                                                                                                       |
| `over_voltage_sdram_i`     | 调整内存（SDRAM）I/O 电压。\[-16,8\] 等同于 \[0.8V,1.4V\]，步长为 0.025V。不支持树莓派 4 及更新款设备。                                                                                                                                                                                                                                                                      |
| `over_voltage_sdram_p`     | 调整内存（SDRAM）物理电压。\[-16,8\] 等同于 \[0.8V,1.4V\]，步长为 0.025V。不支持树莓派 4 及更新款设备。                                                                                                                                                                    |
| `force_turbo`     | 强制进入超频模式频率，无论 ARM 核心是否空闲。如同时设定 `over_voltage_*`，启用该选项可能导致设置保修位。                                                                                                                                                                                                                                                             |
| `initial_turbo`     | 启用[启动加速模式](https://forums.raspberrypi.com/viewtopic.php?f=29&t=6201&start=425&_gl=1*xfo3n1*_ga*ODAwMTM3MTg4LjE3MTc1NzY1NTQ.*_ga_22FD70LWDS*MTcyMjQ2MzY2My43NS4xLjE3MjI0NjM2NjguMC4wLjA.#p180099)，持续给定的秒数，或直至设置 cpufreq 频率。最大值为 `60`。                                                                                                                                                                                                                                                                                          |
| `arm_freq_min`     |  动态频率时钟 `arm_freq` 的最小值。请注意，将该值降低至低于默认值的数值并不会触发任何实质上的节能，且当前并不支持。                                                                                                                                                                                                                                                     |
| `core_freq_min`     | 动态频率时钟 `core_freq` 的最小值。                                                                                                                                                                                                                                                                                                                              |
| `gpu_freq_min`     | 动态频率调节 `gpu_freq` 的最小值。                                                                                                                                                                                                                                                                                                                                 |
| `h264_freq_min`     | 动态频率调节 `h264_freq` 的最小值。                                                                                                                                                                                                                                                                                                                                |
| `isp_freq_min`     | 动态频率调节 `isp_freq` 的最小值。                                                                                                                                                                                                                                                                                                                                 |
| `v3d_freq_min`     | 动态频率时钟 `v3d_freq` 的最小值。                                                                                                                                                                                                                                                                                                                                 |
| `hevc_freq_min`     | 动态频率时钟 `hevc_freq` 的最小值。                                                                                                                                                                                                                                                                                                                                |
| `sdram_freq_min`     | 动态频率时钟 `sdram_freq` 的最小值。                                                                                                                                                                                                                                                                                                                               |
| `over_voltage_min`     | 动态频率时钟 `over_voltage` 的最小值。该值应位于区间 \[-16,8\] 内，等同于 \[0.8V,1.4V\]，步进为 0.025V。换言之，指定 -16 将使 CPU/GPU 核心空闲电压变为 0.8V；设定为 8 将把最低电压变为 1.4V。在树莓派 4、5 上，该参数已弃用。                                                                                                                                         |
| `over_voltage_delta`     | 在树莓派 4、5 上，参数 `over_voltage_delta` 会将给定的偏移量（µV）添加到 DVFS 算法计算的数值中。                                                                                                                                                                                                                                                        |
| `temp_limit`     | 过热保护。当 SoC 达到设定值（°C）时，会将时钟和电压设置为默认值。超过 85 的值仍为 85。                                                                                                                                                                                                                                                                          |
| `temp_soft_limit`     | **仅适用于 3A+、3B+。**  CPU 速度节流控制。它设定了启动 CPU 时钟速度节流系统的温度。在此温度下，时钟速度将从 1400MHz 降至 1200MHz。默认值为 `60`，最大可升至 `70`，但可能会大不稳定。                                                                                                                                                                                    |

下表提供了各种树莓派型号参数的默认值，所有频率均以 MHz 表示。

| 参数 | 树莓派 Zero、Zero W | 树莓派 1 | 树莓派 2 | 树莓派 3 | 树莓派 3A+、3B+ | CM4 和树莓派 4B ⇐ R1.3 | 树莓派 4B R1.4                   | 树莓派 400 | 树莓派 Zero 2 W | 树莓派 5   |
| ------ | ------------ | ---------- | ---------- | ---------- | ----------------------- | -------------------------- | ---------------------------------- | ------------ | ----------------- | -------- |
| `arm_freq`     | 1000       | 700      | 900      | 1200     | 1400                  | 1500                     | 1500、1800（如 `arm_boost = 1`） | 1800       | 1000            | 2400   |
| `core_freq`     | 400        | 250      | 250      | 400      | 400                   | 500                      | 500                              | 500        | 400             | 910    |
| `h264_freq`     | 300        | 250      | 250      | 400      | 400                   | 500                      | 500                              | 500        | 300             | 不适用 |
| `isp_freq`     | 300        | 250      | 250      | 400      | 400                   | 500                      | 500                              | 500        | 300             | 910    |
| `v3d_freq`     | 300        | 250      | 250      | 400      | 400                   | 500                      | 500                              | 500        | 300             | 910    |
| `hevc_freq`     | 不适用         | 不适用       | 不适用       | 不适用       | 不适用                   | 500                      | 500                              | 500        | 不适用              | 910    |
| `sdram_freq`     | 450        | 400      | 450      | 450      | 500                   | 3200                     | 3200                             | 3200       | 450             | 4267   |
| `arm_freq_min`     | 700        | 700      | 600      | 600      | 600                   | 600                      | 600                              | 600        | 600             | 1500   |
| `core_freq_min`     | 250        | 250      | 250      | 250      | 250                   | 200                      | 200                              | 200        | 250             | 500    |
| `gpu_freq_min`     | 250        | 250      | 250      | 250      | 250                   | 250                      | 250                              | 250        | 250             | 500    |
| `h264_freq_min`     | 250        | 250      | 250      | 250      | 250                   | 250                      | 250                              | 250        | 250             | 不适用 |
| `isp_freq_min`     | 250        | 250      | 250      | 250      | 250                   | 250                      | 250                              | 250        | 250             | 500    |
| `v3d_freq_min`     | 250        | 250      | 250      | 250      | 250                   | 250                      | 250                              | 250        | 250             | 500    |
| `sdram_freq_min`     | 400        | 400      | 400      | 400      | 400                   | 3200                     | 3200                             | 3200       | 400             | 4267   |

下表提供了所有通用参数默认值。

| 参数 | 默认值                           |
| ------ | -------------------------------- |
| `initial_turbo`     | 0（秒）                        |
| `temp_limit`     | 85（°C）                      |
| `over_voltage`     | 0（1.35V、树莓派 1 为 1.2V） |
| `over_voltage_min`     | 0（1.2V）                      |
| `over_voltage_sdram`     | 0（1.2V）                      |
| `over_voltage_sdram_c`     | 0 (1.2 V)                   |
| `over_voltage_sdram_i`     | 0 (1.2 V)                   |
| `over_voltage_sdram_p`     | 0 (1.2 V)                   |

固件使用自适应电压调节（AVS）来确定最佳的 CPU/GPU 核心电压（由 `over_voltage` 和 `over_voltage_min` 定义的区间内）。

#### 适用于树莓派 4、400 和 CM4

当系统处于空闲状态时，最低主频必须保持在一定的速度，以支持显示器的最高像素时钟（忽略 blanking）。因此，如果显示模式为 4Kp60，则将把 `core_freq` 提升到 500 MHz 以上。

| 显示参数 |  `core_freq` 最大值 |
| ---------- | ---------------- |
| 默认值     | 500            |
| `hdmi_enable_4kp60`         | 550            |

>**注意**
>
>无需使用 `hdmi_enable_4kp60`，树莓派 5 默认即支持双 4Kp60 显示屏。

* 超频需要最新版本的固件。
* 最新的固件在系统超频时会自动提高电压。手动设定 `over_voltage` 会禁用超频时的自动电压调节。
* 建议在超频时对单个参数（`isp_freq`、`v3d_freq` 等）的频率进行设定。不建议设定 `gpu_freq`，因为 ISP、V3D、HEVC 等的最大稳定频率不同。
* 树莓派 4 及更新款设备上的内存（SDRAM）频率不可设定。

#### `force_turbo`

在默认情况下（`force_turbo=0`），按需的 CPU 频率驱动程序会在 ARM 核心繁忙时把时钟提升到最大频率，并在 ARM 核心空闲时将其降至最低频率。

`force_turbo=1` 可覆盖上述行为，即使 ARM 核心负载并不大，也会强制使用最大频率。

### 时钟关系

#### 树莓派 4

GPU 核心、CPU、内存（SDRAM）和 GPU 各自拥有自己的锁相环（PLL），且频率可互相独立。h264、v3d 和 ISP 模块则使用相同的锁相环（PLL）。

要查看树莓派当前的频率（KHz），请输入： `cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_cur_freq`。将结果除以 1000 可获得以 MHz 为单位的值。请注意，此频率是内核请求的频率，若在有限制的情况下（如高温）CPU 的实际运行速度可能比报告的要慢。使用 `vcgencmd`——`vcgencmd measure_clock arm` 可获取 ARM CPU 实际频率的瞬时测量值 。该频率以赫兹为单位显示。

### 监控核心温度

##### 白皮书

>[树莓派设备散热](https://pip.raspberrypi.com/categories/685-whitepapers-app-notes/documents/RP-003608-WP/Cooling-a-Raspberry-Pi-device.pdf)
>
>本白皮书详细介绍了你的树莓派会发热的可能性原因，以及为何你可能想要对其进行降温，并提供了有关冷却过程的参数。

要查看树莓派的温度，请运行以下命令：

```
$ cat /sys/class/thermal/thermal_zone0/temp
```

通过将结果除以 1000 可获得摄氏度的值。或者，你可以使用 `vcgencmd measure_temp` 报告的 GPU 温度。

达到温度极限不会对 SoC 造成伤害，只会导致 CPU 降频。散热器可以帮助控制核心温度，从而提高性能。如果给树莓派安装了外壳，则极为有用。散热器上的空气流动会使冷却效果更好。

当核心温度位于 80°C 和 85°C 之间时 ARM 核心将被限速。若温度超过 85°C，ARM 核心、GPU 均将被限速。

对于树莓派 3B+ 来说，其印刷电路板（PCB）技术有所改良，提供了更好的散热和热量上限。此外，还引入了软温度限制，旨在最大限度地延长设备在达到 85°C 硬限制之前的“冲刺”时间。当达到软限制时，时钟速度会从 1.4GHz 降至 1.2GHz，并略微降低操作电压。这减少了温度的上升速度：我们用更长时间的 1.2GHz，取代了短时间的 1.4GHz。在默认情况下，软限制为 60°C。可通过 `config.txt` 设置中的 `temp_soft_limit` 更改此设置。

### 监控电压

维持供电电压大于 4.8V 才能确保可靠性能。请注意，某些 USB 充电器（电源）电压可能会降至 4.2V。这是因为它们通常设计用于为 3.7V 的锂聚合物电池充电，而非为计算机提供 5V 电源供应。

要监测树莓派的电源供电电压，你需要用万用表测量 GPIO 引脚的 VCC 和 GND。有关更多信息，请查看文档的[电源](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#power-supply)部分。

如电压降至 4.63V 以下（±5％），ARM 核心、GPU 将降频，并将在内核日志中打印标识低电压状态的信息。

树莓派 5 的电源管理芯片（PMIC）搭载了内置模数转换器（ADC），可测量供电电压。要查看当前的供电电压，请运行以下命令：

```
$ vcgencmd pmic_read_adc EXT5V_V
```

### 超频问题

大多数超频问题会实时反应为启动失败。如果发生了这种情况，请在下次启动时按住 **shift** 键。将临时禁用所有超频，你即可成功启动，然后再修改你的设置。

## 条件筛选器

当单张 SD 卡（SD 卡镜像）与一块树莓派和一台显示器搭配使用时，很轻松地，就能根据所需的特定组合设置 `config.txt`。可维持这种方式，仅在发生变化时才进行修改。

但是，如果一块树莓派在不同显示器之间交换使用，或一张 SD 卡（SD 卡镜像）在多块开发板间交换使用，那么单套设置可能就不大够用了。条件筛选器能让你定义配置文件的某些部分仅适用于特定情况，从而让不同硬件在读取相同的 `config.txt` 时能创建不同的配置。

### 筛选器 `[all]` 

筛选器 `[all]` 是最基本的筛选器。它会重置所有先前设置的筛选器，并能将任意下表列出设置应用于所有硬件。通常，最好在筛选设置组的末尾添加筛选器`[all]` ，以避免意外组合筛选器（另见下文）。

### 筛选器

条件筛选器的适用性如下表所示。

| 筛选器 | 适用型号                                                                 |
| -------- | -------------------------------------------------------------------------- |
| `[pi1]`       | 1A、1B、1A+、1B+，计算模块 1                           |
| `[pi2]`       | 2B（基于 BCM2836、BCM2837）                                       |
| `[pi3]`       | 3B、3B+、3A+，计算模块 3、3+      |
| `[pi3+]`       | 3A+、3B+（同时引用 `[pi3]` 的内容）                            |
| `[pi4]`       | 4B、400，计算模块 4、4S                    |
| `[pi5]`       | 树莓派 5                                                                 |
| `[pi400]`       | Pi 400（同时引用 `[pi4]` 内容）                                              |
| `[cm4]`       |计算模块 4（同时引用 `[pi4]` 内容）                                          |
| `[cm4s]`       |计算模块 4S（同时引用 `[pi4]` 内容）                                         |
| `[pi0]`       | Zero、Zero W、Zero 2 W                                                   |
| `[pi0w]`       | Zero W（同时引用 `[pi0]` 内容）                                              |
| `[pi02]`       | Zero 2W（同时引用 `[pi0w]`、`[pi0]` 的内容）                               |
| `[board-type=Type]`       | 按 `Type` 值筛选——参见[树莓派修订代码](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#raspberry-pi-revision-codes)。如 `[board-type=0x14]` 将匹配 CM4。|

对于设置不同的 `kernel`、`initramfs` 和 `cmdline` 设置极为有用，因为树莓派 1、2 所需内核不同。它们还有助于定义不同的超频设置，因为树莓派 1、2 默认的主频各异。比如，为每块树莓派设置不同的 `initramfs` 映像：

```
[pi1]
initramfs initrd.img-3.18.7+ followkernel
[pi2]
initramfs initrd.img-3.18.7-v7+ followkernel
[all]
```

记得在最后使用筛选器 `[all]` ， 这样后续设置就不会仅限于树莓派 2 硬件。

>**注意**
>
>某些型号的树莓派（Zero W、Zero 2 W，树莓派 3B+、400，计算模块 4、4S）会引用多个筛选器的设置（如上表所述）。这意味着如果你想让某个设置仅用于（例如）4B，且不把该设置应用于树莓派 400，那么 `[pi4]` 部分中的设置需要在随后的 `[pi400]` 部分中通过替代设置来还原——此部分的顺序很重要。或者，你可以使用筛选器 `[board-type=0x11]`，这个筛选器与不同的硬件产品之间有一对一的映射关系。

### 筛选器 `[none]` 

该 [none] 筛选器阻止任何随后的设置应用于任何硬件。尽管没有什么是你不能没有 [none] 做的，但它可以是一个有用的方法，可以在不必注释掉每一行的情况下，在 config.txt 中保留未使用设置的组。

### 筛选器 `[tryboot]` 

如果为 reboot 设置了参数 `tryboot`，则此筛选器为真。

筛选器 `[tryboot]` 的用于 `autoboot.txt`，以便在 `tryboot` 模式下选择不同的引导分区，进行操作系统的安全失败（fail-safe）式更新。

### 筛选器 `[EDID=*]`

在树莓派上使用单张 SD 卡切换多台显示器时，并且空白配置不足以自动选择每台显示器所需的分辨率时，可根据显示器的 EDID 名称选择特定设置。

要查看已连接显示器的 EDID 名称，你需按照以下步骤操作。运行以下命令，查看你的树莓派上有哪些输出设备：

```
$ ls -1 /sys/class/drm/card?-HDMI-A-?/edid
```

在树莓派 4 上，打印类似如下输出：

```
/sys/class/drm/card1-HDMI-A-1/edid
/sys/class/drm/card1-HDMI-A-2/edid
```

然后，你需要以每个这些文件名运行 `edid-decode`，比如：

```
$ edid-decode /sys/class/drm/card1-HDMI-A-1/edid
```

如果没有显示器连接为输出设备，它将告诉你 EDID 为空；若已连接显示器，将为你提供有关显示器功能的丰富信息。你需查找`Manufacturer`、`Display Product Name` 所在行。然后，“EDID 名称”为 `<Manufacturer>-<Display Product Name>`，并将字符串中的所有空格都将换成下划线。比如，如果你的 `edid-decode` 输出为：

```
....
  Vendor & Product Identification:
    Manufacturer: DEL
....
    Display Product Name: 'DELL U2422H'
....
```

此显示器的 EDID 名称将是 `DEL-DELL_U2422H`。

然后，你可以将其用作条件筛选器，指定仅在连接此特定显示器时才适用的设置：

```
[EDID=DEL-DELL_U2422H]
cmdline=cmdline_U2422H.txt
[all]
```

这些设置仅适用于启动时。必须在启动前接入显示器，=且树莓派必须能够读取其 EDID 信息以找到正确的名称。在启动后，若热插拔不同的显示器，在树莓派上也不会选择其他设定。

在树莓派 4 上，如果同时使用了两个 HDMI 端口，则 EDID 筛选器将与两者进行匹配，并将应用所有匹配条件筛选器的配置。

>**注意**
>
>在树莓派 5 上未提供此设置。

### 串号筛选器

有时候需将设置设定为仅适用于单块特定的树莓派——即使你将 SD 卡更换为另一张也如此。下面的示例涉及了许可证密钥和超频设置（虽然许可证密钥可以其他方式支持不同的 SD 卡交换）。你还可以使用此功能来设定不同的显示设置（即使无法识别上述 EDID），只要你不在树莓派之间切换显示器就行。例如，如果你的显示器没有提供能用的 EDID 名称（或你正在使用复合输出（亦无法读取 EDID））。

要查看你树莓派的串号，请运行以下命令：

```
$ cat /proc/cpuinfo
```

尾部输出将打印一个 16 位十六进制值。你树莓派的串号是最后八位数字（十六进制）。比如，若你看到：

```
Serial          : 0000000012345678
```

则串号为 12345678。

>**注意**
>
>在某些树莓派型号上，前 8 位数字（十六进制）会包含 `0` 以外的数值。即使在这种情况下，也只使用最后八位数字（十六进制）作为串号。

你可以定义仅用于特定树莓派的设置：

```
[0x12345678]
# 此处设置仅适用于符合该序列号的树莓派

[all]
# 此处设置用于所有硬件
```

### GPIO 筛选器

你还可以根据 GPIO 的状态进行筛选。例如：

```
[gpio4=1]
# 此处设置在 GPIO 4 为高电平时生效

[gpio2=0]
# 此处设置在 GPIO 2 为低电平时生效

[all]
# 此处设置用于所有硬件
```

### 组合条件筛选器

相同类型的筛选器会互相取代，因此 `[pi2]` 会覆盖 `[pi1]`，因为两者不可能同时为真。

不同类型的筛选器可通过逐个列出筛选器来进行组合，例如:

```
# 此处设置用于所有硬件

[EDID=VSC-TD2220]
# 这些设置仅在接入 VSC-TD2220 显示器时生效

[pi2]
# 这些设置仅在树莓派 2 上接入了 VSC-TD2220 显示器时生效

[all]
# 此处设置用于所有硬件
```

使用筛选器 `[all]` 可重置先前所有筛选器，避免意外地组合不同类型的筛选器。

## 内存选项

### `total_mem`

此参数可用于强制限制树莓派的内存容量：指定你想要让树莓派使用的总内存量（MB）。如，要让 4GB 的树莓派 4B 表现为 1GB 款，请使用以下内容：

```
total_mem=1024
```

此值最小值为 128MB，最大值为主板搭载的总内存量。

## 许可证密钥和编解码器参数

可通过购买许可证来激活硬件编解码器解码：树莓派 3 及其早期型号上的附带了编解码器。该许可证与你树莓派的 CPU 序列号绑定。

树莓派 4 已永久禁用了硬件解码器 MPEG2 和 VC1。无法启用这些编解码器，因此也无需硬件编解码器许可证密钥。对于典型用例，MPEG2 和 VC1 文件的软解码性能已足矣。

树莓派 5 搭载了 H.265（HEVC）硬件解码。该解码默认已启用，因此无需硬件解码许可密钥。

### `decode_MPG2`

`decode_MPG2` 是用于激活 MPEG-2 硬件解码的许可密钥，例如 `decode_MPG2=0x12345678`。

### `decode_WVC1`

`decode_WVC1` 是用于激活 VC-1 硬件解码的许可密钥，例如 `decode_WVC1=0x12345678`。

如果你有多块树莓派，并为每块树莓派都购买了编解码器许可证，你可以在一个 `config.txt` 中最多写入八个许可证密钥——如 `decode_MPG2=0x12345678,0xabcdabcd,0x87654321`。这让你可以在不必每次都编辑 `config.txt`，就能在不同的树莓派间交换同一张 SD 卡。

## 视频参数

### HDMI 分辨率

要控制 HDMI 设置，请使用`cmdline.txt` 中的 [屏幕配置实用程序](https://www.raspberrypi.com/documentation/computers/configuration.html#set-resolution-and-rotation)、[KMS 视频设置](https://www.raspberrypi.com/documentation/computers/configuration.html#set-the-kms-display-mode)。

#### 用于树莓派 4 的 HDMI 管道

为了支持双显示器和最高 4Kp60 的分辨率，树莓派 4 每个时钟周期会产生 2 个输出像素。

以每时钟 2 像素的速度运行一切意味着树莓派 4 无法支持不能被 2 整除的水平时序。

在 CEA 和 DMT 标准中仅有一种不兼容的分辨率：DMT mode 81, 1366x768 @ 60Hz。该模式的水平同步和后沿时序值为奇数，宽度无法被 8 整除。

如果你的显示器带有这种分辨率，树莓派 4 会自动降到下一个显示器的标称模式，通常为 1280x720。

#### 树莓派 5 的 HDMI 管道

虽然树莓派 5 亦可在每个时钟周期输出 2 个像素，但它对奇异时序有特殊处理，可以直接处理这些分辨率。

### 复合视频模式

每款树莓派计算机上都能找到复合视频输出。

| 型号          | 复合输出              |
| ----------------- | ----------------------- |
| 树莓派 1A、1B | RCA 插孔              |
| 树莓派 Zero     | 未焊接的 `TV` 接头      |
| 树莓派 Zero 2 W | 主板底部的测试点      |
| 树莓派 5        | HDMI 插口旁的 J7 触点 |
| 其他型号    | 3.5 mm AV 插孔      |

>**注意**
>
>树莓派 400 未提供复合视频输出。

#### `enable_tvout`

置为 `1` 将启用复合视频输出，置为 `0` 将禁用复合视频输出。在树莓派 4、5 上，仅当你将其置为 `1` 时，才可使用复合输出（同时亦会禁用 HDMI 输出）。树莓派 400 不支持复合输出。

| 型号       | 默认值 |
| ---------------- | ------ |
| 树莓派 4, 5、400 | 0    |
| 其他   | 1    |

除了树莓派 4、5 以外，均须禁用 HDMI 输出才能启用复合输出。当未连接（或未检测到）HDMI 显示器时，将禁用 HDMI 输出。设置 `enable_tvout=0` 可阻止在 HDMI 禁用时启用复合输出。

要启用复合输出，请在 `/boot/firmware/config.txt` 的 `dtoverlay=vc4-kms-v3d` 这行末尾添加 `,composite` ：

```
dtoverlay=vc4-kms-v3d,composite
```

在默认情况下，会输出复合视频（NTSC）。要选择其他模式，请将以下内容添加到 `/boot/firmware/cmdline.txt` 中这一行：

```
vc4.tv_norm=<视频模式>
```

请用以下值替换占位符 `<视频模式>`：

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

在默认情况下，会在 I²C 总线上检测树莓派触摸显示屏。`ignore_lcd=1` 可跳过此检测阶段，以禁用 LCD 显示屏。

#### `disable_touchscreen`

启用和禁用触摸屏。

`disable_touchscreen=1` 可禁用树莓派官方触摸显示屏的触摸屏组件。

### 通用显示参数

#### `disable_fw_kms_setup`

在默认情况下，固件会解析所有接入 HDMI 显示器的 EDID，并选择适当的显示模式，然后通过内核命令行上的设置将显示的分辨率和帧率（以及过扫描参数）传给 Linux 内核。在极少数情况下，固件可能会选择 EDID 中不存在的模式，可能并不兼容该设备。使用 `disable_fw_kms_setup=1` 可以禁用传递的视频模式参数，从而避免此问题。Linux 视频模式系统（KMS）会自己解析 EDID 并选择适当的模式。

>**注意**
>
>在树莓派 5 上，此参数默认为 `1`。

## 相机设置

### `disable_camera_led`

将 `disable_camera_led` 置为 `1` 可在录制视频、拍摄照片时关闭摄像机的红色 LED 指示灯。这对于防止反光（如摄像机正对着窗户时）极其有用。

### `awb_auto_is_greyworld`

将 `awb_auto_is_greyworld` 置为 `1`，可让自身不支持灰色世界选项的库、应用程序使用夜视（NoIR）摄像头捕捉有效的图像、视频。它将自动 awb 模式切换使用灰色世界算法。仅适用于无红外摄像机、[已移除红外滤光片](https://www.raspberrypi.com/documentation/accessories/camera.html#filter-removal)的高质量（HQ）摄像机。
