---
title:  "水力模型"
date: 2022-07-18 10:00:00 +0800
categories: hydraulic
---

The general guideline is "If you cannot make your model replicate reality, then simplify reality until you can model it . . ."

## 水力模型

{% assign filtered_posts = site.hydraulic-model | where_exp: "item", "item.url contains '/hydraulic-model/basic/'"%}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endfor %}
</ol>

## EPANET

```text
EPANET = EPA + NET

EPA = U.S. Environmental Protection Agency 美国环境保护局
NET = network
```



{% assign filtered_posts = site.hydraulic-model | where_exp: "item", "item.url contains '/hydraulic-model/epanet/'"%}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endfor %}
</ol>

## Reference

- [EPANET](https://www.epa.gov/water-research/epanet)
  - [1. Introduction](https://epanet22.readthedocs.io/en/latest/1_introduction.html)
  - [3. The Network Model](https://epanet22.readthedocs.io/en/latest/3_network_model.html)
  - [12. Analysis Algorithms](https://epanet22.readthedocs.io/en/latest/12_analysis_algorithms.html)
- [Samples and libraries for EPANET developers (C, C++, C#, Haskell, Java, JavaScript, MATLAB, Python, Visual Basic)](http://epanet.de/developer/index.html.en)
- [EPANET文件解析和管线还原](https://bibichuan.github.io/posts/9d35c66.html)

