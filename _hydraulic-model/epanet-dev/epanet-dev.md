---
title:  "EPANET: Dev"
sequence: 004
---



## Load

```java
import com.sun.jna.Library;
import com.sun.jna.Native;

public interface EpaNet2Library extends Library {
    EpaNet2Library INSTANCE = Native.load("D:\\software\\lib\\EPANET.dll", EpaNet2Library.class);
}
```

```java
public class EpaNetRun {
    public static void main(String[] args) {
        EpaNet2Library instance = EpaNet2Library.INSTANCE;
        System.out.println(instance);
    }
}
```

```text
Proxy interface to Native Library <D:\software\lib\EPANET.dll@140716846219264>
```

## Debug

```text
System.setProperty("jna.debug_load", "true");
```

```java
public class EpaNetRun {
    public static void main(String[] args) {
        System.setProperty("jna.debug_load", "true");
        EpaNet2Library instance = EpaNet2Library.INSTANCE;
        System.out.println(instance);
    }
}
```

## Find Lib

Use `-Djna.library.path=xxx` on JVM launch.

```text
System.setProperty("jna.library.path", "D:\\lib");
```

```java
import com.sun.jna.Library;
import com.sun.jna.Native;

public interface EpaNet2Library extends Library {
    // 注意：使用了EPANET，而没有加.dll后缀；加上也没有错
    EpaNet2Library INSTANCE = Native.load("EPANET", EpaNet2Library.class);
}
```

```java
public class EpaNetRun {
    public static void main(String[] args) {
        System.setProperty("jna.debug_load", "true");
        System.setProperty("jna.library.path", "D:\\software\\lib");
        EpaNet2Library instance = EpaNet2Library.INSTANCE;
        System.out.println(instance);
    }
}
```

## 错误

### 不是有效的 win32 程序

- 报错：%1 不是有效的 win32 程序
- 问题原因：系统和jdk都是64位的，加载的库是32位的
- 解决办法：换成相同位数的库

## Reference

编译：

- [64-bit resources for EPANET developers](http://epanet.de/developer/64bit.html.en)

数据：

- 

x86_64-w64-mingw32-gcc -c epanet.c hydcoeffs.c inpfile.c main.c quality.c rules.c epanet2.c hydraul.c input1.c mempool.c qualreact.c smatrix.c genmmd.c hydsolver.c input2.c output.c qualroute.c hash.c hydstatus.c input3.c project.c report.c

代码：

- epanet2.2_toolkit中的owa_epanet.chm和epanet2.h
- Libro-Iniciacion-Toolkit-de-Epanet-ingles.pdf文件
- 由JNAerator生成的epanet2.jar
- [jhawanet/epajava](https://github.com/jhawanet/epajava)的epajava.jar，也是基于JNA
- [rafaelalmeida/jgrasstools: epanet/core/](https://github.com/rafaelalmeida/jgrasstools/tree/master/hortonmachine/src/main/java/org/jgrasstools/hortonmachine/modules/networktools/epanet/core)
   - [EpanetWrapper.java](https://github.com/rafaelalmeida/jgrasstools/blob/master/hortonmachine/src/main/java/org/jgrasstools/hortonmachine/modules/networktools/epanet/core/EpanetWrapper.java)
- Baseform-Epanet-Java-Library
- [OpenWaterAnalytics/epanet-dev](https://github.com/OpenWaterAnalytics/epanet-dev)

