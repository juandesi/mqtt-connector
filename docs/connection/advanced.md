---
layout: default
title: Advanced
parent: Connection
nav_order: 3
---

# Advanced Connection Configuration

The advanced connection configuration enables the user to configure timeouts and reconnection options.

#### Example Advanced Settings
The example is for MQTT5, but the same properties apply for MQTT3
{: .fs-2 }
{% capture tab_content %}

Studio
===
![advanced]({{ site.baseurl }}/images/advanced.png)
====

Code
===

```xml
<mqtt:config name="MQTT5">
    <mqtt:mqtt5-connection host="test.mosquitto.org" keepAlive="10" connectTimeout="10">
        <reconnection failsDeployment="true">
            <reconnect frequency="2000" count="2"/>
        </reconnection>
    </mqtt:mqtt5-connection>
</mqtt:config>
```

{% endcapture %}
{% include tabs.html tab_group="module" %}

---

## Timeout Properties

### Keep Alive

Time interval in which the client sends a ping to the broker if no other MQTT packets are sent during this period of time. It is used to determine if the connection is still up. the Keep Alive Unit property qualifies the Keep Alive attribute

| Property | Default value | Expression |
| ----------- | ----------- | ------------- |
| `keepAlive` | `60` | `not supported`|
| `keepAliveUnit` | `SECONDS` | `not supported`|

### Connect Timeout

The timeout between sending the Connect and receiving the ConnAck message. The Connect Timeout Unit property qualifies the Connect Timeout attribute

| Property | Default value | Expression |
| ----------- | ----------- | ------------- |
| `connectTimeout` | - | `not supported`|
| `connectTimeoutUnit` | `SECONDS` | `not supported`|

## Reconnection

Mule provide out-of-the-box reconnection strategies to be applied to all connectors that work with connections. 

When an operation in a fails to connect to the broker, the default behavior is for the operation to fail immediately and return a connectivity error.

This default behavior can be modified by configuring a reconnection strategy for the operation.

You can configure a reconnection strategy for an operation either by modifying the operation properties or by modifying the connection configuration (this case).

### Fails Deployment

When the application is deployed, a connectivity test is performed on all connectors. If set to true, deployment fails if the test doesn’t pass after exhausting the associated reconnection strategy

| Parameter | Description | Expression |
| ----------- | ----------- | ------ |
| `failsDeployment` | `false` | `not supported`|

### Reconnection Strategy

Defines the reconnection strategy to use: None, Standard or Forever

* **None**

Is the default behavior, which immediately returns a connectivity error if the attempt to connect is unsuccessful

* **Standard** (reconnect)

Sets the number of reconnection attempts and the interval at which to execute them before returning a connectivity error

* **Forever** (reconnect-forever)

Attempts to reconnect continually at a given interval