---
title: "水力模型：快速介绍"
sequence: "007"
---

## 什么是水力模型？

简单地说，**管网模型**就是根据**真实的供水管网**建立的**数学模型**。

```text
管网模型 = 真实的供水管网 ---> 数学模型
```

## 管网模型

### 物理管网的组成（现实）

在真实的管网当中，包含了不同的组成部分。例如，管线、阀门、水泵、水池等。

- 问题：在现实世界中，这些组成部分（管线、阀门、水泵、水池）怎么转换成**管网模型**呢？
- 回答：提取关键的物理参数。

### 管网模型的组成（抽象）

{:refdef: style="text-align: center;"}
![](/assets/image/hydraulic-model/pipeline-network-model.png)
{: refdef}

## 水力计算

### 计算什么？

在管网当中，需要解决的两个最基本问题：

- 第一个，每一个管线（pipe/link）中的“流速”是多少？
- 第二个，每一节点（junction/node）中的“水头”（head）是多少？

### 计算思路

求解思路：将“大问题”转换成“小问题”。

从整体来说，完整管网的水力计算，是比较复杂的，不太容易计算。

相对而言，一根管线的水计算，则会容易一些。

### 如何计算？

EPANET使用Global Gradient Algorithm (GGA)，需要多次迭代。
每次迭代，分成两个步骤来解决：

- 第一步，求解node heads
- 第二步，求解link flow

迭代求解：水力模型的求解，需要进行多次迭代（循环）来求解，每一次迭代都会引起流量、水头的变化。

条件收敛：水力模型，达到一个“稳定”的状态之后，就会停止下来。

{:refdef: style="text-align: center;"}
![](/assets/image/hydraulic-model/hydraulic-model-gga.png)
{: refdef}
