---
title: "Modbus VS. MQTT"
sequence: 112
---

IoT gateway protocol **MQTT** and **Modbus**:

- Local protocol **Modbus** for short-distance device connection and 
- extensible Internet protocol "Message Queuing Telemetry Transmission (**MQTT**)" that supports the Internet of Things for global communication.

```text
Modbus 适合短距离传输；MQTT 适合长距离传输。
```

What is the difference between the two gateway protocols.

{:refdef: style="text-align: center;"}
![](/assets/image/iot/modbus-vs-mqtt.png)
{: refdef}

## Modbus protocol

Modbus has evolved into a comprehensive set of protocols supporting multiple physical links (such as RS-485).

```text
Modbus 是一个应用层的协议，它可以在不同的物理层（physical links）上
```

The core of Modbus is a serial communication protocol, using **master-slave mode**.
The host sends a request to the slave, and the slave responses.

```text
Modbus 的工作方式是 master-slave
```

In a standard Modbus network, there is one master and a maximum of 247 slaves
(however, if 2-byte addressing is used, this limit can be significantly increased).

```text
master 和 slave 的数量对应关系：1 vs 247
```

With RS-485, the communication between the master and the slave occurs in the frame indicating the function code.
The function code can identify the function to be operated, such as reading independent input;
reading first-in first-out queue; or executing diagnostic function.
Then, the slave responds according to the received function code.
The response is relatively simple and is indicated by a set of bytes.
Therefore, the slave can be a smart device or a simple device with only one sensor.

```text
master 和 slave 的沟通过程
```

From this description, you can see that the Modbus protocol is very simple,
but its openness as a protocol makes it the actual communication protocol for the entire industry or SCADA system.

```text
Modbus 协议正是因为简单，所以应用广泛
```

## MQTT

```text
MQTT = message queue telemetry transmission
```

MQTT is an open and lightweight machine-to-machine protocol, designed for IoT interaction.

The MQTT network contains an MQTT broker, which is responsible for coordinating the interaction between MQTT brokers.
The agent is a publisher, responsible for publishing information for users.

MQTT has very few requirements because it is designed for embedded devices with limited resources.
In addition to occupying less space,
MQTT can also provide excellent communication efficiency (even through a low-bandwidth network for communication)
and very little overhead (compared to protocols such as HTTP).
In 3G networks, the throughput speed of MQTT is 93 times that of Representational State Transfer (REST) using HTTP.

MQTT can use the least method to indicate the operation to be implemented on a specific topic,
and then implement the publish/subscribe model.
The agent first connects to the broker, and then publish or subscribe to the topic.
Upon completion, the agent will be disconnected from the broker. MQTT method definition:

## Reference

- [What is the difference between MQTT protocol and Modbus protocol](https://www.zoko-link.com/Product-knowledge/MQTT-Modbus-protocol.html)
