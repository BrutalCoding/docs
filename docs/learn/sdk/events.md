---
description: Pub/sub events with atRecords
---

# Events

* Notify / monitor

{% tabs %}
{% tab title="Flutter / Dart" %}
In Dart, the AtClient is stored within the AtClientManager. Once an atSign has been [onboarded](onboarding.md), you will be able to access the AtClientManager for its associated atSign.

## AtClientManager

AtClientManager is a [singleton](https://en.wikipedia.org/wiki/Singleton\_pattern) model. When `AtClientManager.getInstance()` is called, it will get the AtClientManager instance for the last onboarded atSign.

```dart
AtClientManager atClientManager = AtClientManager.getInstance();
```

{% hint style="info" %}
If you need simultaneous access to multiple atClients, you need to create a new [isolate](https://dart.dev/language/concurrency#how-isolates-work) for each additional atClient, and onboard its atSign within the isolate.&#x20;

An example of this pattern can be found in [at\_daemon\_server](https://github.com/atsign-foundation/at\_services/tree/trunk/packages/at\_daemon\_server/lib/src/server).
{% endhint %}
{% endtab %}

{% tab title="Java" %}

{% endtab %}

{% tab title="Untitled" %}
Coming soon!
{% endtab %}
{% endtabs %}
