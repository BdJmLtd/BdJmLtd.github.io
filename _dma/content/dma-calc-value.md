---
title: "计算值"
sequence: 118
---

{:refdef: style="text-align: center;"}
![](/assets/image/dma/water-loss-vs-real-loss.png)
{: refdef}

{:refdef: style="text-align: center;"}
![](/assets/image/dma/standard-iwa-water-balance.png)
{: refdef}

## 漏失率

漏失水量，是管网漏水量（物理漏水量），包括

- 输水管及干管漏水量 （管网的输水过程）
- 水池/水塔等渗漏及溢流 （管网中的储水容器）
- 进户管漏失量 （从管网到用户）

管网漏失率（中文）：

<p>
\[
漏失率 = \frac{漏失水量}{供水量} \times 100 \%
\]
</p>

管网漏失率（英文）：

<p>
\[
R_{RL} = \frac{Q_{r1} + Q_{r2} + Q_{r3} + Q_{r4}}{Q_{s}} \times 100 \%
\]
</p>

其中，

<ul>
    <li>\(R_{RL}\)表示管网漏失率（\(\%\)）。R表示Rate，RL表示Real Loss</li>
    <li>\(Q_{r1}\)表示明漏水量（\(万m^{3}\)）</li>
    <li>\(Q_{r2}\)表示暗漏水量（\(万m^{3}\)）</li>
    <li>\(Q_{r3}\)表示背景漏失水量（\(万m^{3}\)）</li>
    <li>\(Q_{r4}\)表示水箱、水池的渗漏和溢流水量（\(万m^{3}\)）</li>
</ul>

## 漏损率

管网漏损率（中文）：

<p>
\[
漏损率 = \frac{漏损水量}{供水量} \times 100 \%
\]
</p>

管网漏损率（英文）：

<p>
\[
R_{WL} = \frac{Q_{s}-Q_{a}}{Q_{s}} \times 100 \%
\]
</p>

其中，

<ul>
    <li>\(R_{WL}\)表示管网漏损率（\(\%\)）。R表示Rate，WL表示Water Loss</li>
    <li>\(Q_{s}\)表示供水总量（\(万m^{3}\)）</li>
    <li>\(Q_{a}\)表示注册用水量（\(万m^{3}\)），其中a表示authorized</li>
</ul>

## 产销差率

<p>
\[
产销差率 = \frac{供水量 - 售水量}{供水量} \times 100 \%
\]
</p>

## 单位管长漏水量

<p>
\[
单位管长漏水量 = \frac{漏水量}{配水管长} \times 100 \%
\]
</p>

## 计量水率

<p>
\[
计量水率 = \frac{年供水量 - 年售水量}{年供水量} \times 100 \%
\]
</p>

## 泄漏量与压力

基本上，**泄漏量**与**压力**之间关系最简单、最可靠的表达形式是：

<p>
\[
L_{1} = L_{0}(P_{1}/P_{0})^{N_{1}}
\]
</p>

<p>
其中，\(P_{0}\)和\(L_{0}\)分别表示管网上初始压力和泄漏流量，
\(P_{1}\)和\(L_{1}\)是改变压力后的相应数值。
\(N_{1}\)对于各个DMA来说，一般介于0.5~1.5之间，取决于主要泄漏类型以及管材的软硬。
</p>

<p>
对于由混合管材组成的大系统，\(N_{1}\)的平均值通常假定取1，意味着泄漏与压力之间是线性关系。
</p>

```text
P = Pressure
L = Leak
```

## 日泄漏量

<p>
\[
日泄漏量 = NDF \times 夜间每小时泄漏量 \%
\]
</p>

<p>
其中，\(NDF\)表示为\(h/d\)，因此每天节约的量是\([L_{1} - L_{0}(P_{1}/P_{0})] \times NDF\)
</p>

<p>
对于重力供水的DMA，\(NDF\)一般小于等于\(24h/d\)，对于有大的摩擦压头损失的低压重力供水系统，
\(NDF\)可能会低至\(12h/d\)。
</p>

<p>
对于直接压力供水或有加压设备（基于时间或流量）的DMA，\(NDF\)一般高于\(24h/d\)，也可能高达\(36h/d\)。
</p>

## ILI

<p>
\[
ILI = \frac{CARL}{UARL} \times 100 \%
\]
</p>

- ILI: Infrastructure Leakage Index 基础设施泄漏指数
- CARL: Current Annual Real Losses 年总实际损失水量
- UARL: Unavoidable Annual Real Losses 不可避免的年度实际损失

