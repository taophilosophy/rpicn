# 树莓派 Connect 企业版

## 简介

**Connect 企业版**（Connect for Organisations）让多个用户通过 [Raspberry Pi Connect](shu-mei-pai-yuan-cheng-fang-wen-raspberry-pi-connect.md) 共享设备访问权限。

组织中的设备支持 Connect 的所有功能，包括[屏幕共享](shu-mei-pai-yuan-cheng-fang-wen-raspberry-pi-connect.md)、[远程 Shell](shu-mei-pai-yuan-cheng-fang-wen-raspberry-pi-connect.md) 访问和[远程更新](shu-mei-pai-yuan-cheng-fang-wen-raspberry-pi-connect.md)。

创建第一个组织时，会自动为该组织开启为期四周的免费试用。

## 创建组织

要创建新组织：

1. 登录你的 Raspberry Pi Connect 账号。

2. 在导航菜单右上角选择**账号切换图标**（两个方向相反的箭头）。

    ![Raspberry Pi Connect 界面，显示账号切换下拉菜单。账号切换器可让你在个人 Connect 账号和组织 Connect 账号之间切换。](https://www.raspberrypi.com/documentation/services/images/account-switcher.png)

3. 选择 **+ 新建组织**，然后输入组织名称。

4. 如果这是你创建的第一个组织，界面会显示**开始免费试用**。如果你之前创建过组织，界面会显示**创建组织**。选择显示给你的按钮。

    组织创建完成，你的 Connect 账号会自动作为管理员加入该组织。

如果你的个人 Connect 账号关联了设备，系统会提示你现在将这些设备转移到新组织。

要转移设备：

1. 点击“将所有设备转移到此组织？”链接。

    随后显示**转移个人设备**页面。

    ![Raspberry Pi Connect 界面，显示用于将树莓派设备从个人 Connect 账号导入组织 Connect 账号的链接。](https://www.raspberrypi.com/documentation/services/images/transfer-personal-devices-link.png)

    如果你有可以转移到新组织的个人设备，系统会在转移前要求你确认：

    ![Raspberry Pi Connect 界面，询问是否要将设备导入组织 Connect 账号。](https://www.raspberrypi.com/documentation/services/images/transfer-devices.png)

2. 选择**个人设备链接**查看个人设备，或选择“转移 x 台设备”（其中“x”是设备数量），确认要将这些计费设备添加到组织账号。

    如果你现在不想添加这些设备，之后随时可以添加。参见[转移设备](#转移设备)。

## 管理用户

你必须具有管理员权限，才能邀请用户加入组织、从组织中移除用户或更改用户在组织中的角色。

要邀请用户：

1. 登录你的 Raspberry Pi Connect 账号。

2. 在导航菜单右上角选择**账号切换图标**（两个方向相反的箭头），然后从列表中选择你的组织。

3. 在页面顶部选择**用户**标签页，然后选择**邀请成员**。

    ![Raspberry Pi Connect 界面，显示与组织 Connect 账号关联的用户。](https://www.raspberrypi.com/documentation/services/images/users.png)

4. 从下拉菜单中选择**角色**。

    组织成员有两种角色：

    * **成员。** 可以远程访问组织内所有设备（使用屏幕共享和远程 Shell），但不能部署远程更新，也不能对组织做任何更改的用户。
    * **管理员。** 可以远程访问组织内所有设备、部署远程更新并更改组织的用户。他们还会收到组织范围内敏感操作的通知邮件，例如新增设备和新的管理 API 访问令牌。

5. 输入要发送邀请的电子邮件地址。

6. 选择**发送邀请**。

    ![Connect 界面，显示邀请用户页面，其中包含角色下拉菜单、电子邮件地址和发送邀请按钮。](https://www.raspberrypi.com/documentation/services/images/invite-user.png)

    邀请会发送到你第 5 步中提供的电子邮件地址。用户可以通过邮件中的邀请链接，使用同一电子邮件地址或任何有效的 Raspberry Pi ID 登录。

要移除用户：

1. 登录你的 Raspberry Pi Connect 账号。

2. 在导航菜单右上角选择**账号切换图标**（两个方向相反的箭头），然后从列表中选择你的组织。

3. 在页面顶部选择**用户**标签页。

    这会显示组织中的所有成员。

4. 在要移除的用户旁边，选择**更多选项图标**（三个垂直点），然后选择**移除…**。

    此时会弹出确认窗口。

5. 如果确定要移除该用户，选择**移除用户**。

    该用户会立即从组织中移除，其与组织之间的 Shell 和屏幕共享会话会在几分钟内终止。

要更改用户的角色：

1. 登录你的 Raspberry Pi Connect 账号。

2. 在导航菜单右上角选择**账号切换图标**（两个方向相反的箭头），然后从列表中选择你的组织。

3. 在页面顶部选择**用户**标签页。

    这会显示组织中的所有成员。

4. 在要更改角色的用户旁边，选择**更多选项图标**（三个垂直点），然后选择**更改角色…**。

5. 从下拉菜单中选择要分配给用户的角色，然后选择**更改角色**。

    用户的角色更改完成，并显示确认屏幕。

## 将树莓派设备与组织关联

你必须具有管理员权限，才能将设备关联到组织。

要将设备关联到组织：

* 如果设备尚未关联到 Connect 账号，请参见[将树莓派设备关联到 Connect 账号](shu-mei-pai-yuan-cheng-fang-wen-raspberry-pi-connect.md)。

* 如果设备已关联到 Connect 账号，请参见[转移设备](#转移设备)。

## 转移设备

你必须具有管理员权限，才能在账号之间转移设备。

要转移设备：

1. 登录你的 Raspberry Pi Connect 账号。

2. 在导航菜单右上角选择账号切换图标。

    ![Raspberry Pi Connect 界面，显示账号切换下拉菜单。账号切换器可让你在个人 Connect 账号和组织 Connect 账号之间切换。](https://www.raspberrypi.com/documentation/services/images/account-switcher-with-organisation.png)

3. 切换到当前拥有该设备的账号（你的个人账号或某个组织）。

4. 选择要转移的设备。

5. 在设备页面选择**设置**。

6. 在**危险区域**下，选择**转移设备…**。

    ![Raspberry Pi Connect 界面，显示可以将设备转移到的账号。](https://www.raspberrypi.com/documentation/services/images/transfer.png)

7. 选择要将设备转移到的账号。

8. 选择**转移**。

## 为设备添加标签

标签可帮助你为组织中的设备分类，并快速找到设备。例如，你可以按位置（`london`、`leeds`）、环境（`production`、`staging`）或用途（`point-of-sale`、`kiosk`）为设备添加标签。

标签会显示在设备页面和设备列表中设备名称的下方。

你必须具有管理员权限，才能添加或移除标签。

要在设备上添加或移除标签：

1. 从设备列表中选择设备。

2. 在设备页面选择**设置**。

    ![编辑标签对话框，显示已应用的标签以及带有建议的自动补全下拉菜单。](https://www.raspberrypi.com/documentation/services/images/tagging.png)

3. 在**常规**部分的**标签**字段下：

    * 要添加标签，请在文本字段中输入。你可以从下拉菜单中选择现有标签，也可以输入新标签名称并选择**创建**选项。
    * 要移除标签，请选择要移除标签旁边的 **x**。

4. 选择**更新设备**以保存更改。

每台设备最多支持 10 个标签。标签名称不得超过 30 个字符，并且只能包含小写字母、数字、连字符和下划线。

## 搜索和筛选设备

设备列表顶部的搜索栏可让你结合自由文本搜索和结构化筛选来查找设备。

要按设备名称或序列号搜索，请在搜索栏中输入任意文本。结果会随着你的输入自动更新。

要按特定属性筛选，请输入限定符，后跟冒号和值。可用的限定符如下：

| 限定符 | 说明 |
|:------:|------|
| `model:` | 按 Raspberry Pi 型号筛选（例如 `model:5`、`model:4b`） |
| `memory:` | 按内存大小筛选（例如 `memory:4gb`、`memory:512mb`） |
| `os:` | 按操作系统筛选（例如 `os:raspios-13`） |
| `tag:` | 按标签筛选（例如 `tag:kiosk`、`tag:production`） |

>**注意**
>
>`model:`、`memory:` 和 `os:` 限定符只能找到运行 Connect 客户端 2.9.0 或更高版本的设备。要更新设备上的 Connect，请参见[更新](shu-mei-pai-yuan-cheng-fang-wen-raspberry-pi-connect.md)。

你可以在单个查询中组合多个筛选条件和自由文本。例如，`model:5 tag:production dashboard` 会查找带有 `production` 标签且名称中包含“dashboard”的 Raspberry Pi 5 设备。

![设备列表，搜索栏中应用了型号和标签筛选条件。](https://www.raspberrypi.com/documentation/services/images/filters.png)

当你在搜索栏中开始输入时，下拉菜单会建议可用的限定符和值。从下拉菜单中选择一个限定符即可查看其可用值，然后选择一个值将其添加为筛选条件。应用后的筛选条件会显示在搜索栏中。

选择筛选条件旁边的 **x** 或按 **Backspace** 键即可移除筛选条件。

多次使用 `tag:` 限定符可以查找具有*所有*指定标签的设备。例如，`tag:production tag:kiosk` 只返回同时具有 `production` 和 `kiosk` 标签的设备。

>**技巧**
>
>选择列表中任意设备上的标签，即可快速将其添加为筛选条件。

## 部署远程更新

你可以使用 Raspberry Pi Connect 的[远程更新](shu-mei-pai-yuan-cheng-fang-wen-raspberry-pi-connect.md)功能，向组织中的设备推送更新。向组织设备部署更新与[向个人设备部署](shu-mei-pai-yuan-cheng-fang-wen-raspberry-pi-connect.md)非常相似，区别如下：

* 组织会维护一个[构件库](#管理构件库)，其中的构件可以多次部署。
* 除了上传构件，你还可以[自行托管构件](#自行托管更新构件)，这样在等待设备上线期间构件不会过期。
* 你可以通过[管理 API](#管理-api) 管理构件和部署。

>**注意**
>
>只有管理员才能部署远程更新和管理更新构件。

首先，按照[脚本构件](shu-mei-pai-yuan-cheng-fang-wen-raspberry-pi-connect.md)或 [A/B 启动更新](shu-mei-pai-yuan-cheng-fang-wen-raspberry-pi-connect.md)所述构建更新构件。

然后选择将其提供给 Raspberry Pi Connect 的方式：

* **上传构件**：由 Connect 为你托管文件。上传文件最大 2 GB，并在上传两小时后过期。如果设备未在该时间内接收部署，将不会收到更新。
* **自行托管构件**：你将文件托管在接收设备可以下载的位置，并提供其位置，详见[自行托管更新构件](#自行托管更新构件)。自行托管的构件不会过期，因此对于可能离线超过两小时的设备，或需要长期向多台设备部署同一构件的情况，请选择这种方式。

### 自行托管更新构件

当你自行托管构件时，Raspberry Pi Connect 不会存储该文件。相反，你向 Connect 提供构件的位置，Connect 会将位置传递给接收设备，以便设备直接下载文件。

将构件托管在接收设备可以访问的任何位置：你自己的 Web 服务器、S3 存储桶、FTP 或 SFTP 服务器，或者使用 `file://` URI 指定接收设备本身的路径。远程更新支持 HTTP、HTTPS、FTP、SFTP 和 file URI。

该位置必须可供接收设备访问，但不必可供 Raspberry Pi Connect 服务器或整个互联网访问。从与接收设备位于同一本地网络的另一台计算机提供构件，效果很好。

以下是一个示例 URI：`http://192.168.0.1:8080/path/to/app.update.tar.zst`

它包含以下必需信息：

* 主机 IP：`192.168.0.1`
* 端口：`8080`
* 路径：`/path/to/app.update.tar.zst`

你还需要构件的 SHA-256 校验和，Connect 会将其传递给设备，以便设备检查构件在传输过程中是否损坏或被篡改。`otamaker` 在构建脚本构件时会输出校验和；否则，请使用 `sha256sum` 计算。

记下 URI 和校验和；部署构件时两者都会用到。

#### 示例：从树莓派提供构件

以下示例从与接收设备位于同一网络的树莓派主机提供更新构件。

1. 在主机上运行 HTTP 服务器，并相应更改构件目录：

    ```bash
    $ python -m http.server 8080 --directory ./work/image-myapp
    ```

2. 计算更新文件的 SHA-256 校验和，然后记下校验和：

    ```bash
    $ sha256sum ./work/image-myapp/myapp-update.tar.zst
    ```

3. 查找主机在本地网络中的 IP 地址，然后记下该 IP 地址。构建构件的 URI 时需要用到它：

    ```bash
    $ hostname -I
    ```

### 管理构件库

组织会维护一个构件库，列在**远程更新**标签页下。你在部署过程中创建的构件也会添加到该库中。

要提前将构件添加到库中，请转到**远程更新**标签页，选择**新建**，然后选择以下选项之一：

* **上传构件**：输入名称并选择文件，详见[上传构件](shu-mei-pai-yuan-cheng-fang-wen-raspberry-pi-connect.md)，然后选择**上传构件**。
* **自行托管构件**：输入名称、URI 和 SHA-256 校验和，然后选择**保存构件**。

![自行托管构件屏幕，显示必填字段：名称、URI 和 SHA-256 校验和。](https://www.raspberrypi.com/documentation/services/images/create-deployment-artefact.png)

构件库还会显示每个上传构件的**过期时间**，或在该时间过后显示**已过期**。过期构件仍保留在库中，因此你仍可以查看部署过什么，但无法再次部署它们。要再次部署同一文件，请重新上传。

>**注意**
>
>构件一旦部署或尝试部署，就无法删除。这样可以在你的账号遭到入侵时提供可追溯性。

### 部署构件

要部署构件，请转到**设备**标签页，然后在接收设备旁边选择**部署**。**部署**按钮仅对启用了远程更新的设备显示。

![Raspberry Pi Connect 设备屏幕，显示设备列表，其中一台设备旁边有部署按钮。](https://www.raspberrypi.com/documentation/services/images/devices-deploy-button.png)

然后，在**新部署**屏幕中，选择以下选项之一：

* **使用现有构件**：从库中选择一个构件，然后选择**下一步**。列表中的每个构件都会显示其名称、校验和的前几个字符、URI 或文件名和大小，对于上传的构件还会显示距离过期还有多长时间。过期构件不会出现在列表中。
* **上传构件**：输入名称并选择文件，详见[上传构件](shu-mei-pai-yuan-cheng-fang-wen-raspberry-pi-connect.md)，然后选择**下一步**。
* **自行托管构件**：输入名称、URI 和 SHA-256 校验和，然后选择**下一步**。

![选择“部署”后，新部署屏幕会让你选择使用现有构件、上传构件或自行托管构件。](https://www.raspberrypi.com/documentation/services/images/new-deployment-view.png)

在**第 2 步：检查并部署**中，检查构件的详细信息，然后选择**部署**。对于上传的构件，此步骤还会显示文件何时过期；只有当接收设备在该时间之前上线并开始部署，部署才会成功。

按照[监控部署](shu-mei-pai-yuan-cheng-fang-wen-raspberry-pi-connect.md)所述跟踪部署进度。

你还可以使用[管理 API](#管理-api) 自动管理更新构件和部署。

## 设置订阅

Connect 企业版的订阅会在四周试用期结束后开始，此后每月按后付费方式结算。

你必须具有管理员权限，才能设置订阅。

要设置订阅：

1. 在页面顶部标签页下方的试用横幅中选择**设置账单**。
2. 输入接收账单相关通知（如发票）的电子邮件地址。
3. 输入支付方式详情并提交。

    * 如果试用期还剩几天，按钮显示为**开始试用**。你的试用会继续，之后将按月计费。
    * 如果试用期已结束，按钮显示为**付款并订阅**。这会启动你的月度订阅。

免费试用结束后，在设置订阅之前，你将无法远程访问组织中的设备。

![Connect 账单界面，显示 28 天免费试用以及开始试用所需填写的付款详情字段。](https://www.raspberrypi.com/documentation/services/images/billing.png)

## 查看审计日志

审计日志按时间顺序显示过去 90 天内的所有活动，最近的事件排在最前面。事件包括设备、组织成员、API 访问令牌和远程访问会话的更改等。超过 90 天的事件会自动删除。

你必须具有管理员权限，才能查看组织中过去 90 天内的活动。要查看审计日志，请打开页面顶部的**审计日志**标签页。

![Connect 审计界面，显示下拉筛选菜单和结果。](https://www.raspberrypi.com/documentation/services/images/audit-log.png)

列表中的每个事件都包含以下信息：

* **时间戳。** 事件发生的时间。
* **来源。** 事件发生在仪表板中还是通过 API 发生。
* **操作。** 操作（例如**创建 API 访问令牌**）及相关详情。
* **对象。** 操作的对象，例如特定设备、组织或访问令牌。
* **操作者。** 执行事件的用户，包括事件发生所在的国家或地区。

你可以按操作类型（例如**远程 Shell 会话已启动**）筛选事件。要筛选列表，请选择列表左上角上方**筛选器**旁边的**操作**下拉菜单。

选择列表右上角上方的**下载 CSV**，以 CSV 格式下载列表。

## 更改组织设置

组织的管理员可以从页面顶部的**设置**标签页配置以下内容。

![Connect 组织设置界面，显示组织名称以及组织的其他数据字段。](https://www.raspberrypi.com/documentation/services/images/organisation-settings.png)

### 重命名组织

要更改组织名称，请在**常规**部分输入新名称。这不会影响你的设备或组织成员。

### 要求双因素身份验证

你可以要求组织中的所有成员在其 Raspberry Pi ID 上启用双因素身份验证（2FA）。这增加了一层保护，防止被盗用的成员账号被用来访问组织设备。

要启用 2FA 要求：

1. 登录 Raspberry Pi Connect。
2. 在右上角通过**账号切换**图标选择你的组织账号。
3. 选择**设置**标签页，然后选择**要求双因素身份验证**。随后会显示通知，确认组织的设置已成功更新。

![Connect 组织设置的身份验证部分，显示要求双因素身份验证按钮。](https://www.raspberrypi.com/documentation/services/images/organisation-authentication.png)

这会启动 14 天宽限期。在宽限期内，我们会向尚未设置 2FA 的组织成员显示横幅。

宽限期结束后，仍未设置 2FA 的成员将被阻止访问组织。在他们于 Raspberry Pi ID 上启用 2FA 之前，将无法再访问组织设备或其他资源。

![宽限期结束后向未启用 2FA 的成员显示的要求启用双因素身份验证页面，其中包含在其 Raspberry Pi ID 上启用 2FA 的链接。](https://www.raspberrypi.com/documentation/services/images/organisation-2fa-required.png)

要禁用 2FA 要求：

1. 登录 Raspberry Pi Connect。
2. 在右上角通过**账号切换**图标选择你的组织账号。
3. 选择**设置**标签页，然后选择**停止要求双因素身份验证**。随后会显示通知，确认组织的设置已成功更新。

>**注意**
>
>禁用后再重新启用 2FA 要求，会重置 14 天宽限期。

### 创建认证密钥

要自动[将设备关联到 Connect](shu-mei-pai-yuan-cheng-fang-wen-raspberry-pi-connect.md)（无需使用 Web 界面），请创建认证密钥。在**认证密钥**部分选择**新建**，然后输入说明和过期时间（1 到 90 天）。

新的认证密钥会显示出来。选择其旁边的剪贴板图标进行复制。请立即复制该认证密钥，因为之后将无法再次查看。

>**重要**
>
>你的认证密钥只显示一次。请立即复制，因为之后将无法再次看到。

### 创建管理 API 访问令牌

要自动创建用于[将设备关联到 Connect](shu-mei-pai-yuan-cheng-fang-wen-raspberry-pi-connect.md) 的认证密钥（无需使用 Web 界面），你可以为 [Connect 企业版管理 API](#管理-api) 创建 API 访问令牌。在 **API 访问令牌**部分选择**新建**，然后输入访问令牌的说明。

>**警告**
>
>管理 API 访问令牌等同于组织管理员的用户名和密码。它可以管理组织中的每台设备、每个认证密钥和每个设备身份。请将其保存在调用管理 API 的机器上（例如预配工作站或 CI 系统）；切勿将其嵌入树莓派系统镜像，也不要复制到设备上。要对设备本身进行身份验证，请使用[设备身份](#创建设备身份)或[认证密钥](#创建认证密钥)生成每台设备的凭据，并改用这些凭据。

新的访问令牌会显示出来。选择其旁边的剪贴板图标进行复制。请立即复制该访问令牌，因为之后将无法再次查看。

>**重要**
>
>你的访问令牌只显示一次。请立即复制，因为之后将无法再次看到。

## 管理 API

管理 API 可让你在不使用 Connect Web 界面的情况下自动管理组织。对管理 API 的请求必须使用有效的管理 API 访问令牌进行身份验证。基础 URL 为 https://api.connect.raspberrypi.com。

### 速率限制

每个管理 API 访问令牌每小时最多可发出 5,000 个请求。限额按固定的一小时窗口计算：计数器在每小时开始时重置，无论你在该小时内何时发出第一个请求。

对已通过身份验证的请求，每个响应都会包含以下标头，以便你跟踪用量：

* `X-Rate-Limit-Limit`：每小时允许的最大请求数。
* `X-Rate-Limit-Remaining`：当前小时内剩余的请求数。
* `X-Rate-Limit-Reset`：距离当前小时结束和计数器重置还有多少秒。

例如：

```http
HTTP/2 200
Content-Type: application/json; charset=utf-8
X-Rate-Limit-Limit: 5000
X-Rate-Limit-Remaining: 4999
X-Rate-Limit-Reset: 3600
```

如果你超过限额，会收到 **429 Too Many Requests** 响应，其中包含相同的标头。请等待 `X-Rate-Limit-Reset` 中给出的秒数后再重试。例如：

```http
HTTP/2 429
X-Rate-Limit-Limit: 5000
X-Rate-Limit-Remaining: 0
X-Rate-Limit-Reset: 1800

Throttled
```

>**注意**
>
>使用无效访问令牌发出的请求仍会计入该令牌的限额，但响应中不会包含速率限制标头。

### 创建设备身份

设备身份可让你在不进行交互式登录的情况下，预先让树莓派设备通过组织身份验证。与认证密钥不同，设备身份可多次使用，并依赖存储在设备一次性可编程存储器中的私钥。

创建设备身份是免费的。只有在设备首次通过组织 Connect 账号进行身份验证后，才会开始对该设备计费，因此设备身份非常适合组织在部署树莓派设备之前预先配置 Connect。

请求必须包含 `X-Connect-Identity-Signature` 标头。要生成该标头，请按以下顺序构造以换行符分隔的载荷：

* HTTP 请求方法（例如 `POST`）
* 完整请求 URL
* `Authorization: <value>`
* `Content-Type: <value>`
* `Accept: <value>`（如果你的 HTTP 客户端会发送该标头）
* HTTP 请求体的 SHA256 十六进制摘要（即下方 `POST` 的 JSON 正文）

使用设备的私钥以 ECDSA（SHA256）对载荷签名，然后对结果进行 Base64 编码。

例如，注册设备身份的请求会生成以下载荷：

```
POST
https://api.connect.raspberrypi.com/organisation/device-identities
Authorization: Bearer rporg_accesstokenhere
Content-Type: application/json
Accept: */*
<SHA256 hex digest of the HTTP request body>
```

在设备上，使用 [rpi-fw-crypto](https://github.com/raspberrypi/utils/tree/master/rpifwcrypto) 对载荷签名。例如，将载荷写入 `payload.txt` 后：

```bash
$ rpi-fw-crypto sign --in payload.txt --key-id 1 --alg ec | base64 -w 0
```

输出即为 `X-Connect-Identity-Signature` 标头的值。

要为组织创建设备身份，请使用[管理 API 访问令牌](#创建管理-api-访问令牌)发出以下 HTTP 请求。

替换以下代码中的这些值：

* `rporg_accesstokenhere`：你的管理 API 访问令牌。
* `signaturehere`：此请求的 `X-Connect-Identity-Signature` 值。
* `-----BEGIN PUBLIC KEY-----...`：设备的 PEM 编码公钥。
* `my-device-identity`：设备身份的说明，会显示在组织的审计日志中。
* `pi5-001`：交换身份时分配给设备的名称（可选，默认为设备的主机名）。
* `production`、`kiosk`：（可选）交换身份时应用于设备的标签。每个标签只能包含小写字母、数字、连字符和下划线，最大长度为 30 个字符。每个设备身份最多可应用十个标签。

**JSON**

```http
POST /organisation/device-identities HTTP/1.1
Host: api.connect.raspberrypi.com
Authorization: Bearer rporg_accesstokenhere
Content-Type: application/json
X-Connect-Identity-Signature: signaturehere

{
    "public_key": "-----BEGIN PUBLIC KEY-----...",
    "description": "my-device-identity",
    "device_name": "pi5-001",
    "tags": ["production", "kiosk"]
}
```

**curl**

```bash
$ curl --header 'Authorization: Bearer rporg_accesstokenhere' --header 'X-Connect-Identity-Signature: signaturehere' --header 'Content-Type: application/json' --data '{"public_key":"-----BEGIN PUBLIC KEY-----...","description":"my-device-identity","device_name":"pi5-001","tags":["production","kiosk"]}' https://api.connect.raspberrypi.com/organisation/device-identities
```

如果成功，你会收到 **201 Created** 响应，其中包含 JSON 格式的设备身份。例如：

```http
HTTP/2 201
Content-Type: application/json; charset=utf-8

{
    "id": "096ce472-2cbd-412a-8295-6c03a1a07ba4",
    "description": "my-device-identity",
    "device_name": "pi5-001",
    "tags": ["production", "kiosk"],
    "created_at": "2026-02-25T16:09:52Z",
    "public_key": "-----BEGIN PUBLIC KEY-----..."
}
```

响应包含以下字段：

* `id`：设备身份的唯一标识符。
* `description`：创建设备身份时使用的说明。
* `device_name`：交换身份时分配给设备的名称。
* `tags`：交换身份时应用于设备的标签。
* `created_at`：创建设备身份的日期和时间（ISO 8601 格式）。
* `public_key`：设备身份的 PEM 编码公钥。

否则，你会收到以下响应之一：

| 响应 | 说明 | 示例 |
| ---- | ---- | ---- |
| **401 Unauthorized** | 管理 API 访问令牌无效。 |  |
| **422 Unprocessable Content** | 无法创建设备身份。 | `{"message":"Validation failed: Public key is invalid"}` |

### 列出设备身份

要列出组织中的所有设备身份，请使用[管理 API 访问令牌](#创建管理-api-访问令牌)发出以下 HTTP 请求。

替换以下代码中的这些值：

* `rporg_accesstokenhere`：你的管理 API 访问令牌。

**HTTP**

```http
GET /organisation/device-identities HTTP/1.1
Host: api.connect.raspberrypi.com
Authorization: Bearer rporg_accesstokenhere
```

**curl**

```bash
$ curl --header 'Authorization: Bearer rporg_accesstokenhere' https://api.connect.raspberrypi.com/organisation/device-identities
```

如果成功，你会收到 **200 OK** 响应，其中包含组织中最多 100 个设备身份（以 JSON 格式表示），按说明的字母顺序排序。例如：

```http
HTTP/2 200
Content-Type: application/json; charset=utf-8

{
    "device_identities": [
        {
            "id": "096ce472-2cbd-412a-8295-6c03a1a07ba4",
            "description": "my-device-identity",
            "device_name": "pi5-001",
            "tags": [],
            "created_at": "2026-02-25T16:09:52Z",
            "public_key": "-----BEGIN PUBLIC KEY-----..."
        }
    ],
    "meta": {
        "page": 1,
        "per_page": 100,
        "total_count": 1,
        "total_pages": 1
    }
}
```

响应包含以下字段：

* `device_identities`：组织中的设备身份列表（每页最多 100 个）。
* `meta`：分页详情。

`device_identities` 列表中的每一项包含以下字段：

* `id`：设备身份的唯一标识符。
* `description`：创建设备身份时使用的说明。
* `device_name`：交换身份时分配给设备的名称。
* `tags`：交换身份时应用于设备的标签。
* `created_at`：创建设备身份的日期和时间（ISO 8601 格式）。
* `public_key`：设备身份的 PEM 编码公钥。

`meta` 对象包含以下字段：

* `page`：响应的当前页码。
* `per_page`：每页的设备身份数量（最多 100）。
* `total_count`：组织中的设备身份总数。
* `total_pages`：组织设备身份的总页数。

如果管理 API 访问令牌无效，你会收到 **401 Unauthorized** 响应。

`page` 和 `per_page` 查询参数的用法与[列出设备](#列出设备)相同。

### 显示设备身份

要显示组织中的单个设备身份，请使用[管理 API 访问令牌](#创建管理-api-访问令牌)发出以下 HTTP 请求。

替换以下代码中的这些值：

* `rporg_accesstokenhere`：你的管理 API 访问令牌。
* `device-identity-id`：设备身份的唯一标识符。

**HTTP**

```http
GET /organisation/device-identities/device-identity-id HTTP/1.1
Host: api.connect.raspberrypi.com
Authorization: Bearer rporg_accesstokenhere
```

**curl**

```bash
$ curl --header 'Authorization: Bearer rporg_accesstokenhere' https://api.connect.raspberrypi.com/organisation/device-identities/device-identity-id
```

如果成功，你会收到 **200 OK** 响应，其中包含 JSON 格式的设备身份详情。例如：

```http
HTTP/2 200
Content-Type: application/json; charset=utf-8

{
    "id": "096ce472-2cbd-412a-8295-6c03a1a07ba4",
    "description": "my-device-identity",
    "device_name": "pi5-001",
    "tags": [],
    "created_at": "2026-02-25T16:09:52Z",
    "public_key": "-----BEGIN PUBLIC KEY-----..."
}
```

否则，你会收到以下响应之一：

| 响应 | 说明 |
| ---- | ---- |
| **401 Unauthorized** | 管理 API 访问令牌无效。 |
| **404 Not Found** | 组织中找不到该设备身份。 |

### 更新设备身份

要更新组织中的现有设备身份，请使用[管理 API 访问令牌](#创建管理-api-访问令牌)发出以下 HTTP 请求。

替换以下代码中的这些值：

* `rporg_accesstokenhere`：你的管理 API 访问令牌。
* `device-identity-id`：设备身份的唯一标识符。
* `my-renamed-device-identity`：设备身份的新说明。
* `pi5-001`：交换身份时分配给设备的新名称（可选）。
* `production`、`kiosk`：交换身份时应用于设备的标签（可选）。

**JSON**

```http
PATCH /organisation/device-identities/device-identity-id HTTP/1.1
Host: api.connect.raspberrypi.com
Authorization: Bearer rporg_accesstokenhere
Content-Type: application/json

{
    "description": "my-renamed-device-identity",
    "device_name": "pi5-001",
    "tags": ["production", "kiosk"]
}
```

**curl**

```bash
$ curl --request PATCH --header 'Authorization: Bearer rporg_accesstokenhere' --header 'Content-Type: application/json' --data '{"description":"my-renamed-device-identity","device_name":"pi5-001","tags":["production","kiosk"]}' https://api.connect.raspberrypi.com/organisation/device-identities/device-identity-id
```

如果成功，你会收到 **200 OK** 响应，其中包含 JSON 格式的更新后设备身份：

```http
HTTP/2 200
Content-Type: application/json; charset=utf-8

{
    "id": "096ce472-2cbd-412a-8295-6c03a1a07ba4",
    "description": "my-renamed-device-identity",
    "device_name": "pi5-001",
    "tags": ["production", "kiosk"],
    "created_at": "2026-02-25T16:09:52Z",
    "public_key": "-----BEGIN PUBLIC KEY-----..."
}
```

>**注意**
>
>设备身份一旦与设备完成交换，就只能更新 `description`。请求体中的任何 `device_name` 或 `tags` 值都会被忽略，因为这些字段仅在身份首次交换时应用。

否则，你会收到以下响应之一：

| 响应 | 说明 | 示例 |
| ---- | ---- | ---- |
| **401 Unauthorized** | 管理 API 访问令牌无效。 |  |
| **404 Not Found** | 组织中找不到该设备身份。 |  |
| **422 Unprocessable Content** | 无法更新设备身份。 | `{"message":"Validation failed: Description can't be blank"}` |

### 删除设备身份

要删除组织中的设备身份，请使用[管理 API 访问令牌](#创建管理-api-访问令牌)发出以下 HTTP 请求。

替换以下代码中的这些值：

* `rporg_accesstokenhere`：你的管理 API 访问令牌。
* `device-identity-id`：设备身份的唯一标识符。

**HTTP**

```http
DELETE /organisation/device-identities/device-identity-id HTTP/1.1
Host: api.connect.raspberrypi.com
Authorization: Bearer rporg_accesstokenhere
```

**curl**

```bash
$ curl --request DELETE --header 'Authorization: Bearer rporg_accesstokenhere' https://api.connect.raspberrypi.com/organisation/device-identities/device-identity-id
```

如果设备身份已与设备完成交换，关联的设备也会被删除，并退出 Raspberry Pi Connect 登录。

如果成功，你会收到 **200 OK** 响应，其中包含 JSON 格式的已删除设备身份详情。例如：

```http
HTTP/2 200
Content-Type: application/json; charset=utf-8

{
    "id": "096ce472-2cbd-412a-8295-6c03a1a07ba4",
    "description": "my-device-identity",
    "device_name": "pi5-001",
    "tags": [],
    "created_at": "2026-02-25T16:09:52Z",
    "public_key": "-----BEGIN PUBLIC KEY-----..."
}
```

否则，你会收到以下响应之一：

| 响应 | 说明 |
| ---- | ---- |
| **401 Unauthorized** | 管理 API 访问令牌无效。 |
| **404 Not Found** | 组织中找不到该设备身份。 |

### 创建认证密钥（API）

要创建用于[将设备关联到 Connect](shu-mei-pai-yuan-cheng-fang-wen-raspberry-pi-connect.md) 的认证密钥，请使用管理 API 访问令牌发出以下 HTTP 请求。

替换以下代码中的这些值：

* `rporg_accesstokenhere`：你的管理 API 访问令牌。
* `my-auth-key`：认证密钥的说明。
* `1`：认证密钥过期前的天数，介于 1 到 90 之间（可选，默认为 1 天）。
* `pi5-001`：使用此密钥添加设备时使用的名称（可选，默认为设备的主机名）。
* `production`、`kiosk`：交换认证密钥时应用于设备的标签（可选）。每个标签只能包含小写字母、数字、连字符和下划线，最大长度为 30 个字符。每个认证密钥最多可应用 10 个标签。

**JSON**

```http
POST /organisation/auth-keys HTTP/1.1
Host: api.connect.raspberrypi.com
Authorization: Bearer rporg_accesstokenhere
Content-Type: application/json

{
    "description": "my-auth-key",
    "ttl_days": 1,
    "device_name": "pi5-001",
    "tags": ["production", "kiosk"]
}
```

**HTTP**

```http
POST /organisation/auth-keys HTTP/1.1
Host: api.connect.raspberrypi.com
Authorization: Bearer rporg_accesstokenhere
Content-Type: application/x-www-form-urlencoded

description=my-auth-key&ttl_days=1&device_name=pi5-001&tags[]=production&tags[]=kiosk
```

**curl**

```bash
$ curl --header 'Authorization: Bearer rporg_accesstokenhere' --data-urlencode 'description=my-auth-key' --data-urlencode 'ttl_days=1' --data-urlencode 'device_name=pi5-001' --data-urlencode 'tags[]=production' --data-urlencode 'tags[]=kiosk' https://api.connect.raspberrypi.com/organisation/auth-keys
```

如果成功，你会收到 **201 Created** 响应，其中包含 JSON 格式的认证密钥。例如：

```http
HTTP/2 201
Content-Type: application/json; charset=utf-8

{
    "id": "12345",
    "description": "my-auth-key",
    "device_name": "pi5-001",
    "tags": ["production", "kiosk"],
    "secret": "rpoak_123456",
    "expires_at": "2025-01-01T00:00:30Z",
    "exchanged_at": null,
    "created_at": "2024-12-31T00:00:30Z"
}
```

响应包含以下字段：

* `id`：认证密钥的唯一标识符。
* `description`：创建认证密钥时使用的说明。
* `device_name`：交换认证密钥时分配给设备的名称。
* `tags`：交换认证密钥时应用于设备的标签。
* `secret`：以 `rpoak_` 为前缀的随机令牌。
* `expires_at`：密钥过期的日期和时间（ISO 8601 格式）。
* `exchanged_at`：认证密钥交换以关联设备的日期和时间（ISO 8601 格式）；如果尚未交换，则为 `null`。
* `created_at`：创建认证密钥的日期和时间（ISO 8601 格式）。

然后，可以在 `secret` 过期前使用它来[将设备关联到 Connect](shu-mei-pai-yuan-cheng-fang-wen-raspberry-pi-connect.md)。

否则，你会收到以下响应之一：

| 响应 | 说明 | 示例 |
| ---- | ---- | ---- |
| **401 Unauthorized** | 管理 API 访问令牌无效。 |  |
| **422 Unprocessable Content** | 无法创建认证密钥。 | `{"message":"Validation failed: Description can't be blank"}` |

>**注意**
>
>你也可以在组织的**设置**页面手动创建认证密钥。

### 列出认证密钥

要列出组织中的所有认证密钥，请使用[管理 API 访问令牌](#创建管理-api-访问令牌)发出以下 HTTP 请求。

替换以下代码中的这些值：

* `rporg_accesstokenhere`：你的管理 API 访问令牌。

**HTTP**

```http
GET /organisation/auth-keys HTTP/1.1
Host: api.connect.raspberrypi.com
Authorization: Bearer rporg_accesstokenhere
```

**curl**

```bash
$ curl --header 'Authorization: Bearer rporg_accesstokenhere' https://api.connect.raspberrypi.com/organisation/auth-keys
```

如果成功，你会收到 **200 OK** 响应，其中包含组织中最多 100 个认证密钥（以 JSON 格式表示），排序为：可用的认证密钥在前，其次是已过期的，最后是已交换的；每组内最新的在前。例如：

```http
HTTP/2 200
Content-Type: application/json; charset=utf-8

{
    "auth_keys": [
        {
            "id": "096ce472-2cbd-412a-8295-6c03a1a07ba4",
            "description": "my-auth-key",
            "device_name": "pi5-001",
            "tags": ["production", "kiosk"],
            "expires_at": "2026-02-26T16:09:52Z",
            "exchanged_at": null,
            "created_at": "2026-02-25T16:09:52Z"
        }
    ],
    "meta": {
        "page": 1,
        "per_page": 100,
        "total_count": 1,
        "total_pages": 1
    }
}
```

响应包含以下字段：

* `auth_keys`：组织中的认证密钥列表（每页最多 100 个）。
* `meta`：分页详情。

`auth_keys` 列表中的每一项包含以下字段：

* `id`：认证密钥的唯一标识符。
* `description`：创建认证密钥时使用的说明。
* `device_name`：交换认证密钥时分配给设备的名称。
* `tags`：交换认证密钥时应用于设备的标签。
* `expires_at`：密钥过期的日期和时间（ISO 8601 格式）。
* `exchanged_at`：认证密钥交换以关联设备的日期和时间（ISO 8601 格式）；如果尚未交换，则为 `null`。
* `created_at`：创建认证密钥的日期和时间（ISO 8601 格式）。

>**注意**
>
>`secret` 仅在首次创建认证密钥时包含在响应中，之后无法再次查看。

`meta` 对象包含以下字段：

* `page`：响应的当前页码。
* `per_page`：每页的认证密钥数量（最多 100）。
* `total_count`：组织中的认证密钥总数。
* `total_pages`：组织认证密钥的总页数。

如果管理 API 访问令牌无效，你会收到 **401 Unauthorized** 响应。

`page` 和 `per_page` 查询参数的用法与[列出设备](#列出设备)相同。

### 显示认证密钥

要显示组织中的单个认证密钥，请使用[管理 API 访问令牌](#创建管理-api-访问令牌)发出以下 HTTP 请求。

替换以下代码中的这些值：

* `rporg_accesstokenhere`：你的管理 API 访问令牌。
* `auth-key-id`：认证密钥的唯一标识符。

**HTTP**

```http
GET /organisation/auth-keys/auth-key-id HTTP/1.1
Host: api.connect.raspberrypi.com
Authorization: Bearer rporg_accesstokenhere
```

**curl**

```bash
$ curl --header 'Authorization: Bearer rporg_accesstokenhere' https://api.connect.raspberrypi.com/organisation/auth-keys/auth-key-id
```

如果成功，你会收到 **200 OK** 响应，其中包含 JSON 格式的认证密钥详情。例如：

```http
HTTP/2 200
Content-Type: application/json; charset=utf-8

{
    "id": "096ce472-2cbd-412a-8295-6c03a1a07ba4",
    "description": "my-auth-key",
    "device_name": "pi5-001",
    "tags": ["production", "kiosk"],
    "expires_at": "2026-02-26T16:09:52Z",
    "exchanged_at": null,
    "created_at": "2026-02-25T16:09:52Z"
}
```

否则，你会收到以下响应之一：

| 响应 | 说明 |
| ---- | ---- |
| **401 Unauthorized** | 管理 API 访问令牌无效。 |
| **404 Not Found** | 组织中找不到该认证密钥。 |

### 更新认证密钥

要更新组织中的现有认证密钥，请使用[管理 API 访问令牌](#创建管理-api-访问令牌)发出以下 HTTP 请求。

替换以下代码中的这些值：

* `rporg_accesstokenhere`：你的管理 API 访问令牌。
* `auth-key-id`：认证密钥的唯一标识符。
* `my-renamed-auth-key`：认证密钥的新说明。
* `pi5-001`：交换认证密钥时分配给设备的新名称（可选）。
* `production`、`kiosk`：交换认证密钥时应用于设备的标签（可选）。

**JSON**

```http
PATCH /organisation/auth-keys/auth-key-id HTTP/1.1
Host: api.connect.raspberrypi.com
Authorization: Bearer rporg_accesstokenhere
Content-Type: application/json

{
    "description": "my-renamed-auth-key",
    "device_name": "pi5-001",
    "tags": ["production", "kiosk"]
}
```

**curl**

```bash
$ curl --request PATCH --header 'Authorization: Bearer rporg_accesstokenhere' --header 'Content-Type: application/json' --data '{"description":"my-renamed-auth-key","device_name":"pi5-001","tags":["production","kiosk"]}' https://api.connect.raspberrypi.com/organisation/auth-keys/auth-key-id
```

如果成功，你会收到 **200 OK** 响应，其中包含 JSON 格式的更新后认证密钥：

```http
HTTP/2 200
Content-Type: application/json; charset=utf-8

{
    "id": "096ce472-2cbd-412a-8295-6c03a1a07ba4",
    "description": "my-renamed-auth-key",
    "device_name": "pi5-001",
    "tags": ["production", "kiosk"],
    "expires_at": "2026-02-26T16:09:52Z",
    "exchanged_at": null,
    "created_at": "2026-02-25T16:09:52Z"
}
```

否则，你会收到以下响应之一：

| 响应 | 说明 | 示例 |
| ---- | ---- | ---- |
| **401 Unauthorized** | 管理 API 访问令牌无效。 |  |
| **404 Not Found** | 组织中找不到该认证密钥。 |  |
| **422 Unprocessable Content** | 认证密钥已过期或已经交换。 | `{"message":"This auth key can no longer be edited."}` |
| **422 Unprocessable Content** | 因其他任何原因无法更新认证密钥。 | `{"message":"Validation failed: Description can't be blank"}` |

### 删除认证密钥

要删除组织中的认证密钥，请使用[管理 API 访问令牌](#创建管理-api-访问令牌)发出以下 HTTP 请求。

替换以下代码中的这些值：

* `rporg_accesstokenhere`：你的管理 API 访问令牌。
* `auth-key-id`：认证密钥的唯一标识符。

**HTTP**

```http
DELETE /organisation/auth-keys/auth-key-id HTTP/1.1
Host: api.connect.raspberrypi.com
Authorization: Bearer rporg_accesstokenhere
```

**curl**

```bash
$ curl --request DELETE --header 'Authorization: Bearer rporg_accesstokenhere' https://api.connect.raspberrypi.com/organisation/auth-keys/auth-key-id
```

你可以删除任何认证密钥，包括已过期或已经交换的认证密钥。删除已交换的认证密钥不会影响关联的设备。

如果成功，你会收到 **200 OK** 响应，其中包含 JSON 格式的已删除认证密钥详情。例如：

```http
HTTP/2 200
Content-Type: application/json; charset=utf-8

{
    "id": "096ce472-2cbd-412a-8295-6c03a1a07ba4",
    "description": "my-auth-key",
    "device_name": "pi5-001",
    "tags": ["production", "kiosk"],
    "expires_at": "2026-02-26T16:09:52Z",
    "exchanged_at": null,
    "created_at": "2026-02-25T16:09:52Z"
}
```

否则，你会收到以下响应之一：

| 响应 | 说明 |
| ---- | ---- |
| **401 Unauthorized** | 管理 API 访问令牌无效。 |
| **404 Not Found** | 组织中找不到该认证密钥。 |

### 列出设备

要列出组织中的所有设备，请使用管理 API 访问令牌发出以下 HTTP 请求。

替换以下代码中的这些值：

* `rporg_accesstokenhere`：你的管理 API 访问令牌。

**HTTP**

```http
GET /organisation/devices HTTP/1.1
Host: api.connect.raspberrypi.com
Authorization: Bearer rporg_accesstokenhere
```

**curl**

```bash
$ curl --header 'Authorization: Bearer rporg_accesstokenhere' https://api.connect.raspberrypi.com/organisation/devices
```

如果成功，你会收到 **200 OK** 响应，其中包含组织中最多 100 台设备（以 JSON 格式表示），按名称的字母顺序排序。例如：

```http
HTTP/2 200
Content-Type: application/json; charset=utf-8

{
    "devices": [
        {
            "id": "69739b44-ebb2-468e-9e24-08126dec4925",
            "name": "raspberrypi5",
            "serial_number": "ea636879c4d47a37",
            "tags": ["production", "kiosk"],
            "board": {
                "model": "Raspberry Pi 5",
                "revision": "1.0",
                "memory": "8 GB"
            },
            "os": {
                "name": "Raspberry Pi OS",
                "version": "13 (Trixie)"
            },
            "kernel_architecture": "aarch64",
            "filters": {
                "model": "5",
                "memory": "8gb",
                "os": "raspios-13"
            }
        }
    ],
    "meta": {
        "page": 1,
        "per_page": 100,
        "total_count": 1,
        "total_pages": 1
    }
}
```

响应包含以下字段：

* `devices`：组织中的设备列表（每页最多 100 台）。
* `meta`：分页详情。

`devices` 列表中的每一项包含以下字段：

* `id`：设备的唯一标识符。
* `name`：设备的名称。
* `serial_number`：设备的序列号。
* `tags`：应用于设备的标签。
* `board`：设备的板型号、修订版和内存。未知时为 `null`。
* `os`：设备上运行的操作系统名称和版本。未知时为 `null`。
* `kernel_architecture`：设备报告的内核架构（例如 `aarch64`）。未知时为 `null`。
* `filters`：与此设备匹配的限定符，用于 `query` 参数（见下文）。仅包含已知的设备属性，因此该对象可能为空。

`board`、`os`、`kernel_architecture` 和 `filters` 字段仅对运行 Connect 客户端 2.9.0 或更高版本的设备填充。

`meta` 对象包含以下字段：

* `page`：响应的当前页码。
* `per_page`：每页的设备数量（最多 100）。
* `total_count`：组织中的设备总数。
* `total_pages`：组织设备的总页数。

如果管理 API 访问令牌无效，你会收到 **401 Unauthorized** 响应。

要获取后续的设备页，请在查询字符串中使用 `page` 参数：

**HTTP**

```http
GET /organisation/devices?page=2 HTTP/1.1
Host: api.connect.raspberrypi.com
Authorization: Bearer rporg_accesstokenhere
```

**curl**

```bash
$ curl --header 'Authorization: Bearer rporg_accesstokenhere' 'https://api.connect.raspberrypi.com/organisation/devices?page=2'
```

要更改每页返回的设备数量，请在查询字符串中使用 `per_page` 参数（最大值为 100）：

**HTTP**

```http
GET /organisation/devices?per_page=10 HTTP/1.1
Host: api.connect.raspberrypi.com
Authorization: Bearer rporg_accesstokenhere
```

**curl**

```bash
$ curl --header 'Authorization: Bearer rporg_accesstokenhere' 'https://api.connect.raspberrypi.com/organisation/devices?per_page=10'
```

要筛选返回的设备，请在查询字符串中使用 `query` 参数。它接受与[Web 界面中的搜索栏](#搜索和筛选设备)相同的语法，结合自由文本搜索和结构化筛选：

* 自由文本会匹配设备名称和序列号。
* `model:`、`memory:`、`os:` 和 `tag:` 限定符按特定属性筛选（例如 `model:5` 或 `tag:production`）。

你可以在单个查询中组合多个筛选条件和自由文本。该值必须进行 URL 编码，包括各项之间的空格。

例如，要查找带有 `production` 标签的 Raspberry Pi 5 设备：

**HTTP**

```http
GET /organisation/devices?query=model%3A5%20tag%3Aproduction HTTP/1.1
Host: api.connect.raspberrypi.com
Authorization: Bearer rporg_accesstokenhere
```

**curl**

```bash
$ curl --header 'Authorization: Bearer rporg_accesstokenhere' --get --data-urlencode 'query=model:5 tag:production' https://api.connect.raspberrypi.com/organisation/devices
```

`query` 参数可以与 `page` 和 `per_page` 参数组合使用，因此你可以在筛选后的列表中分页。

为每台设备返回的 `filters` 对象列出了与其匹配的确切限定符值，因此你可以使用这些值构建 `query`。例如，`filters` 中包含 `"os": "raspios-13"` 的设备与查询 `os:raspios-13` 匹配。

`model:` 限定符接受以下值：

| 值 | 型号 |
| ---- | ---- |
| `a` | Raspberry Pi A |
| `b` | Raspberry Pi B |
| `a+` | Raspberry Pi A+ |
| `b+` | Raspberry Pi B+ |
| `2b` | Raspberry Pi 2B |
| `cm1` | Raspberry Pi CM1 |
| `3b` | Raspberry Pi 3B |
| `zero` | Raspberry Pi Zero |
| `cm3` | Raspberry Pi CM3 |
| `zerow` | Raspberry Pi Zero W |
| `3b+` | Raspberry Pi 3B+ |
| `3a+` | Raspberry Pi 3A+ |
| `cm3+` | Raspberry Pi CM3+ |
| `4b` | Raspberry Pi 4B |
| `zero2w` | Raspberry Pi Zero 2 W |
| `400` | Raspberry Pi 400 |
| `cm4` | Raspberry Pi CM4 |
| `cm4s` | Raspberry Pi CM4S |
| `5` | Raspberry Pi 5 |
| `cm5` | Raspberry Pi CM5 |
| `500` | Raspberry Pi 500 |
| `cm5lite` | Raspberry Pi CM5 Lite |
| `cm0` | Raspberry Pi CM0 |

`memory:` 限定符接受以下值：

| 值 | 内存 |
| ---- | ---- |
| `256mb` | 256 MB |
| `512mb` | 512 MB |
| `1gb` | 1 GB |
| `2gb` | 2 GB |
| `4gb` | 4 GB |
| `8gb` | 8 GB |
| `16gb` | 16 GB |

>**注意**
>
>与 Web 界面一样，`model:`、`memory:` 和 `os:` 限定符只能匹配运行 Connect 客户端 2.9.0 或更高版本的设备。

### 显示设备

要显示组织中的单台设备，请使用管理 API 访问令牌发出以下 HTTP 请求。

替换以下代码中的这些值：

* `rporg_accesstokenhere`：你的管理 API 访问令牌。
* `device-id`：设备的唯一标识符。

**HTTP**

```http
GET /organisation/devices/device-id HTTP/1.1
Host: api.connect.raspberrypi.com
Authorization: Bearer rporg_accesstokenhere
```

**curl**

```bash
$ curl --header 'Authorization: Bearer rporg_accesstokenhere' https://api.connect.raspberrypi.com/organisation/devices/device-id
```

如果成功，你会收到 **200 OK** 响应，其中包含 JSON 格式的设备详情。例如：

```http
HTTP/2 200
Content-Type: application/json; charset=utf-8

{
    "id": "69739b44-ebb2-468e-9e24-08126dec4925",
    "name": "raspberrypi5",
    "serial_number": "ea636879c4d47a37",
    "tags": ["production", "kiosk"],
    "board": {
        "model": "Raspberry Pi 5",
        "revision": "1.0",
        "memory": "8 GB"
    },
    "os": {
        "name": "Raspberry Pi OS",
        "version": "13 (Trixie)"
    },
    "kernel_architecture": "aarch64",
    "filters": {
        "model": "5",
        "memory": "8gb",
        "os": "raspios-13"
    }
}
```

响应包含的字段与列出设备时返回的 `devices` 列表中每一项的字段相同。`board`、`os`、`kernel_architecture` 和 `filters` 字段仅对运行 Connect 客户端 2.9.0 或更高版本的设备填充。

否则，你会收到以下响应之一：

| 响应 | 说明 |
| ---- | ---- |
| **401 Unauthorized** | 管理 API 访问令牌无效。 |
| **404 Not Found** | 组织中找不到给定的设备 ID。 |

### 更新设备

要更新组织中设备的名称或标签，请使用管理 API 访问令牌发出以下 HTTP 请求。

两个字段都是可选的：请求体中省略的任何字段都保持不变。

`tags` 字段会替换设备的现有标签，因此请包含所有要保留的标签。标签名称不得超过 30 个字符，并且只能包含小写字母、数字、连字符和下划线。每台设备最多支持十个标签。

要移除所有标签，请传入空列表（`"tags": []`）。

替换以下代码中的这些值：

* `rporg_accesstokenhere`：你的管理 API 访问令牌。
* `device-id`：设备的唯一标识符。
* `raspberrypi5`：设备的新名称（可选）。
* `production`、`kiosk`：设备的新标签（可选）。

**JSON**

```http
PATCH /organisation/devices/device-id HTTP/1.1
Host: api.connect.raspberrypi.com
Authorization: Bearer rporg_accesstokenhere
Content-Type: application/json

{
    "name": "raspberrypi5",
    "tags": ["production", "kiosk"]
}
```

**curl**

```bash
$ curl --request PATCH --header 'Authorization: Bearer rporg_accesstokenhere' --header 'Content-Type: application/json' --data '{"name":"raspberrypi5","tags":["production","kiosk"]}' https://api.connect.raspberrypi.com/organisation/devices/device-id
```

如果成功，你会收到 **200 OK** 响应，其中包含 JSON 格式的更新后设备：

```http
HTTP/2 200
Content-Type: application/json; charset=utf-8

{
    "id": "69739b44-ebb2-468e-9e24-08126dec4925",
    "name": "raspberrypi5",
    "serial_number": "ea636879c4d47a37",
    "tags": ["production", "kiosk"],
    "board": {
        "model": "Raspberry Pi 5",
        "revision": "1.0",
        "memory": "8 GB"
    },
    "os": {
        "name": "Raspberry Pi OS",
        "version": "13 (Trixie)"
    },
    "kernel_architecture": "aarch64",
    "filters": {
        "model": "5",
        "memory": "8gb",
        "os": "raspios-13"
    }
}
```

否则，你会收到以下响应之一：

| 响应 | 说明 | 示例 |
| ---- | ---- | ---- |
| **401 Unauthorized** | 管理 API 访问令牌无效。 |  |
| **404 Not Found** | 组织中找不到给定的设备 ID。 |  |
| **422 Unprocessable Content** | 无法更新设备。 | `{"message":"Validation failed: Name can't be blank"}` |

### 删除设备

要删除组织中的设备并使其退出 Raspberry Pi Connect 登录，请使用管理 API 访问令牌发出以下 HTTP 请求。

替换以下代码中的这些值：

* `rporg_accesstokenhere`：你的管理 API 访问令牌。
* `device-id`：设备的唯一标识符。

**HTTP**

```http
DELETE /organisation/devices/device-id HTTP/1.1
Host: api.connect.raspberrypi.com
Authorization: Bearer rporg_accesstokenhere
```

**curl**

```bash
$ curl --request DELETE --header 'Authorization: Bearer rporg_accesstokenhere' https://api.connect.raspberrypi.com/organisation/devices/device-id
```

如果成功，你会收到 **200 OK** 响应，其中包含 JSON 格式的已删除设备详情。例如：

```http
HTTP/2 200
Content-Type: application/json; charset=utf-8

{
    "id": "69739b44-ebb2-468e-9e24-08126dec4925",
    "name": "raspberrypi5",
    "serial_number": "ea636879c4d47a37",
    "tags": ["production", "kiosk"],
    "board": {
        "model": "Raspberry Pi 5",
        "revision": "1.0",
        "memory": "8 GB"
    },
    "os": {
        "name": "Raspberry Pi OS",
        "version": "13 (Trixie)"
    },
    "kernel_architecture": "aarch64",
    "filters": {
        "model": "5",
        "memory": "8gb",
        "os": "raspios-13"
    }
}
```

否则，你会收到以下响应之一：

| 响应 | 说明 |
| ---- | ---- |
| **401 Unauthorized** | 管理 API 访问令牌无效。 |
| **404 Not Found** | 组织中找不到给定的设备 ID。 |

### 列出构件

要列出组织中的所有远程更新构件，请使用[管理 API 访问令牌](#创建管理-api-访问令牌)发出以下 HTTP 请求。

替换以下代码中的这些值：

* `rporg_accesstokenhere`：你的管理 API 访问令牌。

**HTTP**

```http
GET /organisation/artefacts HTTP/1.1
Host: api.connect.raspberrypi.com
Authorization: Bearer rporg_accesstokenhere
```

**curl**

```bash
$ curl --header 'Authorization: Bearer rporg_accesstokenhere' https://api.connect.raspberrypi.com/organisation/artefacts
```

如果成功，你会收到 **200 OK** 响应，其中包含组织中最多 100 个构件（以 JSON 格式表示），先按名称的字母顺序排序，再按创建时间排序，最早的在前。例如：

```http
HTTP/2 200
Content-Type: application/json; charset=utf-8

{
    "artefacts": [
        {
            "id": "ee92e7e6-2c2c-4e7d-9d80-2cce8a6c7e8a",
            "name": "kiosk-v1.0",
            "type": "uri",
            "uri": "https://example.com/kiosk-v1.0.tar.zst",
            "checksum": "d39fc02ad7878db7f6803f54dfce89346a763a603cb8e62221ba893fee9c5cc6",
            "expires_at": null,
            "created_at": "2026-02-25T16:09:52Z"
        }
    ],
    "meta": {
        "page": 1,
        "per_page": 100,
        "total_count": 1,
        "total_pages": 1
    }
}
```

每个构件都有以下字段：

* `id`：构件的唯一标识符。
* `name`：构件的名称。名称在组织内不必唯一。
* `type`：构件的提供方式：`uri` 表示[自行托管](#自行托管更新构件)的构件，`file` 表示上传到 Connect 的构件。
* `uri`：设备下载构件的位置。对于上传的构件，这是指向已上传文件的链接；一旦 Connect 删除该文件，则为 `null`。
* `checksum`：构件的十六进制编码 SHA-256 校验和。
* `expires_at`：上传构件过期且无法再部署的日期和时间（ISO 8601 格式）；对于自行托管的构件为 `null`。
* `created_at`：创建构件的日期和时间（ISO 8601 格式）。

要筛选返回的构件，请在查询字符串中使用 `name` 参数。这会按构件名称进行不区分大小写的前缀匹配：

**HTTP**

```http
GET /organisation/artefacts?name=kiosk HTTP/1.1
Host: api.connect.raspberrypi.com
Authorization: Bearer rporg_accesstokenhere
```

**curl**

```bash
$ curl --header 'Authorization: Bearer rporg_accesstokenhere' --get --data-urlencode 'name=kiosk' https://api.connect.raspberrypi.com/organisation/artefacts
```

`page` 和 `per_page` 查询参数的用法与[列出设备](#列出设备)相同，并且可以与 `name` 参数组合使用，因此你可以在筛选后的列表中分页。

如果管理 API 访问令牌无效，你会收到 **401 Unauthorized** 响应。

### 显示构件

要显示组织中的单个远程更新构件，请使用[管理 API 访问令牌](#创建管理-api-访问令牌)发出以下 HTTP 请求。

替换以下代码中的这些值：

* `rporg_accesstokenhere`：你的管理 API 访问令牌。
* `artefact-id`：构件的唯一标识符。

**HTTP**

```http
GET /organisation/artefacts/artefact-id HTTP/1.1
Host: api.connect.raspberrypi.com
Authorization: Bearer rporg_accesstokenhere
```

**curl**

```bash
$ curl --header 'Authorization: Bearer rporg_accesstokenhere' https://api.connect.raspberrypi.com/organisation/artefacts/artefact-id
```

如果成功，你会收到 **200 OK** 响应，其中包含 JSON 格式的构件[详情](#列出构件)。例如：

```http
HTTP/2 200
Content-Type: application/json; charset=utf-8

{
    "id": "ee92e7e6-2c2c-4e7d-9d80-2cce8a6c7e8a",
    "name": "kiosk-v1.0",
    "type": "uri",
    "uri": "https://example.com/kiosk-v1.0.tar.zst",
    "checksum": "d39fc02ad7878db7f6803f54dfce89346a763a603cb8e62221ba893fee9c5cc6",
    "expires_at": null,
    "created_at": "2026-02-25T16:09:52Z"
}
```

否则，你会收到以下响应之一：

| 响应 | 说明 |
| ---- | ---- |
| **401 Unauthorized** | 管理 API 访问令牌无效。 |
| **404 Not Found** | 组织中找不到给定的构件 ID。 |

### 创建构件

要为组织创建远程更新构件，请使用[管理 API 访问令牌](#创建管理-api-访问令牌)发出以下 HTTP 请求。

>**注意**
>
>管理 API 只能创建[自行托管](#自行托管更新构件)的构件。要上传构件，请使用[远程更新标签页](#管理构件库)。

替换以下代码中的这些值：

* `rporg_accesstokenhere`：你的管理 API 访问令牌。
* `kiosk-v1.0`：构件的名称。名称在组织内不必唯一。
* `https://example.com/kiosk-v1.0.tar.zst`：设备下载构件的 URI。
* `d39fc02ad7878db7f6803f54dfce89346a763a603cb8e62221ba893fee9c5cc6`：构件的十六进制编码 SHA-256 校验和。

**JSON**

```http
POST /organisation/artefacts HTTP/1.1
Host: api.connect.raspberrypi.com
Authorization: Bearer rporg_accesstokenhere
Content-Type: application/json

{
    "name": "kiosk-v1.0",
    "uri": "https://example.com/kiosk-v1.0.tar.zst",
    "checksum": "d39fc02ad7878db7f6803f54dfce89346a763a603cb8e62221ba893fee9c5cc6"
}
```

**curl**

```bash
$ curl --header 'Authorization: Bearer rporg_accesstokenhere' --data-urlencode 'name=kiosk-v1.0' --data-urlencode 'uri=https://example.com/kiosk-v1.0.tar.zst' --data-urlencode 'checksum=d39fc02ad7878db7f6803f54dfce89346a763a603cb8e62221ba893fee9c5cc6' https://api.connect.raspberrypi.com/organisation/artefacts
```

如果成功，你会收到 **201 Created** 响应，其中包含 JSON 格式的构件详情。例如：

```http
HTTP/2 201
Content-Type: application/json; charset=utf-8

{
    "id": "ee92e7e6-2c2c-4e7d-9d80-2cce8a6c7e8a",
    "name": "kiosk-v1.0",
    "type": "uri",
    "uri": "https://example.com/kiosk-v1.0.tar.zst",
    "checksum": "d39fc02ad7878db7f6803f54dfce89346a763a603cb8e62221ba893fee9c5cc6",
    "expires_at": null,
    "created_at": "2026-02-25T16:09:52Z"
}
```

否则，你会收到以下响应之一：

| 响应 | 说明 | 示例 |
| ---- | ---- | ---- |
| **401 Unauthorized** | 管理 API 访问令牌无效。 |  |
| **422 Unprocessable Content** | 无法创建构件。 | `{"message":"Validation failed: Name can't be blank"}` |

### 删除构件

要删除组织中的构件，请使用[管理 API 访问令牌](#创建管理-api-访问令牌)发出以下 HTTP 请求。

替换以下代码中的这些值：

* `rporg_accesstokenhere`：你的管理 API 访问令牌。
* `artefact-id`：构件的 `id`（由[创建构件](#创建构件)返回）。

**HTTP**

```http
DELETE /organisation/artefacts/artefact-id HTTP/1.1
Host: api.connect.raspberrypi.com
Authorization: Bearer rporg_accesstokenhere
```

**curl**

```bash
$ curl --request DELETE --header 'Authorization: Bearer rporg_accesstokenhere' https://api.connect.raspberrypi.com/organisation/artefacts/artefact-id
```

如果成功，你会收到 **200 OK** 响应，其中包含 JSON 格式的已删除构件详情。例如：

```http
HTTP/2 200
Content-Type: application/json; charset=utf-8

{
    "id": "ee92e7e6-2c2c-4e7d-9d80-2cce8a6c7e8a",
    "name": "kiosk-v1.0",
    "type": "uri",
    "uri": "https://example.com/kiosk-v1.0.tar.zst",
    "checksum": "d39fc02ad7878db7f6803f54dfce89346a763a603cb8e62221ba893fee9c5cc6",
    "expires_at": null,
    "created_at": "2026-02-25T16:09:52Z"
}
```

否则，你会收到以下响应之一：

| 响应 | 说明 | 示例 |
| ---- | ---- | ---- |
| **401 Unauthorized** | 管理 API 访问令牌无效。 |  |
| **404 Not Found** | 组织中找不到给定的构件 ID。 |  |
| **422 Unprocessable Content** | 构件已部署到设备。 | `{"message":"Cannot delete artefacts that have been deployed"}` |

### 列出部署

要列出组织中某台设备的远程更新部署，请使用[管理 API 访问令牌](#创建管理-api-访问令牌)发出以下 HTTP 请求。

替换以下代码中的这些值：

* `rporg_accesstokenhere`：你的管理 API 访问令牌。
* `device-id`：设备的唯一标识符。

**HTTP**

```http
GET /organisation/devices/device-id/deployments HTTP/1.1
Host: api.connect.raspberrypi.com
Authorization: Bearer rporg_accesstokenhere
```

**curl**

```bash
$ curl --header 'Authorization: Bearer rporg_accesstokenhere' https://api.connect.raspberrypi.com/organisation/devices/device-id/deployments
```

如果成功，你会收到 **200 OK** 响应，其中包含该设备最多 100 个部署（以 JSON 格式表示），最近的排在最前面。例如：

```http
HTTP/2 200
Content-Type: application/json; charset=utf-8

{
    "deployments": [
        {
            "id": "fdf45c44-2c0e-4f12-9b04-3a6a1c0d3b8d",
            "state": "failed",
            "state_reason": "Checksum mismatch",
            "device_id": "69739b44-ebb2-468e-9e24-08126dec4925",
            "artefact_id": "ee92e7e6-2c2c-4e7d-9d80-2cce8a6c7e8a",
            "created_at": "2026-02-25T16:09:52Z",
            "updated_at": "2026-02-25T16:10:30Z"
        }
    ],
    "meta": {
        "page": 1,
        "per_page": 100,
        "total_count": 1,
        "total_pages": 1
    }
}
```

每个部署的 `state` 是 `pending`、`in_progress`、`succeeded`、`failed` 或 `cancelled` 之一。对于 `failed` 部署，`state_reason` 包含部署失败原因的人类可读说明（例如校验和不匹配，或部署被更新的部署取代）；对于其他状态，其值为 `null`。

要筛选返回的部署，请在查询字符串中使用 `state` 参数，并带上上述状态之一：

**HTTP**

```http
GET /organisation/devices/device-id/deployments?state=pending HTTP/1.1
Host: api.connect.raspberrypi.com
Authorization: Bearer rporg_accesstokenhere
```

**curl**

```bash
$ curl --header 'Authorization: Bearer rporg_accesstokenhere' 'https://api.connect.raspberrypi.com/organisation/devices/device-id/deployments?state=pending'
```

`page` 和 `per_page` 查询参数的用法与[列出设备](#列出设备)相同。

否则，你会收到以下响应之一：

| 响应 | 说明 | 示例 |
| ---- | ---- | ---- |
| **400 Bad Request** | `state` 参数不是可识别的状态之一。 | `{"message":"Unknown state \"exploded\""}` |
| **401 Unauthorized** | 管理 API 访问令牌无效。 |  |
| **404 Not Found** | 组织中找不到给定的设备 ID。 |  |

### 显示部署

要显示组织中的单个部署，请使用[管理 API 访问令牌](#创建管理-api-访问令牌)发出以下 HTTP 请求。

替换以下代码中的这些值：

* `rporg_accesstokenhere`：你的管理 API 访问令牌。
* `deployment-id`：部署的唯一标识符。

**HTTP**

```http
GET /organisation/deployments/deployment-id HTTP/1.1
Host: api.connect.raspberrypi.com
Authorization: Bearer rporg_accesstokenhere
```

**curl**

```bash
$ curl --header 'Authorization: Bearer rporg_accesstokenhere' https://api.connect.raspberrypi.com/organisation/deployments/deployment-id
```

如果成功，你会收到 **200 OK** 响应，其中包含 JSON 格式的部署详情。例如：

```http
HTTP/2 200
Content-Type: application/json; charset=utf-8

{
    "id": "fdf45c44-2c0e-4f12-9b04-3a6a1c0d3b8d",
    "state": "succeeded",
    "state_reason": null,
    "device_id": "69739b44-ebb2-468e-9e24-08126dec4925",
    "artefact_id": "ee92e7e6-2c2c-4e7d-9d80-2cce8a6c7e8a",
    "created_at": "2026-02-25T16:09:52Z",
    "updated_at": "2026-02-25T16:10:30Z"
}
```

否则，你会收到以下响应之一：

| 响应 | 说明 |
| ---- | ---- |
| **401 Unauthorized** | 管理 API 访问令牌无效。 |
| **404 Not Found** | 组织中找不到该部署。 |

### 创建部署

要将构件部署到设备，请使用[管理 API 访问令牌](#创建管理-api-访问令牌)发出以下 HTTP 请求。新部署会取代已为该设备排队的任何待处理部署。

替换以下代码中的这些值：

* `rporg_accesstokenhere`：你的管理 API 访问令牌。
* `device-id`：接收设备的唯一标识符。
* `artefact-id`：构件的 `id`（由[创建构件](#创建构件)返回）。

**JSON**

```http
POST /organisation/devices/device-id/deployments HTTP/1.1
Host: api.connect.raspberrypi.com
Authorization: Bearer rporg_accesstokenhere
Content-Type: application/json

{
    "artefact_id": "artefact-id"
}
```

**curl**

```bash
$ curl --header 'Authorization: Bearer rporg_accesstokenhere' --data-urlencode 'artefact_id=artefact-id' https://api.connect.raspberrypi.com/organisation/devices/device-id/deployments
```

如果成功，你会收到 **201 Created** 响应，其中包含 JSON 格式的部署详情。例如：

```http
HTTP/2 201
Content-Type: application/json; charset=utf-8

{
    "id": "fdf45c44-2c0e-4f12-9b04-3a6a1c0d3b8d",
    "state": "pending",
    "state_reason": null,
    "device_id": "69739b44-ebb2-468e-9e24-08126dec4925",
    "artefact_id": "ee92e7e6-2c2c-4e7d-9d80-2cce8a6c7e8a",
    "created_at": "2026-02-25T16:09:52Z",
    "updated_at": "2026-02-25T16:09:52Z"
}
```

否则，你会收到以下响应之一：

| 响应 | 说明 | 示例 |
| ---- | ---- | ---- |
| **400 Bad Request** | 缺少 `artefact_id`。 |  |
| **401 Unauthorized** | 管理 API 访问令牌无效。 |  |
| **404 Not Found** | 组织中找不到设备或构件，或者构件已过期。 |  |
| **403 Forbidden** | 组织的免费试用已结束，且尚未设置账单。 | `{"message":"Deployments are blocked until billing has been set up"}` |

### 取消部署

要取消待处理的部署，请使用[管理 API 访问令牌](#创建管理-api-访问令牌)发出以下 HTTP 请求。

替换以下代码中的这些值：

* `rporg_accesstokenhere`：你的管理 API 访问令牌。
* `deployment-id`：部署的唯一标识符。

**HTTP**

```http
PUT /organisation/deployments/deployment-id/cancel HTTP/1.1
Host: api.connect.raspberrypi.com
Authorization: Bearer rporg_accesstokenhere
```

**curl**

```bash
$ curl --request PUT --header 'Authorization: Bearer rporg_accesstokenhere' https://api.connect.raspberrypi.com/organisation/deployments/deployment-id/cancel
```

如果成功，你会收到 **200 OK** 响应，其中包含 JSON 格式的更新后部署详情：

```http
HTTP/2 200
Content-Type: application/json; charset=utf-8

{
    "id": "fdf45c44-2c0e-4f12-9b04-3a6a1c0d3b8d",
    "state": "cancelled",
    "state_reason": null,
    "device_id": "69739b44-ebb2-468e-9e24-08126dec4925",
    "artefact_id": "ee92e7e6-2c2c-4e7d-9d80-2cce8a6c7e8a",
    "created_at": "2026-02-25T16:09:52Z",
    "updated_at": "2026-02-25T16:10:30Z"
}
```

否则，你会收到以下响应之一：

| 响应 | 说明 | 示例 |
| ---- | ---- | ---- |
| **401 Unauthorized** | 管理 API 访问令牌无效。 |  |
| **404 Not Found** | 组织中找不到该部署。 |  |
| **422 Unprocessable Content** | 部署已取消、已成功或已失败，因此无法取消。 | `{"message":"Cannot cancel deployment in state \"succeeded\""}` |

## 批量预配

你可以通过将一台 Raspberry Pi 5 系列设备设置为预配主机，连续预配多台 Raspberry Pi 5 系列设备（Raspberry Pi 5、Raspberry Pi 500 和 Raspberry Pi 500+）。

### 要求

要使用设备身份进行批量预配，必须具备以下条件：

* 两台 Raspberry Pi 5 系列设备（一台作为主机，一台作为接收设备）。
* 一个 Raspberry Pi Connect 组织账号。
* 一根以太网线（此工作流程尚不支持 Wi-Fi）。
* 一根短而高质量的 USB-A 转 USB-C 线缆，用于在预配过程中传输电源和数据。不要使用劣质、仅充电或过长的线缆，否则可能导致预配失败。
* 接收设备的启动介质：一张 32 GB 或更大的存储卡。
* 主机设备：一张 32 GB 或更大的存储卡。为加快预配速度，请使用 32 GB 或更大的 SSD。

### 第 1 步：准备设备

1. 断开或移除接收设备和主机设备上的外部 USB 设备或扩展板。

    USB 设备和扩展板会增加功耗，可能干扰预配过程。

### 第 2 步：在主机设备上安装 `rpi-sb-provisioner`

>**技巧**
>
>镜像生成会占用大量磁盘空间（每次构建可能达到数 GB 或更多），而且在 SSD 上的构建过程明显快于存储卡。Raspberry Pi 500+ 或配备 M.2 HAT+ 的 Raspberry Pi 5 是主机的不错选择。

1. 在主机设备的命令行中输入以下命令，以下载最新固件：

    ```bash
    sudo apt update
    sudo apt upgrade
    ```

2. 在主机设备的命令行中输入以下命令，以安装 Raspberry Pi Secure Boot Provisioner（`rpi-sb-provisioner`）：

    ```bash
    sudo apt update
    sudo apt install rpi-sb-provisioner=2.3.0
    ```

3. 安装完成后，在主机设备的 Web 浏览器中访问 Raspberry Pi Secure Boot Web 预配器界面：http://localhost:3142。

    ![Web 预配器界面确认 `rpi-sb-provisioner` 已成功安装。](https://www.raspberrypi.com/documentation/services/images/provisioner-webui.png)

### 第 3 步：安装 `rpi-image-gen`

`rpi-image-gen` 构建要刷写到接收设备的操作系统镜像。

1. 在主机设备上，从命令行运行以下命令，以从 GitHub 克隆 `rpi-image-gen` 仓库：

    ```bash
    $ git clone https://github.com/raspberrypi/rpi-image-gen.git
    ```

2. 进入克隆的目录，然后运行以下命令安装依赖项：

    ```bash
    $ cd rpi-image-gen
    $ sudo ./install_deps.sh
    ```

### 第 4 步：在主机设备上准备并配置镜像

>**技巧**
>
>rpi-image-gen 包含一个带层和配置的示例应用。更多信息，请参见[远程更新](shu-mei-pai-yuan-cheng-fang-wen-raspberry-pi-connect.md)。

要在主机设备上准备镜像：

1. 进入 `rpi-image-gen` 安装文件夹。
2. 定义构建时要安装的额外软件包。更多信息，请参见 [Packages](https://raspberrypi.github.io/rpi-image-gen/config/index.html#_packages)。
3. 添加无线网络凭据。更多信息，请参见 [Wireless Networking](https://github.com/raspberrypi/rpi-image-gen/tree/master/examples/ota)。
4. 从命令行设置用户账号和密码，并生成构建：

    ```bash
    ./rpi-image-gen build -S ./examples/ota/ -c ota.yaml -- \
      IGconf_device_user1=admin \
      IGconf_device_user1pass='R@spb3rry*pi'
    ```

`rpi-image-gen` 会在 `rpi-image-gen/work/deploy` 文件夹中创建一个 `.tar.zst` 镜像文件。

### 第 5 步：将镜像导入预配器并配置设备

1. 在主机设备上，打开 http://localhost:3142/options/get 处的预配器 Web 界面，或从界面顶部的标签中选择**获取**。
2. 在 **Gold Master OS 镜像**框中，选择**上传新镜像**，然后将刚创建的 `.tar.zst` 文件（例如 `rpi-image-gen/work/deploy-1.0.0/myapp-1.0.0.tar.zst`）拖放到框中。

    ![预配器 Web 界面，显示可用镜像表中列出的操作系统镜像。](https://www.raspberrypi.com/documentation/services/images/provisioner-osimages.png)

3. 在**可用镜像**表中选择该镜像。
4. 向下滚动到**设备与固件**表，然后选择以下内容：

    * 设备系列：**Raspberry Pi 5**。

    ![设备与固件表，显示接收设备的设备类型、存储类型和固件设置。](https://www.raspberrypi.com/documentation/services/images/provisioner-firmware.png)

    * 存储类型：**SD 卡**。
    * 设备固件：**2026-05-26**。

5. 向下滚动到**安全配置**表，然后选择 **Naked**。

    ![预配 Web 界面，显示已选择 Naked 安全配置。](https://www.raspberrypi.com/documentation/services/images/provisioner-security.png)

你的更改会自动保存。

### 第 6 步：创建管理 API 令牌

要让预配器在预配过程中自动向你的 Connect 组织注册设备身份，请创建[管理 API 访问令牌](#创建管理-api-访问令牌)。

1. 打开 Raspberry Pi Connect，然后选择你的组织。
2. 转到 **API 访问令牌**部分，然后选择**预配**标签页。
3. 在**认证密钥**部分选择**新建**，按照屏幕提示配置密钥，然后选择**创建认证密钥**。
4. 复制该密钥。
5. 打开 http://localhost:3142/options/get 处的预配器 Web 界面。
6. 向下滚动到**云服务**部分，然后将密钥粘贴到 **Connect 管理 API 访问令牌**字段中。

![预配 Web 界面的云服务部分，显示 API 访问令牌字段和可选的前缀字段。](https://www.raspberrypi.com/documentation/services/images/provisioner-API.png)

### 第 7 步：将接收设备连接到主机设备

接下来，将接收设备置于 USB 启动模式，以便主机设备接管。

1. 将线缆的 USB-A 端插入主机设备。
2. 按住接收设备的电源按钮，同时插入线缆的 USB-C 端。通电后松开电源按钮。

    接收设备会出现在主机设备的预配器界面中。预配会自动开始。

### 第 8 步：启动接收设备

预配完成后：

1. 从主机设备上拔下接收设备。
2. 将接收设备连接到其自己的电源。
3. 连接一根以太网线。
4. 打开接收设备的电源。

接收设备启动后，会出现在 Raspberry Pi Connect 的**设备**标签页中。
