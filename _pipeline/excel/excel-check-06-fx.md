---
title:  "Excel检查：excel-check-fx"
categories: pipeline
sequence: 007
---

项目`excel-check-fx`的主要目的使用JavaFX显示检查Excel的结果。

## 开发环境

- JDK版本：17
- IDE: IntelliJ IDEA 2022.1.3 (Community Edition)
- JavaFX: 17.0.1

## 源代码

### 项目地址

```text

```

### 用户界面

在`src/main/resources/fxml`目录中，存放了多个`*.fxml`文件：

- 主界面：`main-view.fxml`
- 数据设置：`data-setting-view.fxml`
- 点、线元信息设置
  - 点信息：`point-meta-setting-view.fxml`
  - 线信息：`line-meta-setting-view.fxml`
- 点、线检查设置
  - 点检查：`point-check-setting-view.fxml`
  - 线检查：`line-check-setting-view.fxml`
- 点要素编码：`feature-code-choose-type-view.fxml`
- 关于界面：`about-view.fxml`

### 配置文件

在`src/main/resources/config`目录中，存放了多个`*.properties`文件：

- 点信息：`point-meta-config.properties`
- 点检查：`point-check-config.properties`
- 点编码：`point-code.txt` （可以编辑）
- 线信息：`line-meta-config.properties`
- 线检查：`line-check-config.properties`
- 用户：`user-config.properties`
