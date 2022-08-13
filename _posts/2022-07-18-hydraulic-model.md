---
title:  "水力模型"
date: 2022-07-18 10:00:00 +0800
categories: hydraulic
---

The general guideline is "If you cannot make your model replicate reality, then simplify reality until you can model it . . ."

## 水力模型

{% assign filtered_posts = site.hydraulic-model | where_exp: "item", "item.url contains '/hydraulic-model/basic/'" | sort: "sequence" %}
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

{% assign filtered_posts = site.hydraulic-model | where_exp: "item", "item.url contains '/hydraulic-model/epanet/'" | sort: "sequence" %}
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

{% assign filtered_posts = site.hydraulic-model | where_exp: "item", "item.url contains '/hydraulic-model/epanet-user/'"%}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endfor %}
</ol>

### 开发者视角：编写程序

{% assign filtered_posts = site.hydraulic-model | where_exp: "item", "item.url contains '/hydraulic-model/epanet-dev/'"%}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endfor %}
</ol>

### 水力模型的数据

{% assign filtered_posts = site.hydraulic-model | where_exp: "item", "item.url contains '/hydraulic-model/data/'" | sort: "sequence" %}
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

- [EPANET](https://www.epa.gov/water-research/epanet)
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

- [Epanet and Development. How to calculate water networks by computer](https://issuu.com/arnalich/docs/epanet_and_development)

