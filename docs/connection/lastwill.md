---
layout: default
title: Last Will
parent: Connection
nav_order: 2
---

# Last Will and Testament

The Last Will and Testament (LWT), also known as 'will publish message', is the message that's published by the broker if the client disconnected ungracefully or with the reason code `DISCONNECT_WITH_WILL_MESSAGE`.

The only mandatory properties for a 'will publish message' are `topic` and `message`, all others have defaults or are optional.

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

---

| Property | Values | Default | MQTT Specification |
| -------- | ------ | ------- | ------------------ |
| `topic` | `String`/`MqttTopic` | mandatory | [3.1.3.3](https://docs.oasis-open.org/mqtt/mqtt/v5.0/os/mqtt-v5.0-os.html#_Toc3901069){:target="_blank"} |
| `qos` | `MqttQos` | `AT_MOST_ONCE` | [3.1.2.6](https://docs.oasis-open.org/mqtt/mqtt/v5.0/os/mqtt-v5.0-os.html#_Toc3901041){:target="_blank"} |
| `payload` | `byte[]`/`ByteBuffer` | - | [3.1.3.4](https://docs.oasis-open.org/mqtt/mqtt/v5.0/os/mqtt-v5.0-os.html#_Toc3901070){:target="_blank"} |
| `retain` | `true`/`false` | `false` | [3.1.2.7](https://docs.oasis-open.org/mqtt/mqtt/v5.0/os/mqtt-v5.0-os.html#_Toc3901042){:target="_blank"} |
| `messageExpiryInterval` | [`0` - `4_294_967_295`] | - | [3.1.3.2.4](https://docs.oasis-open.org/mqtt/mqtt/v5.0/os/mqtt-v5.0-os.html#_Toc3901064){:target="_blank"} |
| `delayInterval` | [`0` - `4_294_967_295`] | `0` | [3.1.3.2.2](https://docs.oasis-open.org/mqtt/mqtt/v5.0/os/mqtt-v5.0-os.html#_Toc3901062){:target="_blank"} |
| `payloadFormatIndicator` | `Mqtt5PayloadFormatIndicator` | - | [3.1.3.2.3](https://docs.oasis-open.org/mqtt/mqtt/v5.0/os/mqtt-v5.0-os.html#_Toc3901063){:target="_blank"} |
| `contentType` | `String`/`MqttUtf8String` | - | [3.1.3.2.5](https://docs.oasis-open.org/mqtt/mqtt/v5.0/os/mqtt-v5.0-os.html#_Toc3901065){:target="_blank"} |
| `responseTopic` | `String`/`MqttTopic` | - | [3.1.3.2.6](https://docs.oasis-open.org/mqtt/mqtt/v5.0/os/mqtt-v5.0-os.html#_Toc3901066){:target="_blank"} |
| `correlationData` | `byte[]`/`ByteBuffer` | - | [3.1.3.2.7](https://docs.oasis-open.org/mqtt/mqtt/v5.0/os/mqtt-v5.0-os.html#_Toc3901067){:target="_blank"} |
| `userProperties` | `Mqtt5UserProperties` | - | [3.1.3.2.8](https://docs.oasis-open.org/mqtt/mqtt/v5.0/os/mqtt-v5.0-os.html#_Toc3901068){:target="_blank"} |

Message expiry can be disabled (the default).

All properties of a Will publish message are the same as of a normal publish message with the 
addition of the `delayInterval`

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

---

| Property | Values | Default | MQTT Specification |
| -------- | ------ | ------- | ------------------ |
| `topic` | `String`/`MqttTopic` | mandatory | [3.1.3.3](https://docs.oasis-open.org/mqtt/mqtt/v5.0/os/mqtt-v5.0-os.html#_Toc3901069){:target="_blank"} |
| `qos` | `MqttQos` | `AT_MOST_ONCE` | [3.1.2.6](https://docs.oasis-open.org/mqtt/mqtt/v5.0/os/mqtt-v5.0-os.html#_Toc3901041){:target="_blank"} |
| `payload` | `byte[]`/`ByteBuffer` | - | [3.1.3.4](https://docs.oasis-open.org/mqtt/mqtt/v5.0/os/mqtt-v5.0-os.html#_Toc3901070){:target="_blank"} |
| `retain` | `true`/`false` | `false` | [3.1.2.7](https://docs.oasis-open.org/mqtt/mqtt/v5.0/os/mqtt-v5.0-os.html#_Toc3901042){:target="_blank"} |

{% endcapture %}
{% include tabs.html tab_group="mqtt-version" %}
