# Linux 内核

## 介绍

树莓派内核托管在 [GitHub](https://github.com/raspberrypi/linux) 上，更新一般滞后于上游的 [Linux 内核](https://github.com/torvalds/linux)。上游内核在持续更新着，而树莓派内核则会集成到 **long-term releases（长期支持版本）** 的 Linux 内核。我们在 [raspberrypi/firmware](https://github.com/raspberrypi/firmware/) 中会为每个长期支持版的 Linux 内核生成一个 `next` 分支。在经过海量的测试和大规模讨论后，我们会将 `next` 分支合并到主分支中。

## 更新

一般的[更新流程](https://www.raspberrypi.com/documentation/computers/os.html#update-software)会自动将把树莓派系统的内核更新到最新稳定版本。如果你想尝试最新不稳定版测试内核，可以[手动更新](https://www.raspberrypi.com/documentation/computers/os.html#rpi-update)。

## 编译内核

操作系统自带的编译器，链接器通常配置为：为能在该系统上运行的可执行文件而进行编译。**本机编译**使用这些默认的编译器和链接器。而 **交叉编译** 是指为与当前编译环境不同的目标系统编译代码的流程。

树莓派内核的交叉编译能让你在 32 位操作系统上编译 64 位内核，反之亦然。你还可以在非树莓派设备上交叉编译 32 位（或 64 位）的树莓派内核。

以下说明分为本机编译和交叉编译两个部分。请选择适合你的那个部分，虽然这两种方式有许多相似步骤，但也有某些明显的差异。

### 下载内核源码

在为特定目标编译之前，你需要内核源码。要下载源码，你需要安装 Git。先在你的设备上安装 Git（如未安装）：

```bash
$ sudo apt install git
```

接下来，下载最新的树莓派内核源码：

```bash
$ git clone --depth=1 https://github.com/raspberrypi/linux
```

这可能需要几分钟。

>**技巧**
>
>命令 `git clone` 用于下载当前活跃分支的代码，我们用这个分支来构建树莓派系统镜像；未包含历史记录。要下载包含全部分支一切历史的完整仓库，请省略参数 `--depth=1`。这会花费更长时间，占用更多存储空间。
>
>如果需要下载的其他分支（不带历史记录），可在上述命令中添加参数 `--branch`，把 `<分支>` 改成你想下载的分支名：
>
>```bash
>$ git clone --depth=1 --branch <分支> https://github.com/raspberrypi/linux
>```
>
>要查看所有可用分支的完整列表，请参见[树莓派内核仓库](https://github.com/raspberrypi/linux)。

现在你已经有了内核源码，可以选择[本机编译](https://www.raspberrypi.com/documentation/computers/linux_kernel.html#natively-build-a-kernel)还是用[交叉编译](https://www.raspberrypi.com/documentation/computers/linux_kernel.html#cross-compile-the-kernel)构建新内核。

### 本机编译内核

本指南假设你运行着树莓派最新版本的[树莓派系统](https://www.raspberrypi.com/documentation/computers/os.html)。

先安装编译所需的依赖包：

```bash
$ sudo apt install bc bison flex libssl-dev make
```

#### 编译配置

本节介绍了如何在编译内核时采用默认配置。你也可以使用以下方式配置你的内核：

* [启用、禁用内核功能](https://www.raspberrypi.com/documentation/computers/linux_kernel.html#configure-the-kernel)
* [打上其他来源的补丁](https://www.raspberrypi.com/documentation/computers/linux_kernel.html#patch-the-kernel)

要准备默认配置，请根据你的树莓派型号执行下表中的对应命令。

| 架构                           | 型号             | 命令                                                  |
| :------------------------------: | :----------------: | :----------------------------------------------------- |
|64 位| 树莓派 3          | `$ cd linux`<br />`$ KERNEL=kernel8`<br />`$ make bcm2711_defconfig`    |
| |树莓派计算模块 3               |                  |                                                       |
| |树莓派 3+                      |                  |                                                       |
|| 树莓派计算模块 3+              |                  |                                                       |
| |树莓派 Zero 2 W                |                  |                                                       |
| |树莓派 4                       |                  |                                                       |
| |树莓派 400                     |                  |                                                       |
| |树莓派计算模块 4               |                  |                                                       |
|| 树莓派计算模块 4S              |                  |                                                       |
| |树莓派 5                       | `$ cd linux`<br />`$ KERNEL=kernel_2712`<br />`$ make bcm2712_defconfig`           |
| 32 位| 树莓派 1          | `$ cd linux`<br />`$ KERNEL=kernel`<br />`$ make bcmrpi_defconfig`    |
| |树莓派计算模块 1               |                  |                                                       |
| |树莓派 Zero                    |                  |                                                       |
|| 树莓派 Zero W                  |                  |                                                       |
|| 树莓派 2                       | `$ cd linux`<br />`$ KERNEL=kernel7`<br />`$ make bcm2709_defconfig`           |
| |树莓派 3                       |                  |                                                       |
| |树莓派计算模块 3               |                  |                                                       |
|| 树莓派 3+                      |                  |                                                       |
| |树莓派计算模块 3+              |                  |                                                       |
| |树莓派 Zero 2 W                |                  |                                                       |
| |树莓派 4                       | `$ cd linux`<br />`$ KERNEL=kernel7l`<br />`$ make bcm2711_defconfig`           |
| |树莓派 400                     |                  |                                                       |
| |树莓派计算模块 4               |                  |                                                       |
|| 树莓派计算模块 4S              |                  |                                                       |

>**注意**
>
>树莓派 4B、5、400，计算模块 4、计算模块 4S 上的 32 位版树莓派系统使用 32 位用户空间，但运行的是 **64 位内核**。如果要编译 32 位内核，请设置 `ARCH=arm`。若要启动 32 位内核，在 `config.txt` 中设置 `arm_64bit=0`。


### 交叉编译内核

首先，你需要一台合适的 Linux 交叉编译主机。我们一般用 Ubuntu。由于树莓派系统同样也是一款基于 Debian 的发行版，所以编译命令非常接近。

#### 安装所需的依赖和工具链

要为交叉编译构建源代码，请在设备上安装所需的依赖包。运行以下命令可安装大多数依赖：

```bash
$ sudo apt install bc bison flex libssl-dev make libc6-dev libncurses5-dev
```

然后，安装适用于你要编译的内核架构之工具链：

* 要安装用于编译 64 位内核的 64 位工具链，请运行以下命令：

  ```bash
  $ sudo apt install crossbuild-essential-arm64
  ```
* 要安装用于编译 32 位内核的 32 位工具链，请运行以下命令：

  ```bash
  $ sudo apt install crossbuild-essential-armhf
  ```

#### 构建配置

本节介绍了如何在构建内核时采用默认配置。你也可以用下述方式配置内核：

* [启用、禁用内核功能](https://www.raspberrypi.com/documentation/computers/linux_kernel.html#configure-the-kernel)
* [打上其他来源的补丁](https://www.raspberrypi.com/documentation/computers/linux_kernel.html#patch-the-kernel)

输入以下命令构建源代码和设备树文件：

| 目标架构       | 目标型号                   | 命令                                                                                                                                                      |
| :--------------: | :--------------------------: | :--------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 64 位          | 树莓派 3                   | `$ cd linux`<br />`$ KERNEL=kernel8`<br />`$ make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- bcm2711_defconfig`                                            |
|| 树莓派计算模块 3                      |                                                                                                                                                           |
|| 树莓派 3+                                |                                                                                                                                                           |
|| 树莓派计算模块 3+                           |                                                                                                                                                           |
|| 树莓派 Zero 2 W                           |                                                                                                                                                           |
|| 树莓派 4                              |                                                                                                                                                           |
|| 树莓派 400                               |                                                                                                                                                           |
|| 树莓派计算模块 4                             |                                                                                                                                                           |
|| 树莓派计算模块 4S                            |                                                                                                                                                           |
|| 树莓派 5       | `$ cd linux`<br />`$ KERNEL=kernel_2712`<br />`$ make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- bcm2712_defconfig`                       |
| 32 位 |        树莓派 1                   | `$ cd linux`<br />`$ KERNEL=kernel`<br />`$ make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- bcmrpi_defconfig`                                              |
|| 树莓派计算模块 1                            |                                                                                                                                                           |
|| 树莓派 Zero                               |                                                                                                                                                           |
|| 树莓派 Zero W                             |                                                                                                                                                           |
|| 树莓派 2       | `$ cd linux`<br />`$ KERNEL=kernel7`<br />`$ make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- bcm2709_defconfig`                           |
|| 树莓派 3       |                            |                                                                                                                                                           |
| |树莓派计算模块 3 |                            |                                                                                                                                                           |
| |树莓派 3+      |                            |                                                                                                                                                           |
| |树莓派计算模块 3+ |                            |                                                                                                                                                           |
| |树莓派 Zero 2 W |                            |                                                                                                                                                           |
| |树莓派 4       | `$ cd linux`<br />`$ KERNEL=kernel7l`<br />`$ make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- bcm2711_defconfig`                          |
| |树莓派 400     |                            |                                                                                                                                                           |
| |树莓派计算模块 4 |                            |                                                                                                                                                           |
| |树莓派计算模块 4S |                            |                                                                                                                                                           |

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

* 运行以下命令编译 64 位内核：

  ```bash
  $ make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- Image modules dtbs
  ```
* 运行以下命令编译 32 位内核：

  ```bash
  $ make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- zImage modules dtbs
  ```

#### 安装内核

内核编译完成后，你需要将其复制到树莓派的启动介质（通常是 SD 卡或 SSD）上，并安装模块。

##### 找到你的启动介质

首先，运行 `lsblk`。然后连接启动介质，再次运行 `lsblk`；新出现的设备就是你的启动介质。你会看到类似如下的输出：

```
sdb
   sdb1
   sdb2
```

如果 `sdb` 代表你的启动介质，`sdb1` 代表 **启动分区**（`FAT32` 格式），而 `sdb2` 代表（可能是 `ext4` 格式的）**根分区**。

首先，将这些分区挂载为 `mnt/boot` 和 `mnt/root`，并根据启动介质的实际位置调整分区字母：

```
$ mkdir mnt
$ mkdir mnt/boot
$ mkdir mnt/root
$ sudo mount /dev/sdb1 mnt/boot
$ sudo mount /dev/sdb2 mnt/root
```

##### 安装

接下来，将内核模块安装到启动介质上：

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
>在多核设备上，`make -j<n>` 选项会将工作分配到多个核心，从而显著加快编译速度。运行 `nproc` 查看你有多少处理器，我们建议传递的数字为处理器数量的 1.5 倍。


接下来，将内核和设备树文件安装到启动分区中，并备份原始内核。

要安装 64 位内核：

* 运行以下命令创建当前内核的备份镜像，安装新的内核镜像、覆盖文件、README 文件，并卸载分区：

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

1. 运行以下命令创建当前内核的备份镜像并安装新的内核镜像：

    ```bash
    $ sudo cp mnt/boot/$KERNEL.img mnt/boot/$KERNEL-backup.img
    $ sudo cp arch/arm/boot/zImage mnt/boot/$KERNEL.img
    ```
2. 根据你的[内核版本](https://www.raspberrypi.com/documentation/computers/linux_kernel.html#identify-your-kernel-version)，运行以下命令安装设备树文件：

    * 对于 6.4 及以下版本的内核：

      ```bash
      $ sudo cp arch/arm/boot/dts/*.dtb mnt/boot/
      ```
    * 对于 6.5 及以上版本的内核：

      ```bash
      $ sudo cp arch/arm/boot/dts/broadcom/*.dtb mnt/boot/
      ```
3. 最后，安装覆盖文件和 README 文件，并卸载分区：

    ```bash
    $ sudo cp arch/arm/boot/dts/overlays/*.dtb* mnt/boot/overlays/
    $ sudo cp arch/arm/boot/dts/overlays/README mnt/boot/overlays/
    $ sudo umount mnt/boot
    $ sudo umount mnt/root
    ```

最后，将启动介质连接到你的树莓派，并连接电源以运行你刚编译的内核。

>**技巧**
>
>或者，可以使用不同的文件名（例如 `kernel-myconfig.img`）来复制内核，而不是覆盖 `kernel.img` 文件。然后，编辑启动分区中的 `config.txt` 文件以选择您的内核：
>
>```bash
>kernel=kernel-myconfig.img
>```
>
>将这种方法与自定义 `LOCALVERSION` 结合使用，以将您的自定义内核与系统管理的标准内核镜像分开。在这种安排下，如果您的内核无法启动，您可以快速恢复到标准内核。


## 配置内核

Linux 内核高度可配置。高级用户可能希望修改默认配置以满足他们的需求，例如启用新的或实验性的网络协议，或支持新硬件。

配置最常通过 `make menuconfig` 界面进行。你也可以手动修改 `.config` 文件，但这可能会更复杂。

### 准备配置

`menuconfig` 工具需要 `ncurses` 开发头文件才能正确编译。要安装这些头文件，请运行以下命令：

```bash
$ sudo apt install libncurses5-dev
```

接下来，[下载内核源代码](https://www.raspberrypi.com/documentation/computers/linux_kernel.html#download-kernel-source)。特别是，确保你已经安装了[默认的本地配置](https://www.raspberrypi.com/documentation/computers/linux_kernel.html#native-build-configuration)或[默认的交叉编译配置](https://www.raspberrypi.com/documentation/computers/linux_kernel.html#cross-compiled-build-configuration)。

### `menuconfig`

待一切准备就绪，你可以按如下方式编译和运行 `menuconfig` 实用程序：

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

要使用 `menuconfig` 实用程序，使用键盘操作：

* 使用 **箭头键** 进行方向导航
* 要进入子菜单（由 `--->` 指示），按 **Enter** 键
* 要返回上一级或退出，按 **Escape** 键两次
* 要切换二进制选项的状态，按 **空格键**
* 要选择多选项的状态，按 **Enter** 打开子菜单，使用 **箭头键** 导航子菜单，再按 **Enter** 选择状态
* 要获取选项或菜单的帮助，按 **H** 键

在简短的编译之后，`menuconfig` 会显示一个包含所有可以配置选项的子菜单列表。选项很多，所以花点时间阅读。避免在第一次尝试时启用或禁用过多的选项；配置过程相对容易出错，所以从小处开始，熟悉配置和构建过程。

### 保存更改

完成更改后，按 **Escape** 直到出现保存新配置的提示。默认情况下，这会保存到 `.config` 文件。你可以通过复制此文件来保存和加载配置。

自定义完成后，你现在可以[构建内核](https://www.raspberrypi.com/documentation/computers/linux_kernel.html#building)了。

## 打补丁

在构建自定义内核时，你可能希望将补丁或补丁集合（补丁集）应用到 Linux 内核。

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

### 应用补丁

应用补丁的方式取决于补丁的分发格式。

开发人员通常将大多数补丁以单个文件的形式分发。使用 `patch` 工具来应用这些补丁。以下命令下载、解压并将实时内核补丁应用到我们的示例内核版本中：

```bash
$ wget https://www.kernel.org/pub/linux/kernel/projects/rt/6.1/patch-6.1.38-rt13-rc1.patch.gz
$ gunzip patch-6.1.38-rt13-rc1.patch.gz
$ cat patch-6.1.38-rt13-rc1.patch | patch -p1
```

有些开发人员以**邮箱格式**分发补丁，这是一种包含多个补丁文件的文件夹。使用 Git 来应用这些补丁。

>**注意**
>
>在使用 Git 应用邮箱补丁之前，请为您的本地 Git 安装配置一个姓名和电子邮件：
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

如果你从 GitHub 克隆了整个内核，头文件已经包含在源代码树中。如果你不需要所有额外的文件，可以仅安装内核头文件，使用 `apt`。

>**技巧**
>
>当发布新内核时，你需要与该内核版本匹配的头文件。更新 `apt` 包以反映最新内核版本可能需要几周时间。要获取最新的头文件版本，[克隆内核](https://www.raspberrypi.com/documentation/computers/linux_kernel.html#building)。

如果你使用的是 64 位版本的树莓派系统，运行以下命令安装内核头文件：

```
$ sudo apt install linux-headers-rpi-v8
```

如果你使用的是 32 位版本的树莓派系统，运行以下命令安装内核头文件：

```
$ sudo apt install linux-headers-rpi-{v6,v7,v7l}
```

>**注意**
>
>安装可能需要几分钟，没有进度指示器。 

## 贡献

你可能有很多理由想要将某些内容加入内核：

* 你编写了一些特定于树莓派的代码，希望大家都能受益
* 你编写了一个通用的 Linux 内核驱动，希望大家都能使用
* 你修复了一个通用内核 bug
* 你修复了一个特定于树莓派的内核 bug

对于树莓派特定的更改或 bug 修复，向树莓派内核提交一个 pull request。对于一般的 Linux 内核更改（例如新的驱动程序），首先向上游 Linux 内核提交 pull request。待 Linux 内核接受了你的更改，我们会收到这些更改。

### 贡献到树莓派内核

首先，复刻[树莓派内核仓库](https://github.com/raspberrypi/linux) 并将其克隆到你的开发设备上。然后，你可以进行更改、测试，并将更改提交到你的复刻。

接下来，将包含你更改的 pull request 提交到[树莓派内核仓库](https://github.com/raspberrypi/linux)。树莓派工程师会审查你的贡献并建议改进。待获得批准，我们会将你的更改合并，最终这些更改会进入树莓派内核的稳定版本。

### 贡献到 Linux 内核

首先，将 [Linux 内核树](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git)克隆到你的开发设备上。然后，你可以进行更改、测试，并将更改提交到你的本地树中。

若你的更改准备好，你可以将其提交给 Linux 内核社区。Linux 内核开发是在邮件列表上进行的，而不是在 GitHub 上。为了使你的更改成为 Linux 内核的一部分，请通过电子邮件将其作为补丁提交给社区。请遵循[提交补丁：将你的代码加入内核的基本指南](https://www.kernel.org/doc/html/latest/process/submitting-patches.html)和[Linux 内核编码风格](https://www.kernel.org/doc/html/latest/process/coding-style.html)的文档。Linux 内核贡献者会审查你的贡献并建议改进。获得批准后，他们会将你的更改合并。最终，这些更改会进入 Linux 内核的长期发布版本。经过测试与树莓派内核的兼容性后，你的更改会进入树莓派内核的稳定版本。
