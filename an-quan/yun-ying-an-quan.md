# 运营安全

运营安全（OpSec）是一种通过减少攻击者获取访问权限或利用漏洞的机会来保护设备的实践。本页介绍提高树莓派运营安全的实用方法。

## 保护用户账户

为防止未经授权的访问，并尽量减少意外或恶意修改系统所造成的影响，你可以通过以下做法保护树莓派：

* 从启动开始就要求输入密码。
* 管理用户权限。
* 对超级用户（`sudo`）命令要求输入密码（设置期间默认启用）。

操作说明以及有关用户账户管理的更多信息，请参阅[用户访问与管理](../shu-mei-pai/xi-tong-pei-zhi.md#用户访问与管理)。

## 更新树莓派系统

为确保系统具备最新的安全功能，我们建议你保持软件为最新状态。更多信息，请参阅树莓派系统页面中的[更新当前的树莓派软件](../shu-mei-pai/raspberry-pi-os.md#更新当前的树莓派软件)。

只有树莓派系统最新的主要版本才会获得所有最新安全修复。因此，我们建议你在最新主要版本发布时也进行升级（例如从 Bookworm 升级到 Trixie）。有关升级操作系统的说明，请参阅[升级到新的大版本](../shu-mei-pai/raspberry-pi-os.md#升级到新的大版本)。

*升级*到最新主要版本与*更新*树莓派系统不同：

* 更新会在你*当前*版本内安装最新的软件包和安全修复，而不会切换到新的主要版本。
* 升级会将你的树莓派迁移到*新的*树莓派系统主要版本。

## 使用防火墙

防火墙通过控制允许或阻止哪些网络连接来帮助保护树莓派。对于大多数用户，我们建议使用 **简单防火墙（UFW）** 来配置防火墙规则、限制对服务的访问，并保护面向互联网的系统。

有关安装、配置和管理 UFW 的说明，请参阅[使用 UFW 的防火墙](ufw-fang-huo-qiang.md)。

## 提高 SSH 安全性

SSH 是远程访问树莓派的常用方式。默认情况下，SSH 需要用户名和密码。要提高 SSH 安全性，请使用基于密钥的身份验证。更多信息，请参阅[配置无密码 SSH](../shu-mei-pai/yuan-cheng-fang-wen.md#配置无密码的-ssh)。

你还可以通过修改 `sshd` 配置来 **允许** 或 **拒绝** 特定用户。更多信息，请参阅[限制可连接的用户](../shu-mei-pai/yuan-cheng-fang-wen.md#限制可连接的用户)。

## 使用 Fail2Ban 阻止可疑活动

将树莓派用作服务器时，你必须刻意在防火墙中开放端口，以允许服务器流量。[Fail2Ban](https://github.com/fail2ban/fail2ban) 可以帮助保护你的服务器。Fail2Ban 会检查日志文件并查找可疑活动，例如多次暴力破解登录尝试。这意味着你不必手动检查日志文件中的入侵尝试，然后再（通过 `iptables`）更新防火墙来阻止它们。

要安装 Fail2Ban，请运行以下命令：

```bash
$ sudo apt install fail2ban
```

安装时，Fail2Ban 会创建 `/etc/fail2ban/jail.conf`。要启用 Fail2Ban，请将 `jail.conf` 复制为 `jail.local`：

```bash
$ sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
```

此配置文件包含一组默认选项，以及用于检查特定服务是否异常的选项。要检查用于 `ssh` 的规则，请在编辑器中打开 `jail.local`：

```bash
$ sudo nano /etc/fail2ban/jail.local
```

如果 `[ssh]` 部分尚不存在，请创建它，然后向该部分添加以下行：

```ini
[ssh]
enabled  = true
port     = ssh
filter   = sshd
backend  = systemd
maxretry = 6
```

这会启用 Fail2Ban 对可疑 `ssh` 活动的检查（包括系统日志检查），并允许在阻止活动之前重试六次。

此文件中的 `[default]` 部分定义默认封禁操作 `iptables-multiport`，当达到检测阈值时，它会运行 `/etc/fail2ban/action.d/iptables-multiport.conf` 文件：

```ini
# 默认封禁操作（例如 iptables、iptables-new、
# iptables-multiport、shorewall 等）。它用于定义
# action_* 变量。可以在全局或 jail.local 文件的
# 每个部分内覆盖
banaction = iptables-multiport
```

Multiport 会封禁所有端口上的所有访问。`action.d` 文件夹包含其他操作配置文件，可用于自定义服务器对可疑活动的响应。

例如，要在三次失败尝试后永久封禁某个 IP 地址，请将 `[ssh]` 部分中的 `maxretry` 值改为 `3`，并将 `bantime` 设置为负数：

```ini
[ssh]
enabled  = true
port     = ssh
filter   = sshd
backend  = systemd
maxretry = 3
bantime  = -1
```
