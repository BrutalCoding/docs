---
description: ESP32 will receive the data sent by the Java application
---

# Step 7 - Receive Data with Java

Step 7 - Receiving Data (Java & ESP32) can be found in [video](https://www.youtube.com/watch?v=atVVpMW-dDs\&list=PLkZCny-S3rfC93\_Xqd\_HBkK\_dAjDzQ9Et\&index=8\&pp=gAQBiAQB)

{% embed url="https://www.youtube.com/watch?index=8&list=PLkZCny-S3rfC93_Xqd_HBkK_dAjDzQ9Et&pp=gAQBiAQB&v=atVVpMW-dDs" %}
Step 7 - Receiving Data (Java & ESP32)
{% endembed %}

## 1. Sending Data from the Java App

Sample code of the Java app sending data to the ESP32's atSign. This code is necessary for the ESP32 to receive the data.

Remember to change the atSigns `"@driving433"` and `"@icy761"` to your own atSigns accordingly.

{% code title="App.java" lineNumbers="true" %}
```java
package com.example;

import org.atsign.client.api.AtClient;
import org.atsign.common.AtSign;
import org.atsign.common.KeyBuilders;
import org.atsign.common.Keys.SharedKey;

public class App {
    public static void main(String[] args) throws Exception {
        // the atSign of the Java application (this is the atSign we are authenticating
        // as)
        AtSign java = new AtSign("@driving433");

        // the atSign of the ESP32 (this is the atSign we are sharing data with)
        AtSign esp32 = new AtSign("@icy761");

        // create AtClient object with factory method
        AtClient atClient = AtClient.withRemoteSecondary("root.atsign.org:64", java, true);

        // create a SharedKey
        SharedKey sharedKey1 = new KeyBuilders.SharedKeyBuilder(java, esp32).key("test").build();

        // put the SharedKey in `java`'s atServer for `esp32` to get
        String response = atClient.put(sharedKey1, "test value").get();
        System.out.println("Response: \"" + response + "\"");
    }
}
```
{% endcode %}

A similar output should be achieved; with the commit id as the response. The commit id in our case is `249`, which tells us that the data has successfully been written.

{% code title="Output" %}
```sh
# ...
L184mNFKw4/NwQCAQSiHX2E+jcRs15pD8ZpUkNw==
        RCVD: @data:success
        SENT: llookup:shared_key.icy761@driving433
        RCVD: @driving433@data:J1wykjV3JTzKwUsccZ8JjajKB141ggGQ8vcI6nqv93ggwOanslWxSixrpHXIodDKX+mU/RIw4w+b4lKoRXRI7LWDs+WJgS68vbk8LTjdh+JigO2hFfXDEemZSWzdfZr8RmKY4RJD7XvlRvInadPzArLM20U3L7yAU7iRAuRZVJf7XpsfNbn0/C7kUfVygwEbdXAOzsCJeFft5IPt15z19awighYWZIk0NGmrb+ml9HcrgVTI236Qd2L76wJU8oTOKJfSKjMtt15xYqU2vasjawrVQnCIldFK2E+sxqzU32bS+Pe4UmiL+nxqdE35oBhvSDPoURCZZqmuQuclrZMCMQ==
        SENT: update:isBinary:false:isEncrypted:true:@icy761:test@driving433 DVp5VOiBK/mfAekWXDy9/A==
        RCVD: @driving433@data:249
Response: "data:249"
```
{% endcode %}

Once the data from the Java app's atSign has been sent to the ESP32's atSign, you may move onto the next step.

## 2. Receiving Data on the ESP32

The ESP32 will now go to the Java atSign's atServer to get the data.

1. First, construct the corresponding shared AtKey that will help point to that encrypted data

```cpp
// key name is "test", 
// sharedBy/creator java (@driving433)
// sharedWith/recipient esp32 (@icy761), 
const auto *at_key = new AtKey("test", java, esp32); 
```

2. Simply get the data with the PKAM authenticated at\_client object obtained from [Step 5](pkam-auth.md).

```cpp
const auto value = at_client->get_ak(*at_key);
std::cout << value << std::endl;
```

3. Your complete code should look similar:

<pre class="language-cpp"><code class="lang-cpp">#include &#x3C;Arduino.h>
#include &#x3C;WiFiClientSecure.h>
#include &#x3C;SPIFFS.h>
#include "at_client.h"

#include "constants.h"

void setup()
{
	// put your setup code here, to run once:

    // change this to the atSign you own and have the keys to
    const auto *esp32 = new AtSign("@esp"); 
	const auto *java = new AtSign("@java");
    
    // reads the keys on the ESP32
    const auto keys = keys_reader::read_keys(*esp32); 
    
    // creates the AtClient object (allows us to run operations)
    auto *at_client = new AtClient(*esp32, keys);  
    
    // pkam authenticate into our atServer
    at_client->pkam_authenticate(SSID, PASSWORD); 

    // key name is "test", 
<strong>    // sharedBy/creator java (@driving433)
</strong>    // sharedWith/recipient esp32 (@icy761), 
<strong>    const auto *at_key = new AtKey("test", java, esp32); 
</strong>
    const auto value = at_client->get_ak(*at_key);
    std::cout &#x3C;&#x3C; value &#x3C;&#x3C; std::endl;
}

void loop()
{
}
</code></pre>

