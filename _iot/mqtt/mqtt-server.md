---
title: "MQTT Server"
sequence: 101
---

## EMQX 移动云

### 连接

- IP: `36.138.170.195`
- Port: `1883`
- Topic: `/sys/shengda/flowmeter/thing/event/property`

### UI 界面

UI界面：

- URL: [http://36.138.170.195:18083](http://36.138.170.195:18083)



## docker

```text
docker run -d --name emqx -p 1883:1883 -p 8083:8083 -p 8084:8084 -p 8883:8883 -p 18083:18083 emqx/emqx:latest
```

## docker compose

```text
$ cat docker-compose.yml 
services:
  emqx:
    image: emqx/emqx
    container_name: emqx_liusen
    ports:
     - 1883:1883
     - 8083:8083
     - 8084:8084
     - 8883:8883
     - 18083:18083
    restart: always
```

