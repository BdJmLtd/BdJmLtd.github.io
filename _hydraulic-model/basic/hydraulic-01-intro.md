---
title:  "水力模型：介绍"
sequence: 001
---

## 是什么

简单地说，管网模型就是根据**真实的供水管网**建立的**数学模型**。

```text
管网模型 = 真实的供水管网 ---> 数学模型
```

管网模型是按照一定的数学原理建立的供水管网水力、 水质方程组以及管网各种的动态和静态信息科学地有机组成的总体。

```text
管网模型的内容 = 供水管网 + 水力 + 水质
```

管网模型，是**模拟、仿真供水管网系统**动态工部的最有效工具。

```text
管网模型的作用 = 模拟（现在） + 预测（未来）
```

## 分类

管网模型的分类：

- 大小
    - 宏观模型
    - 微观模型
- 难易
    - 简化模型
    - 复杂模型
- 动静
    - 静态模型
    - 动态模型

## 管网模型与现有系统

### 现有系统

- GIS系统
- SCADA系统
- DMA系统
- 营业收费系统

DMA（District Metering Area，即独立计量区域）是指通过截断管段或关闭管段上阀门的方法，将管网分为若干个相对独立的区域，
并在每个区域的进水管和出水管上安装流量计，从而实现对各个区域入流量与出流量的监测。

{:refdef: style="text-align: center;"}
![](/assets/image/pipeline/dma/typical-dma-configuration.png)
{: refdef}

SCADA(Supervisory Control And Data Acquisition)系统，即数据采集与监视控制系统，
是以计算机为基础的生产过程控制与调度自动化系统，它可以对现场的运行设备进行监视和控制。

### 系统之间的依赖关系

管网建模系统的依赖关系：

{:refdef: style="text-align: center;"}
![](/assets/image/hydraulic-model/hydraulic-model-relations-with-other-info-systems.png)
{: refdef}

