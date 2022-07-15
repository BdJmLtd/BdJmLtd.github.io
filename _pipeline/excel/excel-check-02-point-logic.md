---
title:  "Excel检查：点"
categories: pipeline
sequence: 003
---

## 图上点号和物探点号相等

检查内容：

- 在同一行数据中，如果“图上点号”和“物探点号”不相同，则进行提示。例如，图上点号是`CS1`，物探点号是`CS2`。

{:refdef: style="text-align: center;"}
![](/assets/image/pipeline/point-check-map-and-prospect-point-marker-not-equal.png)
{: refdef}

```text
'图上点号'和'物探点号'是否一致检查: 1
|001| 行 2:
    列 A(1): [CS1]
    列 B(2): [CS2]
```

## 重复的点号

检查内容：

<ul>
    <li>
        在不同行数据中，如果“图上点号”在第\(i\)行数据和第\(j\)行数据相同，则进行提示。
        <ul>
            <li>如果两行的“图上点号”相同，则进一步判断，后续的字段是否一致。</li>
        </ul>
    </li>

</ul>

{:refdef: style="text-align: center;"}
![](/assets/image/pipeline/point-check-duplicate.png)
{: refdef}

```text
点重复检查: 1
|001| CS1:
    行 2 列 A(1): [CS1, 特征：非普查区, 附属物：, X：3379503.338, Y：501548.722, 地面高程：46.923, 点编码：4]
    行 13 列 A(1): [CS1, 特征：, 附属物：水表井, X：3379505.148, Y：501547.846, 地面高程：46.98, 点编码：24]
```

## 特征和附属物互斥

检查内容：

- 在同一行数据中，“特征”和“附属物”两者只能一个有值。

{:refdef: style="text-align: center;"}
![](/assets/image/pipeline/point-check-feature-and-appendage-only-one.png)
{: refdef}

```text
特征和附属物二选一检查: 1
|001| 行 5:
    列 C(3): [弯头]
    列 D(4): [阀门]
```

## 坐标和高程

检查内容：

<ul>
    <li>
        在不同行数据中，如果“X、Y、地面高程”在第\(i\)行数据和第\(j\)行数据相同，则进行提示。
    </li>
</ul>

{:refdef: style="text-align: center;"}
![](/assets/image/pipeline/point-check-same-x-y-altitude.png)
{: refdef}

```text
|001| 501253.636:3378822.843:42.43:
    行 15 列 E(5): [501253.636, 3378822.843, 42.43]
    行 16 列 E(5): [501253.636, 3378822.843, 42.43]
```

## 点编码

检查内容：

- “特征”或“附属物”与“点编码”对应。

### 原有规则

软件安装完成之后，会生成`C:\Users\<用户名>\.bdjm\excel\config\point-code.txt`文件。

其内容，可以根据实际情况进行修改：

```text
1;false;探测点;弯头,三通,四通,入户
2;false;量测点;直线点
3;false;预留口;
4;false;非普查;
5;false;偏心井;
6;false;一井多盖;
7;false;一井多阀;
8;true;阀门;排气阀
9;true;管帽;盲堵
10;false;变径;变径点
```

上面每一行的格式如下：

```text
点编码;true或false;正式名字;别名1,别名2,别名3
```

- 第一列，点编码，就是数字。
- 第二列，`true`代表附属物，`false`表示特征。
- 第三列，特征或附属物的正式名字。
- 第四列，可以是别名，或者子类别的名字。

注意：**先要把`point-code.txt`内容修改为正确的值，才能检测出正确的结果**。

{:refdef: style="text-align: center;"}
![](/assets/image/pipeline/point-check-point-code-old.png)
{: refdef}

```text
点编码检查: 22
|001| 行 2:
    列 C(3): [非普查区, 记录值：4, 预期值：0]
|002| 行 3:
    列 D(4): [水表井, 记录值：24, 预期值：21]
```

### 技术规程2017

在《管线探测技术规程CJJ61-2017》的附录F [管线要素分类与代码表]({% link _pipeline/dict/pipeline-feature-and-code.md %})中，
描述了要素编码的规则。

