---
layout: default
title: Operations
has_children: true
nav_order: 6
---

# Operations

MQTT is a **publish/subscribe** protocol that allows edge-of-network devices to send a message to a broker. Clients connect to this broker, which then mediates communication between the two or more devices. Each device can register to one or more topics.

In MQTT the process of sending messages is called **publishing**, and to receive messages an MQTT client must **subscribe** to an MQTT topic.

This defines 2 operations: `PUBLISH` and `SUBSCRIBE`

[Learn more about MQTT operations](https://www.hivemq.com/blog/mqtt-essentials-part-4-mqtt-publish-subscribe-unsubscribe/){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 }
