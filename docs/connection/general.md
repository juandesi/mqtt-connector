---
layout: default
title: General
parent: Connection
nav_order: 1
---

# General Configuration


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