---
layout: default
title: Advanced
parent: Connection
nav_order: 3
---

# Advanced Connection Configuration

With the advanced configuration properties you can adjust various settings to optimize resource management on the MQTT broker side for a particular connection.


{% capture tab_content %}

Studio
===
![advanced]({{ site.baseurl }}/images/advanced.png)
====

Code
===

```xml
<mqtt:config name="MQTT5">
<mqtt:mqtt5-connection host="test.mosquitto.org" port="1883" 
            clientId="TestIdentifier" cleanSession="true"/>
</mqtt:config>
```

{% endcapture %}
{% include tabs.html tab_group="module" %}

---

| Parameter | Description | Default value |
| ----------- | ----------- | ------------- |
| `keepAlive` | Time interval in which the client sends a ping to the broker if no other MQTT packets are sent during this period of time. It is used to determine if the connection is still up. | `60` |
| `keepAliveUnit` | The time unit used to interpret the `keepAlive` value. | `SECONDS` |
| `connectTimeout` | The timeout between sending the Connect and receiving the ConnAck message. | - |
| `connectTimeoutUnit` | The time unit used to interpret the `connectTimeout` value. | `SECONDS` |
