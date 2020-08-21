---
layout: default
title: Quick Start
nav_order: 1
---

# Quick Start!

The following contains a simple example on how to add the connector to your project, connect to a broker, then subscribe to a topic and publish messages to the same topic using the MQTT 3.
{: .fs-5 .fw-300 }

## Add the MQTT connector to your project

Include the following Maven dependency:

```xml
<dependency>
    <groupId>desi.juan</groupId>
    <artifactId>mule-mqtt-connector</artifactId>
    <version>1.0.0</version>
    <classifier>mule-plugin</classifier>
</dependency>
```
See the [Installation](2_installation.md) section for more information.
{: .fs-3 }

## Connecting to the broker

First let's connect to an actual broker. The following example shows how to connect to the **test.mosquitto.org** broker, which is a [publicly available MQTT broker](https://test.mosquitto.org/).  

To achieve this let's set up the host with the following value: `test.mosquitto.org`

Like this:

## Subscribing to a topic

Now that the test connectivity execution to the broker was successful, you can setup a subscription. We will add a logger after the **On New Message** to log the published messages.

## Publishing to the subscribed topic

Similar to subscribing, once you have a connected configuration, you can also publish messages to the just subscribed topic.

In this case, let's publish to the subscribed topic and add an scheduler to trigger the flow.

## Run the application

Now go and run your app! You'll start to see logged messages in the subscription flow that are being published by your publish flow. 

That's all!