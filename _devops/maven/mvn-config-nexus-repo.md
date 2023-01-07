---
title: "配置 Nexus 仓库"
sequence: '001'
---

## 配置

### 系统层面

#### hosts

通过 `SwitchHosts` 软件来配置 `hosts` 信息：

```text
192.168.30.18 maven.lan.net
```

这个 `maven.lan.net` 域名，会在下面的 `settings.xml` 文件中用到。

#### settings.xml

在 `C:\Users\<当前用户>\.m2` 目录，添加 `settings.xml` 文件：

- [settings.xml](./settings.xml)

### 项目层面

#### pom.xml

在项目的 `pom.xml` 文件中，添加如下配置：

```xml
<distributionManagement>
    <repository>
        <id>${releases.id}</id>
        <name>${releases.name}</name>
        <url>${releases.url}</url>
    </repository>
    <snapshotRepository>
        <id>${snapshots.id}</id>
        <name>${snapshots.name}</name>
        <url>${snapshots.url}</url>
    </snapshotRepository>
</distributionManagement>
```

如果想发布源码，添加如下内容：

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-source-plugin</artifactId>
        </plugin>
    </plugins>
</build>
```

## 使用

部署到内网（http://maven.lan.net:8081/）：

```text
mvn clean deploy -DskipTests
或
mvn clean deploy -DskipTests -Pdev
```

部署到外网（http://36.138.170.6:14581/nexus/）：

```text
mvn clean deploy -DskipTests -Pprod
```

