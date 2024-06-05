# Linux 内核

## 内核

树莓派内核托管在 GitHub 上；更新滞后于上游 Linux 内核。上游内核不断更新；我们采用内核的长期版本，这些版本在首页上有提及，并将更改集成到我们自己的树莓派内核中。然后我们创建一个包含内核不稳定端口的“next”分支，经过广泛测试和讨论后，我们将其推送到我们存储库的主分支。

### 更新您的内核

如果您使用标准的 Raspberry Pi OS 更新和升级过程，这将自动将内核更新到我们内核的最新稳定版本。这是推荐的步骤。但是，在某些情况下，您可能希望更新到最新的“激进”或测试内核。只有在树莓派工程师建议这样做，或者最新软件中有特定功能时，您才应该这样做。

### 将您的代码放入内核

有许多原因您可能希望将某些内容放入内核中：

* 您编写了一些树莓派特定的代码，希望所有人都能从中受益
* 您为设备编写了一个通用的 Linux 内核驱动程序，并希望所有人都能使用它
* 您修复了一个通用内核错误
* 您修复了一个树莓派特定的内核错误

首先，您应该复刻 Linux 存储库并在构建系统上克隆该存储库；这可以是您的树莓派上的系统，也可以是您用于交叉编译的 Linux 机器。然后，您可以进行更改、测试并将其提交到您复刻的存储库中。

接下来，根据代码是树莓派特定的还是通用的进行操作：

* 对于树莓派特定的更改或错误修复，请向内核提交拉取请求。
* 对于一般的 Linux 内核更改（例如新驱动程序），这些更改需要首先提交到上游。只要它们被提交到上游并被接受，再提交拉取请求，我们就能收到它。

## 构建内核

操作系统附带的默认编译器和链接器被配置为构建可在该操作系统上运行的可执行文件 - 它们是本机工具 - 但情况并非一定如此。交叉编译器被配置为为非运行构建过程的目标构建代码，使用它被称为交叉编译。

树莓派内核的交叉编译有两个用途：它允许使用 32 位操作系统构建 64 位内核，反之亦然。这也意味着即使是一台普通的笔记本电脑也可以比树莓派本身更快地交叉编译树莓派内核。

下面的说明分为本机构建和交叉编译两部分。选择适合您情况的部分；尽管两者之间有许多共同步骤，但也存在一些重要区别。

### 本地构建内核

>**重要**
>
>在 Raspberry Pi OS 的 32 位发行版上构建 64 位内核是一个交叉编译练习，因为它需要安装交叉编译器 ( gcc-aarch64-linux-gnu )。如果你在 Pi 4B、Pi 400、CM4 或 CM4S 上运行 Raspberry Pi OS 的 32 位发行版，那么你将运行一个 32 位用户空间和 64 位内核 — 因此，如果你想显式构建一个 32 位内核，你应该设置 ARCH=arm ，并且要启动这个内核，你需要在 config.txt 中设置 arm_64bit=0 。我们提供了交叉编译内核的说明。

在树莓派上，首先安装最新版本的 Raspberry Pi OS。然后启动你的树莓派，登录，并确保你连接到互联网，以便访问源代码。

首先安装 Git 和构建依赖项：

```
sudo apt install git bc bison flex libssl-dev make
```

接下来获取源代码，这将需要一些时间：

```
git clone --depth=1 https://github.com/raspberrypi/linux
```

#### 选择源代码

上面的 git clone 命令将下载当前活动分支（我们正在构建 Raspberry Pi OS 镜像的分支）而不包含任何历史记录。省略 --depth=1 将下载整个存储库，包括所有分支的完整历史记录，但这需要更长的时间并占用更多存储空间。

要下载其他分支（同样不包含历史记录），请使用 --branch 选项：

```
git clone --depth=1 --branch <branch> https://github.com/raspberrypi/linux
```

其中 `<branch>` 是您希望下载的分支的名称。

有关可用分支的信息，请参考原始 GitHub 存储库。

#### 内核配置

配置内核；除了默认配置外，您可能希望更详细地配置内核或从其他来源应用补丁，以添加或删除所需功能。

##### 应用默认配置

首先，通过运行以下命令准备默认配置，具体取决于您树莓派的型号。

对于树莓派 1、Zero 和 Zero W，以及树莓派计算模块 1 默认（仅 32 位）构建配置：

```
cd linux
KERNEL=kernel
make bcmrpi_defconfig
```

适用于树莓派 2、3、3+ 和 Zero 2 W，以及树莓派计算模块 3 和 3+ 默认的 32 位构建配置：

```
cd linux
KERNEL=kernel7
make bcm2709_defconfig
```

适用于树莓派4 和 400，以及树莓派计算模块 4 默认的 32 位构建配置：

```
cd linux
KERNEL=kernel7l
make bcm2711_defconfig
```

适用于树莓派3、3+、4、400 和 Zero 2 W，以及树莓派计算模块 3、3+ 和 4 默认的 64 位构建配置：

```
cd linux
KERNEL=kernel8
make bcm2711_defconfig
```

针对树莓派 5 默认的 64 位构建配置：

```
cd linux
KERNEL=kernel_2712
make bcm2712_defconfig
```

##### 使用 LOCALVERSION 自定义内核版本

除了内核配置更改外，您可能希望调整 LOCALVERSION 以确保您的新内核不会收到与上游内核相同的版本字符串。这样可以澄清您在 uname 的输出中运行自己的内核，并确保 /lib/modules 中的现有模块不会被覆盖。

要调整 LOCALVERSION ，请更改 .config 中的以下行：

```
CONFIG_LOCALVERSION="-v7l-MY_CUSTOM_KERNEL"
```

您还可以按照内核配置说明中显示的图形方式更改此设置。它位于“常规设置” => “本地版本 - 附加到内核发布”。

#### 构建内核

构建并安装内核、模块和设备树块。这一步根据您使用的树莓派型号可能需要很长时间。对于 32 位内核：

```
make -j4 zImage modules dtbs
sudo make modules_install
# Choose one of the following based on the kernel version
  # For kernels up to 6.4:
  sudo cp arch/arm/boot/dts/*.dtb /boot/firmware/
  # For kernel 6.5 and above:
  sudo cp arch/arm/boot/dts/broadcom/*.dtb /boot/firmware/
sudo cp arch/arm/boot/dts/overlays/*.dtb* /boot/firmware/overlays/
sudo cp arch/arm/boot/dts/overlays/README /boot/firmware/overlays/
sudo cp arch/arm/boot/zImage /boot/firmware/$KERNEL.img
```

对于 64 位内核：

```
make -j4 Image.gz modules dtbs
sudo make modules_install
sudo cp arch/arm64/boot/dts/broadcom/*.dtb /boot/firmware/
sudo cp arch/arm64/boot/dts/overlays/*.dtb* /boot/firmware/overlays/
sudo cp arch/arm64/boot/dts/overlays/README /boot/firmware/overlays/
sudo cp arch/arm64/boot/Image.gz /boot/firmware/$KERNEL.img
```

>**注意**
>
>在树莓派 2、3、4 和 5 上，参数 `-j4` 将工作分配给所有四个核心，可显著加快编译速度。

如果您现在重启，您的树莓派应该正在运行您新编译的内核。

### 交叉编译内核

首先，您需要一个适合的 Linux 交叉编译主机。我们倾向于使用 Ubuntu；因为 Raspberry Pi OS 也是一个 Debian 发行版，这意味着许多方面都是相似的（比如命令行）。

您可以在 Windows 上使用 VirtualBox（或 VMWare）或直接将其安装到您的计算机上。

#### 安装所需的依赖项和工具链

要为交叉编译构建源代码，请确保您的计算机上已安装所需的依赖项，方法是执行：

```
sudo apt install git bc bison flex libssl-dev make libc6-dev libncurses5-dev
```

##### 安装 32 位内核的 32 位工具链

```
sudo apt install crossbuild-essential-armhf
```

##### 为 64 位内核安装 64 位工具链

```
sudo apt install crossbuild-essential-arm64
```

#### 获取内核源码

下载当前分支的最小源码，请运行：

```
git clone --depth=1 https://github.com/raspberrypi/linux
```

请参阅上面的选择源部分，了解如何选择不同的分支的说明。

#### 编译源码

输入以下命令编译源代码和设备树文件：

##### 32 位配置

适用于树莓派 1、Zero 和 Zero W，以及树莓派计算模块 1：

```
cd linux
KERNEL=kernel
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- bcmrpi_defconfig
```

适用于树莓派 2、3、3+ 和 Zero 2 W，以及树莓派计算模块 3 和 3+：

```
cd linux
KERNEL=kernel7
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- bcm2709_defconfig
```

适用于树莓派 4 和 400，以及树莓派计算模块 4：

```
cd linux
KERNEL=kernel7l
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- bcm2711_defconfig
```

##### 64 位配置

适用于树莓派 3、3+、4、400 和 Zero 2 W，以及树莓派计算模块 3、3+ 和 4：

```
cd linux
KERNEL=kernel8
make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- bcm2711_defconfig
```

适用于树莓派 5：

```
cd linux
KERNEL=kernel_2712
make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- bcm2712_defconfig
```

>**注意**
>
>标准的，基于 bcm2711_defconfig 的内核（ kernel8.img ）也可在树莓派 5 上运行。为获得最佳性能，您应该使用 kernel_2712.img ，但在需要 4KB 页大小的情况下，则应使用 kernel8.img （ kernel=kernel8.img ）。 

##### 使用配置构建

>**注意**
>
>为了加快多处理器系统上的编译速度，并在单处理器设备上获得一些改进，使用 -j n ，其中 n 是处理器数量 ×1.5。您可以使用 nproc 命令查看您有多少处理器。

###### 对于所有 32 位构建

```
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- zImage modules dtbs
```

###### 对于所有 64 位构建

>**注意**
>
>请注意 32 位和 64 位镜像目标之间的区别。 

```
make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- Image modules dtbs
```

#### 直接安装到 SD 卡上

内核编译完成后，您需要将其复制到您的树莓派上并安装模块。最好直接使用 SD 卡阅读器完成此操作。

首先，在插入 SD 卡之前和之后使用 lsblk 来识别它。您最终应该得到类似这样的东西：

```
sdb
   sdb1
   sdb2
```

其中 sdb1 是 FAT 文件系统（引导）分区， sdb2 是 ext4 文件系统（根）分区。

首先安装这些，根据需要调整分区字母：

```
mkdir mnt
mkdir mnt/fat32
mkdir mnt/ext4
sudo mount /dev/sdb1 mnt/fat32
sudo mount /dev/sdb2 mnt/ext4
```

>**注意**
>
>您应该根据您的设置适当调整驱动器字母，例如，如果您的 SD 卡显示为 /dev/sdc 而不是 /dev/sdb 。 
接下来，在 SD 卡上安装内核模块：

##### 32 位

```
sudo env PATH=$PATH make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- INSTALL_MOD_PATH=mnt/ext4 modules_install
```

##### 64 位

```
sudo env PATH=$PATH make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- INSTALL_MOD_PATH=mnt/ext4 modules_install
```

最后，将内核和设备树 blob 复制到 SD 卡上，确保备份旧内核：

##### 适用于 32 位

```
sudo cp mnt/fat32/$KERNEL.img mnt/fat32/$KERNEL-backup.img
sudo cp arch/arm/boot/zImage mnt/fat32/$KERNEL.img
# Choose one of the following based on the kernel version
  # For kernels up to 6.4:
  sudo cp arch/arm/boot/dts/*.dtb mnt/fat32/
  # For kernel 6.5 and above:
  sudo cp arch/arm/boot/dts/broadcom/*.dtb mnt/fat32/
sudo cp arch/arm/boot/dts/overlays/*.dtb* mnt/fat32/overlays/
sudo cp arch/arm/boot/dts/overlays/README mnt/fat32/overlays/
sudo umount mnt/fat32
sudo umount mnt/ext4
```

##### 适用于 64 位

```
sudo cp mnt/fat32/$KERNEL.img mnt/fat32/$KERNEL-backup.img
sudo cp arch/arm64/boot/Image mnt/fat32/$KERNEL.img
sudo cp arch/arm64/boot/dts/broadcom/*.dtb mnt/fat32/
sudo cp arch/arm64/boot/dts/overlays/*.dtb* mnt/fat32/overlays/
sudo cp arch/arm64/boot/dts/overlays/README mnt/fat32/overlays/
sudo umount mnt/fat32
sudo umount mnt/ext4
```

另一种选择是将内核复制到相同的位置，但使用不同的文件名 - 例如，使用 kernel-myconfig.img - 而不是覆盖 kernel.img 文件。然后，您可以编辑 config.txt 文件以选择树莓派将启动的内核：

```
kernel=kernel-myconfig.img
```

这样做的好处是，可以将您的自定义内核与系统管理的标准内核映像以及任何自动更新工具分开，并允许您在您的内核无法启动时轻松恢复到标准内核。

最后，将卡插入树莓派并启动。

## 配置内核

Linux 内核是高度可配置的。高级用户可能希望修改默认配置，以根据自己的需求进行定制，例如启用新的或实验性网络协议，或启用对新硬件的支持。

配置通常通过 make menuconfig 界面完成。或者，您可以手动修改 .config 文件，但这对新用户来说可能更困难。

### 准备配置

menuconfig 工具需要 ncurses 开发头文件才能正确编译。您可以使用以下命令安装这些文件：

```
 sudo apt install libncurses5-dev
```

您还需要下载和准备内核源代码，如构建指南中所述。特别要确保已安装默认配置。

### 使用 menuconfig

如果您已经设置好并准备就绪，您可以按照以下方式编译和运行 menuconfig 实用程序：

```
 make menuconfig
```

如果您正在交叉编译 32 位内核：

```
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- menuconfig
```

或者，如果您正在交叉编译 64 位内核：

```
make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- menuconfig
```

menuconfig 实用程序具有简单的键盘导航。经过简短的编译后，您将看到一个包含所有可配置选项的子菜单列表。有许多选项，所以请花些时间阅读并熟悉它们。

使用箭头键进行导航，使用回车键进入子菜单（由 ---> 指示），连续按两次 Esc 键返回上一级或退出，使用空格键循环更改选项状态。某些选项有多个选择，这种情况下它们将显示为子菜单，按回车键将选择一个选项。您可以在大多数条目上按 h 键获取有关特定选项或菜单的帮助。

抵制在第一次尝试时启用或禁用大量功能的诱惑；相对容易破坏您的配置，因此从小处开始，熟悉配置和构建过程。

### 保存您的更改

如果您完成了所需的更改，请按 Escape，直到提示您保存新配置。默认情况下，这将保存到 .config 文件。您可以通过复制此文件保存和加载配置。

## 打补丁内核

在构建自定义内核时，您可能希望将补丁或补丁集（patchsets）应用于 Linux 内核。

补丁集通常与较新的硬件一起提供，作为一种临时措施，然后将这些补丁应用于上游（主线）Linux 内核，然后传播到树莓派内核源代码。但是，也存在用于其他目的的补丁集，例如为实时使用启用完全可抢占内核。

### 版本识别

下载和应用补丁时，检查内核版本非常重要。在内核源目录中，运行 head Makefile -n 3 将显示与源相关的版本：

```
VERSION = 6
PATCHLEVEL = 1
SUBLEVEL = 38
```

在这种情况下，这些源适用于 6.1.38 内核。您可以使用 uname -r 命令查看系统上运行的版本。

### 应用补丁

应用补丁的方式取决于补丁的提供格式。大多数补丁是单个文件，并使用 patch 实用程序应用。要下载并为我们的示例内核版本打补丁以使用实时内核补丁：

```
 wget https://www.kernel.org/pub/linux/kernel/projects/rt/6.1/patch-6.1.38-rt13-rc1.patch.gz
 gunzip patch-6.1.38-rt13-rc1.patch.gz
 cat patch-6.1.38-rt13-rc1.patch | patch -p1
```

在我们的示例中，我们只需下载文件，解压缩它，然后使用 cat 工具和 Unix 管道将其传递给 patch 实用程序。

一些补丁集以邮箱格式补丁集的形式提供，排列为一组补丁文件的文件夹。我们可以使用 Git 将这些补丁应用到我们的内核，但首先必须配置 Git，让它知道我们在进行这些更改时是谁。

```
 git config --global user.name "Your name"
 git config --global user.email "your email in here"
```

在我们完成这一步之后，我们就可以应用补丁：

```
 git am -3 /path/to/patches/*
```

如果有疑问，请咨询补丁的分发者，他应该告诉您如何应用它们。有些补丁集将需要针对特定提交进行打补丁；请按照补丁分发者提供的详细信息操作。

## 内核头文件

如果您正在编译内核模块或类似内容，您将需要 Linux 内核头文件。这些文件在编译与内核进行接口的代码时提供所需的各种函数和结构定义。

如果您从 GitHub 克隆了整个内核，头文件已经包含在源代码树中。如果您不需要所有额外的文件，可以仅从 Raspberry Pi OS 存储库安装内核头文件。

如果您正在使用 Raspberry Pi OS 的 32 位版本，请运行：

```
 sudo apt install linux-headers-rpi-{v6,v7,v7l}
```

或者，如果您正在使用 Raspberry Pi OS 的 64 位版本，请运行：

```
 sudo apt install linux-headers-rpi-v8
```

>**注意**
>
>由于需要安装许多小文件，此命令完成可能需要相当长的时间。没有进度指示器。

当发布新内核版本时，您将需要与该内核版本匹配的头文件。仓库更新以同步最新内核版本可能需要几周时间。如果发生这种情况，最好的方法是克隆内核。
