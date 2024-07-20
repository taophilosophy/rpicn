# 树莓派硬件

## 介绍

树莓派推出了 **多个** 系列的计算机：

* **旗舰系列** 通常被简称为“Raspberry Pi（树莓派）”，搭载高性能硬件、完整的 Linux 操作系统。其外形尺寸与信用卡大小相当，内置了大量常见接口。
* **Zero** 系列搭载了完整的 Linux 操作系统和最基本的接口，价格实惠，体积小，功耗低。
* 计算模块系列，一般简称为 "CM"。计算模块系列搭载了高性能硬件和完整的 Linux 操作系统，适合工业和嵌入式的小尺寸用途。计算模块拥有与相应旗舰型号相当的硬件，但接口较少，甚至没有板载 GPIO 引脚。用户需将计算模块连接到一块独立的基板上，它提供了使用接口和引脚。

此外，树莓派还推出了 Pico 系列微型多用途微控制器板。Pico 型号不运行 Linux，也不支持可移动存储，只能通过把二进制文件刷入到板载闪存存储器的方式进行编程。

### 旗舰系列

B 代表其带有以太网口。A 代表低成本产品线——他们体积更小，没有以太网口，内存也小；因受开发版高度限制，USB 接口也更少。

| Model                                                                                                                                                             | SoC                                    | 存储                     | GPIO              | 外设接口                                                                                                                                                                                                                                                                                                                                            |
| ----------------------------- | ---------------------------------------- | -------------------------- | ------------------- | -------------------------------------- |
| <img style="width:60%;"  src="https://www.raspberrypi.com/documentation/computers/images/model-b.jpg?hash=caa7985f73e4fb3af8fb7b0a614d88b3" /> <br> 树莓派 A                | [BCM2835](https://www.raspberrypi.com/documentation/computers/processors.html#bcm2835)                                       | 256MB<br><br>512MB           | 26 针 GPIO 母座 |* HDMI<br>* 2 × USB 2.0<br>* CSI 相机接口 <br>* DSI 显示器接口 <br>* 3.5 mm 音频插孔 <br>* RCA 复合视频 <br>* 以太网（100Mb/s）<br>* SD 卡插槽 <br>* micro USB 电源                                                                                                                                                                                                           |
| <img style="width:60%;"  src="https://www.raspberrypi.com/documentation/computers/images/model-a.jpg?hash=9b8ad338273f437641f74eb13a32adc1" /><br> 树莓派 A        | [BCM2835](https://www.raspberrypi.com/documentation/computers/processors.html#bcm2835)                                       | 256MB                    | 26 针 GPIO 母座 | * HDMI<br>* USB 2.0<br>* CSI 摄像头接口 <br>* DSI 显示接口 <br>* 3.5 mm 音频插孔 <br>* RCA 复合视频 <br>* SD 卡插槽 <br>* micro USB 电源                                                                                                                                                                                                                                         |
| <img style="width:60%;"  src="https://www.raspberrypi.com/documentation/computers/images/model-b-plus.jpg?hash=83f51a836116f3df1378346158d6e148" /><br> 树莓派 A+ | [BCM2835](https://www.raspberrypi.com/documentation/computers/processors.html#bcm2835)                                       | 512MB                    | 40 针 GPIO 母座   | * HDMI<br>* 4 × USB 2.0<br>* CSI 摄像头接口 <br>* DSI 显示器接口 <br>* 3.5 mm AV 插孔 <br>* 以太网（100Mb/s）<br>* microSD 卡槽 <br>* micro USB 电源                                                                                                                                                                                                                           |
| <img style="width:60%;"  src="https://www.raspberrypi.com/documentation/computers/images/model-a-plus.jpg?hash=e0df62b537945082df16ff45f453d2ad" /><br> 树莓派 A+         | [BCM2835](https://www.raspberrypi.com/documentation/computers/processors.html#bcm2835)                                       | 256MB<br><br>512MB           | 40 针 GPIO  母座    | * HDMI<br>* USB 2.0<br>* CSI 摄像头接口 <br>* DSI 显示器接口 <br>* 3.5 mm 音视频插孔 <br>* microSD 卡槽 <br>* micro USB 供电                                                                                                                                                                                                                                                |
| <img style="width:60%;"  src="https://www.raspberrypi.com/documentation/computers/images/2-model-b.jpg?hash=f7ccdaf24be1e125198d6ef11a7d3258" /><br> 树莓派 2 型 B           | BCM2836（在 1.2 版中切换到 BCM2837） | 1 GB                     | 40 针 GPIO 母座   | * HDMI <br>* 4 × USB 2.0 <br>* CSI 摄像头接口 <br>* DSI 显示接口 <br>* 3.5 mm AV 插孔 <br>* 以太网 （100Mb/s）<br>* microSD 卡插槽 <br>* micro USB 电源                                                                                                                                                                                                                           |
| <img style="width:60%;"  src="https://www.raspberrypi.com/documentation/computers/images/3-model-b.jpg?hash=26b673f0b2c427e9e29fada4336a3569" /><br> 树莓派 3 A        | [BCM2837](https://www.raspberrypi.com/documentation/computers/processors.html#bcm2837)                                       | 1 GB                     | 40 针 GPIO 母座    | * HDMI <br>* 4 × USB 2.0 <br>* CSI 摄像头接口 <br>* DSI 显示器接口 <br>* 3.5 mm AV 插孔 <br>* 以太网（100Mb/s）<br>* 2.4GHz 单频 802.11n Wi-Fi（35Mb/s）<br>* 蓝牙 4.1，蓝牙低功耗（BLE）<br>* microSD 卡槽 <br>* micro USB 电源                                                                                                                                                      |
| <img style="width:60%;"  src="https://www.raspberrypi.com/documentation/computers/images/3-model-b-plus.jpg?hash=55357b0ece66311f90f82db2dc09f3d2" /><br> 树莓派 3B+    | [BCM2837b0](https://www.raspberrypi.com/documentation/computers/processors.html#bcm2837b0)                                       | 1GB                      | 40 针 GPIO 母座 | * HDMI<br>* 4 × USB 2.0<br>* CSI 相机接口 <br>* DSI 显示接口 <br>* 3.5 mm AV 插孔 <br>* 支持 PoE 的以太网（300Mb/s）<br>* 2.4/5GHz 双频 802.11ac Wi-Fi（100Mb/s）<br>* 蓝牙 4.2，蓝牙低功耗（BLE）<br>* microSD 卡槽 <br>* micro USB 电源                                                                                                                                             |
| <img style="width:60%;"  src="https://www.raspberrypi.com/documentation/computers/images/3-model-a-plus.jpg?hash=e8035ce9e2c7f5d1c8050e039aaacbaa" /><br> 树莓派 3A+    | [BCM2837b0](https://www.raspberrypi.com/documentation/computers/processors.html#bcm2837b0)                                       | 512 MB                   | 40 针 GPIO 母座   | * HDMI <br>* USB 2.0 <br>* CSI 相机接口 <br>* DSI 显示接口 <br>* 3.5 mm AV 插孔 <br>* 2.4/5GHz 双频段 802.11ac Wi-Fi （100Mb/s） <br>* 蓝牙 4.2、低功耗蓝牙（BLE） <br>* microSD 卡槽 <br>* micro USB 电源                                                                                                                                                                     |
| <img style="width:60%;"  src="https://www.raspberrypi.com/documentation/computers/images/4-model-b.jpg?hash=f56bee1ea763677368e20dbc59574c85" /><br> 树莓派 4 A  | [BCM2711](https://www.raspberrypi.com/documentation/computers/processors.html#bcm2711)                                       | 1GB<br><br>2GB<br><br>4GB<br><br>8GB | 40 针 GPIO 母座 | * 2 × micro HDMI <br>* 2 × USB 2.0<br>* 2 × USB 3.0<br>* CSI 摄像头接口 <br>* DSI 显示屏接口 <br>* 3.5 mm 音视频插孔 <br>* PoE 支持的千兆以太网（1Gb/s）<br>* 2.4/5GHz 双频 802.11ac Wi-Fi (120Mb/s)<br>* 蓝牙 5, 低功耗蓝牙（BLE）<br>* microSD 卡槽 <br>* USB-C 电源 (5V, 3A (15W))                                                                                                       |
| <img style="width:60%;"  src="https://www.raspberrypi.com/documentation/computers/images/400.jpg?hash=59a07dc791fc54f56c2416f42ced88e3" /><br> 树莓派 400                    | [BCM2711](https://www.raspberrypi.com/documentation/computers/processors.html#bcm2711)                                       | 4GB                      | 40 针 GPIO 母座 | * 2× micro HDMI <br>* USB 2.0 <br>* 2× USB 3.0 <br>* 千兆以太网（1Gb/s） <br>* 2.4/5GHz 双频 802.11ac 无线网络（120Mb/s） <br>* 蓝牙 5，蓝牙低功耗（BLE） <br>* microSD 卡槽 <br>* USB-C 电源（5V，3A（15W））                                                                                                                                                            |
| <img style="width:60%;"  src="https://www.raspberrypi.com/documentation/computers/images/5.jpg?hash=b888dab3bb8bcb8dd4e0541c99238eec" /><br> 树莓派 5                                | [BCM2712](https://www.raspberrypi.com/documentation/computers/processors.html#bcm2712)                                       | 4GB<br><br>8GB | 40 针 GPIO 母座 | * 2 × micro HDMI<br>* 2 × USB 2.0<br>* 2 × USB 3.0<br>* 2 × CSI 摄像头/DSI 显示接口 <br>* 单通道 PCIe FFC 连接器 <br>* UART 连接器 <br>* RTC 电池连接器 <br>* 四针 JST-SH PWM 风扇连接器 <br>* 支持 PoE+ 的千兆以太网（1Gb/s）<br>* 2.4/5GHz 双频段 802.11ac Wi-Fi 5（300Mb/s）<br>* 蓝牙 5，低功耗蓝牙（BLE）<br>* microSD 卡槽 <br>* USB-C 电源（5V 5A（25W），支持 5V 3A（15W），但会将外设限制到 600mA）|

更多有关旗舰系列树莓派接口的信息，请参阅原理图和机械图。

### Zero 系列

带 H 后缀的型号在 GPIO 母座上预先焊接了排针。不带 H 后缀的型号 GPIO 母座上没有焊接排针；用户必须手动焊接排针或者使用第三方排针套件。

所有 Zero 系列型号具有以下连接功能：

* 一个 microSD 卡槽
* 一个 CSI 摄像头接口 (早期的 Zero 1.3 版引入了该接口)
* 一个 mini HDMI 接口
* 2 × micro USB 接口（一个用于电源输入，另一个供外部设备使用）

| Model                                                                                                                                                   | SoC | 存储器 | GPIO                          | 无线连接                                                             |
| ---------------------------------------- | ----- | -------- | ------------------------------- | ---------------------------------------------------------------------- |
| <img style="width:60%;"  src="https://www.raspberrypi.com/documentation/computers/images/zero.jpg?hash=2d93a49cf668312604cfc00fc0660214" /><br> 树莓派 Zero             | [BCM2835](https://www.raspberrypi.com/documentation/computers/processors.html#bcm2835)    | 512MB  | 40 针 GPIO 母座（未焊接）   | 无                                                                   |
| <img style="width:60%;"  src="https://www.raspberrypi.com/documentation/computers/images/zero-w.jpg?hash=3752f16ba033177e867614e87292076d" /><br> 树莓派 Zero W       | [BCM2835](https://www.raspberrypi.com/documentation/computers/processors.html#bcm2835)    | 512MB  | 40 针 GPIO 母座（未焊接）   | * 2.4GHz 单频 802.11n Wi-Fi（35Mb/s）<br>* 蓝牙 4.0，蓝牙低功耗（BLE）   |
| <img style="width:60%;"  src="https://www.raspberrypi.com/documentation/computers/images/zero-wh.jpg?hash=f7d7c5c9b132395f45c308741fc85c7e" /><br> 树莓派 Zero WH    | [BCM2835](https://www.raspberrypi.com/documentation/computers/processors.html#bcm2835)    | 512MB  | 40 针 GPIO 母座            | * 2.4GHz 单频 802.11n Wi-Fi（35Mb/s）<br>* 蓝牙 4.0，蓝牙低功耗（BLE） |
| <img style="width:60%;"  src="https://www.raspberrypi.com/documentation/computers/images/zero-2-w.jpg?hash=5c934105e0a9be90fa0d506cac91a46f" /><br> 树莓派 Zero 2 W | [RP3A0](https://www.raspberrypi.com/documentation/computers/processors.html#rp3a0)    | 512MB  | 40 针 GPIO 母座（未焊接） | * 2.4GHz 单频 802.11n Wi-Fi (35Mb/s)<br>* 蓝牙 4.2，蓝牙低功耗（BLE）  |

### 计算模块系列

| Model                                                                                                                                                                           | SoC | 存储器                   | 存储                                 | 外形尺寸                | 无线连接                                                                    |
|---------------------------------------------- | ----- | -------------------------- | -------------------------------------- | ------------------------- | ----------------------------------------------------------------------------- |
| <img style="width:60%;"  src="https://www.raspberrypi.com/documentation/computers/images/compute-module-1.jpg?hash=725d6ee61d958098dc68dc7739deab88" /><br> 树莓派计算模块 1 | [BCM2835](https://www.raspberrypi.com/documentation/computers/processors.html#bcm2835)    | 512MB                    | 0GB（精简版）<br><br>4GB                 | DDR2 SO-DIMM            | none                                                                        |
| <img style="width:60%;"  src="https://www.raspberrypi.com/documentation/computers/images/compute-module-3.jpg?hash=3a5ff7c853190d7a07c51bf67c1082b8" /><br> 树莓派计算模块 3        | [BCM2837](https://www.raspberrypi.com/documentation/computers/processors.html#bcm2837)    | 1GB                      | 0GB（精简版）<br><br>4GB                 | DDR2 SO-DIMM            | 无                                                                          |
| <img style="width:60%;"  src="https://www.raspberrypi.com/documentation/computers/images/compute-module-3-plus.jpg?hash=352ed6d3402586078299193abe8ba754" /><br> 树莓派计算模块 3+ | [BCM2837b0](https://www.raspberrypi.com/documentation/computers/processors.html#bcm2837b0)    | 1GB                      | 0GB（Lite）<br><br>8GB<br><br>16GB<br><br>32GB   | DDR2 SO-DIMM            | 无                                                                          |
| <img style="width:60%;"  src="https://www.raspberrypi.com/documentation/computers/images/compute-module-4s.jpg?hash=4ec9821548515598adfe5a3cdc14789d" /><br> 树莓派计算模块 4S     | [BCM2711](https://www.raspberrypi.com/documentation/computers/processors.html#bcm2711)    | 1GB<br><br>2GB<br><br>4GB<br><br>8GB | 0GB（精简版）<br><br>8GB<br><br>16GB<br><br>32GB | DDR2 SO-DIMM            | 无                                                                          |
| <img style="width:60%;"  src="https://www.raspberrypi.com/documentation/computers/images/compute-module-4.jpg?hash=989dcf3efb7c9d59f463fe404a5e3820" /><br> 树莓派计算模块 4        | [BCM2711](https://www.raspberrypi.com/documentation/computers/processors.html#bcm2711)    | 1GB<br><br>2GB<br><br>4GB<br><br>8GB | 0GB (精简)<br><br>8GB<br><br>16GB<br><br>32GB    | 双 100 引脚高密度连接器 | 可选:<br><br>* 2.4/5GHz 双频 802.11ac Wi-Fi 5 （300Mb/s）<br>* 蓝牙 5, 低功耗蓝牙（BLE） |

>**注意**
>
>几个计算模块外形尺寸与物理 DDR2 SO-DIMM 兼容，但与 DDR2 SO-DIMM 电气规格不兼容。

有关树莓派计算模块的更多信息，请参阅计算模块文档。

### Pico 微控制器

带 H 后缀的型号在 GPIO 母座上预先焊接了排针。不带 H 后缀的型号不附带已连接到 GPIO 母座的排针；用户必须手动焊接排针或者连接第三方排针套件。

| Model                                                                                                                                                   | SoC | 存储       | 存储空间 | GPIO                      | 无线连接                                                             |
| --------------------------------------------------------------------------------------------------------------------------------------------------------- | ----- | ------------ | ---------- | --------------------------- | ---------------------------------------------------------------------- |
| <img style="width:60%;"  src="https://www.raspberrypi.com/documentation/computers/images/pico.png?hash=950c52fb95a01a3eec3b225e71a14bc9" /><br> 树莓派 Pico             | [RP2040](https://www.raspberrypi.com/documentation/microcontrollers/rp2040.html#welcome-to-rp2040)    | 264  KB | 2MB      | 40 针 GPIO 母座（未焊接） | 无                                                                   |
| <img style="width:60%;"  src="https://www.raspberrypi.com/documentation/computers/images/pico-h.png?hash=26d4f02827ffd2c911119d36da30bb27" /><br> 树莓派 Pico H       | [RP2040](https://www.raspberrypi.com/documentation/microcontrollers/rp2040.html#welcome-to-rp2040)    | 264  KB | 2MB      | 40 针 GPIO 母座（未焊接） | 无                                                                   |
| <img style="width:60%;"  src="https://www.raspberrypi.com/documentation/computers/images/pico-w.png?hash=ab356bc12db87ee6d8d3d62388baf4bd" /><br> 树莓派 Pico W | [RP2040](https://www.raspberrypi.com/documentation/microcontrollers/rp2040.html#welcome-to-rp2040)    | 264  KB | 2MB      | 40 针 GPIO 母座（未焊接） | * 2.4GHz 单频 802.11n Wi-Fi（10Mb/s）<br>* 蓝牙 5.2，蓝牙低功耗（BLE） |
|<img style="width:60%;"  src="https://www.raspberrypi.com/documentation/computers/images/pico-wh.png?hash=a6be966c70758bbcd9f5115c4096cf2c" /><br> 树莓派 Pico WH    | [RP2040](https://www.raspberrypi.com/documentation/microcontrollers/rp2040.html#welcome-to-rp2040)    | 264  KB | 2MB      | 40 针 GPIO 母座        | * 2.4GHz 单频 802.11n Wi-Fi（10Mb/s）<br>* 蓝牙 5.2，蓝牙低功耗（BLE） |

有关各种型号树莓派 Pico 的更多信息，请参阅 Pico 文档。

## 电路图和机械图纸

各种树莓派开发板的原理图：

### 树莓派 5

* [机械图纸，PDF](https://datasheets.raspberrypi.com/rpi5/raspberry-pi-5-mechanical-drawing.pdf)
* 树莓派 5 的 STEP 文件

### 树莓派 4 型号 B

* [原理图，版本 4.0](https://datasheets.raspberrypi.com/rpi4/raspberry-pi-4-reduced-schematics.pdf)
* [机械图纸，PDF](https://datasheets.raspberrypi.com/rpi4/raspberry-pi-4-mechanical-drawing.pdf)
* [机械图纸，DXF](https://datasheets.raspberrypi.com/rpi4/raspberry-pi-4-mechanical-drawing.dxf)

### 树莓派 3 A+

* [示意图，修订版 1.0](https://datasheets.raspberrypi.com/rpi3/raspberry-pi-3-b-plus-reduced-schematics.pdf)
* [机械图纸，PDF](https://datasheets.raspberrypi.com/rpi3/raspberry-pi-3-b-plus-mechanical-drawing.pdf)
* [机械图纸，DXF](https://datasheets.raspberrypi.com/rpi3/raspberry-pi-3-b-plus-mechanical-drawing.dxf)
* [案例图纸，PDF](https://datasheets.raspberrypi.com/case/raspberry-pi-3-b-plus-case-mechanical-drawing.pdf)

### 树莓派 3 A+

* [方案图，版本 1.0](https://datasheets.raspberrypi.com/rpi3/raspberry-pi-3-a-plus-reduced-schematics.pdf)
* [机械图纸，PDF](https://datasheets.raspberrypi.com/rpi3/raspberry-pi-3-a-plus-mechanical-drawing.pdf)
* [外壳图纸，PDF](https://datasheets.raspberrypi.com/case/raspberry-pi-3-a-plus-case-mechanical-drawing.pdf)

### 树莓派 3 B

* [原理图，修订版 1.2](https://datasheets.raspberrypi.com/rpi3/raspberry-pi-3-b-reduced-schematics.pdf)
* [机械图纸，PDF](https://datasheets.raspberrypi.com/rpi3/raspberry-pi-3-b-mechanical-drawing.pdf)
* [机械图纸，DXF](https://datasheets.raspberrypi.com/rpi3/raspberry-pi-3-b-mechanical-drawing.dxf)

### 树莓派 2 B 

* [电路图，修订版 1.2](https://datasheets.raspberrypi.com/rpi2/raspberry-pi-2-b-reduced-schematics.pdf)

### 树莓派 1 B+

* [原理图，修订版 1.2](https://datasheets.raspberrypi.com/rpi/raspberry-pi-b-plus-reduced-schematics.pdf)
* [机械图纸，PDF](https://datasheets.raspberrypi.com/rpi/raspberry-pi-b-plus-mechanical-drawing.pdf)
* [机械图纸，DXF](https://datasheets.raspberrypi.com/rpi/raspberry-pi-b-plus-mechanical-drawing.dxf)

### 树莓派 1 A+

* [电路图，修订版 1.1](https://datasheets.raspberrypi.com/rpi/raspberry-pi-a-plus-reduced-schematics.pdf)

>**注意**
>
>树莓派 3 A+ 的机械图也适用于树莓派 1 A+。
### 树莓派 Zero 2 W

* [线路图](https://datasheets.raspberrypi.com/rpizero2/raspberry-pi-zero-2-w-reduced-schematics.pdf)
* [机械图纸，PDF](https://datasheets.raspberrypi.com/rpizero2/raspberry-pi-zero-2-w-mechanical-drawing.pdf)
* [测试点](https://datasheets.raspberrypi.com/rpizero2/raspberry-pi-zero-2-w-test-pads.pdf)

#### 测试点

树莓派 Zero 2 W 在生产过程中使用了许多测试点位置。

![zero2 pad diagram](https://www.raspberrypi.com/documentation/computers/images/zero2-pad-diagram.png?hash=2e74c93201a0f4ee0c22848ce2cfa382)

| 标签           | 功能                        | X（距原点，mm） | 距原点 Y（mm） |
| ---------------- | ----------------------------- | --------------------- | -------------------- |
| STATUS\_LED | LED 的电源状态（低 = 打开） | 5.15                | 8.8                |
| CORE           | 处理器电源                  | 6.3                 | 18.98              |
| RUN            | 连接 GND 可复位           | 8.37                | 22.69              |
| 5V             | 5V 输入                     | 8.75                | 11.05              |
| 5V             | 5V 输入                     | 11.21               | 6.3                |
| GND            | 接地                   | 10.9                | 3.69               |
| GND            | 接地                  | 17.29               | 2.41               |
| USB\_DP     | USB 接口                    | 22.55               | 1.92               |
| USB\_DM     | USB 接口                 | 24.68               | 1.92               |
| OTG            | 在路上的 ID 针脚            | 39.9                | 7.42               |
| 1V8            | 1.8V 模拟供电               | 42.03               | 8.42               |
| TV             | 复合电视输出                | 45.58               | 3.17               |
| GND            | 接地                       | 49.38               |3.05               |
| GND            | 接地                     | 55.99               | 22.87              |
| 3V3            | 3.3V I/O 供应               | 48.55               | 22.44              |
| SD\_CLK     | SD 卡时钟引脚               | 60.95               | 18.45              |
| SD\_CMD     | SD 卡命令引脚               | 58.2                | 16.42              |
| SD\_DAT0    | SD 数据引脚                 | 58.13               | 20.42              |
| SD\_DAT1    | SD 数据引脚                 | 60.65               | 21.1               |
| SD\_DAT2    | SD 数据引脚                 | 57.78               | 13.57              |
| SD\_DAT3    | SD 数据引脚                 | 60.8                | 15.22              |
| BT\_ON      | 蓝牙电源状态                | 25.13               | 19.55              |
| WL\_ON      | 无线局域网电源状态          | 27.7                | 19.2               |

### 树莓派 Zero W

* [电路图，修订版 1.1](https://datasheets.raspberrypi.com/rpizero/raspberry-pi-zero-w-reduced-schematics.pdf)
* [机械图纸，PDF](https://datasheets.raspberrypi.com/rpizero/raspberry-pi-zero-w-mechanical-drawing.pdf)

### 树莓派 Zero

* [原理图，修订版 1.3](https://datasheets.raspberrypi.com/rpizero/raspberry-pi-zero-reduced-schematics.pdf)
* [机械图纸，PDF](https://datasheets.raspberrypi.com/rpizero/raspberry-pi-zero-mechanical-drawing.pdf)
* [外壳图纸，PDF - 空白盖](https://datasheets.raspberrypi.com/case/raspberry-pi-zero-case-mechanical-drawing.pdf)
* [外壳图纸，PDF - GPIO 盖](https://datasheets.raspberrypi.com/case/raspberry-pi-zero-case-with-gpio-mechanical-drawing.pdf)
* [外壳图纸，PDF - 相机盖](https://datasheets.raspberrypi.com/case/raspberry-pi-zero-case-with-camera-mechanical-drawing.pdf)

## 产品合规性和安全性

所有树莓派产品均通过了大量的合规测试。有关更多信息，请参阅产品信息网站。

### 阻燃等级

树莓派设备中使用的 PCB 符合 UL94-V0 标准。

>**注意**
>
>仅适用于 PCB。

### 树莓派合规支持

依据树莓派在合规测试期间的实际测试情况，合规支持计划的目标是消除合规问题导航的负担，为公司更轻松地将新产品推向消费者提供支持。它为用户提供了与 UL 公司的专门团队联系的机会，他们借助对树莓派的深入了解，评估和测试用户的产品。

了解更多关于树莓派合规支持计划的信息。

### 由树莓派提供支持

由树莓派提供支持的 Powered by 树莓派 计划，为希望使用树莓派 logo 形式的公司提供了一个流程，涵盖了搭载树莓派计算机、芯片的产品，以及由树莓派提供的服务。如果你希望开始申请流程，可以在线操作。

### 已审批的设计合作伙伴

我们的已审批设计合作伙伴名单提供了一组我们密切合作并支持的咨询公司，使它们能够在硬件、软件和机械领域提供付费设计服务。

## 频率管理和发热控制

所有型号的树莓派在重负荷情况下，都会进行一定程度的发热管理，以避免过热。SoC 内部有温度传感器，GPU 上的软件会轮询以确保温度不超过我们定义的上限，所有型号均为 85°C。可以将此值设定为更低的数值，但不能设置为更高。当设备接近极限时，芯片（Arm，GPU）上使用的各种频率和有时电压会降低。这会减少产生的热量，保持温度控制在一定范围内。

当核心温度在 80°C 和 85°C 之间时，Arm 核心将逐渐降频。如果温度达到 85°C，那么 Arm 核心和 GPU 都将开始降频。

树莓派 3 B+ 采用了新的 PCB 技术，以提供更好的散热性能和增加热量质量。此外，引入了软温度限制，旨在最大化延长设备在达到硬限制 85°C 之前的 "冲刺" 时间。当达到软限制时，时钟速度从 1.4GHz 降至 1.2GHz，并略微降低操作电压。这减缓了温度升高的速度：我们以短暂的 1.4GHz 时间换取了更长时间的 1.2GHz 运行。默认情况下，软限制为 60°C，可以通过 config.txt 中的 temp_soft_limit 参数进行更改。

树莓派 4 B 继续采用与树莓派 3 B+ 相同的 PCB 技术，以帮助散热。目前尚未进行软限制。

### 使用 DVFS

>**注意**
>
>仅适用于树莓派 4 B、400，计算模块 4 的 DVFS 讨论。

树莓派 4 实现了动态电压和频率调节（DVFS）。这种技术使得树莓派 4 设备能在保持性能不变的同时降低运行温度。

固件会监控 SoC 内部的各种时钟（例如 Arm、Core、V3D、ISP、H264、HEVC），当它们未全速运行时，供给给这些时钟驱动的芯片部分的电压，将相比全速时有所减少。事实上，只提供一定的电压就足以确保其以特定运行水准正常运行。这可以显著降低 SoC 的功耗，从而了减少产生的总发热量。

由于可能引发系统稳定性问题，特别是在使用电压降低固定时钟外设（例如 PCIe）时，存在潜在的系统稳定性问题，有三种 DVFS 模式，可在 /boot/firmware/config.txt 中配置，具有以下特性。大多数系统应该使用 dvfs=3，不带显示的设备可能会因为较小的功耗降低而从 dvfs=1 中受益，但会面临 PCIe 稳定性问题的风险。

| 属性=值 | 描述                                                                                                                 |
| --------- | ---------------------------------------------------------------------------------------------------------------------- |
| `dvfs=1`        | 允许欠压                                                                                                             |
| `dvfs=2`        | 固定默认操作频率的电压                                                                                               |
| `dvfs=3`        | 根据需求增加超频电压（默认）。如果在 config.txt 中指定了 over_voltage，则会禁用动态电压调节，使设备退回 dvfs=2。|

>**注意**
>
>该参数已在树莓派 5 上移除，并将处于模式 3。

此外，还使用了更细粒度的 CPU 调度器，用来更精细地控制 ARM 核频率，这意味着 DVFS 更有用。现在的步进频率为 1500MHz、1000MHz、750MHz 和 600MHz。这些步进可以在 SoC 限流时有益，意味着几乎不会完全降至 600MHz，从而大大提高了全负载时的性能。

默认的 CPU 调度器是 ondemand。可以使用 cpufrequtils 软件包中的 cpufreq-set 命令手动更改调度器以减少空闲功耗：

```
$ sudo apt install cpufrequtils
$ sudo cpufreq-set -g powersave
```

### 测量温度

由于树莓派设备使用的 SoC 架构，如果在树莓派系统发行版中使用上游温度监控代码（如基于 Linux 的温度测量）可能不准确。但是，vcgencmd 命令能够提供准确且即时的 SoC 温度的实时数值，因为它直接与 GPU 通信：

```
$ vcgencmd measure_temp
```

### 添加散热片

由于内置限流功能，不用散热片也不会造成 SoC 过热损坏。不过，安装散热片和小型风扇可以缓解发热限流并提高性能。要获得最佳气流，并略微改善散热效果，可考虑将树莓派竖着放。

### 风扇套件

树莓派 5 有两款官方风扇可选，用于辅助散热：

* [主动散热器](https://www.raspberrypi.com/products/active-cooler/)
* [用于树莓派 5 的外壳](https://www.raspberrypi.com/products/raspberry-pi-5-case/)

这两款均应插入至主板右上方的风扇连接器（四针 JST-SH PWM），位于 40 针 GPIO 母座和 USB 2 之间。风扇连接器与 USB 外围设备一同受电流限额。我们为超频用户使用主动散热器外壳，因为它有更好的散热能力。

以上两种可选官方配件都由树莓派固件主动管理。随着树莓派的温度升高，风扇的反应如下：

* 在 50°C 以下，风扇不会转动（0% 速度）
* 在 50°C 时，风扇缓慢转动（30% 速度）
* 在 60°C 时，风扇转速提高至中速（50% 速度）
* 在 67.5°C 时，风扇转速提高至高速（70% 速度）
* 在 75°C 时，风扇转速达到全速（100% 速度）

温度下降时，应用相同的行为，并有 5°C 的滞后性；当温度下降到低于上述每个阈值 5°C 时，风扇速度才会降低。

启动时，风扇自动运转，以查看转速控制，并看风扇是否在旋转。如果可以，则启用 cooling_fan 设备树驱动。默认情况下，该驱动位于 bcm2712-rpi-5-b.dtb，但可以通过 status=disabled 进行修改。

#### 风扇连接器引脚图

风扇连接器是一个 1 mm 间距的 JST-SH 插座，包含以下四个引脚：

| 引脚 | 功能 | 电线颜色 |
| ------ | ------ | ---------- |
| 1    | +5V  | 红     |
| 2    | PWM  | 蓝     |
| 3    | GND  | 黑     |
| 4    | Tach | 黄     |

### 树莓派启动 EEPROM

树莓派 5、树莓派 4、400、计算模块 4 和计算模块 4S 计算机使用 EEPROM 启动系统。其他型号的树莓派 计算机使用位于启动文件系统中的 bootcode.bin 文件。

>**注意**
>
>在 rpi-eeprom GitHub 存储库中，你可以找到用于创建 rpi-eeprom 的脚本和预编译的二进制文件。

### 引导诊断

如果在引导过程中出现错误，则会通过绿色的 LED 灯传递故障信息。更新版本的引导加载程序将在 HDMI 显示器上显示诊断消息。

### 更新引导程序

有很多方法可以对你树莓派的引导程序进行更新。

#### 树莓派 5、树莓派 4 和树莓派 400

树莓派操作系统会自动更新引导加载程序来进行重要的错误修复。要手动更新引导加载程序或更改启动顺序，请使用 raspi-config。

#### 使用树莓派启动盘制作工具来更新引导加载程序

树莓派启动盘制作器提供了一个图形界面，用于更新引导加载程序并选择引导模式。

1. 下载树莓派启动盘制作工具
2. 选择一个未使用的 SD 卡（引导加载程序镜像会格式化整个卡）
3. 启动树莓派镜像制作工具
4. 选择 Choose OS
5. 选择 Misc utility images ![Select Misc utility images](https://www.raspberrypi.com/documentation/computers/images/misc-utility-images.png?hash=662b949f2e370649419c8efc7fc522f4)
6. 为你的树莓派选择 Bootloader (Pi 400 是 4 系列的一部分)![Choose a family for your bootloader](https://www.raspberrypi.com/documentation/computers/images/bootloader-family-select.png?hash=26cda00ff3f46580eac44af916437614)
7. 选择引导模式： SD （推荐），USB 或 Network ![Choose the storage from which you’d like to boot](https://www.raspberrypi.com/documentation/computers/images/bootloader-storage-select.png?hash=08b572c18e189ab4dd7688838fc0a97b)
8. 选择 SD card 然后 Write
9. 单击 Yes 继续
10. 使用新的镜像引导树莓派，并等待至少十秒钟
11. 当绿色活动指示有规律的闪烁，HDMI 显示器绿屏时，你已成功写入引导程序了
12. 断开树莓派的电源并拔出 SD 卡

#### 使用 raspi-config 来更新引导加载程序

要从树莓派系统内部更改启动模式或引导加载程序版本，请运行 raspi-config。

1. 升级树莓派系统以获取 rpi-eeprom 软件包的最新版本。
2. 运行 sudo raspi-config。
3. 选择 Advanced Options。
4. 选择 Bootloader Version。
5. 选择 Default 可恢复出厂设置、选择 Latest 可获取最新发布的引导程序。
6. 使用 sudo reboot 重启。

### 更新引导程序配置

引导加载程序的 default 版本代表最新的出厂默认固件镜像。它提供了关键的错误修复、硬件支持，并且特性均在 latest 版本中经过测试，然后定期更新。latest 引导加载程序更频繁地更新，以包含最新的修复和改进。

专业用户可以切换到 latest 引导加载程序以获得最新功能。

运行以下命令以启动 raspi-config。

```
$ sudo raspi-config
```

转到 Advanced Options，然后选择 Bootloader Version。选择 Latest 并选择 Yes 确认。选择 Finish 并确认要重启。重启后，再次打开命令提示符并更新你的系统：

```
$ sudo apt update
```

如果运行 sudo rpi-eeprom-update，你会看到引导加载程序的更新版本是 latest 发布。

```
*** UPDATE AVAILABLE ***
BOOTLOADER: update available
   CURRENT: Thu 18 Jan 13:59:23 UTC 2024 (1705586363)
    LATEST: Mon 22 Jan 10:41:21 UTC 2024 (1705920081)
   RELEASE: latest (/lib/firmware/raspberrypi/bootloader-2711/latest)
            Use raspi-config to change the release.

  VL805_FW: Using bootloader EEPROM
     VL805: up to date
   CURRENT: 000138c0
    LATEST: 000138c0
```

现在你可以更新你的引导加载程序。

```
$ sudo rpi-eeprom-update -a
$ sudo reboot
```

重启，然后运行 sudo rpi-eeprom-update。现在你应该看到 CURRENT 日期已更新为引导程序的最新版本。

```
BOOTLOADER: up to date
   CURRENT: Mon 22 Jan 10:41:21 UTC 2024 (1705920081)
    LATEST: Mon 22 Jan 10:41:21 UTC 2024 (1705920081)
   RELEASE: latest (/lib/firmware/raspberrypi/bootloader-2711/latest)
            Use raspi-config to change the release.

  VL805_FW: Using bootloader EEPROM
     VL805: up to date
   CURRENT: 000138c0
    LATEST: 000138c0
```

#### 阅读当前引导程序配置

要查看当前运行引导程序使用的配置，请运行以下命令：

```
$ rpi-eeprom-config
```

#### 从引导加载程序镜像中读取配置

要从引导加载程序镜像中读取配置：

```
$ rpi-eeprom-config pieeprom.bin
```

#### 编辑当前的引导加载程序配置

执行以下命令以将当前引导加载程序配置加载到文本编辑器中。当编辑器关闭时，rpi-eeprom-config 将更新后的配置应用于最新的可用引导加载程序版本，并使用 rpi-eeprom-update 在系统重启时安排更新：

```
$ sudo -E rpi-eeprom-config --edit
$ sudo reboot
```

如果更新后的配置与原配置相同或为空，则不会进行任何更改。

编辑器由环境变量 EDITOR 决定。

#### 应用已保存的配置

以下命令将 boot.conf 应用于最新的可用引导加载程序镜像，并使用 rpi-eeprom-update 安排在系统重启时更新。

```
$ sudo rpi-eeprom-config --apply boot.conf
$ sudo reboot
```

### 自动更新

rpi-eeprom-update systemd 服务在启动时运行，并在新镜像可用时应用更新，自动迁移当前的引导加载程序配置。

要禁用自动更新：

```
$ sudo systemctl mask rpi-eeprom-update
```

要重新启用自动更新：

```
$ sudo systemctl unmask rpi-eeprom-update
```

>**注意**
>
>如果设置了 FREEZEVERSION 引导加载程序配置，则更新服务将跳过任何自动更新。这样可以避免在安装了多个操作系统或更换 SD 卡时逐个禁用更新服务的需要。

#### `rpi-eeprom-update`

树莓派操作系统使用 rpi-eeprom-update 脚本实现自动更新服务。该脚本还可以以交互方式运行或进行封装，创建定制的引导加载程序更新服务。

读取当前引导加载程序版本：

```
$ vcgencmd bootloader_version
```

检查是否有可用更新：

```
$ sudo rpi-eeprom-update
```

 安装更新：

```
$ sudo rpi-eeprom-update -a
$ sudo reboot
```

取消待定更新：

```
$ sudo rpi-eeprom-update -r
```

安装特定的引导程序镜像:

```
$ sudo rpi-eeprom-update -d -f pieeprom.bin
```

-d 参数指示 rpi-eeprom-update 使用指定的镜像文件中的配置，而不是自动迁移当前的配置。

显示内置文档:

```
$ rpi-eeprom-update -h
```

### 引导加载程序发布状态

固件发布状态对应于引导加载程序固件镜像的特定子目录（ /lib/firmware/raspberrypi/bootloader/... ），可以更改以选择不同的发行版本。

* default -用于支持新硬件、关键错误修复，并通过在 latest 版本测试过的新功能的定期更新。
* latest - 当新功能可用时进行更新

由于发布状态字符串只是一个子目录名称，因此可以创建自己的发布版本，例如固定发布或自定义网络引导配置。

#### 更改启动加载程序版本

>**注意**
>
>你可以通过编辑 /etc/default/rpi-eeprom-update 文件并将 FIRMWARE_RELEASE_STATUS 条目更改为适当的流来更改在更新过程中使用的发布版本。

#### 更新启动加载器配置文件中的启动加载器镜像

以下命令将 pieeprom.bin 中的启动加载器配置替换为 boot.conf 并将新镜像写入 new.bin ：

```
$ rpi-eeprom-config --config boot.conf --out new.bin pieeprom.bin
```

#### `recovery.bin`

在开机时，BCM2711、BCM2712 上的 ROM 会在 SD 卡的启动分区的根目录中查找文件 recovery.bin。如果能找到一个有效的 recovery.bin，那么 ROM 就会执行这个文件，而不是读取 EEPROM。该机制可以确保始终能对引导加载程序闪存恢复出厂设置。

欲了解更多信息，请参阅 EEPROM 启动流程。

#### 引导加载程序更新文件

| 文件名 | 目的                                                                    |
| -------- | ------------------------------------------------------------------------- |
| `recovery.bin`       | 引导加载程序恢复可执行文件                                              |
| `pieeprom.upd`       | 引导程序 EEPROM 镜像                                                    |
| `pieeprom.bin`       | 引导程序 EEPROM 镜像 - 与 pieeprom.upd 相同，但更改 recovery.bin 的行为 |
| `pieeprom.sig`       | 引导程序镜像的 sha256 校验和（pieeprom.upd/pieeprom.bin）               |
| `vl805.bin`       | VLI805 USB 固件 EEPROM 镜像 - 仅适用于树莓派 4B 修订版 1.3 及更老版本。|
| `vl805.sig`       | vl805.bin 的 sha256 校验和                                              |

* 如果引导加载程序更新镜像为 pieeprom.upd，则更新完成后 recovery.bin 会被重命名为 recovery.000，然后系统会重启。由于检测不到 recovery.bin，ROM 将从 SPI 闪存加载新更新的引导加载程序，然后正常启动操作系统。
* 如果引导加载程序更新镜像为 pieeprom.bin，那么更新完成后 recovery.bin 将。如更新成功，HDMI 显示绿屏，绿色状态 LED 快速闪烁；如果更新失败，HDMI 显示红屏，并且通过状态 LED 传递错误代码。
* .sig 文件包含了相应镜像文件的十六进制 sha256 校验和；将来可能会添加其他字段。
* 在 BCM2711、BCM2712 上的 ROM 查找 recovery.bin 的功能，不能放在 USB 大容量存储设备及 TFTP 中。而且，更新版本的引导加载程序已支持自更新功能，使引导加载程序能够自己重新刷新 SPI 闪存。请参阅引导加载程序配置页面上的 ENABLE_SELF_UPDATE。
* EEPROM 更新的临时文件会在启动时由 rpi-eeprom-update 服务自动删除。

若要获取有关 rpi-eeprom-update 配置文件的更多信息，请参阅 rpi-eeprom-update -h。

#### EEPROM 写保护

引导加载程序和 VLI EEPROM 都支持硬件写保护。有关如何在更新 EEPROM 时启用此功能的更多信息，请参阅 eeprom_write_protect 选项。

## 树莓派 4 的启动诊断

从树莓派 4 引导加载程序的 2020-04-16 版本开始，诊断信息会出现在 HDMI 显示器上。要查看诊断信息，请关机树莓派 4，移除 SD 卡，然后重启。在连接的显示器上应该会出现类似如下的诊断显示。

![Boot diagnostics screen](https://www.raspberrypi.com/documentation/computers/images/bootloader-diagnostics.png?hash=474195e522544fb421403622e269ab1b)

该诊断页面也会出现在以下情况：引导加载程序无法引导插入的 SD 卡、无法进行网络引导；比如：SD 卡中没有可引导的镜像、卡是假冒伪劣产品、网络引导参数错误。

一旦显示了诊断页面，就只能通过重新插拔设备电源（即拔掉然后重新插上电源）重启。

诊断页面最上面的一行说明了树莓派型号、内存容量。二维码是指向下载页面的链接。

诊断信息如下：

| 行 | 信息                                                                                                                    |
| ---- | ------------------------------------------------------------------------------------------------------------------------- |
| `bootloader`   | 引导加载程序 git 版本 - RO（如果 EEPROM 受写保护） - 软件构建日期                                                       |
| `update-ts`   | 更新 EEPROM 配置的时间戳。在自更新模式下检查此时间戳，以避免更新到旧配置。                                    |
| `secure-boot`   | 如果启用了安全启动，则显示处理器版本（B0/C0）和签名启动状态参数。否则，此行为空。                             |
| `board`   | 主板版本 - 序列号 - 以太网 MAC 地址                                                                                     |
| `boot`   | 模式（当前启动模式名称和编号）顺序（BOOT ORDER 配置）尝试（当前启动模式的重试次数）重启（通过启动模式列表的循环次数）。|
| `SD`   | SD 卡检测状态（已检测/未检测）。                                                                              |
| `part`   | 主引导记录主分区类型:LBA.                                                                                               |
| `fw`   | 如果存在，则 start.elf 和 fixup.dat 的文件名 (例如 start4x.elf，fixup4x.dat ).                                         |
| `net`   | 网络引导: 链路状态（上/下），客户端 IP 地址（ip），子网（sn），默认网关（gw）                                           |
| `tftp`   | 网络引导：TFTP 服务器 IP 地址                                                                                           |
| `display`   | 指示是否检测到热插拔（ HPD=1 ），以及每个 HDMI 输出是否成功读取 EDID（ EDID=ok ）。                           |

可以使用 DISABLE_HDMI 参数禁用此显示器，请参阅引导加载程序配置。

>**注意**
>
>该功能仅用于诊断引导故障；它并不是可交互的引导程序。如果你需要交互式引导程序，请考虑使用类似 U-Boot 的工具。

## 树莓派引导模式

树莓派有许多不同的引导阶段。本文档解释了引导模式的工作原理，以及哪些引导模式支持 Linux 引导。

### 特殊 bootcode.bin 专用启动模式

基于 BCM2837 的树莓派可以从 USB 设备和以太网引导 - 也就是说，树莓派 2B v1.2，树莓派 3B 和树莓派 3B+（由于树莓派 3A+ 没有内置以太网接口，无法进行网络引导）。此外，所有早于 树莓派 4 的 树莓派 型号可以使用仅 bootcode.bin 方法启用 USB 设备引导。

>**注意**
>
>自树莓派 4 以降，旗舰级设备不再使用文件 bootcode.bin。因为这些设备使用板载 EEPROM 芯片中的引导加载程序。更多信息，请参阅 EEPROM 引导流程和 SPI 引导 EEPROM 的文档。

格式化 SD 卡为 FAT32，把最新的 bootcode.bin 复制到里面。把 SD 卡插入到树莓派中。从 SD 卡加载 bootcode.bin 以后，树莓派就能使用 USB 主机模式启动了。

这对于基于 BCM2835、BCM2836 芯片的树莓派 1、2 和 Zero 型号非常有用，在树莓派 3 无法启动的情况下（与烧录到 BCM2837A0 中的启动代码相比，最新的 bootcode.bin 为树莓派 3B 提供了额外的错误修复）。

如果即使使用了这个 bootcode.bin，你的大容量存储设备还是无法使用，请在 SD 卡上新建一个名为“timeout”的文件。这将使其等待大容量存储设备初始化的时间延长至 6 秒。

### bootcode.bin 启用 UART

>**注意**
>
>适用于在树莓派 4 发布前的开发板。

有关使用 EEPROM 引导加载程序启用 UART 的信息，请参阅引导加载程序配置文档。

可以启用早期阶段的 UART 来调试引导问题（与上述 bootcode.bin 仅引导模式非常有用）。要做到这一点，请确保你的固件版本是新的（包括 bootcode.bin ）。要检查当前固件是否支持 UART：

```
$ strings bootcode.bin | grep BOOT_UART
```

要从 bootcode.bin 启用 UART：

```
$ sed -i -e "s/BOOT_UART=0/BOOT_UART=1/" bootcode.bin
```

接下来，将合适的 USB 串行电缆连接到计算机（尽管你可能会发现，最简单的方法就是使用 USB 串行电缆，因为它可以在无需设置烦人的 config.txt 的情况下直接使用树莓派）。在树莓派或计算模块上使用独立的引脚 6、8 和 10（GND、GPIO14、GPIO15）。

然后在 Linux 或 macOS 上使用 screen，或者在 Windows 上使用 putty 来连接到串口。

设置串口接收速率为 115200-8-N-1，然后启动你的树莓派。你应该可即时从设备上获得 bootcode.bin 的串行输出。

## USB 启动模式

U 盘有两种独立的启动模式:

* USB 设备启动
* USB 主机启动

固件会根据 OTP 位在引导时选择两种模式中的一种。用两位控制 USB 引导。第一位启用 USB 设备引导，为默认设置；第二位启用 USB 主机引导。

如果设置了 USB 主机引导模式位，则处理器会读取 OTGID 引脚来决定是作为主机引导（驱动到零，就像在任何树莓派 A/B+ 上一样）还是作为设备引导（保持漂浮）。树莓派 Zero 通过 USB 连接器可以访问 OTGID 引脚；计算模块可以通过边缘连接器访问 OTGID 引脚。

其他一些 OTP 位可允许某些 GPIO 引脚选择引导模式。

### U 盘设备引导模式

>**注意**
>
>U 盘引导可用于旗舰级的计算模块系列，Zero 系列和衍生的 A 款。

当启用此引导模式（通常在无法从 SD 卡引导后），树莓派 将其置为 USB 设备模式，等待主机发送的 USB 重置。在 Github 上可以找到示例代码，展示主机需如何与树莓派进行通信。

主机首先通过控制端点 0 向设备发送一个结构。这包含了启动的大小和签名（安全未启用，因此不需要签名）。其次，代码通过端点 1 传输（ bootcode.bin ）。最后，设备将用以下代码之一回复：

* 0 - 成功
* 0x80 - 失败

### USB 主机引导模式

>**注意**
>
>自树莓派计算模组 3、Zero 系列 2 W、树莓派 2B（1.2 版）、树莓派 3B 以及自树莓派 3B+ 以来，主机引导功能可在计算模块系列和所有旗舰系列设备上使用。树莓派 3A+ 支持大容量存储引导，但不支持网络引导。

USB 主机引导模式采用以下逻辑:

1. 启用 USB 接口 并等待 D+ 线拉高，表示连接了 USB 2.0 设备（我们只支持 USB2.0）
2. 如果设备是一个集线器：
    1. 启用所有集线器的下游接口的电源
    2. 对于每个 port，循环最多两秒（如果 program_usb_boot_timeout=1 已设置，则为五秒）
        1. 释放复位并等待 D+被拉高以指示设备已连接
        2. 如果检测到设备：
            1. 发送“获取设备描述符”
                1. 如果 VID == SMSC 并且 PID == 9500
                    1. 将设备添加到以太网设备列表
            2. 如果类接口是大容量存储类
                1. 将设备添加到大容量存储设备列表
3. 否则
    1. 枚举单个设备
4. 浏览大容量存储设备列表
    1. 从大容量存储设备启动
5. 浏览以太网设备列表
    1. 从以太网引导

在树莓派 3B，3A+ 和 3B+ 上，默认禁用主机引导。要启用 USB 主机引导，请将 program_usb_boot_mode=1 这一行添加到 /boot/firmware/config.txt 的末尾。

>**警告**
>
>任何对 OTP 的修改都是永久性的，无法撤销。
。
>在树莓派 3A+ 上，将 OTP 位设置为启用 USB 主机引导模式将永久性地阻碍其以 USB 设备模式启动。

## USB 大容量存储引导

>**注意**
>
>自计算模块 3 起，Zero 2 W 起的 Zero 系列，以及自树莓派 2B（版本 1.2）起的所有旗舰系列设备均可使用。

USB 大容量存储启动能让你从 USB 大容量存储设备（如闪存驱动器、USB 磁盘）启动 Raspberry Pi。连接 USB 设备时（尤其是硬盘和 SSD），需要注意它们的功耗要求。接入多个磁盘通常需要额外的外部电源，可以是带电源的硬盘盒、带供电的 USB 集线器。

>**注意**
>
>树莓派 4B 之前的型号存在已知问题，可能导致无法从某些 USB 设备启动。

### 带有 EEPROM 引导加载程序的设备

树莓派 4 和更新款的旗舰系列设备以及自计算模块 4 和 4S 起，支持默认情况下的 USB 引导，只要在 BOOT_ORDER 配置中指定 USB 引导。

>**注意**
>
>早期版本的树莓派 4 可能需要更新引导加载程序才能从 USB 启动。

>**注意**
>
>计算模块 4 的早期版本可能需要更新引导加载程序才能从 USB 启动。

### 树莓派 3B+

树莓派 3B+ 支持开箱即用的 USB 大容量存储启动。

### 树莓派 2B，3A+，3B，CM3，CM3+，Zero 2 W

在树莓派 2B v1.2，3A+，3B，Zero 2 W 和计算模块 3 和 3+ 上，必须先启用 USB 主机启动模式。才能从 USB 大容量存储启动和网络启动。

>**注意**
>
>树莓派 3A+ 和 Zero 2 W 不支持网络启动。
要启用这些设备的 USB 主机启动模式，请在 OTP（一次可编程）内存中设置 USB 主机位。要设置该位，请从包含以下行的 SD 卡引导 /boot/firmware/config.txt。设置该位后，你可以在没有 SD 卡的情况下从 USB 启动。

#### 使用 OTP 启用 USB 主机启动模式

>**警告**
>
>对 OTP（一次可编程）内存所做的任何修改都是永久性的，无法撤销。
。
>在树莓派 3A+ 上，设置 OTP 位来启用 USB 主机启动模式将永久阻碍该树莓派以 USB 设备模式启动。

使用安装了树莓派系统的 SD 卡来编程 OTP 位。

要启用 USB 主机启动模式，请将以下行添加到 config.txt 中：

```
program_usb_boot_mode=1
```

然后使用 sudo reboot 重启你的 Raspberry Pi。要检查 OTP 是否已正确编程，请运行以下命令：

```
$ vcgencmd otp_dump | grep 17:
17:3020000a
```

如果输出显示 0x3020000a，则 OTP 已成功编程。如果看到不同的输出，请再次尝试编程过程。确保 config.txt 末尾没有空行。

你现在可以像从 SD 卡引导一样从 USB 大容量存储设备引导。有关更多信息，请参阅以下部分。

### 从 U 盘启动

过程与 SD 卡相同 - 把操作系统镜像写入 U 盘存储设备。

存储设备准备就绪后，连接驱动器并启动 Raspberry Pi，需注意外部驱动器的额外 USB 电源需求。

大约五到十秒后，树莓派 应该开始启动了。如果连接的显示器上出现彩虹屏。请确定未将 SD 卡插入树莓派，因为如果插入了 SD 卡，树莓派将优先从 SD 卡启动。

查看引导模式文档可了解引导顺序和备选引导模式（网络、USB 设备、GPIO 或 SD 卡启动）。

### 已知问题

* 检查可引导 USB 设备的默认超时时间为两秒。某些闪存驱动器和硬盘启动速度过慢。可以将此超时时间延长到五秒（需在 SD 卡中新建文件 timeout），但要注意某些设备可能需要更长时间来响应。
* 某些闪存驱动器采用了非常罕见的协议，引导码无法处理，因此造成不兼容。

### 特殊 bootcode.bin -仅引导模式

对于树莓派 2B v1.2、3A+、3B 和 3B+，如果你无法使用特定的 USB 设备来启动，你可以使用 bootcode.bin 专用启动模式。树莓派 仍会从 SD 卡启动，但只会从 SD 卡中读取 bootcode.bin；你操作系统的其余部分仍存储于 USB 设备。

### 硬件兼容性

在从 USB 大容量存储设备启动之前，请验证该设备在 Linux 下是否正常工作。使用 SD 卡引导，插入 USB 大容量存储设备。USB 设备应显示为可移动驱动器。这在使用 USB SATA 转换设备时尤其重要，该适配器可能由引导加载程序支持大容量存储模式，但如果 Linux 选择 USB 附加 SCSI-UAS 模式，则有概率不兼容。

使用硬盘驱动器（HDD）通常需要带供电的 USB 集线器。即使一切看起来正常，如果 USB 集线器没带电源，你可能会遇到间歇性故障。

### 多个可引导驱动器

在搜索可引导分区时，引导加载程序会同时扫描所有 USB 大容量存储设备，并选择首个响应的设备。如果引导分区没有找到合适的 start.elf 文件，则引导加载程序将尝试下一个可用设备。没有根据 USB 拓扑结构指定引导设备的方法；这减缓引导速度并带来不必要的配置复杂性。

>**注意**
>
>可使用 config.txt 文件条件过滤器来选择复杂设备配置中的备用固件。

## 网络引导

本节描述了树莓派 3B、3B+ 和 2B v1.2 上的网络引导工作原理。

在树莓派 4 和树莓派 5 上，网络引导是在 EEPROM 中的第二阶段引导加载程序中实现的。更多信息，请参阅树莓派 4 引导加载程序配置。

我们还有关于设置网络引导系统的教程。

仅适用于上述型号树莓派中内置的有线适配器进行网络引导。无线局域网引导不受支持，也不支持从其他有线网络设备引导。

### 网络引导流程

要进行网络引导，引导 ROM 执行以下操作：

* 初始化板载以太网设备（Microchip LAN9500 或 LAN7500）
* 发送 DHCP 请求（使用厂商类别标识符 DHCP 选项 60 设置为 PXEClient:Arch:00000:UNDI:002001 )
* 接收 DHCP 回复
* （可选）接收 DHCP 代理回复
* ARP 到 tftpboot 服务器
* ARP 回复包含 tftpboot 服务器以太网地址
* TFTP RRQ `bootcode.bin`
  * 服务器响应 TFTP 错误响应，并附带文本错误消息，文件未找到
  * 服务器会回复包含文件头部块编号的数据块（512 B）中的第一个块，文件已存在
    * 树莓派回复 TFTP ACK 数据包，包含块编号，并重复直到最后一个非 512 B 块
* TFTP RRQ bootsig.bin 下载请求
  * 这通常会产生错误 file not found。这是预料之中的，TFTP 引导服务器应该能够处理它。

从此刻开始，bootcode.bin 代码继续加载系统。它将尝试访问的第一个文件是 <serial_number>/start.elf。如果这不会导致错误，那么要读取的其他文件将会在前面加上 serial_number。这很有用，因为它使你能够为你的 Raspberry Pis 创建具有不同 start.elf /内核的独立目录。

要获取设备的序列号，你可以尝试使用这种引导模式，并查看使用 tcpdump / wireshark 访问的文件，或者你可以运行标准的树莓派系统 SD 卡和 cat /proc/cpuinfo。

如果你将所有文件放入 TFTP 目录的根目录中，那么随后所有的文件都将从那里访问。

### 调试网络引导模式

首先要检查的是 OTP 位是否被正确编程。为此，你需要将 program_usb_boot_mode=1 添加到 config.txt，然后重启（使用可以正确引导到树莓派系统的标准 SD 卡）。完成后，你应该可以执行以下操作：

```
$ vcgencmd otp_dump | grep 17:
```

如果第 17 行包含 3020000a，则 OTP 已正确编程。现在，你可以拔掉 SD 卡，插入以太网了，然后在树莓派上电约 5 秒后，以太网指示灯应该被点亮。

要在服务器上捕获以太网数据包，请在 tftpboot 服务器上（如果未使用，则在 DHCP 服务器上）使用 tcpdump。否则，你将无法看到发送的数据包，因为网络交换机不是集线器！

```
$ sudo tcpdump -i eth0 -w dump.pcap
```

将从 eth0 写入文件 dump.pcap 中的所有内容。然后，你可以对数据包进行后处理或上传到 cloudshark 进行通信。

#### DHCP 请求/响应

至少你应该看到一个类似以下内容的 DHCP 请求和回复：

```
6:44:38.717115 IP (tos 0x0, ttl 128, id 0, offset 0, flags [none], proto UDP (17), length 348)
    0.0.0.0.68 > 255.255.255.255.67: [no cksum] BOOTP/DHCP, Request from b8:27:eb:28:f6:6d, length 320, xid 0x26f30339, Flags [none] (0x0000)
	  Client-Ethernet-Address b8:27:eb:28:f6:6d
	  Vendor-rfc1048 Extensions
	    Magic Cookie 0x63825363
	    DHCP-Message Option 53, length 1: Discover
	    Parameter-Request Option 55, length 12:
	      Vendor-Option, Vendor-Class, BF, Option 128
	      Option 129, Option 130, Option 131, Option 132
	      Option 133, Option 134, Option 135, TFTP
	    ARCH Option 93, length 2: 0
	    NDI Option 94, length 3: 1.2.1
	    GUID Option 97, length 17: 0.68.68.68.68.68.68.68.68.68.68.68.68.68.68.68.68
	    Vendor-Class Option 60, length 32: "PXEClient:Arch:00000:UNDI:002001"
	    END Option 255, length 0
16:44:41.224619 IP (tos 0x0, ttl 64, id 57713, offset 0, flags [none], proto UDP (17), length 372)
    192.168.1.1.67 > 192.168.1.139.68: [udp sum ok] BOOTP/DHCP, Reply, length 344, xid 0x26f30339, Flags [none] (0x0000)
	  Your-IP 192.168.1.139
	  Server-IP 192.168.1.1
	  Client-Ethernet-Address b8:27:eb:28:f6:6d
	  Vendor-rfc1048 Extensions
	    Magic Cookie 0x63825363
	    DHCP-Message Option 53, length 1: Offer
	    Server-ID Option 54, length 4: 192.168.1.1
	    Lease-Time Option 51, length 4: 43200
	    RN Option 58, length 4: 21600
	    RB Option 59, length 4: 37800
	    Subnet-Mask Option 1, length 4: 255.255.255.0
	    BR Option 28, length 4: 192.168.1.255
	    Vendor-Class Option 60, length 9: "PXEClient"
	    GUID Option 97, length 17: 0.68.68.68.68.68.68.68.68.68.68.68.68.68.68.68.68
	    Vendor-Option Option 43, length 32: 6.1.3.10.4.0.80.88.69.9.20.0.0.17.82.97.115.112.98.101.114.114.121.32.80.105.32.66.111.111.116.255
	    END Option 255, length 0
```

Vendor-Option Option 43 包含了回复的重要部分。这个部分必须包含字符串"树莓派 Boot"。由于引导 ROM 中的一个错误，你可能需要在字符串末尾添加三个空格。

#### TFTP 文件读取

当供应商参数被正确指定时，你将看到随后发送的 TFTP RRQ 数据包。RRQ 可以通过第一个数据块或错误消息来回复，表明文件未找到。在少数情况下，他们甚至会收到第一个数据包，然后由 树莓派 中止传输（当检查文件是否存在时会发生这种情况）。下面的示例仅包括三个数据包：原始读取请求、第一个数据块（始终是包含一个标头和 512 B 数据的 516 B，尽管最后一个块始终少于 512 B 且可能为零长度），以及第三个数据包（包含与数据块中帧编号匹配的确认帧号）。

```
16:44:41.224964 IP (tos 0x0, ttl 128, id 0, offset 0, flags [none], proto UDP (17), length 49)
    192.168.1.139.49152 > 192.168.1.1.69: [no cksum]  21 RRQ "bootcode.bin" octet
16:44:41.227223 IP (tos 0x0, ttl 64, id 57714, offset 0, flags [none], proto UDP (17), length 544)
    192.168.1.1.55985 > 192.168.1.139.49152: [udp sum ok] UDP, length 516
16:44:41.227418 IP (tos 0x0, ttl 128, id 0, offset 0, flags [none], proto UDP (17), length 32)
    192.168.1.139.49152 > 192.168.1.1.55985: [no cksum] UDP, length 4
```

### 已知问题

以太网引导模式存在一些已知问题。由于引导模式的实现在芯片本身，除了使用仅包含 bootcode.bin 文件的 SD 卡外，没有其他解决方法。

#### DHCP 请求在五次尝试后超时

Raspberry Pi 将尝试进行五次 DHCP 请求，每次间隔五秒，总共持续 25 秒。如果服务器在此期间无法响应，Raspberry Pi 将进入低功耗状态。除非使用 SD 卡上的 bootcode.bin，否则没有解决办法。

#### 不支持在不同子网上的 TFTP 服务器

在 Raspberry Pi 3 B+ (BCM2837B0) 中已修复。

#### DHCP 中继故障

DHCP 检查还检查了跳数值是否为 1，而在 DHCP 中继情况下，它不会这样。

在树莓派 3 A+ 中已修复。

#### 树莓派启动字符串

在 DHCP 回复中，“树莓派启动”字符串由于计算字符串长度的错误而需要占用额外三个空格。

在树莓派 3 型号 B+ 中已修复。

#### DHCP UUID 常量

DHCP UUID 设置为常量值。

已在树莓派 3 A+ 修复；该值设置为 32 位序列号。

#### ARP 检查可能在 TFTP 事务中间无法响应

树莓派只会在初始化阶段响应 ARP 请求；一旦开始传输数据，它将无法继续响应。

已在树莓派 3 A+ 修复。

#### DHCP 请求/回复/确认序列未正确实现

在启动时，树莓派广播 DHCPDISCOVER 数据包。DHCP 服务器回复一个 DHCPOFFER 数据包。然后树莓派继续启动而不执行 DHCPREQUEST 或等待 DHCPACK。这可能导致两个不同设备被提供相同的 IP 地址并在未正确分配给客户端的情况下使用它。

不同的 DHCP 服务器在这种情况下有不同的行为。dnsmasq（取决于设置）将散列 MAC 地址以确定 IP 地址，并 ping 该 IP 地址以确保它尚未被使用。这减少了这种情况发生的机会，因为这需要在散列中发生碰撞。

## GPIO 启动模式

>**注意**
>
>GPIO 引导模式仅适用于树莓派 3A+、3B、3B+，计算模块 3、3+。

老的树莓派可以配置：以在接通电源时使用连接到 GPIO 连接器的硬件选择启动模式。这是通过在 SoC 的 OTP 存储器中设置位来完成的。一旦设置了这些位，它们会永久性分配五个 GPIO，以便进行选择。只要设置了 OTP 位，就无法撤销。你应该仔细考虑是否启用此功能，因为这五个 GPIO 针脚将始终控制引导。尽管在树莓派引导后可以使用这些 GPIO 进行其他功能，但你必须进行额外设置，才能在树莓派引导时启用所需的启动模式。

要启用 GPIO 引导模式，请将以下行添加到 config.txt 文件中：

```
program_gpio_bootmode=n
```

其中 n 是你希望使用的 GPIO 的 bank。然后重启树莓派一次，以使用此设置编程 OTP。Bank 1 是 GPIO 22-26，Bank 2 是 GPIO 39-43。除非你有一个计算模块，否则必须使用 bank 1：Bank 2 上的 GPIO 仅在计算模块上可用。由于 OTP 位的排列方式，如果你首先为 Bank 1 编程 GPIO 引导模式，那么稍后可以选择 Bank 2。反之不成立：一旦选择 Bank 2 作为 GPIO 引导模式，就无法选择 Bank 1。

一旦启用了 GPIO 引导模式，树莓派将不再启动。你必须拉高至少有关一个引导模式的 GPIO 引脚，才能启动树莓派。

### 引脚分配

#### 树莓派 3B 和计算模块 3

| 引脚 1 | 引脚 2 | 启动类型                 |
| -------- | -------- | -------------------------- |
| 22     | 39     | SD0                      |
| 23     | 40     | SD1                      |
| 24     | 41     | NAND（目前不支持 Linux） |
| 25     | 42     | SPI (目前不支持 Linux)   |
| 26     | 43     | USB                      |

以上表格中的 USB 选项同时选择 USB 设备引导模式和 USB 主机引导模式。要使用 USB 引导模式，必须在 OTP 存储器中启用。有关更多信息，请参阅 USB 设备引导和 USB 主机引导。

#### 后续的树莓派 3B（带金属盖的 BCM2837B0）、树莓派 3A+、3B+ 和 Compute Module 3+

| 银行 1 | 银行 2 | 引导类型                  |
| -------- | -------- | --------------------------- |
| 20     | 37     | SD0                       |
| 21     | 38     | SD1                       |
| 22     | 39     | NAND（目前不支持 Linux）  |
| 23     | 40     | SPI（目前不支持 Linux）   |
| 24     | 41     | USB 设备                  |
| 25     | 42     | USB 主机 - 大容量存储设备 |
| 26     | 43     | USB 主机 - 以太网         |

>**注意**
>
>各种启动模式按照 GPIO 线的数字顺序尝试，即 SD0，然后 SD1，然后 NAND 等等。

### 启动流程

SD0 是博通 SD 卡/MMC 接口。当 SoC 内部的引导 ROM 运行时，SD0 将始终连接到内置的 microSD 卡。在带有 eMMC 设备的计算模块上，SD0 连接到该设备；在 Compute Module Lite 上，SD0 可用于边缘连接器，并连接到 CMIO 载板上的 microSD 卡。SD1 是 Arasan SD 卡/MMC 接口，也能够支持 SDIO。所有具有内置无线局域网的树莓派都使用 SD1 通过 SDIO 连接到无线芯片。

GPIO 针脚的默认上拉电阻为 50KΩ，详见 BCM2835 ARM 外围设备数据表第 102 页。推荐使用 5KΩ 的上拉电阻将 GPIO 针脚拉高：这样既可使 GPIO 正常工作，同时不会产生太多功耗。

## NVMe 固态硬盘引导

NVMe（高速非易失性内存）是通过 PCIe 总线进行外部存储访问的标准。你可以通过 Compute Module 4（CM4）IO 板或树莓派 5 上的 PCIe 槽连接 NVMe 驱动器。再通过一些额外配置，你就可以从 NVMe 驱动器启动了。

### 准备工作

#### 硬件

* NVMe M.2 固态硬盘
* 一款从 PCIe 转标准 M.2 的转接器

  * 对于树莓派 5，我们推荐使用 M.2 HAT+，它能把树莓派的 PCIe FFC 槽转换为 M Key 接口。
  * 对于 CM4，可搜索 "PCIe 3.0 ×1 转 M.2 NGFF M-Key SSD NVMe PCIe 转接器"

要检查你的 NVMe 驱动器是否正确连接，请从其他存储设备（如 SD 卡）引导你的 Raspberry Pi，并运行 ls -l /dev/nvme*。示例输出如下所示。

```
crw------- 1 root root 245, 0 Mar  9 14:58 /dev/nvme0
brw-rw---- 1 root disk 259, 0 Mar  9 14:58 /dev/nvme0n1
```

#### 软件

运行以下命令查看你正在运行的固件版本：

```
$ sudo rpi-eeprom-update
```

对于树莓派 5，你需要使用 2023 年 12 月 6 日及之后发布的固件。

为了 CM4，NVMe 引导支持于 2021 年 7 月引入。你需要自那时起发布的以下版本的软件：

* 引导加载程序
* VideoCore 固件
* 树莓派系统 Linux 内核

最新的树莓派系统发布包含你所需的一切。使用树莓派镜像制作工具将树莓派系统镜像安装到你的驱动器上。

### 编辑 EEPROM 启动顺序

对于树莓派 5，你需要启动树莓派系统以编辑启动顺序。你可以从 SD 卡或 USB 驱动器启动 树莓派 完成此步骤。即使更改启动设备，EEPROM 配置也会持久保留，因为 EEPROM 配置存储在板上本身。

使用树莓派配置命令行界面来更新启动加载程序：

```
$ sudo raspi-config
```

在 Advanced Options > Bootloader Version 下，选择 Latest。然后，使用 Finish 键或 Escape 键退出 raspi-config。

运行以下命令以将固件更新至最新版本：

```
$ sudo rpi-eeprom-update -a
```

然后，使用 sudo reboot 重启。你的树莓派 5 应该从 NVMe 启动。

对于 CM4，请使用 rpiboot 更新引导加载程序。你可以在 USB 启动 GitHub 存储库中找到构建 rpiboot 并配置 IO 板切换 ROM 到 usbboot 模式的说明。

对于带有 eMMC 的 CM4 版本，请确保你已将 NVMe 设置为引导顺序中的第一项。请记住在 recovery/boot.conf 中将 NVMe 引导模式 6 添加到 BOOT_ORDER 中。

当 SD 卡插槽为空时，CM4 Lite 会自动从 NVMe 引导。

### NVMe `BOOT_ORDER`

EEPROM 配置中的 BOOT_ORDER 设置控制引导行为。对于 NVMe 引导，请使用引导模式 6。有关更多信息，请参见树莓派引导加载程序配置。

### 例子

以下是引导加载程序检测到 NVMe 驱动器时 UART 输出的示例：

```
Boot mode: SD (01) order f64
Boot mode: USB-MSD (04) order f6
Boot mode: NVME (06) order f
VID 0x144d MN Samsung SSD 970 EVO Plus 250GB
NVME on
```

然后它将找到一个 FAT 分区并加载 start4.elf ：

```
Read start4.elf bytes  2937840 hnd 0x00050287 hash ''
```

然后加载内核并引导操作系统：

```
MESS:00:00:07.096119:0: brfs: File read: /mfs/sd/kernel8.img
MESS:00:00:07.098682:0: Loading 'kernel8.img' to 0x80000 size 0x1441a00
MESS:00:00:07.146055:0:[   0.000000] Booting Linux on physical CPU 0x0000000000 [0x410fd083]
```

在 Linux 中，SSD 显示为 /dev/nvme0，而“namespace”显示为 /dev/nvme0n1。将会有两个分区 /dev/nvme0n1p1 （FAT）和 /dev/nvme0n1p2 （EXT4）。使用 lsblk 来检查分区分配：

```
NAME        MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
nvme0n1     259:0    0 232.9G  0 disk
├─nvme0n1p1 259:1    0   256M  0 part /boot/firmware
└─nvme0n1p2 259:2    0 232.6G  0 part /
```

### 故障排除

如果引导过程失败，请在 rpi-eeprom GitHub 存储库上提交问题，确保附上控制台输出以及引导过程中所有屏幕显示的内容。

## HTTP 引导

网络安装功能使用以太网上的 HTTP 引导树莓派进入嵌入式树莓派启动盘制作工具。

除了网络安装，你还可能用 HTTP 下载的文件显式引导设备启动，即使禁用引导，网络安装也能用。

例如，你可以将这添加到你的 BOOT_ORDER 作为备用引导方法，或者将其放在 GPIO 条件后，在 GPIO 引脚拉低时从你自己的服务器启动 HTTP 引导。

例如，如果将以下内容添加到你的 EEPROM 配置中，且 GPIO 8（默认状态为 1 或高电平）被拉低，将下载文件 http://downloads.raspberrypi.org:80/net_install/boot.img、http://downloads.raspberrypi.org:80/net_install/boot.sig。如果启用开机网络安装，则会使用相同的网址。如果 GPIO 8 未被拉低，则行为将保持不变。

```
[gpio8=0]
BOOT_ORDER=0xf7
HTTP_HOST=downloads.raspberrypi.org
NET_INSTALL_ENABLED=0
```

boot.img 和签名文件 boot.sig 是个包含引导文件系统的内存盘。详情请参阅 boot_ramdisk。

如果启用安全启动并且未设置 HTTP_HOST，则将忽略 BOOT_ORDER 中的 HTTP。

### 要求

要使用 HTTP 引导，请更新至 2022 年 3 月 10 日及更新版本的引导程序。HTTP 引导需要有线以太网连接。

要使用定制 CA 证书，请更新至 2024 年 4 月 5 日及更新版本的引导程序。只有运行 BCM2712 CPU 的设备支持定制 CA 证书。

### 键

所有 HTTP 下载必须签名。引导加载程序包含一个用于默认主机 fw-download-alias1.raspberrypi.com 上文件的公钥。除非设置了 HTTP_HOST，并在 EEPROM 中内置公钥，否则该密钥将用于验证网络安装镜像。这能让你在自己的服务器上托管树莓派网络安装镜像。

>**警告**
>
>使用你自己的网络安装镜像将需要你对镜像进行签名，并将你的公钥添加到 EEPROM。如果你后续进行了公版 EEPROM 更新，你的密钥将丢失，并且需要重新添加。

USBBOOT 包含了编程公钥所需的全部工具。

使用以下命令将你的公钥添加到 EEPROM。boot.conf 包含你的修改：

```
$ rpi-eeprom-config -c boot.conf -p mypubkey.pem -o pieeprom.upd pieeprom.original.bin
```

使用以下命令可为你的 EEPROM 生成签名：

```
$ rpi-eeprom-digest -i pieeprom.upd -o pieeprom.sig
```

然后，使用以下命令使用你的私钥对网络安装镜像进行签名：

```
$ rpi-eeprom-digest -i boot.img -o boot.sig -k myprivkey.pem
```

最后，将 boot.img 和 boot.sig 放在你的网络服务器上，以使用自己签名的网络安装镜像。

### 证书

为了安全起见，网络安装使用 HTTPS 从树莓派网站下载操作系统镜像。此功能使用我们在引导程序中内置的自有 CA 根证书来验证主机。

你可以将你自己的定制 CA 证书添加到设备的 EEPROM，以安全地从你自己的网站下载镜像。使用工具 rpi-eeprom-config 的参数 --cacertder 能添加 DER 编码的证书。你必须在 EEPROM 配置设置中放置证书的哈希值，以确保证书未经篡改。

运行以下命令生成 DER 编码的证书：

```
$ openssl x509 -in your_ca_root_cert.pem -out cert.der -outform DER
```

然后，运行以下命令生成证书的 SHA-256 哈希：

```
$ sha256sum cert.der
```

应该会看到类似输出如下：

```
701bd97f67b0f5483a9734e6e5cf72f9a123407b346088638f597878563193fc  cert.der
```

接下来，更新 boot.conf 以包含证书的哈希值：

```
$ sudo rpi-eeprom-config --edit
```

在 [gpio8=0] 部分配置以下设置，替换为：

* 将 <your_website> 替换为你的网站，例如 yourserver.org
* 将 <path_to_files> 替换为托管在你的网站上的 OS 镜像的路径，例如 path/to/files
* 使用上面生成的哈希值 701bd97f67b0f5483a9734e6e5cf72f9a123407b346088638f597878563193fc，例如 <hash>

```
[all]
BOOT_UART=1
POWER_OFF_ON_HALT=0
BOOT_ORDER=0xf461

[gpio8=0]
BOOT_ORDER=0xf7
NET_INSTALL_ENABLED=0
HTTP_HOST=<your_website>
HTTP_PATH=<path_to_files>
HTTP_CACERT_HASH=<hash>
```

当你指定 HTTP_CACERT_HASH 时，Network Install 将通过 HTTPS 下载镜像。没有哈希时，Network Install 将使用 HTTP 下载镜像。

最后，使用以下命令将所有内容加载到 EEPROM 中：

```
$ rpi-eeprom-config -c boot.conf -p mypubkey.pem -o pieeprom.bin --cacertder cert.der pieeprom.original.bin
$ rpi-eeprom-digest -k myprivkey.pem -i pieeprom.bin -o pieeprom.sig
```

在网络启动过程中，你的树莓派应该使用 HTTPS 而不是 HTTP。要查看由网络安装解析的完整的 HTTPS 下载链接，请查看引导输出：

```
Loading boot.img ...
HTTP: GET request for https://yourserver.org:443/path/to/files/boot.sig
HTTP: GET request for https://yourserver.org:443/path/to/files/boot.img
```

### 安全启动

如果启用了安全启动，则树莓派只能运行由客户私钥签名的代码。因此，如果你想要在安全启动的情况下使用网络安装、HTTP 启动模式，你必须使用自己的密钥签署 boot.img 并生成 boot.sig，并在某处托管这些文件供下载。EEPROM 中的公钥将用于验证镜像。

如果启用安全启动且未设置 HTTP_HOST，则网络安装和 HTTP 引导将被禁用。

有关安全启动的更多信息，请参阅 USBBOOT。

## 引导顺序

>**重要**
>
>此启动顺序仅适用于基于 BCM2837、BCM2837B0 的树莓派。在此之前的型号，树莓派将尝试 SD 卡引导，然后是 USB 设备模式引导。有关树莓派 4 和树莓派 5 的引导顺序，请参阅 EEPROM 引导流程部分。

树莓派 3 上的 USB 引导默认取决于所使用的版本。如果默认未启用 USB 引导模式，请参阅此页面获取有关启用 USB 引导模式的信息。

当 BCM2837 引导时，它使用两个不同的来源来确定要启用哪些引导模式。首先，会检查一次性可编程（OTP）存储器块，看哪些引导模式已启用。如果启用了 GPIO 引导模式设置，则会测试相关的 GPIO 线，以选择应尝试哪个已在 OTP 中启用的引导模式。请注意，GPIO 引导模式仅可用于选择已在 OTP 中启用的引导模式。有关配置 GPIO 引导模式的详细信息，请参阅 GPIO 引导模式。默认情况下，GPIO 引导模式已禁用。

接下来，启动 ROM 会在每个启动源中检查名为`bootcode.bin`的文件；如果找到，它会将代码加载到本地 128K 缓存并跳转到该代码。总体启动模式过程如下：

* BCM2837 启动
* 读取 OTP 以确定启用哪些启动模式
* 如果启用了 GPIO 启动模式，请使用 GPIO 启动模式来细化启用的启动模式列表
* 如果启用：检查 GPIO 48-53 上的主 SD 是否存在 bootcode.bin
  * 成功 - 启动
  * 失败 - 超时（五秒）
* 如果启用：检查辅助 SD
  * 成功 - 启动
  * 失败 - 超时（五秒）
* 如果启用：检查 NAND
* 如果启用：检查 SPI
* 如果启用：检查 USB
  * 如果 OTG 引脚 == 0
    * 启用 USB，等待有效的 USB 2.0 设备（两秒）
      * 设备已找到：
        * 如果设备类型 == hub
          * 递归每个设备
        * 如果设备类型 == (大容量存储或 LAN951x)
          * 存储在设备列表中
    * 递归遍历每个 MSD
      * 如果找到 bootcode.bin 引导
    * 递归遍历每个 LAN951x
      * DHCP / TFTP 引导
  * 其他（设备模式启动）
    * 启用设备模式并等待主机 PC 枚举
    * 我们用 VID: 0a5c PID: 0x2763 回复 PC（树莓派 1 或树莓派 2）或 0x2764 （树莓派 3）

>**注意**
>
>如果没有插入 SD 卡，SD 引导模式将在五秒钟后失败。为了缩短这个时间并更快地切换到 USB 模式，你可以插入空白的 SD 卡，或者使用上面描述的 GPIO 引导模式 OTP 设置，只启用 USB。GPIO 的默认拉取在 ARM 外围设备数据手册的第 102 页上有定义。如果引导时的值不等于默认拉取值，则启用该引导模式。USB 枚举是一种使下游设备在集线器上获取电源，然后等待设备拉动 D+ 和 D- 线以指示其是 USB 1 还是 USB 2 的方法。这可能需要一段时间：对于某些设备，硬盘驱动器可能需要长达 3 秒的时间来启动并开始枚举过程。因为这是唯一能检测硬件连接的方法，所以我们必须等待的最短时间为两秒。如果设备在最大超时时间后仍未响应，则可以使用 program_usb_boot_timeout=1 在 config.txt 中增加超时时间至五秒。MSD 引导优先于以太网引导。不再需要第一个分区是 FAT 分区，因为 MSD 引导将继续搜索第一个分区之外的 FAT 分区。引导 ROM 现在还支持 GUID 分区，并已测试过使用 Mac、Windows 和 Linux 分区的硬盘。使用供应商 ID 0x0424 和产品 ID 0xec00 可以检测 LAN951x，这与独立的 LAN9500 设备不同，后者的产品 ID 是 0x9500 或 0x9e00。要使用独立的 LAN9500，需要添加 I²C EEPROM 以更改这些 ID 以匹配 LAN951x。

主要 SD 卡引导模式默认设置为 GPIO 49-53。可以在第二组引脚上从次要 SD 卡引导，即将次要 SD 卡连接到 GPIO 引脚。但是，我们尚未启用此功能。

NAND 引导和 SPI 引导模式的确能用，尽管它们还未完全支持 GPU。

USB 设备引导模式在出厂时默认启用，但 USB 主机引导模式只有在 program_usb_boot_mode=1 时才启用。一旦启用，处理器将使用处理器上的 OTGID 引脚的值来在这两种模式之间做出决定。在所有树莓派 B/B+ 上，OTGID 引脚被驱动为 0，因此一旦启用，就只能通过主机模式引导（无法再使用设备模式引导，因为 LAN951x 设备阻挡了路径）。

如果将 OTGID 引脚浮置（例如，插入 PC），则树莓派 Zero 或计算模块将作为 USB 设备引导启动，因此你可以将 bootcode.bin 推入设备中。相关 usbboot 代码可在 GitHub 上找到。

## EEPROM 引导流程

自树莓派 4 起，树莓派 旗舰设备使用 EEPROM 启动加载程序。与以前的产品相比，主要区别在于第二阶段启动加载程序是从 SPI 闪存 EEPROM 加载，而不是像以前的产品一样从 bootcode.bin 文件加载。

### 第一阶段启动加载程序

ROM（第一阶段）的引导流程如下：

* SoC 上电
* 读取 OTP（一次性可编程存储器）以确定是否配置了 `nRPIBOOT` GPIO
* 如果 `nRPIBOOT` GPIO 为高电平或 OTP 未定义 `nRPIBOOT` GPIO
  * 检查 OTP 以查看是否可以从 SD/EMMC 加载 `recovery.bin`
    * 如果启用了 SD `recovery.bin`，则检查主 SD/EMMC 中的 `recovery.bin`
      * 成功 - 运行 `recovery.bin` 并更新 SPI EEPROM
      * 失败 - 继续
  * 检查 SPI EEPROM 中的第二阶段加载程序
    * 成功 - 运行第二阶段启动加载程序
    * 失败 - 继续
* 如果成功
  * 尝试从 [USB 设备启动](https://www.raspberrypi.com/documentation/computers/compute-module.html#flash-compute-module-emmc) 加载 `recovery.bin`
    * 成功 - 运行 `recovery.bin` 并更新 SPI EEPROM 或切换到 USB 大容量存储设备模式
    * 失败 - 重试 USB 设备启动

>**注意**
>
>recovery.bin 是一个用于更新引导加载程序 SPI EEPROM 镜像的最小第二阶段程序。

### 第二阶段引导程序

本节介绍了第二阶段引导程序的高级流程。

请参阅[引导程序配置](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#raspberry-pi-bootloader-configuration) 页面以获取有关每种引导模式的更多信息，以及[引导文件夹](https://www.raspberrypi.com/documentation/computers/configuration.html#boot-folder-contents) 页面以了解此阶段加载的 GPU 固件文件的描述。

* 初始化时钟和 SDRAM
* 读取 EEPROM 配置文件
* 检查`PM_RSTS`寄存器以确定是否请求 HALT
  * 检查`POWER_OFF_ON_HALT`和`WAKE_ON_GPIO`的 EEPROM 配置设置
  * 如果`POWER_OFF_ON_HALT`为`1`且`WAKE_ON_GPIO`为`0`，则
    * 使用 PMIC 关闭系统电源
  * 否则，如果`WAKE_ON_GPIO`为`1`，则
    * 启用 GPIO3 的下降沿中断以便在 GPIO3 被拉低时唤醒
  * 进入休眠
* While True
  * 从 EEPROM 配置文件中的 BOOT_ORDER 参数读取下一个引导模式
  * 如果引导模式为`RESTART`，则
    * 跳回到`BOOT_ORDER`字段中的第一个引导模式
  * 否则如果引导模式为`STOP`，则
    * 显示 start.elf 未找到的[错误模式](https://www.raspberrypi.com/documentation/computers/configuration.html#led-warning-flash-codes) 并永久等待。
  * 否则如果引导模式为`SD CARD`，则
    * 尝试从 SD 卡加载固件
      * 成功 - 运行固件
      * 失败 - 继续
  * 否则如果引导模式为`NETWORK`，则
    * 使用 DHCP 协议请求 IP 地址
    * 从 DHCP 或静态定义的 TFTP 服务器加载固件
    * 如果未找到固件或发生超时或网络错误，则继续
  * 否则如果引导模式为`USB-MSD`或引导模式为`BCM-USB-MSD`，则
    * 当 USB 发现未超时时
      * 检查 USB 大容量存储设备
      * 如果找到新的大容量存储设备，则
        * 对每个驱动器（LUN）
          * 尝试加载固件
            * 成功 - 运行固件
            * 失败 - 前进到下一个 LUN
  * 否则如果引导模式为`NVME`，则
    * 扫描 PCIe 以查找 NVMe 设备，如果找到
      * 尝试从 NVMe 设备加载固件
        * 成功 - 运行固件
        * 失败 - 继续
  * 否则如果引导模式为`RPIBOOT`，则
    * 尝试使用 USB 设备模式从 USB OTG 端口加载固件 - 参见[USB 引导](https://github.com/raspberrypi/usbboot)。`RPIBOOT`模式没有超时。

#### Raspberry Pi 5 的不同

* 电源按钮用于从 PMIC STANDBY、HALT 唤醒，而非 GPIO 3。
* 固件加载 start.elf 而不是 start.elf。实际上，引导加载程序内置了嵌入版本的 start.elf。
* 连接到 3A 电源时，默认禁用 USB 启动。在 /boot/firmware/config.txt 中设置 usb_max_current_enable=1 可启用 USB 启动。或者你可以在 USB 启动失败时，按一下电源按钮来临时启用 usb_max_current_enable 并继续引导。但是，如果是按电源按钮启用的，该设置在重启后将失效。

### 引导加载程序更新

如果找到 pieeprom.upd 文件，固件启动之前也可以更新引导加载程序。有关引导加载程序更新的更多信息，请参阅引导加载程序 EEPROM 页面。

### 安全模式操作系统更新（ tryboot ）

引导加载程序/固件提供了一个一次性标志，如果设置了该标志，会清除，但会导致加载 tryboot.txt 而不是 config.txt。这种备用配置将指定待处理的 OS 更新固件、cmdline、内核和 os_prefix 参数。因为在启动固件之前清除了该标志，所以崩溃或重置会导致在下次重启时加载原始的 config.txt 文件。

要设置 tryboot 标志，请在 reboot 命令中的分区号后添加 tryboot。通常，分区号默认为 0。但如果要添加额外的参数，则必须指定分区号。传递参数给 reboot 时始终使用引号：它只接受一个参数：

```
$ sudo reboot '0 tryboot'
```

所有树莓派型号都支持 tryboot，但是在树莓派 4 A 1.0 和 1.1 版本上，EEPROM 不能写保护。这是因为旧的树莓派 4B 设备必须重置电源供应（会丢失 tryboot 状态），而这些信息正存储在 EEPROM。

如果 secure-boot 启用，则 tryboot 模式将导致加载 tryboot.img 而不是 boot.img。

### tryboot_a_b 模式

如果 autoboot.txt 中的 tryboot_a_b 属性设置为 1，则加载的是 config.txt 而不是 tryboot.txt。这是因为在更高级别（分区）已经进行了 tryboot 切换，因此在备用分区本身内部不需要具有 tryboot.txt 文件。

当从内置的 boot.img 镜像加载文件，tryboot_a_b 属性会被隐式设置为 1。

## 树莓派引导加载程序配置

### 编辑配置

在编辑引导加载程序配置之前，请更新你的系统以获取 rpi-eeprom 软件包的最新版本。

要查看当前的 EEPROM 配置，请运行以下命令：

```
$ rpi-eeprom-config
```

要编辑当前的 EEPROM 配置并将更新应用于最新的 EEPROM 版本，请运行以下命令：

```
$ sudo -E rpi-eeprom-config --edit
```

关于 EEPROM 更新过程的更多信息，请参阅启动 EEPROM。

### 配置属性

本节描述引导加载程序中所有可用的配置项。语法与 config.txt 相同，但属性是特定于引导加载程序的。条件过滤器也受支持，除了 EDID 之外。

#### `BOOT_UART`

如果 1 则启用 GPIO 14 和 15 上的 UART 调试输出。将接收调试终端配置为 115200bps，8 位，无奇偶校验位，1 个停止位。

 默认: 0

#### `UART_BAUD`

仅适用于树莓派 5。

更改引导加载程序 UART 的波特率。

支持的值: 9600 , 19200 , 38400 , 57600 , 115200 , 230400 , 460800 , 921600

 默认: 115200

#### `WAKE_ON_GPIO`

如果 1 则 sudo halt 将在较低功耗模式下运行，直到 GPIO3 或 GLOBAL_EN 短接至地。

在树莓派 5 上，此设置并不相关，因为专用电源按钮可以始终用于唤醒来自 HALT 或 STANDBY。

 默认: 1

#### `POWER_OFF_ON_HALT`

如果 1 和 WAKE_ON_GPIO=0，那么 sudo halt 将关闭所有 PMIC 输出。这是 halt 的最低功耗状态，但可能会导致一些 HATs 出现问题，因为 5V 仍将处于开启状态。GLOBAL_EN 必须短接地来启动。

树莓派 400 有一个专用的电源按钮，即使处理器关闭也能工作。这个功能默认启用，但可设置 WAKE_ON_GPIO=2 来使用外部 GPIO 电源按钮，而不是专用电源按钮。

在树莓派 5 上，这将把 PMIC 置于 STANDBY 模式，其中所有输出都被关闭。无需设置 WAKE_ON_GPIO，按下专用电源按钮将启动设备。

 默认: 0

#### `BOOT_ORDER`

BOOT_ORDER 设置允许对不同启动模式的优先级进行灵活配置。它表示为一个 32 位无符号整数，其中每个半 B 代表一个启动模式。启动模式按照从最低有效半 B 到最高有效半 B 的顺序尝试。

##### BOOT_ORDER 字段

BOOT_ORDER 属性定义了不同引导模式的顺序。它是从右到左读取的，最多可以定义八位数字。

| 值 | 模式 | 说明                                                                                        |
| ---- | ------ | ---------------------------------------------------------------------------------------------- |
| `0x0`   | `SD CARD DETECT`     | 尝试 SD 卡，然后等待卡检测指示卡已更改。现在已弃用，因为 0xf ( RESTART ) 可用。    |
| `0x1`   | `SD CARD`     | SD 卡 (或 Compute Module 4 上的 eMMC)。                                            |
| `0x2`   | `NETWORK`     | 网络引导-请参阅网络引导服务器教程。                                                |
| `0x3`   | `RPIBOOT`     | RPIBOOT-请参阅 usbboot。                                                           |
| `0x4`   | `USB-MSD`     | USB 大容量存储引导-请参阅 USB 大容量存储引导。                                     |
| `0x5`   | `BCM-USB-MSD`     | 通过 USB-C 插口从 USB 2.0 启动（CM4：CM4IO 板上的 USB-A 插口）。在树莓派 5 上不可用。  |
| `0x6`   | `NVME`     | 仅限于 CM4 和 Pi 5：从连接到 PCIe 接口的 NVMe SSD 启动。有关更多详细信息，请参阅 NVMe 启动。|
| `0x7`   | `HTTP`     | 通过以太网上的 HTTP 引导。有关更多详细信息，请参阅 HTTP 引导。                     |
| `0xe`   | `STOP`     | 停止并显示错误模式。需要电源循环以退出此状态。                                     |
| `0xf`   | `RESTART`     | 从 BOOT_ORDER 字段中的第一个引导模式重启，即循环。                             |

RPIBOOT 与计算模块 4 同时使用，加载自定义调试镜像（例如，Linux RAM-disk）而不是正常的引导。这应该是最后的引导选项，因为它目前不支持超时或重试。

##### BOOT_ORDER 示例

| BOOT\_ORDER | 说明                                                                 |
| ---------------- | ---------------------------------------------------------------------- |
| `0xf41`               | 首先尝试 SD 卡，然后是 USB-MSD，再重复（如果 BOOT_ORDER 为空时默认） |
| `0xf14`               | 首先尝试 U 盘，然后是 SD 卡，然后重复                                |
| `0xf21`               | 首先尝试 SD 卡，然后是网络，然后重复                                 |
| `0xf46`               | 首先尝试 NVMe，然后是 USB-MSD，然后重复                              |

#### `MAX_RESTARTS`

如果遇到 0xf 重启 ( RESTART ) 引导模式超过 MAX_RESTARTS 次数，则会触发看门狗复位。这不建议一般使用，但在需要完全重置以解决硬件或网络接口问题的测试或远程系统上可能会有用。

默认值： -1 (无限)

#### `SD_BOOT_MAX_RETRIES`

在移动到由 BOOT_ORDER 定义的下一个引导模式之前，在 SD 引导失败后重试的次数。

-1 意味着无限重试。

 默认值: 0

#### `NET_BOOT_MAX_RETRIES`

失败后在移动到下一个由 BOOT_ORDER 定义的引导模式之前，网络引导将重试的次数。

-1 表示无限重试。

 默认： 0

#### `DHCP_TIMEOUT`

整个 DHCP 序列在失败当前迭代之前的超时时间（毫秒）。

 最小值: 5000

 默认值: 45000

#### `DHCP_REQ_TIMEOUT`

DHCP DISCOVER 或 DHCP REQ 重试之前的超时时间（毫秒）。

 最小值: 500

 默认值: 4000

#### `TFTP_FILE_TIMEOUT`

通过 TFTP 单个文件下载的超时时间（毫秒）。

 最小值: 5000

 默认值: 30000

#### `TFTP_IP`

可选的点分十进制 IP 地址（例如 192.168.1.99 ）用于 TFTP 服务器，覆盖来自 DHCP 请求的服务器 IP。

在家庭网络上，可能会发现这很有用，因为可以使用 tftpd-hpa 代替 dnsmasq，其中宽带路由器是 DHCP 服务器。

 默认： ""

#### `TFTP_PREFIX`

为了让每个树莓派都有唯一 TFTP 启动目录，引导加载程序会将文件名前缀添加到特定于设备的目录。如果在带前缀的目录中找不到 start4.elf 或 start.elf，则会清除前缀。

在早期型号上，序列号被用作前缀，但在树莓派 4 和 5 上，MAC 地址不再由序列号生成，这使得通过检查 DHCPDISCOVER 包自动创建 tftpboot 目录在服务器上变得困难。为了方便，TFTP_PREFIX 可以定义为 MAC 地址、固定值或序列号（默认）。

| 值 | 描述                                   |
| ---- | ---------------------------------------- |
| 0  | 使用序列号，例如 9ffefdef/             |
| 1  | 使用 TFTP_PREFIX_STR 指定的字符串      |
| 2  | 使用 MAC 地址，例如 dc-a6-32-01-36-c2/ |

 默认值: 0

#### `TFTP_PREFIX_STR`

当 TFTP_PREFIX 设置为 1 时，指定用于自定义目录前缀的字符串。例如：- TFTP_PREFIX_STR=tftp_test/

 默认值: ""

最大长度：32 个字符

#### `PXE_OPTION43`

使用不同的字符串覆盖 PXE Option43 匹配字符串。通常最好将定制应用于 DHCP 服务器，而不是更改客户端行为，但在无法进行更改的情况下提供此选项。

 默认：树莓派 Boot

#### `DHCP_OPTION97`

在之前的版本中，客户端 GUID（Option97）只是将序列号重复四次。默认情况下，新的 GUID 格式为四字符码（FourCC）的串联（ RPi4 0x34695052 适用于 树莓派 4 或 RPi5 0x35695052 适用于树莓派 5），板子版本（例如 0x00c03111 或 0x00d04170 ）（4 B），MAC 地址的最低有效 4 B 以及 4 B 的序列号。这旨在是独一无二的，同时也向 DHCP 服务器提供结构化信息，使得可以识别树莓派 4 和 5 计算机，而无需依赖以太网 MAC OUID。

指定 DHCP_OPTION97=0 以恢复旧行为，或指定非零十六进制值以指定自定义的 4 B 前缀。

 默认值： 0x34695052

#### `MAC_ADDRESS`

用给定的值覆盖树莓派以太网 MAC 地址。例如 dc:a6:32:01:36:c2

 默认： ""

#### `MAC_ADDRESS_OTP`

使用存储在客户 OTP 寄存器中的值覆盖树莓派以太网 MAC 地址。

例如，要使用存储在 Customer OTP 的行 0 和 1 中的 MAC 地址。

```
MAC_ADDRESS_OTP=0,1
```

第一个值（例如中的第 0 行）包含 OUI 和 MAC 地址的最高 8 位。第二个值（例如中的第 1 行）存储 MAC 地址的剩余 16 位。这与在制造时用于树莓派 MAC 地址的格式相同。

可以选择并以任何顺序组合任意两个客户行。

Customer OTP 行是 OTP 寄存器 36 到 43，在 vcgencmd otp_dump 输出中，所以如果前两行被编程如下，则 MAC_ADDRESS_OTP=0,1 就会给出一个 MAC 地址为 e4:5f:01:20:24:7e。

```
36:247e0000
37:e45f0120
```

 默认值： ""

#### 静态 IP 地址配置

如果设置了 TFTP_IP 和以下选项，则跳过 DHCP，并应用静态 IP 配置。如果 TFTP 服务器与客户端在同一子网上，则可能省略 GATEWAY。

##### `CLIENT_IP`

客户端的 IP 地址，例如 192.168.0.32

 默认： ""

##### `SUBNET`

子网地址掩码，例如 255.255.255.0

 默认： ""

##### `GATEWAY`

如果 TFTP 服务器位于不同子网上，则要使用的网关地址，例如 192.168.0.1

 默认： ""

#### `DISABLE_HDMI`

如果 DISABLE_HDMI=1，HDMI 启动诊断显示将被禁用。其他非零值保留供将来使用。

 默认： 0

#### `HDMI_DELAY`

跳过 HDMI 诊断显示，最多 N 秒（默认值 5）,除非发生致命错误。默认行为旨在避免在正常 SD/USB 引导时，引导加载程序诊断屏幕短暂出现。

 默认: 5

#### `ENABLE_SELF_UPDATE`

启用引导加载程序从 TFTP 或 USB 大容量存储设备（MSD）引导文件系统中更新自身。

如果自更新已启用，则引导加载程序将在引导文件系统中查找更新文件（.sig/.upd）。如果更新镜像与当前镜像不同，则应用更新并重置系统。否则，如果 EEPROM 镜像是逐字节相同的，则引导将继续正常进行。

 注：

* 2021 年之前的引导加载程序版本不支持 self-update。
* 2022 年之前，SD 启动中未启用自更新功能。在树莓派 4 上，ROM 已经可以从 SD 卡加载 recovery.bin。在 CM4 上，自更新和 recovery.bin 都不生效，需要使用 USB 启动（请参阅计算模块 EEPROM 引导程序文档）。
* 从 2022 年开始（beta 和稳定版），可以启用 SD 卡的自更新功能。
* 对于网络启动，请确保 TFTP boot 目录可以通过 NFS 挂载，并且 rpi-eeprom-update 可以写入其中。

 默认值: 1

#### `FREEZE_VERSION`

以前，此属性仅由 rpi-eeprom-update 脚本检查。但是，现在自更新已启用，引导加载程序还将检查此属性。如果设置为 1，则将覆盖 ENABLE_SELF_UPDATE 以停止自动更新。要禁用 FREEZE_VERSION，你必须使用带有 recovery.bin 的 SD 卡引导。

自定义 EEPROM 更新脚本也必须检查此标志。

 默认： 0

#### `HTTP_HOST`

如果启动网络安装或 HTTP 引导，则会从此服务器下载 boot.img 和 boot.sig。

无效的主机名将被忽略。它们应仅包含小写字母数字字符和 - 或 .。如果设置了 HTTP_HOST，则将禁用 HTTPS 并改用普通的 HTTP。你可以指定 IP 地址以避免 DNS 查找的需要。在主机名中不要包含 HTTP 方案及正斜杠。

 默认: fw-download-alias1.raspberrypi.com

#### `HTTP_PORT`

你可以使用此属性来更改用于网络安装和 HTTP 引导的端口。当使用默认主机 `fw-download-alias1.raspberrypi.com` 时，启用 HTTPS。如果更改了 `HTTP_HOST`，则禁用 HTTPS 并使用普通 HTTP。

当禁用 HTTPS 时，即使将 `HTTP_PORT` 更改为 `443`，仍将使用普通 HTTP。

默认值：如果启用 HTTPS，则为`443`，否则为`80`

#### `HTTP_PATH`

用于网络安装和 HTTP 引导的路径。

区分大小写。路径分隔符使用正斜杠（Linux 样式）。前导和尾部的正斜杠不是必需的。

如果未设置 `HTTP_HOST`，则忽略 `HTTP_PATH`，URL 将为 `https://fw-download-alias1.raspberrypi.com:443/net_install/boot.img`。如果设置了 `HTTP_HOST`，URL 将为 `http://<HTTP_HOST>:<HTTP_PORT>/<HTTP_PATH>/boot.img`

默认值：`net_install`

#### `IMAGER_REPO_URL`

嵌入式树莓派制造者应用程序会在启动时下载一个 JSON 文件进行配置。

你可以更改内嵌的树莓派制作程序应用程序使用的 JSON 文件的网址，以便提供你自己的镜像。你可以通过 --repo 参数传递网址来测试标准的 树莓派 制作程序应用程序。

 默认： http://downloads.raspberrypi.org/os_list_imagingutility_v3.json

#### `NET_INSTALL_ENABLED`

当启用网络安装时，如果检测到了键盘，引导加载程序会在启动时显示网络安装界面。

为了启用网络安装，请添加 NET_INSTALL_ENABLED=1，或者为了禁用网络安装，请添加 NET_INSTALL_ENABLED=0。

如果设置 DISABLE_HDMI=1，则此设置将被忽略，网络安装将被禁用。

为了检测键盘，网络安装必须初始化 USB 控制器并枚举设备。这会增加约 1 秒的启动时间，因此在某些嵌入式应用中禁用网络安装可能更为有利。

在树莓派 4 和树莓派 400 上默认为 1，在计算模块 4 上为 0。

#### `NET_INSTALL_KEYBOARD_WAIT`

如果启用了网络安装，则引导加载程序会尝试检测键盘和按 SHIFT 键以启动网络安装。你可以使用此属性更改此等待时间的长度（以毫秒为单位）。

将此设置为 0 将禁用对键盘的等待，尽管如果找不到引导文件且 USB 引导模式为 4 且处于 BOOT_ORDER 中，则仍可以启动网络安装。

>**注意**
>
>测试表明检测键盘和 SHIFT 至少需要 750 毫秒。

 默认: 900

#### NETCONSOLE - 高级日志记录

NETCONSOLE 复制调试消息到网络接口。IP 地址和接口由 NETCONSOLE 字符串定义。

>**注意**
>
>NETCONSOLE 阻塞，直到以太网连接建立或超时发生。超时值为 DHCP_TIMEOUT，尽管除非请求网络引导，否则不会尝试 DHCP。

##### 格式

有关更多信息，请参阅 Netconsole 文档。

```
src_port@src_ip/dev_name,dst_port@dst_ip/dst_mac
E.g. 6665@169.254.1.1/,6666@/
```

为了简化解析，引导加载程序要求每个字段分隔符都存在。必须指定源 IP 地址，但以下字段可以留空并分配默认值。

* src_port - 6665
* dev_name - "" (设备名称始终被忽略)
* dst_port - 6666
* dst_ip - 255.255.255.255
* dst_mac - 00:00:00:00:00

通过将测试树莓派 4 连接到运行 WireShark 的另一个树莓派，并选择“udp.srcport == 6665”作为过滤器，然后选择 分析 → 跟随 → UDP 数据流 以 ASCII 日志形式查看数据的一种方式。

默认情况下不应启用 NETCONSOLE，因为这可能会导致网络问题。可以通过 GPIO 过滤器按需启用。

```
# Enable debug if GPIO 7 is pulled low
[gpio7=0]
NETCONSOLE=6665@169.254.1.1/,6666@/
```

默认: "" (未启用)

最大长度: 32 个字符

#### `PARTITION`

如果未显式地由 reboot 命令 (例如 sudo reboot N ) 或 boot_partition=N 在 autoboot.txt 中设置，则可以使用 PARTITION 选项来指定引导分区号。用户可以按下按钮来从救援分区启动。

```
# Boot from partition 2 if GPIO 7 is pulled low
[gpio7=0]
PARTITION=2
```

 默认值: 0

#### `PSU_MAX_CURRENT`

仅适用于树莓派 5。

如果设置，该参数指示固件跳过 USB 供电握手，并假定连接到了具有给定电流等级的电源。通常设置为 3000（小电流电源） 或 5000（大电流电源）。

 默认: ""

#### `USB_MSD_EXCLUDE_VID_PID`

一个包含最多四个 VID/PID 对的列表，指定引导加载程序应忽略的设备。如果这与 HUB 匹配，则该 HUB 不会被枚举，导致所有下游设备被排除。这旨在允许在引导枚举期间忽略有问题的设备（例如，枚举速度非常慢）。这是引导加载程序特有的，并不传递给操作系统。

格式是一个以 VID 为最高有效半 B 的十六进制值的逗号分隔列表。不允许有空格。例如 034700a0,a4231234

 默认值： ""

#### `USB_MSD_DISCOVER_TIMEOUT`

如果在此超时期间未找到任何 USB 大容量存储设备，则停止 USB-MSD 并选择下一个引导模式。

最小值： 5000 （5 秒）

默认: 20000 (20 秒)

#### `USB_MSD_LUN_TIMEOUT`

在前进到下一个 LUN 之前等待的毫秒数，例如多槽 SD-CARD 读卡器。这仍在调整中，但可能有助于加快启动速度，如果连接了旧、慢设备以及包含 OS 的快速 USB-MSD 设备。

 最小值: 100

默认: 2000 (2 秒)

#### `USB_MSD_PWR_OFF_TIME`

仅适用于树莓派 4。

当树莓派重启时，硬件会关闭 USB 电源。短暂的断电时间可能会导致某些 USB 设备出现问题，因此可以使用此参数强制执行较长的断电时间，就像在物理上拔掉电线一样。

在 RaspberryPi 4 版本 1.3 及更早版本上，要配置/长关机需要启用 XHCI 控制器，因此实际上会先进行短关机，然后是较长的可配置关机。通过将此参数设置为零，可以跳过较长的可配置关机。

在更新的版本中，硬件确保 USB 电源在重启后关闭，引导加载程序只在此超时经过后才启用电源。这是在内存初始化后发生的，确保 USB 电源至少关闭两秒。因此，此参数通常对新的硬件版本没有影响。

 最小值： 0

 最大值: 5000

默认值: 1000 (1 秒)

#### `USB_MSD_STARTUP_DELAY`

如果定义了，那么在 USB 主控制器初始化后，延迟给定的超时时间进行 USB 枚举。如果 USB 硬盘驱动器需要很长时间初始化并触发 USB 超时，那么可以使用此延迟给驱动程序额外的初始化时间。可能还需要增加总体 USB 超时时间 ( USB_MSD_DISCOVER_TIMEOUT )。

 最小值: 0

最大值: 30000 (30 秒)

 默认值: 0

#### `VL805`

仅适用于计算模块 4。

如果 VL805 属性设置为 1，则引导加载程序将搜索 VL805 PCIe XHCI 控制器，并尝试使用嵌入在引导加载程序 EEPROM 中的 VL805 固件进行初始化。这使得工业设计可以使用 VL805 XHCI 控制器而无需提供专用的 SPI EEPROM 来存储 VL805 固件。

* 在计算模块 4 上，引导加载程序永远不会写入专用的 VL805 SPI EEPROM。此选项仅配置控制器从 SDRAM 加载固件。
* 如果 VL805 XHCI 控制器有专用的 EEPROM，请勿使用此选项。它将无法初始化，因为 VL805 ROM 将尝试使用专用的 SPI EEPROM（如果已安装）。
* 嵌入式 VL805 固件假定与树莓派 4B 相同的 USB 配置（两个 USB 3.0 接口和四个 USB 2.0 ports）。不支持加载替代的 VL805 固件镜像，应该改用专用的 VL805 SPI EEPROM 来替换这样的配置。

 默认: 0

#### `XHCI_DEBUG`

此属性是一个位字段，用于控制 USB 调试消息在大容量存储引导模式下的冗长程度。启用所有这些消息会生成大量日志数据，会降低启动速度，甚至可能导致启动失败。对于详细日志，最好使用 NETCONSOLE。

| 值 | 日志                        |
| ---- | ----------------------------- |
| `0x1`   | U 盘描述符                  |
| `0x2`   | 大容量存储模式状态机        |
| `0x4`   | 大容量存储模式状态机 - 详细 |
| `0x8`   | 所有的 USB 请求             |
| `0x10`   | 设备和集线器状态机          |
| `0x20`   | 所有的 xHCI TRBs (非常详细) |
| `0x40`   | 所有 xHCI 事件（非常冗长）  |

要合并值，请将它们相加。例如：

```
# Enable mass storage and USB descriptor logging
XHCI_DEBUG=0x3
```

默认： 0x0 （未启用任何 USB 调试消息）

#### [config.txt] 部分

在读取 config.txt GPU 固件 start4.elf 后，读取引导加载程序 EEPROM 配置并检查是否存在名为 [config.txt] 的部分。如果 [config.txt] 部分存在，则将从此部分开头到文件末尾的内容附加到内存中，以便与从引导分区读取的 config.txt 文件的内容组合。这可用于自动应用设置到每个操作系统，例如 dtoverlays。

>**警告**
>
>如果你配置引导加载程序时出现无法引导的无效配置，则必须重新刷新引导加载程序 EEPROM 为有效配置以引导。

>**技巧**
>
>一些配置属性存储在 config.txt 中。有关这些属性的更多信息，请参阅配置属性。

## 显示并行接口 (DPI)

##### [在树莓派上使用 DPI 显示](https://pip.raspberrypi.com/categories/685-whitepapers-app-notes/documents/RP-003471-WP/Using-a-DPI-display.pdf)

在树莓派上使用 DPI 显示器

40 针通用输入/输出（GPIO）连接器可用于将显示并行接口（DPI）显示器连接到树莓派设备，作为使用专用显示串行接口（DSI）或高清多媒体接口（HDMI）的替代方案。

所有带有 40 针排针和计算模块的树莓派板都提供了高达 24 位并行 RGB 接口。此接口允许将并行 RGB 显示器连接到树莓派的 GPIO，无论是在 RGB24（每种红、绿和蓝色各 8 位）还是 RGB666（每种颜色 6 位）或 RGB565（5 位红色，6 位绿色和 5 位蓝色）模式下。

此接口由 GPU 固件控制，并可以通过用户通过特殊 config.txt 参数和启用正确的 Linux 设备树叠加层来进行编程。

### GPIO 引脚

树莓派 GPIO 的 Bank 0 上可选择的一个替代功能是 DPI（显示并行接口），这是一个简单的时钟并行接口（最多可提供 R、G 和 B 的 8 位；时钟、使能、水平同步和垂直同步）。此接口在 GPIO Bank 0 上作为替代功能 2（ALT2）可用：

| GPIO | ALT2 |
| ------ | ------ |
| `GPIO0`     | `PCLK`     |
| `GPIO1`     | `DE`     |
| `GPIO2`     | `LCD_VSYNC`     |
| `GPIO3`     | `LCD_HSYNC`     |
| `GPIO4`     | `DPI_D0`     |
| `GPIO5`     | `DPI_D1`     |
| `GPIO6`     | `DPI_D2`     |
| `GPIO7`     | `DPI_D3`     |
| `GPIO8`     | `DPI_D4`     |
| `GPIO9`     | `DPI_D5`     |
| `GPIO10`     | `DPI_D6`     |
| `GPIO11`     | `DPI_D7`     |
| `GPIO12`     | `DPI_D8`     |
| `GPIO13`     | `DPI_D9`     |
| `GPIO14`     | `DPI_D10`     |
| `GPIO15`     | `DPI_D11`     |
| `GPIO16`     | `DPI_D12`     |
| `GPIO17`     | `DPI_D13`     |
| `GPIO18`     | `DPI_D14`     |
| `GPIO19`     | `DPI_D15`     |
| `GPIO20`     | `DPI_D16`     |
| `GPIO21`     | `DPI_D17`     |
| `GPIO22`     | `DPI_D18`     |
| `GPIO23`     | `DPI_D19`     |
| `GPIO24`     | `DPI_D20`     |
| `GPIO25`     | `DPI_D21`     |
| `GPIO26`     | `DPI_D22`     |
| `GPIO27`     | `DPI_D23`     |

>**注意**
>
>DPI 输出引脚上的颜色值可以以 565、666 或 24 位模式显示（请参阅下表和参数 output_format 的 dpi_output_format 部分）的多种方式： 



|     |     |     |     |     |     |     |     |     |     |     |     |     |     |     |     |     |     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **Mode** | **RGB bits** | **GPIO** |     |     |     |     |     |     |     |     |     |     |     |     |     |     |     |     |     |     |     |     |     |     |     |
| **27** | **26** | **25** | **24** | **23** | **22** | **21** | **20** | **19** | **18** | **17** | **16** | **15** | **14** | **13** | **12** | **11** | **10** | **9** | **8** | **7** | **6** | **5** | **4** |     |     |
| 1   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   |
| 2   | 565 | -   | -   | -   | -   | -   | -   | -   | -   | 7   | 6   | 5   | 4   | 3   | 7   | 6   | 5   | 4   | 3   | 2   | 7   | 6   | 5   | 4   | 3   |
| 3   | 565 | -   | -   | -   | 7   | 6   | 5   | 4   | 3   | -   | -   | 7   | 6   | 5   | 4   | 3   | 2   | -   | -   | -   | 7   | 6   | 5   | 4   | 3   |
| 4   | 565 | -   | -   | 7   | 6   | 5   | 4   | 3   | -   | -   | -   | 7   | 6   | 5   | 4   | 3   | 2   | -   | -   | 7   | 6   | 5   | 4   | 3   | -   |
| 5   | 666 | -   | -   | -   | -   | -   | -   | 7   | 6   | 5   | 4   | 3   | 2   | 7   | 6   | 5   | 4   | 3   | 2   | 7   | 6   | 5   | 4   | 3   | 2   |
| 6   | 666 | -   | -   | 7   | 6   | 5   | 4   | 3   | 2   | -   | -   | 7   | 6   | 5   | 4   | 3   | 2   | -   | -   | 7   | 6   | 5   | 4   | 3   | 2   |
| 7   | 888 | 7   | 6   | 5   | 4   | 3   | 2   | 1   | 0   | 7   | 6   | 5   | 4   | 3   | 2   | 1   | 0   | 7   | 6   | 5   | 4   | 3   | 2   | 1   | 0   |

### 禁用其他 GPIO 外设

必须禁用使用冲突 GPIO 引脚的所有其他外设叠加层。在 config.txt 中，请注意注释或反转启用 I²C 或 SPI 的任何 dtparams：

```
dtparam=i2c_arm=off
dtparam=spi=off
```

### 配置显示器

内核模式设置（KMS）通用显示接口使输出能够连接到任意显示器，只要你有适当的驱动程序。

#### 自动检测

自动检测允许你的树莓派与显示器连接，无需手动配置设备树叠加。默认情况下启用了自动检测。你可以通过将以下行添加到 config.txt 来启用显示器自动检测：

```
display_auto_detect=1
```

用 0 替换 1 以禁用自动检测。当你连接启用自动检测的官方树莓派显示器时，KMS 会自动确定显示并配置适当的显示设置。

#### 手动配置显示器

>**注意**
>
>在树莓派系统 Bookworm 或更高版本中，先前用于设置 DPI 的 dpi_output_format 和 dpi_timings 条目已被 vc4-kms-dpi-generic 叠加层取代。

要使用除树莓派官方显示屏之外的其他显示屏，必须在配置文件中指定 dtoverlay 条目。面板制造商应在 Linux 内核代码中配置你的显示屏的定时，并提供一个叠加层来启用这些设置。请参阅 Adafruit Kippah 显示屏条目以获取示例。以下示例演示如何在你的 txt 文件中为 Kippah 显示屏设置一个 dtoverlay 条目：

```
dtoverlay=vc4-kms-kippah-7inch-overlay
```

显示定时通常在内核中定义，但你也可以在提供的 BSD 驱动程序中定义它们。如果你的面板在内核代码中缺乏定义的叠加层，则可以使用 BSD 驱动程序将显示定时定义为参数。这使你能够为任何显示屏手动配置设备树条目。

以下示例演示如何使用设备树参数定义定时：

```
dtoverlay=vc4-kms-v3d
dtoverlay=vc4-kms-dpi-generic,hactive=480,hfp=26,hsync=16,hbp=10
dtparam=vactive=640,vfp=25,vsync=10,vbp=16
dtparam=clock-frequency=32000000,rgb666-padhi
```

>**注意**
>
>设备树行长度不得超过 80 个字符。当设置需要超过 80 个字符的行时，请将该参数的赋值拆分为多行。

参数显示树定义支持以下参数:

| 选项 | 说明                                             |
| ------ | ---------------------------------------------------- |
| `clock-frequency`     | 显示时钟频率（Hz）                                 |
| `hactive`     | 水平活动像素                                       |
| `hfp`     | 水平前廊                                           |
| `hsync`     | 水平同步脉冲宽度                                   |
| `hbp`     | 水平后廊                                           |
| `vactive`     | 纵向活动线                                         |
| `vfp`     | 纵向前肩                                           |
| `vsync`     | 纵向同步脉冲宽度                                   |
| `vbp`     | 垂直后肩                                           |
| `hsync-invert`     | 水平同步低电平                                     |
| `vsync-invert`     | 垂直同步低电平                                     |
| `de-invert`     | 数据使能低电平                                     |
| `pixclk-invert`     | 负边沿像素时钟                                     |
| `rgb565`     | 在 GPIO 0-19 上改变为 RGB565 输出                  |
| `rgb666-padhi`     | 在 GPIO 0-9，12-17 和 20-25 上改变为 RGB666 输出   |
| `rgb888`     | 在 GPIOs 0-27 上更改为 RGB888 输出                 |
| `bus-format`     | 覆盖 MEDIA_BUS_FMT_*值的总线格式，也被 rgbXXX 覆盖 |
| `backlight-gpio`     | 定义用于背光控制的 GPIO（默认值：无）              |

## GPIO 和 40 针排针

你可以在所有当前的树莓派主板上找到一个 40 针 GPIO（通用输入/输出）排针。主板上所有的 GPIO 排针间距均为 0.1 英寸（2.54 mm）。

>**注意**
>
>“H”后缀的 Zero 和 Pico 没有排针。

![GPIO pinout diagram](https://www.raspberrypi.com/documentation/computers/images/GPIO-Pinout-Diagram-2.png?hash=df7d7847c57a1ca6d5b2617695de6d46)

通用 I/O (GPIO) 引脚可配置为通用输入、通用输出，或者最多六种特殊交替设置之一，其功能取决于引脚。

![GPIO layout](https://www.raspberrypi.com/documentation/computers/images/GPIO.png?hash=335edaa0c254546813319d80556f842f)

>**注意**
>
>GPIO 引脚编号方案不按数字顺序排列。GPIO 引脚 0 和 1 位于板上（物理引脚 27 和 28），但保留供高级用途。

### 输出

作为输出引脚指定的 GPIO 引脚可以设置为高电平（3.3V）或低电平（0V）。

### 输入

作为输入引脚指定的 GPIO 引脚可以读取为高电平（3.3V）或低电平（0V）。使用内部上拉或下拉电阻器可以更轻松地实现此功能。GPIO2 和 GPIO3 引脚内置上拉电阻器，但对于其他引脚，可以在软件中进行配置。

### 查看树莓派的 GPIO 引脚布局

可以通过打开终端窗口并运行命令 pinout 在树莓派上访问 GPIO 参考。此工具由 GPIO Zero Python 库提供，在树莓派系统中预装。

>**警告**
>
>尽管把简单的组件连接到 GPIO 引脚是安全的，但要小心线路的连接方式。应该用电阻限制通过 LED 的电流。不要给 3.3V 的组件用 5V。不要把电机直接连接到 GPIO 引脚，应该使用 H 桥电路、电机控制板。

### 权限

为了使用 GPIO 接口，你的用户必须是 gpio 组的成员。默认用户账户已经是了，但对于其他用户，你必须使用以下命令手动加入：

```
$ sudo usermod -a -G gpio <username>
```

### GPIO 引脚

BCM2835 封装的 GPIO 在外设数据表中有时被称为“pads”，这是一个半导体设计术语，即“连接到外部世界的芯片”。

这些 pads 是可配置的 CMOS 推挽输出驱动器/输入缓冲器。可用于寄存器控制设置的包括：

* 内部上拉/下拉使能/失能
* 输出驱动强度
* 输入施密特触发器滤波

#### 上电状态

所有 GPIO 引脚在上电复位时恢复为通用输入。还应用了默认拉电状态，详细信息请参阅 Arm 外设数据手册中的备用功能表。大多数 GPIO 引脚都应用了默认拉电。

### 中断

每个 GPIO 引脚在配置为通用输入时，可以配置为 Arm 的中断源。可配置多个中断产生源：

* 边沿敏感（高/低）
* 上升/下降沿
* 异步上升/下降沿

水平中断会保持中断状态，直到系统软件清除该中断（例如通过处理产生中断的附加外围设备）。

普通的上升/下降沿检测在检测中内置了少量的同步。在系统时钟频率下，引脚在三个周期窗口内采样，生成中断的标准是在稳定的转换中，即记录为 1 0 0 或 0 1 1。异步检测绕过此同步，以便检测非常窄的事件。

### 备用功能

几乎所有的 GPIO 引脚的功能都能被修改。SoC 内部的外设模块可以选择出现在一组 GPIO 引脚中的一个及多个上，例如，I²C 总线可以配置为至少三个独立位置之一。当引脚配置为替代功能时，例如，控制驱动强度或施密特触发器等仍然适用。

大部分功能适用于所有引脚，个别仅适用于特定引脚：

* PWM（脉冲宽度调制）
  * 所有引脚都支持软件 PWM
  * GPIO12、GPIO13、GPIO18、GPIO19 支持硬件 PWM
* SPI
  * SPI0：MOSI（GPIO10）；MISO（GPIO9）；SCLK（GPIO11）；CE0（GPIO8），CE1（GPIO7）
  * SPI1：MOSI（GPIO20）；MISO（GPIO19）；SCLK（GPIO21）；CE0（GPIO18）；CE1（GPIO17）；CE2（GPIO16）
* I²C
  * 数据: (GPIO2); 时钟 (GPIO3)
  * EEPROM 数据: (GPIO0); EEPROM 时钟 (GPIO1)
* 串行
  * TX（GPIO14）; RX（GPIO15）

### 电压规格

主板上有两个 5V 针脚、两个 3.3V 针脚，以及一些接地针脚（GND），这些不能被重新配置。剩余的针脚都是通用的 3.3V 针脚，意味着输出被设置为 3.3V，输入是 3.3V 兼容的。

下表列出了针对 BCM2835、BCM2836、BCM2837 和 RP3A0 系列产品（例如树莓派 Zero 或树莓派 3+）的 GPIO 针脚的各种电压规格。有关计算模块的信息，请参阅相应的数据表。

| 符号          | 参数          | 条件            | 最小 | 典型 | 最大 | 单元   |
| --------------- | --------------- | ----------------- | ------ | ------ | ------ | -------- |
| V\~IL\~ | 低电压输入    | -               | -    | -    | 0.9  | V      |
| V\~IH\~ | 高电压输入^a^ | -               | 1.6  | -    | -    | V      |
| I\~IL~        | 输入泄漏电流  | TA = +85°C     | -    | -    | 5    | μA   |
| C\~IN\~ | 输入电容      | -               | -    | 5    | -    | 电源   |
| 音量          | 输出低电压    | IOL \= -2mA  | -    | -    | 0.14 | V      |
| V\~OH\~ | 输出高电压^b^ | IOH = 2 mA    | 3.0  | -    | -    | V      |
| I\~OL\~ | 输出低电流^c^ | 电压 = 0.4V | 18   | -    | -    | mA   |
| I\~OH\~ | 输出高电流^c^ | VO \= 2.3V   | 17   | -    | -    | mA   |
| 上拉电阻      | 上拉电阻      | -               | 50   | -    | 65   | kΩ    |
| 下拉电阻      | 下拉电阻      | -               | 50   | -    | 65   | kΩ |

^a^ 滞后效应已启用 ^b^ 默认驱动强度 (8mA) ^c^ 最大驱动强度 (16mA)

下表显示了 BCM2711 系列产品（例如树莓派 4、400）上 GPIO 引脚的电压规格。有关计算模块的信息，请参阅相关数据表。

| 符号          | 参数          | 条件           | 最小值 | 典型 | 最大 | 单元 |
| --------------- | --------------- | ---------------- | -------- | ------ | ------ | ------ |
| 低电压输入    | 输入低电压    | -              | -      | -    | 0.8  | V    |
| 高电压输入    | 输入高电压^a^ | -              | 2.0    | -    | -    | V    |
| I\~IL\~ | 输入漏电流    | TA = +85℃     | -      | -    | 10   | μA  |
| V\~OL\~ | 输出低电压^b^ | IOL \= -4mA | -      | -    | 0.4  | V    |
| V\~OH\~ | 输出高电位^b^ | IOH = 4mA   | 2.6    | -    | -    | V    |
| I\~OL\~ | 输出低电流^c^ | VO \= 0.4V  | 7      | -    | -    | mA |
| 输出高电流    | 输出高电流    | VO \= 2.6V  | 7      | -    | -    | mA   |
| R\~PU\~ | 上拉电阻      | -              | 33     | -    | 73   | kΩ  |
| R\~PD\~ | 下拉电阻      | -              | 33     | -    | 73   | kΩ  |

^a^ 滞后效应已启用 ^b^ 默认驱动强度 (4mA) ^c^ 最大驱动强度 (8mA)

## GPIO 控制器

GPIO 驱动强度并不表示最大电流，仅表示在此电流下 pad 仍将符合规范。你应该设置 GPIO 驱动强度以匹配所连接的设备，以便设备能够正常工作。

### 控制驱动强度

在 pad 内部有多个并联驱动器。如果将驱动强度设置为低（ 0b000 ），则大多数驱动器将处于三态状态，因此不会对输出电流产生影响。如果增加驱动强度，则会并联更多驱动器。图表显示了该行为。

>**警告**
>
>对于树莓派 4、400，计算模块 4，当前级别是图表中显示数值的一半。

![GPIO drive strength diagram](https://www.raspberrypi.com/documentation/computers/images/pi_gpio_drive_strength_diagram.png?hash=466ec669893a20d65c4f54da5aea9e3f)

### 当前数值

当前数值指定了在此电路板仍能满足规范的最大电流。

当前值不是垫片将提供的电流，也不是电流限制。

触点片输出是一个电压源：

* 如果设置为高电平，触点片将尝试将输出驱动到电源电压（3.3V）

该触点将尝试将输出引至高电平或低电平。成功取决于所连接设备的要求。如果该触点短接至地线，则无法输出高电平。它将尽可能输送尽可能多的电流，电流仅受内部电阻限制。

如果该触点输出高电平且短接至地线，在一段时间后将损坏。如果你将其连接至 3.3V 并输出低电平同样也是如此。

符合规格是由保证的电压水平确定的。由于引脚是数字的，因此有两个电压级别，高电平和低电平。I/O 接口有两个处理输出电平的参数：

* V~OL~，最大低电平电压（在 3.3V VDD IO 时为 0.14V）
* V~OH~，最小高电平电压（在 3.3V VDD IO 时为 3.0V）

V~OL~=0.14V 意味着如果输出为低电平，则电压将 <= 0.14V。V~OH~=3.0V 意味着如果输出为高电平，则电压将 >= 3.0V。

例如，驱动强度为 16mA 表示如果你将端口设置为高电平，可以吸收高达 16mA 电流，并且输出电压保证 >=V~OH~。这也意味着，如果你将驱动强度设置为 2mA，但吸收了 16mA 电流，则电压将不会达到 V~OH~，而会更低。事实上，可能不足以被外部设备识别为高电平。

GPIO 引脚的物理特性有更多信息。

>**注意**
>
>在计算模块设备上，可以将 VDD IO 从标准的 3.3V 更改。在这种情况下，V~OL~ 和 V~OH~ 将根据 GPIO 部分的表格进行更改。

树莓派 的 3.3V 电源为每个 GPIO 引脚的设计最大电流是 ~3mA。如果你将每个引脚的负载设定为 16mA，则总电流为 272mA。在此负载水平下，3.3V 电源将崩溃。会引发大电流脉冲，特别是如果有电容负载。脉冲将在附近的其他引脚之间反弹。这可能会造成对 SD 卡乃至内存行为的干扰。

### 安全电流

所有的键盘的电子元件均设计为 16mA。这是一个安全值，在此范围内你不会损坏设备。即使你将驱动强度设置为 2mA，然后负载为 16mA，也不会损坏设备。除此之外的最大安全电流都不保证。

### GPIO 地址

* 0x 7e10 002c PADS (GPIO 0-27)
* 0x 7e10 0030 PADS（GPIO 28-45）
* 0x 7e10 0034 PADS（GPIO 46-53）

| 位    | 字段名称 | 说明                                       | 类型 | 复位 |
| ------- | ---------- | -------------------------------------------- | ------ | ------ |
| 31:24 | PASSWRD  | 写入时必须为 0x5A；意外写保护密码          | W    | 0    |
| 23:5  |          | 保留 - 写入为 0，读取不影响                |      |      |
| 4     | SLEW     | 斜坡率; 0 = 斜坡率受限; 1 = 斜坡率不受限制 | RW   | 1    |
| 3     | HYST     | 启用输入滞后; 0 = 禁用; 1 = 启用           | RW   | 1    |
| 2:0   | DRIVE    | 驱动强度，请参见下面的详细列表             | RW   | 3    |

当心同时切换输出（SSO）限制，这些限制取决于设备以及 PCB 的质量和布局，去耦电容器的数量和质量，触点子上的负载类型（电阻，电容）以及树莓派无法控制的其他因素。

### 驱动强度列表

* 0 = 2mA
* 1 = 4mA
* 2 = 6mA
* 3 = 8mA
* 4 = 10mA
* 5 = 12mA
* 6 = 14mA
* 7 = 16mA

## 树莓派的工业用途

树莓派经常被用作其他产品的组件。本文档介绍了一些额外的功能，以便于使用你树莓派的其他功能。

### 一次性可编程设置

##### [在树莓派单板计算机上使用一次性可编程内存](https://pip.raspberrypi.com/categories/685-whitepapers-app-notes/documents/RP-003611-WP/Using-the-One-time-programmable-memory-on-Raspberry-Pi-single-board-computers.pdf)

在树莓派开发板计算机上使用一次性可编程内存

所有树莓派单板计算机（SBCs）都有内置的一次编程（OTP）存储器区域，实际上是主片上的一部分。正如其名称（一次性）暗示的那样，OTP 存储器只能被写入一次（即二进制 0 只能改为 1）。一旦某位置 1，就永远无法恢复为 0。可将 OTP 的每一位都视为一根保险丝。对其进行编程代表有意地熔断保险丝 —— 这是一种不可逆的过程，因为你无法进入芯片内部去替换它！

本白皮书假定树莓派正在运行树莓派操作系统（OS），并且已完全更新最新固件和内核。

有许多可以使用的 OTP 值。要查看所有 OTP 值的列表，请运行以下命令：

```
$ vcgencmd otp_dump
```

这个转储中的一些有趣的行：

* 28 - 序列号
* 29 - 序列号的补码
* 30 - 板子修订号码

此外，从 36 到 43（包括 36 和 43），有八行 32 位供客户使用。

>**注意**
>
>在 BCM2712 设备上，这些数字是不同的。第 31 行是序列号，第 32 行是板子修订号码。客户行是 77 到 84（包括 77 和 84）。

一些这些行可以使用 vcmailbox 进行编程。这是一个 Linux 驱动程序界面，用于处理行的编程。要执行此操作，请参考文档和 vcmailbox 示例应用程序。

vcmailbox 应用程序可以直接在树莓派系统的命令行上使用。一个示例用法是：

```
$ vcmailbox 0x00010004 8 8 0 0
```

...会返回类似于：

```
0x00000020 0x80000000 0x00010004 0x00000008 0x800000008 0xnnnnnnnn 0x00000000 0x00000000
```

以上使用邮箱属性接口 GET_BOARD_SERIAL，请求大小为 8 B，响应大小为 8 B（发送两个整数作为请求 0,0）。对此的响应将是两个整数（0x00000020 和 0x80000000），后跟标签代码、请求长度、响应长度（第 31 位设为 1 表示它是响应），然后是 64 位序列号（其中最高 32 位始终为 0）。

### 编写和读取客户 OTP 值

>**警告**
>
>OTP 值是一次性可编程的。一旦将位从 0 更改为 1，则无法改回。

要设置定制 OTP 值，你需要使用 SET_CUSTOMER_OTP (0x38021) 标签如下：

```
$ vcmailbox 0x00038021 [8 + number * 4] [8 + number * 4] [start_num] [number] [value] [value] [value] ...
```

* start_num = 要从 0-7 编程的第一行
* number = 要编程的行数
* value = 每个值到程序

因此，要将 OTP 客户行 4、5 和 6 编程为分别为 0x11111111、0x22222222、0x33333333，你将使用：

```
$ vcmailbox 0x00038021 20 20 4 3 0x11111111 0x22222222 0x33333333
```

然后将会编程第 40、41、42 行。

要读回值，你可以使用：

```
$ vcmailbox 0x00030021 20 20 4 3 0 0 0
```

 这应该显示：

```
0x0000002c 0x80000000 0x00030021 0x00000014 0x80000014 0x00000000 0x00000003 0x11111111 0x22222222 0x33333333
```

如果你想将此功能集成到你自己的代码中，你应该能够通过使用 vcmailbox.c 代码作为示例来实现这一点。

### 在非 BCM2712 设备上锁定 OTP

可以锁定 OTP 更改，以避免它们再次被编辑。

这可以通过使用带有 OTP 写邮箱的特殊参数来完成。

```
$ vcmailbox 0x00038021 8 8 0xffffffff 0xaffe0000
```

一旦锁定，客户 OTP 值将无法修改。请注意，此锁定操作是不可逆的。

### 在 BCM2712 设备上锁定 OTP

可以使用以下命令将客户区域标记为只读。

```
$ vcmailbox 0x00030086 4 4 0
```

一次性密码仅在设备重置前锁定，因此每次启动时都需要重新应用一次性密码锁定。

### 使非 BCM2712 设备上的客户一次性密码位不可读

可以完全阻止读取客户一次性密码位。这可以通过在一次性密码写邮箱中使用特殊参数来实现：

```
$ vcmailbox 0x00038021 8 8 0xffffffff 0xaffebabe
```

这个操作对于绝大多数用户来说可能没有什么用处，并且是不可逆的。

### 定制 MAC 地址对于 BCM2712 设备

在 BCM2712 设备上，以太网、Wi-Fi 和蓝牙 MAC 地址在 OTP 存储器中设置。这些值可以随客户值而改变。

获取客户端的 MAC 地址 vcmailbox 0x00030082/3/4 6 6 0 0，其中 2 是以太网，3 是 Wi-Fi，4 是蓝牙：

```
$ vcmailbox 0x00030083 6 6 0 0
0x00000020 0x80000000 0x00030083 0x00000006 0x80000006 0xddccbbaa 0x0000ffee 0x00000000
```

要设置客户端的 MAC 地址，必须按正确顺序将其发送为两个 32 字的单词。你可以运行一个命令来检查它是否格式正确：

```
$ vcmailbox 0x00030085 6 6 0x44332211 0x6655
```

检查日志以查看 MAC 地址是否符合你的预期：

```
$ sudo vclog -m
1057826.701: read mac address 11:22:33:44:55:66
```

多播地址不被视为有效。MAC 地址中最高位的最低有效位是多播位，因此确保这个位未设置。

然后可以使用命令 vcmailbox 0x00038082/3/4 6 6 <row1> <row0> 设置客户 MAC 地址：

```
$ vcmailbox 0x00038082 6 6 0x44332211 0x6655
```

如果客户 MAC 地址设置为 ff:ff:ff:ff:ff:ff，则将被忽略。

### 设备特定的私钥

使用 Broadcom BCM2712 处理器的设备具有 16 行 OTP 数据（512 位），用于支持文件系统加密。不使用 BCM2712 的设备具有可用于设备特定的私钥的 8 行 OTP（256 位）。

可以使用类似于管理客户 OTP 行所使用的相似 vcmailbox 命令来编程和读取这些行。如果不需要安全引导 / 文件系统加密，则可以使用设备私钥行来存储通用信息。

* 设备专用密钥行只能通过 vcmailbox 命令读取，该命令需要访问 /dev/vcio，该访问权限仅限于树莓派系统上的 video 组。
* 树莓派计算机没有硬件保护密钥存储。建议将此功能与安全启动结合使用，以限制对这些数据的访问。
* 树莓派系统不支持加密根文件系统。

有关开源磁盘加密的更多信息，请参见 Cryptsetup。

#### 使用 rpi-otp-private-key 将密钥编程到 OTP 中。

rpi-otp-private-key 脚本包装设备私钥 vcmailbox API，使得更容易以 OpenSSL 格式读取和写入密钥。

>**注意**
>
>usbboot 库包含你需要的所有工具，包括 rpi-eeprom 作为 Git 子模块。

把这个 32 B 的密钥读取为 64 个字符的十六进制数：

```
$ cd usbboot/tools
$ rpi-otp-private-key
```

 示例输出：

```
f8dbc7b0a4fcfb1d706e298ac9d0485c2226ce8df7f7596ac77337bd09fbe160
```

将 32 B 的随机生成数字写入设备私钥。

>**警告**
>
>此操作无法撤销。

```
$ rpi-otp-private-key -w $(openssl rand -hex 32)
```

>**注意**
>
>要指定要使用的 OTP 行数，请传递 -l <word count>。要指定密钥存储中的起始位置，请传递 `-o <word offset>`。

#### 读取/写入密钥的邮箱 API

读取所有行。

```
$ vcmailbox 0x00030081 40 40 0 8 0 0 0 0 0 0 0 0
```

 示例输出：

```
0x00000040 0x80000000 0x00030081 0x00000028 0x80000028 0x00000000 0x00000008 0xf8dbc7b0 0xa4fcfb1d 0x706e298a 0xc9d0485c 0x2226ce8d 0xf7f7596a 0xc77337bd 0x09fbe160 0x00000000
```

将所有行写入（用密钥数据替换末尾的八个零）：

```
$ vcmailbox 0x00038081 40 40 0 8 0 0 0 0 0 0 0 0
```

写入前一个示例中显示的密钥：

```
$ vcmailbox 0x38081 40 40 0 8 0xf8dbc7b0 0xa4fcfb1d 0x706e298a 0xc9d0485c 0x2226ce8d 0xf7f7596a 0xc77337bd 0x09fbe160
```

## OTP 寄存器和位定义

所有树莓派范围使用的 SoC 都具有内置的一次可编程（OTP）存储器块。少数位置具有出厂程序化的数据。

 OTP 存储器大小：

* 非 BCM2712 设备：66 个 32 位值
* BCM2712 设备：192 个 32 位值

要显示 OTP 的内容，请运行以下命令：

```
$ vcgencmd otp_dump
```

### 针对非 BCM2712 设备的 OTP 寄存器

此列表包含关于寄存器的公开信息。如果某个寄存器或位未在此定义，则表示它未公开。

16 OTP 控制寄存器 - BCM2711
* 第 26 位：禁用 VC JTAG
* 位 27: 禁用 VC JTAG
  17 引导模式寄存器
* 位 1: 将振荡器频率设置为 19.2MHz
* 位 3: 启用 SDIO 引脚上的上拉电阻
* 位 15: 禁用 ROM RSA 密钥 0 -（如果设置，则启用安全启动）（BCM2711）
* 位 19: 启用 GPIO 引导模式
* 位 20：设置用于检查 GPIO 引导模式的银行
* 位 21：启用从 SD 卡引导
* 位 22：设置用于引导的银行
* 位 28：启用 USB 设备引导
* 位 29：启用 USB 主机引导（以太网和大容量存储）

>**注意**
>
>在 BCM2711 上，引导模式由引导加载程序 EEPROM 配置而不是 OTP 定义。

18 启动模式寄存器的副本
  28 序列号
  29 ~(序列号)
30 修订代码 ^1^
33 电路板修订扩展 - 意义取决于电路板型号。这通过设备树在 /proc/device-tree/chosen/rpi-boardrev-ext 中提供，并且可以通过在 config.txt 中设置 board_rev_ext 来临时覆盖测试目的中的 OTP 值。

*计算模块 4
  * 位 30：计算模块是否安装了 Wi-Fi 模块
    * 0 - Wi-Fi
    * 1 - 没有 Wi-Fi
  * Bit 31:计算模块是否安装了 EMMC 模块
    * 0 - EMMC
    * 1 - 无 EMMC（Lite）

* 树莓派 400
  * 位 0-7：piwiz 使用的默认键盘国家代码
36-43  客户 OTP 值
  45 MPG2 解码密钥
  46 WVC1 解码密钥

47-54 SHA256 RSA 公钥的安全引导

55 安全启动标志（由引导加载程序保留使用）

56-63 256 位设备特定私钥

64-65 MAC 地址；如果设置，系统将优先使用此地址，而不是基于序列号自动生成的地址

66 高级启动寄存器（非 BCM2711）

* 位 0-6：ETH_CLK 输出引脚的 GPIO
* 位 7：启用 ETH_CLK 输出
* 位 8-14：LAN_RUN 输出引脚的 GPIO
* 位 15：启用 LAN_RUN 输出
* 位 24：延长 USB HUB 超时参数
* 位 25: ETH_CLK 频率:
  * 0 - 25MHz
  * 1 - 24MHz

^1^还包含禁用过压、OTP 编程和 OTP 读取的位。

### BCM2712 设备上的 OTP 寄存器

此列表包含关于寄存器的公开信息。如果此处未定义寄存器或位，则表示其非公开。

  22 引导模式寄存器

* 第 1 位：从 SD 卡启动
* 第 2-4 位：从 SPI EEPROM 启动（以及哪些 GPIO）
* 位 10: 禁止从 SD 卡引导
* 位 11: 禁止从 SPI 引导
* 位 12: 禁止从 USB 引导

23 引导模式寄存器的副本

  29 高级引导模式

* 0-7 位：SD 卡检测的 GPIO
* 位 8-15：用于 RPIBOOT 的 GPIO

序列号的低 32 位为 31

  32 板上修订版本

33 板属性 - 其含义取决于板。这可通过设备树在 /proc/device-tree/chosen/rpi-boardrev-ext 中获取

35 序列号的高 32 位 全 64 位序列号可在 /proc/device-tree/serial-number 中获取

50-51 以太网 MAC 地址 这会传递到操作系统中的设备树中，例如 /proc/device-tree/axi/pcie@120000/rp1/ethernet@100000/local-mac-address

52-53 Wi-Fi MAC 地址 这将传递给操作系统中的设备树，例如 /proc/device-tree/axi/mmc@1100000/wifi@1/local-mac-address

54-55 蓝牙 MAC 地址 这将传递给操作系统中的设备树，例如 /proc/device-tree/soc/serial@7d50c000/bluetooth/local-bd-address

77-84 客户 OTP 值

86board 国家 - piwiz 使用的默认键盘国家代码。如果设置，则可通过设备树在 /proc/device-tree/chosen/rpi-country-code 中获取。

87-88 客户以太网 MAC 地址。如果设置，将覆盖 OTP 行 50-51。

89-90 客户 Wi-Fi MAC 地址。如果设置，将覆盖 OTP 行 52-53。

89-90  客户蓝牙 MAC 地址 如果设置，将覆盖 OTP 行 54-55

109-114 工厂设备 UUID 目前是一个 16 位数字 id，应与设备上的条形码匹配。使用零字符填充并进行 c40 编码。

此项信息可通过设备树在 /proc/device-tree/chosen/rpi-duid 中获取。

## 树莓派连接器用于 PCIe

![树莓派 connector for PCIe](https://www.raspberrypi.com/documentation/computers/images/pcie.jpg?hash=35b4d5db3702574625f0e1e9686cdd51)

树莓派连接器用于 PCIe

树莓派 5 版在主板的右侧有一个 FPC 连接器。该连接器提供了 PCIe Gen 2.0 ×1 接口，用于连接快速外设。

将 PCIe HAT+ 设备连接到树莓派。你的树莓派应该会自动检测到该设备。要连接非 HAT+ 设备，请将其连接到树莓派，然后手动启用 PCIe。

有关 PCIe FPC 连接器引脚分配和创建第三方设备、配件和 HAT 所需的其他详细信息，请参阅树莓派 PCIe 标准文档。建议同时阅读树莓派 HAT+ 规格说明。

>**注意**
>
>目前无法枚举位于在交换机后的 PCIe 设备。

### 启用 PCIe

默认情况下，除非连接到了 HAT+ 设备，否则不会启用 PCIe 连接器。要启用连接器，请将以下行添加到 /boot/firmware/config.txt ：

```
dtparam=pciex1
```

使用 sudo reboot 重启以使配置更改生效。

>**注意**
>
>你还可以使用别名 nvme。

### 从 PCIe 启动

默认情况下，树莓派设备不会从 PCIe 存储启动。要启用从 PCIe 启动，请更改引导加载程序配置中的 BOOT_ORDER。使用以下命令编辑 EEPROM 配置：

```
$ sudo rpi-eeprom-config --edit
```

将 BOOT_ORDER 行替换为如下行：

```
BOOT_ORDER=0xf416
```

若要从非 HAT+ 设备启动，还需添加以下行：

```
PCIE_PROBE=1
```

保存更改后，使用 sudo reboot 重启你的树莓派以更新 EEPROM。

### PCIe 3.0

>**警告**
>
>树莓派 5 未获 3.0 速度认证。PCIe 3.0 连接可能不稳定。

#### 通过 config.txt

连接已被证明符合 Gen 2.0 速度（5 GT/sec），但你可以强制使用 Gen 3.0（10 GT/sec）速度。要启用 PCIe Gen 3.0 速度，请向 /boot/firmware/config.txt 添加以下行：

```
dtparam=pciex1_gen=3
```

重启你的 Raspberry Pi，并使用 sudo reboot 使这些设置生效。

#### 通过 raspi-config

运行以下命令打开树莓派配置 CLI：

```
$ sudo raspi-config
```

完成以下步骤以启用 PCIe Gen 3.0 速度：

1. 选择 Advanced Options。
2. 选择 PCIe Speed。
3. 选择 Yes 以启用 PCIe Gen 3 模式。
4. 选择 Finish 以退出。

使用 sudo reboot 重启你的 Raspberry Pi，以使这些设置生效。

## 电源按钮

>**注意**
>
>本小节仅适用于带有电源按钮的树莓派型号，如树莓派 5。

当你首次将树莓派插入电源时，不用按按钮，它可以自动引导并启动到操作系统。

如果你运行着桌面版树莓派，你可以通过短按电源按钮来执行彻底的关机。一个窗口将出现询问你是否要关机、重启或注销。

可选择菜单选项或者再次按下电源按钮以直接执行彻底关机。

>**注意**
>
如果你运行着桌面版树莓派，则可以通过连续快速地按两下电源按钮来关闭计算机。如果你运行着无桌面界面的树莓派操作系统精简版，则按一下电源按钮即可触发关机流程。

### 重启

如果树莓派主板已关闭但仍接入电源，按下电源按钮可重启。

>**注意**
>
>重置电源管理集成电路（PMIC）也可以重启。连接 HAT 会重置 PMIC。在连接 HAT 之前，应始终断开设备与电源的连接。

### 硬关机

要强制执行硬关机，请长按电源按钮。

### 添加你自己的电源按钮

![The J2 jumper on 树莓派 5](https://www.raspberrypi.com/documentation/computers/images/j2.jpg?hash=00e7c33a44c6f752d7818627617a44fb)

 J2 跳线帽

J2 跳线帽位于 RTC 电池连接器和主板边缘间。在此引出可以让你向树莓派 5 添加自己的电源按钮，方法是添加一个常开 (NO) 瞬时开关，将两个焊盘连接起来。短按此开关将执行与板载电源按钮相同的操作。

## 电源供应

树莓派型号的电源供应要求有所不同。所有型号都需要 5.1V 供应，但通常根据型号需要提高电流。到树莓派 3 为止的所有型号需要一个 micro USB 电源连接器，而树莓派 4、树莓派 400 和树莓派 5 使用 USB-C 连接器。

每个树莓派消耗的电流取决于连接的外围设备。

### 推荐的电源适配器

对于树莓派 1、2、3，我们推荐使用 2.5A micro USB 适配器。对于树莓派 4、400，我们推荐使用 3A USB-C 适配器。对于树莓派 5，我们推荐使用 27W USB-C 电源适配器。

>**注意**
>
>所有树莓派型号都不支持 USB-PPS。

>**注意**
>
>如果你使用第三方多接口的 USB-PD 电源适配器，在连接树莓派时，再插入其他设备会导致电源适配器与树莓派之间的重新协商。如果树莓派已开机，可无缝进行。但如果树莓派已关机，该协商可能造成树莓派重启。

### 以太网供电（PoE）连接器

![The PoE connector,width=](https://www.raspberrypi.com/documentation/computers/images/poe.jpg?hash=c85522d9ada495cda39eb5e7198205a5)

树莓派 5 PoE 扩展版

树莓派 5 上的以太网插孔支持 PoE +，支持 IEEE 802.3at-2009 PoE 标准。

树莓派 4B 和 3B +上的以太网插孔支持 PoE，支持 IEEE 802.3af-2003 PoE 标准。

所有具有 PoE 兼容以太网插孔的树莓派型号都需要通过以太网 port 绘制电源的 HAT。对于支持 PoE 的型号，我们建议使用 PoE HAT。对于支持 PoE + 的型号，我们建议使用 PoE + HAT。

### 典型功率要求

| 产品               | 推荐的 PSU 电流容量 | 最大总 USB 外设电流吸收                        | 典型裸板活动电流消耗 |
| -------------------- | --------------------- | ------------------------------------------------ | ---------------------- |
| 树莓派 1A   | 700mA            | 500mA                                       | 200mA             |
| 树莓派 1B | 1.2A                | 500mA                                       | 500mA             |
| 树莓派 1A+     | 700mA            | 500mA                                       | 180mA             |
| 树莓派 1B+     | 1.8A                | 1.2A                                           | 330mA             |
| 树莓派 2B      | 1.8A                | 1.2A                                           | 350mA             |
| 树莓派 3B    | 2.5A                | 1.2A                                           | 400mA             |
| 树莓派 3A+   | 2.5A                | 仅受电源、主板和连接器评级限制。     | 350mA             |
| 树莓派 3B+     | 2.5A                | 1.2A                                           | 500mA             |
| 树莓派 4B    | 3.0A                | 1.2A                                           | 600mA             |
| 树莓派 5           | 5.0A                | 1.6A（如果使用 3A 电源则为 600mA） | 800mA           |
| 树莓派 400         | 3.0A                | 1.2A                                           | 800mA             |
| 树莓派 Zero        | 1.2A                | 仅受电源、板卡和连接器评级限制                 | 100mA             |
| 树莓派 Zero W      | 1.2A                | 受电源、主板和连接器额定值的限制。   | 150mA             |
| 树莓派 Zero 2 W    | 2A                  | 仅受电源、主板和连接器额定值限制。   | 350mA                |

>**注意**
>
>当连接到 5A，+5V（25W）的电源能力的适配器时，树莓派 5 可为下游 USB 外设提供 1.6A 的电源。当连接到其他兼容的电源时，树莓派 5 将限制下游 USB 设备的电源为 600mA。

大多数树莓派能提供足够的电流给 USB 外设，可供应大多数 USB 设备，包括键盘、鼠标和适配器。然而，某些设备需要额外的电流，比如调制解调器、外部磁盘和大功率天线。如果要连接某 USB 设备，但是其电力需求超过了上表中指定的数值，请使用带外部供电的 USB 集线器。

如果你在树莓派上使用各种接口，其电力需求会增加。GPIO 引脚总共可安全供给 50mA；每个引脚最多可单独供给 16mA。HDMI 使用 50mA。相机模块需要 250mA。USB 键盘和鼠标可消耗从 100mA 到 1000mA 不等的电流。请检查你准备连接到树莓派的设备的功率，并相应购买适配器。如果不确定，请使用带外部供电的 USB 集线器。

运行以下命令检查输出到 USB 的电力状态：

```
$ vcgencmd get_config usb_max_current_enable
```

以下表格总结了不同树莓派型号在各种工作负载期间所绘制的功率（A）量：

|                   |      | 树莓派 1B+ | 树莓派 2B | 树莓派 3B | 树莓派 Zero | 树莓派 4B |
| ------------------- | ------ | ------------ | ----------- | ----------- | ------------- | ----------- |
| 引导              | 最大 | 0.26       | 0.40      | 0.75      | 0.20        | 0.85      |
|                   | 平均 | 0.22       | 0.22      | 0.35      | 0.15        | 0.7       |
| 闲置              | 平均 | 0.20       | 0.22      | 0.30      | 0.10        | 0.6       |
| 视频播放（H.264） | 最大 | 0.30       | 0.36      | 0.55      | 0.23        | 0.85      |
|                   | 平均 | 0.22       | 0.28      | 0.33      | 0.16        | 0.78      |
| 压力              | 最大 | 0.35       | 0.82      | 1.34      | 0.35        | 1.25      |
|                   | 平均 | 0.32       | 0.75      | 0.85      | 0.23        | 1.2       |
| 停止当前          |      |            |           | 0.10      | 0.055       | 0.023     |

>**注意**
>
>这些测量基于标准的树莓派系统镜像（截至 2016 年 2 月 26 日或 2019 年 6 月对于树莓派 4），室温，树莓派 连接到了 HDMI 显示器、USB 键盘和 USB 鼠标。树莓派 3 A 连接到了无线局域网接入点，树莓派 4 连接到了以太网。所有这些功耗测量均为近似值，并未考虑来自额外 USB 设备的功耗；如果连接了多个额外 USB 设备或 HAT，功耗很容易超过这些测量值。

##### [树莓派 4 和计算模块 4 上的额外 PMIC 功能](https://pip.raspberrypi.com/categories/685-whitepapers-app-notes/documents/RP-004340-WP/Extra-PMIC-features-on-Raspberry-Pi-4-and-Compute-Module-4.pdf)

树莓派 4 和计算模块 4 上的额外 PMIC 功能

树莓派 4 和 CM4 上使用了多种不同的 PMIC 设备。所有这些 PMIC 都提供了额外的功能，除了电压供应之外。本文档描述了如何在软件中访问这些功能。

#### 降低树莓派 5 关机后的功率

默认情况下，树莓派 5 关闭后仍会消耗电力，约 1 瓦至 1.4 瓦。可以减少这种功率消耗：手动编辑 EEPROM 配置来，使用 sudo rpi-eeprom-config -e。将设置更改为以下内容：

```
BOOT_UART=1
POWER_OFF_ON_HALT=1
BOOT_ORDER=0xf416
```

在关机后，功耗应该会降至约 0.01 W。

### 电源供应警告

从树莓派 B+（2014 年）以来的所有型号，除了 Zero 系列，都配备了低电压检测电路，如检测到供电电压低于 4.63 V（±5%），将在内核日志中打印一行条目。

如果你看到警告，请切换到更高质量的电源适配器和电线。劣质电源会损坏存储甚至引发树莓派产生未知行为。

电压会因多种原因而降低：你可能已将太多高需求的 USB 设备插入；电源适配器供应可能不足；接入适配器的电线可能过细。

##### [制作更具弹性的文件系统](https://pip.raspberrypi.com/categories/685-whitepapers-app-notes/documents/RP-003610-WP/Making-a-more-resilient-file-system.pdf)

创建更具弹性的文件系统

树莓派设备经常用作数据存储和监控设备，通常在可能发生意外断电的地方使用。与所有计算设备一样，电力中断可能造成存储损坏。

本白皮书提供了一些选项，介绍如何通过选择适当的文件系统和设置来防止在以上以及其他情况下的数据损坏，以确保数据完整性。

### 电源和树莓派系统

引导加载程序通过设备树 /proc/device-tree/chosen/power 传递有关电源供应的信息。用户通常不会直接阅读此信息。

max_current max 电流（单位：mA）

PDO 转储 - 高级用户的调试

是否将电流限制器设置为高或低

在将控制权转移给操作系统之前，启动期间是否发生任何 USB 超电流

重置事件 PMIC 重置原因，例如看门狗、过压或欠压、过温

PMIC 具有内置的 ADC，可以测量供电电压 EXT5V_V 等等。使用以下命令查看 ADC 测量值：

```
$ vcgencmd pmic_read_adc
```

你无法看到 USB 电流或其他直接连接到 5V 的设备，因为这将绕过 PMIC。你不应该期望这些值加起来等于电源供应的 W 数。但是，监视核心电压等事项可能很有用。

### 反向供电

USB 规范要求 USB 设备不能向上游设备供电。如果 USB 设备向上游设备供电，则称为反向供电。通常是因为连接了劣质的带供电的 USB 集线器，并且会导致带电 USB 集线器向主机的 树莓派 供电。不建议这么做，因为通过集线器向 树莓派 供电将绕过内置在树莓派中的保护电路，使其在发生电涌时易受损坏。

## 实时时钟（RTC）

树莓派 5 内置了一个 RTC 模块。它通过位于 USB-C 电源连接器右侧，主板上的 J5（BAT）连接器接入电池供电。

![The J5 battery connector](https://www.raspberrypi.com/documentation/computers/images/j5.png?hash=70853cc7a9a01cd836ed8351ece14d59)

J5 电池连接器

你可以设置唤醒闹钟，将主板切换至极低功耗状态（约 3mA）。达到闹钟时间时，主板将重新上电。这对像延时图像这样的周期性任务非常有用。

编辑引导加载程序配置以支持唤醒警报的低功率模式：

```
$ sudo -E rpi-eeprom-config --edit
```

添加以下两行。

```
POWER_OFF_ON_HALT=1
WAKE_ON_GPIO=0
```

你可以使用以下方式测试功能：

```
$ echo +600 | sudo tee /sys/class/rtc/rtc0/wakealarm
$ sudo halt
```

将会使板进入极低功耗状态，然后在 10 分钟后唤醒并重启。

RTC 还提供了启动时的时间，例如 dmesg，适用于缺乏 NTP 访问权限的用例：

```
[    1.295799] rpi-rtc soc:rpi_rtc: setting system clock to 2023-08-16T15:58:50 UTC (1692201530)
```

>**注意**
>
>即使没有备用电池连接到 J5 连接器，RTC 仍然可用。

### 添加备用电池

![Lithium-manganese rechargeable RTC battery](https://www.raspberrypi.com/documentation/computers/images/rtc-battery.jpg?hash=1a1bf655f9bce54c3b4c0a345f3e025c)

锂锰可充电 RTC 电池

官方电池部件是一枚可充电的锂锰硬币电池，配有预装的两针 JST-SH 插头和粘性安装触点。适用于在主板的主电源断开时为 RTC 供电。由于关机时的电流吸收为个位数µA，可保持时间为几个月。

>**注意**
>
>不建议把大部分（非可充电）锂电池用作 RTC 的备用电源。RTC 的备用电流消耗要高于大多数专用 RTC 模块，使用寿命将非常短暂。

>**警告**
>
>不要使用锂离子电池作为 RTC 的电源。

### 启用电池充电

RTC 配备了恒流（3mA）恒压充电器。

默认情况下，禁用电池充电。有 sysfs 个文件显示充电电压和限制：

```
/sys/devices/platform/soc/soc:rpi_rtc/rtc/rtc0/charging_voltage:0
/sys/devices/platform/soc/soc:rpi_rtc/rtc/rtc0/charging_voltage_max:4400000
/sys/devices/platform/soc/soc:rpi_rtc/rtc/rtc0/charging_voltage_min:1300000
```

要以设定电压为电池充电，请添加 rtc_bbat_vchg 到 /boot/firmware/config.txt ：

```
dtparam=rtc_bbat_vchg=3000000
```

重启以使用新的电压设置。检查 sudo reboot 文件，确保充电电压已正确设置。

### 禁用电池充电

要停止充电，请从 config.txt 中删除包含 rtc_bbat_vchg 的所有行。

## 串行外围设备接口（SPI）

树莓派计算机配备多个 SPI 总线。SPI 可用于连接各种外围设备 - 显示器、网络控制器（以太网、CAN 总线）、UART 等。这些设备最好由内核设备驱动程序支持，但 spidev API 允许用多种语言编写用户空间驱动程序。

### SPI 硬件

树莓派 Zero, 1, 2 和 3 都有三个 SPI 控制器：

* U 盘，在所有树莓派的引脚上都有两个硬件芯片选择信号；还有一种仅适用于 Compute 模块的备用映射。
* U 盘，在除早期树莓派 1 A 和 A 之外的所有树莓派型号上都有三个硬件芯片选择信号。
* SPI2，也具有三个硬件芯片选择器，仅在计算模块 1、3 和 3+ 上可用。

在树莓派 4、400，计算模块 4 上，还有四个额外的 SPI 总线：SPI3 到 SPI6，每个总线都有两个硬件芯片选择器。这些额外的 SPI 总线可通过某些 GPIO 引脚的替代功能分配来使用。有关更多信息，请参阅 BCM2711 Arm 外围设备数据表。

BCM2835 Arm 外围设备数据表的第 10 章介绍了主控制器。第 2.3 章说明了辅助控制器。

#### 引脚/GPIO 映射

##### SPI0

| SPI 功能 | 母座引脚 | 博通引脚名称 | 博通引脚功能 |
| ---------- | ---------- | ------------------- | ------------------- |
| `MOSI`         | 19       | `GPIO10`                  | `SPI0_MOSI`                  |
| `MISO`         | 21       | `GPIO09`                  | `SPI0_MISO`                  |
| `SCLK`         | 23       | `GPIO11`                  | `SPI0_SCLK`                  |
| `CE0`         | 24       | `GPIO08`                  | `SPI0_CE0_N`                  |
| `CE1`         | 26       | `GPIO07`                  | `SPI0_CE1_N`                  |

##### SPI0 备用镜像（仅限计算模块，不包括 CM4）

| SPI 功能 | 博通引脚名称 | 博通引脚功能 |
| ---------- | ------------------- | ------------------- |
| `MOSI`         | `GPIO38`                  | `SPI0_MOSI`                  |
| `MISO`         | `GPIO37`                  | `SPI0_MISO`                  |
| `SCLK`         | `GPIO39`                  | `SPI0_SCLK`                  |
| `CE0`         | `GPIO36`                  | `SPI0_CE0_N`                  |
| `CE1`         | `GPIO35`                  | `SPI0_CE1_N`                  |

##### SPI1

| SPI 功能 | 母座引脚 | 博通引脚名称 | 博通引脚功能 |
| ---------- | ---------- | ------------------- | ------------------- |
| `MOSI`         | 38       | `GPIO20`                  | `SPI1_MOSI`                  |
| `MISO`         | 35       | `GPIO19`                  | `SPI1_MISO`                  |
| `SCLK`         | 40       | `GPIO21`                  | `SPI1_SCLK`                  |
| `CE0`         | 12       | `GPIO18`                  | `SPI1_CE0_N`                  |
| `CE1`         | 11       | `GPIO17`                  | `SPI1_CE1_N`                  |
| `CE2`         | 36       | `GPIO16`                  | `SPI1_CE2_N`                  |

##### SPI2（仅适用于计算模块，不含 CM4）

| SPI 功能 | 博通引脚名称 |博通引脚功能 |
| ---------- | ------------------- | ------------------- |
| `MOSI`         | `GPIO41`                  | `SPI2_MOSI`                  |
| `MISO`         | `GPIO40`                  | `SPI2_MISO`                  |
| `SCLK`         | `GPIO42`                  | `SPI2_SCLK`                  |
| `CE0`         | `GPIO43`                  | `SPI2_CE0_N`                  |
| `CE1`         | `GPIO44`                  | `SPI2_CE1_N`                  |
| `CE2`         | `GPIO45`                  | `SPI2_CE2_N`                  |

##### SPI3（仅限 BCM2711）

| SPI 功能 | 母座引脚 | 博通引脚名称 |博通引脚功能 |
| ---------- | ---------- | ------------------- | ------------------- |
| `MOSI`         | 03       | `GPIO02`                  | `SPI3_MOSI`                  |
| `MISO`         | 28       | `GPIO01`                  | `SPI3_MISO`                  |
| `SCLK`         | 05       | `GPIO03`                  | `SPI3_SCLK`                  |
| `CE0`         | 27       | `GPIO00`                  | `SPI3_CE0_N`                  |
| `CE1`         | 18       | `GPIO24`                  | `SPI3_CE1_N`                  |

##### SPI4（仅限 BCM2711）

| SPI 功能 | 母座引脚 | 博通引脚名称 | 博通引脚功能 |
| ---------- | ---------- | ------------------- | ------------------- |
| `MOSI`         | 31       | `GPIO06`                  | `SPI4_MOSI`                  |
| `MISO`         | 29       | `GPIO05`                  | `SPI4_MISO`                  |
| `SCLK`         | 26       | `GPIO07`                  | `SPI4_SCLK`                  |
| `CE0`         | 07       | `GPIO04`                  | `SPI4_CE0_N`                  |
| `CE1`         | 22       | `GPIO25`                  | `SPI4_CE1_N`                  |

##### SPI5（仅限 BCM2711）

| SPI 功能 | 母座引脚| 博通引脚名称 | 博通引脚功能 |
| ---------- | ---------- | ------------------- | ------------------- |
| `MOSI`         | 08       | `GPIO14`                  | `SPI5_MOSI`                  |
| `MISO`         | 33       | `GPIO13`                  | `SPI5_MISO`                  |
| `SCLK`         | 10       | `GPIO15`                  | `SPI5_SCLK`                  |
| `CE0`         | 32       | `GPIO12`                  | `SPI5_CE0_N`                  |
| `CE1`         | 37       | `GPIO26`                  | `SPI5_CE1_N`                  |

##### SPI6（仅限 BCM2711）

| SPI 功能 | 母座引脚 | 博通引脚名称 | 博通引脚功能  |
| ---------- | ---------- | ------------------- | -------------------- |
| MOSI     | 38       | GPIO20            | SPI6\_MOSI      |
| MISO     | 35       | GPIO19            | SPI6\_MISO      |
| SCLK     | 40       | GPIO21            | SPI6\_SCLK      |
| CE0      | 12       | GPIO18            | SPI6\_CE0\_N |
| CE1      | 13       | GPIO27            | SPI6\_CE1\_N |

#### 主模式

信号名称缩写:

 SCLK 串行时钟

CEchip 启用（通常称为芯片选择）

MOSI 主发送从接收

MISO 主接收从发送

MOMI 主在主出

##### 标准模式

在标准 SPI 模式下，外设实现标准三线串行协议（SCLK，MOSI 和 MISO）。

##### 双向模式

在双向 SPI 模式中，实现了相同的 SPI 标准，只是使用单根导线传输数据（MOMI），而不是标准模式下使用的两根导线（MISO 和 MOSI）。在这种模式下，MOSI 引脚充当 MOMI 引脚。

##### 低速串行接口（LoSSI）模式

LoSSI 标准允许向外围设备（LCD）发出命令并在它们之间传输数据。LoSSI 命令和参数均为 8 位长，但额外的一位用于指示 B 是命令还是参数/数据。数据时此额外位设置为高位，命令时设置为低位。最终的 9 位值被串行化输出。LoSSI 常与 MIPI DBI 类型 C 兼容的 LCD 控制器一起使用。

>**注意**
>
>某些命令会触发 SPI 控制器自动读取，因此该模式不能用作多功能的 9 位 SPI。

#### 传输模式

* 轮询
* 中断
* DMA

#### 速度

CLK 寄存器的时钟分频器 (CDIV) 字段设置了 SPI 时钟速度:

SCLK 核心时钟 / CDIV

如果 CDIV 设置为 0，则除数为 65536。除数必须是 2 的倍数，奇数向下舍入。请注意，由于模拟电气问题（上升时间、驱动强度等），并非所有可能的时钟速率都可用。

查看 Linux 驱动程序部分获取更多信息。

#### 芯片选择

在 DMA 模式下操作时，与 CS 线的自动断言和取消断言相关的建立时间和保持时间如下：

* CS 线将在传输的第一个 B 的 msb 之前至少提前三个核心时钟周期。
* CS 线将在最后的时钟脉冲的下降沿后至少延迟一个核心时钟周期取消断言。

### SPI 软件

#### Linux 驱动程序

默认的 Linux 驱动程序是 spi-bcm2835 .

默认情况下，SPI0 已禁用。要启用，请使用 raspi-config，或确保 dtparam=spi=on 在 /boot/firmware/config.txt 中没有被注释掉。默认情况下，它使用两个芯片选择线，但可以使用 dtoverlay=spi0-1cs 将其减少到一个。还有 dtoverlay=spi0-2cs；没有任何参数时，它等同于 dtparam=spi=on。

要启用 SPI1，你可以使用 1、2 或 3 个芯片选择线。将适当的线添加到 /boot/firmware/config.txt 中：

```
#1 chip select
dtoverlay=spi1-1cs
#2 chip select
dtoverlay=spi1-2cs
#3 chip select
dtoverlay=spi1-3cs
```

类似的叠加层也适用于 SPI2、SPI3、SPI4、SPI5 和 SPI6。

驱动程序不使用硬件片选线，因为某些限制。相反，它可以使用任意数量的 GPIO 作为软件/GPIO 片选。这意味着你可以选择任何多余的 GPIO 作为 CS 线，所有这些 SPI 叠加层都包括该控制 - 详细信息请参见 /boot/firmware/overlays/README，或运行（例如） dtoverlay -h spi0-2cs （可能有助于列出所有这些）。

##### 速度

该驱动程序支持所有是核心时钟的偶数整除数的速度，尽管如上所述，并非所有这些速度都将支持数据传输，因为 GPIO 和连接的设备存在限制。作为经验法则，50MHz 以上的任何速度都不太可能工作，但具体情况可能有所不同。

##### 支持的模式位

 SPI_CPOL 时钟极性

 SPI_CPHA 时钟相位

SPI_CS_HIGH 芯片选择高电平

SPI_NO_CS1 每总线一个设备，无芯片选择

SPI_3WIRE 双向模式，数据输入输出引脚共享

双向模式，也称为 3 线模式，由 spi-bcm2835 内核模块支持。请注意，在此模式下，spi_transfer 结构体的 tx 或 rx 字段必须是 NULL 指针之一，因为只支持半双工通信。否则，传输将失败。spidev_test.c 源代码未正确考虑此情况，因此在 3 线模式下根本无法工作。

##### 支持的每字比特数

* 8 - 正常
* 9 - 支持使用 LoSSI 模式

##### 传输模式

所有 SPI 总线支持中断模式。SPI0 和 SPI3-6 还支持 DMA 传输。

##### SPI 驱动延迟

此线程讨论延迟问题。

#### spidev

spidev 提供了一个基于用户空间的单个 SPI CS 线接口。设备树用于指示 CS 线是由内核驱动模块驱动还是由 spidev 代表用户管理；不能同时两者都做。请注意，树莓派自己的内核对于使用设备树启用 spidev 更加宽松 - 上游内核会打印关于此类用法的警告，并最终可能完全阻止它。

##### 从 C 中使用 spidev

Linux 文档中有一个环回测试程序，可用作起点。请参阅故障排除部分。

##### 使用 spidev 从 Python

有几个 Python 库提供对 spidev 的访问，包括 spidev ( pip install spidev - see https://pypi.org/project/spidev/) 和 SPI-Py ( https://github.com/lthiery/SPI-Py)。

##### 使用 spidev 从像 bash 这样的 shell。

以下命令写入二进制 1、2 和 3：

```
$ echo -ne "\x01\x02\x03" > /dev/spidev0.0
```

#### 其他 SPI 库

还有其他用户空间库可以通过直接操作硬件来提供 SPI 控制：这并不推荐。

### 故障排除

#### 回环测试

这可以用来测试 SPI 发送和接收。在 MOSI 和 MISO 之间放一根电线。它不测试 CE0 和 CE1。

```
$ wget https://raw.githubusercontent.com/raspberrypi/linux/rpi-6.1.y/tools/spi/spidev_test.c
$ gcc -o spidev_test spidev_test.c
$ ./spidev_test -D /dev/spidev0.0
spi mode: 0
bits per word: 8
max speed: 500000 Hz (500 KHz)

FF FF FF FF FF FF
40 00 00 00 00 95
FF FF FF FF FF FF
FF FF FF FF FF FF
FF FF FF FF FF FF
DE AD BE EF BA AD
F0 0D
```

上述部分内容是从 elinux SPI 页面复制而来的，该页面也引用了这里。两者都受 CC-SA 许可协议保护。

## 通用串行总线（USB）

一般来说，Linux 支持的所有设备，树莓派都能用，尽管在树莓派 4 之前的型号上有一些限制。

### 最大功率输出

与所有计算机一样，树莓派上的 USB U 盘提供的功率有限。USB 设备通常因电力问题而出现故障。要排除电力不足引发问题的可能性，请使用带供电的集线器把 USB 设备接入树莓派。

| 型号         | USB U 盘的最大功率输出                                          |
| ---------------- | ----------------------------------------------------------------- |
| 树莓派 Zero, 1 | 每接口各 500mA^1^                                            |
| 树莓派 2, 3, 4 | 所有接口共 1200mA                                        |
| 树莓派 5 | 如果使用 3A 电源，电流为 600mA；如果使用 5A 电源，电流为 1600mA |

1. 对于早期的树莓派 1 A，限制为接口各 100mA。

### 树莓派 5

树莓派 5 需要高品质 USB-C 电源适配器才能启动，至少 +5V 3A（15W）。然而，用这样的电源适配器会限制外围设备的电流。如果你在首次启动时没有 +5V 5A 的电源适配器，操作系统会告警，外围设备的电流将受限为 600mA。

如果用户希望驱动大功率外设（如硬盘和固态硬盘），同时保留面对峰值工作负载仍有余量。应使用能够提供 +5V 5A（25W）的 USB-PD 电源适配器。如果树莓派 5 固件检测到了这样的电源适配器，它会把外设的 USB 电流限制缓解至 1.6A，为下游 USB 设备提供额外 5W 电力，并为主板上电力预算提供额外的 5W 电力。

>**注意**
>
>USB 和风扇接口共用电力预算。

### 树莓派 4

树莓派 4 提供了两个 USB 3.0 接口和两个 USB 2.0 接口，它们连接至 VL805 USB 控制器。四个接口上所有的 USB 2.0 均连接到了 VL805 内的单个 USB 2.0 集线器。这限制了 USB 1.1 和 USB 2.0 设备的总可用带宽与单个 USB 2.0 接口保持一致。

树莓派 4 老版本上 USB Type C 接口使用的 USB 控制器，默认情况下被禁用。

### 树莓派 Zero，1，2 和 3

树莓派 1 代 B+、树莓派 2 和树莓派 3 主板提供四个 USB 2.0 ports。树莓派 Zero 主板配备一个 micro USB on-the-go (OTG) port。

树莓派 4 之前的型号上的 USB 控制器仅对某些设备提供基本支持，这会带来较高的软件处理开销。它仅支持一个根 USB 接口：所有连接设备的流量都通过此单一总线传输，该总线的最大速度为 480Mbps。

USB 2.0 规范定义了三种设备速度 - 低速、全速和高速。大多数鼠标和键盘是低速设备，大多数 USB 声音设备是全速设备，而大多数视频设备（网络摄像头或视频捕捉器）是高速设备。

若把多个高速 USB 设备同时接入树莓派，通常没有问题。

与低速和全速设备通信时产生的软件开销意味着同时活动的低速和全速设备数量会受限制。连接少量这些类型设备到树莓派不会造成问题。

### 已知的 USB 故障

#### 与 USB 3.0 集线器的互操作性

在使用全速或低速设备（包括大多数鼠标和键盘）时，与 USB 3.0 集线器一起使用的问题。大多数 USB 3.0 集线器硬件中存在的一个错误意味着在连接到 USB 3.0 集线器的全速或低速设备时，树莓派 4 之前的型号无法与这些设备通信。

当通过 USB 3.0 集线器接入时，USB 2.0 高速设备（包括 USB 2.0 集线器）可正确运行。

避免将低速或全速设备连接到 USB 3.0 集线器。作为解决方法，将 USB 2.0 集线器插入 USB 3.0 集线器的下游 port，然后将低速设备连接，或者在树莓派和 USB 3.0 集线器之间使用 USB 2.0 集线器，然后将低速设备插入 USB 2.0 集线器。

#### USB 1.1 网络摄像头

旧的网络摄像头可能是全速设备。因为这些设备传输大量数据并产生额外的软件开销，无法保证可靠运行。作为解决方法，请尝试以分辨率调用摄像头。

#### 世异 USB 声卡

昂贵的发烧友级声卡通常占用了大量的 USB 带宽。不能保证与 96kHz/192kHz DAC 的可靠操作。作为一种解决方法，强制输出流为 CD 音质（44.1kHz/48kHz 16 位）将带宽降低到可靠水平。

#### 单个 TT USB 集线器

USB 2.0 和 3.0 集线器具有一种机制，用于与连接到其下游接口的全速或低速设备通信，称为事务转换器 (TT)。此设备缓冲来自主机的高速请求，并将它们以全速或低速传输给下游设备。USB 规范允许两种集线器配置：单个 TT (所有接口共用一个 TT) 和多个 TT (每个 port 一个 TT)。由于硬件限制，如果将太多全速或低速设备插入单个 TT 集线器，这些设备可能会表现不可靠。建议使用多个 TT 集线器与多个全速和低速设备进行接口处理。作为解决方法，将全速和低速设备分散放置在树莓派自己的 USB 接口 和单个 TT 集线器之间。

## 树莓派修订代码

每个不同的树莓派型号修订版都有一个唯一的修订代码。你可以通过运行以下命令查找树莓派的修订代码：

```
$ cat /proc/cpuinfo
```

最后三行显示硬件类型、修订代码和树莓派的唯一序列号。例如：

```
Hardware    : BCM2835
Revision    : a02082
Serial      : 00000000765fc593
```

>**注意**
>
>所有树莓派计算机报告 BCM2835，即使是带有 BCM2836、BCM2837、BCM2711 和 BCM2712 处理器的也一样。你不应该使用此字符串来检测处理器。使用下面的信息解码修订代码，或 cat /sys/firmware/devicetree/base/model。

### 旧式修订代码

树莓派的第一批型号从 0002 到 0015 分配了顺序十六进制修订代码：

| 代码 | 型号 | 修订 | RAM         | 制造商   |
| ------ | ------- | ------ | ------------- | ---------- |
| 0002 | B     | 1.0  | 256MB       | Egoman   |
| 0003 | B     | 1.0  | 256MB       | Egoman   |
| 0004 | B     | 2.0  | 256MB       | 索尼英国 |
| 0005 | B     | 2.0  | 256MB       | 佳世达     |
| 0006 | B     | 2.0  | 256MB       | Egoman   |
| 0007 | A     | 2.0  | 256MB       | Egoman   |
| 0008 | A     | 2.0  | 256MB       | 索尼英国 |
| 0009 | A     | 2.0  | 256MB       | 佳世达   |
| 000d | B     | 2.0  | 512MB       | Egoman   |
| 000e | B     | 2.0  | 512MB       | 索尼英国 |
| 000f | B     | 2.0  | 512MB       | Egoman   |
| 0010 | B+    | 1.2  | 512MB       | 索尼英国 |
| 0011 | CM1   | 1.0  | 512MB       | 索尼英国 |
| 0012 | A+  | 1.1  | 256MB       | 索尼英国 |
| 0013 | B+  | 1.2  | 512MB       | 英蓓特     |
| 0014 | CM1   | 1.0  | 512MB       | 英蓓特     |
| 0015 | A+    | 1.1  | 256MB/512MB | 英蓓特     |

### 新式修订代码

使用树莓派 2 的推出，引入了新样式的修订代码。不同于顺序的是，十六进制代码的每一位代表修订的一部分信息：

```
NOQuuuWuFMMMCCCCPPPPTTTTTTTTRRRR
```

| 部分                    | 代表        | 选项                      |
| ------------------------- | ------------- | --------------------------- |
| N（位 31）              | 过压        | 0：允许过压               |
|                         |             | 1：禁止过压               |
| O (位 30)               | OTP 程序^1^ | 0：允许 OTP 编程          |
|                         |             | 1：禁止 OTP 编程          |
| Q（位 29）              | OTP 读取^1^ | 0：允许 OTP 读取          |
|                         |             | 1：OTP 读取不允许         |
| uuu（位 26-28）         | 未使用      | 未使用                    |
| W（位 25）              | 保修位^2^   | 0: 担保保修有效           |
|                         |             | 1: 因超频而无效的保修保证 |
| u (位 24)               | 未使用      | 未使用                    |
| F（位 23）              | 新标志      | 1：新风格修订             |
|                         |             | 0：旧风格修订             |
| MMM（位于第 20-22 位）  | 存储器大小  | 0：256MB                  |
|                         |             | 1: 512MB                  |
|                         |             | 2: 1GB                    |
|                         |             | 3: 2GB                    |
|                         |             | 4：4GB                    |
|                         |             | 5：8GB                    |
| CCCC（位于 16-19 位）   | 制造商      | 0: 索尼英国               |
|                         |             | 1: Egoman                 |
|                         |             | 2: 英蓓特                 |
|                         |             | 3: 索尼日本               |
|                         |             | 4: 英蓓特                 |
|                         |             | 5：Stadium                 |
| PPPP（位 12-15）        | 处理器      | 0: BCM2835                |
|                         |             | 1: BCM2836                |
|                         |             | 2: BCM2837                |
|                         |             | 3: BCM2711                |
|                         |             | 4: BCM2712                |
| TTTTTTTT (位于 4-11 位) | 类型        | 0：A                      |
|                         |             | 1：B                      |
|                         |             | 2：A+                     |
|                         |             | 3：B+                     |
|                         |             | 4：2B                     |
|                         |             | 5：Alpha（早期原型）     |
|                         |             | 6：CM1                    |
|                         |             | 8：3B                     |
|                         |             | 9：Zero                     |
|                         |             | a：CM3                    |
|                         |             | c：Zero W                 |
|                         |             | d：3B+                    |
|                         |             | ext: e：3A+               |
|                         |             | f：仅供内部使用             |
|                         |             | 10：CM3+                  |
|                         |             | 11：4B                    |
|                         |             | 12：Zero 2 W              |
|                         |             | 13: 400                   |
|                         |             | 14：CM4                   |
|                         |             | 15：CM4S                  |
|                         |             | 16：仅供内部使用          |
|                         |             | 17: 5                     |
| RRRR（位 0-3）          | 修订        | 0、1、2 等。    |

^1^ 编程 OTP 位的信息。

^2^ 树莓派 4 上从不设置保修位。

### 使用新样式的修订代码

>**注意**
>
>此列表不是详尽无遗的 - 可能有正在使用但不在此表中的代码。请参阅下一节，了解如何使用修订代码来识别板子的最佳实践。

| 代码   | 型号              | 修订 | RAM   | 制造商   |
| -------- | -------------------- | ------ | ------- | ---------- |
| 900021 | A+                 | 1.1  | 512MB | 索尼英国 |
| 900032 | B+                 | 1.2  | 512MB | 索尼英国 |
| 900092 | Zero                 | 1.2  | 512MB | 索尼英国 |
| 900093 | Zero                 | 1.3  | 512MB | 索尼英国 |
| 9000c1 | Zero W             | 1.1  | 512MB | 索尼英国 |
| 9020   | 3A+                | 1.0  | 512MB | 索尼英国 |
| 90200  | 3A+                | 1.1  | 512MB | 索尼英国 |
| 920092 | Zero                 | 1.2  | 512MB | 英蓓特     |
| 920093 | Zero                 | 1.3  | 512MB | 英蓓特     |
| 900061 | CM1                | 1.1  | 512MB | 索尼英国 |
| a01040 | 2B                 | 1.0  | 1GB   | 索尼英国 |
| a01041 | 2B                 | 1.1  | 1GB   | 索尼英国 |
| a02082 | 3B                 | 1.2  | 1GB   | 索尼英国 |
| a020a0 | CM3                | 1.0  | 1GB   | 索尼英国 |
| a020d3 | 3B+                | 1.3  | 1GB   | 索尼英国 |
| a020d4 | 3B+                | 1.4  | 1GB   | 索尼英国 |
| a02042 | 2B（搭载 BCM2837） | 1.2  | 1GB   | 索尼英国 |
| a21041 | 2B                 | 1.1  | 1GB   | 英蓓特 |
| a22042 | 2B（搭载 BCM2837） | 1.2  | 1GB   | 英蓓特   |
| a22082 | 3B                 | 1.2  | 1GB   | 英蓓特     |
| a220a0 | CM3                | 1.0  | 1GB   | 英蓓特 |
| a32082 | 3B                 | 1.2  | 1GB   | 索尼日本 |
| a52082 | 3B                 | 1.2  | 1GB   | Stadium   |
| a22083 | 3B                 | 1.3  | 1GB   | 英蓓特     |
| a02100 | CM3+               | 1.0  | 1GB   | 索尼英国 |
| a03111 | 4B                 | 1.1  | 1GB   | 索尼英国 |
| b03111 | 4B                 | 1.1  | 2GB   | 索尼英国 |
| b03112 | 4B                 | 1.2  | 2GB   | 索尼英国 |
| b03114 | 4B                 | 1.4  | 2GB   | 索尼英国 |
| b03115 | 4B                 | 1.5  | 2GB   | 索尼英国 |
| c03111 | 4B                 | 1.1  | 4GB   | 索尼英国 |
| c03112 | 4B                 | 1.2  | 4GB   | 索尼英国 |
| c03114 | 4B                 | 1.4  | 4GB   | 索尼英国 |
| c03115 | 4B                 | 1.5  | 4GB   | 索尼英国 |
| d03114 | 4B                 | 1.4  | 8GB   | 索尼英国 |
| d03115 | 4B                 | 1.5  | 8GB   | 索尼英国 |
| c03130 | 树莓派 400         | 1.0  | 4GB   | 索尼英国 |
| a03140 | CM4                | 1.0  | 1GB   | 索尼英国 |
| b03140 | CM4                | 1.0  | 2GB   | 索尼英国 |
| c03140 | CM4                | 1.0  | 4GB   | 索尼英国 |
| d03140 | CM4                | 1.0  | 8GB   | 索尼英国 |
| 902120 | Zero 2 W             | 1.0  | 512MB | 索尼英国 |
| c04170 | 5                  | 1.0  | 4GB   | 索尼英国 |
| d04170 | 5                  | 1.0  | 8GB   | 索尼英国 |

### 使用修订代码进行板识别

从命令行，我们可以使用以下命令获取板的修订代码：

```
$ cat /proc/cpuinfo | grep Revision
Revision      : c03111
```

在上面的示例中，我们有一个十六进制的修订代码 c03111。将其转换为二进制，我们得到 0 0 0 000 0 0 1 100 0000 0011 00010001 0001。根据上表，已插入空格以显示修订代码的各部分之间的边界。

从最低阶位开始，底部的四位（0-3）是板子的修订号，所以这块板子的修订号是 1。接下来的八位（4-11）是板子类型，在这种情况下是二进制 00010001，十六进制 11，所以这是一个树莓派 4B。使用相同的过程，我们可以确定处理器是 BCM2711，板子由索尼英国制造，并且有 4GB 的 RAM。

#### 在你的程序中获取修订代码

很明显，有这么多编程语言，不可能为所有这些语言都举例，但这里有两个快速例子，分别针对 C 和 Python。这两个例子都使用系统调用运行一个 bash 命令，获取 cpuinfo 并将结果传送给 awk 以恢复所需的修订代码。然后，它们使用位操作来提取代码中的 New、Model 和 Memory 字段。

```
#include <stdio.h>
#include <stdlib.h>

int main( int argc, char *argv[] )
{
  FILE *fp;
  char revcode[32];

  fp = popen("cat /proc/cpuinfo | awk '/Revision/ {print $3}'", "r");
  if (fp == NULL)
    exit(1);
  fgets(revcode, sizeof(revcode), fp);
  pclose(fp);

  int code = strtol(revcode, NULL, 16);
  int new = (code >> 23) & 0x1;
  int model = (code >> 4) & 0xff;
  int mem = (code >> 20) & 0x7;

  if (new && model == 0x11 && mem >= 3)  // Note, 3 in the mem field is 2GB
     printf("We are a 4B with at least 2GB of RAM!\n" );

  return 0;
}
```

同样的 Python 代码：

```
import subprocess

cmd = "cat /proc/cpuinfo | awk '/Revision/ {print $3}'"
revcode = subprocess.check_output(cmd, shell=True)

code = int(revcode, 16)
new = (code >> 23) & 0x1
model = (code >> 4) & 0xff
mem = (code >> 20) & 0x7

if new and model == 0x11 and mem >= 3 : # Note, 3 in the mem field is 2GB
    print("We are a 4B with at least 2GB RAM!")
```

### 修订代码使用的最佳实践

为了避免在创建新的板卡版本时出现问题，请不要使用版本代码（例如 c03111 ）。

一个天真的实现使用一个支持的版本代码列表，将检测到的代码与该列表进行比较，以决定该设备是否受支持。当出现新的板卡版本或者生产地点发生变化时，这种方法就会失效：每次都会创建一个新的版本代码，而不在支持的版本代码列表中。这将导致同一板卡类型的新版本被拒绝，尽管它们始终保持向后兼容。每当出现新版本时，你都必须发布一个包含新版本代码的新支持的版本代码列表-这是一个繁重的支持负担。

相反，请使用以下方法之一：

* 根据板型字段（3A、4B 等）进行过滤，该字段表示但不表示修订版。
* 根据内存量字段进行过滤，因为 RAM 大致对应板的计算能力。

例如，你可以限制支持具有 2GB 或更多 RAM 的树莓派 4B 型号。上一节的示例使用了这种推荐方法。

>**注意**
>
>始终检查第 23 位，即“新”标志，以确保修订代码是新版本，然后再检查其他字段。

#### 检查树莓派型号和 CPU 跨发行版

在各个 Linux 发行版中，/proc/cpuinfo 的支持和格式会有所不同。要检查树莓派设备在任何 Linux 发行版（包括树莓派系统）上的型号或 CPU，请检查设备树：

```
$ cat /proc/device-tree/compatible | tr '\0' '\n'
raspberrypi,5-model-b
brcm,bcm2712
```

输出两个空值分隔的字符串值，每个字符串值包含逗号分隔的制造和型号。例如，树莓派 5 输出上述板和 CPU 字符串。这些对应以下值：

* raspberrypi （板制造）
* 5-model-b （板型号）
* brcm (CPU 品牌)
* bcm2712 (CPU 型号)

树莓派型号具有以下设备树数值：

| 设备名称                | 制造商 | 型号 | CPU 制造商 | CPU |
| ------------------------- | -------- | ------- | ------------ | ----- |
| 树莓派 5                | `raspberrypi`       | `5-model-b`      | `brcm`           | `bcm2712`    |
| 树莓派 400              | `raspberrypi`       | `400`      | `brcm`           | `bcm2711`    |
| 树莓派计算模块 4        | `raspberrypi`       | `4-compute-module`      | `brcm`           | `bcm2711`    |
| 树莓派 4A        | `raspberrypi`       | `4-model-a`      | `brcm`           | `bcm2711`    |
| 树莓派 4B        | `raspberrypi`       | `4-model-b`      | `brcm`           | `bcm2711`    |
| 树莓派计算模块 3        | `raspberrypi`       | `3-compute-module`      | `brcm`           | `bcm2837`    |
| 树莓派 3A+          | `raspberrypi`       | `3-model-a-plus`      | `brcm`           | `bcm2837`    |
| 树莓派 3B+          | `raspberrypi`       | `3-model-b-plus`      | `brcm`           | `bcm2837`    |
| 树莓派 3B           | `raspberrypi`       | `3-model-b`      | `brcm`           | `bcm2837`    |
| 树莓派 2B           | `raspberrypi`       | `2-model-b`      | `brcm`           | `bcm2836`    |
| 树莓派计算模块          | `raspberrypi`       | `compute-module`      | `brcm`           | `bcm2835`    |
| 树莓派 A+             | `raspberrypi`       | `model-a-plus`      | `brcm`           | `bcm2835`    |
| 树莓派 A+         | `raspberrypi`       | `model-b-plus`      | `brcm`           | `bcm2835`    |
| 树莓派 A 修订版 2 | `raspberrypi`       | `model-b-rev2`      | `brcm`           | `bcm2835`    |
| 树莓派 A          | `raspberrypi`       | `model-a`      | `brcm`           | `bcm2835`    |
| 树莓派 A          | `raspberrypi`       | `model-b`      | `brcm`           | `bcm2835`    |
| 树莓派 Zero 2 W         | `raspberrypi`       | `model-zero-2-w`      | `brcm`           | `bcm2837`    |
| 树莓派 Zero             | `raspberrypi`       | `model-zero`      | `brcm`           | `bcm2835`    |
| 树莓派 Zero W           | `raspberrypi`       | `model-zero-w`      | `brcm`           | `bcm2835`    |
