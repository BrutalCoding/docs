---
description: An overview of Atsign's core pillars of technology
---

# Core Technology

## Overview

<figure><img src="../../.gitbook/assets/core-overview-simple.png" alt="Diagram of Atsign&#x27;s Core Technology"><figcaption></figcaption></figure>

<details>

<summary>Relationships</summary>

Every **atServer** is associated with one **atSign**, and each atServer stores many **atRecords.**

When provided an **atSign**, the **atDirectory** returns a DNS address and port number for its **atServer.**

The **atProtocol** is the protocol used to speak to an **atServer.**

</details>

## atServer

An atServer is a private datastore for storing encrypted data owned by an atSign, and a rendezvous point for information exchange. An atServer is responsible for the delivery of encrypted information to other atServers, from which the owners of those atSigns can then retrieve the data.&#x20;

{% hint style="info" %}
Unless explicitly made public, atServers only store encrypted data and do not have access to the cryptographic keys, nor the ability to decrypt the stored information.
{% endhint %}

### Functionality

An atServer provides the following functionality:

* Cryptographic authentication of client devices
* Cryptographic authentication of other atServers.
* Persistence of encrypted data on behalf of the controlling atSign.
* Caching of data shared by others with the controlling atSign.
* Notification of data change events to clients (edge devices) and other atServers to facilitate delivery of information shared with them.
* Synchronization of data with multiple clients (edge devices).
* TLS wire encryption from clients to atServers using SSL certificates.
* Mutually authenticated TLS 1.2/1.3 wire encryption between atServers using SSL certificates.

## atDirectory

In order for an atSign to communicate with another one on the internet, we need to locate the atServer that can send and receive information securely on its behalf.&#x20;

The location of an atServer is found using the atDirectory service (`root.atsign.org:64`). This directory returns the DNS address and port number of the atServer for any atSign that it has a record for. The atDirectory service contains no information about the owner of the atSign.

## atProtocol

{% hint style="info" %}
The atProtocol communicates via layer 7, the application layer of the OSI model.
{% endhint %}

The atProtocol is an application protocol which enables peer-to-peer, end-to-end encrypted data sharing between atSigns. You can learn more about the atProtocol by reading the [specification](https://github.com/atsign-foundation/at\_protocol/blob/trunk/specification/at\_protocol\_specification.md).
