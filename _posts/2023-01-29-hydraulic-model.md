---
title:  "水力模型 Hydraulic Model"
date: 2023-01-29 10:00:00 +0800
categories: hydraulic
---

The general guideline is "If you cannot make your model replicate reality, then simplify reality until you can model
it . . ."

## 相关资料

水力模型（hydraulic model）和 EPANET 之间的关系：水力模型是一个通用的概念，而 EPANET 是一个具体的实现。
最早的 EPANET 是由美国环境保护局使用 C 或 C++ 开发的，后续有其它语言的版本，例如：Javascript、Python 和 Java 等。

- 代码
    - [jm-hydraulic-model-web][jm-hydraulic-model-web-url]
    - [jm-hydraulic-model-service][jm-hydraulic-model-service-url]
- EPANET
    - C/C++: [EPANET 官网][epanet-url]
    - Javascript: [epanet-js][epanet-js-url]
    - Python: [wntr](https://pypi.org/project/wntr/) Water Network Tool for Resilience (WNTR)
- 资料：
    - 飞秋共享 `EPANET` 文件夹。其中，测试数据位于 `01-data` 子文件夹。
    - 飞秋共享 `Hydraulic` 文件夹
    - [The Network Model](https://epanet22.readthedocs.io/en/latest/3_network_model.html)
    - 《EPANET2 用户手册》 第 3 章 管网模型
    - 数据检查
        - [判断图的连通性的三种方法：DFS、BFS 和并查集](https://zhuanlan.zhihu.com/p/201096910)
- 视频：
    - [B站：供水水力模型的建立](https://www.bilibili.com/video/BV1uZ4y1H7wQ) WaterDesk 是由上海慧水公司独立开发的免费水力模型应用软件

```text
EHM = EPANET Hydraulic Model

A B C D E F G H ... M
1 2 3 4 5 6 7 8 ... 13

前端接口：5813
后端接口：4186
```

## 水力模型

{% assign filtered_posts = site.hydraulic-model | where_exp: "item", "item.url contains '/hydraulic-model/basic/'" |
sort: "sequence" %}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endfor %}
</ol>

## EPANET

### 概念

```text
EPANET = EPA + NET

EPA = U.S. Environmental Protection Agency 美国环境保护局
NET = network
```

{% assign filtered_posts = site.hydraulic-model | where_exp: "item", "item.url contains '/hydraulic-model/epanet/'" |
sort: "sequence" %}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endfor %}
</ol>

### 用户视角：使用软件

A model can only be as good as the data which it is based on.

{% assign filtered_posts = site.hydraulic-model | where_exp: "item", "item.url contains '
/hydraulic-model/epanet-user/'"%}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endfor %}
</ol>

### 开发者视角：编写程序

{% assign filtered_posts = site.hydraulic-model | where_exp: "item", "item.url contains '
/hydraulic-model/epanet-dev/'"%}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endfor %}
</ol>

### 水力模型的数据

{% assign filtered_posts = site.hydraulic-model | where_exp: "item", "item.url contains '/hydraulic-model/data/'" |
sort: "sequence" %}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endfor %}
</ol>

## Reference

EPANET

- [EPANET][epanet-url]
- 用户
    - [Self-Extracting Installation Program for EPANET 2.2 (EXE)](https://github.com/USEPA/EPANET2.2/releases/download/2.2.0/epanet2.2_setup.exe)
    - [Non-Installing Software for EPANET 2.2 (ZIP)](https://github.com/USEPA/EPANET2.2/releases/download/2.2.0/epanet2.2.zip)
- 开发
    - [EPANET 2.2 Programmer's Toolkit Files (ZIP)](https://github.com/USEPA/EPANET2.2/releases/download/2.2.0/epanet2.2_toolkit.zip)
    - [EPANET 2.2 Source Code Files (ZIP)](https://github.com/USEPA/EPANET2.2/archive/2.2.0.zip)
- 文档
    - [EPANET 2.2 Online User's Manual](https://epanet22.readthedocs.io/en/latest/)
        - [1. Introduction](https://epanet22.readthedocs.io/en/latest/1_introduction.html)
        - [3. The Network Model](https://epanet22.readthedocs.io/en/latest/3_network_model.html)
        - [12. Analysis Algorithms](https://epanet22.readthedocs.io/en/latest/12_analysis_algorithms.html)
- [Samples and libraries for EPANET developers (C, C++, C#, Haskell, Java, JavaScript, MATLAB, Python, Visual Basic)](http://epanet.de/developer/index.html.en)
- [EPANET文件解析和管线还原](https://bibichuan.github.io/posts/9d35c66.html)
- [EPANET源码解读](https://www.cnblogs.com/KingOfFreedom/tag/EPANET%E6%BA%90%E7%A0%81%E8%A7%A3%E8%AF%BB/)

- [Epanet and Development. How to calculate water networks by computer](https://issuu.com/arnalich/docs/epanet_and_development)
- [OWA-EPANET Toolkit](http://wateranalytics.org/EPANET/)

- 不同编程语言实现的 EPANET
    - C/C++: [EPANET][epanet-url]
    - Javascript: [epanet-js][epanet-js-url]
    - Python:
        - [wntr](https://pypi.org/project/wntr/) The Water Network Tool for Resilience (WNTR) is a Python package
          designed to simulate and analyze resilience of water distribution networks.
          [DOC](https://wntr.readthedocs.io/en/stable/overview.html)
        - [EPANET](https://pypi.org/project/EPANET/) Python interface for the popular urban drainage model EPANET 2.0
          engine.

视频：

- [供水水力模型的建立](https://www.bilibili.com/video/BV1uZ4y1H7wQ)
- [Bentley水模型软件使用技巧](https://ke.qq.com/course/431413/3642712088024373)
- [水锤及水力模型技术与应用](https://ke.qq.com/course/459986)

Github:

- [Open Water Analytics](https://github.com/OpenWaterAnalytics)
    - [OpenWaterAnalytics/EPANET](https://github.com/OpenWaterAnalytics/EPANET): The Water Distribution System Hydraulic and Water Quality Analysis Toolkit
    - [OpenWaterAnalytics/epanet-rtx](https://github.com/OpenWaterAnalytics/epanet-rtx):
      EPANET-RTX is the real-time extension to the EPANET Hydraulic Toolkit.
      It provides an interoperable framework for moving data between an SCADA database,
      various time series analysis methods, and a hydraulic solver.
    - [OpenWaterAnalytics/epanet-dev](https://github.com/OpenWaterAnalytics/epanet-dev):
      This is a collaborative project to develop a new version of the EPANET computational engine
      for analyzing water distribution systems.
    - [OpenWaterAnalytics/WNTR](https://github.com/OpenWaterAnalytics/WNTR):
      An EPANET compatible python package to simulate and analyze water distribution networks under disaster scenarios.

[epanet-url]: https://www.epa.gov/water-research/epanet

[epanet-js-url]: https://epanetjs.com/

[jm-hydraulic-model-service-url]: http://36.138.170.6:8929/bdjm/jm-hydraulic-model-service

[jm-hydraulic-model-web-url]: http://36.138.170.6:8929/bdjm/jm-hydraulic-model-web