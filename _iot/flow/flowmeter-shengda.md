---
title: "电磁流量计-开封市盛达水表有限公司"
sequence: 'shengda'
---

## Overview

{:refdef: style="text-align: center;"}
![](/assets/image/iot/shengda-flowmeter-ldc-200-pic.png)
{: refdef}

### 规格

{:refdef: style="text-align: center;"}
![](/assets/image/iot/shengda-flowmeter-ldc-200-spec.png)
{: refdef}

### 键盘

{:refdef: style="text-align: center;"}
![](/assets/image/iot/shengda-flowmeter-ldc-200-keyboard-desc.png)
{: refdef}

## 两种状态 和 按键操作

### 两种状态

仪表有两种状态：**测量状态** 和 **参数设置状态**。

第一种，测量状态：

{:refdef: style="text-align: center;"}
![](/assets/image/iot/shengda-flowmeter-ldc-200-state-working.png)
{: refdef}

第二种，参数设置状态：

{:refdef: style="text-align: center;"}
![](/assets/image/iot/shengda-flowmeter-ldc-200-state-param-setting.png)
{: refdef}

### 按键操作

在这两种状态下，按键有不同的功能：

- 测量状态
  - 上键：循环选择屏幕上行显示内容
  - 下键：循环选择屏幕下行显示内容
  - 复合键 + 确认键：进入**参数设置状态**（按键顺序，先按下**复合键**，再按下**确认键**）
- 参数设置状态
  - 移动
    - 上键：向上移动
    - 下键：向下移动
    - 复合键 + 下键：向左移动（按键顺序，先按下**复合键**，再按下**下键**）
    - 复合键 + 上键：向右移动（按键顺序，先按下**复合键**，再按下**上键**）
  - 确认键
    - 短按：进入/退出子菜单
    - 长按：连续按下 5 秒钟，返回**测量状态**

## 进行参数设置

要进行仪表参数设定，必须使仪表从**测量状态**进入**参数设置状态**。

### 进入参数设置状态

在**测量状态**下，按**复合键+确认键**，此时出现如下界面：

{:refdef: style="text-align: center;"}
![](/assets/image/iot/shengda-flowmeter-ldc-200-param-setting-001.png)
{: refdef}

等待几秒后，进入**参数设置**界面：

{:refdef: style="text-align: center;"}
![](/assets/image/iot/shengda-flowmeter-ldc-200-param-setting-002.png)
{: refdef}

按下**确认键**，出现状态转换密码（`00000`）：：

{:refdef: style="text-align: center;"}
![](/assets/image/iot/shengda-flowmeter-ldc-200-param-setting-003.png)
{: refdef}





### 输入密码

输入密码：`19818`

{:refdef: style="text-align: center;"}
![](/assets/image/iot/shengda-flowmeter-ldc-200-param-setting-004.png)
{: refdef}

输入密码完成后，再次按下**复合键+确认键**，就进入**参数设置状态**。

### 参数项

#### 语言

语言：中文、英文

{:refdef: style="text-align: center;"}
![](/assets/image/iot/shengda-flowmeter-ldc-200-param-setting-005.png)
{: refdef}

{:refdef: style="text-align: center;"}
![](/assets/image/iot/shengda-flowmeter-ldc-200-param-setting-005-val.png)
{: refdef}

#### 仪表通讯地址

设备地址：001~255

为什么是001到255呢？因为它占用1个字节。

{:refdef: style="text-align: center;"}
![](/assets/image/iot/shengda-flowmeter-ldc-200-param-setting-006.png)
{: refdef}

{:refdef: style="text-align: center;"}
![](/assets/image/iot/shengda-flowmeter-ldc-200-param-setting-006-val.png)
{: refdef}

例如，下面的16进制数：

```text
0x01041010000274CE
```

第一个字节就是`0x01`，它就是通讯地址。

#### 仪表通讯速度

波特率：300、600、1200、4800、9600、14400、19200、38400

{:refdef: style="text-align: center;"}
![](/assets/image/iot/shengda-flowmeter-ldc-200-param-setting-007.png)
{: refdef}

{:refdef: style="text-align: center;"}
![](/assets/image/iot/shengda-flowmeter-ldc-200-param-setting-007-val.png)
{: refdef}

#### 测量管道口径

{:refdef: style="text-align: center;"}
![](/assets/image/iot/shengda-flowmeter-ldc-200-param-setting-008.png)
{: refdef}

{:refdef: style="text-align: center;"}
![](/assets/image/iot/shengda-flowmeter-ldc-200-param-setting-008-val.png)
{: refdef}

#### 流量单位

流量单位：

<ul>
  <li>升：\(L/s\)、\(L/m\)、\(L/h\)</li>
  <li>立方米：\(m^{3}/s\)、\(m^{3}/m\)、\(m^{3}/h\)</li>
  <li>吨：\(T/s\)、\(T/m\)、\(T/h\)</li>
</ul>

{:refdef: style="text-align: center;"}
![](/assets/image/iot/shengda-flowmeter-ldc-200-param-setting-009.png)
{: refdef}

{:refdef: style="text-align: center;"}
![](/assets/image/iot/shengda-flowmeter-ldc-200-param-setting-009-val.png)
{: refdef}

#### 仪表量程设置

{:refdef: style="text-align: center;"}
![](/assets/image/iot/shengda-flowmeter-ldc-200-param-setting-010.png)
{: refdef}

#### 流向

流向：正向、反向

{:refdef: style="text-align: center;"}
![](/assets/image/iot/shengda-flowmeter-ldc-200-param-setting-011.png)
{: refdef}

## Modbus 指令

### 变量寄存器地址表

{:refdef: style="text-align: center;"}
![](/assets/image/iot/shengda-flowmeter-l-mag-modbus-variable-address.png)
{: refdef}

- 单条数据
  - 瞬时流量（浮点）: `01041010000274CE`
  - 瞬时流速（浮点）: `010410120002D50E`
  - 流量百分比（浮点）: `010410140002350F`
  - 流体电导比（浮点）: `01041016000294CF`
  - 正向累积量整数部分（整数）: `010410180002F50C`
  - 正向累积量小数部分（浮点）: `0104101A000254CC`
  - 反向累积量整数部分（整数）: `0104101C0002B4CD`
  - 反向累积量小数部分（浮点）: `0104101E0002150D`
  - 瞬时流量单位（Unsigned short）: `01041020000134C0`
  - 累积总量单位（Unsigned short）: `0104102100016500`
  - 上限报警（Unsigned short）: `0104102200019500`
  - 下限报警（Unsigned short）: `010410230001C4C0`
  - 空管报警（Unsigned short）: `0104102400017501`
  - 系统报警（Unsigned short）: `01041025000124C1`
- 多个数据: `01041010001674C1`


```text
1623226509806317570
1623227386877276161
instantaneousFlow@1

PRS@162322650980631
CRI@162322738687727

AE@162322738687727
AH@162322738687727
AL@162322738687727
AS@162322738687727

CRI@162322738687727
CRF@162322738687727
CFI@162322738687727
CFF@162322738687727

FP@162322738687727
FV@162322738687727
FI@162322738687727

RC@162322738687727

UC@162322738687727
UF@162322738687727
```

```text
AE: emptyPipeAlarm
AH: alarmHighValue
AL: alarmLowValue
AS: systemAlarm

CRI: reverseAccumulation Integer
CRF: reverseAccumulation Fraction
CFI: forwardAccumulation Integer
CFF: forwardAccumulation Fraction

FP: flowPercentage
FV: flowVelocity
FI: instantaneousFlow

RC: fluidConductivityRatio

UC: cumulativeTotalUnit
UF: flowUnit
```

```text
/sys/${productKey}/${deviceName}/thing/event/property/post
/sys/shengda/flowmeter/thing/event/property/post
```

### 参数寄存器地址表

```text
0106003F4D6A
```

#### 修改流量单位

第一步，输入密码：

主机命令：

```text
0106003F4D6A0CB9
```

从机回应：

```text
01 06 00 3F 4D 6A 0C B9
```

第二步，发送修改流量单位命令

主机命令：

```text
010600060005A9C8
```

从机回应：

```text
01 06 00 06 00 05 A9 C8 
```

第三步，修改语言为英文

主机命令：

```text
010600000001480A
```

从机回应：

```text

```

#### 总量清零

发送总量清零命令，密码为 `42330` (`0xA55A`)。

第一步，输入密码：

主机命令：

```text
01060047A55AC2B4
```

从机回应：

```text

```
