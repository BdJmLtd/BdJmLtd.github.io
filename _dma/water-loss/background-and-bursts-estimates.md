---
title: "背景漏水与爆管漏水量估计法 BABE (Background and Bursts Estimates)"
sequence: 102
---

In the 1990s, the development of a model for recognizing **the components of real water loss**
was considered necessary by the UK Leakage Control Initiative.
This method, which was introduced as the **Background and Bursts Estimates (BABE)** method,

The BABE method recognized and estimated the **real water loss** as leakage in the background, burst, reported overflows
and leaks at the reservoirs, unreported bursts, overflows at the customers' private tanks,
main lines, distribution, connections, and internal network lines of customers.

- real water loss
    - leakage in the background
    - burst
        - reported overflows
        - unreported bursts
    - leaks at the reservoirs
    - overflows at the customers' private tanks
    - main lines, distribution, connections, and internal network lines of customers

<p>
In the UK, <b>background leakage</b> is defined as the sum of all leakages
with lower flow rates than \(0.5 m^{3}/h\) in the pressure of 50 meters;
otherwise, they are considered as <b>bursts</b>.
</p>


## 参数

In the **BABE** method, two parameters including **infrastructure condition** and **leakage exponent** will be examined.

```text
BABE ---> infrastructure condition + leakage exponent
```

Also, in the **MNF** technique, the influence of **LNC (Legitimate Night-time Consumption)** of the customers and
the **leakage exponent** on the obtained results will be evaluated and compared.

```text
MNF ---> LNC + leakage exponent
```

## Reference

- [Leakage estimation in water networks based on the BABE and MNF analyses: a case study in Gavankola village, Iran][iwaponline]
- [水损专栏 - BABE (Background & Burst Estimates) 分析法](118-china.com/ngxyy/viewnews.html?hospitalNewsId=6a7f06f8-62f0-4730-bb2c-54d25876c604)

[iwaponline]: https://iwaponline.com/ws/article/20/6/2296/75114/Leakage-estimation-in-water-networks-based-on-the
