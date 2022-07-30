---
title:  "水力模型：用水模式"
sequence: 005
---

用水模型，是不同类型用户（如工业、居民等）在一段时间内的连续用水规律。

```text
用水模型 = 在一段时间内的用水规律
```

对于动态模型，用水模式是进行模型关键节点水量在时间分配的关键数据。

由于用水模式直接参与模型水力模拟计算，因此保证用水模型的精准度，是提高模型精度值的关键措施。

```text
用户模式精准 ---> 水力模拟计算精准
```

## 典型的居民用水

Typical Residential Pattern:

{:refdef: style="text-align: center;"}
![](/assets/image/hydraulic-model/epanet/typical-residential-pattern.png)
{: refdef}

```text
0.6 0.5 0.4 0.3
0.4 0.5 1.2 1.6
1.6 1.5 1.3 1.1
1.0 1.0 0.9 0.9
1.0 1.1 1.2 1.3
1.3 1.3 1.2 0.9
```

<table>
<tbody>
<tr>
    <th class="w3-center">1</th>
    <td class="w3-center">0.6</td>
</tr>
<tr>
    <th class="w3-center">2</th>
    <td class="w3-center">0.5</td>
</tr>
<tr>
    <th class="w3-center">3</th>
    <td class="w3-center">0.4</td>
</tr>
<tr>
    <th class="w3-center">4</th>
    <td class="w3-center">0.3</td>
</tr>
<tr>
    <th class="w3-center">5</th>
    <td class="w3-center">0.4</td>
</tr>
<tr>
    <th class="w3-center">6</th>
    <td class="w3-center">0.5</td>
</tr>
<tr>
    <th class="w3-center">7</th>
    <td class="w3-center">1.2</td>
</tr>
<tr>
    <th class="w3-center">8</th>
    <td class="w3-center">1.6</td>
</tr>
<tr>
    <th class="w3-center">9</th>
    <td class="w3-center">1.6</td>
</tr>
<tr>
    <th class="w3-center">10</th>
    <td class="w3-center">1.5</td>
</tr>
<tr>
    <th class="w3-center">11</th>
    <td class="w3-center">1.3</td>
</tr>
<tr>
    <th class="w3-center">12</th>
    <td class="w3-center">1.1</td>
</tr>
<tr>
    <th class="w3-center">13</th>
    <td class="w3-center">1.0</td>
</tr>
<tr>
    <th class="w3-center">14</th>
    <td class="w3-center">1.0</td>
</tr>
<tr>
    <th class="w3-center">15</th>
    <td class="w3-center">0.9</td>
</tr>
<tr>
    <th class="w3-center">16</th>
    <td class="w3-center">0.9</td>
</tr>
<tr>
    <th class="w3-center">17</th>
    <td class="w3-center">1.0</td>
</tr>
<tr>
    <th class="w3-center">18</th>
    <td class="w3-center">1.1</td>
</tr>
<tr>
    <th class="w3-center">19</th>
    <td class="w3-center">1.2</td>
</tr>
<tr>
    <th class="w3-center">20</th>
    <td class="w3-center">1.3</td>
</tr>
<tr>
    <th class="w3-center">21</th>
    <td class="w3-center">1.3</td>
</tr>
<tr>
    <th class="w3-center">22</th>
    <td class="w3-center">1.3</td>
</tr>
<tr>
    <th class="w3-center">23</th>
    <td class="w3-center">1.2</td>
</tr>
<tr>
    <th class="w3-center">24</th>
    <td class="w3-center">0.9</td>
</tr>
</tbody>
</table>




