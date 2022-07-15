---
title:  "Excel检查：线"
categories: pipeline
sequence: 004
---

## 点号缺失检查

检查内容：

- 同一行数据中，“起始点号”和“终止点号”，任意一个缺失。

具体实现：

- 在“基础检查”的“非空检查”中实现。

## 起点和终点相同检查

检查内容：

- 在同一行数据中，“起始点号”和“终止点号”，两者相同。例如，“起始点号”为<code>CS9</code>和“终止点号”也为<code>CS9</code>，则进行提示。

{:refdef: style="text-align: center;"}
![](/assets/image/pipeline/line-check-begin-and-end-same-point-marker.png)
{: refdef}

## 管线重复检查

检查内容：

<ul>
    <li>
        第一种情况，两行数据中的“起始点号”和“终止点号”相同，则进行提示：
        <ul>
            <li>在第\(i\)行中，“起始点号”和“终止点号”分别为<code>CS1</code>和<code>CS1</code></li>
            <li>在第\(j\)行中，“起始点号”和“终止点号”分别为<code>CS1</code>和<code>CS2</code></li>
        </ul>
    </li>
    <li>
        第二种情况，两行数据中的“起始点号”和“终止点号”互换，则进行提示：
        <ul>
            <li>在第\(i\)行中，“起始点号”和“终止点号”分别为<code>CS1</code>和<code>CS2</code></li>
            <li>在第\(j\)行中，“起始点号”和“终止点号”分别为<code>CS2</code>和<code>CS1</code></li>
        </ul>
    </li>
</ul>

{:refdef: style="text-align: center;"}
![](/assets/image/pipeline/line-check-duplicate.png)
{: refdef}

## 属性一致性检查

检查内容：

<ul>
    <li>同一个管点：埋深、高程、埋设方式、材质和管径是否一致，断面尺寸是否一致。</li>
    <li>”同一个管点“，在不同的”管线“当中的”高程“应该是一致的。</li>
    <li>”同一个管点“，在不同的”管线“当中的”埋深“应该是一致的。</li>
    <li>”同一个管点“，在不同的”管线“当中的”断面尺寸“应该是一致的。</li>
</ul>

<div class="w3-panel w3-pale-green w3-bottombar w3-border-green w3-border">
    <p>“断面尺寸”，对于管线来说是“管径”，对于方沟来说是“宽X高”。</p>
</div>
