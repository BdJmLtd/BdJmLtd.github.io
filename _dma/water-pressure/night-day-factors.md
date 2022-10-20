---
title: "夜日因子 NDF (Night-Day Factors)"
sequence: 112
---

```text
NDF = Night-Day Factors
```

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

## Reference

- [How to Estimate Leakage using Minimum Nightly Flow](https://help.innovyze.com/display/info360/How+to+Estimate+Leakage+using+Minimum+Nightly+Flow)
