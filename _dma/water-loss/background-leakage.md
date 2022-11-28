---
title: "背景泄漏计算 (Background Leakage)"
sequence: 105
---

当泄漏水平得到控制后，进一步减少漏水就变得越来越困难。
在这种情况下，有必要对每一个泄漏组成进行更详细的评估。

## BABE

背景漏水与爆管漏水量估计法（BABE，Background and Bursts Estimates）用来提高最小流量分析的可信度。
BABE方法，不仅可以对不同大小、不同压力、混合基础结构的DMA作比较，
还能定量无法避免的泄漏，确定实际可以避免的漏水损失（过量损失）。

```text
笔记：BABE很优秀

可以避免的漏水损失 = 过量损失
```

## 过量损失

DMA中的**过量损失**由**暗漏**造成。

```text
笔记：由“暗漏”导致了“过量损失”。
```

为了计算过量损失，夜间最小流量的其他组成必须测量或估算。

虽然BABE方法需要大量数据，但是刚开始使用时，可通过设定初始值来简化，直到积累了更准确的数据。

DMA过量漏水分析：

{:refdef: style="text-align: center;"}
![](/assets/image/dma/avoidable-water-loss.png)
{: refdef}

典型用户水管构造：

{:refdef: style="text-align: center;"}
![](/assets/image/dma/typical-domestic-user-pipeline-structure.png)
{: refdef}

## 背景泄漏

### 收集数据

DMA的背景泄漏水平可以用下面的数值估算：

- 主管道长度
- DMA夜间压力平均值 AZNP
- 连接用户数
- 私有管道长度

### 第一个版本

2004年，国际水协公布了计算背景泄漏水平的公式，在设备状况良好的情况下，平均压力为50m的情况下，该公式表示为：

<p>
\[
\begin{align}
背景泄漏量(L/h) = & 0.02 \times 主管道长度(m) + 1.25 \times 连接用户数 + \\
                & 0.033 \times 私有管道长度(m) + \\
                & 0.25 \times 居民住宅数与非居民住宅数总和
\end{align}
\]
</p>

### 第二个版本

下面等式给出了一个更加简单的计算方法：

<p>
\[
\begin{align}
背景泄漏量 = & ICF \times (0.02 \times 主管道长度 + 1.25 \times 连接用户数) + \\
           & ICF \times 0.033 \times 私有管道长度 + \\
           & 0.25 \times 居民住宅数与非居民住宅数总和
\end{align}
\]
</p>


其中，ICF为基础设施的状况因子，它用来表示主管道的好坏程度。
一般情况下，它的取值范围为1到4之间，其中1表示状况很好，4表示状况很差。

在英国，ICF一般取值为2。

### 第三个版本

从更深层次考虑，以**地区平均夜间压力**为基础对公式进行修正。
修正因子，在国际上，一般取值为1.5。

这样，DMA的背景泄漏水平损失可以用下面的公式进行计算：

<p>
\[
\begin{align}
背景泄漏量 = & ICF \times (0.02 \times 主管道长度 + 1.25 \times 连接用户数) + \\
           & ICF \times 0.033 \times 私有管道长度 \times (AZNP / 50)^{1.5} + \\
           & 0.25 \times 居民住宅数与非居民住宅数总和 \times (AZNP / 50)^{1.5}
\end{align}
\]
</p>

