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

检查内容细节，可以参考[这里]({% link _posts/2022-07-09-pipeline.md %})

注意：如果直接使用“点线联合检查”的功能，很大概率会出现错误，其原因是数据当中存在错误，在前几步检查当中需要先检测出来，进行修正。


