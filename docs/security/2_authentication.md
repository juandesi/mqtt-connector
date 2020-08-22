---
layout: default
title: Authentication
nav_order: 2
parent: Security
---

# Authentication
Authentication is the process of verifying an user identity. The MQTT connector provides different ways to authenticate with MQTT brokers and it is possible to support multiple authentication schemes at once.

## Simple Authentication 

MQTT provides username/password authentication as part of the protocol. Be sure to use network encryption if you are using this option; otherwise, the username and password will be vulnerable to interception. 

{% capture tab_content %}

MQTT 5
===

  {% capture tab_content %}
  
  Studio
  ===
![mqtt5-userpass]({{ site.baseurl }}/images/mqtt5-user-pass.png)
  ====

  Code
  ===

```xml
<mqtt:config name="MQTT5">
    <mqtt:mqtt5-connection host="test.mosquitto.org" port="8883">
        <mqtt:simple-auth username="diegod" password="LOS"/>
    </mqtt:mqtt5-connection>
</mqtt:config>
```

  {% endcapture %}
  {% include tabs.html tab_group="module" %}

---

In `MQTT5` both `username` and `password` are **optional** properties, but at least one
is required if using simple authentication.

| Parameter | Description |
| ----------- | ----------- |
| `username` | Username to uniquely identify with the broker. **Optional** |
| `password` | String of characters used for authenticating a user on a computer system. **Optional**  |

====

MQTT 3
===

  {% capture tab_content %}
  
  Studio
  ===
![mqtt3-userpass]({{ site.baseurl }}/images/mqtt3-user-pass.png)
  ====

  Code
  ===

```xml
<mqtt:config name="MQTT3">
    <mqtt:mqtt3-connection host="test.mosquitto.org" port="8883">
        <mqtt:simple-auth username="juanito" password="complex"/>
    </mqtt:mqtt3-connection>
</mqtt:config>
```

  {% endcapture %}
  {% include tabs.html tab_group="module" %}

---

| Parameter | Description |
| ----------- | ----------- |
| `username` | Username to uniquely identify with the broker. Username is **required** if using simple auth on MQTT3.|
| `password` | String of characters used for authenticating a user on a computer system. Password is **optional**. |

{% endcapture %}
{% include tabs.html tab_group="mqtt-version" %}

***

## TLS Mutual Authentication

Another popular way of authenticating clients is via client certificates and can be used in addition or as an alternative to using username and password.

In cryptography, a client certificate is a type of digital certificate that is used by client systems to make authenticated requests to a remote server.
Client certificates play a key role in many mutual authentication designs, providing strong assurances of a requester’s identity ([Wikipedia](https://en.wikipedia.org/wiki/Client_certificate) ).

A client certificate identifies the client just like the server certificate identifies the server.

The client certificate must be provided by setting a keystore, using the [Advanced TLS configuration](1_tls.md).

#### Example keystore configuration

{% capture tab_content %}

Studio
===
![mqtt3-userpass]({{ site.baseurl }}/images/mqtt3-user-pass.png)
====

Code
===

```xml
<mqtt:config name="MQTT3">
  <mqtt:mqtt3-connection host="test.mosquitto.org" port="8883">
      <mqtt:simple-auth username="juanito" password="complex"/>
  </mqtt:mqtt3-connection>
</mqtt:config>
```

{% endcapture %}
{% include tabs.html tab_group="module" %}

--- 

##### Keystore configuration

This is the keystore configuration parameters, you can see the whole TLS Configuration in [Advanced TLS configuration](1_tls.md).

| Property | Description | Default value | Expression |
| ----------- | ----------- | ------------- | ------- |
| `path` | The location of the key store. | - | `not supported` |
| `type` | The type of store used. | `JKS` | `not supported` |
| `alias` | When the key store contains many private keys, this attribute indicates the alias of the key that should be used. If not defined, the first key in the file is used by default. | - | `not supported` |
| `keyPassword` | The password used to protect the private key. | - | `not supported` |
| `password` | The password used to protect the key store file. | - | `not supported` |
| `algorithm` | The algorithm used by the key store. | - | `not supported` |
