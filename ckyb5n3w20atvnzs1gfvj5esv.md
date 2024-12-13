---
title: "$SYS topic in MQTT"
datePublished: Wed Jan 12 2022 06:21:25 GMT+0000 (Coordinated Universal Time)
cuid: ckyb5n3w20atvnzs1gfvj5esv
slug: dollarsys-topic-in-mqtt
cover: https://cdn.hashnode.com/res/hashnode/image/unsplash/FO7JIlwjOtU/upload/v1641885037909/TLF5n2XH3.jpeg
tags: iot, internet-of-things

---

This is a reserved topic and is implemented by most MQTT and used to publish information about the broker.
They are read-only topics for the MQTT clients. There is no standard for topic structure but have [guides](https://github.com/mqtt/mqtt.org/wiki/SYS-Topics) 
Some of the Topics are Static which means Messages on a static $SYS topic are not required to be sent on every $SYS topic update interval. These messages are sent once the broker subscribes to the $SYS topic. Mark this topic with Static keyword
### Required Topics
Every broker which claims to support the $SYS topics should support these topics.

**Topics List**:

- The total number of bytes received since the broker started.
```
$SYS/broker/load/bytes/received
```
- The total number of bytes sent since the broker started.
```
$SYS/broker/load/bytes/sent
```
- The number of currently connected clients.
```
$SYS/broker/clients/connected
```
- The total number of persistent clients (with clean session disabled) that are registered at the broker but are currently disconnected.
```
$SYS/broker/clients/disconnected
```
- The maximum number of active clients that have been connected to the broker. This is only calculated when the $SYS topic tree is updated, so short lived client connections may not be counted.
```
$SYS/broker/clients/maximum
```
- The total number of connected and disconnected clients with a persistent session currently connected and registered on the broker.
```
$SYS/broker/clients/total
```
- The total number of messages of any type received since the broker started.
```
$SYS/broker/messages/received
```
- The total number of messages of any type sent since the broker start.
```
$SYS/broker/messages/sent
```
- The total number of publish messages that been dropped due to inflight/queuing limits.
```
$SYS/broker/messages/publish/dropped
```
- The total number of PUBLISH messages received since the broker started.
```
$SYS/broker/messages/publish/received
```
- The total number of PUBLISG messages sent since the broker started.
```
$SYS/broker/messages/publish/sent
```
- The total numbers of retained messages active on broker.
```
$SYS/broker/messages/retained/count
```
- The total number of subscriptions active on broker.
```
$SYS/broker/subscriptions/count
```
- The current time on the server.
```
$SYS/broker/time
```
- The amount of time in seconds the broker has been online.
```
$SYS/broker/uptime
```
- The version of the broker. Static.
```
$SYS/broker/version
```

### Optional Topics:
A broker implementation may decide if it implements an optional topic. Static.

- The repository changeset (revision) associated with build. Static
```
$SYS/broker/changeset
```
- When bridges are configured to/from the broker, common practice is to provide a status topic that indicates the state of the connection. This is provided within $SYS/broker/bridge/ by default. If the value of the topic is 1 the connection is active, if 0 then it is not active.
```
$SYS/broker/bridge/#
```
- The moving average of the number of CONNECT packets received by the broker over different time intervals. The final "+" of the hierarchy can be 1min, 5min or 15min. The value returned represents the number of connections received in 1 minute, averaged over 1, 5 or 15 minutes.
```
$SYS/broker/load/connections/+
```
- The moving average of the number of bytes received by the broker over different time intervals. The final "+" of the hierarchy can be 1min, 5min or 15min. The value returned represents the number of bytes received in 1 minute, averaged over 1, 5 or 15 minutes.
```
$SYS/broker/load/bytes/received/+
```
- The moving average of the number of bytes sent by the broker over different time intervals. The final "+" of the hierarchy can be 1min, 5min or 15min. The value returned represents the number of bytes sent in 1 minute, averaged over 1, 5 or 15 minutes.
```
$SYS/broker/load/bytes/sent/+
```
- The moving average of the number of all types of MQTT messages received by the broker over different time intervals. The final "+" of the hierarchy can be 1min, 5min or 15min. The value returned represents the number of messages received in 1 minute, averaged over 1, 5 or 15 minutes.
```
$SYS/broker/load/messages/received/+
```
- The moving average of the number of all types of MQTT messages sent by the broker over different time intervals. The final "+" of the hierarchy can be 1min, 5min or 15min. The value returned represents the number of messages send in 1 minute, averaged over 1, 5 or 15 minutes.
```
$SYS/broker/load/messages/sent/+
```

- The moving average of the number of publish messages dropped by the broker over different time intervals. This shows the rate at which durable clients that are disconnected are losing messages. The final "+" of the hierarchy can be 1min, 5min or 15min. The value returned represents the number of messages dropped in 1 minute, averaged over 1, 5 or 15 minutes.
```
$SYS/broker/load/publish/dropped/+
```

- The moving average of the number of publish messages received by the broker over different time intervals. The final "+" of the hierarchy can be 1min, 5min or 15min. The value returned represents the number of publish messages received in 1 minute, averaged over 1, 5 or 15 minutes.
```
$SYS/broker/load/publish/received/+
```

- The moving average of the number of publish messages sent by the broker over different time intervals. The final "+" of the hierarchy can be 1min, 5min or 15min. The value returned represents the number of publish messages sent in 1 minute, averaged over 1, 5 or 15 minutes.
```
$SYS/broker/load/publish/sent/+
```

- The moving average of the number of socket connections opened to the broker over different time intervals. The final "+" of the hierarchy can be 1min, 5min or 15min. The value returned represents the number of socket connections in 1 minute, averaged over 1, 5 or 15 minutes.
```
$SYS/broker/load/sockets/+
```

- The number of messages with QoS>0 that are awaiting acknowledgments.
```
$SYS/broker/messages/inflight
```

- The number of messages currently held in the message store. This includes retained messages and messages queued for durable clients.
```
$SYS/broker/messages/stored
```

- The timestamp at which this particular build of the broker was made. Static.
```
$SYS/broker/timestamp
```

- Get Client IP.
```
$SYS/clients/[client-id]/ip
```
- Get Client Connected Time.
```
$SYS/clients/[client-id]/connectedtime
```
