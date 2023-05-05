---
description: The atServer address book
---

# atDirectory

In order for an atSign to communicate with another one on the internet, we need to locate the atServer that can send and receive information securely on its behalf.&#x20;

The location of an atServer is found using the atDirectory service (`root.atsign.org:64`). This directory returns the DNS address and port number of the atServer for any atSign that it has a record for. The atDirectory service contains no information about the owner of the atSign.
