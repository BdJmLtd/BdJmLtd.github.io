---
title: "微型工业级RTU TG501-计讯 配置过程"
sequence: 103
---

```text
<Time:2023-03-15 10:34:17>:载入设备参数成功 ...
<Time:2023-03-15 10:34:20>:AT+VER
<Time:2023-03-15 10:34:21>:Version:TG501B1-B01-06.7
Time: Apr 22 2022 10:07:03 
OK
```

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-setting-config-version-tg501b1-b01-067.png)
{: refdef}

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-setting-config-version-tg501b1-b01-067-mqtt.png)
{: refdef}

```text
<Time:2023-03-15 10:45:34>:载入设备参数成功 ...
<Time:2023-03-15 10:45:36>:AT+VER
<Time:2023-03-15 10:45:38>:Version:TG501B1-B01-06.7-MQTT-V1.2
Time: Apr 22 2022 10:12:14 
OK
```

## 升级

第一步，打开 `TG501B1-CN-1.29-MQTT-V1.0.exe` 软件。

第二步，在**下载工具**中，点击**加载**按钮，找到 `TG501B1-B01-06.7-MQTT-V1.2.bin` 文件。

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-upgrade-001.png)
{: refdef}

第三步，点击**下载**按钮。这时候，会提示“请将设备重新上电”，我们只要拔掉电源，等一会儿，再接上电源就行了。

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-upgrade-002.png)
{: refdef}

如果右侧信息中出现错误（download x block error），只要再次点击**下载**按钮即可。

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-upgrade-003.png)
{: refdef}

等待一会儿，就会成功，看到右侧提示信息 ”download success ok“：

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-upgrade-004.png)
{: refdef}

## 参数配置

选择**参数配置**，然后点击**进入配置**：

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-setting-enter-config.png)
{: refdef}

### 通道参数设置（压力）

在 `参数配置 --> 通道参数设置 --> 通道01` 界面，设置如下：

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-setting-adc0-config-001.png)
{: refdef}

第一步，设置**硬件接口**

- 硬件接口：`ADC0`

在下图当中，在 `ADC0` 接口连接一根线到压力变送器上，因此选择  `ADC0`。

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-adc0-line.png)
{: refdef}


第二步，设置**通信参数**。这些值，与压力变送器的参数密切相关。

- 通信参数：
    - ADC类型：电流 （因为压力变送器输出的是 4-20mA 的电流）
    - 上量程：`1` （压力变送器的量程是 0-1MPa）
    - 下量程：`0` （压力变送器的量程是 0-1MPa）
    - 输入电流最大值：`20` （压力变送器的输出是 4-20mA）
    - 输入电流最小值：`4` （压力变送器的输出是 4-20mA）
    - 采集开关：启用
    - 上报编码：`PRS@xxxxxx` （这里是 Json 格式里的 key，根据实际情况调整）

{:refdef: style="text-align: center;"}
![](/assets/image/iot/pressure-transmitter-parameters-001.png)
{: refdef}

```text
{
    "params": {
        // 上报编码，决定这里的 key
        "PRS@162322650980631": 0.00,
        ...
    },
    "timestamp": "1675909110000"
}
```

第三步，进行保存。点击**保存参数**，可以看到右侧输出“设置成功”：

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-setting-adc0-config-002.png)
{: refdef}


### 串口设置

在 `参数配置 --> 串口设置` 界面，设置如下：

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-setting-serial-rs4850-config-001.png)
{: refdef}

第一步，设置 `RS485-0` 中的波特率为 `9600`。

第二步，进行保存。点击**保存参数**，可以看到右侧输出“设置成功”：

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-setting-serial-rs4850-config-002.png)
{: refdef}

问题一：为什么选择 `RS485-0` 串口？

在下图当中，
- `A0` 和 `B0` 就代表 `RS485-0`串口，它连接的就是流量计。当前设备，不支持 `RS485-1` 串口。
- 右侧的 `GND`、`RXD0` 和 `TXD0` 是 `RS232-0` 串口，它是连接电脑的，用来调试设备用的。
- 左侧的 `GND`、`RXD1` 和 `TXD1` 是 `RS232-1` 串口，它的用途是连接具体的设备，但是并没有使用。

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-rs4850-line.png)
{: refdef}

问题二：为什么 `RS485-0` 串口中选择波特率为 `9600`？
这是因为流量计上设置的波特率也是 9600，RTU 和流量计两者必须一致，才能正常通信。

{:refdef: style="text-align: center;"}
![](/assets/image/iot/shengda-flowmeter-ldc-200-param-setting-007.png)
{: refdef}

{:refdef: style="text-align: center;"}
![](/assets/image/iot/shengda-flowmeter-ldc-200-param-setting-007-val.png)
{: refdef}


### 中心地址参数

在 `参数配置 --> 中心地址参数` 界面，设置如下：

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-setting-server-config-001.png)
{: refdef}

第一步，在**中心 1** 中，串口选择 `RS485-0`，并设置**主地址**和**端口**：

- 串口选择：`RS485-0`
- 主地址：`36.138.170.195`
- 端口：`1883`

第二步，进行保存。点击**保存参数**，可以看到右侧输出“设置成功”：

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-setting-server-config-002.png)
{: refdef}

### MODBUS

在下面的配置采集器的过程，需要用到流量计的 Modbus 变量地址信息：

{:refdef: style="text-align: center;"}
![](/assets/image/iot/shengda-flowmeter-l-mag-modbus-variable-address.png)
{: refdef}

#### 采集器 0 瞬时流量

在 `参数配置 --> MODBUS` 界面，设置如下：

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-setting-modbus-sensor-01-001.png)
{: refdef}

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-setting-modbus-sensor-01-002.png)
{: refdef}

#### 采集器 1 瞬时流速

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-setting-modbus-sensor-02-001.png)
{: refdef}

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-setting-modbus-sensor-02-002.png)
{: refdef}

#### 采集器 2 流量百分比

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-setting-modbus-sensor-03-001.png)
{: refdef}

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-setting-modbus-sensor-03-002.png)
{: refdef}

#### 采集器 3 流体电导比

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-setting-modbus-sensor-04-001.png)
{: refdef}

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-setting-modbus-sensor-04-002.png)
{: refdef}

#### 采集器 4 正向累积量整数部分

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-setting-modbus-sensor-05-001.png)
{: refdef}

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-setting-modbus-sensor-05-002.png)
{: refdef}

#### 采集器 5 正向累积量小数部分

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-setting-modbus-sensor-06-001.png)
{: refdef}

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-setting-modbus-sensor-06-002.png)
{: refdef}

#### 采集器 6 反向累积量整数部分

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-setting-modbus-sensor-07-001.png)
{: refdef}

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-setting-modbus-sensor-07-002.png)
{: refdef}

#### 采集器 7 反向累积量小数部分

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-setting-modbus-sensor-08-001.png)
{: refdef}

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-setting-modbus-sensor-08-002.png)
{: refdef}

#### 采集器 8 瞬时流量单位

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-setting-modbus-sensor-09-001.png)
{: refdef}

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-setting-modbus-sensor-09-002.png)
{: refdef}

#### 采集器 9 累积总量单位

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-setting-modbus-sensor-10-001.png)
{: refdef}

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-setting-modbus-sensor-10-002.png)
{: refdef}

#### 采集器 10 上限报警

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-setting-modbus-sensor-11-001.png)
{: refdef}

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-setting-modbus-sensor-11-002.png)
{: refdef}

#### 采集器 11 下限报警

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-setting-modbus-sensor-12-001.png)
{: refdef}

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-setting-modbus-sensor-12-002.png)
{: refdef}

#### 采集器 12 空管报警

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-setting-modbus-sensor-13-001.png)
{: refdef}

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-setting-modbus-sensor-13-002.png)
{: refdef}

#### 采集器 13 系统报警

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-setting-modbus-sensor-14-001.png)
{: refdef}

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-setting-modbus-sensor-14-002.png)
{: refdef}

### MQTT

在 `参数配置 --> MQTT` 界面，设置如下：

- 用户名：`devops`
- 密码：`123456`
- 订阅主题：`xxx` （暂时没有想好）
- 发布主题：`/sys/shengda/flowmeter/thing/event/property`
- client ID: `client-from-rtu`
- 数据格式：`json`
- 上报时间间隔：`30` （单位：秒）

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-setting-mqtt-config-001.png)
{: refdef}

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-setting-mqtt-config-002.png)
{: refdef}

### 重启设备

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot/rtu-setting-restart.png)
{: refdef}
