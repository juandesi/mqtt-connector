---
layout: default
title: Publish
parent: Operations
nav_order: 1
---

# Publish

This operation as the name implies, **publishes** or sends a message to a MQTT broker and returns immediately to the flow without returning anything after passing the request to an async client. If the publish operation is not successful, it will throw a mule error.

Messages are published with a `topic`. The MQTT broker needs the `topic` to route the message to subscribers. Hence the `topic` is mandatory for a publish message (it is the only required property).

This operation accepts MQTT5 and MQTT3 configurations; the example below works for both of them. For specific features the documentation below the example describes the behavior for each version of the protocol; choose the one that fits in your project.

  {% capture tab_content %}

  Studio
  ===
![publish-config]({{ site.baseurl }}/images/publish-config.png)
  ====

  Code
  ===

```xml
<mqtt:publish config-ref="mqtt-config" topic="test/topic"/>
```

  {% endcapture %}
  {% include tabs.html tab_group="module" %}

---

{% capture tab_content %}

MQTT 5.0
===

- [Connector Configuration](#connector-configuration)
- [Topic](#topic)
- [Message](#message)
- [Quality of Service (QoS)](#quality-of-service-qos)
- [Retain](#retain)
- [Properties](#properties)

====

MQTT 3.1.1
===

- [Connector Configuration](#connector-configuration)
- [Topic](#topic)
- [Message](#message)
- [Quality of Service (QoS)](#quality-of-service-qos)
- [Retain](#retain)

{% endcapture %}{% include tabs.html tab_group="mqtt-version" %}

***

## Connector Configuration

The name of the configuration set to use with the operation.

| Property | Default | Type | Expressions |
| -------- | ------- | ---- | ---------- | 
| `config-ref` | - | String | `not supported` |

## Topic

Messages are published with a topic.
The MQTT broker needs the topic to route the message to subscribers.
Hence the topic is mandatory for a Publish message (it is the only required property).
A topic can be hierarchically structured in multiple topic levels (divided by `/`) enabling easier filtering for
subscribers.

| Property | Default | Type | Expressions |
| -------- | ------- | ---- | ---------- | 
| `topic` | - | String | `supported` |

## Message

Is the payload of the publish message that carries the actual application data.
MQTT is data-agnostic so you can use any format for the message content. 

By default, the message content is taken from the `payload` of the incoming mule message, but you can customize it using a DataWeave script.


| Property | Default | Type | Expressions | 
| -------- | ------- | ---- | ----- | 
| `message` | `#[payload]` | Binary | `required` |

## Quality of Service (QoS)

The QoS levels ensure different message delivery guarantees in case of connection failures.
The QoS level should be chosen based on the use case.

| QoS 0 | AT MOST ONCE  | Messages are not redelivered after a failure. Some messages may be lost. |
| QoS 1 | AT LEAST ONCE | Messages are redelivered after a failure if they were not acknowledged by the broker. Some messages may be delivered more than once (initial delivery attempt + redelivery attempt(s)). |
| QoS 2 | EXACTLY ONCE  | Messages are redelivered after a failure if they were not acknowledged by the broker. The broker additionally filters duplicated messages based on message ids. |

The trade-off between the QoS levels is the lower or higher latency and the amount of state that has to be stored on sender 
and receiver.

Keep in mind that the MQTT QoS levels cover guarantees between the client and the broker (not directly the subscribers)
as MQTT is an asynchronous protocol (which is an advantage because it decouples publishers and subscribers and makes the 
system more robust and scalable).
Different brokers might provide different guarantees for end-to-end communication (especially if they are clustered).

| Property | Default | Type | Expressions |
| -------- | ------- | ---- | ---------- | 
| `qos` | `AT_MOST_ONCE` | String Enum <br/> .`AT_MOST_ONCE` <br/> .`AT_LEAST_ONCE` <br/> .`EXACTLY_ONCE` | `supported` |

## Retain

The retain flag indicates that the message should be stored in the broker for its topic.
New subscribers then get the last retained message on that topic even if they were not connected when it was published.

| Property | Default | Type | Expression |
| -------- | ------- | ---- | ---------- | 
| `retain` | `false` | Boolean | `supported` |



{% capture tab_content %}

MQTT 5.0
===

***

## Properties

MQTT 5 ONLY
{: .label .label-green }

MQTT 5.0 protocol adds many properties which can add metadata for the broker or subscriber to change behavior in certain scenarios.

For the publish operation, all the properties are bundled into a single object that must be created using DataWeave and then is decomposed by the connector while executing. The parameter can be configured in the `Properties` tab (see below).

| Property | Default | Type | Expression |
| -------- | ------- | ---- | ---------- | 
| `properties` | - | Object | `required` |

  {% capture tab_content %}

  In Line Declaration
  ===
![publish-properties-inline]({{ site.baseurl }}/images/publish-properties-inline.png)

  ====

  Using Transform Message 
  ===
  If needed, you can take advantage of metadata by creating a variable (in this case called 'props') and mapping the values to necessary properties. Once created, the variable can be referenced from the properties parameter in the publish operation.
  {: .fs-2 } 

![publish-properties]({{ site.baseurl }}/images/publish-properties.png)


  {% endcapture %}
  {% include tabs.html tab_group="module" %}

The properties supported for the publish command are the following: 
{: .fs-5 }

### Message Expiry Interval

The message expiry interval is the time interval (in seconds) the message will be queued for subscribers. If no message expiry interval is provided, then is assumed disabled.

| Property | Default | Type |
| -------- | ------- | ---- |
| `messageExpiryInterval` | - | Number | 

### Payload Format Indicator

To indicate if the payload is text or binary data, you can use the the payload format indicator.
Used in conjunction with the [content type](#content-type) the payload encoding can be described precisely.

| Property | Default | Type |
| -------- | ------- | ---- |
| `payloadFormatIndicator` | - | String Enum <br/> `UNSPECIFIED` <br/> `UTF-8` |

### Content Type

The content type describes the encoding of the payload.
It can be any string, but it is recommended to use a MIME type to ensure interoperability.

| Property | Default | Type |
| -------- | ------- | ---- |
| `contentType` | (will use the **payload** media type if present) | String |

### Response Topic

Although MQTT is a publish/subscribe protocol, it can be used with a request/response pattern.
MQTT's request/response is different from synchronous request/response (like HTTP) as it still has all MQTT 
characteristics like asynchronism, decoupling of sender and receiver and 1-to-many communication.
Requesting is done by subscribing to a response topic and then publishing to a request topic.
The publish includes the response topic so a responder knows to which topic it should publish the response.
To correlate request and response (as they are asynchron, multiple responses from different clients are possible), you 
can use the [correlation data](#correlation-data).

| Property | Default | Type |
| -------- | ------- | ---- |
| `responseTopic` | - | String |

### Correlation Data

Correlation data can be used to correlate a request to its response.
If it is part of the request message then the responder copies it to the response message.

| Property | Default | Type |
| -------- | ------- | ---- |
| `correlationData` | - | String |

### User Properties

User Properties are user defined name and value pairs which are sent with the MQTT5 publish message. As long as you don’t exceed the maximum message size, you can use an unlimited number of user properties to add metadata to MQTT messages and pass information between publisher, broker, and subscriber

| Property | Default | Type |
| -------- | ------- | ---- |
| `userProperties` | - | Object of string value pairs |


====

MQTT 3.1.1
===

{% endcapture %}{% include tabs.html tab_group="mqtt-version" tab_no_header=true %}


--- 

For more information about publish properties, check the [Oasis MQTT5 standard](https://docs.oasis-open.org/mqtt/mqtt/v5.0/os/mqtt-v5.0-os.html#_Toc3901109).
{: .fs-2 }

## Errors
