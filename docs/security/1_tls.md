---
layout: default
title: SSL/TLS
nav_order: 1
parent: Security
redirect_from: /docs/client_configuration.html
---

# SSL/TLS

SSL/TLS protocols allow the connection between two mediums (client-server) to be encrypted. Encryption helps you make sure that no third party is able to read the data or tamper with it.

The SSL/TLS configuration is the same for both `MQTT3` and `MQTT5`, and it comes in two flavors:

## Simple TLS config  

The simple TLS configuration allows to setup TLS with a single CA certificate, without the need of creating a truststore file for a single certificate.

This is exceptionally good for testing, but is also good for production if your use case fits.

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
            <mqtt:simple-tls-config caCertificate="resources/mosquitto.org.crt" />
        </mqtt:tls-configuration>
    </mqtt:mqtt5-connection>
</mqtt:config>
```

{% endcapture %}
{% include tabs.html tab_group="module" %}

---

| Property | Description | Default value | Expression |
| ----------- | ----------- | ------------- | -------- |
| `caCertificate` | The path to the CA X509 certificate resource. | - | `not supported` |

## Advanced TLS config  

The advanced TLS configuration is based on the TLS context with a trust store file and additional information to establish the secure communication.

The TLS Context can be defined in line (like in the example below), but can also be declared as a reference to a global defined one.

It is important to know that the TLS Context has the capability to configure a key store, but for setting up TLS, only a trust store will br required. The key store will be used to perform transport level authentication (Mutual TLS authentication) that is described in the [Authentication](2_authentication.md#tls-mutual-authentication) section.

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
                    <tls:trust-store path="resources/truststore.jks" type="jks"
                                     password="changeit" insecure="false"/>
                </tls:context>
            </mqtt:advanced-tls-config>
        </mqtt:tls-configuration>
    </mqtt:mqtt5-connection>
</mqtt:config>
```

{% endcapture %}
{% include tabs.html tab_group="module" %}

---

### TLS Context 

The TLS Context enables to set all security files and configuration in a single object. This can be also declared globally and referenced.
{: .fs-3 }

##### Enabled Protocols

A comma separated list of protocols enabled for this context.
{: .fs-3 }

| Property | Default value | Expression |
| ----------- | ------------- | -------- |
| `enabledProtocols` | - | `not supported` |

##### Enabled Cipher Suites
A comma separated list of cipher suites enabled for this context.
{: .fs-3 }

| Property | Default value | Expression |
| ----------- | ------------- | -------- |
| `enabledCipherSuites` | - | `not supported` |

##### TLS trust store

Contains all the configuration for a trust store file that stores CA certificates.
{: .fs-3 }

| Property | Description | Default value | Expression |
| ----------- | ----------- | ------------- | ------- |
| `path` | The location of the trust store. | - | `not supported` |
| `password` | The password for the trust store file. | - | `not supported` |
| `type` | The type of the trust store. | `JKS` | `not supported` |
| `algorithm` | The algorithm used by the trust store. | - | `not supported` |
| `insecure` | Disables verification of the server hostname in the server certificate. | `false` | `not supported` |

##### TLS key store

Contains all the configuration for a key store that is used to store users credentials.
{: .fs-3 }

The keystore is used to setup Mutual TLS authentication. See [Authentication](2_authentication.md#tls-mutual-authentication).
{: .fs-3 }

| Property | Description | Default value | Expression |
| ----------- | ----------- | ------------- | ------- |
| `path` | The location of the key store. | - | `not supported` |
| `type` | The type of store used. | `JKS` | `not supported` |
| `alias` | When the key store contains many private keys, this attribute indicates the alias of the key that should be used. If not defined, the first key in the file is used by default. | - | `not supported` |
| `keyPassword` | The password used to protect the private key. | - | `not supported` |
| `password` | The password used to protect the key store file. | - | `not supported` |
| `algorithm` | The algorithm used by the key store. | - | `not supported` |
