---
title:  "水力模型：调整参数"
sequence: 006
---

## 预处理

### 排除不连通的管线

在水力模型中，需要计算水在管网中的流动。
如果一段管线不与其它的管线相连接，是没有办法计算的，因此需要排除不连通的管线。

## 初始值设置

### 管点 Junction

- [ ] 节点的需水量
  - 用水表的监测流量（例如，200立方米每小时）和管线的管径（例如，300毫米），求流速（例如，0.78米每秒）。
    那么相同管径（例如，300毫米）的管线可以采用近似或相同的流速来求解流量。
  - 并不是每个Junction都有需水量，只有出水的地方（边界上的点）才有需水量

### 管线 Pipe

- [ ] 设置管线的粗糙系数 Roughness Coefficient

### 水池 Reservoir



### 水塔 Tank

### 水泵

- [ ] 设置扬程曲线

### Option

- UNITS: CMH
- HEADLOSS: H-W
- DEMAND MODEL: DDA

### Time

- DURATION: 24 HOURS
- HYDRAULIC TIMESTEP: 1 HOURS
- PATTERN TIMESTEP: 1 HOURS

## 调整参数


## Reference

- [Youtube: Negative pressures in EPANET and how to fix them](https://www.youtube.com/watch?v=tPt1Egyk37Y)

