---
description: A private, encrypted datastore
---

# atServer

### What is an atServer?

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
