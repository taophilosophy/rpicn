# 树莓派远程访问（Raspberry Pi Connect）Beta

## 简介

树莓派远程访问（Raspberry Pi Connect）可让您在世界上任何地方，安全地访问您的树莓派。

![hero](https://www.raspberrypi.com/documentation/services/images/hero.png?hash=abae19beca53f018d9c434ddee214cd9)

要使用 Connect，请在您的树莓派上[安装 Connect 软件 ](https://www.raspberrypi.com/documentation/services/connect.html#install-connect)。然后访问[connect.raspberrypi.com](https://connect.raspberrypi.com/)，在浏览器窗口中访问运行在您的树莓派上的桌面或 Shell。

Connect 使用安全的加密连接。默认情况下，Connect 在您的树莓派和浏览器之间直接通信。然而，当 Connect 无法在树莓派和浏览器之间建立直接连接时，我们会使用中继服务器。在这种情况下，树莓派仅保留操作 Connect 所需的元数据。

Connect 目前处于开发的测试阶段。

| 注意 | 要使用 Connect，您的树莓派必须运行[Raspberry Pi OS Bookworm](https://www.raspberrypi.com/news/bookworm-the-new-version-of-raspberry-pi-os/) 或更新版本。 |
| ------ | ------------------------------------------------------- |

## 安装


要开始安装，请打开一个终端窗口。运行以下命令来更新您的系统和软件包：

```
$ sudo apt update
$ sudo apt upgrade
```

在您的树莓派上运行以下命令来安装 Connect：

```
$ sudo apt install rpi-connect
```

安装完成后，请重新启动您的树莓派或[手动启动 Connect 服务 ](https://www.raspberrypi.com/documentation/services/connect.html#manually-start-connect) 来使用 Connect：

```
$ sudo reboot
```

下次登录树莓派时，Connect 将会自动启动。

### Connect Lite

我们提供了 Connect 的替代 **Lite** 版本，仅支持远程 Shell 访问，无法进行屏幕共享。

在您的树莓派上运行以下命令来安装 Connect Lite：

```
$ sudo apt install rpi-connect-lite
```

重新启动您的树莓派或[手动启动 Connect 服务 ](https://www.raspberrypi.com/documentation/services/connect.html#manually-start-connect) 来使用 Connect。

考虑[启用用户持久登录 ](https://www.raspberrypi.com/documentation/services/connect.html#enable-remote-shell-at-all-times)，即使您的用户账户未登录，也可以访问您的设备。

| 提示 | Lite 版本命令使用与完整版本 Connect 相同的`rpi-connect`名称。`rpi-connect-lite`只是一个软件包名称。 |
| ----- | ------------------------------------------------------------------------------------------- |

### 手动启动 Connect

| 注意 | 默认情况下，Connect 会在登录时自动启动。除非您从登录项中移除它，否则第一次启动后无需手动启动 Connect。 |
| ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

要从命令行手动启动服务，请运行以下命令：

```
$ systemctl --user start rpi-connect
```

## 将树莓派与树莓派 ID 关联


现在您已在树莓派上安装了 Connect，您必须将您的树莓派与您的树莓派 ID 关联起来才能使用 Connect。

如果您没有树莓派 ID，[创建一个 ](https://www.raspberrypi.com/documentation/services/id.html#create-a-raspberry-pi-id)。

要将您的树莓派与树莓派 ID 关联，使用 Connect 生成一个验证 URL。访问该 URL 并登录您的树莓派 ID，将您的树莓派添加到您的账户中。

您可以使用树莓派桌面上的 Connect 图标或`rpi-connect`命令行工具生成验证 URL。

### 通过树莓派桌面

一旦`rpi-connect`服务开始运行，Connect 图标将出现在系统托盘中。

![just installed](https://www.raspberrypi.com/documentation/services/images/just_installed.png?hash=692f34b6fd6ffda725743c0b13fe39d4)

单击 Connect 图标，从下拉菜单中选择“Sign in”。

![sign in](https://www.raspberrypi.com/documentation/services/images/sign-in.png?hash=503e210239051b7f27465e633e19b811)

这将打开一个验证 URL，您可以使用它将您的树莓派关联到您的树莓派 ID 上。

### 通过命令行

使用以下命令生成一个链接，将您的树莓派与您的树莓派 ID 连接起来：

```
$ rpi-connect signin
```

该命令应输出类似以下内容：

```
通过访问 https://connect.raspberrypi.com/verify/XXXX-XXXX 完成登录
```

在任何设备上访问生成的验证 URL，并使用您的树莓派 ID 登录，将您的树莓派与树莓派 ID 关联起来。

### 完成树莓派连接

访问上一步生成的验证 URL。

使用您的[树莓派 ID](https://www.raspberrypi.com/documentation/services/id.html) 登录到 Connect。

![使用 ID 登录 ](https://www.raspberrypi.com/documentation/services/images/login-with-id.png?hash=4767d1f31e88c81aa3a89b1a5dba11b9)

认证后，为您的树莓派分配一个名称。选择一个能帮助您识别设备的名称。点击“创建设备并登录”按钮继续。

![创建设备 ](https://www.raspberrypi.com/documentation/services/images/create-device.png?hash=23e46f4bc2cfdeb6de2d3c3bc2c2e790)

您现在可以远程连接到您的树莓派了。Connect 系统托盘图标会变成蓝色，表示您的树莓派已经与 Connect 服务连接。您会收到一封新设备登录 Connect 的电子邮件通知。

![登录邮件 ](https://www.raspberrypi.com/documentation/services/images/sign-in-email.png?hash=ef25669d6e5d66866d3ab09b653e7561)

| 警告 | 如果您收到一封未识别设备登录 Connect 的电子邮件，请立即更改您的树莓派 ID 密码。[从 Connect 中移除设备 ](https://www.raspberrypi.com/documentation/services/connect.html#manage-devices) 来永久解除与您账户的关联。考虑[启用双因素身份验证 ](https://www.raspberrypi.com/documentation/services/id.html#enable-two-factor-authentication) 来保护您的账户安全。 |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

点击 Connect 系统托盘图标以打开 Connect 菜单。该菜单显示您的当前登录状态，登出选项，以及启用或禁用远程访问方法的选项。

| 提示 | Connect 会使用您的设备序列号对通信进行签名。将 SD 卡移动到其他设备会导致您从 Connect 中注销。 |
| ----- | ------------------------------------------------------------------------------------------------------------------------------- |

## 访问您的树莓派

现在您的树莓派出现在 Connect 仪表板上，您可以通过浏览器从任何地方访问您的树莓派。Connect 提供多种远程交互方式。

### 屏幕共享

Connect 包含在浏览器中共享您的树莓派屏幕的功能。使用以下说明共享您的树莓派屏幕。

| 注意 | 屏幕共享需要**Wayland**窗口服务器。默认情况下，树莓派 OS 仅在树莓派 5、4 或 400 上使用 **64 位** 发行版的 Raspberry Pi OS **Bookworm**才使用 Wayland。屏幕共享与树莓派 OS Lite 或使用 X 窗口服务器的系统 **不兼容**。 |
| ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

在任何计算机上访问[connect.raspberrypi.com](https://connect.raspberrypi.com/)。

Connect 将您重定向到树莓派 ID 服务进行登录。登录后，Connect 会显示已连接设备的列表。支持屏幕共享的设备在设备名称下方显示灰色的 **屏幕共享** 徽章。

![设备列表 ](https://www.raspberrypi.com/documentation/services/images/list-of-devices.png?hash=e6b8b984af50f0a6a2bf598fd93196f7)

点击您想访问的设备右侧的 **通过 Connect** 按钮。从菜单中选择 **屏幕共享** 选项。这将打开一个浏览器窗口，显示您树莓派的桌面。

![屏幕共享连接中 ](https://www.raspberrypi.com/documentation/services/images/screen-sharing-connecting.png?hash=1635bce768aa5cee5af4471cd6797c06)

现在您可以像本地使用您的树莓派一样使用它。要了解更多连接信息，请将鼠标悬停在 **断开连接** 按钮右侧的挂锁图标上。

![屏幕共享开始 ](https://www.raspberrypi.com/documentation/services/images/screen-sharing-start.png?hash=76e29e56e835ec5c22b99f7ddd725200)

| 提示 | 使用桌面上方的 **从远程复制** 和 **粘贴到远程** 按钮在本地和远程剪贴板之间传输文本。 |
| ----- | ----------------------------------------------------------------------------------------------------- |

连接后，Connect 仪表板中**屏幕共享**徽章旁边会出现绿色圆点，表示有活动的屏幕共享会话。悬停以查看当前的屏幕共享会话数。

![屏幕共享活动 ](https://www.raspberrypi.com/documentation/services/images/screen-sharing-active.png?hash=ebd9ed1debe009f1c908ab50456033c2)

当屏幕共享会话进行中时，系统托盘中的 Connect 图标会变成紫色并显示一个闭合的圆圈。

![屏幕共享连接 ](https://www.raspberrypi.com/documentation/services/images/screen-sharing-connected.png?hash=f0ea6b9d4d3645d4e78698272ff90ad2)

#### 停止屏幕共享

要关闭屏幕共享会话，请点击桌面上方的 **断开连接** 按钮。

![屏幕共享结束 ](https://www.raspberrypi.com/documentation/services/images/screen-sharing-end.png?hash=f6e18e205b5e1a6891035d426df22431)

#### 禁用屏幕共享

要关闭屏幕共享，请点击 Connect 系统托盘图标并取消选择 **允许屏幕共享**。您的树莓派仍然登录到 Connect，但您将无法从 Connect 仪表板创建屏幕共享会话。

![禁用屏幕共享桌面 ](https://www.raspberrypi.com/documentation/services/images/screen-sharing-disabled-desktop.png?hash=fd904d7f45f9d31d199812b7fb0ceb23)

或者，您可以使用以下命令禁用屏幕共享：

```
$ rpi-connect vnc off
```

在 Connect 仪表板上，**屏幕共享** 徽章和 **通过 Connect** 菜单中的 **屏幕共享** 选项将显示为删除线。

![禁用屏幕共享 ](https://www.raspberrypi.com/documentation/services/images/screen-sharing-disabled.png?hash=3883a6ecf61f7a41299c9283a362bc3c)

要重新启用屏幕共享，请执行以下操作之一：

* 点击 Connect 系统托盘图标并选择 **允许屏幕共享**
* 运行以下命令：

  ```
  $ rpi-connect vnc on
  ```
  
### 远程 shell

Connect 包含从浏览器访问在 Raspberry Pi 上运行的 shell 的功能。按照以下说明访问远程 shell。

在任何计算机上访问 [connect.raspberrypi.com](https://connect.raspberrypi.com/)。

Connect 会重定向到 Raspberry Pi ID 服务以进行登录。登录后，Connect 显示已链接设备的列表。可远程访问 shell 的设备在设备名称下方显示灰色的 **Remote shell** 标记。

![设备列表 ](https://www.raspberrypi.com/documentation/services/images/list-of-devices.png?hash=e6b8b984af50f0a6a2bf598fd93196f7)

点击您想访问的设备右侧的 **Connect via** 按钮。从菜单中选择 **Remote shell** 选项。这将在您的 Raspberry Pi 上打开一个 shell 会话。

![连接远程 shell](https://www.raspberrypi.com/documentation/services/images/remote-shell-connecting.png?hash=847ea2f508da1c9ccf7dff55858110d3)

现在您可以像本地一样使用您的 Raspberry Pi。

![启动远程 shell](https://www.raspberrypi.com/documentation/services/images/remote-shell-start.png?hash=f30aa1e036aceddbf93db8052b90a1ba)

| 提示 | 在某些操作系统上，浏览器会拦截像 **Ctrl** + **Shift** + **C** 和 **Ctrl+C** 这样的键组合。您可以使用右键菜单或 **Ctrl** + **Insert** 进行复制，**Shift** + **Insert** 进行粘贴。 |
| ----- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |

连接后，Connect 仪表板上的 **Remote shell** 标记旁边会出现绿色圆点，表示活动的远程 shell 会话。悬停显示当前的远程 shell 会话数量。

![活动远程 shell](https://www.raspberrypi.com/documentation/services/images/remote-shell-active.png?hash=6bc5011a8cdba03770454b404688372c)

| 提示 | 每个远程 shell 连接都会创建一个全新的连接，就像 SSH 一样。要跨多个会话持久化后台命令和配置，请使用 `screen` 或 `tmux`。 |
| ----- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

当远程 shell 会话进行时，系统托盘中的 Connect 图标会变为紫色，并显示一个闭合的圆圈。

![连接的远程 shell](https://www.raspberrypi.com/documentation/services/images/remote-shell-connected.png?hash=50522c3af85883c3781a9938988dac82)

| 提示 | `CONNECT_TTY` 环境变量指示会话使用由 Connect 提供的远程 shell。 |
| ----- | --------------------------------------------------------------------------------------------- |

#### 结束远程 shell 会话

要关闭远程 shell 会话，请运行 `exit` 命令或关闭窗口。

![结束远程 shell](https://www.raspberrypi.com/documentation/services/images/remote-shell-end.png?hash=d59a5b649768c4e0481519eea1cd1591)

#### 禁用远程 shell 访问

要关闭远程 shell 访问，请点击 Connect 系统托盘图标并取消选择 **Allow remote shell**。您的 Raspberry Pi 仍然登录到 Connect，但您将无法从 Connect 仪表板创建远程 shell 会话。

![桌面禁用远程 shell](https://www.raspberrypi.com/documentation/services/images/remote-shell-disabled-desktop.png?hash=ea2ce53c56113b41b4234e392bc7dac8)

或者，您可以使用以下命令禁用远程 shell 访问：

```
$ rpi-connect shell off
```

在 Connect 仪表板上，**Remote shell** 标记和 **Connect via** 菜单中的 **Remote shell** 选项将显示为被划掉。

![禁用远程 shell](https://www.raspberrypi.com/documentation/services/images/remote-shell-disabled.png?hash=8f212b4f08d929bbd325ae45089eef6a)

要重新启用屏幕共享，请执行以下操作之一：

* 点击 Connect 系统托盘图标并选择 **Allow remote shell**
* 运行以下命令：

  ```
  $ rpi-connect shell on
  ```

## 随时启用远程 shell

Connect 作为用户级服务运行，而不是作为 root。因此，只有当您的用户帐户当前在 Raspberry Pi 上登录时，Connect 才能正常工作。如果禁用自动登录并重新启动，这可能导致您的 Raspberry Pi 不可访问。为了即使在您没有登录设备时也能继续运行 Connect，请启用 **user-lingering**。从您的用户帐户运行以下命令以启用 user-lingering：

```
$ loginctl enable-linger
```

| 提示 | 我们建议在所有无头 Raspberry Pi OS Lite 设置上启用 user-lingering，以防止远程重启后设备变得不可访问。 |
| ----- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |

## 管理设备

Connect 仪表板列出了与您的 Raspberry Pi ID 链接的所有 Raspberry Pi 设备，并显示可以访问它们的各种方法。

![设备列表 ](https://www.raspberrypi.com/documentation/services/images/list-of-devices.png?hash=e6b8b984af50f0a6a2bf598fd93196f7)

点击设备名称以打开设备详细信息页面。该屏幕提供有关设备的低级信息。您还可以编辑设备名称或从 Connect 中删除设备。

![设备详细信息 ](https://www.raspberrypi.com/documentation/services/images/device-details.png?hash=febeb62918a3230fffe99e541e136a0f)

从 Connect 中删除设备会自动登出设备上的 Connect。Connect 系统托盘图标变为灰色，并且菜单只提供 **Sign in** 选项。

## 更新

要更新到最新版本的 Connect，请运行以下命令：

```
$ sudo apt update
$ sudo apt install --only-upgrade rpi-connect
```

重新启动设备以使更新生效：

```
$ sudo reboot
```

Here's the translation of the provided text:

---

## 断开连接设备

在树莓派上运行以下命令来注销你的树莓派 ID，这将在连接屏幕上禁用你的设备：

```
$ rpi-connect signout
```

| 提示 | 要完全从你的连接账户中移除一个树莓派，请从[连接仪表板 ](https://www.raspberrypi.com/documentation/services/connect.html#manage-devices) 中移除它。 |
| ----- | ------------------------------------------------------------- |

## 卸载

运行以下命令从树莓派上移除连接软件：

```
$ sudo apt remove --purge rpi-connect
```

| 提示 | 如果你安装了 Connect Lite，请在上述命令中使用 `rpi-connect-lite` 替换 `rpi-connect`。 |
| ----- | --------------------------------------------------------------------- |

卸载后，树莓派的序列号仍与你的树莓派 ID 关联。设备仍然显示在连接仪表板上，但无法用于远程访问。如果你再次安装 Connect，即使使用不同的 SD 卡，在同一台树莓派上，它将重复使用连接仪表板中现有的设备名称。

要解除树莓派与树莓派 ID 之间的关联，请从连接仪表板的设备列表中移除树莓派。

## 故障排除


### 已知问题

* 屏幕共享仅支持共享树莓派的单个主显示器。当树莓派连接多个 HDMI 屏幕时，Connect 有时会共享次要屏幕的内容。你可以通过右键单击桌面并在**桌面首选项**中更改任务栏位置来解决此问题。
* Connect 不支持屏幕键盘。为了完整功能，请使用物理键盘。
* Connect 需要支持[ECMAScript 2020](https://caniuse.com/?search=es2020)（ES11）的浏览器，因为它使用了旧版本浏览器中不可用的[特性 ](https://caniuse.com/?feats=mdn-javascript_operators_optional_chaining,mdn-javascript_operators_nullish_coalescing,mdn-javascript_builtins_globalthis,es6-module-dynamic-import,bigint,mdn-javascript_builtins_promise_allsettled,mdn-javascript_builtins_string_matchall,mdn-javascript_statements_export_namespace,mdn-javascript_operators_import_meta)。
* 浏览器截获某些键和键组合。因此，你无法将这些键输入到你的 Connect 窗口中。屏幕共享包括一个工具栏，模拟一些最受欢迎的被截获键。

### 查看 Connect 状态

要查看 Connect 服务的当前状态，请运行以下命令：

```
$ rpi-connect status
```

此命令的输出显示你当前是否已登录到 Connect，以及在你的树莓派上启用的远程服务。

### 启用增强日志记录

你可以为`rpi-connect`及其专用的 WayVNC 服务器启用调试日志，详细记录树莓派上的本地操作。

#### 在`rpi-connect`中启用增强日志记录

用以下命令打开`rpi-connect`配置文件进行编辑：

```
$ systemctl --user edit rpi-connect
```

在注释之间输入以下配置行：

```
ExecStart=
ExecStart=/usr/bin/rpi-connectd -socket %t/rpi-connect-wayvnc.sock -v
```

| 注意 | 你需要 **同时** 使用以 `ExecStart=` 开头的两行。 |
| ------ | ----------------------------------- |

最后，使用以下命令重启服务：

```
$ systemctl --user restart rpi-connect
```

#### 在专用的`wayvnc`服务器中启用增强日志记录

打开与 Connect 关联的专用 WayVNC 服务器的配置文件：

```
$ systemctl --user edit rpi-connect-wayvnc
```

在注释之间输入以下配置行：

```
ExecStart=
ExecStart=/usr/bin/rpi-connect-env /usr/bin/wayvnc --config /etc/rpi-connect/wayvnc.config --render-cursor --unix-socket --socket=%t/rpi-connect-wayvnc-ctl.sock -Ldebug %t/rpi-connect-wayvnc.sock
```

| 注意 | 你需要 **同时** 使用以 `ExecStart=` 开头的两行。 |
| ------ | ----------------------------------- |

最后，使用以下命令重启服务：

```
$ systemctl --user restart rpi-connect-wayvnc
```

### 查看 Connect 日志

要查看 Connect 服务及其专用 WayVNC 服务器的日志，请运行以下命令：

```
$ journalctl --user --follow --unit rpi-connect --unit rpi-connect-wayvnc
```

