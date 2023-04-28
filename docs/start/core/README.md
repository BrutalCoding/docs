---
description: An overview of Atsign's core pillars of technology
---

# Core Technology

<figure><img src="../../.gitbook/assets/4 Pillars Full.png" alt=""><figcaption><p>The 4 Pillars of Atsign's Core Technology</p></figcaption></figure>

## atSigns

An atSign (e.g. @alice) is simply a resolvable address (kind of like an email address) on the atPlatform. Anything can have an atSign, a person, organization, or thing (IoT), even individual songs or videos could have atSign addresses.

Read more [here](atsign.md).

## atServers

An atServer is a private datastore for storing encrypted data owned by an atSign, and a rendezvous point for information exchange. An atServer is responsible for the delivery of encrypted information to other atServers, from which the owners of those atSigns can then retrieve the data. What is important to know is that the atServer stores only encrypted information and never has access to the cryptographic keys themselves.

Read more [here](atserver.md).

## The atDirectory

In order for an atSign to communicate with another one on the internet, we need to locate the atServer that can send and receive information securely on its behalf. This location is found using the AtDirectory service (root.atsign.org). This directory returns the DNS address and port number of the atServer for any atSign that it has a record for. The atDirectory service contains no information about the owner of the atSign.

Read more [here](atdirectory.md).

## The atProtocol

**Lorem Ipsum** is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book.

Read more [here](atprotocol.md).



