---
title: "查看端口（Linux）"
sequence: '001'
---

根据命令查询：

```text
ps -ef | grep "java -jar"
```

查询端口：

```text
netstat -nltp
```

查询指定端口：

```text
netstat -nltp | grep "端口号"
```

根据PID结束进程：

```text
kill -9 "进程PID号"
```
