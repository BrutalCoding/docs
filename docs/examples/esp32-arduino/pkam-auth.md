---
description: >-
  Write some code for your ESP32's atSign to PKAM authenticate into its
  corresponding atServer
---

# Step 5 - PKAM Authentication

Step 5 - PKAM Authentication can also be found in [video](https://www.youtube.com/watch?v=eBafKbASuaU\&list=PLkZCny-S3rfC93\_Xqd\_HBkK\_dAjDzQ9Et\&index=6\&pp=gAQBiAQB)

{% embed url="https://www.youtube.com/watch?index=6&list=PLkZCny-S3rfC93_Xqd_HBkK_dAjDzQ9Et&pp=gAQBiAQB&v=eBafKbASuaU" %}
Step 5 - Pkam Authentication
{% endembed %}

PKAM Authentication is the process of authenticating an application's session into an atServer. A PKAM authenticated session is required for your ESP32 to run atServer operations (also known as verbs) to put and get atRecords and send data to other atSigns. More on PKAM Authentication can be read [here](../../core/).

## 1. Creating `constants.h`

1. Create a `constants.h` header file under the `include/` folder in our project.
2. Define your WiFi's SSID and Password. This can be your home WiFi or your own personal hotspot.

```cpp
#pragma once

#define SSID "******"
#define PASSWORD "******"
```

3. Optional: if you are working inside of a Git project, add `constants.h` into your `.gitignore` so that you do not accidentally commit this file.

## 2. PKAM Authentication Code in `main.cpp`

1. Include the `constants.h` header in your `main.cpp` source file.

{% code title="main.cpp" %}
```cpp
/// ...
#include "constants.h"
/// ...
```
{% endcode %}

2. Add the following code inside `void setup() {}` to PKAM authenticate. Be sure to change the atSign to the corresponding atSign that you've uploaded the keys with in [Step 3](upload-atkeys.md).

{% code title="main.cpp" %}
```cpp
void setup()
{
    // put your setup code here, to run once:

    // change this to the atSign you own and have the keys to
    const auto *at_sign = new AtSign("@24glad32"); 
    
    // reads the keys on the ESP32
    const auto keys = keys_reader::read_keys(*at_sign); 
    
    // creates the AtClient object (allows us to run operations)
    auto *at_client = new AtClient(*at_sign, keys);  
    
    // pkam authenticate into our atServer
    at_client->pkam_authenticate(SSID, PASSWORD); 
}
```
{% endcode %}

3. Put your ESP32 into download mode and run the Upload and Monitor command. If all is successful, you should see a similar output. The key output you should look for here is `response: success` and `authenticated: 1`.

{% code title="Output" %}
```sh
Attempting to connect to SSID...
..
Connected!
IP address: 12345678
Connected to root.atsign.org:64
 ce749e70-f570-5486-9f86-eb9ec5e038d8.swarm0002.atsign.zone:5604
res: " ce749e70-f570-5486-9f86-eb9ec5e038d8.swarm0002.atsign.zone:5604"
Connected to ce749e70-f570-5486-9f86-eb9ec5e038d8.swarm0002.atsign.zone:5604
first: "@data:["publickey@24glad32","signing_publickey@24glad32"]"
Secondary connected: 1
challenge: "_def2da36-4c10-4b0e-97c1-f09c314637c2@24glad32:44fc42a6-774e-4bb8-bd6a-90d4c58b590a"
import: 0
complete: 0
private key check: 0
sign success: 0
pkam command: "pkam:VVw2RNcwhNw/l7vLLeC10VqNU2xqfUtjf7T82PvoxQ+uaN6QW9zj8Pi4+b8UgUNu6G8L1RkdmU2UMCkWrB/L0v2Jh1oK7eHth8PN4B91F/4rtxd1AGkfV+aiX5IyRLBC8prl5qdcqKqf3Gt6XCSV4/NDCOrXQqXdd/njZ/gmCLJlyPPlSu6IkOzMxu2nAcwNe7daSFw1agcyLLyhjdl3oJOopxGFX3zRar3vnex5F71A/1BIyP0h5OjZ0ZItngWaujMxEwwyvMINQJa0nflwk7z6phP+Vnt+7+oKNQCDhRfUTDaWHm4t++2Mp6BrHDh5KPCFCK9psgFGu+tx8nvpjg=="
response: success
authenticated: 1
```
{% endcode %}

4. If your output is not similar, ensure that the `.atKeys` are uploaded and that you are using the correct SSID and Password. It may take a few attempts to get it working (sometimes due to weak connection). Seek help on our [discord](https://discord.atsign.com) if you are still stuck.
