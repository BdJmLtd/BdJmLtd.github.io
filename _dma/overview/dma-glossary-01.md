---
title: "术语表-01"
sequence: 112
---

## 城镇供水术语

> 参考来源：《城镇供水管网漏损控制及评定标准》CJJ92-2016 第2页 术语

### 第一批概念

- 供水管网（water distribution system）：连接水厂和用户水表（含）之间的管道及其附属设施的总称。

### 第二批概念

- 供水总量（system input quantity）进入供水管网中的全部水量之和，包括自产供水量和外购供水量。
  - 注册用户用水量（authorized consumption）：在供水单位登记注册的用户的计费用水量和免费用水量。
    - 计费用水量（billed authorized consumption）：在供水单位注册的计费用户的用水量。
    - 免费用水量（unbilled authorized consumption）：按规定减免收费的注册用户的用水量和用于管网维护和冲洗等的水量。
  - 漏损水量（water losses）：供水总量和注册用户用水量之间的差值。由漏失水量、计量损失水量和其他损失水量组成。
    - 漏失水量（real loss）：各种类型的管线漏点、管网中水箱及水池等渗漏和溢流造成实际漏掉的水量。
      - 明漏水量（reported leakage）：水溢出地面或可见的管网漏点的漏失水量。
      - 暗漏水量（unreported leakage）：在地面以下检测到的管网漏点的漏失水量。
      - 背景漏失水量（background leakage）：现有技术手段和措施未能检测到的管网漏点的漏失水量。
    - 计量损失水量（metering losses）：计量表具性能限制或计量方式改变导致计量误差的损失水量。
    - 其他损失水量（other losses）：未注册用户用水和用户拒查等管理因素导致的损失水量。

```text
小总结：
漏失水量，是物理漏失，是真实的管线、水箱、水池渗漏和溢流造成的，是管网自身的因素；
计量损失水量，是由于计量表（水表、流量计）的误差造成的，是管网自身之外的附属因素；
其他损失水量，是人的因素。
```

{:refdef: style="text-align: center;"}
![水量平衡表](/assets/image/dma/water-balance-table-jm.png)
{: refdef}

进一步出现各种指标：

- 漏失率（real loss rate）：管网**漏失水量**与**供水总量**之比，通用用百分比表示。
- 漏损率（water loss rate）：管网**漏损水量**与**供水总量**之比，通常用百分比表示。
- 基本漏损率（benchmark water loss rate）：漏损率评定标准修正前的基准控制值。
- 单位供水量管长（pipe length per unit water supply）：管径大于等于75mm的管道总长与供水总量之比。
- 水表量程比（turndown rate）：水表常用流量和最小流量的比值。

### 第三批概念

- 区域管理（zone management）：将供水管网划分为若干供水区域，对每个供水区域的水量、水压进行监测控制，实现漏损量化管理的方式。
- 独立计量区（district metered area）：将供水管网分割成单独计量的供水区域，规模一般小于区域管理的范围。
- 压力管理（pressure management）：在满足用户用水需求的前提下，根据管理需要对供水管网运行压力进行调控。

> 没有理解：区域管理和独立计量区，它们的区别在哪里？独立计量区的规模比较小，那怎么区分大小呢？多大算大，多小算小呢？

### 第四批概念

- 夜间最小流量（minimum night flow）：**独立计量区**每日夜间用户用水量最小时的进水流量。
- 零压测试（zero-pressure test）：为判断**独立计量区**是否封闭，关闭边界阀门后放水，监测区域内压力是否下降至零。

This is a test that checks whether a particular area in a water system is watertight.
The valves around the area are closed and the pressure monitored -
if there is zero water pressure through the area,
it means the boundaries of that area are watertight.

## 水量计量仪表

> 内容参考来源：[流量计量名词术语及定义](https://www.doc88.com/p-9959655870639.html)

### 第一组

- 供水单位（water supply enterprise）：向客户提供生活饮用水服务的城镇公共供水单位和自建设施单位（包括自来水公司和水厂等）
- 用水单位（water use customer）：接受供水服务的客户
- 机械式水表（mechanical type water meter）：速度式水表和容积式水表的统称。
- 带电子装置水表（water meter equipped with electronic devices）：装备了电子装置以实现预定功能的水表。
  - 带电子装置水表，包括配备了电子装置的机械式水表、基于电磁或电子原理工作的水表。
  - 电子装置，包括流量信息转换和处理单元，并可附加贮存记忆装置、预置装置、价格显示装置等。
- 复式水表（combination meter）：有一个大流量水表、一个小流量水表和一个转换装置组成的一种管道式水表。
  - 转换装置根据流经水表的流量大小自动引导水流流过小流量水表或者大流量水表，或者同时流过两个水表。
  - 注：水表的读数，有两个独立的积算器给出，或者由一个积算器将两个水表上的数值相加后给出。

### 第二组

- 水表配备率（the equipping rate of water meter）：实配水表台数与应配水表台数之比。
- 水表检测率（the detection rate of water meter）：实测水表总台数与应测水表总台数之比。
- 

### 第三组

<ul>
  <li>过载流量（overload flowrate）\(Q_{4}\)：要求水表在短时间内能符合最大允许误差要求，随后在额定工作条件下仍能保持计量特性的最大流量。</li>
  <li>常用流量（permanent flowrate）\(Q_{3}\)：额定工作条件下的最大流量。在此流量下，水表应正常工作并符合最大允许误差要求。</li>
  <li>分界流量（transitional flowrate）\(Q_{2}\)：出现在常用流量\(Q_{3}\)和最小流量\(Q_{1}\)之间、将流量范围划分成各有特定最大允许误差的“高区”和“低区”两个区的流量。</li>
  <li>最小流量（minimum flowrate）\(Q_{1}\)：要求水表的示值符合最大允许误差的最低流量。</li>
  <li>量程比（flow turndown）：常用流量\(Q_{3}\)和最小流量\(Q_{1}\)的比值。也可用字母\(R\)加数字表示，如\(R100\)表示\(Q_{3}/Q_{1}=100\)</li>
  <li>最大流量（maximum flowrate）\(Q_{5}\)：满足计量性能的最大流量。</li>
</ul>

> **overload flowrate** means the highest flowrate
> at which the relevant instrument operates for a short period of time without deteriorating

## 流量计量名词术语及定义

> 内容参考自：[流量计量名词术语及定义](https://www.doc88.com/p-9959655870639.html)

### 第一组

- 流量（flow rate）：流体流过一定截面的量称为流量。流量是**瞬时流量**和**累积流量**的统称。
  - 在一段时间内，流体流过一定截面的量称为**累积流量**，也称总量。
  - 当时间很短时，流体流过一定截面的量称为**瞬时流量**，在不会产生误解的情况下，**瞬时流量**也可简称**流量**。
  - 流量用体积表示时，称为**体积流量**；用质量表示时，称为**质量流量**。
- 最大流量（maximum flow-rate）：满足计量性能要求的最大流量。
- 最小流量（minimum flow-rate）：满足计量性能要求的最小流量。
- 流量范围（flow-rate range）：由最大流量和最小流量所限定的范围，在该范围内满足计量性能的要求。
- 分界流量（transitional flow-rate）：在最大流量和最小流量之间的流量值，它将流量范围分割成两个区，即“高区”和“低区”。
- 公称流量（nominal flow-rate）：在公称流量下，流量计应能在连续运行和间断运行时满足计量性能的要求。
  - 注：对水表，**公称流量**称为**常用流量**。

### 第二组

- 流量计（flow meter）：测量流量的器具。通常由一次装备和二次装置组成。
  - 注：准确度高、稳定性好，可作为其他流量计比对标准使用的流量计称为**标准流量计**。
- 一次装置（primary device）：产生流量信号的装置。根据所采用的原理，一次装置可以在管道内部或外部。
- 二次装置（secondary device）：接受来自一次装置的信号并显示、记录、转换和（或）传送该信号以得到流量值的装置。
- 压力损失（pressure loss）：由于管道中存在一次装置而产生的不可恢复的压力降。
- 工作条件（working conditions）：流经一次装置并符合一次装置规范的被测流体物理性质的特性值。
- 工作温度（working temperature）：流经一次装置并符合一次装置规范的被测流体的温度。
- 工作压力（working pressure）：流经一次装置并符合一次装置规范的被测流体的绝对静压。
- 安装条件（installation condition）：允许使用流量计（或流量测量装置）的物理环境。
  - 注：物理环境，包括外界条件、流体状态、流体的物理性质的数值范围、管路及其相应配件的几何配置。

### 第三组

- 紊流（turbulent flow）：与**粘性力**相比，**惯性力**起主要作用的流动，也称**湍流**。
  - 注：紊流，是时间和空间上不规则（随机）的速度波动叠加在平均流上的流动。
- 层流（laminar flow）：与**惯性力**相比，**粘性力**起主要作用的流动。
  - 注：层流，是流体的质点作分层运动，在流层之间不发生混杂的流动。
- 稳定流（steady flow）：速度、压力和温度基本不随时间变化，且不影响测量准确度的流动，也称定常流。
  - 注：观察到的稳定流实际上是其速度、压力和温度等量都会围绕着平均值有很小的变化，但不影响到测量的不确定度的流动。
- 不稳定流（unsteady flow）：速度、压力、密度和温度中的一个或多个参数随时间波动的流动，也称非定常流。
  - 注：所考虑的时间间隔应足够长，以便排除紊流本身的随机分量。
- 多相流（multiphase flow）：两种或两种以上不同相的流体一起流动。只有两相流体一起流动时，又称为两相流。
- 临界流（critical flow）：流体流经节流件喉部，下游与上游的绝对压力之比小于临界值的流动。临界流上游流体状态（压力、温度和速度分布）不变时，质量流量保持恒定。
- 速度分布（velocity distribution）：在管道横截面上流体速度轴向量的分布模式。

### 第四组 水表（water meters）

- “容积式”水表（“volumetric” water meter）：安装在封闭管道中，由一些被逐次充满和排放水的已知容积的容室和凭借流动驱动的机构组成的一种装置。
- “速度式”水表（“velocity” water meter）：安装在封闭管道中，由一个被水流速度驱动运转的一次装置组成的装置。运动元件的运动通过机械方式或其他方式传输给指示装置，积算出累积体积流量。
- 螺翼式水表（woltmann water meter）：仪表壳体内安置一个旋转轴与流动方向重合的螺旋翼片的装置。
- 单流束水表（single-jet water meter）；多流束水表（multi-jet water meter）：由围绕垂直于水流的轴线旋转的涡轮转子构成的一种水表。
  - 如果是单股流束冲击在转子边缘的某一处，则称之为单流束水表；
  - 如果是多股流束同时冲击在转子边缘的几个点处，则称之为多流束水表。

## NRW

- NRW = Non Revenue Water 产销差水量/无收益水量

- AZNP: Average Zone Night Pressure
- CARL: Current Annual Real Losses 年总实际损失水量
- ELL: economic level of leakage
- ICF：Infrastructure Condition Factor 基础设施的状况因子，用来表示主要输水管道的坏损程度。
  一般情况下，它的取值范围为1至4(1表示状况很好，4表示状况差)，常用的取值在0.5~2.0之间。
- ILI: Infrastructure Leakage Index 基础设施泄漏指数
- MNF: Minimum night flow
- UARL: Unavoidable Annual Real Losses 不可避免的年度实际损失

UARL is also used in the calculation of the Infrastructure Leakage Index (ILI):

```text
ILI = Current Annual Real Losses (CARL)/UARL
```

