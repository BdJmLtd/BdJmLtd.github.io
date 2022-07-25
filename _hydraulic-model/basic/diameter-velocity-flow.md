---
title:  "管径、流速、流量"
sequence: 002
---

## 公式

公式：

<p>
\[\begin{align}
流量 &= 横截面积 \times 流速\\
    &= \pi \times {半径}^{2} \times 流速\\ 
    &= \pi \times (\frac{直径}{2})^{2} \times 流速 \\
\end{align}\]
</p>

计量单位：

<ul>
    <li>圆周率（\(\pi\)）：3.1415926</li>
    <li>管径单位：毫米（\(mm\)）。注意：需要除以1000，转换成米（\(m\)）</li>
    <li>流速单位：米每秒（\(m/s\)）</li>
    <li>流量单位：立方米每小时（\(m^{3}/h\)）。注意：单位是1小时（\(h\)），需要乘以3600</li>
</ul>

## 示例

例如，管径是200\(mm\)，流速是3\(m/s\)，那么流量：

<p>
\[\begin{align}
每秒流量 &= \pi \times (\frac{200mm/1000}{2})^{2} \times 3m/s \\
           &= \pi \times (\frac{0.2m}{2})^{2} \times 3m/s \\
           &= \pi \times (0.1m)^{2} \times 3m/s \\
           &= \pi \times 0.01m^{2} \times 3m/s \\
           &= (\pi \times 0.01 \times 3) m^{3}/s \\
           &= (3.1415926 \times 0.01 \times 3) m^{3}/s \\
           &= 0.094247778 m^{3}/s \\
\end{align}\]
</p>

<p>
\[\begin{align}
每小时流量 &= 每秒流量 \times 3600 \\
           &= 0.094247778 m^{3}/s \times 3600 \\
           &= 339.2920008 m^{3}/h
\end{align}\]
</p>

## 计算

<form>
<table>
<thead>
</thead>
<tr>
    <td>圆周率（\(\pi\)）</td>
    <td>3.1415926</td>
</tr>
<tr>
    <td><label for="pipe-diameter">管径：</label></td>
    <td><input id="pipe-diameter" type="text" value="200"/>\(mm\)</td>
</tr>
<tr>
    <td><label for="pipe-velocity">流速：</label></td>
    <td><input id="pipe-velocity" type="text" value="3"/>\(m/s\)</td>
</tr>
<tr>
    <td><label for="pipe-flow">流量：</label></td>
    <td><input id="pipe-flow" type="text" disabled="disabled"/>\(m^{3}/h\)</td>
</tr>
<tr>
    <td class="w3-center" colspan="2">
        <input type="button" value="计算" onclick="calculateFlow()"/>
        <input type="reset" value="重置"/>
    </td>
</tr>
</table>
</form>

<script>
    function calculateFlow() {
        const diameter = $('#pipe-diameter').val();
        const velocity = $('#pipe-velocity').val();
        const pi = 3.1415926;
        const radius = diameter / 1000 / 2;
        const area = pi * radius * radius;
        const flow = area * velocity * 3600;
        const value = flow.toFixed(7);
        $('#pipe-flow').val(value);
    }
</script>

## 管径流速推荐安全值

```text
下面的表格来自《计算管径、压力、流速、流量表格.xls》文件
```

<table>
<thead>
<tr>
    <th class="w3-center">管径（\(mm\)）</th>
    <th class="w3-center">闭式系统<br/>流速（\(m/s\)）</th>
    <th class="w3-center">开式系统<br/>流速（\(m/s\)）</th>
</tr>
</thead>
<tbody>
<tr>
    <td class="w3-center">20</td>
    <td class="w3-center">0.5-0.6</td>
    <td class="w3-center">0.4-0.5</td>
</tr>
<tr>
    <td class="w3-center">25</td>
    <td class="w3-center">0.6-0.7</td>
    <td class="w3-center">0.5-0.6</td>
</tr>
<tr>
    <td class="w3-center">32</td>
    <td class="w3-center">0.7-0.9</td>
    <td class="w3-center">0.6-0.8</td>
</tr>
<tr>
    <td class="w3-center">40</td>
    <td class="w3-center">0.8-1</td>
    <td class="w3-center">0.7-0.9</td>
</tr>
<tr>
    <td class="w3-center">50</td>
    <td class="w3-center">0.9-1.2</td>
    <td class="w3-center">0.8-1.0</td>
</tr>
<tr>
    <td class="w3-center">65</td>
    <td class="w3-center">1.1-1.4</td>
    <td class="w3-center">0.9-1.2</td>
</tr>
<tr>
    <td class="w3-center">80</td>
    <td class="w3-center">1.2-1.6</td>
    <td class="w3-center">1.1-1.4</td>
</tr>
<tr>
    <td class="w3-center">100</td>
    <td class="w3-center">1.3-1.8</td>
    <td class="w3-center">1.2-1.6</td>
</tr>
<tr>
    <td class="w3-center">125</td>
    <td class="w3-center">1.5-2.0</td>
    <td class="w3-center">1.4-1.8</td>
</tr>
<tr>
    <td class="w3-center">150</td>
    <td class="w3-center">1.6-2.2</td>
    <td class="w3-center">1.5-2.0</td>
</tr>
<tr>
    <td class="w3-center">200</td>
    <td class="w3-center">1.8-2.5</td>
    <td class="w3-center">1.6-2.3</td>
</tr>
<tr>
    <td class="w3-center">250</td>
    <td class="w3-center">1.8-2.6</td>
    <td class="w3-center">1.7-2.4</td>
</tr>
<tr>
    <td class="w3-center">300</td>
    <td class="w3-center">1.6-2.5</td>
    <td class="w3-center">1.6-2.1</td>
</tr>
<tr>
    <td class="w3-center">400</td>
    <td class="w3-center">1.8-2.6</td>
    <td class="w3-center">1.8-2.3</td>
</tr>
</tbody>
</table>

