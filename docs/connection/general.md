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
![mqtt5-connection]({{ site.baseurl }}/images/mqtt5-connection.png)
  ====

  Code
  ===

```xml
<mqtt:config name="MQTT5">
  <mqtt:mqtt5-connection host="test.mosquitto.org" port="1883" clientId="TestIdentifier"
                         cleanStart="TRUE" sessionExpiryInterval="60"/>
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
![mqtt3-connection]({{ site.baseurl }}/images/mqtt3-connection.png)
  ====

  Code
  ===

```xml
<mqtt:config name="MQTT3">
  <mqtt:mqtt3-connection host="test.mosquitto.org" port="1883" 
                         clientId="TestIdentifier" cleanSession="TRUE"/>
</mqtt:config>
```

  {% endcapture %}
  {% include tabs.html tab_group="module" %}

{% endcapture %}
{% include tabs.html tab_group="mqtt-version" %}

---

## Host

The host name or IP address of the MQTT server.

| Property | Default value | Expression |
| ----------- | ------------- | ------- |
| `host` | - | `not supported` |

## Port

The port of the MQTT server.

| Property | Default value | Expression |
| ----------- | ------------- | ------- |
| `port` | `1883` | `not supported` |

## Identifier

The unique identifier of the MQTT client.

| Property | Default value | Expression |
| ----------- | ------------- | ------- |
| `identifier` | connector generates an identifier | `not supported` |


{% capture tab_content %}

MQTT 5.0
===

## Clean Start

If `true` and there is a session associated with the configured `clientId`, the server must resume communication with the client based on the state of the session. If there is no session associated with the `clientId`, the server must create a new session. 

If set to `false` a new session is always created.

| Property | Default value | Expression |
| ----------- | ------------- | ------- |
| `cleanStart` | `TRUE` | `not supported` |

It's important to note that if the [sessionExpiryInterval](#session-expiry-interval) property is empty or 0, then sessions are n  ot going to be stored for the client.
{: .fs-2 }

## Session Expiry Interval

 Defines the period of time that the broker stores the session information of that particular MQTT client. When the session expiry interval is set to 0 or empty, the session information is immediately removed from the broker as soon as the network connection of the client closes. The Session Expiry Interval Unit property qualifies the Connect Timeout attribute

| Property | Default value | Expression |
| ----------- | ------------- | ------- |
| `sessionExpiryInterval` | `60` | `not supported` |
| `sessionExpiryIntervalUnit` | `SECONDS` | `not supported` |

====

MQTT 3.1.1
===

## Clean Session

Determines if the client wants to start a new “clean” session (true) or wants to resume a previous session if available (false).

| Property | Default value | Expression |
| ----------- | ------------- | ------- |
| `cleanSession` | `TRUE` | `not supported` |

{% endcapture %}{% include tabs.html tab_group="mqtt-version" tab_no_header=true %}

