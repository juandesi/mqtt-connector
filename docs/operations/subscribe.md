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
- [Subscriptions](#subscriptions)
- [Message](#mule-message)
- [Errors](#errors)

====

MQTT 3
===

- [Subscriptions](#subscriptions)
- [Message](#mule-message)
- [Errors](#errors)

{% endcapture %}{% include tabs.html tab_group="mqtt-version" %}

---

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

| QoS 0 | AT MOST ONCE  | Messages are received once, some messages may be lost. |
| QoS 1 | AT LEAST ONCE | Messages are not acknowledged by the broker. Some messages may be received more than once |
| QoS 2 | EXACTLY ONCE  | Messages are acknowledged by the broker, additionally filters duplicate messages based on message ids. |

The broker transmits a published message to subscribing clients using the QoS level. If the subscription defines a lower QoS than the publishing client, the broker transmits the message with the lower quality of service.

| Property | Default | Type | Expressions |
| -------- | ------- | ---- | ---------- | 
| `qosLevel` | `AT_MOST_ONCE` | String Enum <br/> .`AT_MOST_ONCE` <br/> .`AT_LEAST_ONCE` <br/> .`EXACTLY_ONCE` | `supported` |

### Reconnection and Resume Session

{% capture tab_content %}

MQTT 5
===

Clean Start + Session Expiry

====

MQTT 3
===

Clean session

{% endcapture %}{% include tabs.html tab_group="mqtt-version" tab_no_header=true %}


## Mule Message

As said before, each message received by the subscriptions will trigger a flow execution with a new **Mule Message**. It's important to understand the structure of the dispatching **Mule Message** to process the message correctly while developing the flow.

The Mule Message is composed of a payload and it's attributes (metadata of the payload), let's see how they both look in the **On New Message** source.

{% capture tab_content %}

MQTT 5
===
### Payload

The payload carries the actual message binary data. MQTT is data-agnostic so the payload can be in any data format.

MQTT 5 Introduced the concept of Content Type for the messages, which is optional, but if present in the incoming message it will be automatically set when the message is dispatched. For example: if the incoming message payload is a JSON object and the content type was set by the sender, then it can be processed with Data Weave without setting anything else (because Data Weave **requires** the Content Type of the payload to understand it).

On contrary, if the Content Type was not set by the sender then you can work with the raw binary message or explicitly provide the Content Type for the message.

If you know that all messages are in a particular format you can set the content type of a message with the **Output MIME Type** property on the **On New Message**  operation and the same Content Type will be applied for all dispatched messages. 

#### Setting Output MIME Type

![output-mimetype]({{ site.baseurl }}/images/output-mimetype.png)

You can also use the mule set payload message processor if your case is more dynamic.

====

MQTT 3
===

### Payload

The payload of a Publish message carries the actual application data. MQTT is data-agnostic so the payload can be in any format.

You can work with the raw binary message or if you know that all messages are in a particular format you can set the content type of a message with the **Output MIME Type** property on the **On New Message**  operation and the same Content Type will be applied for all dispatched messages. 

#### Setting Output MIME Type

![output-mimetype]({{ site.baseurl }}/images/output-mimetype.png)

You can also use the mule set payload message processor if your case is more dynamic.

{% endcapture %}{% include tabs.html tab_group="mqtt-version" tab_no_header=true %}


### Attributes

The attributes contain metadata associated to the payload, this metadata consists in a set of properties that are bundled in a message.

#### Example attributes usage

{% capture tab_content %}

MQTT 5
===
![input-attributes-mqtt5]({{ site.baseurl }}/images/input-attributes-mqtt5.png)
====
MQTT 3
===
![input-attributes-mqtt3]({{ site.baseurl }}/images/input-attributes-mqtt3.png)
{% endcapture %}{% include tabs.html tab_group="mqtt-version" tab_no_header=true %}
--- 

##### Topic
The topic the message was sent to. This is useful to find the topic when the subscriber used a topic filter to match `n` topics
{: .fs-2 .fw-300 }

| Attribute | Type | Accessible With |
| -------- | ---- | ---------- |
| `topic` | String | `attributes.topic` |

##### Qos

The qos level of the receiving message. the MAX qos level is the one defined in the subscription. e.g.: if a message is sent with QoS 2 but the subscription is done with QoS 1, the receiving message QoS will be 1.
{: .fs-2 .fw-300 }

| Attribute | Type | Accessible With |
| -------- | ---- | ---------- |
| `qos` | String Enum <br/> .`AT_MOST_ONCE` <br/> .`AT_LEAST_ONCE` <br/> .`EXACTLY_ONCE` | `attributes.qos` |

##### Retain

Indicates that the message should be stored at the broker for its topic.
{: .fs-2 .fw-300 }

| Attribute | Type | Accessible With |
| -------- | ---- | ---------- |
| `retain`| Boolean | `attributes.retain` |

{% capture tab_content %}

MQTT 5
===

##### Payload Format Indicator

Indicates if the payload is text or binary data, used in conjunction with the content type if the payload format is `UTF8` encoded text.	
{: .fs-2 .fw-300 }

| Attribute | Type | Accessible With |
| -------- | ---- | ---------- |
| `payloadFormatIndicator` | String enum <br/> .`UNSPECIFIED` <br/> `UTF_8` | `attributes.payloadFormatIndicator` |

##### Content Type 

The Content Type identifies the kind of UTF-8 text encoded payload. When the Payload Format Indicator is set to 1, a MIME content type descriptor is expected (but not mandatory). Any valid UTF-8 String can be used.
{: .fs-2 .fw-300 }

If the Content Type attribute is present will be automatically set to the payload.
{: .fs-2 .fw-300 }

| Attribute | Type | Accessible With |
| -------- | ---- | ---------- |
| `contentType`| String | `attributes.contentType` |

##### Response Topic

The response topic field represents the topic on which the responses from the receivers of the message are expected. Used to implement a request-response pattern using MQTT.
{: .fs-2 .fw-300 }

| Attribute | Type | Accessible With |
| -------- | ---- | ---------- |
| `responseTopic` | String | `attributes.responseTopic` |

##### Correlation Data

Correlation data is optional binary data that follows the response topic. The sender of the request uses the data for identifying to which specific request a response that is received later relates. Response topics can be used without correlation data.
Using the correlation makes it possible for the original sender of the request to handle asynchronous responses that can possibly be sent from multiple receivers. This data is irrelevant to the MQTT broker and only functions as a means to identify the relationship between sender and receiver.
{: .fs-2 .fw-300 }

| Attribute | Type | Accessible With |
| -------- | ---- | ---------- |
| `correlationData` | String | `attributes.correlationData` |

##### Message Expiry Interval

Defines the period of time that the broker stores a published message for subscribers that are not currently connected.
{: .fs-2 .fw-300 }

| Attribute | Type | Accessible With |
| -------- | ---- | ---------- |
| `messageExpiryInterval` | Number | `attributes.messageExpiryInterval` |

##### User Properties

User properties are basic UTF-8 string key-value pairs that you can be appended to a message. As long as the maximum message size is not exceeded, an unlimited number of user properties can be passed as information between publisher, broker, and subscriber.
{: .fs-2 .fw-300 }

The User Properties feature is very similar to the HTTP headers concept.
{: .fs-2 .fw-300 }

| Attribute | Type | Accessible With |
| -------- | ---- | ---------- |
| `userProperties` | Object | `attributes.userProperties.['NAME_OF_CUSTOM_PROPERTY']` |



====

MQTT 3
===

{% endcapture %}{% include tabs.html tab_group="mqtt-version" tab_no_header=true %}

--- 

## Errors