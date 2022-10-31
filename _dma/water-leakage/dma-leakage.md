---
title: "泄漏组成"
sequence: 101
---

{:refdef: style="text-align: center;"}
![](/assets/image/dma/dma-leakage.png)
{: refdef}

## 漏损原因

Generally, leakage in the WDNs (Water Distribution Networks) occurs due to the low quality of materials in pipes
or other network components, errors in design, inappropriate maintenance,
high pressure in the network, and pipe break and bursts.

## 分类

泄漏主要有两部分组成：

- 泄漏
  - 背景泄漏 Background Leakage（检测不到，通过视觉和声学的方法检测不到）
  - 破损泄漏（检测的到）
    - 明漏 Reported Leakage
    - 暗漏 Unreported Leakage

{:refdef: style="text-align: center;"}
![](/assets/image/dma/types-of-real-losses.png)
{: refdef}

## 背景泄漏

背景泄漏，是所有泄漏源的集合，其中每一个泄漏源都很小，视觉和声觉的方法都检测不到。

**Background leakage** is generally defined as the leakage below the level of detection (with current technology).

<p>
背景泄漏，是指在压力\(0.5MPa\)时，流量小于\(0.25m^{3}/h\)，它代表现代检测技术实际可检测到的最小值。
</p>

压力管理，对这一部分泄漏有重大影响。

## 破损泄漏

破损泄漏，是供水管网破裂造成的漏水，又可分为明漏和暗漏。

```text
破损泄漏 = 明漏 + 暗漏
```

### 明漏

**明漏**是指相关人员向管理部门报告的漏水，发现此类漏水的一般是用户或公众。

### 暗漏

**暗漏**，是指如果不进行检测就一直持续的漏水。

### 明漏 vs. 暗漏

明漏，一般能看到，而每年水损失的最大部分是来自于暗漏，因为漏水的时间长。

## 泄漏量

### 公式

总的泄漏量，受**识别**、**破损定位**、和**修复速度**的影响，因此控制漏水时间就可以减少漏水量。

<p>
\[
破损泄漏总量 = 破损瞬时流量 \times 破损持续时间
\]
</p>

### 漏水时间

应用DMA，可以极大地缩短发现漏水的时间和区域，实现漏点快速定位，以提高供水效益。

{:refdef: style="text-align: center;"}
![](/assets/image/dma/leak-run-time-awareness.png)
{: refdef}

总的漏水时间，可以划分为三个区间，分别称为**发现**、**定位**和**修复**。

- 发现时间：从漏水发生到水管理部门获知有漏水发生之间的时间。
- 定位时间：精准定位漏水点所需的时间。
- 修复时间：在漏水点被精准定位后，修复所用的时间，包括策划以及依法向公路管理部门发送通告。

总漏水量 = 单位时间泄漏量 X 漏水发生的时长

## 漏损控制：主动和被动

The methods of leakage reduction include **passive control**,
like repairing the daily pipe breaks and bursts,
and **active control of leaks**,
such as the detection of the leakage exact location, repairing it,
replacing the damaged pipelines, and pressure management.

```text
- passive control
  - repairing the daily pipe breaks and bursts
- active control
  - the detection of the leakage exact location
  - repairing it
  - replacing the damaged pipelines
  - pressure management
```
