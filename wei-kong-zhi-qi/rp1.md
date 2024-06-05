# RP1

## 关于 RP1

![Architecture diagram of the RP1](https://www.raspberrypi.com/documentation/microcontrollers/images/rp1.jpg)

 架构

RP1 是一款 12×12mm，0.65mm 间距的 BGA 南桥芯片，为 Raspberry Pi 5 提供了大部分 I/O 功能。

 它提供：

* 4 通道 PCIe 2.0 端点
* 千兆以太网 MAC
* 2× USB 3 主机控制器

  * 每个都有 1× USB 3 和 1× USB 2 端口
  * 与 Raspberry Pi 4 相比，可用的 USB 带宽超过两倍
* 2× SDIO 端口/eMMC（不在 Raspberry Pi 5 上使用）
* 2× MIPI 转换器（4 通道，支持 DSI 和 CSI-2）
* 视频 DAC（3 通道，支持 PAL/NTSC 和 VGA）

  * 仅在 Raspberry Pi 5 上使用一个通道（复合）
* 低速外围设备（SPI、UART、I2C、PWM、GPIO、I2S）
* Delta-sigma PWM 音频输出

RP1 的更多信息可以在 RP1 外围设备文档中找到。
