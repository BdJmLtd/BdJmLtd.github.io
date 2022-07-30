---
title:  "EPANET: 管段的粗糙系数"
sequence: 007
---

Roughness Coefficient

## 全新管材

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

## 随时间变化

**Be aware that a pipe's roughness coefficient can change considerably with age.**


<div class="w3-panel w3-yellow w3-topbar w3-bottombar w3-border-amber">
    <p>注意：pipe的roughness coefficient随时间而发生比较大的变化</p>
</div>
