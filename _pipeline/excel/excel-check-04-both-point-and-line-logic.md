---
title:  "Excel检查：点和线联合"
categories: pipeline
sequence: 005
---

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

## 管段夹角

### 介绍

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
