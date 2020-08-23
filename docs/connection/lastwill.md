---
layout: default
title: Last Will
parent: Connection
nav_order: 2
---

# Last Will and Testament

The Last Will and Testament (LWT), also known as 'will publish message', is the message that's published by the broker if the client disconnected ungracefully or with the reason code `DISCONNECT_WITH_WILL_MESSAGE`.

The only mandatory properties for a 'will publish message' are `topic` and `message`, all others have defaults or are optional.

#### Example Last Will and Testament Configuration
{% capture tab_content %}

MQTT 5
===

  {% capture tab_content %}
  
  Studio
  ===
![mqtt5-will]({{ site.baseurl }}/images/mqtt5-will.png)
  ====

  Code
  ===

```xml
<mqtt:config name="MQTT5">
  <mqtt:mqtt5-connection host="test.mosquitto.org">
    <mqtt:mqtt5-will message="I'm out!" topic="topic/will" contentType="text/plain" 
                     qosLevel="AT_LEAST_ONCE" correlationData="data1" messageExpiryInterval="30"
                     payloadFormatIndicator="UTF8" responseTopic="response/topic" 
                     delayInterval="10" retain="true">
      <mqtt:user-properties >
        <mqtt:user-property key="custom" value="property" />
      </mqtt:user-properties>
    </mqtt:mqtt5-will>
  </mqtt:mqtt5-connection>
</mqtt:config>
```

  {% endcapture %}
  {% include tabs.html tab_group="module" %}

---

All properties of a Will publish message are the same as of a normal publish message for MQTT5 with the 
addition of the `delayInterval`, described below.

| Property | Description | Expression |
| ----------- | ----------- | ------- |
| `delayInterval` | The Server delays publishing the Will Message until the Will `delayInterval` has passed or the Session ends, whichever happens first. If a new Network Connection to this Session is made before the Will `delayInterval` has passed, the Server MUST NOT send the Will Message | `not supported` |

====

MQTT 3
===

  {% capture tab_content %}
  
  Studio
  ===
![mqtt3-will]({{ site.baseurl }}/images/mqtt3-will.png)
  ====

  Code
  ===

```xml
<mqtt:config name="MQTT3">
  <mqtt:mqtt3-connection host="test.mosquitto.org">
    <mqtt:mqtt3-will message="I'm out !" topic="test/mule/topic" 
                     retain="true" qosLevel="EXACTLY_ONE"/>
  </mqtt:mqtt3-connection>
</mqtt:config>
```

  {% endcapture %}
  {% include tabs.html tab_group="module" %}

---

All properties of a Will publish message are the same as of a normal publish message for MQTT3.

{% endcapture %}
{% include tabs.html tab_group="mqtt-version" %}

The difference between MQTT Publish properties and Will message properties is that the later properties **do not** support expressions, because this would generate dynamic connections for each different will message property set.
