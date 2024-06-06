# Build 扩展板（Build HAT）

## Build 扩展板（Build HAT）简介

树莓派 Build 扩展板是一个附加板，可连接到树莓派的 40 引脚 GPIO 标头，与 LEGO® Education 合作设计，可轻松使用树莓派计算机控制 LEGO® Technic™ 电机和传感器。

![build hat](https://www.raspberrypi.com/documentation/accessories/images/build-hat.jpg)

>**注意**
>
>可在设备兼容性部分找到受支持设备的完整列表。 

它为 LEGO® Technic™ 电机和 SPIKE™ 组合中的传感器提供四个连接器。可用的传感器包括距离传感器、颜色传感器和多功能力传感器。角度电机有各种尺寸，并包括集成编码器，可查询其位置。

Build 扩展板适用于所有带有 40 针 GPIO 引脚的树莓派计算机，包括通过连接排线或其他扩展设备的树莓派 400。连接的 LEGO® Technic™ 设备可以轻松在 Python 中进行控制，同时还可以连接标准的树莓派配件，如摄像头模块。

树莓派 Build 扩展板的电源适配器（PSU）单独出售，旨在为 Build 扩展板、树莓派计算机以及所有连接的 LEGO® Technic™ 设备供电。

![psu](https://www.raspberrypi.com/documentation/accessories/images/psu.jpg)

从 LEGO® Education 经销商单独提供的 SPIKE™ Prime 套装 45678 和 SPIKE™ Prime 扩展套装 45681 中，包含一组由 Build 扩展板支持的实用元件。

受支持设备的完整列表

>**注意**
>
>该 HAT 与所有 40 针 GPIO 树莓派板块兼容，包括树莓派 4 和树莓派 Zero。通过添加排线电缆或其他延伸设备，也可与树莓派 400 一起使用。 

* 控制 SPIKE™ Portfolio 中包含的 4 个 LEGO® Technic™ 电机和传感器。
* 控制您的 LEGO® Technic™ 设备的易于使用的 Python 库
* 适用于带有 40 针 GPIO 引脚的任何树莓派计算机
* Onboard RP2040 微控制器管理 LEGO® Technic™设备的低级控制
* 单独提供外部 8V PSU 以为 Build 扩展板和树莓派供电

>**注意**
>
>由于不支持通过 GPIO 引脚供电，Build 扩展板不能为树莓派 400 供电 。

## 准备您的 Build 扩展板

>**注意**
>
>在开始使用您的树莓派 Build 扩展板之前，您应该设置您的树莓派，使用 Raspberry Pi Imager 安装最新版本的操作系统。

将 9mm 的间隔柱连接到板的底部。将树莓派 Build 扩展板安装到您的树莓派上。确保将其正确放置。与其他扩展板不同，所有组件都在底部，为顶部的面包板或乐高® 元件留出空间。

![fitting build hat](https://www.raspberrypi.com/documentation/accessories/images/fitting-build-hat.gif)

### 访问 GPIO 引脚

如果您想使用树莓派的 GPIO 引脚，您可以添加一个可选的高头并使用 15 毫米间隔柱。

![tall headers](https://www.raspberrypi.com/documentation/accessories/images/tall-headers.png)

下面的引脚是 Build 扩展板本身使用的，您不应该连接其他东西到这些引脚上。

| GPIO    | 使用      | 状态   |
| --------- | ----------- | -------- |
| GPIO0/1 | ID 识别器 |        |
| GPIO4   | 重置      |        |
| GPIO14  | 发送      |        |
| GPIO15  | 接收      |        |
| GPIO16  | RTS       | 未使用 |
| GPIO17  | CTS       | 未使用 |

### 设置您的树莓派

树莓派启动后，通过单击 Raspberry 菜单按钮，然后选择“首选项”，再选择“Raspberry Pi 配置”来打开 Raspberry Pi 配置工具。

单击“接口”选项卡，并按照下面所示调整串行设置：

![setting up](https://www.raspberrypi.com/documentation/accessories/images/setting-up.png)

#### 使用您的无头树莓派

如果您正在无头运行您的树莓派并使用 raspi-config ，请从第一个菜单中选择“接口选项”。

![raspi config 1](https://www.raspberrypi.com/documentation/accessories/images/raspi-config-1.png)

然后选择“P6 串行端口”。

![raspi config 2](https://www.raspberrypi.com/documentation/accessories/images/raspi-config-2.png)

禁用串行控制台：

![raspi config 3](https://www.raspberrypi.com/documentation/accessories/images/raspi-config-3.png)

并启用串口。

![raspi config 4](https://www.raspberrypi.com/documentation/accessories/images/raspi-config-4.png)

最终设置应该看起来像这样。

![raspi config 5](https://www.raspberrypi.com/documentation/accessories/images/raspi-config-5.png)

如果您已经进行了任何更改，此时需要重新启动。

### 为 Build 扩展板供电

连接外部电源 — 推荐使用官方树莓派 Build 扩展板电源 — 但是凡是可靠的 +8V±10% 电源，能够通过 DC 5521 中心正枪形连接器（5.5mm × 2.1mm × 11mm）提供 48W 的电源，都可以为 Build 扩展板供电。除非您正在使用树莓派 400，否则无需额外再将树莓派接入电源。

>**注意**
>
>旧版 HAT 无法为树莓派 400 供电，因为它不支持通过 GPIO 引脚取电。 

![powering build hat](https://www.raspberrypi.com/documentation/accessories/images/powering-build-hat.gif)

>**注意**
>
>乐高® Technic™ 电机非常强大；因此，为了驱动它们，您需要外部的 8V 电源。如果您想从电机编码器和 SPIKE™ 力传感器读取数据，您可以通过您树莓派的 USB 电源接口以平常的方式为您的树莓派和 Build 扩展板供电。与电机一样，SPIKE™颜色和距离传感器需要外部电源供应。 

您可以选择使用 Python 或 .NET 与 Build 扩展板一起使用。

## 使用 Python 操作 Build 扩展板

### 安装 Python 库

安装 Build HAT Python 库。打开终端，然后输入，

```
$ sudo apt install python3-build-hat
```

有关 Build HAT Python 库的更多信息，请参阅 ReadTheDocs。

### 使用 Python 控制电机

有许多电机可以与 Build 扩展板一起使用

#### 连接电机

将电机连接到 Build 扩展板上的接口 A。 LPF2 连接器需要正确插入。 如果连接器无法轻松滑入，请旋转 180 度后重试。

![connect motor](https://www.raspberrypi.com/documentation/accessories/images/connect-motor.gif)

#### 使用电机

启动 Thonny IDE。添加以下代码：

```
from buildhat import Motor

motor_a = Motor('A')

motor_a.run_for_seconds(5)
```

通过单击播放/运行按钮来运行程序。如果这是自树莓派启动以来首次运行 Build 扩展板程序，那么在固件复制到板上时会有几秒钟的暂停。您应该看到红色 LED 熄灭，绿色 LED 点亮。以后再执行 Python 程序就不会有这种暂停了。

![blinking light](https://www.raspberrypi.com/documentation/accessories/images/blinking-light.gif)

您的电机应该顺时针转动 5 秒钟。

![turning motor](https://www.raspberrypi.com/documentation/accessories/images/turning-motor.gif)

更改代码的最后一行并重新运行。

```
motor_a.run_for_seconds(5, speed=50)
```

电机现在应该转得更快。再做一个改变：

```
motor_a.run_for_seconds(5, speed=-50)
```

电机应该向相反方向（逆时针）转动

点击 Thonny 中的加号按钮创建一个新程序。添加以下代码：

```
from buildhat import Motor

motor_a = Motor('A')

while True:
    print("Position: ", motor_a.get_aposition())
```

运行程序。拿起电机并转动轴。您应该看到在 Thonny REPL 中打印的数字在变化。

### 使用 Python 中的传感器

有许多传感器可与 Build 扩展板一起使用。

#### 使用传感器

将彩色传感器连接到 Build 扩展板的 B 接口，将力传感器连接到 C 端口。

>**注意**
>
>如果您不打算驱动电机，则无需外部电源，可以使用标准 USB 电源为您的树莓派供电。 

创建另一个新程序：

```
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

运行它，并将一个彩色物体（LEGO®元素最理想）放在颜色传感器前，然后按下力传感器压杆。传感器的 LED 应该亮起，并且最接近的颜色名称应该显示在 thonny REPL 中。

## 使用来自 .NET 的 Build 扩展板

### 安装 .NET 框架

在树莓派上无法用 APT 安装从微软获取的 .NET 框架。但是，您可以参照微软的官方说明来安装 .NET 框架。这还有一个简化的第三方途径可以将 .NET 工具链安装到您的树莓派上。

>**警告**
>
>安装脚本以 APT 运行。您应该先阅读它，并确保您理解它在做什么。如果您有任何疑问，应该按照官方说明手动操作。

```
$ wget -O - https://raw.githubusercontent.com/pjgpetecodes/dotnet5pi/master/install.sh | sudo bash
```

安装 .NET 框架后，您可以创建您的项目：

```
$ dotnet new console --name buildhat
```

这将在 buildhat 子目录中创建一个默认程序，我们需要在该目录中才能继续：

```
$ cd buildhat
```

您现在需要安装以下 NuGet 软件包：

```
$ dotnet add package System.Device.Gpio --version 2.1.0
$ dotnet add package Iot.Device.Bindings --version 2.1.0
```

### 运行 C# 代码

您可以使用 dotnet run 命令运行程序。现在让我们试一下，确保一切正常。它应该打印出 "Hello World!"

```
$ dotnet run
Hello World!
```

(在接下来的说明中，当指示“运行程序”时，您只需重新运行 dotnet run )

### 编辑 C# 代码

在下面的说明中，您将编辑生成的 C# 程序文件 buildhat/Program.cs ，该文件是在运行上述命令时生成的。

任何文本编辑器都可以用来编辑 C# 代码，包括预装的 Geany IDE/文本编辑器。Visual Studio Code（通常称为 "VS Code"）也是一个流行的替代方案。

### 使用 .NET 从 Build 扩展板进行操作

树莓派 Build 扩展板在 LEGO® 术语中被称为"Brick"，您可以使用 Build 扩展板串行协议直接与之通信

您可以按照以下方式创建一个 brick 对象

```
Brick brick = new("/dev/serial0");
```

但是您需要记住在代码结尾处处理 brick 。

```
brick.Dispose();
```

>**警告**
>
>如果您不调用 `brick.Dispose()` ，您的程序将不会停止。 

如果您想避免在最后调用 brick.Dispose ，那么请使用 using 语句创建您的模块：

```
using Brick brick = new("/dev/serial0");
```

在这种情况下，当程序结束时，您的砖将被自动处理。

#### 显示信息

您可以收集各种软件版本、签名和输入电压：

```
var info = brick.BuildHatInformation;
Console.WriteLine($"version: {info.Version}, firmware date: {info.FirmwareDate}, signature:");
Console.WriteLine($"{BitConverter.ToString(info.Signature)}");
Console.WriteLine($"Vin = {brick.InputVoltage.Volts} V");
```

>**注意**
>
>输入电压仅在启动时读取一次，之后就不再读取。 

#### 获取传感器和电机详细信息

函数 GetSensorType ， GetSensor 将允许您检索连接传感器上的任何信息。

```
SensorType sensor = brick.GetSensorType((SensorPort)i);
Console.Write($"Port: {i} {(Brick.IsMotor(sensor) ? "Sensor" : "Motor")} type: {sensor} Connected: ");
```

在这个例子中，您也可以使用 IsMotor 静态函数来检查连接的元素是传感器还是电机。

```
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

ActiveSensor 具有一系列高级属性和功能，可以帮助理解传感器的每个元素。还可以从砖块中调用原始功能。这将允许您选择特定模式并执行高级场景。虽然这是可能的，但电机和传感器类已经被创建，以使您的生活更轻松。

#### 事件

大多数传感器在其特殊属性上实现事件。您可以简单地订阅 PropertyChanged 和 PropertyUpdated 。当值发生变化时，将触发更改的事件，而在成功更新属性时将触发更新的事件。根据使用的模式，一些属性可能会一直在后台更新，而另一些则偶尔更新。

当颜色变化或电机位置变化时，您可能只对此感兴趣，将其用作转速表。在这种情况下， PropertyChanged 就是您需要的！

```
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

砖块在初始化之前可能需要很长时间。已实现等待连接传感器的功能。

```
brick.WaitForSensorToConnect(SensorPort.PortB);
```

如果要实现诸如在一段时间后警告用户并重试等高级功能，也需要一段 CancellationToken 时间。

### 使用 .NET 中的电机

有两种类型的电机，被动电机和主动电机。主动电机将提供详细位置、绝对位置和速度，而被动电机只能通过速度来控制。

有一组常见的函数可用于控制电机的速度。有两个重要的函数： SetPowerLimit 和 SetBias ：

```
train.SetPowerLimit(1.0);
train.SetBias(0.2);
```

只接受从 0.0 到 1.0 的值。功率限制是一种方便的方法，可以按比例减少最大功率。

添加到正电机驱动值并从负电机驱动值中减去的当前端口的偏置值集。这可以用来补偿大多数直流电机在完全转动之前需要一定量驱动的事实。

当创建电机时，默认值为功率限制为 0.7，偏置为 0.3。

#### 被动电机

![Train motor](https://www.raspberrypi.com/documentation/accessories/images/train-motor.png)

训练电机，来自 Bricklink 的图像

典型的被动电机是火车和较旧的 Powered Up 电机。 Speed 属性可以设置和读取。它既是目标，也是同时测量速度的传感器，因为这些传感器没有测量它们的方法。该值范围为 -100 到 +100。

控制 Start 、 Stop 和 SetSpeed 的功能也可用。以下是如何使用它的示例：

```
Console.WriteLine("This will run the motor for 20 secondes incrementing the PWM");
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
>在火车启动后，您可以调整速度，电机会相应调整。 

#### 活动电机

![Active motor](https://www.raspberrypi.com/documentation/accessories/images/active-motor.png)

活动电机，来自 Bricklink 的图片

活动马达具有 Speed ， AbsolutePosition ， Position 和 TargetSpeed 作为特殊属性。即使马达停止运行，它们也会持续读取。

代码片段显示了如何获取马达，启动它们并读取属性：

```
brick.WaitForSensorToConnect(SensorPort.PortA);
brick.WaitForSensorToConnect(SensorPort.PortD);
var active = (ActiveMotor)brick.GetMotor(SensorPort.PortA);
var active2 = (ActiveMotor)brick.GetMotor(SensorPort.PortD);
active.Start(50);
active2.Start(50);
// Make sure you have an active motor plug in the port A and D
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
>在需要时不要忘记启停您的马达。

高级功能适用于活动电机。您可以请求移动几秒钟，到特定位置，到特定绝对位置。以下是一些示例：

```
// From the previous example, this will turn the motors back to their initial position:
active.TargetSpeed = 100;
active2.TargetSpeed = 100;
// First this motor and will block the thread
active.MoveToPosition(0, true);
// Then this one and will also block the thread
active2.MoveToPosition(0, true);
```

每个功能都允许您阻塞或不阻塞线程，直到操作完成。请注意，对于绝对位置和相对位置移动，存在几度的容差。

```
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

您可以将电机放置在浮动位置，意味着它不再受任何约束。这是一种模式，您可以在将电机用作转速计时使用，移动它并读取位置。如果电机仍受约束，您可能无法移动它。

### 使用 .NET 中的传感器

就像对于电机一样，您有主动和被动传感器。最近的传感器是主动的。被动的是灯光和简单按钮。主动传感器包括距离或颜色传感器，以及小型的 3x3 像素显示屏。

#### 按钮/触摸被动传感器

按钮/触摸被动传感器具有一个特定属性 IsPressed 。当按钮被按下时，该属性设置为 true。这里是一个带有事件的完整示例：

```
brick.WaitForSensorToConnect(SensorPort.PortA);
var button = (ButtonSensor)brick.GetSensor(SensorPort.PortA);
bool continueToRun = true;
button.PropertyChanged += ButtonPropertyEvent;
while (continueToRun)
{
    // You can do many other things here
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

#### 被动光

![Passive light](https://www.raspberrypi.com/documentation/accessories/images/passive-light.png)

被动光，来自 Bricklink 的图像

被动光是火车灯。它们可以打开，您可以控制它们的亮度。

```
brick.WaitForSensorToConnect(SensorPort.PortA);
var light = (PassiveLight)brick.GetSensor(SensorPort.PortA);
// Brightness 50%
light.On(50);
Thread.Sleep(2000);
// 70% Brightness
light.Brightness = 70;
Thread.Sleep(2000);
// Switch light off
light.Off()
```

#### 主动传感器

主动传感器类是一个通用类，所有主动传感器都继承自它，包括主动马达。它们包含一组关于它们如何连接到 Build 扩展板、模式、详细组合模式、硬件、软件版本以及一个名为 ValueAsString 的特定属性。字符串值包含最后一次测量的字符串集合。测量到达时，枚举将包含 `P0C0: ， +23 ， -42` 和 0 。这样做是为了如果您正在使用高级模式并自行管理组合模式和命令，您将能够获得测量值。

所有活动传感器都可以运行特定的测量模式或组合模式。您可以通过高级模式使用 SelectModeAndRead 和 SelectCombiModesAndRead 功能设置一个您想要持续拥有的特定模式。重要的是要理解更改模式或设置新模式将停止先前的模式。

可以在组合模式中组合的模式列在 CombiModes 属性中。当您设置其中一个模式时，传感器的所有属性将自动更新。

#### WeDo Tilt Sensor

![WeDo Tilt sensor](https://www.raspberrypi.com/documentation/accessories/images/wedo-tilt.png)

WeDo Tilt sensor，来自 Bricklink 的图像

WeDo Tilt Sensor 具有特殊 Tilt 属性。类型是一个点，其中 X 是 X 倾斜，Y 是 Y 倾斜。数值范围从 -45 到 +45，它们被限制在这些值并表示度数。

您可以使用 ContinuousMeasurement 属性为该传感器设置连续测量。

```
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

![WeDo Distance sensor](https://www.raspberrypi.com/documentation/accessories/images/wedo-distance.png)

WeDo 距离传感器，来自 Bricklink 的图像

WeDo 距离传感器通过 Distance 属性以毫米为单位提供距离

```
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

![spike force sensor](https://www.raspberrypi.com/documentation/accessories/images/spike-force.png)

Spike 力传感器，来自 Bricklink 的图片

这个力传感器测量施加在其上的压力，以及是否被按下。这两个属性可以通过 Force 和 IsPressed 属性访问。

```
brick.WaitForSensorToConnect(SensorPort.PortA);
var force = (ForceSensor)brick.GetSensor(SensorPort.PortA);
force.ContinuousMeasurement = true;
while(!force.IsPressed)
{
    console.WriteLine($"Force: {force.Force} N");
    Thread.Sleep(200);
}
```

#### SPIKE Essential 3x3 Color Light Matrix

![spike 3x3 matrix](https://www.raspberrypi.com/documentation/accessories/images/3x3matrix.png)

spike 3x3 matrix, [Image from Bricklink](https://www.bricklink.com/v2/catalog/catalogitem.page?P=45608c01&name=Electric,%203%20x%203%20Color%20Light%20Matrix%20-%20SPIKE%20Prime&category=%5BElectric%5D#T=C)

这是一个带有 9 个不同 LED 的小型 3x3 显示屏，可以单独控制。该类公开了控制屏幕的功能。以下是一个使用它们的示例：

```
brick.WaitForSensorToConnect(SensorPort.PortA);
var matrix = (ColorLightMatrix)brick.GetSensor(SensorPort.PortA);
for(byte i = 0; i < 10; i++)
{
    // Will light every led one after the other like a progress bar
    matrix.DisplayProgressBar(i);
    Thread.Sleep(1000);
}

for(byte i = 0; i < 11; i++)
{
    // Will display the matrix with the same color and go through all of them
    matrix.DisplayColor((LedColor)i);
    Thread.Sleep(1000);
}

Span<byte> brg = stackalloc byte[9] { 1, 2, 3, 4, 5, 6, 7, 8, 9 };
Span<LedColor> col = stackalloc LedColor[9] { LedColor.White, LedColor.White, LedColor.White,
  LedColor.White, LedColor.White, LedColor.White, LedColor.White, LedColor.White, LedColor.White };
// Shades of grey
matrix.DisplayColorPerPixel(brg, col);
```

#### SPIKE Prime 颜色传感器和颜色和距离传感器

 SPIKE 颜色传感器：

![spike color sensor](https://www.raspberrypi.com/documentation/accessories/images/spike-color.png)

SPIKE 颜色传感器，来自 Bricklink 的图像

颜色和距离传感器：

![Color distance sensor](https://www.raspberrypi.com/documentation/accessories/images/color-distance.png)

颜色距离传感器，来自 Bricklink 的图像

这些颜色传感器具有多种属性和功能。您可以获得 Color ， ReflectedLight 和 AmbiantLight 。

除此之外，颜色和距离传感器可以测量 Distance ，并具有物体 Counter 。它将自动计算进出范围的物体数量。这可以用来计算通过传感器前方的物体。距离限制在 0 到 10 厘米之间。

```
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
>为了更好地测量，不建议以非常快的方式更改测量模式，颜色集成可能无法正确完成。此示例为您展示了可以使用传感器做什么。此类不实现连续测量模式。您可以通过高级模式使用 SelectModeAndRead 函数设置一个连续拥有的特定模式。重要的是要理解更改模式或设置新模式将停止先前的模式。 

#### SPIKE Prime 超声波距离传感器

![spike distance sensor](https://www.raspberrypi.com/documentation/accessories/images/spike-distance.png)

钉距传感器，来自 Bricklink 的图像

这是一个距离传感器，它实现了一个 Distance 属性，可以提供毫米距离。这个还有一个 ContinuousMeasurement 模式可用。

```
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

您可以下载有关文档

* [树莓派 Build HAT 串行协议](https://datasheets.raspberrypi.com/build-hat/build-hat-serial-protocol.pdf)
* [树莓派 Build HAT Python 库](https://datasheets.raspberrypi.com/build-hat/build-hat-python-library.pdf)

Python 库文档的详细信息也可以在 ReadTheDocs 上找到。您可以在 .NET IoT Github 存储库中找到有关 .NET 库的更多信息。

您还可以关注树莓派基金会的项目，

* [ 乐高® 游戏控制器](https://projects.raspberrypi.org/en/projects/lego-game-controller)
* [ 乐高® 机器人车](https://projects.raspberrypi.org/en/projects/lego-robot-car)
* [ 乐高® 绘图仪](https://projects.raspberrypi.org/en/projects/lego-plotter)
* [ 乐高® 机器人脸](https://projects.raspberrypi.org/en/projects/lego-robot-face)
* [ 乐高® 数据仪表板](https://projects.raspberrypi.org/en/projects/lego-data-dash)

## 设备兼容性

Build 扩展板库支持 SPIKE™组合中包含的所有乐高® Technic™设备，以及来自乐高® Mindstorms 机器人发明家套件和其他使用 PoweredUp 连接器的设备。

>**重要**
>
>包含 Maker Plate 的 SPIKE™ Prime Expansion Set 的产品代码为 45681。原始 Expansion Set 为 45680，不包括 Maker Plate。 

| 说明               | 颜色      | 乐高物品编号                     | 在固件中支持 | 在 Python 中支持 | 替代编号       | BrickLink | 可用于                                                                                  | 设置数字            | 类             | 类型   | 设备标识 |
| --------------------- | ----------- | ---------------------------------- | -------------- | ------------------ | ---------------- | ----------- | ----------------------------------------------------------------------------------------- | --------------------- | ---------------- | -------- | ---------- |
| 大角度电机          | 白色/青色 | 45602                            | 是的         | 是的             | 45602          | [ 链接](https://www.bricklink.com/v2/catalog/catalogitem.page?S=45602-1#T=S&O=%7B%22iconly%22:0%7D)          | SPIKE Prime Set, SPIKE Prime Expansion Set                                              | 45678, 45680        | 电机           | 活动   | 31       |
| 中型角度电机        | 白色/青色 | 45603                            | 是           | 是的             | 45603          | [ 链接](https://www.bricklink.com/v2/catalog/catalogitem.page?S=45603-1#T=S&O=%7B%22iconly%22:0%7D)          | SPIKE Prime Set                                                                         | 45678               | 电机           | 主动   | 30       |
| 中等角度电机        | 白色/灰色 | 6299646, 6359216, 6386708        | 是           | 是               | 436655         | [ 链接](https://www.bricklink.com/v2/catalog/catalogitem.page?P=54696c01&idColor=86#T=C&C=86)          | Mindstorms 机器人发明家                                                                 | 51515               | 电机           | 主动的 | 4B       |
| 小型角动力电机      | 白色/青色 | 45607, 6296520                   | 是的         | 是的             |                | [ 链接](https://www.bricklink.com/v2/catalog/catalogitem.page?P=45607c01)          | SPIKE Essentials Set                                                                    |                     | 电机           | 主动   | 41       |
| 光/颜色传感器       | 白色/黑色 | 6217705                          | 是的         | 是的             |                | [ 链接](https://www.bricklink.com/v2/catalog/catalogitem.page?P=37308c01&idColor=11#T=C&C=11)          | SPIKE Prime Set, SPIKE Prime Expansion Set, Mindstorms Robot Inventor, SPIKE Essentials | 45678, 45680, 51515 | 颜色传感器     | 主动   | 3D       |
| 距离传感器          | 白色/黑色 | 6302968                          | 是           | 是               |                | [ 链接](https://www.bricklink.com/v2/catalog/catalogitem.page?P=37316c01&idColor=11#T=C&C=11)          | SPIKE Prime Set, Mindstorms Robot Inventor                                              | 45678, 51515        | DistanceSensor | 主动   | 3E       |
| 系统中型电机        | 白色/灰色 | 45303, 6138854, 6290182, 6127110 | 是的         | 是的             |                |           | Wedo 2.0，乐高点子钢琴，应用程序控制的蝙蝠车                                            | 76112               |                | 被动   | 1        |
| 力传感器            | 白/黑     | 6254354                          | 是的         | 是的             | 45606          | [ 链接](https://www.bricklink.com/v2/catalog/catalogitem.page?P=37312c01&idColor=11#T=C&C=11)          | SPIKE Prime Set                                                                         | 45678               | 力传感器       | 主动   | 3F       |
| 3×3 LED            | 白色/青色 | 45608, 6297023                   | 是           | 是的             |                | [ 链接](https://www.bricklink.com/v2/catalog/catalogitem.page?P=45608c01)          | SPIKE Essentials                                                                        |                     | 矩阵           | 主动   | 40       |
| 系统列车电机        | 黑色      | 88011                            | 是的         | 是的             | 28740, 88011-1 | [ 链接](https://www.bricklink.com/v2/catalog/catalogitem.page?S=88011-1#T=S&O=%7B%22iconly%22:0%7D)          | 货运火车，迪士尼火车和车站，客运列车                                                    |                     |                | 被动   | 2        |
| 供电 LED 灯         | 黑色      | 88005                            | 是的         |                  |                | [ 链接](https://www.bricklink.com/v2/catalog/catalogitem.page?S=88005-1#T=S&O=%7B%22iconly%22:0%7D)          |                                                                                         |                     |                | 被动   | 8        |
| 中等线性电机        | 白色/灰色 | 88008                            | 是           | 是               | 26913, 88008-1 | [ 链接](https://www.bricklink.com/v2/catalog/catalogitem.page?S=88008-1#T=S&O=%7B%22iconly%22:0%7D)          | 提升, 机器人指挥官                                                                      |                     | 电机           | 主动 | 26       |
| 技术大电机          | 灰色/灰色 | 88013                            | 是的         | 是的             | 22169          | [ 链接](https://www.bricklink.com/v2/catalog/catalogitem.page?S=88013-1#T=S&O=%7B%22iconly%22:0%7D)          |                                                                                         |                     |                | 主动   | 2E       |
| Technic XL 电机     | 灰色/灰色 | 88014                            | 是的         | 是的             | 22172, 88014   | [ 链接](https://www.bricklink.com/v2/catalog/catalogitem.page?S=88014-1#T=S&O=%7B%22iconly%22:0%7D)          |                                                                                         |                     |                | 主动 | 2F       |
| 颜色 + 距离传感器   | 白色/灰色 | 88007                            | 部分         | ？               | 26912          | [ 链接](https://www.bricklink.com/v2/catalog/catalogitem.page?S=88007-1#T=S&O=%7B%22iconly%22:0%7D)          |                                                                                         |                     |                | 主动   | 25       |
| WeDo 2.0 运动传感器 | 白色/灰色 | 45304, 6138855                   |              |                  | 5003423-1      | [ 链接](https://www.bricklink.com/v2/catalog/catalogitem.page?S=9583-1#T=S&O=%7B%22iconly%22:0%7D%7D)          |                                                                                         |                     |                | 主动   | 35       |
| WeDo 2.0 倾斜传感器 | 白色/灰色 | 45305, 6138856                   |              |                  | 5003423-1      | [ 链接](https://www.bricklink.com/v2/catalog/catalogitem.page?S=9584-1#T=S&O=%7B%22iconly%22:0%7D)          |                                                                                         |                     |                | 主动   | 34       |

## 机械图纸

树莓派 Build 扩展板的机械图纸。

![mech build hat](https://www.raspberrypi.com/documentation/accessories/images/mech-build-hat.png)
