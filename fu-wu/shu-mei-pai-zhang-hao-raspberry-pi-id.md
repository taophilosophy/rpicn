# 树莓派账号（Raspberry Pi ID）

## 创建树莓派 ID

在 GitHub 上编辑此文档：[点击此处 ](https://github.com/raspberrypi/documentation/blob/develop/documentation/asciidoc/services/id/signing_up.adoc)

要使用树莓派服务，您首先需要创建一个[树莓派 ID](https://id.raspberrypi.com/)。

在浏览器中访问 [id.raspberrypi.com](https://id.raspberrypi.com/)。

输入电子邮件和密码。点击 **注册** 按钮来创建您的账户。

![创建账户 ](https://www.raspberrypi.com/documentation/services/images/create_account_identity.png?hash=b7d11456c6e8e284a9b5cd9b91e1de77)

创建账户后，您将收到一封验证电子邮件。

![验证身份 ](https://www.raspberrypi.com/documentation/services/images/verify_identity.png?hash=fae9bdb9ea173de1bb1175ce2eb6d51e)

在邮件中点击 **验证电子邮件** 按钮以验证您的电子邮件地址并完成账户创建。

![已登录身份 ](https://www.raspberrypi.com/documentation/services/images/signed_in_identity.png?hash=75b76927f5b2e4cc641bfdbfc13b31d3)

创建树莓派账号后，您可以使用 **使用树莓派账号登录** 按钮登录树莓派服务。

## 启用双因素身份验证

在 GitHub 上编辑此文档：[点击此处 ](https://github.com/raspberrypi/documentation/blob/develop/documentation/asciidoc/services/id/2fa.adoc)

与大多数现代网络服务类似，树莓派账号支持使用基于时间的一次性密码 (TOTP) 的双因素身份验证 (2FA)。

双因素身份验证增加了额外的保护层。除了密码外，2FA 还需要另一个信息来登录。您应该基于 *您拥有的东西*（如智能手机）或 *您的生物特征信息* 来作为第二因素。

本指南使用您的智能手机作为认证的第二因素。

| 提示 | 树莓派账号支持 macOS 和 iOS iCloud 钥匙串集成。在您的 Mac 或 iPhone 上右键单击 QR 码，选择 "设置验证代码" 选项。 |
| ----- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |

### 安装双因素认证应用

首先，在您的手机上下载一个生成 TOTP 的应用程序。安装任何 2FA 应用程序，如 [Authy](https://authy.com/) 或 Google Authenticator。

### 启用双因素身份验证

要启用双因素身份验证，请在登录到您的 [树莓派 ID](https://id.raspberrypi.com/) 后点击 **双因素身份验证** 选项。

![启用 2FA](https://www.raspberrypi.com/documentation/services/images/enable_2fa.png?hash=4d98c2191e3e389bd8a049dcb2585ca4)

在您的手机上打开 2FA 应用程序。使用您的树莓派账号提供的 QR 码扫描您的 2FA 应用程序以开始生成令牌。

| 注意 | 请查看您的 2FA 应用程序的文档，了解如何扫描 QR 码生成令牌。 |
| ------ | ----------------------------------------------------------------------------------------------- |

![认证 ](https://www.raspberrypi.com/documentation/services/images/authenticate.png?hash=cf3423489e85d64e8aeafd30eee67eb7)

输入您的 2FA 应用程序生成的六位数字 TOTP 以注册 2FA 应用程序与您的树莓派 ID。

将出现确认屏幕，包含恢复代码。请将恢复代码存储在安全的地方。**这是唯一的方法在您丢失手机和 2FA 应用程序时绕过 2FA**。

![已启用 TOTP](https://www.raspberrypi.com/documentation/services/images/totp_enabled.png?hash=b2448ab2aa08b20103aa24050e46497a)

您现在已经配置了树莓派账号需要使用手机上 2FA 应用程序生成的 TOTP 进行登录。

| 注意 | 您可以随时在 [id.raspberrypi.com](https://id.raspberrypi.com/) 上禁用双因素身份验证。 |
| ------ | --------------------------------------------------------------------------- |
