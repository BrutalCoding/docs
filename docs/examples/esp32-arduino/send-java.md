---
description: Learn how to send data from the ESP32 to your Java app
---

# Step 6 - Send Data with Java

Step 6 - Sending Data (ESP32 & Java) can be found in [video](https://www.youtube.com/watch?v=o1acO81EPVk\&list=PLkZCny-S3rfC93\_Xqd\_HBkK\_dAjDzQ9Et\&index=7\&pp=gAQBiAQB)

{% embed url="https://www.youtube.com/watch?index=7&list=PLkZCny-S3rfC93_Xqd_HBkK_dAjDzQ9Et&pp=gAQBiAQB&v=o1acO81EPVk" %}
Step 6 - Sending Data (Java & ESP32)
{% endembed %}

## 1. Prerequisite Generation of AES Key

If the two atSigns you are using in your application have already sent encrypted data between each other before, then you may skip this step.

As of writing this on `May 10th, 2023`, there are limitations to the ESP32 client.&#x20;

`at_esp32` cannot bootstrap the shared AES key between atSigns because there is no AES Key generation features implemented yet.&#x20;

Due to current limitations of the client, the Java app must first generate the shared AES key for the ESP32 to use. Then any subsequent data sent from the ESP32 to the Java app should be fine.

Here is some sample code of sending the initial data from the Java app to the ESP32. After running this once, we can start writing code for the ESP32 to send data to the Java app.

The goal of this step is for the two atSigns to have a shared AES key. If these two atSigns have already securely communicated peer-to-peer, then you may skip this step.&#x20;

A video tutorial of this step can be found [here](https://youtu.be/o1acO81EPVk?t=84).&#x20;

```java
package com.example;

import org.atsign.client.api.AtClient;
import org.atsign.common.AtException;
import org.atsign.common.AtSign;
import org.atsign.common.KeyBuilders;
import org.atsign.common.Keys.SharedKey;

public class App {
    public static void main(String[] args) throws Exception {
        AtSign java = new AtSign("@driving433");
        AtSign esp32 = new AtSign("@icy761");
        AtClient atClient = AtClient.withRemoteSecondary("root.atsign.org:64", java);

        // sending initial "handshake"
        SharedKey initialKey = new KeyBuilders.SharedKeyBuilder(atSign, esp32).key("test").build();

        String response = atClient.put(initialKey, "Hello World!").get();
        System.out.println("Response: " + response);
    }
}
```

## 2. Sending Data from the ESP32

1. Add the following code after PKAM authenticating (which was completed in [Step 5](pkam-auth.md)).

<pre class="language-cpp" data-title="void setup() inside of main.cpp "><code class="lang-cpp"><strong>// creating an AtKey. This is analogous to a key from a key-value pair in a map.
</strong><strong>// the key name is "test"
</strong><strong>// the shared by atSign is `at_sign` (the data is shared by the esp32 atSign)
</strong><strong>// the shared with atSign is `java` (the data is shared with the java atSign)
</strong><strong>const auto *at_key = new AtKey("test", at_sign, java);
</strong>
// putting the shared key into the esp32's atServer.
at_client->put_ak(*at_key, "Hello!");
</code></pre>

2. Your `main.cpp` should look similar to:

{% code title="main.cpp" lineNumbers="true" %}
```cpp
#include <Arduino.h>
#include <WiFiClientSecure.h>
#include <SPIFFS.h>
#include "at_client.h"

#include "constants.h"

void setup()
{
    // put your setup code here, to run once:

    // change this to the atSign you own and have the keys to
    const auto *at_sign = new AtSign("@esp"); 
    const auto *java = new AtSign("@java");
    
    // reads the keys on the ESP32
    const auto keys = keys_reader::read_keys(*at_sign); 
    
    // creates the AtClient object (allows us to run operations)
    auto *at_client = new AtClient(*at_sign, keys);  
    
    // pkam authenticate into our atServer
    at_client->pkam_authenticate(SSID, PASSWORD); 

    const auto *at_key = new AtKey("test", at_sign, java);

    at_client->put_ak(*at_key, "Hello, World!");
}

void loop()
{
    // put your main code here, to run repeatedly:
}
```
{% endcode %}

## 3. Receiving the Data in Java

Below is some sample code of receiving this data from a Java app running the [Java SDK](https://github.com/atsign-foundation/at\_java).

A thorough step-by-step explanation can be found in our [video](https://www.youtube.com/watch?v=o1acO81EPVk\&list=PLkZCny-S3rfC93\_Xqd\_HBkK\_dAjDzQ9Et\&index=7\&pp=gAQBiAQB).

```java
package com.example;

import org.atsign.client.api.AtClient;
import org.atsign.common.AtSign;
import org.atsign.common.KeyBuilders;
import org.atsign.common.Keys.SharedKey;

public class App {
    public static void main(String[] args) throws Exception {
        AtSign java = new AtSign("@driving433");
        AtSign esp32 = new AtSign("@icy761");
        AtClient atClient = AtClient.withRemoteSecondary("root.atsign.org:64", java);

        SharedKey sharedKey = new KeyBuilders.SharedKeyBuilder(esp32, java).key("test").build();

        String data = atClient.get(sharedKey).get();
        System.out.println("Data: " + data);
    }
}
```

Your output may be similar to:\


<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption><p>Java Output</p></figcaption></figure>
