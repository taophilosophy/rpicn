# RP1

## 关于 RP1

![RP1 架构图](https://www.raspberrypi.com/documentation/microcontrollers/images/rp1.jpg)

RP1 是一款 12×12mm，引脚中心距为 0.65mm 的 BGA 南桥芯片，它为树莓派 5 提供了主要的 I/O（输入/输出）功能。

RP1 可提供：

* PCIe 2.0 x4
* 千兆以太网 MAC（GEM）控制器
* USB 3 主机控制器 x2
  * 每个都有 USB 3 x1 和 USB 2 x1 端口
  * USB 可用带宽是树莓派 4 的 2 倍
* SDIO 通道/eMMC x2（树莓派 5 未使用）
* MIPI 转换器 x2（4 通道，支持 DSI 和 CSI-2）
* 视频数模转换器（DAC）（3 通道，支持 PAL/NTSC 和 VGA）
  * 树莓派 5 仅使用单通道（复合视频）
* 低速外围设备（SPI、UART、I²C、PWM、GPIO、I²S）
* Delta-sigma（Σ-Δ）脉宽调制（PWM）音频输出

可在 [RP1 外围设备](https://datasheets.raspberrypi.com/rp1/rp1-peripherals.pdf?_gl=1*1ldjb52*_ga*ODAwMTM3MTg4LjE3MTc1NzY1NTQ.*_ga_22FD70LWDS*MTcyMjUyNTM0MC43OC4xLjE3MjI1MjUzNzIuMC4wLjA.)文档中找到更多有关 RP1 的信息。
