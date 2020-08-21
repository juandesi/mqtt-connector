---
layout: default
title: General
parent: Connection
nav_order: 1
---

# General Configuration
The general connection configuration declares the most common and often used properties to stablish an MQTT connection with a broker.

You can connect with a MQTT broker by only providing the `host` parameter; all other parameters will use default values as defined in the MQTT specification. If not defined there, reasonable default values will be used. 

#### General Configuration Example
{% capture tab_content %}

MQTT 5
===

  {% capture tab_content %}
  
  Studio
  ===
![mqtt5-connection]({{ site.baseurl }}/images/3-connection-mqtt5.png)
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
![mqtt3-connection]({{ site.baseurl }}/images/3-connection-mqtt3.png)
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

---

The properties described in this section can be seen in the following table:

| Property | Description | Default value | Expression |
| ----------- | ----------- | ------------- | ------- |
| `host` | The host name or IP address of the MQTT server. | - | `not supported` |
| `port` | The port of the MQTT server. | `1883` | `not supported` |
| `identifier` | The unique identifier of the MQTT client. | connector generates an identifier | `not supported` |
| `cleanSession` | Determines if the client wants to start a new “clean” session (true) or wants to resume a previous session if available (false). This is called cleanStart in MQTT5. | `true` | `not supported` |

Good Practice
{: .label }

For connections with `cleanSession = true` it's a good practice to have a separate configuration for subscribers, will avoid problems with fetching previous session queued messages.