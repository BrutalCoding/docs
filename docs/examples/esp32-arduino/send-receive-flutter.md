---
description: Learn how to send/receive encrypted data from/to an ESP32 and a Flutter app
---

# Step 8 - Send & Receive Data with Flutter

Step 8 - Sending & Receiving Data with a Flutter App (ESP32 & Flutter) can be found in [video](https://www.youtube.com/watch?v=L24F-SwRC\_s\&list=PLkZCny-S3rfC93\_Xqd\_HBkK\_dAjDzQ9Et\&index=9\&t=8s\&pp=gAQBiAQB)

{% embed url="https://www.youtube.com/watch?index=9&list=PLkZCny-S3rfC93_Xqd_HBkK_dAjDzQ9Et&pp=gAQBiAQB&t=8s&v=L24F-SwRC_s" %}
Step 8 - Sending & Receiving Data with a Flutter App (ESP32 & Flutter)
{% endembed %}

{% hint style="warning" %}
Ensure that Step 1 to Step 5 have been completed successfully. The [video](https://www.youtube.com/watch?v=L24F-SwRC\_s\&list=PLkZCny-S3rfC93\_Xqd\_HBkK\_dAjDzQ9Et\&index=9\&t=8s\&pp=gAQBiAQB) also covers this step-by-step.
{% endhint %}

## 1. ESP32 Onboarding

{% hint style="info" %}
Completing Steps 1-5 will help make this step make a lot more sense.
{% endhint %}

1. Initialize AtSign constant objects of the ESP32 and the Flutter App

```cpp
const auto *esp32 = new AtSign("@tastelessbanana");
const auto *flutter = new AtSign("@jeremy_0");
```

2. Next, we will read the keys that was uploaded to the ESP32. These `.atKeys` should match the atSign that you intend the ESP32 to be using.

```cpp
const auto keys = keys_reader::read_keys(*esp32);
```

3. Initialize the `at_client` object and pkam authenticate.

```cpp
auto *at_client = new AtClient(*esp32, keys);
at_client->pkam_authenticate(SSID, PASSWORD);
```

4. The final code block inside of `void setup() {}` should look similar to:

```cpp
const auto *esp32 = new AtSign("@tastelessbanana");
const auto *flutter = new AtSign("@jeremy_0");

const auto keys = keys_reader::read_keys(*esp32);

auto *at_client = new AtClient(*esp32, keys);

at_client->pkam_authenticate(SSID, PASSWORD);
```

5. Now, we are ready to write code for the ESP32 to send/receive data.

## 2. Flutter App Onboarding

1. Get `at_app`, our CLI tool for quickly creating atPlatform Flutter apps. Note: you will need to have [Flutter installed](https://docs.flutter.dev/get-started/install).

{% code title="Terminal" %}
```sh
dart pub global activate at_app
```
{% endcode %}

2. Open an empty directory on your system, and run `at_app create .`

```sh
mkdir ef_flutter # making a directory called "ef_flutter"
cd ef_flutter # changing into that directory
at_app create . # creating an at_app in this directory
```

3. Open your desired emulator/simulator, and run `flutter run`

```sh
flutter run
```

A similar screen should appear

<figure><img src="../../.gitbook/assets/image (1).png" alt="" width="228"><figcaption><p>Onboarding Screen</p></figcaption></figure>

4. Drag your `.atKeys` into the app and it should upload your keys to your device. These keys should be the keys of the atSign you intend to be the Flutter app's atSign.&#x20;

<figure><img src="../../.gitbook/assets/image (2).png" alt="" width="336"><figcaption><p>Dragging and Dropping <code>@jeremy_0</code>'s <code>.atKeys</code> into the iOS Simulator</p></figcaption></figure>

5. After completing this, select "Upload backup key file" and select the keys you've uploaded.&#x20;

<figure><img src="../../.gitbook/assets/image (5).png" alt="" width="326"><figcaption><p>Upload backup key file</p></figcaption></figure>

6. You should have successfully onboarded your atSign into the Flutter App. Now, your Flutter app is setup and some code is ready to be written for sending/receiving data.

<figure><img src="../../.gitbook/assets/image (14).png" alt="" width="350"><figcaption><p>Successfully Onboarded</p></figcaption></figure>

## 3. Send Data on Flutter App -> Receive Data on ESP32

### A. Flutter App (Sending Data)

On the home screen, let's add a button that will send the data to the ESP32's atSign when this button is pressed.

{% code title="home_screen.dart" %}
```dart
ElevatedButton(
  onPressed: () async {
    // put code
    
    // put key
    // @esp32:num.soccer0@flutter
    final AtKey sharedWithESP32 = AtKey()
      ..sharedWith = esp32
      ..key = 'num'
      ..namespace = 'soccer0'
      ..sharedBy = flutter;
      
    // put the data
    bool success =
        await atClient.put(sharedWithESP32, 'init');
        
    // sync with remote
    atClient.syncService.sync();
    
    print('write succes? $success');
  },
  child: Text('Do Thing'),
),
```
{% endcode %}

### B. ESP32 (Receiving Data)

Code for the ESP32 getting the data from the Flutter App's atSign

1. After PKAM authentication, let us first create an AtKey that points to the data.

```cpp
// key name is "num"
// the sharedBy is Flutter's atSign
// the sharedWith is ESP32's atSign
auto *shared_with_us = new AtKey("num", flutter, esp32);
```

2. Set the namespace. The Dart SDK currently enforces namespaces.

```cpp
shared_with_us->namespace_str = "soccer0";
```

3. Get the data

```cpp
const auto data = at_client->get_ak(*shared_with_us);
```

4. The full code inside of `void setup() {}` should look similar to:

{% code title="main.cpp" %}
```cpp
// @esp32:num.soccer0@flutter
auto *shared_with_us = new AtKey("num", flutter, esp32);
shared_with_us->namespace_str = "soccer0";

const auto data = at_client->get_ak(*shared_with_us);
```
{% endcode %}

5. Run **Upload and Monitor** and the data should be successfully fetched by the ESP32.&#x20;

Print it with:

```cpp
std::cout << data << std::endl;
```

## 4. Send Data on ESP32 -> Receive Data on Flutter App

### A. ESP32 (Sending Data)

In this step, the ESP32 will send data to Flutter's atSign.

1. First, we construct the AtKey. It is important to coordinate the namespace between applications. In this case, the namespace is `soccer0`.

```dart
auto *shared_with_flutter = new AtKey("num", esp32, flutter);
shared_with_flutter->namespace_str = "soccer0";
```

2. Next, run `at_client->put_ak` to put the AtKey into the ESP's atServer

```cpp
const auto val = std::string{"hello"};
at_client->put_ak(*shared_with_flutter, val);
```

3. Run **Upload and Monitor**
4. Code in `void setup() {}` should look similar:

```cpp
// @flutter:num.soccer0@esp32
auto *shared_with_flutter = new AtKey("num", esp32, flutter);
shared_with_flutter->namespace_str = "soccer0";

const auto val = std::string{"hello"};

at_client->put_ak(*shared_with_flutter, val);

std::cout << "put value :" << val << "\n";
```

### B. Flutter App (Receiving Data)

Similarly in the [previous step](send-receive-flutter.md#a.-flutter-app-sending-data), we will construct an AtKey such that we are getting data from the ESP32's atSign's atServer and use `atClient.get(atKey)` to retrieve that value.

<pre class="language-dart"><code class="lang-dart">// 1. get code
// get key
// @flutter:num.soccer0@esp32
final AtKey sharedWithUs = AtKey()
    ..sharedWith = flutter
<strong>    ..namespace = 'soccer0'
</strong>    ..key = 'num'
    ..sharedBy = esp32;

final String value = (await atClient.get(sharedWithUs)).value;
</code></pre>
