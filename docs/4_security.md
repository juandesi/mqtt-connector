---
layout: default
title: Security
has_children: true
nav_order: 4
---

# Security

Security in MQTT is divided in multiple layers. Each layer prevents different kinds of attacks. The goal of MQTT is to provide a lightweight and easy-to-use communication protocol for the Internet of Things. The protocol itself specifies only a few security mechanisms. MQTT implementations commonly use other state-of-the-art security standards: for example, SSL/TLS for transport security. Since security is difficult, it makes sense to build upon generally accepted standards.

## Transport Level 

TLS/SSL is commonly used for transport encryption. This method is a secure and proven way to make sure that data can’t be read during transmission and provides client-certificate authentication to verify the identity of both sides.

## Application Level

The MQTT protocol provides a client identifier and username/password credentials to authenticate devices on the application level. These properties are provided by the protocol itself. Authorization or control of what each device is allowed to do is defined by the specific broker implementation.