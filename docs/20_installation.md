---
layout: default
title: Installation
nav_order: 3
---

# Installation

The MQTT Connector is available in a maven repository and can be setup easily in your mule project. You will need to include the following snippet inside your `pom.xml` file.
{: .fs-5 .fw-300 }

## Using Maven

#### Repository
Add this repository to your project repositories.
{: .fs-2 }

```xml
<repository>
    <id>mqtt-connector-repo</id>
    <url>https://raw.github.com/juandesi/mule-mqtt-connector/mvn-repo/</url>
</repository>
```

#### Dependency
Add this dependency to the mule project dependencies.
{: .fs-2 }

```xml
<dependency>
    <groupId>desi.juan</groupId>
    <artifactId>mule-mqtt-connector</artifactId>
    <version>1.0.0</version>
    <classifier>mule-plugin</classifier>
</dependency>
```

## Snapshots

Snapshots can be obtained from the same repository.

```xml
<dependency>
    <groupId>desi.juan</groupId>
    <artifactId>mule-mqtt-connector</artifactId>
    <version>1.1.0-SNAPSHOT</version>
    <classifier>mule-plugin</classifier>
</dependency>
```


