---
title: "水表和压力 Json 数据格式解析"
sequence: 102
---

一个 Json 格式的数据示例：

```text
{
    "params": {
        "AE@162322738687727": 0,       // 空管报警 Empty Pipe Alarm
        "AH@162322738687727": 0,       // 上限报警 Alarm High Value
        "AL@162322738687727": 0,       // 下限报警 Alarm Low Value
        "AS@162322738687727": 0,       // 系统报警 System Alarm
        "CFF@162322738687727": 0.10,   // 正向累积量小数部分 Forward Accumulation Fraction，C 表示 Cumulative，即“累积的”
        "CFI@162322738687727": 1194,   // 正向累积量整数部分 Forward Accumulation Integer
        "CRF@162322738687727": 0.76,   // 反向累积量小数部分 Reverse Accumulation Fraction
        "CRI@162322738687727": 45,     // 反向累积量整数部分 Reverse Accumulation Integer
        "FI@162322738687727": 43.80,   // 瞬时流量 Instantaneous Flow
        "FP@162322738687727": 14.26,   // 流量百分比 Flow Percentage
        "FV@162322738687727": 0.43,    // 瞬时流速 Flow Velocity
        "PRS@162322650980631": 0.00,   // 压力 Pressure
        "RC@162322738687727": 0.00,    // 流体电导比 Fluid Conductivity Ratio
        "UC@162322738687727": 1,       // 累积总量单位 Cumulative Total Unit
        "UF@162322738687727": 5        // 瞬时流量单位 Flow Unit
    },
    "timestamp": "1675909110000"
}
```

- `params`：传递的主要参数 
- `timestamp`：时间戳

## params

```text
缩写@Id
```

- 缩写：表示流量计的各项指标
- Id：表示设备的 ID

长度限制：

- 在计讯 RTU 设备中，上传编码（即`缩写@Id`）最多支持 19 个字符
- `缩写` 部分，占用 2~3 个字符
- `@` 部分，占用 1 个字符
- `Id` 部分，占用 15~16 个字符。为了兼容 `缩写` 部分（占用 2~3 个字符），使用 15 个字符比较稳妥。

<table>
    <thead>
    <tr>
        <th>缩写</th>
        <th>名称</th>
        <th>备注</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>AE</td>
        <td>空管报警</td>
        <td>
            <ul>
                <li>A 表示 Alarm，即“报警”</li>
                <li>E 表示 Empty，即“空的”</li>
            </ul>
            Empty Pipe Alarm
        </td>
    </tr>
    <tr>
        <td>AH</td>
        <td>上限报警</td>
        <td>
            <ul>
                <li>A 表示 Alarm，即“报警”</li>
                <li>H 表示 High，即“高的”</li>
            </ul>
            Alarm High Value
        </td>
    </tr>
    <tr>
        <td>AL</td>
        <td>下限报警</td>
        <td>
            <ul>
                <li>A 表示 Alarm，即“报警”</li>
                <li>L 表示 Low，即“低的”</li>
            </ul>
            Alarm Low Value
        </td>
    </tr>
    <tr>
        <td>AS</td>
        <td>系统报警</td>
        <td>
            <ul>
                <li>A 表示 Alarm，即“报警”</li>
                <li>S 表示 System，即“系统”</li>
            </ul>
          System Alarm
        </td>
    </tr>
    <tr>
        <td>CFF</td>
        <td>正向累积量小数部分</td>
        <td>
            <ul>
                <li>C 表示 Cumulative，即“累积的”</li>
                <li>F 表示 Forward，即“正向的”</li>
                <li>F 表示 Fraction，即“小数部分”</li>
            </ul>
            Forward Accumulation Fraction
        </td>
    </tr>
    <tr>
        <td>CFI</td>
        <td>正向累积量整数部分</td>
        <td>
            <ul>
                <li>C 表示 Cumulative，即“累积的”</li>
                <li>F 表示 Forward，即“正向的”</li>
                <li>I 表示 Integer，即“整数部分”</li>
            </ul>
            Forward Accumulation Integer
        </td>
    </tr>
    <tr>
        <td>CRF</td>
        <td>反向累积量小数部分</td>
        <td>
            <ul>
                <li>C 表示 Cumulative，即“累积的”</li>
                <li>R 表示 Reverse，即“反向的”</li>
                <li>F 表示 Fraction，即“小数部分”</li>
            </ul>
            Reverse Accumulation Fraction
        </td>
    </tr>
    <tr>
        <td>CRI</td>
        <td>反向累积量整数部分</td>
        <td>
            <ul>
                <li>C 表示 Cumulative，即“累积的”</li>
                <li>R 表示 Reverse，即“反向的”</li>
                <li>I 表示 Integer，即“整数部分”</li>
            </ul>
            Reverse Accumulation Integer
        </td>
    </tr>
    <tr>
        <td>FI</td>
        <td>瞬时流量</td>
        <td>
            <ul>
                <li>F 表示 Flow，即“流量”</li>
                <li>I 表示 Instantaneous，即“瞬时的”</li>
            </ul>
            Instantaneous Flow
        </td>
    </tr>
    <tr>
        <td>FP</td>
        <td>流量百分比</td>
        <td>
            <ul>
                <li>F 表示 Flow，即“流量”</li>
                <li>P 表示 Percent，即“百分比”</li>
            </ul>
           Flow Percentage
        </td>
    </tr>
    <tr>
        <td>FV</td>
        <td>瞬时流速</td>
        <td>
            <ul>
                <li>F 表示 Flow，即“流量”</li>
                <li>V 表示 Velocity，即“速度”</li>
            </ul>
            Flow Velocity
        </td>
    </tr>
    <tr>
        <td>PRS</td>
        <td>压力</td>
        <td>
            <ul>
                <li>PRS 表示 Pressure，即“压力”</li>
            </ul>
            Pressure
        </td>
    </tr>
    <tr>
        <td>RC</td>
        <td>流体电导比</td>
        <td>
            <ul>
                <li>R 表示 Ratio，即“比率”</li>
                <li>C 表示 Conductivity，即“导电”</li>
            </ul>
            Fluid Conductivity Ratio
        </td>
    </tr>
    <tr>
        <td>UC</td>
        <td>累积总量单位</td>
        <td>
            <ul>
                <li>U 表示 Unit，即“单位”</li>
                <li>C 表示 Cumulative，即“累积的”</li>
            </ul>
            Cumulative Total Unit
        </td>
    </tr>
    <tr>
        <td>UF</td>
        <td>瞬时流量单位</td>
        <td>
            <ul>
                <li>U 表示 Unit，即“单位”</li>
                <li>F 表示 Flow，即“流量”</li>
            </ul>
            Flow Unit
        </td>
    </tr>
    </tbody>
</table>


在上表中，一些**首字母**的含义如下：

- `A`：表示 Alarm，即“报警”
- `C`：表示 Cumulative，即“累积的”
- `F`：表示 Flow，即“流量”
- PRS：表示 Pressure，即“压力”
- `R`：表示 Ratio，即“比率”
- `U`：表示 Unit，即“单位”

