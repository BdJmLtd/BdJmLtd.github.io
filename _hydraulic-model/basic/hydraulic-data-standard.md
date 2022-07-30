---
title:  "水力模型：数据标准"
sequence: 003
---

外部管线数据入库需要遵守如下数据标准：

点表：

{:refdef: style="text-align: center;"}
![](/assets/image/hydraulic-model/data/hydraulic-data-standard-point.png)
{: refdef}

线表：

{:refdef: style="text-align: center;"}
![](/assets/image/hydraulic-model/data/hydraulic-data-standard-line.png)
{: refdef}

上图代表点和线对象的属性结构，其中带`*`号的属性为必填属性，也就是外部数据入系统时必须不为空的属性。带`？+数字`的表示相同数字的属性至少有一个不为空。

其中阀门类型只能取值为：PRV(减压阀)，PSV(稳压阀)，PBV(压力制动阀)，FCV(流量控制阀)，TCV(节流控制阀)，GPV(常规阀门)。

不同类型的阀门，阀门参数代表的意义不同：对于PRV，PSV和PBV，代表压力；对于FCV，为流量；对于TCV，为损失系数；对于GPV，为水头损失曲线。
属性下面的带括号的文字描述的是属性值的单位。

如果不能准知道管线的粗糙系数，就要填上管线材质，以便根据不同材质默认的粗糙系数进行计算，材质可选项为：铸铁，混凝土（或衬里），镀锌铁，塑料，钢，陶土。

