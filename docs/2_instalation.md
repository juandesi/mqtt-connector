---
layout: default
title: Installation
nav_order: 2
---

# Installation

The MQTT Connector is available in a maven repository and can be setup easily in your mule project. You will need to include the following inside your `pom.xml` file.

## Find it in Exchange

find it in exchange TODO

## Using Maven

#### Repository
Add this repository to your project repositories.
{: .fs-2 }

```xml
<repository>
    <id>mvnrepository</id>
    <name>mvnrepository</name>
    <url>http://www.mvnrepository.com</url>
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
    <version>2.0.0-SNAPSHOT</version>
    <classifier>mule-plugin</classifier>
</dependency>
```


