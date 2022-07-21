---
title:  "Excel检查：使用文档"
categories: pipeline
sequence: 008
---

## 安装和卸载

### 安装

双击`JMExcelCheck-1.0.exe`，开始安装：

{:refdef: style="text-align: center;"}
![](/assets/image/pipeline/jm-excel-check-exe-installer.png)
{: refdef}

下一步，选择安装目录：

{:refdef: style="text-align: center;"}
![](/assets/image/pipeline/jm-excel-check-choose-installation-directory.png)
{: refdef}

安装完成之后，会在桌面生成图标：

{:refdef: style="text-align: center;"}
![](/assets/image/pipeline/jm-excel-check-desktop-icon.png)
{: refdef}

### 卸载

第一步，卸载软件。Windows设置 --> 应用 --> 应用和功能，找到`JMExcelCheck`，点击“卸载”：

{:refdef: style="text-align: center;"}
![](/assets/image/pipeline/jm-excel-check-uninstall.png)
{: refdef}

第二步，删除配置。下面的`.bdjm`文件夹（bd=BaoDing）是存放软件配置的地方，可以全部删除。

```text
C:\Users\用户名\.bdjm
```

例如，用户名是`1`，其路径是`C:\Users\1\.bdjm`：

{:refdef: style="text-align: center;"}
![](/assets/image/pipeline/jm-excel-check-config-directory.png)
{: refdef}

经过上述两个步骤，软件就完全删除了。

## 使用软件

双击桌面图标，打开软件：

{:refdef: style="text-align: center;"}
![](/assets/image/pipeline/jm-excel-check-ui.png)
{: refdef}

### 数据文件夹

**数据文件夹**，是包含点表（以P结尾）和线表（以L结尾）目录。

例如：

```text
D:\Data\某庆\化二+厂外点线表
```

{:refdef: style="text-align: center;"}
![](/assets/image/pipeline/jm-excel-check-data-directory.png)
{: refdef}

目前支持的水种类型：

```java
public enum PipeType {
    CAS("脱氧水"),
    CPS("处理后排水"),
    CS("生产水"),
    CYS("除盐水"),
    CW("生产污水"),
    DGS("低硅水"),
    FES("生产废水"),

    HAS("海水水"),
    HHS("海水回水"),
    HS("生活水"),
    HW("生活污水"),


    J("给水"),
    JW("含碱污水"),
    LW("含硫污水"),

    P("排水"),
    QFS("清净废水"),
    RHS("软化水"),
    S("新鲜水"),
    SW("含酸污水"),
    UW("含油污水"),
    WHS("污水回用水"),

    XF("消防水"),
    XHS("循环水"),
    XHW("循环冷却水排污"),
    XL("循环冷水"),
    XR("循环热水"),

    YS("雨水"),
    YUS("原水"),
    YW("雨污合流"),

    ZS("中水"),
    ZSS("再生水"),
    ;
}
```

#### 打开

操作：**文件** --> **打开数据文件夹**

{:refdef: style="text-align: center;"}
![](/assets/image/pipeline/jm-excel-check-open-data-directory.png)
{: refdef}

界面左侧显示各个类型的数据：

{:refdef: style="text-align: center;"}
![](/assets/image/pipeline/jm-excel-check-after-open-data-directory.png)
{: refdef}

#### 关闭

操作：**文件** --> **关闭数据文件夹**

### Excel文件

打开和关闭Excel文件：

- 打开：选择`XL-循环冷水`，然后**文件**-->**加载Excel数据**，会打开相应的文件。
- 关闭：选择`XL-循环冷水`，然后**文件**-->**关闭Excel数据**，会关闭相应的文件。

{:refdef: style="text-align: center;"}
![](/assets/image/pipeline/jm-excel-check-load-excel-data.png)
{: refdef}

快捷键：

- 在`XL-循环冷水`上右键点击，可以加载相应的Excel文件。
- 在**空白处**右键点击，可以关闭加载的Excel文件。

### 数据检查

检查顺序：先**基础检查**，再进行**点检查**，再进行**线检查**，最后进行**点线联合检查**。

检查内容细节，可以参考[这里]({% link _posts/2022-07-09-pipeline.md %})：

- [基础检查]({% link _pipeline/excel/excel-check-01-common-logic.md %})
- [点检查]({% link _pipeline/excel/excel-check-02-point-logic.md %})
- [线检查]({% link _pipeline/excel/excel-check-03-line-logic.md %})
- [点线联合检查]({% link _pipeline/excel/excel-check-04-both-point-and-line-logic.md %})

注意：如果直接使用“点线联合检查”的功能，很大概率会出现错误，其原因是数据当中存在错误，在前几步检查当中需要先检测出来，进行修正。


