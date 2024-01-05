---
description: Pub/sub events with atRecords
---

# Events

{% tabs %}
{% tab title="Flutter / Dart" %}
In Dart, the AtClient is stored within the AtClientManager. Once an atSign has been [onboarded](onboarding.md), you will be able to access the AtClientManager for its associated atSign.

### AtClientManager

AtClientManager is a [singleton](https://en.wikipedia.org/wiki/Singleton\_pattern) model. When `AtClientManager.getInstance()` is called, it will get the AtClientManager instance for the last onboarded atSign.

```dart
AtClientManager atClientManager = AtClientManager.getInstance();
```

{% hint style="info" %}
If you need simultaneous access to multiple atClients, you need to create a new [isolate](https://dart.dev/language/concurrency#how-isolates-work) for each additional atClient, and onboard its atSign within the isolate.

An example of this pattern can be found in [at\_daemon\_server](https://github.com/atsign-foundation/at\_services/tree/trunk/packages/at\_daemon\_server/lib/src/server).
{% endhint %}

### AtClient

As previously mentioned, the AtClientManager stores the actual AtClient itself. You can retrieve the `AtClient` by calling `atClientManager.atClient`.

```dart
AtClient atClient = atClientManager.atClient;
```

#### atID

Before you can do anything with an atRecord, you need an [atID](../core/atrecord.md#atidentifier) to represent it.

If you don't know how to create an atID, please see the [reference](atid-reference/) first.

{% hint style="info" %}
The following examples use the self atID `phone.wavi@<current atSign>`

It is up to the developer to modify the atID according to their use case.
{% endhint %}
{% endtab %}

{% tab title="Other Clients" %}
Coming soon!
{% endtab %}
{% endtabs %}
