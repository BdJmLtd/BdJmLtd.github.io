---
title:  "Excel检查：打包成exe"
categories: pipeline
sequence: 008
---

## jpackage

`jpackage` is a command-line tool to create native installers and packages for Java applications.

> jpackage是一个JDK的命令行工具，它可以将Java程序转换成安装包。

For example, we use DMG files on macOS and MSI files on Windows.

> 例如，生成macOS上的DMG文件，生成Windows上的MSI安装文件。

### 为什么选择JDK 17？

- JDK版本：17

从JDK 14版本，引入`jpackage`工具；在JDK 16版本，正式发布`jpackage`工具；JDK 17是LTS（Long Term Support，长期支持）版本。

### 前提条件

The key prerequisites for using the `jpackage` command are:

- The system used for packaging must contain the application to be packaged, a JDK, and software needed by the packaging tool.
- And, it needs to have the underlying packaging tools used by `jpackage`:
  - RPM, DEB on Linux: On Red Hat Linux, we need the rpm-build package; on Ubuntu Linux, we need the `fakeroot` package
  - PKG, DMG on macOS: Xcode command line tools are required when the –mac-sign option is used to request that the package be signed, and when the –icon option is used to customize the DMG image
  - EXE, MSI on Windows: On Windows, we need the third party tool **WiX** 3.0 or later
- Finally, the application packages must be built on the target platform.
  This means to package the application for multiple platforms, we must run the packaging tool on each platform.

{:refdef: style="text-align: center;"}
![Packaging Prerequisite](/assets/image/pipeline/jpackage-prerequisite.png)
{: refdef}

## 项目代码

这部分对应下图中的application的部分：

{:refdef: style="text-align: center;"}
![Packaging Prerequisite](/assets/image/pipeline/jpackage-prerequisite.png)
{: refdef}

application包括code（项目代码）和dependencies（依赖的Jar包）两部分。

```text
application = code + dependencies
```

我们要做两件事情：

- 第一件事情，将dependencies（依赖的Jar包）复制到`target/libs`目录下，通过`maven-dependency-plugin`插件实现。
- 第二件事情，将code（项目代码）打包成Jar文件，然后放到`target/libs`目录下。

### 配置pom.xml文件

`pom.xml`文件配置的重点

- `maven-dependency-plugin`插件，目的是将依赖的Jar文件（dependencies）复制到`target/libs`目录下。
- `maven-jar-plugin`插件，目的是将项目代码（code）打成Jar包文件。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>jm-data-excel</artifactId>
        <groupId>bdjm</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <artifactId>jm-data-excel-gui-fx</artifactId>

    <!-- 省略... -->

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-jar-plugin</artifactId>
                <configuration>
                    <archive>
                        <manifest>
                            <mainClass>jm.data.excel.gui.fx.Main</mainClass>
                            <addDefaultImplementationEntries>false</addDefaultImplementationEntries>
                            <addDefaultSpecificationEntries>false</addDefaultSpecificationEntries>
                        </manifest>
                        <addMavenDescriptor>false</addMavenDescriptor>
                    </archive>
                </configuration>
            </plugin>

            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-dependency-plugin</artifactId>
                <executions>
                    <execution>
                        <id>lib-copy-dependencies</id>
                        <phase>package</phase>
                        <goals>
                            <goal>copy-dependencies</goal>
                        </goals>
                        <configuration>
                            <!-- 排除JavaFX的groupId，因为我们会设置PATH_TO_FX和PATH_TO_FX_MODS环境变量 -->
                            <excludeGroupIds>org.openjfx</excludeGroupIds>
                            <!-- 将项目依赖的Jar包复制到target/libs目录下 -->
                            <outputDirectory>${project.build.directory}/libs</outputDirectory>
                            <overWriteReleases>false</overWriteReleases>
                            <overWriteSnapshots>false</overWriteSnapshots>
                            <overWriteIfNewer>true</overWriteIfNewer>
                        </configuration>
                    </execution>
                </executions>
            </plugin>

            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-resources-plugin</artifactId>
                <executions>
                    <execution>
                        <id>copy-jar-package</id>
                        <phase>package</phase>
                        <goals>
                            <goal>copy-resources</goal>
                        </goals>
                        <configuration>
                            <!-- 将项目生成的Jar包复制到target/libs目录下 -->
                            <outputDirectory>${project.build.directory}/libs</outputDirectory>
                            <resources>
                                <resource>
                                    <directory>${project.build.directory}</directory>
                                    <includes>
                                        <include>*.jar</include>
                                    </includes>
                                </resource>
                            </resources>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
</project>
```

### 生成Jar包

执行命令生成Jar包：

```text
mvn package -Dmaven.test.skip=true
```

这一步执行完成后：

- 会将依赖的Jar包都复制到`target/libs`目录下。
- 会生成`jm-data-excel-gui-fx-1.0-SNAPSHOT.jar`，并复制到`target/libs`目录中。

## JavaFX SDK和jmods

这部分对应下图中的JavaFX的部分：

{:refdef: style="text-align: center;"}
![Packaging Prerequisite](/assets/image/pipeline/jpackage-prerequisite.png)
{: refdef}

### 下载

下载地址：

```text
https://gluonhq.com/products/javafx/
```

下载JavaFX的SDK和jmods：

{:refdef: style="text-align: center;"}
![下载JavaFX SDK和jmods](/assets/image/pipeline/javafx-download-windows-sdk-and-jmods.png)
{: refdef}

在上图当中，选择的是18.0.1版本。选择JavaFX版本的优先顺序：

- 第一优先级，如果有LTS版本，更可以选择LTS版本。例如，17.0.3版本是LTS版本，但是没有找到下载地址。
- 第二优先级，如果有更新的版本，可以选择更新的版本。

### 解压

下载完成之后，得到`openjfx-18.0.1_windows-x64_bin-sdk.zip`和`openjfx-18.0.1_windows-x64_bin-jmods.zip`两个文件：

{:refdef: style="text-align: center;"}
![JavaFX SDK和jmods](/assets/image/pipeline/javafx-windows-sdk-jmods-zip-files.png)
{: refdef}

对两个文件进行解压，例如，得到路径分别为：

```text
D:\software\jdk\javafx-sdk-18.0.1
D:\software\jdk\javafx-jmods-18.0.1
```

## 安装WiX Toolset

这部分对应下图中的Wix的部分：

{:refdef: style="text-align: center;"}
![Packaging Prerequisite](/assets/image/pipeline/jpackage-prerequisite.png)
{: refdef}

WiX Toolset is an **open-source project**, developed by **Microsoft** and it is being maintained by Rob Mensching.
It provides you a set of tools to create **Windows Installer Packages** from XML Source Code.

### 下载

下载地址：

```text
https://wixtoolset.org/releases/
```

### 安装

下载成功之后，得到`wix311.exe`文件：

{:refdef: style="text-align: center;"}
![wix311.exe](/assets/image/pipeline/wix-311-exe.png)
{: refdef}

进行安装。

### 配置环境变量

在环境变量`Path`中添加：

```text
C:\Program Files (x86)\WiX Toolset v3.11\bin
```

例如，在Win 10操作系统下，配置`Path`环境变量：

{:refdef: style="text-align: center;"}
![wix311.exe](/assets/image/pipeline/win10-env-path-add-wix-toolset.png)
{: refdef}

## 生成exe

第一步，切换到`target`目录，打开`cmd`命令行，执行下面两条命令设置环境变量：

```text
set PATH_TO_FX="X:\path\to\javafx-sdk-<version>\lib"
set PATH_TO_FX_MODS="X:\path\to\javafx-jmods-<version>"
```

注意，路径修改为正确的值，例如：

```text
set PATH_TO_FX="D:\software\jdk\javafx-sdk-18.0.1\lib"
set PATH_TO_FX_MODS="D:\software\jdk\javafx-jmods-18.0.1"
```

第二步，执行`jpackage`命令生成exe文件：

```text
jpackage --type exe --dest installer --input libs ^
--main-jar jm-data-excel-gui-fx-1.0-SNAPSHOT.jar ^
--main-class jm.data.excel.gui.fx.Main ^
--module-path %PATH_TO_FX_MODS% ^
--add-modules javafx.base,javafx.controls,javafx.fxml,javafx.graphics ^
--win-menu --win-shortcut --win-dir-chooser ^
--win-menu-group JinMa ^
--name JMExcelCheck ^
--app-version 1.0.5 ^
--vendor 保定市金马漏水检测有限公司 ^
--icon ..\src\main\resources\images\jm-logo.ico
```

注意检查事项：

- 第一，有没有将`--main-jar`指定的Jar包（例如，`jm-data-excel-gui-fx-1.0-SNAPSHOT.jar`）放到`--input`指定的目录（例如，`libs`）
- 第二，`--main-jar`和`--main-class`的值是否写正确。
- 第三，`--app-version`是否需要更新
- 第四，`--add-modules`是否需要添加新的内容，例如`javafx.web`。

<div class="w3-panel w3-pale-green w3-bottombar w3-border-green w3-border">
    <p>通常，在使用Windows命令行时，当输入一个命令后回车代表执行该命令。</p>
    <p>但是，有时命令过长或其他原因，我们想在命令中换行，怎么办呢？</p>
    <p>这时，可以在一行末尾加“^”号再回车，代表命令还要继续。</p>
</div>

在`--add-modules`中，如果不包含`javafx.web`，生成`exe`的体积45MB；
如果包含`javafx.web`，生成`exe`的体积70MB，体积变化有点大。
引入`javafx.web`，会让程序功能更丰富，我还没有想好怎么使用，或者说不太会用它：

```text
jpackage --type exe --dest installer --input libs ^
--main-jar jm-data-excel-gui-fx-1.0-SNAPSHOT.jar ^
--main-class jm.data.excel.gui.fx.Main ^
--module-path %PATH_TO_FX_MODS% ^
--add-modules javafx.base,javafx.controls,javafx.fxml,javafx.graphics,javafx.web ^
--win-menu --win-shortcut --win-dir-chooser ^
--win-menu-group JinMa ^
--name JMExcelCheck ^
--app-version 1.0.5 ^
--vendor 保定市金马漏水检测有限公司 ^
--icon ..\src\main\resources\images\jm-logo.ico
```

{:refdef: style="text-align: center;"}
![生成exe](/assets/image/pipeline/jpackage-application-to-exe.gif)
{: refdef}

执行完成之后，会生成exe文件：

{:refdef: style="text-align: center;"}
![JMExcelCheck-1.0.exe](/assets/image/pipeline/installer-jm-excel-check-exe.png)
{: refdef}
