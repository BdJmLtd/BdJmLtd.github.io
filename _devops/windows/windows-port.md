---
title: "查看端口（Windows）"
sequence: '001'
---

查询端口：

```text
netstat -ano
```

查询指定端口

```text
netstat -ano | findstr "端口号"
```

根据进程PID查询进程名称：

```text
tasklist | findstr "进程PID号"
```

根据PID结束进程：

```text
taskkill -f -pid "进程PID号"
```
