---
title: "微型工业级RTU TG501-计讯"
sequence: 102
---

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot-rtu-rs485-usb.jpg)
{: refdef}


## RTU 设备连接电脑

第一步，使用 RS232 串口，转换成 USB 接口，然后连接电脑

> 备注：我使用 RS485 串口，总是不成功；换成 RS232 就成功了。

第二步，查看是否连接成功。

右键**此电脑**，选择**管理**（或者运行 `devmgmt.msc` 命令）：

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot-rtu-tg501-b1-001.png)
{: refdef}

打开**计算机管理**对话框后，选择**设备管理器**，
在右侧选择**端口（COM 和 LPT）**，可以看到有一个**USB Serial Port (COM5)**，表示 RTU 连接电脑成功了：

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot-rtu-tg501-b1-002.png)
{: refdef}

## 打开软件

第一步，打开 `TG501B1-TOOLS-V1.19.exe` 或 `TG501B1-CN-1.29-MQTT-V1.0.exe` 软件：

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot-rtu-tg501-b1-003.png)
{: refdef}

第二步，查看参数。

在软件的左下角，可以看到串口号、波特率和校验位的信息：

- 串口号：COM5 （这里会根据连接的 USB 接口位置不同而变化）
- 波特率：115200 （一定要选择 `115200` 波特率）
- 校验位：None

如果下方的按钮显示为

- “关闭串口”，表明串口已经打开，不需要做任何操作 （**默认情况**）
- “打开串口”，表明串口没有打开，需要点击按钮进行打开

## RTU 的两种状态

RTU 有两个状态：

- 第一个，**工作状态**，用于发送数据（压力、流量）
- 第二个，**参数配置状态**，用于设置参数

这两个状态是彼此互斥的。
比如说，对 RTU 进入了“参数配置状态”，（设置服务器的地址），此时 RTU 就不在“工作状态”了，也就是不会发送任何数据给服务器。
参数配置完成后，需要重启设备，配置的参数才会生效；重启完成之后，自动进入**工作状态**，就可以发送数据了。

默认情况下，RTU 处于**工作**状态。

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot-rtu-tg501-b1-004.png)
{: refdef}



两种状态的切换：

- 从工作状态向

，需要**断电**或**重启设备**操作。

### 进入工作状态

第一步，选择**调试工具**，点击**开启接收**按钮：

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot-rtu-tg501-b1-005.png)
{: refdef}

第二步，左侧变成“灰色”不能进行选择，表示正在使用“工作”状态：

- 点击“关闭接收”，可以退出调试，不再接收设备的信息
- “保存日志”和“清除日志”都是对上面的调试信息进行操作

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot-rtu-tg501-b1-006.png)
{: refdef}

### 进入参数设置状态

第一步，选择**参数配置**，再点击**重新加载**：

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot-rtu-tg501-b1-007.png)
{: refdef}

这时，弹出提示信息“请将设备重新上电”，断开电源 10 秒，再接通电源就好了：

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot-rtu-tg501-b1-008.png)
{: refdef}

断开电源，停留 10 秒，再接通电源，看到“载入设备参数成功...”的信息：

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot-rtu-tg501-b1-009.png)
{: refdef}

第二步，点击**进入配置**按钮（这一步好像没用）：

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot-rtu-tg501-b1-010.png)
{: refdef}

第三步，选择**中心地址参数**，在**中心1**设置**主地址+端口**：

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot-rtu-tg501-b1-011.png)
{: refdef}

第四步，配置完成后，点击**保存参数**，最后点击**重启设备**。

```text
注意：参数配置完成后，需要重启设备，否则参数无法生效。
```

## RTU 与流量计

### 设备连接（物理层面）

使用 RS485 线，将 RTU 与 流量计 两个设备连接起来：

{:refdef: style="text-align: center;"}
![](/assets/image/iot/rtu-rs485-connect-flow-meter.png)
{: refdef}

### 参数配置（软件层面）

第一步，在**串口设置**中选择正确的串口，例如，与 RTU 连接就是使用 `RS485-0` 串口，设置正确**波特率**：

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot-rtu-tg501-b1-012.png)
{: refdef}

第二步，在**中心地址参数**中，一定要将**串口选择**设置正确（对应上一步的 `RS485-0` 串口），否则接收不到数据：

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot-rtu-tg501-b1-013.png)
{: refdef}

## Reference

- [计讯](http://www.top-iot.com/)
    - [微型工业级RTU TG501](http://www.top-iot.com/content-55-62-1.html)
