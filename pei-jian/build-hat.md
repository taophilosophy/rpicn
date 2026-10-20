# Build 扩展板（Build HAT）

## 简介

[树莓派 Build 扩展板](https://raspberrypi.com/products/build-hat)是一块附加板，可连接到树莓派的 40 引脚 GPIO 排针。它与乐高®教育（LEGO® Education）合作设计，可让你轻松使用树莓派计算机控制乐高®机械组（LEGO® Technic™）电机和传感器。

>**警告**
>
> 树莓派 Build 扩展板目前尚不支持树莓派系统 *Trixie*。要使用 Build 扩展板，请暂时安装或继续使用树莓派系统 *Bookworm*。

![Build 扩展板](.gitbook/assets/build-hat.jpg)

>**注意**
>
> 受支持设备的完整列表见[设备兼容性](#设备兼容性)一节。

它为 SPIKE™ 系列产品中的乐高®机械组电机和传感器提供了四个连接器。可用的传感器包括距离传感器、颜色传感器和多用途力传感器。角度电机有多种尺寸，并带有集成编码器，可查询其位置。

Build 扩展板适用于所有带有 40 引脚 GPIO 排针的树莓派计算机，包括借助排线或其他扩展设备连接的键盘系列（Keyboard-series）设备。连接的乐高®机械组设备可轻松用 Python 控制，同时还可搭配摄像头模块等标准树莓派配件。

树莓派 Build 扩展板的电源适配器（PSU）[单独出售](https://raspberrypi.com/products/build-hat-power-supply)，旨在为 Build 扩展板、树莓派计算机以及所有连接的乐高®机械组设备供电。

![电源适配器](.gitbook/assets/psu.jpg)

SPIKE™ Prime 套装 45678 和 SPIKE™ Prime 扩展套装 45681 可从乐高®教育经销商处单独购买，其中包含一组 Build 扩展板支持的实用元件。

>**注意**
>
> 该扩展板可与所有带 40 引脚 GPIO 排针的树莓派开发板配合使用，包括 Zero 系列设备。借助排线或其他扩展设备，也可与键盘系列设备配合使用。

* 最多可控制 SPIKE™ 系列产品中包含的 4 个乐高®机械组电机和传感器
* 易于使用的 [Python 库](https://buildhat.readthedocs.io/)，用于控制你的乐高®机械组设备
* 适用于所有带有 40 引脚 GPIO 排针的树莓派计算机
* 板载 [RP2040](https://www.raspberrypi.com/documentation/microcontrollers/microcontroller-chips.html) 微控制器负责乐高®机械组设备的低层控制
* 外部 8V 电源适配器[单独出售](https://raspberrypi.com/products/build-hat-power-supply)，用于为 Build 扩展板和树莓派供电

>**注意**
>
> Build 扩展板无法为键盘系列设备供电，因为它们不支持通过 GPIO 排针供电。

## 准备你的 Build 扩展板

>**注意**
>
> 在开始使用你的树莓派 Build 扩展板之前，请先设置你的树莓派，并使用[树莓派启动盘制作工具](https://www.raspberrypi.com/downloads/)安装最新版本的操作系统。

将 9 mm 间隔柱装到板的底部。将树莓派 Build 扩展板安装到你的树莓派上。确保方向正确。与其他扩展板不同，所有组件都在底部，为顶部的面包板或乐高®元件留出空间。

![安装 Build 扩展板](.gitbook/assets/fitting-build-hat.webm)

### 访问 GPIO 引脚

如果你想访问树莓派的 GPIO 引脚，可以添加一个可选的长排针，并使用 15 mm 间隔柱。

![长排针](.gitbook/assets/tall-headers.jpg)

下面的引脚由 Build 扩展板本身使用；请勿将任何东西连接到这些引脚上。

| GPIO    | 使用     | 状态   |
| :-----: | :------: | :----: |
| GPIO0/1 | ID prom  |        |
| GPIO4   | 重置     |        |
| GPIO14  | 发送     |        |
| GPIO15  | 接收     |        |
| GPIO16  | RTS      | 未使用 |
| GPIO17  | CTS      | 未使用 |

### 设置你的树莓派

树莓派启动后，单击 Raspberry 菜单按钮，然后选择 **Preferences > Control Centre**，打开控制中心工具。

选择 **Interfaces** 选项卡，并按照下图所示调整串口设置：

![设置](.gitbook/assets/setting-up.png)

#### 以无头方式使用树莓派

如果你以无头方式运行树莓派，并使用 `raspi-config`，请从第一个菜单中选择 “Interface Options”。

![raspi config 1](.gitbook/assets/raspi-config-1.png)

然后选择 “P6 Serial Port”。

![raspi config 2](.gitbook/assets/raspi-config-2.png)

禁用串口控制台：

![raspi config 3](.gitbook/assets/raspi-config-3.png)

然后启用串口硬件。

![raspi config 4](.gitbook/assets/raspi-config-4.png)

最终设置如下所示。

![raspi config 5](.gitbook/assets/raspi-config-5.png)

如果你在此期间进行了一些更改，此时需要重启。

### 为 Build 扩展板供电

连接外部电源：推荐使用[官方树莓派 Build 扩展板电源](https://raspberrypi.com/products/build-hat-power-supply)。不过，任何可靠的 +8V±10% 电源，只要能通过 DC 5521 中心正极桶形连接器（5.5 mm × 2.1 mm × 11 mm）提供 48 W 功率，都能为 Build 扩展板供电。除非你使用的是键盘系列设备，否则无需为树莓派连接额外的 USB 电源。

>**注意**
>
> Build 扩展板无法为键盘系列设备供电，因为它们不支持通过 GPIO 排针供电。

![扩展板供电](.gitbook/assets/powering-build-hat.webm)

>**注意**
>
> 乐高®机械组电机非常强大；因此，要驱动它们，你需要外部 8V 电源。如果你想从电机编码器和 SPIKE™ 力传感器读取数据，可以按照平常的方式，通过树莓派设备的 USB 电源插口为树莓派和 Build 扩展板供电。与电机一样，SPIKE™ 颜色和距离传感器也需要[外部电源](https://raspberrypi.com/products/build-hat-power-supply)。

你可以选择使用 Python 或 .NET 来操作 Build 扩展板。

## 使用 Python 操作 Build 扩展板

### 安装 Build 扩展板 Python 库

要安装 Build 扩展板 Python 库，请打开终端窗口并运行以下命令：

```bash
$ sudo apt install python3-build-hat
```

有关 Build 扩展板 Python 库的更多信息，请参阅 [ReadTheDocs](https://buildhat.readthedocs.io/)。

### 使用 Python 控制电机

有许多电机可与 Build 扩展板配合使用。

#### 连接电机

将电机连接到 Build 扩展板上的 A 端口。LPF2 连接器需要以正确的方向插入。如果连接器无法轻松滑入，请旋转 180 度后重试。

![接入电机](.gitbook/assets/connect-motor.webm)

#### 使用电机

启动 [Thonny IDE](https://thonny.org/)。添加以下程序代码：

```python
from buildhat import Motor

motor_a = Motor('A')

motor_a.run_for_seconds(5)
```

通过单击播放/运行按钮来运行程序。如果这是自树莓派启动以来首次运行 Build 扩展板程序，固件复制到板上的过程中会暂停几秒。红色 LED 熄灭，绿色 LED 点亮。此后运行 Python 程序就不再需要这段等待。

![熄灭灯](.gitbook/assets/blinking-light.webm)

你的电机顺时针转动 5 秒。

![电机转动](.gitbook/assets/turning-motor.webm)

更改程序的最后一行并重新运行。

```python
motor_a.run_for_seconds(5, speed=50)
```

电机现在转得更快了。再做一处更改：

```python
motor_a.run_for_seconds(5, speed=-50)
```

电机向相反方向（逆时针）转动。

单击 Thonny 中的加号按钮创建一个新程序。添加以下代码：

```python
from buildhat import Motor

motor_a = Motor('A')

while True:
    print("Position: ", motor_a.get_aposition())
```

运行程序。抓住电机并转动轴。Thonny REPL 中打印的数字会发生变化。

### 使用 Python 读取传感器

有大量传感器可与 Build 扩展板配合使用。

#### 使用传感器

将颜色传感器连接到 Build 扩展板上的 B 端口，将力传感器连接到 C 端口。

>**注意**
>
> 如果你不打算驱动电机，则无需外部电源，可以使用标准 USB 电源为你的树莓派供电。

创建另一个新程序：

```python
from signal import pause
from buildhat import ForceSensor, ColorSensor

button = ForceSensor('C')
cs = ColorSensor('B')

def handle_pressed(force):
    cs.on()
    print(cs.get_color())

def handle_released(force):
    cs.off()

button.when_pressed = handle_pressed
button.when_released = handle_released
pause()
```

运行程序，将一个彩色物体（乐高®元件最理想）放在颜色传感器前，然后按下力传感器的压杆。传感器的 LED 亮起，Thonny REPL 中会显示最接近的颜色名称。

## 使用 .NET 操作 Build 扩展板

### 安装 .NET 框架

微软的 .NET 框架无法通过 `apt` 在树莓派上安装。不过，你可以参照微软的[官方说明](https://docs.microsoft.com/en-us/dotnet/iot/deployment)来安装 .NET 框架。此外，还有一条简化的[第三方途径](https://www.petecodes.co.uk/install-and-use-microsoft-dot-net-5-with-the-raspberry-pi/)可将 .NET 工具链安装到你的树莓派上。

>**警告**
>
> 安装脚本以 `root` 身份运行。在运行它之前，请先阅读它，并确保你理解它在做什么。如果你有任何疑问，请按照[官方说明](https://docs.microsoft.com/en-us/dotnet/iot/deployment)手动操作。

```bash
$ wget -O - https://raw.githubusercontent.com/pjgpetecodes/dotnet5pi/master/install.sh | sudo bash
```

安装 .NET 框架后，你可以创建你的项目：

```bash
$ dotnet new console --name buildhat
```

这将在 `buildhat` 子目录中创建一个默认程序；要继续操作，需要先进入该目录：

```bash
$ cd buildhat
```

你现在需要安装以下 NuGet 软件包：

```bash
$ dotnet add package System.Device.Gpio --version 2.1.0
$ dotnet add package Iot.Device.Bindings --version 2.1.0
```

### 运行 C# 代码

你可以使用 `dotnet run` 命令运行程序。现在让我们试一下，确保一切正常。它会打印出 “Hello World!”。

```bash
$ dotnet run
Hello World!
```

（在接下来的说明中，当指示“运行程序”时，你只需重新运行 `dotnet run`）

### 编辑 C# 代码

在下面的说明中，你将编辑文件 `buildhat/Program.cs`，即运行上述命令时生成的 C# 程序。

任何文本编辑器都可以用来编辑 C# 代码，包括预装的 Geany IDE/文本编辑器。[Visual Studio Code](https://code.visualstudio.com/docs/setup/raspberry-pi/)（通常称为 “VS Code”）也是一个流行的替代方案。

### 通过 .NET 访问 Build 扩展板

树莓派 Build 扩展板在乐高®术语中被称为 “Brick（积木）”，你可以使用 [Build 扩展板串行协议](https://pip.raspberrypi.com/documents/RP-008140-DS)从 .NET 直接与它通信。

你可以按照以下方式创建一个 `brick` 对象：

```csharp
Brick brick = new("/dev/serial0");
```

但你需要记住在代码末尾释放 `brick`。

```csharp
brick.Dispose();
```

>**警告**
>
> 如果你不调用 `brick.Dispose()`，你的程序将不会终止。

如果你想避免在结尾调用 `brick.Dispose`，那么请使用 `using` 语句创建 brick 对象：

```csharp
using Brick brick = new("/dev/serial0");
```

在这种情况下，当程序结束时，你的 brick 会被自动释放。

#### 显示 Build 扩展板信息

你可以读取各种软件版本、签名和输入电压：

```csharp
var info = brick.BuildHatInformation;
Console.WriteLine($"version: {info.Version}, firmware date: {info.FirmwareDate}, signature:");
Console.WriteLine($"{BitConverter.ToString(info.Signature)}");
Console.WriteLine($"Vin = {brick.InputVoltage.Volts} V");
```

>**注意**
>
> 输入电压仅在启动时读取一次，之后不再读取。

#### 获取传感器和电机详细信息

函数 `GetSensorType` 和 `GetSensor` 可让你获取已连接传感器的任何信息。

```csharp
SensorType sensor = brick.GetSensorType((SensorPort)i);
Console.Write($"Port: {i} {(Brick.IsMotor(sensor) ? "Sensor" : "Motor")} type: {sensor} Connected: ");
```

在这个例子中，你也可以使用 `IsMotor` 静态函数来检查连接的元素是传感器还是电机。

```csharp
if (Brick.IsActiveSensor(sensor))
{
    ActiveSensor activeSensor = brick.GetActiveSensor((SensorPort)i);
}
else
{
    var passive = (Sensor)brick.GetSensor((SensorPort)i);
    Console.WriteLine(passive.IsConnected);
}
```

`ActiveSensor` 具有一系列高级属性和函数，可用于了解传感器的各个元素。还可以通过它们调用 brick 的底层函数。这样你就能选择特定模式并实现更复杂的场景。虽然这些操作都能做到，但我们已经提供了电机类和传感器类，让你用起来更省心。

#### 事件

大多数传感器在其特殊属性上实现了事件。你可以直接订阅 `PropertyChanged` 和 `PropertyUpdated`。当值发生变化时会触发 changed 事件，而当属性成功更新时会触发 updated 事件。根据所使用的模式，一些属性可能会一直在后台更新，而另一些则偶尔更新。

如果你只关心颜色变化或电机位置变化，想把电机当作转速表使用，那么 `PropertyChanged` 正是你需要的！

```csharp
Console.WriteLine("Move motor on Port A to more than position 100 to stop this test.");
brick.WaitForSensorToConnect(SensorPort.PortA);
var active = (ActiveMotor)brick.GetMotor(SensorPort.PortA);
bool continueToRun = true;
active.PropertyChanged += MotorPropertyEvent;
while (continueToRun)
{
    Thread.Sleep(50);
}

active.PropertyChanged -= MotorPropertyEvent;
Console.WriteLine($"Current position: {active.Position}, eventing stopped.");

void MotorPropertyEvent(object? sender, PropertyChangedEventArgs e)
{
    Console.WriteLine($"Property changed: {e.PropertyName}");
    if (e.PropertyName == nameof(ActiveMotor.Position))
    {
        if (((ActiveMotor)brick.GetMotor(SensorPort.PortA)).Position > 100)
        {
            continueToRun = false;
        }
    }
}
```

#### 等待初始化

brick 可能需要很长时间才能完成初始化。已实现等待传感器连接的功能。

```csharp
brick.WaitForSensorToConnect(SensorPort.PortB);
```

如果你需要实现高级功能（例如在一段时间后警告用户并重试），还可以传入一个 `CancellationToken`。

### 使用 .NET 控制电机

电机有两种类型：**被动**电机和**主动**电机。主动电机可提供详细位置、绝对位置和速度，而被动电机只能通过速度来控制。

有一组通用的函数可用于控制电机的速度。其中有两个重要的函数：`SetPowerLimit` 和 `SetBias`：

```csharp
train.SetPowerLimit(1.0);
train.SetBias(0.2);
```

这两个函数只接受 0.0 到 1.0 之间的值。功率限制是一种方便的方法，可以按比例减小最大功率。

偏置值针对当前端口设置，会加到正的电机驱动值上，并从负的电机驱动值中减去。大多数直流电机需要一定的驱动量才能开始转动，偏置值可以用来补偿这一点。

创建电机时的默认值为：功率限制 0.7，偏置 0.3。

#### 被动电机

![火车电机](.gitbook/assets/train-motor.png)

[火车电机，来自 Bricklink 的图片](https://www.bricklink.com/v2/catalog/catalogitem.page?P=bb0896c01)

典型的被动电机是火车电机和较旧的 Powered Up 电机。`Speed` 属性可以设置和读取。由于这类电机没有测量自身速度的方法，该值既是目标速度，也是测得的速度。取值范围为 -100 到 +100。

还提供了用于控制的 `Start`、`Stop` 和 `SetSpeed` 函数。以下是一个使用示例：

```csharp
Console.WriteLine("This will run the motor for 20 seconds incrementing the PWM");
train.SetPowerLimit(1.0);
train.Start();
for (int i = 0; i < 100; i++)
{
    train.SetSpeed(i);
    Thread.Sleep(250);
}

Console.WriteLine("Stop the train for 2 seconds");
train.Stop();
Thread.Sleep(2000);
Console.WriteLine("Full speed backward for 2 seconds");
train.Start(-100);
Thread.Sleep(2000);
Console.WriteLine("Full speed forward for 2 seconds");
train.Start(100);
Thread.Sleep(2000);
Console.WriteLine("Stop the train");
train.Stop();
```

>**注意**
>
> 火车启动后，你可以调整速度，电机会相应调整。

#### 主动电机

![主动电机](.gitbook/assets/active-motor.png)

[主动电机，来自 Bricklink 的图片](https://www.bricklink.com/v2/catalog/catalogitem.page?P=bb0960c01)

主动电机具有 `Speed`、`AbsolutePosition`、`Position` 和 `TargetSpeed` 等特殊属性。即使电机停止运行，这些属性也会持续更新。

以下代码片段展示如何获取电机、启动它们并读取属性：

```csharp
brick.WaitForSensorToConnect(SensorPort.PortA);
brick.WaitForSensorToConnect(SensorPort.PortD);
var active = (ActiveMotor)brick.GetMotor(SensorPort.PortA);
var active2 = (ActiveMotor)brick.GetMotor(SensorPort.PortD);
active.Start(50);
active2.Start(50);
// 确保端口 A 和 D 上插有主动电机
while (!Console.KeyAvailable)
{
    Console.CursorTop = 1;
    Console.CursorLeft = 0;
    Console.WriteLine($"Absolute: {active.AbsolutePosition}     ");
    Console.WriteLine($"Position: {active.Position}     ");
    Console.WriteLine($"Speed: {active.Speed}     ");
    Console.WriteLine();
    Console.WriteLine($"Absolute: {active2.AbsolutePosition}     ");
    Console.WriteLine($"Position: {active2.Position}     ");
    Console.WriteLine($"Speed: {active2.Speed}     ");
}

active.Stop();
active2.Stop();
```

>**注意**
>
> 在需要时不要忘记启动和停止你的电机。

高级功能适用于主动电机。你可以让它转动指定秒数，也可以把它移动到特定位置或特定绝对位置。以下是一些示例：

```csharp
// 承上例，这会把电机转回初始位置：
active.TargetSpeed = 100;
active2.TargetSpeed = 100;
// 先让这台电机转动，会阻塞线程
active.MoveToPosition(0, true);
// 再让另一台电机转动，同样会阻塞线程
active2.MoveToPosition(0, true);
```

每个函数都允许你在操作执行期间阻塞或不阻塞线程。请注意，对于绝对位置和相对位置移动，存在几度的容差。

```csharp
brick.WaitForSensorToConnect(SensorPort.PortA);
var active = (ActiveMotor)brick.GetMotor(SensorPort.PortA);
active.TargetSpeed = 70;
Console.WriteLine("Moving motor to position 0");
active.MoveToPosition(0, true);
Console.WriteLine("Moving motor to position 3600 (10 turns)");
active.MoveToPosition(3600, true);
Console.WriteLine("Moving motor to position -3600 (so 20 turns the other way");
active.MoveToPosition(-3600, true);
Console.WriteLine("Moving motor to absolute position 0, should rotate by 90°");
active.MoveToAbsolutePosition(0, PositionWay.Shortest, true);
Console.WriteLine("Moving motor to position 90");
active.MoveToAbsolutePosition(90, PositionWay.Shortest, true);
Console.WriteLine("Moving motor to position 179");
active.MoveToAbsolutePosition(179, PositionWay.Shortest, true);
Console.WriteLine("Moving motor to position -180");
active.MoveToAbsolutePosition(-180, PositionWay.Shortest, true);
active.Float();
```

你可以将电机置于浮动（float）状态，即不再对它施加任何约束。当你把电机用作转速表时可以使用这种模式：移动电机并读取位置。如果电机仍受约束，你可能无法移动它。

### 使用 .NET 读取传感器

与电机一样，传感器也分为主动和被动两种。较新的传感器大多是主动的。被动传感器包括灯光和简单的按钮。主动传感器包括距离传感器、颜色传感器，以及小型的 3×3 像素显示屏。

#### 按钮/触摸被动传感器

按钮/触摸被动传感器具有一个特殊属性 `IsPressed`。当按钮被按下时，该属性设置为 true。以下是一个带事件的完整示例：

```csharp
brick.WaitForSensorToConnect(SensorPort.PortA);
var button = (ButtonSensor)brick.GetSensor(SensorPort.PortA);
bool continueToRun = true;
button.PropertyChanged += ButtonPropertyEvent;
while (continueToRun)
{
    // 你可以在这里做许多其他事情
    Thread.Sleep(50);
}

button.PropertyChanged -= ButtonPropertyEvent;
Console.WriteLine($"Button has been pressed, we're stopping the program.");
brick.Dispose();

void ButtonPropertyEvent(object? sender, PropertyChangedEventArgs e)
{
    Console.WriteLine($"Property changed: {e.PropertyName}");
    if (e.PropertyName == nameof(ButtonSensor.IsPressed))
    {
        continueToRun = false;
    }
}
```

#### 被动灯光

![被动灯光](.gitbook/assets/passive-light.png)

[被动灯光，来自 Bricklink 的图片](https://www.bricklink.com/v2/catalog/catalogitem.page?P=22168c01)

被动灯光是火车灯。你可以打开它们，并控制它们的亮度。

```csharp
brick.WaitForSensorToConnect(SensorPort.PortA);
var light = (PassiveLight)brick.GetSensor(SensorPort.PortA);
// 亮度 50%
light.On(50);
Thread.Sleep(2000);
// 亮度 70%
light.Brightness = 70;
Thread.Sleep(2000);
// 关闭灯光
light.Off()
```

#### 主动传感器

主动传感器类是一个通用类，所有主动传感器（包括主动电机）都继承自它。该类包含一组属性，涉及与 Build 扩展板的连接方式、模式、详细的组合（Combi）模式、硬件和软件版本，以及一个名为 `ValueAsString` 的特殊属性。字符串值包含以字符串集合形式表示的最后一次测量。测量到达时形如 `P0C0: +23 -42 0`，枚举将包含 `P0C0:`、`+23`、`-42` 和 `0`。这样设计是为了让你在使用高级模式并自行管理组合模式和命令时，也能获取测量值。

所有主动传感器都可以运行特定的测量模式或组合模式。你可以通过高级模式，使用 `SelectModeAndRead` 和 `SelectCombiModesAndRead` 函数设置你想要持续使用的特定模式。需要注意，更改模式或设置新模式会停止之前的模式。

可以组合进组合模式的模式列在 `CombiModes` 属性中。当你设置其中某个模式时，传感器的所有属性都会自动更新。

#### WeDo 倾斜传感器

![WeDo 倾斜传感器](.gitbook/assets/wedo-tilt.png)

[WeDo 倾斜传感器，来自 Bricklink 的图片](https://www.bricklink.com/v2/catalog/catalogitem.page?P=20841)

WeDo 倾斜传感器有一个特殊的 `Tilt` 属性。该类型是一个点（point），其中 X 是 X 轴倾斜值，Y 是 Y 轴倾斜值。数值范围从 -45 到 +45，被限制在这些值内，单位为度。

你可以使用 `ContinuousMeasurement` 属性为该传感器设置连续测量。

```csharp
brick.WaitForSensorToConnect(SensorPort.PortA);
var tilt = (WeDoTiltSensor)brick.GetSensor(SensorPort.PortA);
tilt.ContinuousMeasurement = true;
Point tiltValue;
while(!console.KeyAvailable)
{
    tiltValue = tilt.Tilt;
    console.WriteLine($"Tilt X: {tiltValue.X}, Tilt Y: {tiltValue.Y}");
    Thread.Sleep(200);
}
```

#### WeDo 距离传感器

![WeDo 距离传感器](.gitbook/assets/wedo-distance.png)

[WeDo 距离传感器，来自 Bricklink 的图片](https://www.bricklink.com/v2/catalog/catalogitem.page?P=20844)

WeDo 距离传感器通过 `Distance` 属性提供以毫米为单位的距离。

```csharp
brick.WaitForSensorToConnect(SensorPort.PortA);
var distance = (WeDoDistanceSensor)brick.GetSensor(SensorPort.PortA);
distance.ContinuousMeasurement = true;
while(!console.KeyAvailable)
{
    console.WriteLine($"Distance: {distance.Distance} mm");
    Thread.Sleep(200);
}
```

#### SPIKE Prime 力传感器

![SPIKE 力传感器](.gitbook/assets/spike-force.png)

[SPIKE 力传感器，来自 Bricklink 的图片](https://www.bricklink.com/v2/catalog/catalogitem.page?P=37312c01)

该力传感器测量施加在它上面的压力，以及它是否被按下。这两个值可分别通过 `Force` 和 `IsPressed` 属性读取。

```csharp
brick.WaitForSensorToConnect(SensorPort.PortA);
var force = (ForceSensor)brick.GetSensor(SensorPort.PortA);
force.ContinuousMeasurement = true;
while(!force.IsPressed)
{
    console.WriteLine($"Force: {force.Force} N");
    Thread.Sleep(200);
}
```

#### SPIKE Essential 3×3 彩色灯光矩阵

![SPIKE Essential 3×3 彩色灯光矩阵](.gitbook/assets/3x3matrix.png)

[SPIKE 3×3 矩阵，来自 Bricklink 的图片](https://www.bricklink.com/v2/catalog/catalogitem.page?P=47592c01)

这是一个小型 3×3 显示屏，带有 9 个可单独控制的 LED。该类公开了控制屏幕的函数。以下是一个使用示例：

```csharp
brick.WaitForSensorToConnect(SensorPort.PortA);
var matrix = (ColorLightMatrix)brick.GetSensor(SensorPort.PortA);
for(byte i = 0; i < 10; i++)
{
    // 像进度条一样逐个点亮每个 LED
    matrix.DisplayProgressBar(i);
    Thread.Sleep(1000);
}

for(byte i = 0; i < 11; i++)
{
    // 用同一种颜色显示矩阵，并依次遍历所有颜色
    matrix.DisplayColor((LedColor)i);
    Thread.Sleep(1000);
}

Span<byte> brg = stackalloc byte[9] { 1, 2, 3, 4, 5, 6, 7, 8, 9 };
Span<LedColor> col = stackalloc LedColor[9] { LedColor.White, LedColor.White, LedColor.White,
  LedColor.White, LedColor.White, LedColor.White, LedColor.White, LedColor.White, LedColor.White };
// 灰度层次
matrix.DisplayColorPerPixel(brg, col);
```

#### SPIKE Prime 颜色传感器与颜色和距离传感器

SPIKE 颜色传感器：

![SPIKE 颜色传感器](.gitbook/assets/spike-color.png)

[SPIKE 颜色传感器，来自 Bricklink 的图片](https://www.bricklink.com/v2/catalog/catalogitem.page?P=37308c01)

颜色和距离传感器：

![颜色和距离传感器](.gitbook/assets/color-distance.png)

[颜色距离传感器，来自 Bricklink 的图片](https://www.bricklink.com/v2/catalog/catalogitem.page?P=bb0891c01)

这些颜色传感器具有多种属性和函数。你可以获取 `Color`、`ReflectedLight` 和 `AmbiantLight`。

除此之外，颜色和距离传感器还可以测量 `Distance`，并带有一个物体计数器 `Counter`。它会自动计算进出量程的物体数量，从而可以统计经过传感器前方的物体。距离限制在 0 到 10 厘米之间。

```csharp
brick.WaitForSensorToConnect(SensorPort.PortC);

var colorSensor = (ColorAndDistanceSensor)brick.GetActiveSensor(SensorPort.PortC);
while (!Console.KeyAvailable)
{
    var colorRead = colorSensor.GetColor();
    Console.WriteLine($"Color:     {colorRead}");
    var reflected = colorSensor.GetReflectedLight();
    Console.WriteLine($"Reflected: {reflected}");
    var ambiant = colorSensor.GetAmbiantLight();
    Console.WriteLine($"Ambiant:   {ambiant}");
    var distance = colorSensor.GetDistance();
    Console.WriteLine($"Distance: {distance}");
    var counter = colorSensor.GetCounter();
    Console.WriteLine($"Counter:  {counter}");
    Thread.Sleep(200);
}
```

>**注意**
>
> 为了获得更好的测量结果，不建议非常频繁地更改测量模式，否则颜色积分可能无法正确完成。这个示例涵盖了该传感器能做的全部事情。此外，该类没有实现连续测量模式。你可以通过高级模式，使用 `SelectModeAndRead` 函数设置你想要持续使用的特定模式。需要注意，更改模式或设置新模式会停止之前的模式。

#### SPIKE Prime 超声波距离传感器

![SPIKE 超声波距离传感器](.gitbook/assets/spike-distance.png)

[超声波距离传感器，来自 Bricklink 的图片](https://www.bricklink.com/v2/catalog/catalogitem.page?P=37316c01)

这是一个距离传感器，它实现了 `Distance` 属性，可提供以毫米为单位的距离。它还提供 `ContinuousMeasurement` 模式。

```csharp
brick.WaitForSensorToConnect(SensorPort.PortA);
var distance = (UltrasonicDistanceSensor)brick.GetSensor(SensorPort.PortA);
distance.ContinuousMeasurement = true;
while(!console.KeyAvailable)
{
    console.WriteLine($"Distance: {distance.Distance} mm");
    Thread.Sleep(200);
}
```

## 更多资源

你可以下载以下文档：

* [树莓派 Build HAT 串行协议](https://pip.raspberrypi.com/documents/RP-008140-DS)
* [树莓派 Build HAT Python 库](https://pip.raspberrypi.com/documents/RP-008139-DS)

Python 库文档的完整详细信息也可以在 [ReadTheDocs](https://buildhat.readthedocs.io/) 上找到。你可以在 [.NET IoT](https://github.com/dotnet/iot/tree/main/src/devices/BuildHat) GitHub 存储库中找到有关 .NET 库的更多信息。

你还可以跟着树莓派基金会的项目一起做：

* [乐高®游戏控制器](https://projects.raspberrypi.org/en/projects/lego-game-controller)
* [乐高®机器人车](https://projects.raspberrypi.org/en/projects/lego-robot-car)
* [乐高®绘图仪](https://projects.raspberrypi.org/en/projects/lego-plotter)
* [乐高®机器人脸](https://projects.raspberrypi.org/en/projects/lego-robot-face)
* [乐高®数据仪表板](https://projects.raspberrypi.org/en/projects/lego-data-dash)

## 设备兼容性

Build 扩展板库支持 SPIKE™ 系列产品中包含的所有乐高®机械组（LEGO® Technic™）设备，以及来自乐高® Mindstorms 机器人发明家（Robot Inventor）套件和其他使用 PoweredUp 连接器的设备。

>**重要**
>
> 包含 Maker Plate 的 SPIKE™ Prime 扩展套装的产品代码为 45681。最初的扩展套装为 45680，不包含 Maker Plate。

| 说明 | 颜色 | 乐高物品编号 | 在固件中支持 | 在 Python 中支持 | 替代编号 | BrickLink | 可用于 | 套装编号 | 类 | 类型 | 设备标识 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 大型角度电机 | 白色/青色 | 45602 | 是 | 是 | 45602 | [链接](https://www.bricklink.com/v2/catalog/catalogitem.page?P=54675c01) | SPIKE Prime 套装、SPIKE Prime 扩展套装 | 45678, 45680 | Motor | 主动 | 31 |
| 中型角度电机 | 白色/青色 | 45603 | 是 | 是 | 45603 | [链接](https://www.bricklink.com/v2/catalog/catalogitem.page?P=54696c01) | SPIKE Prime 套装 | 45678 | Motor | 主动 | 30 |
| 中型角度电机 | 白色/灰色 | 6299646, 6359216, 6386708 | 是 | 是 | 436655 | [链接](https://www.bricklink.com/v2/catalog/catalogitem.page?P=54696c01) | Mindstorms 机器人发明家 | 51515 | Motor | 主动 | 4B |
| 小型角度电机 | 白色/青色 | 45607, 6296520 | 是 | 是 |  | [链接](https://www.bricklink.com/v2/catalog/catalogitem.page?P=68488c01) | SPIKE Essential 套装 |  | Motor | 主动 | 41 |
| 光/颜色传感器 | 白色/黑色 | 6217705 | 是 | 是 |  | [链接](https://www.bricklink.com/v2/catalog/catalogitem.page?P=37308c01) | SPIKE Prime 套装、SPIKE Prime 扩展套装、Mindstorms 机器人发明家、SPIKE Essential | 45678, 45680, 51515 | ColorSensor | 主动 | 3D |
| 距离传感器 | 白色/黑色 | 6302968 | 是 | 是 |  | [链接](https://www.bricklink.com/v2/catalog/catalogitem.page?P=37316c01) | SPIKE Prime 套装、Mindstorms 机器人发明家 | 45678, 51515 | DistanceSensor | 主动 | 3E |
| 系统中型电机 | 白色/灰色 | 45303, 6138854, 6290182, 6127110 | 是 | 是 |  | [链接](https://www.bricklink.com/v2/catalog/catalogitem.page?P=21980) | WeDo 2.0、乐高 Ideas 钢琴、App 控制的蝙蝠车 | 76112 |  | 被动 | 1 |
| 力传感器 | 白色/黑色 | 6254354 | 是 | 是 | 45606 | [链接](https://www.bricklink.com/v2/catalog/catalogitem.page?P=37312c01) | SPIKE Prime 套装 | 45678 | ForceSensor | 主动 | 3F |
| 3×3 LED | 白色/青色 | 45608, 6297023 | 是 | 是 |  | [链接](https://www.bricklink.com/v2/catalog/catalogitem.page?P=47592c01) | SPIKE Essential |  | Matrix | 主动 | 40 |
| 系统火车电机 | 黑色 | 88011 | 是 | 是 | 28740, 88011-1 | [链接](https://www.bricklink.com/v2/catalog/catalogitem.page?P=bb0896c01) | 货运火车、迪士尼火车和车站、客运列车 |  |  | 被动 | 2 |
| PoweredUp LED 灯 | 黑色 | 88005 | 是 |  |  | [链接](https://www.bricklink.com/v2/catalog/catalogitem.page?P=22168c01) |  |  |  | 被动 | 8 |
| 中型线性电机 | 白色/灰色 | 88008 | 是 | 是 | 26913, 88008-1 | [链接](https://www.bricklink.com/v2/catalog/catalogitem.page?P=bb0893c01) | Boost、Droid Commander |  | Motor | 主动 | 26 |
| Technic 大型电机 | 灰色/灰色 | 88013 | 是 | 是 | 22169 | [链接](https://www.bricklink.com/v2/catalog/catalogitem.page?P=bb0959c01) |  |  |  | 主动 | 2E |
| Technic XL 电机 | 灰色/灰色 | 88014 | 是 | 是 | 22172, 88014 | [链接](https://www.bricklink.com/v2/catalog/catalogitem.page?P=bb0960c01) |  |  |  | 主动 | 2F |
| 颜色 + 距离传感器 | 白色/灰色 | 88007 | 部分 | ？ | 26912 | [链接](https://www.bricklink.com/v2/catalog/catalogitem.page?P=bb0891c01) |  |  |  | 主动 | 25 |
| WeDo 2.0 运动传感器 | 白色/灰色 | 45304, 6138855 |  |  | 5003423-1 | [链接](https://www.bricklink.com/v2/catalog/catalogitem.page?P=43718) |  |  |  | 主动 | 35 |
| WeDo 2.0 倾斜传感器 | 白色/灰色 | 45305, 6138856 |  |  | 5003423-1 | [链接](https://www.bricklink.com/v2/catalog/catalogitem.page?P=14618) |  |  |  | 主动 | 34 |

## 机械图纸

树莓派 Build 扩展板的机械图纸。

![Build 扩展板机械图纸](.gitbook/assets/mech-build-hat.png)
