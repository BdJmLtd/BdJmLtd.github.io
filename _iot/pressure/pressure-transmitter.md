---
title: "压力变送器-淄博秉润自动化仪表有限公司"
sequence: '001'
---

## 压力变送器

### 压力变送器参数

压力变送器参数

- 规格型号：BR20FUEIIERLm(5)C1
- 量程：0-1MPa
- 输出：4-20mA
- 供电：24VDC
- 生产日期：2016.10

{:refdef: style="text-align: center;"}
![](/assets/image/iot/pressure-transmitter-parameters-001.png)
{: refdef}

{:refdef: style="text-align: center;"}
![](/assets/image/iot/pressure-transmitter-parameters-002.png)
{: refdef}

### 设备连接

{:refdef: style="text-align: center;"}
![](/assets/image/iot/pressure-transmitter-connect-rtu.png)
{: refdef}

{:refdef: style="text-align: center;"}
![](/assets/image/iot/pressure-transmitter-connect-rtu-abstract.png)
{: refdef}

- 变压器，将 220V 交流电转换成 24V 直流电
- RTU，工作电压是 5V-35V 直流电，接收 24V 直流电是没有问题的
- 压力变送器
  - 供电要求是 24V 直流电，正好符合
  - 压力变送器，输出 4-24mA 的电流，这就是**模拟量**，它会传输给 RTU，接着，RTU 负责将 **模拟量**（电流）转换成**数字量**。

### 电压

- VDC 经常作为 Volts Direct Current 的缩写，用来表示**直流电压**。
- VAC 表示**交流电压**。

## RTU 配置

### 配置 ADC

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot-rtu-tg501-b1-adc0-config.png)
{: refdef}

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot-rtu-tg501-b1-adc0-config-pressure-transmitter.png)
{: refdef}

### 配置 MODBUS 工作模式

{:refdef: style="text-align: center;"}
![](/assets/image/iot/top-iot-rtu-tg501-b1-mode-modbus-rtu.png)
{: refdef}

在上图中，

- MODBUS 工作模式：选择**网络RTU功能**
- MODBUS 设备地址（1-255）：2

例如，一条 16 进制的压力指令：`0x0203000A0002E43A`。第一个字节是 `0x02`，就表示设备地址是 `2`。


