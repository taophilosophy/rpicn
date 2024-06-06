# 树莓派远程访问（Raspberry Pi Connect）

## 介绍

无论身在何处，均可通过 Raspberry Pi Connect 安全访问您的树莓派。

![hero](https://www.raspberrypi.com/documentation/services/images/hero.png)

要使用 Connect，请在您的树莓派上安装 Connect 软件。然后访问 connect.raspberrypi.com，在浏览器窗口中通过屏幕共享访问您的树莓派。您可以像将显示器插入树莓派一样使用桌面。

Connect 使用安全加密连接。默认情况下，Connect 直接在您树莓派和浏览器之间通信。但是，当 Connect 无法在您的树莓派和浏览器之间建立直接连接时，我们会使用位于伦敦的中继服务器。在后面情况下，raspberrypi.com 仅保留操作 Connect 所需的元数据。

## 安装

需要 64 位 Raspberry Pi OS Bookworm 的树莓派才能运行 Connect，该 OS 使用 Wayland 窗口服务器。支持的设备型号为树莓派 5、树莓派 4 及树莓派 400。

>**注意**
>
>Connect 与 Raspberry Pi OS Lite 或使用 X windows 服务器的系统并不兼容。 

要开始安装，请打开终端。运行以下命令来更新您的系统和软件包：

```
$ sudo apt update
$ sudo apt upgrade
```

### 安装 Connect

可在您的树莓派上运行以下命令来安装 Connect：

```
$ sudo apt install rpi-connect
```

安装完成后，重启您的树莓派以启动 Connect 服务：

```
$ sudo reboot
```

再次登录树莓派时，Connect 将自动启动。

### 开始连接

>**注意**
>
> 默认情况下，连接会在登录时自动启动。除非您从登录项中将其删除，否则无需手动启动连接。

要从命令行手动启动服务，请运行以下命令：

```
$ systemctl --user start rpi-connect
```

## 使用连接

现在您已经在您的树莓派上安装了 Connect，您必须将您的树莓派与您的 Raspberry Pi ID 关联起来才能使用 Connect。

如果您没有 Raspberry Pi ID，请创建一个。

### 链接您的树莓派和 Raspberry Pi ID

要将您的树莓派与您的 Raspberry Pi ID 绑定，请使用 Connect 生成验证链接。请访问该链接并登录您的 Raspberry Pi ID 以将您的树莓派绑定到您的帐户。

您可以使用树莓派桌面上的 Connect 图标或命令行 rpi-connect 生成验证链接。

#### 通过树莓派桌面

在 rpi-connect 服务开始运行后，系统托盘中会出现 Connect 的图标。

![just installed](https://www.raspberrypi.com/documentation/services/images/just_installed.png)

点击 Connect 图标，从下拉菜单中选择“登录”。这将打开一个验证链接，您可以使用它将您的树莓派链接到您的 Raspberry Pi ID。

![sign in](https://www.raspberrypi.com/documentation/services/images/sign-in.png)

#### 通过命令行

使用以下命令生成一个链接，该链接将绑定您的树莓派到您的 Raspberry Pi ID：

```
$ rpi-connect signin
```

此命令应该输出类似以下内容：

```
Complete sign in by visiting https://connect.raspberrypi.com/verify/XXXX-XXXX
```

访问任何设备上的链接，将您的树莓派与您的 Raspberry Pi ID 绑定。

#### 在 Connect 中完成树莓派的绑定。

访问在上一步骤中生成的验证链接。

使用您的 Raspberry Pi ID 登录 Connect。

![login with id](https://www.raspberrypi.com/documentation/services/images/login-with-id.png)

验证后，会为您的树莓派分配一个名称。选择一个能帮助您识别设备的名称。单击“创建设备并登录”按钮继续。

![create device](https://www.raspberrypi.com/documentation/services/images/create-device.png)

您现在可以从您的树莓派进行屏幕共享。Connect 系统托盘图标将变为蓝色，表示您的树莓派已连接到 Connect 服务。您应该收到一封电子邮件通知，提示新设备已登录到 Connect。

![sign in email](https://www.raspberrypi.com/documentation/services/images/sign-in-email.png)

>**警告**
>
>如果收到电子邮件，称有一台您不认识的设备登录了 Connect，请立即更改您的 Raspberry Pi ID 密码。从 Connect 中移除该设备，以永久取消它与您的帐户的绑定。请考虑启用双因素身份验证，以保护您的帐户安全。


![linked with](https://www.raspberrypi.com/documentation/services/images/linked-with.png)

单击 Connect 系统托盘图标以打开 Connect 菜单。该菜单显示您当前的登录状态，登出选项，以及启用或禁用屏幕共享的选项。

>**注意**
>
>您还可以使用终端命令 rpi-connect signout 来从 Connect 中移除您的树莓派。 

Connect 通过设备序列号通信。在设备之间移动 SD 卡会使您从 Connect 中注销。

### 连接到您的树莓派

现在您的树莓派已在 Connect 网站中列出，您可以在任何地方仅用浏览器来共享您的树莓派屏幕。

在计算机上访问 connect.raspberrypi.com。

Connect 会将您重定向到 Raspberry Pi ID 服务以进行登录。登录后，Connect 会显示已链接设备的列表。可用于屏幕共享的设备在设备名称下方显示灰色的屏幕共享标签。

![list of devices](https://www.raspberrypi.com/documentation/services/images/list-of-devices.png)

单击您想要屏幕共享的设备右侧的“Connect”按钮。这将打开浏览器窗口，显示您的树莓派的桌面。

![connecting](https://www.raspberrypi.com/documentation/services/images/connecting.png)

您现在可以像在本地一样使用您的树莓派。有关 Connect 的更多信息，请将鼠标悬停在断开按钮右侧的挂锁图标上。

![session start](https://www.raspberrypi.com/documentation/services/images/session-start.png)

>**技巧**
>
>使用桌面上方的从远程复制和粘贴到远程按钮在本地和远程剪贴板之间复制。 

连接后，在 Connect 网站中的屏幕共享标签旁会出现一个绿点。这表示活动屏幕共享会话。悬停可查看当前屏幕共享会话数。

![connect service connected](https://www.raspberrypi.com/documentation/services/images/connect-service-connected.png)

系统托盘中的 Connect 图标在屏幕共享会话进行时会变为紫色，并显示一个闭合的圆圈。

![pi desktop connected](https://www.raspberrypi.com/documentation/services/images/pi-desktop-connected.png)

### 从您的树莓派断开连接

要关闭屏幕共享会话，请单击桌面上方的断开按钮。

![session end](https://www.raspberrypi.com/documentation/services/images/session-end.png)

### 禁用屏幕共享

要关闭屏幕共享，请单击连接系统托盘图标，取消选择允许屏幕共享。连接系统托盘图标的下部将变为灰色。您仍然登录到连接，但您的屏幕无法共享。

![no sharing](https://www.raspberrypi.com/documentation/services/images/no-sharing.png)

在连接门户中，与该树莓派旧版旁边的连接按钮将消失，屏幕共享标签将显示为删除线格式。

![no connect button ui](https://www.raspberrypi.com/documentation/services/images/no-connect-button-ui.png)

要重新启用屏幕共享，请执行以下操作之一：

* 单击连接系统托盘图标，然后选择允许屏幕共享
* 运行终端命令 rpi-connect vnc on

### 管理您的树莓派

连接列出与您的 Raspberry Pi ID 绑定的所有树莓派。每个设备都有一个“连接”按钮，用于打开屏幕共享会话（如果该设备已启用屏幕共享）。每个设备的设备名称下都有一组标签，指示可用服务。

![list of devices](https://www.raspberrypi.com/documentation/services/images/list-of-devices.png)

单击设备名称以打开设备详细信息页面。此屏幕提供有关您的设备的低级信息。您还可以编辑设备名称或从“Connect”中删除设备。

![device details](https://www.raspberrypi.com/documentation/services/images/device-details.png)

从 Connect 中删除设备会自动注销设备上的 Connect。Connect 系统托盘图标会变为灰色，菜单只提供“登录”选项。

### 更新 Connect

要更新到最新版本的 Connect，请运行以下命令：

```
$ sudo apt update
$ sudo apt install --only-upgrade rpi-connect
```

重启设备以使更新生效：

```
$ sudo reboot
```

### 卸载 Connect

运行以下命令可从树莓派中移除 Connect 软件：

```
$ sudo apt remove --purge rpi-connect
```

卸载后，树莓派的序列号仍与您的 Raspberry Pi ID 绑定。设备仍然显示在 Connect 网站中，但无法用于屏幕共享。如果您在同一台树莓派上再次安装 Connect，即使使用不同的 SD 卡，它也将在 Connect 门户中复用现有设备名称。

要解除树莓派与 Raspberry Pi ID 之间的绑定，请从 Connect 网站上的设备列表中删除树莓派。

## 故障排除

### 已知问题

* Connect 仅支持共享树莓派的单个主显示屏。当树莓派连接到多个 HDMI 屏幕时，Connect 有时会共享辅助屏幕的内容。您可以通过右键单击桌面并在“桌面首选项”中更改任务栏位置来解决此问题。
* Connect 不支持屏幕键盘。为了实现完整功能，请使用物理键盘。
* Connect 需要使用实现了 ECMAScript 2020（ES11）的浏览器，因为它使用了旧版浏览器中不可用的功能。
* 浏览器会拦截某些按键和组合键。因此，您无法将这些键输入到您的 Connect 窗口中。Connect 提供了工具栏来模拟一些最常用的被拦截的按键。

### 启用增强型日志记录

您可以为 rpi-connect 和其专用的 WayVNC 服务器启用调试日志，以详细记录树莓派上的本地操作。

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

>**注意**
>
>以 `ExecStart=` 开头的这两行都是您所需要的。


最后，使用以下命令重启服务：

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

>**注意**
>
>以 `ExecStart=` 开头的这两行都是您所需要的。

最后，使用以下命令重启服务：

```
$ systemctl --user restart rpi-connect-wayvnc
```

### 查看连接日志

要查看 Connect 服务及其专用 WayVNC 服务器的日志，请运行以下命令：

```
$ journalctl --user --follow --unit rpi-connect --unit rpi-connect-wayvnc
```
