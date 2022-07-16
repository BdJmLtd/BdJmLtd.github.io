---
title:  "Excel检查：点和线联合"
categories: pipeline
sequence: 005
---

## 缺失和冗余点检查

检查内容：

- 缺失点，线表使用了某个点，但这个点没有出现在点表里。
- 冗余点，线表没有使用某个点，但这个点出现在了点表里。

## 埋深和高程检查

### 介绍

核心检查逻辑：

```text
地面高程 = 埋深 + 管线高程
```

其中，

- 地面高程，位于“点表”当中
- 埋深、管线高程，位于“线表”当中。一条管段，它有“起点”和“终点”：起点埋深、终点埋深、起点高程、终点高程。

---

### 预处理

在进行检查之前，先做一些**前期准备工作**：

- 第一步，保证点表（Point）当中的数据正确
  - 第一点，点表当中，不能有重复的点号
  - 第二点，点表当中，“地面高程”应该是数值
- 第二步，保证线表（Line）当中的数据正确
  - 第一点，“起点”和“终点”在点表当中是存在的
  - 第二点，起点埋深、终点埋深、起点高程、终点高程这四个字段，应该都是数值类型。

---

### 进行验证

前期准备完成之后，进行核心逻辑验证：

```text
地面高程 = 埋深 + 管线高程
```

## 管线长度检查

### 介绍

<p>
管线长度，起点\((x_{1}, y_{1}, z_{1})\)和终点\((x_{2}, y_{2}, z_{2})\)，使用三维距离：
</p>

<p>
\[
length = \sqrt{(x_{1}-x_{2})^{2} + (y_{1}-y_{2})^{2} + (z_{1}-z_{2})^{2}}
\]
</p>

### 预处理

- 第一步，点表验证
  - 第一点，点号不能重复。
  - 第二点，X、Y坐标为数值。
- 第二步，线表验证
  - 第一点，起点和终点。
    - 起点和终点，两者都不能空。
    - 起点和终点，不能是同一点。
    - 起点和终点，不能重复。
  - 第二点，无论起点，还是终点，在点表中是存在的。
  - 第三点，起点高程、终点高程是数值

### 验证

- 如果管段长度超过某个值（例如，75米或50米），则进行提示。
- 如果管段长度小于某个值（例如，0.05米），则进行提示。

```text
public static double getDistance(double x1, double y1, double z1, 
                                 double x2, double y2, double z2) {
    double diffX = x1 - x2;
    double diffY = y1 - y2;
    double diffZ = z1 - z2;
    return Math.sqrt(diffX * diffX + diffY * diffY + diffZ * diffZ);
}
```

## 管线坡度检查

### 介绍

管线坡度，计算“管线”与“水平面”的夹角。

{:refdef: style="text-align: center;"}
![管线坡度](/assets/image/pipeline/pipeline-slope.png)
{: refdef}

<p>
先通过<code>height</code>和<code>length</code>的值，计算出\(sin \theta\)的值：
</p>


<p>
\[
sin \theta = \frac{height}{length}
\]
</p>

<p>
再通过\(arcsin\)来计算\(\theta\)的值：
</p>

<p>
\[
\theta = arcsin(sin \theta)
\]
</p>

---

注意：

<ol>
  <li>没有使用\(tan \theta\)。因为有些管线是“垂直”的，就是会现\(\frac{height}{width} = \frac{height}{0}\)的情况</li>
  <li>
    没有使用\(cos \theta\)。因为求<code>height</code>只需要\(|z_{1}-z_{2}|\)就可以了，
    而计算<code>width</code>则需要计算\(\sqrt{(x_{1}-x_{2})^{2} + (y_{1}-y_{2})^{2}}\)，计算量会相对多一些。
  </li>
</ol>

### 预处理

与“管线长度检查”一样。

### 验证

坡度的范围应该是从0度到90度：

- 如果管段坡度超过某个值（例如，30度或10度），则进行提示。


```text
public static double getSlope(double x1, double y1, double z1, 
                              double x2, double y2, double z2) {
    double length = getDistance(x1, y1, z1, x2, y2, z2);
    double height = Math.abs(z1 - z2);
    double sinValue = height / length;
    double radian = Math.asin(sinValue);
    return Math.toDegrees(radian);
}
```

## 管点多通检查

### 介绍

检查内容：

- 例如，点为三通时，应该连接三个管线；点为四通时，应该连接四个管线。

### 预处理

- 第一步，点表验证
  - 第一点，点号不能重复。
- 第二步，线表验证
  - 第一点，起点和终点。
    - 起点和终点，两者都不能空。
    - 起点和终点，不能是同一点。
    - 起点和终点，不能重复。
  - 第二点，无论起点，还是终点，在点表中是存在的。

### 设置

如何设置“特征”与“n个方向“的关系？

- 在`设置|点检查设置`中，可以指定“一个方向特征”、“两个方向特征”、“三个方向特征”和“多个方向特征”。

{:refdef: style="text-align: center;"}
![](/assets/image/pipeline/jm-excel-check-settings-point-check-connection.png)
{: refdef}

### 验证

```text
管点多通检查：299
|001| CS1连接到1条管线，其特征是非普查区，目前使用的特征有：[非普查, 起止点, 出地点, 堵头, 出水口, 上杆]
     行2 列1：CS1~CS2
|002| CS2连接到2条管线，其特征是水表井，目前使用的特征有：[转折点, 直线点, 变径点, 变坡点, 变材点]
     行2 列1：CS1~CS2
     行3 列1：CS2~CS3
```

在第`|001|`数据中，`非普查区`和`非普查`是同一个意思，但是程序认为两者是不同的，这时候，需要将`非普查区`加入到一个方向特征的配置当中。

## 管段夹角

### 介绍

计算内容：

- 同一个管点，可以连接多条管线；计算连接同一管点的任意两个管线之间的夹角。夹角，是三维空间的夹角，不是二维空间，要考虑x, y, z。

### 预处理

- 第一步，点表验证
  - 第一点，点号不能重复。
  - 第二点，X、Y坐标为数值。
- 第二步，线表验证
  - 第一点，起点和终点。
    - 起点和终点，两者都不能空。
    - 起点和终点，不能是同一点。
    - 起点和终点，不能重复。
  - 第二点，无论起点，还是终点，在点表中是存在的。
  - 第三点，起点高程、终点高程是数值
  - 第四点，同一点，在不同管段中的埋深、高程应该是一样的。

### 验证

```text
public static double computeAngle(double x1, double y1, double z1, 
                                  double x2, double y2, double z2) {
    double dotProduct = x1 * x2 + y1 * y2 + z1 * z2;
    double distance1 = getDistance(x1, y1, z1, 0, 0, 0);
    double distance2 = getDistance(0, 0, 0, x2, y2, z2);
    double cosTheta = dotProduct / (distance1 * distance2);
    double radian = Math.acos(cosTheta);
    return Math.toDegrees(radian);
}
```
