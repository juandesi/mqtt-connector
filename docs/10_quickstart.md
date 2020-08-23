---
layout: default
title: Quick Start
nav_order: 2
---

# Quick Start!

The following contains a simple example on how to add the connector to your project, connect to a broker, subscribe to a topic and ultimately publish messages to it using the MQTT 3.
{: .fs-5 .fw-300 }

## Add the MQTT connector to your project

Include the following Maven dependency:

```xml
<dependency>
    <groupId>desi.juan</groupId>
    <artifactId>mule-mqtt-connector</artifactId>
    <version>1.0.0</version>
    <classifier>mule-plugin</classifier>
</dependency>
```
See the [Installation](20_installation.md) section for more information.
{: .fs-3 }

## Connecting to the broker

First, let's connect to an actual broker. The following example shows how to connect to the **test.mosquitto.org** broker, which is a [publicly available MQTT broker](https://test.mosquitto.org/).  

To achieve this, let's set up the host with the following value: `test.mosquitto.org`, like this:

#### Connection Setup
{% capture tab_content %}

Studio
===
![quickstart-connection]({{ site.baseurl }}/images/quickstart-connection.png)
====

Code
===

```xml
<mqtt:config name="mosquitto-config">
	<mqtt:mqtt3-connection host="test.mosquitto.org"/>
</mqtt:config>
```

{% endcapture %}
{% include tabs.html tab_group="module" %}

Click the **Test Connection** button to validate that the connection is working. You should see a message like this one:

![quickstart-test-connection]({{ site.baseurl }}/images/quickstart-test-connection.png)


## Subscribing to a topic

Now that the connectivity execution test to the broker was successful, you can setup a subscription. To subscribe to a tooic let's add the MQTT connector **On New Message** source and add a Subscription to the `test/mule/topic` topic. Finally, add a logger after the source to log to the console all incoming messages.

#### Subscribe Flow
{% capture tab_content %}

Studio
===
![quickstart-sub]({{ site.baseurl }}/images/quickstart-sub.png)
====

Code
===

```xml
<flow name="OnNewMessage">
    <mqtt:listener config-ref="mosquitto-config">
        <mqtt:subscriptions>
            <mqtt:subscription topic="test/mule/topic"/>
        </mqtt:subscriptions>
    </mqtt:listener>
    <logger level="INFO" message="#[payload]"/>
</flow>
```

{% endcapture %}
{% include tabs.html tab_group="module" %}

## Publishing to the subscribed topic

Similar to subscribing, once you have a connected configuration, you can also publish messages to the recently subscribed topic using the same configuration.

For this example, let's publish to the topic that we subscribed in the previous step. Let's create a new flow with a scheduler to trigger the flow and after that add the MQTT connector Publish operation. Once all processors are added, change the message property from the Publish operation to `Hello World!`.

#### Publish Flow
{% capture tab_content %}

Studio
===
![quickstart-pub]({{ site.baseurl }}/images/quickstart-pub.png)
====

Code
===

```xml
<flow name="PublishFlow">
    <scheduler>
        <scheduling-strategy>
            <fixed-frequency/>
        </scheduling-strategy>
    </scheduler>
    <mqtt:publish config-ref="mosquitto-config" topic="test/mule/topic">
        <mqtt:message>#['Hello world!']</mqtt:message>
    </mqtt:publish>
</flow>
```

{% endcapture %}
{% include tabs.html tab_group="module" %}

## Run the application

Now go and run your app! You'll start to see log messages from the subscription flow that are being published by your publish flow. 

That's all!

Download the test app [here](https://drive.google.com/file/d/1X9N3PRvlSgM6kvZSs-JIk7F3KXBMSSdB/view?usp=sharing) and try it out. You can import it in Studio. (crafted for runtime 4.2.0)
{: .fs-2 }
