---
description: Let's talk.
---

# Put and Get data asynchronously

## Sending and receiving data

The next step is to send and receive for this to work we need to get the atKeys file containing the cryptographic keys and login or onboard to the atServer. From there we can `put` data and `get` data as if a database was local to us but in fact data is remote on the data owners atServer.

This is achieved by every data element having an owner (the sending atSign) and a receiving atSign, behind the scenes the atSDK encrypts the data and sends it on to the atServer for delivery. All we need to do is a simple:

```dart
await atClient.put(sharedRecordID, message, putRequestOptions: pro);
```

of course we also have to setup the atClient object and onboard but that is all in the `at_key_put.dart` file for you. so lets send some data.&#x20;

\*Note here we are using the atSigns activated in the previous section just substitute your own atSigns

```
 dart run .\bin\at_key_put.dart -a "@energetic22" -n "atsign" -o "@7capricorn" -m "hello world" 
 
 dart run .\bin\at_key_get.dart -a "@7capricorn" -n "atsign" -o "@energetic22"
```

<figure><img src="../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

You may notice yourself that the first time you fail to get the message. This is because we specifiied in the metadata that the TTL is 60000 millisecond or 1 minute. Try again as you see in the above image and you should get your message too.

```dart
    ..metadata = (Metadata()
      ..ttl = 60000 // expire after 60 seconds
      ..ttr = -1); // allow recipient to keep a cached copy
```

The code is worth taking a look at the code as it less than 70 lines, but allows data to transferred from a device anywhere to a device anywhere, and the data is fully encrypted.&#x20;

The data in this example is "store and forward", which is ideal for many use cases but sometimes we need near real time data and that's what we cover next.
