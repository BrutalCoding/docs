---
description: Fulfill these prerequisites before continuing further
---

# Step 1 - Prerequisites

## Prerequisites

* [VSCode](https://code.visualstudio.com/download) with the [PlatformIO extension](https://platformio.org/install/ide?install=vscode)
* [2 atSigns](../../core/atsign.md#how-do-i-get-an-atsign) and their `.atKeys` files. Watch this [video](prerequisites.md#generating-your-.atkeys-file) for getting your `.atKeys`
* An [ESP32](https://www.espressif.com/en/products/modules/esp32) and a micro-USB **data** cable for connecting your ESP32 to your computer.

It is important that you get and own these 2 atSigns and have their associated `.atKeys` files. Also ensure that the cable you are using for your project is a **data** cable. It is a common mistake to be using a [non-data cable](#user-content-fn-1)[^1] when found that your ESP32 is not being recognized by the PlatformIO extension.

A sensor is not required for this demo. We will simply be transmitting some arbitrary string of text between an ESP32 and a Java or Flutter app.

## Generating your `.atKeys` file

{% embed url="https://www.youtube.com/watch?index=1&list=PLkZCny-S3rfC93_Xqd_HBkK_dAjDzQ9Et&pp=gAQBiAQB&t=8s&v=8xJnbsuF4C8" %}
Step 1 - Uploading your `.atKeys`
{% endembed %}

[^1]: Non-data cables only support charging and are not capable of data-transfer.
