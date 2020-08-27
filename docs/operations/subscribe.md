---
layout: default
title: On New Message 
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

MQTT 5
===


====

MQTT 3
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


## Mule Message

As said before, each message received by the subscriptions will trigger a flow execution with a new **Mule Message**. It's of importance to understand the structure of that **Mule Message** to develop the flow and process the message correctly.

The Mule Message is composed of a payload and it's attributes (metadata of the payload), let's take a look to both in the **On New Message** source.

{% capture tab_content %}

MQTT 5
===
### Payload

The payload carries the actual message binary data. MQTT is data-agnostic so the payload can be in any data format.

MQTT 5 Introduced the concept of Content Type for the messages, which is optional, but if present in the incoming message it will be automatically set when the message is dispatched. For example: if the incoming message payload is a JSON object and the content type was set by the sender, then we can process it with data weave without setting anything else. 

#### JSON Data Weave Example

IMAGE

On contrary, if the Content Type was not set by the sender then you can work with the raw binary message or explicitly provide the Content Type for the message.

If you know that all messages are in a particular format you can set the content type of a message with the **Output MIME Type** property on the **On New Message**  operation and the same Content Type will be applied for all dispatched messages. 

#### Setting Output MIME Type

IMAGE

You can also use the mule set payload message processor if your case is more dynamic.

### Attributes

The attributes contain metadata associated to the payload


====

MQTT 3
===

### Payload

The payload of a Publish message carries the actual application data. MQTT is data-agnostic so the payload can be in any format.

You can work with the raw binary message or if you know that all messages are in a particular format you can set the content type of a message with the **Output MIME Type** property on the **On New Message**  operation and the same Content Type will be applied for all dispatched messages. 

#### Setting Output MIME Type

IMAGE

You can also use the mule set payload message processor if your case is more dynamic.

### Attributes

The attributes contain metadata associated to the payload

{% endcapture %}{% include tabs.html tab_group="mqtt-version" tab_no_header=true %}

--- 