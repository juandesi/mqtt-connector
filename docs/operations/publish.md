---
layout: default
title: Publish
parent: Operations
nav_order: 1
---

# Publish

Messages are published with a topic. The MQTT broker needs the `topic` to route the message to subscribers. Hence the `topic` is mandatory for a publish message (it is the only required property).

{% capture tab_content %}

MQTT 5.0
===

  {% capture tab_content %}

  Studio
  ===
![mqtt5-connection]({{ site.baseurl }}/images/3-connection-mqtt5.png)
  ====

  Code
  ===

```xml
<mqtt:config name="MQTT3">
<mqtt:mqtt5-connection host="test.mosquitto.org" port="1883" 
            clientId="TestIdentifier" cleanSession="true"/>
</mqtt:config>
```

  {% endcapture %}
  {% include tabs.html tab_group="module" %}

--- 

- [Topic](#topic)
- [Message](#message)
- [Quality of Service (QoS)](#quality-of-service-qos)
- [Retain](#retain)
- [Message Expiry Interval](#message-expiry-interval)
- [Payload Format Indicator](#payload-format-indicator)
- [Content Type](#content-type)
- [Response Topic](#response-topic)
- [Correlation Data](#correlation-data)
- [User Properties](#user-properties)

====

MQTT 3.1.1
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

- [Topic](#topic)
- [Message](#message)
- [Quality of Service (QoS)](#quality-of-service-qos)
- [Retain](#retain)

{% endcapture %}{% include tabs.html tab_group="mqtt-version" %}

***


## Topic

Messages are published with a topic.
The MQTT broker needs the topic to route the message to subscribers.
Hence the topic is mandatory for a Publish message (it is the only required property).
A topic can be hierarchically structured in multiple topic levels (divided by `/`) enabling easier filtering for
subscribers.

| Property | Default | Type |
| -------- | ------- | ---- |
| `topic` | - | String |

## Message

Is the payload of the publish message that carries the actual application data.
MQTT is data-agnostic so you can use any format for the payload. 

| Property | Default | Type |
| -------- | ------- | ---- |
| `message` | - | Binary |

## Quality of Service (QoS)

The QoS levels ensure different message delivery guarantees in case of connection failures.
The QoS level should be chosen based on the use case.

| QoS 0 | AT MOST ONCE  | Messages are not redelivered after a failure. Some messages may be lost. |
| QoS 1 | AT LEAST ONCE | Messages are redelivered after a failure if they were not acknowledged by the broker. Some messages may be delivered more than once (initial delivery attempt + redelivery attempt(s)). |
| QoS 2 | EXACTLY ONCE  | Messages are redelivered after a failure if they were not acknowledged by the broker. The broker additionally filters duplicate messages based on message ids. |

The trade-off between the QoS levels is lower or higher latency and the amount of state that has to be stored on sender 
and receiver.

Keep in mind that the MQTT QoS levels cover guarantees between the client and the broker (not directly the subscribers)
as MQTT is an asynchronous protocol (which is an advantage because it decouples publishers and subscribers and makes the 
system more robust and scalable).
Different brokers might provide different guarantees for end-to-end communication (especially if they are clustered).

| Property | Default | Type |
| -------- | ------- | ---- |
| `qos` | `AT_MOST_ONCE` | String Enum <br/> .`AT_MOST_ONCE` <br/> .`AT_LEAST_ONCE` <br/> .`EXACTLY_ONCE` | 

## Retain

The retain flag indicates that the message should be stored at the broker for its topic.
New subscribers then get the last retained message on that topic even if they were not connected when it was published.

| Property | Default | Type |
| -------- | ------- | ---- |
| `retain` | `false` | Boolean | 



{% capture tab_content %}

MQTT 5.0
===

***

## Properties

The properties supported for the publish command are the followings:

MQTT 5 ONLY
{: .label .label-green }

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

### Message Expiry Interval

The message expiry interval is the time interval (in seconds) the message will be queued for subscribers. If no message expiry interval is provided, then is assumed disabled.

| Property | Default | Type |
| -------- | ------- | ---- |
| `messageExpiryInterval` | | - | Number | 

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
| `contentType` | (will use the **payload** media type if present) | `String` |

### Response Topic

Although MQTT is a publish/subscribe protocol, it can be used with a request/response pattern.
MQTT's request/response is different from synchronous request/response (like HTTP) as it has still all MQTT 
characteristics like asynchronism, decoupling of sender and receiver and 1-to-many communication.
Requesting is done by subscribing to a response topic and then publishing to a request topic.
The publish includes the response topic so a responder knows to which topic it should publish the response.
To correlate request and response (as they are asynchron, multiple responses from different clients are possible), you 
can use the [correlation data](#correlation-data).

| Property | Default | Type |
| -------- | ------- | ---- |
| `responseTopic` | - | `String` |

### Correlation Data

Correlation data can be used to correlate a request to its response.
If it is part of the request message then the responder copies it to the response message.

| Property | Default | Type |
| -------- | ------- | ---- |
| `correlationData` | - | `String` |

### User Properties

User Properties are user defined name and value pairs which are sent with the MQTT5 publish message.

| Property | Default | Type |
| -------- | ------- | ---- |
| `userProperties` | - | `String value pairs` |

====

MQTT 3.1.1
===

{% endcapture %}{% include tabs.html tab_group="mqtt-version" tab_no_header=true %}
>>>>>>> Stashed changes
