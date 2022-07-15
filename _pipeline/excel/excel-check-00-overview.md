---
title:  "Excel检查：概览"
categories: pipeline
---

## 内容分类

{:refdef: style="text-align: center;"}
![](/assets/image/pipeline/excel-point-and-line-data-check.png)
{: refdef}

检查内容分成四类：

- 通用检查：不论是“点”表，还是“线”表，它们有一些共性的内容，都可以在这里检查。
- 点表：单独检查。
- 线表：单独检查。
- 点表+线表：联合检查。

## 检查步骤

{:refdef: style="text-align: center;"}
![](/assets/image/pipeline/excel-point-and-line-data-check-process.png)
{: refdef}

检查步骤：

<ul>
    <li>第一步，基础检查。例如，单元格内容不能为空、单元格内容为数值。</li>
    <li>第二步，对单个“点”表数据进行检查。</li>
    <li>第三步，对单个“线”表数据进行检查。</li>
    <li>第四步，联合“点”表和“线”表数据进行检查。</li>
    <li>第五步，进一步检查。</li>
</ul>

## 实现思路

{:refdef: style="text-align: center;"}
![](/assets/image/pipeline/excel-point-and-line-data-check-implementation.png)
{: refdef}

<p>
    实现思路：
</p>
<ul>
    <li>第一步，将硬盘上的Excel文件读取到内存中，生成二维字符串数组 <code>String[][]</code></li>
    <li>第二步，对二维字符串数组 <code>String[][]</code>应用验证逻辑</li>
    <li>第三步，将验证结果输出显示</li>
</ul>

## 用户界面

{:refdef: style="text-align: center;"}
![](/assets/image/pipeline/excel-check-ui-three-parts.png)
{: refdef}

菜单分成三个部分：

- 第一部分，打开Excel文件。
- 第二部分，对Excel内容进行检查。
- 第三部分，其它。
