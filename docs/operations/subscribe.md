---
layout: default
title: Subscribe 
parent: Operations
nav_order: 2
---

# On New Message 

Publishing a message doesn’t make sense if no one ever receives it. In other words, if there are no clients to subscribe to the topics of the messages. To receive messages on topics of interest the client can Subscribe on the MQTT broker to the topics of interest. In the MQTT Connector the **On New Message** source, enables the capability to subscribe to any number of topics an trigger a flow execution for each new message received.

{% capture tab_content %}

Studio
===
![subscribe-config]({{ site.baseurl }}/images/subscribe-config.png)
====

Code
===

```xml
<mqtt:listener config-ref="MQTT5">
    <mqtt:subscriptions >
        <mqtt:subscription topicFilter="#" qosLevel="AT_LEAST_ONCE"/>
    </mqtt:subscriptions>
</mqtt:listener>
```

{% endcapture %}
{% include tabs.html tab_group="module" %}

---

{% capture tab_content %}

MQTT 5.0
===


====

MQTT 3.1.1
===

{% endcapture %}{% include tabs.html tab_group="mqtt-version" %}

## Subscriptions

The **On New Message** can declare multiple subscriptions for a client. Each subscription is made up of a topic filter and a QoS level.

#### Example Subscription
![subscribe-config]({{ site.baseurl }}/images/single-subscription.png)

if there are overlapping subscriptions for one client, the broker delivers the message that has the highest QoS level for that topic.

### Topic Filter

Topic filters are used to subscribe to topics and receive publications. Topic filters can contain wildcards. With wildcards, you can subscribe to multiple topics. Learn more about topic filters and wildcards [here](https://www.ibm.com/support/knowledgecenter/SSFKSJ_8.0.0/com.ibm.mq.pro.doc/q005020_.htm)


| Property | Default | Type | Expression |
| -------- | ------- | ---- | ---------- |
| `topicFilter` | - | String | `not supported` |

### QOS level

The Quality of Service (QoS) level is an agreement between the sender of a message and the receiver of a message that defines the guarantee of delivery for a specific message. There are 3 QoS levels in MQTT:

| QoS 0 | AT MOST ONCE  |  |
| QoS 1 | AT LEAST ONCE |  |
| QoS 2 | EXACTLY ONCE  |  |

The broker transmits a published message to subscribing clients using the QoS level. If the subscription defines a lower QoS than the publishing client, the broker transmits the message with the lower quality of service.

| Property | Default | Type | Expressions |
| -------- | ------- | ---- | ---------- | 
| `qos` | `AT_MOST_ONCE` | String Enum <br/> .`AT_MOST_ONCE` <br/> .`AT_LEAST_ONCE` <br/> .`EXACTLY_ONCE` | `supported` |

{% capture tab_content %}

MQTT 5.0
===

### Attributes

MQTT5

====

MQTT 3.1.1
===

### Attributes

MQTT3

{% endcapture %}{% include tabs.html tab_group="mqtt-version" tab_no_header=true %}

--- 