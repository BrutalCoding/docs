---
description: Building & Uploading your code to your ESP32 for the first time
---

# Step 4 - Building & Uploading Your Project

Step 4 - Building & Uploading Your Project can be found in video format on our YouTube [here](https://www.youtube.com/watch?v=93Jf4orcxPA\&list=PLkZCny-S3rfC93\_Xqd\_HBkK\_dAjDzQ9Et\&index=5\&pp=gAQBiAQB)

{% embed url="https://www.youtube.com/watch?index=5&list=PLkZCny-S3rfC93_Xqd_HBkK_dAjDzQ9Et&pp=gAQBiAQB&v=93Jf4orcxPA" %}
Step 4 - Building & Uploading Your Project
{% endembed %}



## 1. Setting up `main.cpp`

1. First, create `main.cpp` inside of the `src/` directory. If it already exists, move onto the next step below.
2. Add the following headers to `main.cpp`

```cpp
#include <WiFiClientSecure.h>
#include <SPIFFS.h>
#include "at_client.h"
```

## 2. Building the Project

To make sure all dependencies are correctly setup, we are going to build the project locally on our machine. Note: this does not upload code to the ESP32; we will do that in the next steps.

1. Run **Build** under **Project Tasks**. See [here](setup-project.md#2.-become-familiar-with-project-tasks), if you do not know what **Project Tasks** is.

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption><p>Running <strong>Build</strong> under <strong>Project Tasks</strong></p></figcaption></figure>

2. You should get a successfully built project with similar output

```sh
Indexing .pio/build/esp32dev/libFrameworkArduino.a
Linking .pio/build/esp32dev/firmware.elf
Retrieving maximum program size .pio/build/esp32dev/firmware.elf
Checking size .pio/build/esp32dev/firmware.elf
Advanced Memory Usage is available via "PlatformIO Home > Project Inspect"
RAM:   [=         ]   8.8% (used 28984 bytes from 327680 bytes)
Flash: [====      ]  36.4% (used 476641 bytes from 1310720 bytes)
Building .pio/build/esp32dev/firmware.bin
esptool.py v4.4
Creating esp32 image...
Merged 2 ELF sections
Successfully created esp32 image.
======================================================== [SUCCESS] Took 7.42 seconds ========================================================
```

3. If you are having trouble, your `platform.ini` and `main.cpp` should be similar:

<pre class="language-cpp" data-title="main.cpp" data-line-numbers><code class="lang-cpp"><strong>#include &#x3C;Arduino.h>
</strong><strong>#include &#x3C;WiFiClientSecure.h>
</strong><strong>#include &#x3C;SPIFFS.h>
</strong><strong>#include "at_client.h"
</strong><strong>
</strong><strong>void setup()
</strong><strong>{
</strong><strong>    // setup code here, to run once:
</strong><strong>}
</strong>
<strong>void loop()
</strong><strong>{
</strong><strong>    // put your main code here, to run repeatedly:
</strong><strong>}
</strong></code></pre>

{% code title="platform.ini" lineNumbers="true" %}
```ini
; PlatformIO Project Configuration File
;
;   Build options: build flags, source filter
;   Upload options: custom upload port, speed and extra flags
;   Library options: dependencies, extra library storages
;   Advanced options: extra scripting
;
; Please visit documentation for the other options and examples
; https://docs.platformio.org/page/projectconf.html

[env:esp32dev]
platform = espressif32
board = esp32dev
framework = arduino
lib_deps = 
	jeremytubongbanua/at_client@^0.2.4
	bblanchon/ArduinoJson@^6.21.2
monitor_speed = 115200
```
{% endcode %}

## 3. Uploading Code to the ESP32

Now let's upload our code to the ESP32 for the first time.

1. Put the ESP32 into **download mode** by holding down the `BOOT` button (synonymously the `EN`  button) and pressing the `RESET` button; still while holding the `BOOT` button. It should be in download mode as long as you are still holding `BOOT` down.
2. Run the **Upload and Monitor** command under [**Project Tasks**](setup-project.md#2.-become-familiar-with-project-tasks)
3. You should get a \[SUCCESS].

## 4. (Optional) Printing Hello World

Let's print `Hello, World!` into the console using `std::cout`.&#x20;

1. Add the following code to your `loop()` function inside of `main.cpp`

{% code title="main.cpp" %}
```cpp
void loop()
{
    std::cout << "Hello, World!" << std::endl;
    delay(1000);
}
```
{% endcode %}

2. Put your ESP32 into download mode and run the **Upload and Monitor** command.
