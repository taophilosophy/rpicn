# RP1

## 关于 RP1

![Architecture diagram of the RP1](https://www.raspberrypi.com/documentation/microcontrollers/images/rp1.jpg)

 架构

RP1 是一款 12×12mm，间距为 0.65mm 的 BGA 南桥芯片，它为树莓派 5 提供了大部分 I/O 功能。

 它提供了：

* 4 通道 PCIe 2.0
* 千兆以太网 MAC
* 2× USB 3 主机控制器
  * 每个都有 1× USB 3 和 1× USB 2 通道
  * 与树莓派 4 相比，USB 可用带宽超过两倍
* 2× SDIO 通道/eMMC（树莓派 5 上未使用）
* 2× MIPI 转换器（4 通道，支持 DSI 和 CSI-2）
* 视频 DAC（3 通道，支持 PAL/NTSC 和 VGA）
  * 树莓派 5 上仅使用了单通道（复合）
* 低速外围设备（SPI、UART、I2C、PWM、GPIO、I2S）
* Delta-sigma PWM 音频输出

可以在 RP1 外围设备文档中找到更多关于 RP1 的信息。
