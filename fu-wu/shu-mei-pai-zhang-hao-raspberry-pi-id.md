# 树莓派账号（Raspberry Pi ID）


## 创建 Raspberry Pi ID

要使用 Raspberry Pi 服务，你必须首先创建个 Raspberry Pi ID。

在浏览器中，打开 <id.raspberrypi.com>。

输入电子邮件和密码。单击“注册”按钮以创建你的账户。

![create account identity](https://www.raspberrypi.com/documentation/services/images/create_account_identity.png)

创建账户后，你将收到一封验证电子邮件。

![verify identity](https://www.raspberrypi.com/documentation/services/images/verify_identity.png)

在电子邮件中单击“验证电子邮件”按钮，验证你的电子邮件地址并完成账户创建。

![signed in identity](https://www.raspberrypi.com/documentation/services/images/signed_in_identity.png)

创建 Raspberry Pi ID 后，你就可以使用“使用 Raspberry Pi ID 登录”按钮登录 Raspberry Pi 服务了。

## 启用双因素身份验证

与大多数现代网络服务一样，Raspberry Pi ID 支持使用基于时间的一次性密码（TOTP）的双因素身份验证（2FA）。

双因素身份验证增加了额外的保护层。除了密码外，2FA 还需要另一种信息来登录。你应该将这第二因素基于你拥有的东西（如智能手机）或你的生物特征信息。

本指南使用你的智能手机作为身份验证的第二因素。

>**技巧**
>
>Raspberry Pi ID 支持 macOS 和 iOS iCloud 钥匙串集成。在你的 Mac 或 iPhone 上右键单击 QR 码，以获取“设置验证代码”选项。

### 安装 2FA 应用程序

首先，在手机上下载一个生成 TOTP 的应用程序。即安装一个 2FA 应用程序，如 Authy 或 Google Authenticator。

### 启用 2FA

要启用双因素认证，请在登录到你的 Raspberry Pi ID 后单击双因素认证选项。

![enable 2fa](https://www.raspberrypi.com/documentation/services/images/enable_2fa.png)

打开手机上的双因素认证应用。使用双因素认证应用扫描由你的 Raspberry Pi ID 提供的 QR 码，开始生成令牌。

>**技巧**
>
>查看你的双因素认证应用文档，了解如何扫描 QR 码以生成令牌。 

![authenticate](https://www.raspberrypi.com/documentation/services/images/authenticate.png)

输入你的 2FA 应用程序生成的六位数字 TOTP，以注册 2FA 应用程序与你的 Raspberry Pi ID 绑定。

将显示确认提示，其中包含恢复代码。将恢复代码存储在安全位置。如果你丢失手机和 2FA 应用程序，这将是唯一绕过 2FA 的方法。

![totp enabled](https://www.raspberrypi.com/documentation/services/images/totp_enabled.png)

你现在已为你的 Raspberry Pi ID 配置为需要 2FA。从现在开始，需要通过手机上的 2FA 应用程序生成的 TOTP 才能登陆。

>**技巧**
>
>你可随时在 id.raspberrypi.com 上禁用双因素身份验证。
