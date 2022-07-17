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

- `main-view.fxml`:：主界面
- `point-meta-view.fxml`：点信息设置界面
- `point-check-view.fxml`：点检查设置界面
- `line-meta-view.fxml`：线信息设置界面
- `line-check-view.fxml`：线检查设置界面
- `about-view.fxml`：关于界面

### 配置文件

- `point-meta-config.properties`：点信息
- `point-check-config.properties`：点检查
- `point-code.txt`：点编码
- `line-meta-config.properties`：线信息
- `line-check-config.properties`：线检查
- `user-config.properties`：用户
