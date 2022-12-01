---
title: "供水管网健康评估"
sequence: 103
---

对供水管线的状态进行评估，即寻找**影响管线健康的因素**与**管线状态**之间的关系。

## 概览

**Water Pipeline Condition Assessment** provides water utilities with an appropriate path
for determining the structural status of an individual pipeline or pipeline system.

```text
小总结：
- 1、管网健康评估的对象，可以是单个管段（an individual pipeline），也可以是整个管网（pipeline system）。

Water Pipeline Condition Assessment --> the structural status of an individual pipeline(单独管段) or pipeline system(管网系统)

```

Such **condition assessments** form a critical piece of an effective **asset management** program
by establishing a baseline to understand the present state of a pipeline.
By recognizing that current state, the **asset management** program then enables the **water utility**
to anticipate future issues and allocate the appropriate measures
to be undertaken to provide for the continuous safe and reliable operation of the system.

```text
小总结：
- 1、管网健康评估（condition assessments），是资产管理（asset management）的一部分。
- 2、管网健康评估的作用：（1）预测未来可能发生的事情；（2）在预测的基础上，提前采取措施

asset management(资产管理) --> condition assessments --> future issues(预测未来可能发生的事情) + appropriate measures(采取措施)
```

This Manual of Practice focuses on the **larger diameter transmission pipelines** of water utilities,
rather than the **smaller diameter distribution systems**.

```text
小总结：关注的是管径较大的管段。
```

It provides technical information and recommendations to **set priorities** and
obtain an accurate determination of the condition of **the individual pipelines** and **pipeline systems**.

```text
小总结：不同的指标，起到的作用大小也不相同，因此有优先级（priorities）的概念。
```

## 思路

### 基于BP神经网络的城市供水管网健康状态评估

- 输入参数
    - 管材（pipe material）
    - 管龄（pipe age）
    - 管径（pipe diameter）
    - 管长（pipe length）
    - 接口类型（junction type）
- 输出参数
    - 管线发生事故的风险系数（risk coefficient of pipe damage）

- 评价方法
    - 传统的方法（缺点：主观性强，数据质量要求高）
        - 基于多元线性回归
        - 层次分析法
        - 模糊理论
    - 新方法
        - 人工神经网络（Artificial Neural Network）
        - 误差反向传播人工神经网络，简称BP（Back-Propagation）神经网络

管网发生破损事故，是内、外因综合作用的结果，影响因素众多且复杂。
在参阅国内外研究成果及了解水厂工作经验的基础上，大致可以概括为物理因素、环境因素、管道运行状况三大类。

- 管线信息（输入参数）
    - 物理因素
        - 管材
        - 管径
        - 管长
        - 管壁厚
        - 安装年代
        - 接头类型
        - 管道防腐
    - 环境因素
        - 路面情况
        - 周边环境
        - 覆土土质
        - 覆土厚度
    - 运行状况
        - 水压
        - 维修记录

由于我国管网基础数据建设尚不完善，且部分数据收集不易，获取全面完整的管线信息难度很大，因此输入参数的选取需要根据各管网的实际情况而定。

本研究筛选出完整度较高的管材、管龄、管径、管长和接口类型5个参数，即模型的输入层节点数为5。

## Reference

- [基于因子分析的供水管网健康状态评价指标遴选_丁相毅](https://www.doc88.com/p-73547190956386.html)
- [基于BP神经网络的城市供水管网健康状态评估_常田](https://www.doc88.com/p-7817627120386.html)
- [城市供水管网管线健康状态评估方法研究及其应用](https://www.doc88.com/p-0846481527030.html)
- [基于回归树的城市供水管网状态估计研究](https://www.doc88.com/p-9743829138570.html)


- [Water Pipeline Condition Assessment](https://ascelibrary.org/doi/book/10.1061/9780784414750)
- []()
