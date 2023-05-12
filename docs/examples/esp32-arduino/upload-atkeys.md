---
description: Upload the atSign .atKeys to the ESP32.
---

# Step 3 - Uploading your .atKeys

Step 3 - Uploading your `.atKeys` can be found in video on our YouTube [here](https://www.youtube.com/watch?v=GBoX\_PqwMGo\&list=PLkZCny-S3rfC93\_Xqd\_HBkK\_dAjDzQ9Et\&index=5).

{% embed url="https://www.youtube.com/watch?index=5&list=PLkZCny-S3rfC93_Xqd_HBkK_dAjDzQ9Et&v=GBoX_PqwMGo" %}
Step 3 - Uploading your `.atKeys`
{% endembed %}

## 1. Copy `.atKeys` in the `data/` Directory

Firstly, create a `data/` directory in the root of your PlatformIO project. Take your `.atKeys` file and place it inside of this newly created directory.

<figure><img src="../../.gitbook/assets/image (7).png" alt="" width="235"><figcaption><p><code>data/</code> directory with <code>.atKeys</code></p></figcaption></figure>

## 2. Putting your ESP32 into Download Mode and Uploading the `.atKeys`

1. Put your ESP32 into download mode by holding down the `BOOT` button and press the `RESET` button ONCE (synonymously the `EN` button); while still holding the `BOOT` button. It should be in download mode as long as you are holding `BOOT` down.
2. While it is in download mode, run the **Upload File System Image** command. This can be seen under **Project Tasks > Platform**.&#x20;

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

1. If you still find **Project Tasks**, open the command palette (via `Ctrl/Cmd` + `Shift` + `P`) and run the "Explorer: Focus on **Project Tasks** View" command
2. You should get a **\[SUCCESS]** in your terminal.&#x20;
3. If you do not get a **\[SUCCESS]**, make sure you are using a **data** USB-A to Micro USB cable (some cables do not transmit data). Also make sure the ESP32 is plugged in (it has happened before 😂).&#x20;
4. If you are still running into issues, please seek support on our [discord](https://discord.atsign.com).
