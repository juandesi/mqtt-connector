---
layout: default
title: Authentication
nav_order: 2
parent: Security
---

# Authentication
Authentication is the process of verifying an user identity. The MQTT connector provides different way to authenticate with MQTT brokers and it is possible to support multiple authentication schemes at once.

## Simple Authentication

MQTT provides username/password authentication as part of the protocol. Be sure to use network encryption if you are using this option otherwise the username and password will be vulnerable to interception. 

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
    <mqtt:mqtt5-connection host="test.mosquitto.org" port="8883">
        <mqtt:simple-auth username="diegod" password="LOS"/>
    </mqtt:mqtt5-connection>
</mqtt:config>
```

  {% endcapture %}
  {% include tabs.html tab_group="module" %}

---

In `MQTT5` both `username` and `password` are **optional** properties, but at least one
is required if using simple authentication.

| Parameter | Description |
| ----------- | ----------- |
| `username` | username to uniquely identify with the broker. **optional** |
| `password` | string of characters used for authenticating a user on a computer system. **optional**  |

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
    <mqtt:mqtt3-connection host="test.mosquitto.org" port="8883">
        <mqtt:simple-auth username="juanito" password="complex"/>
    </mqtt:mqtt3-connection>
</mqtt:config>
```

  {% endcapture %}
  {% include tabs.html tab_group="module" %}


| Parameter | Description |
| ----------- | ----------- |
| `username` | username to uniquely identify with the broker. Username is **required** if using simple auth on MQTT3|
| `password` | string of characters used for authenticating a user on a computer system. Password is **optional**  |

{% endcapture %}
{% include tabs.html tab_group="mqtt-version" %}

***

## TLS Mutual Authentication

...