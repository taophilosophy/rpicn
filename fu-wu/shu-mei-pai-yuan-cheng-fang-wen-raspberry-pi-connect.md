# 树莓派远程访问（Raspberry Pi Connect）

## 介绍

Raspberry Pi Connect 可安全访问您的 Raspberry Pi，无论身在何处。

![hero](https://www.raspberrypi.com/documentation/services/images/hero.png)

要使用 Connect，请在您的 Raspberry Pi 上安装 Connect 软件。然后访问 connect.raspberrypi.com，在浏览器窗口中通过屏幕共享访问您的 Raspberry Pi。您可以像将显示器插入 Raspberry Pi 一样使用桌面。

Connect 使用安全加密连接。默认情况下，Connect 在您的 Raspberry Pi 和浏览器之间直接通信。但是，当 Connect 无法在您的 Raspberry Pi 和浏览器之间建立直接连接时，我们会在伦敦使用中继服务器。在这种情况下，Raspberry Pi 仅保留操作 Connect 所需的元数据。

## 安装

Connect 需要运行 64 位 Raspberry Pi OS Bookworm 的 Raspberry Pi，该 OS 使用 Wayland 窗口服务器。所需的 OS 版本需要 Raspberry Pi 5、Raspberry Pi 4 或 Raspberry Pi 400。

| NOTE | Connect 不兼容 Raspberry Pi OS Lite 或使用 X windows 服务器的系统。 |
| ------ | ----------------------------------------------------------------- |

要开始安装，请打开一个终端窗口。运行以下命令来更新您的系统和软件包：

```
$ sudo apt update
$ sudo apt upgrade
```

### 安装 Connect

在您的 Raspberry Pi 上运行以下命令以安装 Connect：

```
$ sudo apt install rpi-connect
```

安装完成后，重新启动您的 Raspberry Pi 以启动 Connect 服务：

```
$ sudo reboot
```

下次登录 Raspberry Pi 时，Connect 将自动启动。

### 开始连接

| NOTE | 默认情况下，连接会在登录时自动启动。除非您从登录项中删除它，否则无需手动启动连接。 |
| ------ | ------------------------------------------------------------------------------------ |

要从命令行手动启动服务，请运行以下命令：

```
$ systemctl --user start rpi-connect
```

## 使用连接

现在您已经在您的 Raspberry Pi 上安装了 Connect，您必须将您的 Raspberry Pi 与您的 Raspberry Pi ID 关联起来才能使用 Connect。

如果您没有 Raspberry Pi ID，请创建一个。

### 链接您的 Raspberry Pi 和 Raspberry Pi ID

要将您的 Raspberry Pi 与您的 Raspberry Pi ID 链接起来，请使用 Connect 生成验证 URL。访问该 URL 并登录您的 Raspberry Pi ID 以将您的 Raspberry Pi 添加到您的帐户。

您可以使用 Raspberry Pi 桌面上的 Connect 图标或 rpi-connect CLI 生成验证 URL。

#### 通过 Raspberry Pi 桌面

一旦 rpi-connect 服务开始运行，系统托盘中会出现连接图标。

![just installed](https://www.raspberrypi.com/documentation/services/images/just_installed.png)

点击连接图标，从下拉菜单中选择“登录”。这将打开一个验证 URL，您可以使用它将您的 Raspberry Pi 链接到您的 Raspberry Pi ID。

![sign in](https://www.raspberrypi.com/documentation/services/images/sign-in.png)

#### 通过命令行

使用以下命令生成一个链接，该链接将连接您的 Raspberry Pi 与您的 Raspberry Pi ID：

```
$ rpi-connect signin
```

此命令应该输出类似以下内容：

```
Complete sign in by visiting https://connect.raspberrypi.com/verify/XXXX-XXXX
```

访问任何设备上的 URL，将您的 Raspberry Pi 与您的 Raspberry Pi ID 链接起来。

#### 在 Connect 中完成 Raspberry Pi 的链接。

访问在上一步骤中生成的验证 URL。

使用您的 Raspberry Pi ID 登录 Connect。

![login with id](https://www.raspberrypi.com/documentation/services/images/login-with-id.png)

验证后，为您的 Raspberry Pi 分配一个名称。选择一个能帮助您识别设备的名称。单击“创建设备并登录”按钮继续。

![create device](https://www.raspberrypi.com/documentation/services/images/create-device.png)

您现在可以从您的 Raspberry Pi 进行屏幕共享。Connect 系统托盘图标将变为蓝色，表示您的 Raspberry Pi 已连接到 Connect 服务。您应该收到一封电子邮件通知，指示新设备已登录到 Connect。

![sign in email](https://www.raspberrypi.com/documentation/services/images/sign-in-email.png)

| WARNING | 如果收到一封电子邮件，说有一台您不认识的设备登录了 Connect，请立即更改您的 Raspberry Pi ID 密码。从 Connect 中移除该设备，以永久取消与您的帐户的关联。考虑启用双因素身份验证，以保护您的帐户安全。 |
| --------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

![linked with](https://www.raspberrypi.com/documentation/services/images/linked-with.png)

单击 Connect 系统托盘图标以打开 Connect 菜单。该菜单显示您当前的登录状态，一个登出选项，以及一个启用或禁用屏幕共享的选项。

| NOTE | 您还可以使用终端命令 rpi-connect signout 从 Connect 中移除您的 Raspberry Pi。 |
| ------ | ------------------------------------------------------------------------------- |

通过设备序列号连接标志通信。在设备之间移动 SD 卡会使您从 Connect 中注销。

### 连接到您的 Raspberry Pi

现在您的 Raspberry Pi 已在 Connect Web 门户中列出，您可以仅使用浏览器在任何地方共享您的 Raspberry Pi 屏幕。

在任何计算机上访问 connect.raspberrypi.com。

连接会将您重定向到 Raspberry Pi ID 服务以进行登录。登录后，Connect 会显示已链接设备的列表。可用于屏幕共享的设备在设备名称下方显示灰色的屏幕共享标签。

![list of devices](https://www.raspberrypi.com/documentation/services/images/list-of-devices.png)

单击您想要屏幕共享的设备右侧的“连接”按钮。这将打开一个浏览器窗口，显示您的 Raspberry Pi 的桌面。

![connecting](https://www.raspberrypi.com/documentation/services/images/connecting.png)

您现在可以像在本地一样使用您的 Raspberry Pi。有关连接的更多信息，请将鼠标悬停在断开按钮右侧的挂锁图标上。

![session start](https://www.raspberrypi.com/documentation/services/images/session-start.png)

| TIP | 使用桌面上方的从远程复制和粘贴到远程按钮在本地和远程剪贴板之间复制。 |
| ----- | ---------------------------------------------------------------------- |

连接后，在连接门户中的屏幕共享标签旁会出现一个绿点。这表示活动屏幕共享会话。悬停以查看当前屏幕共享会话数。

![connect service connected](https://www.raspberrypi.com/documentation/services/images/connect-service-connected.png)

系统托盘中的连接图标在屏幕共享会话进行时会变为紫色，并显示一个闭合的圆圈。

![pi desktop connected](https://www.raspberrypi.com/documentation/services/images/pi-desktop-connected.png)

### 从您的 Raspberry Pi 断开连接

要关闭屏幕共享会话，请单击桌面上方的断开按钮。

![session end](https://www.raspberrypi.com/documentation/services/images/session-end.png)

### 禁用屏幕共享

要关闭屏幕共享，请单击连接系统托盘图标，取消选择允许屏幕共享。连接系统托盘图标的下部将变为灰色。您仍然登录到连接，但您的屏幕无法共享。

![no sharing](https://www.raspberrypi.com/documentation/services/images/no-sharing.png)

在连接门户中，与该 Raspberry Pi 旧版旁边的连接按钮将消失，屏幕共享标签将显示为带有删除线。

![no connect button ui](https://www.raspberrypi.com/documentation/services/images/no-connect-button-ui.png)

要重新启用屏幕共享，请执行以下操作之一：

* 单击连接系统托盘图标，然后选择允许屏幕共享
* 运行终端命令 rpi-connect vnc on

### 管理您的 Raspberry Pi

连接列出与您的 Raspberry Pi ID 关联的所有 Raspberry Pi。每个设备都有一个“连接”按钮，用于打开屏幕共享会话（如果该设备已启用屏幕共享）。每个设备的设备名称下都有一组标签，指示可用服务。

![list of devices](https://www.raspberrypi.com/documentation/services/images/list-of-devices.png)

单击设备名称以打开设备详细信息页面。此屏幕提供有关您的设备的低级信息。您还可以编辑设备名称或从“连接”中删除设备。

![device details](https://www.raspberrypi.com/documentation/services/images/device-details.png)

从 Connect 中删除设备会自动注销设备上的 Connect。Connect 系统托盘图标会变为灰色，菜单只提供“登录”选项。

### 更新 Connect

要更新到最新版本的 Connect，请运行以下命令：

```
$ sudo apt update
$ sudo apt install --only-upgrade rpi-connect
```

重新启动设备以使更新生效：

```
$ sudo reboot
```

### 卸载 Connect

运行以下命令从 Raspberry Pi 中移除 Connect 软件：

```
$ sudo apt remove --purge rpi-connect
```

卸载后，Raspberry Pi 的序列号仍与您的 Raspberry Pi ID 关联。设备仍然显示在 Connect 门户中，但无法用于屏幕共享。如果您在同一台 Raspberry Pi 上再次安装 Connect，即使使用不同的 SD 卡，它也将在 Connect 门户中重用现有设备名称。

要切断 Raspberry Pi 与 Raspberry Pi ID 之间的链接，请从 Connect 门户的设备列表中删除 Raspberry Pi。

## 故障排除

### 已知问题

* Connect 仅支持共享 Raspberry Pi 的单个主显示屏。当 Raspberry Pi 连接到多个 HDMI 屏幕时，Connect 有时会共享辅助屏幕的内容。您可以通过右键单击桌面并在“桌面首选项”中更改任务栏位置来解决此问题。
* Connect 不支持屏幕键盘。为了实现完整功能，请使用物理键盘。
* Connect 需要使用实现 ECMAScript 2020（ES11）的浏览器，因为它使用了旧版浏览器中不可用的功能。
* 浏览器拦截某些键和键组合。因此，您无法将这些键输入到您的 Connect 窗口中。Connect 提供了一个工具栏来模拟一些最受欢迎的被拦截键。

### 启用增强日志记录

您可以为 rpi-connect 和其专用的 WayVNC 服务器启用调试日志，以详细记录 Raspberry Pi 上的本地操作。

#### 在 rpi-connect 中启用增强型日志记录

使用以下命令打开 rpi-connect 配置文件进行编辑

```
$ systemctl --user edit rpi-connect
```

在注释之间输入以下配置行：

```
ExecStart=
ExecStart=/usr/bin/rpi-connect-env /usr/bin/rpi-connectd -socket=%t/rpi-connect-wayvnc.sock -v
```

| NOTE | 您需要两行都以 ExecStart= 开头。 |
| ------ | ---------------------------------- |

最后，使用以下命令重新启动服务：

```
$ systemctl --user restart rpi-connect
```

#### 在专用 wayvnc 服务器中启用增强日志记录

打开与 Connect 关联的专用 WayVNC 服务器的配置文件

```
$ systemctl --user edit rpi-connect-wayvnc
```

在注释之间输入以下配置行

```
ExecStart=
ExecStart=/usr/bin/rpi-connect-env /usr/bin/wayvnc --config /etc/rpi-connect/wayvnc.config --render-cursor --unix-socket --socket=%t/rpi-connect-wayvnc-ctl.sock -Ldebug %t/rpi-connect-wayvnc.sock
```

| NOTE | 您需要同时使用以 ExecStart= 开头的这两行。 |
| ------ | -------------------------------------------- |

最后，使用以下命令重新启动服务：

```
$ systemctl --user restart rpi-connect-wayvnc
```

### 查看连接日志

要查看 Connect 服务及其专用 WayVNC 服务器的日志，请运行以下命令：

```
$ journalctl --user --follow --unit rpi-connect --unit rpi-connect-wayvnc
```
