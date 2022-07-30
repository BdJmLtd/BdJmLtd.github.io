---
title:  "EPANET: 水头损失"
sequence: 007
---

```text
粗糙系数         --->              阻力系数          ---> 水头损失
-----------------------------------------------------------------
Roughness Coefficient ---> Resistance Coefficient ---> Head Loss
-----------------------------------------------------------------
（凭经验得来的）                  三个不同的公式
```

这几个概念的关系：

- 首先，**粗糙系数**（Roughness Coefficient），是由人们的生活经验得来的，它是人们直接提供的数据。
- 其次，**阻力系数**（Resistance Coefficient），是在**粗糙系数**（Roughness Coefficient）的基础计算得到的，这就用到三个公式中的某一个。
  因此，**阻力系数**（Resistance Coefficient）是计算的值，而不是人们提供的值。
- 再者，**水头损失**（Head Loss），是在**阻力系数**（Resistance Coefficient）的基础上得来的。
- 最后，**局部水损**（Minor Loss），是为了增加**水头损失**（Head Loss）的精确度而添加的计算项。

## 水头损失公式

Head Loss Formula

### 三个公式

The hydraulic head lost by water flowing in a pipe due to friction with the pipe walls
can be computed using one of three different formulas:

- Hazen-Williams formula 海澄－威廉公式
- Darcy-Weisbach formula 达西-韦史巴赫公式
- Chezy-Manning formula 谢才-曼宁公式

<div class="w3-panel w3-pale-green w3-bottombar w3-border-green w3-border">
    <p>三个公式，选其一</p>
</div>

### 三个公式的特点

The **Hazen-Williams** formula is **the most commonly used headloss formula** in the US.
It cannot be used for liquids other than water and was
originally developed for turbulent flow only.

<div class="w3-panel w3-pale-green w3-bottombar w3-border-green w3-border">
    <p>Hazen-Williams，是最常用的，但是只适合于water</p>
</div>

The **Darcy-Weisbach formula** is the most theoretically correct.
It applies over all flow regimes and to all liquids.

<div class="w3-panel w3-pale-green w3-bottombar w3-border-green w3-border">
    <p>Darcy-Weisbach是理论上最正确的</p>
</div>

The **Chezy-Manning formula** is more commonly used for **open channel flow**.

<div class="w3-panel w3-pale-green w3-bottombar w3-border-green w3-border">
    <p>Chezy-Manning最适合于open channel flow。</p>
    <p>
明渠流（英语：open-channel flow）是水力学的分支，是液体在管道或水路中的流动，而且液体存在自由表面，包括未全满的液体在管道中流动，则称为管流。 
流体的重量是这种流体的主要驱动来源。
    </p>
</div>

## Head Loss

<p>
    Each formula uses the following equation to compute headloss
    between the start and end node of the pipe:
</p>
<p>
    \[h_{L} = A q^{B}\]
</p>
<p>
    where <span>\(h_{L}\)</span> = headloss (Length), <span>\(q\)</span> = flow rate (Volume/Time),
    <span>\(A\)</span> = resistance coefficient, and <span>\(B\)</span> = flow exponent.
</p>
<div class="w3-panel w3-yellow w3-topbar w3-bottombar w3-border-amber">
    <p>这个公式，应该来说，它是不“准确”的</p>
    <p>可以参考Fixed Demand Model当中的更“复杂”一点的公式，会发现两者不一样：</p>
    <p>
        \[h_{Lij} = r \: q_{ij} \: |q_{ij}|^{n-1} + m \: q_{ij} \: |q_{ij}|\]
    </p>
    <p>
        我猜测，这种不一致性，可能是文档编写者想让人更好的理解，也可能就是纯粹的没有维护好文档的一致性。
    </p>
</div>

### 阻力系数

Resistance Coefficient

<p>
    <a href="#table-pipe-headloss-formulas"><span>Table 3.1</span></a>
    lists expressions for the resistance coefficient and values for the flow
    exponent for each of the formulas.
</p>

<table>
    <caption>
        Pipe Headloss Formulas for Full Flow (for headloss in feet英尺 and flow rate in cfs 立方英尺每秒)
    </caption>
    <thead>
    <tr>
        <th>Formula</th>
        <th>
            Resistance  Coefficient(<span>\(A\)</span>)
        </th>
        <th>
            Flow Exponent(<span>\(B\)</span>)
        </th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>Hazen-Williams</td>
        <td><span>\(4.727\,C^{-1.852}\,d^{-4.871}\,L\)</span></td>
        <td><span>\(1.852\)</span></td>
    </tr>
    <tr>
        <td>Darcy-Weisbach</td>
        <td><span>\(0.0252\,f(\epsilon,d,q)\,d ^{-5}\,L\)</span></td>
        <td><span>\(2\)</span></td>
    </tr>
    <tr>
        <td>Chezy-Manning</td>
        <td><span>\(4.66\,n^{2}\,d^{-5.33}\,L\)</span></td>
        <td><span>\(2\)</span></td>
    </tr>
    </tbody>
</table>

> 因为用的英尺和立方英尺每秒的单位，因此这里的内容，准确来说，是不对的

<p>Notes:</p>
<ul>
    <li><span>\(C\)</span> = Hazen-Williams roughness coefficient</li>
    <li><span>\(\epsilon\)</span> = Darcy-Weisbach roughness coefficient (ft)</li>
    <li><span>\(f\)</span> = friction factor  (dependent on <span>\(\epsilon\)</span>, <span>\(d\)</span>, and <span>\(q\)</span>)</li>
    <li><span>\(n\)</span> = Manning roughness coefficient</li>
    <li><span>\(d\)</span> = pipe diameter (ft)</li>
    <li><span>\(L\)</span> = pipe length (ft)</li>
    <li><span>\(q\)</span> = flow rate (cfs)</li>
</ul>

<p>
    <strong>Each formula uses a different pipe roughness coefficient that must be determined empirically.</strong>
</p>
<div class="w3-panel w3-pale-green w3-bottombar w3-border-green w3-border">
    <p>对于pipe来说，它的roughness coefficient是凭借经验来估算的值。</p>
</div>

<p>
    With the Darcy-Weisbach formula EPANET uses different methods to
    compute the friction factor <span>\(f\)</span> depending on the flow regime:
</p>
<ul>
    <li>The Hagen–Poiseuille formula is used for <b>laminar flow</b> (Re &lt; 2,000).</li>
    <li>
        The Swamee and Jain approximation to the Colebrook-White equation is
        used for <b>fully turbulent flow</b> (Re &gt; 4,000).
    </li>
    <li>
        A cubic interpolation from the Moody Diagram is used for
        <b>transitional flow</b> (2,000 &lt; Re &lt; 4,000).
    </li>
</ul>
<div class="w3-panel w3-pale-green w3-bottombar w3-border-green w3-border">
    <p>根据雷诺数（Reynolds number）数值不同，Darcy-Weisbach公式采用不同的计算方法：</p>
    <ul>
        <li>如果Re &lt; 2,000，表示“层流”（laminar flow），使用Hagen–Poiseuille公式</li>
        <li>如果2,000 &lt; Re &lt; 4,000，表示“过渡（状态）流”（transitional flow），使用Moody图的cubic内插值方式</li>
        <li>如果Re &gt; 4,000，表示“完全紊流”（fully turbulent flow），使用Colebrook-White公式的Swamee-Jain近似</li>
    </ul>
</div>

### 粗糙系数

Roughness Coefficient

<p>
    <a href="#table-roughness-coeff"><span>Table 3.2</span></a>
    lists general ranges of these coefficients for different types of new pipe materials.
</p>

<table>
    <caption>
        Roughness Coefficients for New Pipe
    </caption>
    <thead>
    <tr>
        <th class="w3-center">Material</th>
        <th class="w3-center">
            Hazen-Williams<br/>
            <span>\(C\)</span><br/>
            (unitless)
        </th>
        <th class="w3-center">
            Darcy-Weisbach<br/>
            <span>\(\epsilon\)</span><br/>
            (ft x <span>\(10^{-3}\)</span>)
        </th>
        <th class="w3-center">
            Manning's<br/>
            <span>\(n\)</span><br/>
            (unitless)
        </th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td class="w3-center">Cast Iron<br/>（铸铁管）</td>
        <td>130 – 140</td>
        <td>0.85</td>
        <td>0.012 – 0.015</td>
    </tr>
    <tr>
        <td class="w3-center">Concrete or Concrete Lined<br/>（混凝土管或者混凝土衬里）</td>
        <td>120 – 140</td>
        <td>1.0 – 10</td>
        <td>0.012 – 0.017</td>
    </tr>
    <tr>
        <td class="w3-center">Galvanized Iron<br/>（镀锌铁管）</td>
        <td>120</td>
        <td>0.5</td>
        <td>0.015 – 0.017</td>
    </tr>
    <tr>
        <td class="w3-center">Plastic<br/>（塑料管）</td>
        <td>140 – 150</td>
        <td>0.005</td>
        <td>0.011 – 0.015</td>
    </tr>
    <tr>
        <td class="w3-center">Steel<br/>（钢管）</td>
        <td>140 – 150</td>
        <td>0.15</td>
        <td>0.015 – 0.017</td>
    </tr>
    <tr>
        <td class="w3-center">Vitrified Clay<br/>（陶土管）</td>
        <td>110</td>
        <td>&#160;</td>
        <td>0.013 – 0.015</td>
    </tr>
    </tbody>
</table>


**Be aware that a pipe's roughness coefficient can change considerably with age.**


<div class="w3-panel w3-yellow w3-topbar w3-bottombar w3-border-amber">
    <p>注意：pipe的roughness coefficient随时间而发生比较大的变化</p>
</div>

## Minor Losses

Minor head losses (also called local losses) are caused by the added turbulence
that occurs at bends and fittings.

<div class="w3-panel w3-pale-green w3-bottombar w3-border-green w3-border">
    <p>minor head loss就是考虑了added turbulence</p>
</div>

The importance of including such losses depends on the layout of the network and
the degree of accuracy required.

<div class="w3-panel w3-pale-green w3-bottombar w3-border-green w3-border">
    <p>其重要性与network layout和accuracy degree有关系</p>
</div>

They can be accounted for by assigning the pipe a minor loss coefficient.

<div class="w3-panel w3-pale-green w3-bottombar w3-border-green w3-border">
    <p>这个minor loss coefficient参数可以依附于pipe上</p>
</div>
<p>
    The minor headloss becomes the product of this coefficient and the velocity head of the pipe, i.e.,
</p>
<div>
    \[h_L = K (\frac{v^2}{2g})\]
</div>
<p>
    where <span>\(K\)</span> = minor loss coefficient,<br/>
    <span>\(v\)</span> = flow velocity (Length/Time),<br/>
    and <span>\(g\)</span> = acceleration of gravity (Length/Time <sup>2</sup>).
</p>

<p>
    <a href="#table-minor-loss-coeff"><span>Table 3.3</span></a>
    provides minor loss coefficients for several types of fittings.
</p>

<table>
    <caption>
        Minor Loss Coefficients for Selected Fittings
    </caption>
    <thead>
    <tr>
        <th>FITTING</th>
        <th>LOSS COEFFICIENT</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>Globe valve, fully open</td>
        <td>10.0</td>
    </tr>
    <tr>
        <td>Angle valve, fully open</td>
        <td>5.0</td>
    </tr>
    <tr>
        <td>Swing check valve, fully open</td>
        <td>2.5</td>
    </tr>
    <tr>
        <td>Gate valve, fully open</td>
        <td>0.2</td>
    </tr>
    <tr>
        <td>Short-radius elbow</td>
        <td>0.9</td>
    </tr>
    <tr>
        <td>Medium-radius elbow</td>
        <td>0.8</td>
    </tr>
    <tr>
        <td>Long-radius elbow</td>
        <td>0.6</td>
    </tr>
    <tr>
        <td>45 degree elbow</td>
        <td>0.4</td>
    </tr>
    <tr>
        <td>Closed return bend</td>
        <td>2.2</td>
    </tr>
    <tr>
        <td>Standard tee - flow through run</td>
        <td>0.6</td>
    </tr>
    <tr>
        <td>Standard tee - flow through branch</td>
        <td>1.8</td>
    </tr>
    <tr>
        <td>Square entrance</td>
        <td>0.5</td>
    </tr>
    <tr>
        <td>Exit</td>
        <td>1.0</td>
    </tr>
    </tbody>
</table>


