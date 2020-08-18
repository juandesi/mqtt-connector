---
layout: default
title: Connection
nav_order: 3
redirect_from: /docs/client_configuration.html
---

# Connection

A MQTT connection declaration declares the MQTT broker/server that will receive and send the MQTT messages and also more information of how that connection is established.

There are 2 types of connections: `MQTT 5` and `MQTT 3`. The configuration is pretty similar, we will see later that `MQTT 5` delivers more features than `MQTT 3`.

## General Configuration


{% capture tab_content %}

MQTT 5
===

  {% capture tab_content %}
  
  Studio
  ===
![mqtt5-connection]({{ site.url }}/images/3-connection-mqtt5.png)
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

====

MQTT 3
===

  {% capture tab_content %}
  
  Studio
  ===
![mqtt3-connection]({{ site.url }}/images/3-connection-mqtt3.png)

  ====

  Code
  ===

```xml
<mqtt:config name="MQTT3">
  <mqtt:mqtt3-connection host="test.mosquitto.org" port="1883" 
             clientId="TestIdentifier" cleanSession="true"/>
</mqtt:config>
```

  {% endcapture %}
  {% include tabs.html tab_group="module" %}


{% endcapture %}
{% include tabs.html tab_group="mqtt-version" %}