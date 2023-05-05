---
description: Basic create, read, update and delete operations with atRecords
---

# CRUD Operations

* create atRecord identifier (ARI?)
* put
* get
* delete

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

## AtClient

As previously mentioned, the AtClientManager stores the actual AtClient itself. You can retrieve the `AtClient` by calling `atClientManager.atClient`.

```dart
AtClient atClient = atClientManager.atClient;
```

### Creating Data

To create data, first you need to create an [atIdentifier](../core/atserver/atrecord.md#atidentifier) to store&#x20;

Rest coming soon!


{% endtab %}

{% tab title="Second Tab" %}



{% endtab %}
{% endtabs %}















