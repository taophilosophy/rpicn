# Linux 内核

## 简介

树莓派内核托管在 [GitHub](https://github.com/raspberrypi/linux) 上，其更新滞后于上游的 [Linux 内核](https://github.com/torvalds/linux)。上游内核在持续更新，而树莓派把 Linux 内核的 **长期维护版本**（long-term releases）集成到树莓派内核中。我们会为每个长期维护的 Linux 内核版本在 [raspberrypi/firmware](https://github.com/raspberrypi/firmware/) 中生成一个 `next` 分支。经过充分的测试和讨论，我们会把每个 `next` 分支合并到仓库的主分支中。

## 更新

日常的树莓派系统[更新流程](raspberry-pi-os.md#更新当前的树莓派软件)会自动把你的内核更新到最新稳定版本。如果你想试用最新的不稳定测试内核，可以[手动更新](raspberry-pi-os.md#更新预发布固件)。

## 编译内核

操作系统随附的默认编译器和链接器都配置为编译在该操作系统上运行的可执行文件。**本地编译（Native builds）** 使用这些默认的编译器和链接器。**交叉编译（Cross-compilation）** 是指为运行构建过程的主机之外的目标编译代码的过程。

对树莓派内核进行交叉编译，可以让你在 32 位操作系统上编译 64 位内核，反之亦然。你也可以在非树莓派设备上交叉编译 32 位或 64 位的树莓派内核。

以下说明分为本地编译和交叉编译两部分，请选择适合你情况的那部分。两种流程虽然有许多相同步骤，但也存在一些重要差异。

>**注意**
>
>在树莓派系统上，固件会直接从启动分区加载内核镜像（`$KERNEL.img`）。Ubuntu 等其他发行版安装和选择内核的方式不同。如果你的树莓派运行的是其他发行版，请按照该发行版的文档安装自定义内核。

### 下载内核源码

在为任何目标编译之前，你需要内核源代码。要获取内核源代码，你需要 Git。如果你尚未安装 Git，请先在设备上安装它：

```bash
$ sudo apt install git
```

接下来，下载最新树莓派内核的源代码：

```bash
$ git clone --depth=1 https://github.com/raspberrypi/linux
```

这可能需要几分钟。

>**技巧**
>
>上面的 `git clone` 命令会下载当前活跃分支，且不带任何历史记录，我们正是用这个分支构建树莓派系统镜像。如果要下载包含所有分支全部历史的完整仓库，请省略 `--depth=1`。这样会花费更长时间，占用更多存储空间。
>
>如果要下载其他分支且不带历史记录，可在上述命令中添加 `--branch` 参数，并把 `<branch>` 换成你想下载的分支名：
>
>```bash
>$ git clone --depth=1 --branch <branch> https://github.com/raspberrypi/linux
>```
>
>要查看所有可用分支的完整列表，请参见[树莓派内核存储库](https://github.com/raspberrypi/linux)。

现在你已经有了内核源码，可以用[本地编译](#本地编译内核)或[交叉编译](#交叉编译内核)的方式编译一个新内核。

### 本地编译内核

本指南假设你的树莓派运行的是最新版本的[树莓派系统](raspberry-pi-os.md)。

先安装编译所需的依赖包：

```bash
$ sudo apt install bc bison flex libssl-dev make
```

#### 编译配置

本节介绍如何在编译内核时应用默认配置。你也可以通过以下方式配置内核：

* [启用或禁用内核功能](#配置内核)
* [应用其他来源的补丁](#打补丁)

要准备默认配置，请根据你的架构和树莓派型号，执行下表中的对应命令。

| 架构 | 型号 | 命令 |
| :--- | :--- | :--- |
| 64 位 | 树莓派 3、3+、计算模块 3、计算模块 3+、Zero 2 W、4、400、计算模块 4、计算模块 4S、5、500、500+、计算模块 5 | `$ cd linux`<br />`$ KERNEL=kernel8`<br />`$ make bcm2711_defconfig` |
| 64 位（优化） | 树莓派 5、500、500+、计算模块 5 | `$ cd linux`<br />`$ KERNEL=kernel_2712`<br />`$ make bcm2712_defconfig` |
| 32 位 | 树莓派 1、计算模块 1、Zero、Zero W | `$ cd linux`<br />`$ KERNEL=kernel`<br />`$ make bcmrpi_defconfig` |
| 32 位 | 树莓派 2、3、3+、计算模块 3、计算模块 3+、Zero 2 W | `$ cd linux`<br />`$ KERNEL=kernel7`<br />`$ make bcm2709_defconfig` |
| 32 位 | 树莓派 4、400、计算模块 4、计算模块 4S（6.18 之前的内核） | `$ cd linux`<br />`$ KERNEL=kernel7l`<br />`$ make bcm2711_defconfig` |

>**注意**
>
>`bcm2712_defconfig` 编译出的 `kernel_2712.img` 针对 BCM2712 设备（Raspberry Pi 5、500、500+、计算模块 5）做了优化，使用 16K 页大小。`bcm2711_defconfig` 编译出的 `kernel8.img` 也能在这些设备上运行，但使用 4K 页大小。在 BCM2712 设备上，如果存在 `kernel_2712.img`，固件会加载它，否则回退到 `kernel8.img`。

>**注意**
>
>在 BCM2711 设备上，32 位版树莓派系统使用 32 位用户空间，但运行的是 **64 位内核**。自内核 6.18 起，BCM2711 设备（Raspberry Pi 4、400、计算模块 4、计算模块 4S）不再支持编译 32 位内核，请改用 64 位的 `kernel8`。对于更早的内核版本，请设置 `ARCH=arm` 编译 32 位内核，并在 `config.txt` 中设置 `arm_64bit=0` 来启动它。

#### 使用 `LOCALVERSION` 自定义内核版本

为了防止内核覆盖 `/lib/modules` 中的现有模块，也为了在 `uname` 输出中看出你运行的是自定义内核，请调整 `LOCALVERSION`。

要调整 `LOCALVERSION`，请修改 `.config` 文件中的这一行：

```ini
CONFIG_LOCALVERSION="-v8-MY_CUSTOM_KERNEL"
```

每种默认配置都会设置自己的 `LOCALVERSION` 后缀，例如 `bcm2711_defconfig`（64 位）为 `-v8`，`bcm2712_defconfig` 为 `-v8-16k`，`bcm2709_defconfig` 为 `-v7`。请保留该后缀，再在后面追加你自己的文字，如上例所示。

>**技巧**
>
>你还可以在图形界面的 `menuconfig` 中更改此设置，路径为 **General setup** \> **Local version - append to kernel release**。有关 `menuconfig` 的更多信息，请参阅[内核配置说明](#配置内核)。

#### 编译

接下来，编译内核。根据你的树莓派型号，此步骤可能需要很长时间。

* 运行以下命令可编译 64 位内核：

  ```bash
  $ make -j6 Image.gz modules dtbs
  ```
* 运行以下命令可编译 32 位内核：

  ```bash
  $ make -j6 zImage modules dtbs
  ```

>**技巧**
>
>在多核树莓派型号上，`make -j<n>` 参数会把工作分配到多个核心，可显著加快编译速度。运行 `nproc` 可以查看你有多少处理器；我们建议传入处理器数量 1.5 倍的数值。

#### 安装内核

接下来，将内核模块安装到启动介质上：

```bash
$ sudo make -j6 modules_install
```

然后，将内核和设备树二进制文件安装到启动分区中，并备份原有内核。

>**重要**
>
>在 BCM2712 设备（Raspberry Pi 5、500、500+、计算模块 5）上，固件会优先加载 `kernel_2712.img`（如果存在），而不是 `kernel8.img`。
>
>树莓派系统默认包含 `kernel_2712.img`。如果你为这类设备编译的是 `KERNEL=kernel8`，必须把下面这行加入 `config.txt`：
>
>```ini
>kernel=kernel8.img
>```

>**技巧**
>
>如果你不想将新编译的内核安装到运行此命令的树莓派上，请把编译好的内核复制到另一块启动介质的启动分区中，而不是 `/boot/firmware/`。

要安装 64 位内核：

* 运行以下命令，备份当前内核，并安装新的内核镜像、设备树二进制文件、叠加层和 README：

  ```bash
  $ sudo cp /boot/firmware/$KERNEL.img /boot/firmware/$KERNEL-backup.img
  $ sudo cp arch/arm64/boot/Image.gz /boot/firmware/$KERNEL.img
  $ sudo cp arch/arm64/boot/dts/broadcom/*.dtb /boot/firmware/
  $ sudo cp arch/arm64/boot/dts/overlays/*.dtb* /boot/firmware/overlays/
  $ sudo cp arch/arm64/boot/dts/overlays/README /boot/firmware/overlays/
  ```

要安装 32 位内核：

1. 备份当前内核并安装新的内核镜像：

    ```bash
    $ sudo cp /boot/firmware/$KERNEL.img /boot/firmware/$KERNEL-backup.img
    $ sudo cp arch/arm/boot/zImage /boot/firmware/$KERNEL.img
    ```
2. 根据你的[内核版本](#确认你的内核版本)，运行以下命令：

    * 对于 6.4 版本及以下的内核：

      ```bash
      $ sudo cp arch/arm/boot/dts/*.dtb /boot/firmware/
      ```
    * 对于 6.5 版本及以上的内核：

      ```bash
      $ sudo cp arch/arm/boot/dts/broadcom/*.dtb /boot/firmware/
      ```
3. 最后，复制叠加层和 README：

    ```bash
    $ sudo cp arch/arm/boot/dts/overlays/*.dtb* /boot/firmware/overlays/
    $ sudo cp arch/arm/boot/dts/overlays/README /boot/firmware/overlays/
    ```

最后，运行以下命令重启树莓派，让它运行新编译的内核：

```bash
$ sudo reboot
```

树莓派重启后，[确认你的内核版本](#确认你的内核版本)。

>**技巧**
>
>另一种做法是用不同的文件名（例如 `kernel-myconfig.img`）复制内核，而不是覆盖 `$KERNEL.img`。然后编辑启动分区中的 `config.txt`，选用你的内核：
>
>```ini
>kernel=kernel-myconfig.img
>```
>
>把这种做法与自定义 `LOCALVERSION` 结合使用，可以让你的自定义内核与系统管理的默认内核镜像彼此分开。这样安排后，一旦你的内核无法启动，也能迅速换回默认内核。
>
>树莓派系统 Bookworm 及更高版本默认包含 `initramfs`，通过在 `config.txt` 中使用 `auto_initramfs` 启用。
>
>当 `auto_initramfs` 设为 `1` 时，固件要求 `initramfs` 的文件名与内核文件名对应：把内核文件名的 `kernel` 前缀换成 `initramfs`，并省略文件扩展名。例如，`kernel-myconfig.img` 会去找 `initramfs-myconfig`。
>
>如果没有提供匹配的文件名，你必须用一个不带 `=` 号的显式 `initramfs` 指令来指定 ramdisk，例如：
>
>```ini
>initramfs <filename> followkernel
>```

>**注意**
>
>编译和更新 `initramfs` 被视为高级技巧，只有经验丰富的用户才会采用。树莓派官方并不支持这种做法，因此我们也不提供相关说明。
>
>如果你用自己的内核覆盖了 `$KERNEL.img`，启动分区上现有的 `initramfs` 仍然包含为旧内核版本编译的模块。这些模块很可能与内核不兼容，因而不会被加载。需要 `initramfs` 的自定义内核编译方式不在本指南的讨论范围内。

### 交叉编译内核

首先，你需要一台合适的 Linux 交叉编译主机。我们通常使用 Ubuntu；由于树莓派系统同样基于 Debian，两者的编译命令也很相似。

#### 安装所需的依赖和工具链

要通过交叉编译构建源代码，请在设备上安装所需的依赖包。运行以下命令可安装大多数依赖：

```bash
$ sudo apt install bc bison flex libssl-dev make libc6-dev libncurses5-dev
```

然后，安装与你要编译的内核架构匹配的工具链：

* 要安装用于编译 64 位内核的 64 位工具链，请运行以下命令：

  ```bash
  $ sudo apt install crossbuild-essential-arm64
  ```
* 要安装用于编译 32 位内核的 32 位工具链，请运行以下命令：

  ```bash
  $ sudo apt install crossbuild-essential-armhf
  ```

#### 构建配置

本节介绍如何在构建内核时应用默认配置。你也可以通过以下方式配置内核：

* [启用或禁用内核功能](#配置内核)
* [应用其他来源的补丁](#打补丁)

请根据你的架构和树莓派型号，运行下表中的对应命令来构建内核源代码和设备树文件：

| 目标架构 | 目标型号 | 命令 |
| :--- | :--- | :--- |
| 64 位 | 树莓派 3、3+、计算模块 3、计算模块 3+、Zero 2 W、4、400、计算模块 4、计算模块 4S、5、500、500+、计算模块 5 | `$ cd linux`<br />`$ KERNEL=kernel8`<br />`$ make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- bcm2711_defconfig` |
| 64 位（优化） | 树莓派 5、500、500+、计算模块 5 | `$ cd linux`<br />`$ KERNEL=kernel_2712`<br />`$ make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- bcm2712_defconfig` |
| 32 位 | 树莓派 1、计算模块 1、Zero、Zero W | `$ cd linux`<br />`$ KERNEL=kernel`<br />`$ make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- bcmrpi_defconfig` |
| 32 位 | 树莓派 2、3、3+、计算模块 3、计算模块 3+、Zero 2 W | `$ cd linux`<br />`$ KERNEL=kernel7`<br />`$ make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- bcm2709_defconfig` |
| 32 位 | 树莓派 4、400、计算模块 4、计算模块 4S（6.18 之前的内核） | `$ cd linux`<br />`$ KERNEL=kernel7l`<br />`$ make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- bcm2711_defconfig` |

>**注意**
>
>`bcm2712_defconfig` 编译出的 `kernel_2712.img` 针对 BCM2712 设备（Raspberry Pi 5、500、500+、计算模块 5）做了优化，使用 16K 页大小。用 `bcm2711_defconfig` 编译出的 `kernel8.img` 也能在这些设备上运行，页大小为 4K。如果存在 `kernel_2712.img`，固件会加载它，否则回退到 `kernel8.img`。

>**注意**
>
>自内核 6.18 起，BCM2711 设备（Raspberry Pi 4、400、计算模块 4、计算模块 4S）不再支持编译 32 位内核，请改用 64 位的 `kernel8`。

#### 使用 `LOCALVERSION` 自定义内核版本

为防止内核覆盖现有的 `/lib/modules` 中的模块，且在 `uname` 输出中表明你运行的是自定义内核，可以调整 `LOCALVERSION`。

要调整 `LOCALVERSION`，请修改 `.config` 文件的这一行：

```bash
CONFIG_LOCALVERSION="-v7l-MY_CUSTOM_KERNEL"
```

>**技巧**
>
>你也可以用 `menuconfig` 图形化修改此设置，路径为 **General setup** \> **Local version - append to kernel release**。有关 `menuconfig` 的更多信息，请参阅[内核配置说明](https://www.raspberrypi.com/documentation/computers/linux_kernel.html#configure-the-kernel)。


#### 构建

* 运行以下命令可编译 64 位内核：

  ```bash
  $ make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- Image modules dtbs
  ```
* 运行以下命令可编译 32 位内核：

  ```bash
  $ make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- zImage modules dtbs
  ```

#### 安装内核

内核编译完成后，你需要把内核复制到树莓派的启动介质（一般是存储卡和固态硬盘），然后安装模块。

##### 找到你的启动介质

首先运行 `lsblk`。然后接入启动介质，再次运行 `lsblk`；新出现的设备就是你的启动介质。你将看到类似如下的输出：

```bash
sdb
   sdb1
   sdb2
```

如果 `sdb` 代表你的启动介质，`sdb1` 代表 **启动分区**（`FAT32` 格式），而 `sdb2` 代表（可能为 `ext4` 格式）**根分区**。

先将这些分区分别挂载到 `mnt/boot`、`mnt/root`，并根据实际的启动介质位置来调整分区字母：

```bash
$ mkdir mnt
$ mkdir mnt/boot
$ mkdir mnt/root
$ sudo mount /dev/sdb1 mnt/boot
$ sudo mount /dev/sdb2 mnt/root
```

##### 安装

接下来，把内核模块安装到启动介质上：

* 对于 64 位内核：

  ```bash
  $ sudo env PATH=$PATH make -j12 ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- INSTALL_MOD_PATH=mnt/root modules_install
  ```
* 对于 32 位内核：

  ```bash
  $ sudo env PATH=$PATH make -j12 ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- INSTALL_MOD_PATH=mnt/root modules_install
  ```

>**技巧**
>
>在多核设备上，参数 `make -j<数量>` 会把工作分配到多个核心，从而显著提高编译速度。可运行 `nproc` 查看你有多少处理器，我们建议使用的数字为处理器数量的 1.5 倍。


接下来，把内核和设备树文件安装到启动分区中，并备份下旧内核。

要安装 64 位内核：

* 运行以下命令可创建当前内核的备份镜像，安装新的内核镜像、叠加层文件、README 文件，然后卸载分区：

  ```bash
  $ sudo cp mnt/boot/$KERNEL.img mnt/boot/$KERNEL-backup.img
  $ sudo cp arch/arm64/boot/Image mnt/boot/$KERNEL.img
  $ sudo cp arch/arm64/boot/dts/broadcom/*.dtb mnt/boot/
  $ sudo cp arch/arm64/boot/dts/overlays/*.dtb* mnt/boot/overlays/
  $ sudo cp arch/arm64/boot/dts/overlays/README mnt/boot/overlays/
  $ sudo umount mnt/boot
  $ sudo umount mnt/root
  ```

要安装 32 位内核：

1. 运行以下命令可创建当前内核的备份镜像，然后安装新的内核镜像：

    ```bash
    $ sudo cp mnt/boot/$KERNEL.img mnt/boot/$KERNEL-backup.img
    $ sudo cp arch/arm/boot/zImage mnt/boot/$KERNEL.img
    ```
2. 根据你的[内核版本](https://www.raspberrypi.com/documentation/computers/linux_kernel.html#identify-your-kernel-version)，可运行以下命令安装设备树文件：

    * 对于 6.4 及以下版本的内核：

      ```bash
      $ sudo cp arch/arm/boot/dts/*.dtb mnt/boot/
      ```
    * 对于 6.5 及以上版本的内核：

      ```bash
      $ sudo cp arch/arm/boot/dts/broadcom/*.dtb mnt/boot/
      ```
3. 最后，安装叠加层文件和 README 文件，然后卸载分区：

    ```bash
    $ sudo cp arch/arm/boot/dts/overlays/*.dtb* mnt/boot/overlays/
    $ sudo cp arch/arm/boot/dts/overlays/README mnt/boot/overlays/
    $ sudo umount mnt/boot
    $ sudo umount mnt/root
    ```

最后，把启动介质接入你的树莓派，然后接入电源，运行你刚编译的内核。然后，[确认你的内核版本](#确认你的内核版本)。

>**技巧**
>
>你还以使用不同的文件名（例如 `kernel-myconfig.img`）来复制内核，而非直接覆盖文件 `kernel.img`。然后，编辑启动分区中的 `config.txt` 文件来选择你的内核：
>
>```bash
>kernel=kernel-myconfig.img
>```
>
>把这种方法与自定义 `LOCALVERSION` 结合使用，可将你的自定义内核与系统管理的标准内核镜像分开。在这种安排下，如果你的内核无法启动，你可以快速还原到标准内核。


## 配置内核

Linux 内核具有极高的可配置性。专业用户可能希望修改默认配置来满足他们的需求，如启用新的/实验性的网络协议，或支持新硬件。

配置一般通过 `make menuconfig` 界面进行。你也可以手动修改文件 `.config`，但这可能会更复杂。

### 准备配置

工具 `menuconfig` 需要 `ncurses` 开发头文件才能正确编译。要安装这些头文件，请运行以下命令：

```bash
$ sudo apt install libncurses5-dev
```

接下来，[下载内核源代码](https://www.raspberrypi.com/documentation/computers/linux_kernel.html#download-kernel-source)。特别是，确保你已经安装了[默认的本地配置](https://www.raspberrypi.com/documentation/computers/linux_kernel.html#native-build-configuration)/[默认的交叉编译配置](https://www.raspberrypi.com/documentation/computers/linux_kernel.html#cross-compiled-build-configuration)。

### `menuconfig`

待一切准备就绪，你可以按如下方式编译和运行实用程序 `menuconfig` ：

```bash
$ make menuconfig
```

要交叉编译 64 位内核：

```bash
$ make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- menuconfig
```

要交叉编译 32 位内核：

```bash
$ make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- menuconfig
```

要使用实用程序 `menuconfig` ，使用键盘操作：

* 使用 **方向键** 进行方向切换
* 要进入子菜单（由 `--->` 指示），按 **回车键** 
* 要返回上一级或退出，按两次 **Esc 键** 
* 要切换二进制选项的状态，按 **空格键**
* 要选择多选项的状态，按 **回车键** 打开子菜单，使用 **方向键** 切换子菜单，再按 **回车键** 选择状态
* 要获取参数/菜单的帮助，按 **H 键** 

在简短的编译之后，`menuconfig` 会显示一个带有所有可以配置选项的子菜单列表。参数很多，所以需要花点时间才能读完。请避免在第一次尝试时启用/禁用过多的选项；配置过程相对容易出错，所以从小处开始，以熟悉配置和构建过程。

### 保存更改

完成更改后，按 **Esc 键** 直到出现保存新配置的提示。在默认情况下，会保存到文件 `.config`。你可以通过复制此文件来保存和加载配置。

自定义完成后，你现在可以[构建内核](https://www.raspberrypi.com/documentation/computers/linux_kernel.html#building)了。

## 打补丁

在构建自定义内核时，你可能希望将补丁/补丁集应用到 Linux 内核。

硬件制造商有时会提供补丁集，作为支持新硬件的临时措施，直到补丁被合并到 Linux 内核和树莓派内核中。然而，还有其他目的的补丁集，例如启用完全抢占的内核以用于实时应用。

### 确认你的内核版本

要检查当前运行在设备上的内核版本，运行以下命令：

```bash
$ uname -r
```

在应用补丁之前，始终检查你的内核版本。在内核源代码目录中，运行以下命令以查看内核版本：

```bash
$ head Makefile -n 4
```

你应会看到类似如下的输出：

```bash
# SPDX-License-Identifier: GPL-2.0
VERSION = 6
PATCHLEVEL = 1
SUBLEVEL = 38
```

在这个实例中，源代码是针对 6.1.38 内核的。

### 打补丁

打补丁的方式取决于补丁的分发格式。

开发人员通常将大多数补丁以单个文件的形式分发。使用工具 `patch` 来打上这些补丁。以下命令可下载、解压并将实时内核补丁应用到我们的示例内核版本中：

```bash
$ wget https://www.kernel.org/pub/linux/kernel/projects/rt/6.1/patch-6.1.38-rt13-rc1.patch.gz
$ gunzip patch-6.1.38-rt13-rc1.patch.gz
$ cat patch-6.1.38-rt13-rc1.patch | patch -p1
```

有些开发人员以 **邮箱格式（mailbox format）** 分发补丁，这是一种包含多个补丁文件的文件夹。可使用 Git 来应用这些补丁。

>**注意**
>
>在使用 Git 应用邮箱补丁之前，请为你的本地 Git 安装配置姓名和电子邮件：
>
>```bash
>$ git config --global user.name "your name"
>$ git config --global user.email "your email"
>```

要使用 Git 应用邮箱格式的补丁，请运行以下命令：

```bash
$ git am -3 /path/to/patches/*
```

始终按照补丁分发者提供的说明进行操作。例如，一些补丁集要求在特定提交基础上打补丁。

## 内核头文件

要编译内核模块，你需要 Linux 内核头文件。这些头文件提供了编译与内核接口的代码所需的函数和结构定义。

如果你从 GitHub 克隆了整个内核，头文件已经包含在源代码树中了。如果你不需要其他额外的文件，可以仅使用 `apt` 安装内核头文件。

>**技巧**
>
>当发布新内核时，你需要与该内核版本匹配的头文件。通过更新 `apt` 包来获取最新版内核可能需要几周时间。要下载最新版本的头文件，请[克隆内核](https://www.raspberrypi.com/documentation/computers/linux_kernel.html#building)。

如果你使用的是 64 位版本的树莓派系统，请运行以下命令安装内核头文件：

```
$ sudo apt install linux-headers-rpi-v8
```

如果你使用的是 32 位版本的树莓派系统，请运行以下命令安装内核头文件：

```
$ sudo apt install linux-headers-rpi-{v6,v7,v7l}
```

>**注意**
>
>安装可能需要几分钟，没有进度指示工具。 

## 贡献

你可能有很多理由想要将某些内容加入内核：

* 你编写了一些树莓派的特定代码，希望大家都能受益
* 你编写了一款通用的 Linux 内核驱动，希望大家都能使用
* 你修复了一项通用内核 bug
* 你修复了一项树莓派的特定内核 bug

对于树莓派特定的更改/bug 修复，可向树莓派内核提交一个 pull request。对于一般的 Linux 内核更改（例如新的驱动程序），请先向上游 Linux 内核提交 pull request。待 Linux 内核接受了你的更改，我们方可收到这些更改。

### 贡献到树莓派内核

首先，复刻[树莓派内核仓库](https://github.com/raspberrypi/linux) 并将其克隆到你的开发设备上。然后，你可以进行更改、测试，并将更改提交到你的复刻。

接下来，将涉及你更改的 pull request 提交到[树莓派内核仓库](https://github.com/raspberrypi/linux)。树莓派工程师会审查你的贡献并提出改进建议。一旦获得批准，我们就会将你的更改合并，最终这些更改会进入稳定版本的树莓派内核。

### 贡献到 Linux 内核

首先，将 [Linux 内核树](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git)克隆到你的开发设备上。然后，你可以进行更改、测试，并将更改提交到你的本地树中。

若你的更改准备就绪，你可以把它提交给 Linux 内核社区。Linux 内核开发是在邮件列表（而非 GitHub）上进行的。为使你的更改成为 Linux 内核的一部分，请通过电子邮件将其作为补丁提交给社区。请遵循文档[提交补丁：如何让你的改动进入内核](https://www.kernel.org/doc/html/latest/translations/zh_CN/process/submitting-patches.html)和[Linux 内核代码风格](https://www.kernel.org/doc/html/latest/translations/zh_CN/process/coding-style.html)。Linux 内核贡献者会审查你的贡献并建议改进。获得批准后，他们会将你的更改合并。最后，这些更改会进入 Linux 内核的长期发布版本。通过树莓派内核的兼容性测试后，你的更改就会进入稳定版本的树莓派内核。
