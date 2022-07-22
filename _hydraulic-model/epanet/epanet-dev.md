---
title:  "EPANET: Dev"
sequence: 003
---

## API

The procedure for working with these functions is as follows:

1. Use the `ENopen` function to open the Epanet library, which will enable the
   rest of the functions, except the ENepanet function.
2. Use the `ENsetxxx` functions to change the properties of elements or
   characteristics of the network or use the `ENgetxxx` functions to retrieve data
   from the network saved in the input file (file with `inp` extension).
3. For a complete simulation use the `ENsolveH` function  (this function
   automatically saves the results in a hydraulic-results file), or if a step-by-step
   simulation is desired use the following sequence of functions: `ENopenH`,
   `ENinitH`, `ENrunH`, `ENnextH`, `ENcloseH`, and access the results through the `ENgetxxx` function series.
4. The `ENsolveQ` function runs a complete simulation of a water quality model
   (this function automatically saves the hydraulic and water quality results in an output file),
   or if running the simulation step-by-step, use the following
   functions sequence: `ENopenQ`, `ENinitQ`, `ENrunQ`, `ENnextQ`, `ENcloseQ`,
   and access the results through the `ENgetxxx` function series.
5. If running new analyses is desired, return to step 2 or use the `ENreport`
   function to save a results report formatted in the results report file.
6. Call the `ENclose` function to close the Epanet file that was opened initially,
   this frees up the memory that was occupied on the computer.

To sum up, with the Epanet API we can do the following tasks:

1. Open and close the Toolkit
2. Retrieve and set network parameters
3. Run a hydraulic simulation
4. Run a water quality simulation
5. Retrieve results
6. Generate a results report

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

