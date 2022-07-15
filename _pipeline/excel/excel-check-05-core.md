---
title:  "Excel检查：excel-check-core"
categories: pipeline
sequence: 006
---

## 数值处理

<p>
    数值类型处理的思路：
</p>
<ul>
    <li>
        <b>第一，优先按“字符串”（String）来处理。</b>
        例如，一个高程，它的值应该是数值，
        但是整个<code>String[][]</code>存的都是字符串（String），
        在判断它的值到底是不是数值类型时，不进行类型转换（Double.parseDouble()），
        而是使用正则表达式对它进行判断。
    </li>
    <li>
        <b>第二，如果数值之间存在“不损失精度的计算”关系，则使用BigDecimal进行计算，保证计算的准确性。</b>
        例如，一个数值加上，或减去另一个数值等于某个结果值。
        如果使用float或double来计算，可能会损失精度。
    </li>
    <li>
        <b>第三，如果涉及“损失精度的计算”时，使用double类型。</b>
        因为求距离或角度时，需要进行“开平方”，就有精度损失。
        使用BigDecimal性能效率不高。
    </li>
</ul>

## 源代码

### 项目地址

```text

```

### 安装到本地

```text
mvn install -Dmaven.test.skip=true
```

