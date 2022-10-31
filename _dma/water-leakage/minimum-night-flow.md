---
title: "夜间最小流量 MNF (Minimum Night Flow)"
sequence: 103
---

**夜间最小流量**，是每天夜里流入DMA的最小流量。
大多数情况下，这个流量主要是**泄漏**造成的，**用户消费**所占份额很小。

> 引入“夜间最小流量”的概念

```text
夜间最小流量 = 泄漏水量（管网） + 用户用水量（人）
```

一般在晚上，用户用水量最低，此时定量泄漏最准确。

{:refdef: style="text-align: center;"}
![](/assets/image/dma/minimum-nightly-flow.png)
{: refdef}


如果所有能查到的泄漏及时修复，则**夜间最小流量**只包括**用户夜间用水**和**背景泄漏**（检测不到）。

```text
笔记：理论情况下，夜间最小流量 = 用户夜间用水 + 背景泄漏
```

## 组成部分

> 此处内容参考自[这里][link01]

<table class="w3-center">
<caption>Components of the night flow</caption>
<thead>
<tr>
    <th>Components of night flow</th>
    <th>Composition</th>
    <th>Abbreviation</th>
    <th>Unit</th>
    <th>Method of determination</th>
</tr>
</thead>
<tbody>
<tr>
    <td rowspan="3">(EMNF)</td>
    <td>Domestic users</td>
    <td>\(Q_{dom}\)</td>
    <td>\(m^{3}/h\)</td>
    <td>Estimated</td>
</tr>
<tr>
    <td>Small non-domestic users</td>
    <td>\(Q_{bulk,small}\)</td>
    <td>\(m^{3}/h\)</td>
    <td>Estimated</td>
</tr>
<tr>
    <td>Large non-domestic users</td>
    <td>\(Q_{bulk,large}\)</td>
    <td>\(m^{3}/h\)</td>
    <td>Measured</td>
</tr>
<tr>
    <td>Transfer</td>
    <td>Transfer of water to neighboring zones</td>
    <td>\(Q_{trans}\)</td>
    <td>\(m^{3}/h\)</td>
    <td>Measured</td>
</tr>
<tr>
    <td>ENF</td>
    <td>Background losses and burst pipes</td>
    <td>\(Q_{loss}\)</td>
    <td>\(m^{3}/h\)</td>
    <td>Calculated</td>
</tr>
</tbody>
</table>

The MNF technique is suitable for the systems with a continuous supply.
The share of **legitimate consumption** and **losses** is determined using Equation

<p>
\[
Q_{in} = Q_{dom} + Q_{bulk} + Q_{trans} + Q_{loss}
\]
</p>

<ul>
    <li>\(Q_{in}\) is the system input</li>
    <li>\(Q_{dom}\) is the domestic night-time consumption</li>
    <li>\(Q_{bulk}\) is the small and large non-domestic nighttime consumptions</li>
    <li>\(Q_{trans}\) is for the transfer of water to neighboring zones</li>
    <li>\(Q_{loss}\) is for the water loss</li>
</ul>

<p>
The <b>legitimate consumption</b> includes
the <b>domestic nighttime consumption</b> (mostly for flushing toilets), \(Q_{dom}\),
and <b>non-domestic nighttime consumption</b>
(administrative, industrial, commercial or agricultural consumers), \(Q_{bulk}\).
</p>

```text
笔记：

legitimate consumption = domestic nighttime consumption + non-domestic nighttime consumption

合情合理的夜间用水量 = 家庭用户用水量 + 非家庭用户用水量
```

**Legitimate consumption** can be a large portion of the **MNF**.
A **field examination** can estimate or determine domestic nighttime consumption;
however, it is important to specify the nighttime consumption of major consumers.

```text
笔记：合理的用水量，可能占用MNF很大的比例，要进行实地调查。
```

<p>
The amount of water transfer to neighboring zones, \(Q_{trans}\),
should be either evaluated or stopped during the evaluation of <b>MNF</b>.
</p>

```text
笔记：在计算MNF时，如果有向邻近区域输水的情况，也需要考虑。
```

## 数据采集

### 采集来源

在简单的DMA中，**夜间最小流量**从单一的设备读取。

```text
简单情况
```

而在有些场合，**夜间最小流量**是几个监测设备计量值之和的最小值（而不是每个监测设备计量的最小值之和）。

```text
复杂一些的情况
```

### 采集频率

> 《分区定量管理理论与实践》（第二版）第39和40页

夜间流量，应该是设定时间（通常按**每小时**）内的平均流量。

通常数据记录仪设定为至少每隔1小时记录1次流量，得到流量1h移动平均值的最小值，
该值与记录的时间间隔略有一些关系，一般可以忽略不计。

```text
笔记：周期为1小时
```

> 期刊《数据采集设置对DMA流量模式的影响》 王子麒 第3页

从基于MNF的真实漏失评估的角度来说，应尽可能地缩短数据采集的周期。
但缩短采集周期无疑增加了水表内存与电量的要求。
在实际工作中，应在二者之间做出权衡。

```text
笔记：理论上来说，周期越短越好；缺点是费电
```

> 期刊《数据采集设置对DMA流量模式的影响》 王子麒 第5页 结论

从真实漏失（real water loss，物理漏失）的角度，采集周期设置为5~15 min较为合理。

```text
笔记：合理的周期为5~15分钟
```

### 出现时间

一般在凌晨2点至凌晨5点之间。

Also, according to hydraulic and consumption conditions,
the **highest frequency of MNF occurrence** was observed at `00:00` and `05:00`.

## 影响因素

### DMA分区大小

DMA的大小影响泄漏水平的识别。

大的DMA漏水量和夜间用水量相对较大，一个漏点占最小流量的比较较小，也就是**分辨率低**。

### 季节

夜间用水量受季节影响很小。

在大多数DMA中，用户夜间用水量每个星期和每个季度会有变化，所以在分析夜间流量组成时需结合当地情况。

## 夜间最小流量分析

> 《分区定量管理理论与实践》（第二版）第89页

夜间最小流量分析：通过每天分析DMA分区内各个区域的夜间最小流量与前几天的夜间最小流量进行对比，从而判断该区域是否有漏水发生。

[link01]: https://iwaponline.com/ws/article/20/6/2296/75114/Leakage-estimation-in-water-networks-based-on-the
