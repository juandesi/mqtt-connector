---
layout: default
title: Connection
has_children: true
nav_order: 4
---

# Connection

A MQTT connection declares the MQTT broker/server that will receive and send the MQTT messages and how that connection with the broker is established.
{: .fs-5 .fw-300 }

There are 2 types of connections: `MQTT 5` and `MQTT 3`. The general configuration is very similar, but we will see later that `MQTT 5` introduced new features that are only supported by this type of connection.
{: .fs-5 .fw-300 }

## Connector Configuration 

Before digging into how to connect with a MQTT broker, it's important to remember a mule concept, the connector configuration.

In the case of the MQTT connector we will not go deeply into the connector configuration because there is not much in to configure there. For the MQTT connector the configuration will only act as a holder for the connection, and will allow the connector operations to reference a particular connection.

#### Configuration with a connection
{% capture tab_content %}

Studio
===
![config]({{ site.baseurl }}/images/config-connection.png)
====

Code
===

```xml
<mqtt:config name="MQTT5-CONFIGURATION">
  <mqtt:mqtt5-connection host="test.mosquitto.org" port="1883"/>
</mqtt:config>
```

{% endcapture %}
{% include tabs.html tab_group="module" %}

In the example above, a configuration named `MQTT5-CONFIGURATION` is declared with a connection that will try to connect with the `test.mosquitto.org` broker. (which is a well known public test broker). The name specified in the configuration, is the name that we will use in our operations to reference the connection.

## Cached Connections

In the MQTT connector for each configuration declared, a connection is established and cached so that one specific configuration always gets the same connection. The connection is maintained until the configuration itself is stopped.

This means that if you declare a configuration with a connection and it's referenced in two different operations, the **exact same** instance is going to be used to execute both operations. This is important to know for cases when the user **DON'T** want to share the same resource.

It is a good practice to separate subscription configurations from publish configurations, but if required configurations can be shared without a problem in most scenarios. 

