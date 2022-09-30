---
title: "DMA信息系统"
sequence: 111
---

## 水务概览

智慧水务集控平台，统一管理权限管理认证（用户、角色、权限），各个子系统关注各自的业务逻辑。

> 权限统一管理，业务各自实现

{:refdef: style="text-align: center;"}
![](/assets/image/dma/water-affairs.png)
{: refdef}

DMA系统，是“智慧水务集控平台”的子系统，**主要解决的问题是供水管网中的水损控制问题**。

> DMA的作用

## 功能模块

{:refdef: style="text-align: center;"}
![](/assets/image/dma/dma-modules.png)
{: refdef}

## DMA与其它系统之间的关系

{:refdef: style="text-align: center;"}
![](/assets/image/dma/from-pipeline-to-dma.png)
{: refdef}

- 静态信息
    - GIS：提供地图服务，引入管网的空间信息
    - 表务管理：水表设备的信息
- 动态信息：
    - SCADA：在GIS和表务管理的基础上，实时收集各种数据，并进行控制
        - 流量，进入DMA系统，评估漏水，再进一步计算产销差
        - 压力，进入压力管理，通过调节压力大小，来维护管网运行的稳定性
        - 水质，进入水质监测系统，来保障居民的健康

实现DMA系统的步骤：

- 第一步，在GIS图上进行分区，三个层级的分区（大、中、小）
    - 空间信息：在地图上绘制
    - 属性信息：DMA分区的名称、用水的类型
    - 分区标准：管径（大用户）、用水类型
- 第二步，表务管理，对水表进行管理
    - 属性信息：仪表号，安装时间、安装位置（描述）
    - 空间信息：水表与具体的”点“信息绑定
- 第三步，DMA分区与设备进行关联
- 第四步，采集数据



