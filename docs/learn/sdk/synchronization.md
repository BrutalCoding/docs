# Synchronization

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

### SyncService

SyncService syncs the client app and remote secondary server’s changes:

* If the client app’s changes are ahead, it pushes the changes to the remote secondary.
* If the remote secondary is ahead, it pulls the changes to the client app.

You can retrieve the SyncService from the AtClientManager like so:

```dart
SyncService syncService = atClientManager.syncService;
```

### Performing Syncs

To simply issue a sync, call the `.sync` function:
{% endtab %}

{% tab title="Java" %}
Currently not supported, see the "Other Clients" tab for more info.
{% endtab %}

{% tab title="Other Clients" %}
At this time, other clients do not support local persistence of the atServer, and thus do not require synchronization.

Future enhancements may enable support for your desired platform. If you require support, please file an issue on the appropriate GitHub repository:

* [Java](https://github.com/atsign-foundation/at\_java)
* [C/C++](https://github.com/atsign-foundation/at\_c)
{% endtab %}
{% endtabs %}
