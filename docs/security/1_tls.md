---
layout: default
title: SSL/TLS
nav_order: 1
parent: Security
redirect_from: /docs/client_configuration.html
---

# SSL/TLS

SSL/TLS protocols allow the connection between two mediums (client-server) to be encrypted. Encryption lets you make sure that no third party is able to read the data or tamper with it.

The SSL/TLS configuration is the same for both `MQTT3` and `MQTT5`, and it comes in two flavors:

## Simple TLS config  

The simple TLS configuration allows to setup TLS with a single CA certificate, without the need to create a truststore file for a single certificate.

This is exceptionally good for testing, but is also good for production, if your use case fits.

This configuration only requires one property: the CA Certificate Path, that must be the path to a X509 certificate.

#### Example Simple TLS config
{% capture tab_content %}

Studio
===
![simple-tls]({{ site.baseurl }}/images/simpletls.png)
====

Code
===

```xml
<mqtt:config name="MQTT5">
    <mqtt:mqtt5-connection host="test.mosquitto.org" port="8883">
        <mqtt:tls-configuration>
            <mqtt:simple-tls-config caCertificate="ca.crt" />
        </mqtt:tls-configuration>
    </mqtt:mqtt5-connection>
</mqtt:config>
```

{% endcapture %}
{% include tabs.html tab_group="module" %}

---

| Parameter | Description | Default value | Expression |
| ----------- | ----------- | ------------- | -------- |
| `caCertificate` | The path to the CA X509 certificate resource. | - | `not supported` |

## Advanced TLS config  

{% capture tab_content %}

Studio
===
![tls]({{ site.baseurl }}/images/tls.png)
====

Code
===

```xml
<mqtt:config name="MQTT5">
    <mqtt:mqtt5-connection host="test.mosquitto.org" port="8883">
        <mqtt:tls-configuration>
            <mqtt:advanced-tls-config>
                <tls:context>
                    <tls:trust-store path="truststore.jks" type="jks" password="changeit" insecure="false"/>
                </tls:context>
            </mqtt:advanced-tls-config>
        </mqtt:tls-configuration>
    </mqtt:mqtt5-connection>
</mqtt:config>
```

{% endcapture %}
{% include tabs.html tab_group="module" %}

---

### Tls Context 

##### Enabled Protocols

A comma separated list of protocols enabled for this context.
{: .fs-2 }

##### Enabled Cipher Suites
A comma separated list of cipher suites enabled for this context.
{: .fs-2 }

##### TLS trust store

| Parameter | Description | Default value | Expression |
| ----------- | ----------- | ------------- | ------- |
| `path` | The location to the trust store file or resource. | - | `not supported` |
| `password` | The password for the trust store file. | - | `not supported` |
| `type` | The type of the trust store. | `JKS` | `not supported` |
| `algorithm` | The algorithm used by the trust store. | - | `not supported` |
| `insecure` | Disables verification of the server hostname in the server certificate. | `false` | `not supported` |
