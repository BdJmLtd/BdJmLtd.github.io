---
title: "夜日因子 NDF (Night to Day Factor)"
sequence: 112
---

```text
NDF = Night-Day Factors
```

注意：

- Night，并不是指“夜晚”，而是指夜间最小流量时的1个小时。
- Day，并不是指“白天”，而是指包含24小时的一整天。

因此，夜日因子（Night to Day Factor）是想通过“1小时”来推衍“24个小时”的一个理想参数。

## 概览

```text
压力 ---> 夜日因子 ---> 背景漏损水量
```

{:refdef: style="text-align: center;"}
![](/assets/image/dma/how-to-understand-night-to-day-factor.png)
{: refdef}

## 如何计算夜日因子NDF

**Night-Day Factors** (NDF's) relate **minimum leak flow rates at night** to **daily leakage**
for different pressure management scenarios,
and are essential parameters for understanding and interpreting leakage based on night flow measurements.

```text
Night-Day Factor: minimum leak flow rates at night ---> daily leakage
```

任何DMA的NDF都可以通过记录24h内AZP处（平均区域压力点）进行计算。

```text
AZP = Average Zone Pressure
```

The premise of **minimum nightly flow calculations** is that
you filter out what happens in your system just **in the middle of the night**
when **usage is at a minimum** and **leakage is at a peak**.
Background leakage is generally influenced by zonal pressures following an orifice flow relationship.
In many systems the pressure is higher overnight
while head loss is minimal and tanks fill up; this coincides with higher leakage.

{:refdef: style="text-align: center;"}
![](/assets/image/dma/minimum-nightly-flow.png)
{: refdef}

```text
Zonal Water Usage --> Average Zone Pressure --> Background Leakage

Minimum Nightly Flow = Background Leakage + Nightly Usage
```

The day-night factor is calculated as:

<p>
\[
F_{DN} = \frac{1}{24} \sum_{i}^{24}(\frac{P_{i}}{P_{night}})^{N1}
\]
</p>

Where:

<ul>
<li>\(P_{i}\) = Pressure at hour \(i\)</li>
<li>\(P_{night}\) = Average pressure at night</li>
<li>\(N_{1}\) = Orifice exponent for system leakage</li>
</ul>

## 日漏水量

> 此处参考[链接][link02]

In order to obtain the **daily water loss** in the studied area,
**the ratio of district night and day pressures** should be considered
when calculating the **Night to Day Factor (NDF)**.

```text
要点：

the ratio of district night and day pressures ---> Night to Day Factor (NDF) ---> daily water loss (日漏水量)

由“压力”计算“夜日因子”，再由“夜日因子”计算“日漏水量”。
```

The pressure profile in the **Average Zone Point (AZP)** should be measured,
and **the leakage exponent of the system (N)**,
should be determined for calculating the **NDF**.

```text
要点：

要求解NDF，需要确定AZP和N两个参数
```

<p>
The amount of <b>daily water loss</b>, \(Q_{loss,d}\), can be acquired using these two equations:
</p>

<p>
\[
\begin{align}
Q_{loss,d} &= NDF \times Q_{loss} \\
NDF &= \sum^{23}_{i=0}(\frac{P_{i}}{P_{MNF}})^{N}
\end{align}
\]
</p>

<ul>
    <li>\(Q_{loss,d}\) indicates the daily water loss in \(m^{3}/day\)</li>
    <li>\(Q_{loss}\) is the mean nighttime consumption in \(m^{3}/hr\)</li>
    <li>\(P_{i}\) is the 24-hour mean pressure</li>
    <li>\(P_{MNF}\) shows the mean pressure during the minimum nighttime consumption condition.</li>
</ul>

## 扩展

### N的取值范围

> 参考自《分区定量管理理论与实践》（第二版）第36页

<p>
经过广泛实验和现场验证，不同的DMA中FAVAD指数\(N_{1}\)的值在\(0.5\)和\(1.5\)之间。
</p>


这是因为在背景泄漏中，

<ul>
    <li>可检测（有报告的、无报告的）<b>非金属管道</b>的\(N_{1}\)接近\(1.5\)，对压力的变化十分敏感。</li>
    <li>可检测（有报告的、无报告的）<b>金属管道</b>的\(N_{1}\)接近\(0.5\)，对压力不太敏感。</li>
</ul>

### N的经验取值

> 参考自《分区定量管理理论与实践》（第二版）第36页

<p>
在对夜间流量组成进行详细分析时，必须考虑不同的泄漏类型有不同的\(N_{1}\)值。
</p>

由AZP压力数据计算NDF，可以使用一个比较简单的实用方法：

{:refdef: style="text-align: center;"}
![](/assets/image/dma/ndf-favad-n1-ili.png)
{: refdef}

第一步，估计DMA中泄漏的程度，分为1（最低）~10（很高）级，这样就可以粗略估计泄漏指数（ILI），这个值一般主观性较强，假定估值是5。

```text
笔记：第一步，为ILI选取一个值
```

第二步，估计金属管道实际可检测漏损的百分数。最粗略的估计是金属管道占管道总长的百分数。假定为60%。

```text
笔记：第二步，为p选定一个值。
```

<p>
第三步，在x轴上读出5，直到碰上60%的曲线，然后从交叉点读出y轴的值来估算\(N_{1}\)的值，大约是\(1.1\)。
</p>

```text
笔记：第三步，读取N1的值。
```

### 不断变化的NDF

> 参考自《分区定量管理理论与实践》（第二版）第36页

由于AZP处的24小时压力分布每天、每周会发生变化，而且每个季度也会变化，所以相应的NDF会跟着变化。

## Reference

- [How to Estimate Leakage using Minimum Nightly Flow][link01]

[link01]: https://help.innovyze.com/display/info360/How+to+Estimate+Leakage+using+Minimum+Nightly+Flow
[link02]: https://iwaponline.com/ws/article/20/6/2296/75114/Leakage-estimation-in-water-networks-based-on-the
