# atID Reference

{% hint style="warning" %}
atID was previous called "AtKey".

Please note that any reference to the word "AtKey" in this document is not associated with cryptographic keys.
{% endhint %}

{% hint style="warning" %}
This article explains how to create an atID in the atClient SDK.

If you are unfamiliar with atIDs please read [this](../core/atrecord.md#atid) first.
{% endhint %}

{% tabs %}
{% tab title="Flutter / Dart" %}
The [at\_commons](https://pub.dev/packages/at\_commons) package contains common elements used in a number of Atsign's Flutter and Dart packages. This package needs to be included in the application in order to create atIDs.

### Installation

First add the package to your project:

```
flutter pub add at_commons
```

Or add the package to your `pubspec.yaml` manually:

{% code title="pubspec.yaml" %}
```yaml
dependencies:
  flutter:
    sdk: flutter
  at_client_mobile: ^3.2.9
  at_onboarding_flutter: ^6.0.3
  at_commons: ^3.0.45
```
{% endcode %}

### Usage

{% hint style="warning" %}
atID was previously called "AtKey".

The code has not fully been migrated to reflect this name change, so please assume that an "AtKey" is functionally equivalent to an atID.
{% endhint %}

See below for how to create the various types of atIDs.

#### Public atID

To create a public atID, first use the `AtKey.public` builder to configure it, then call `.build` to create it.

{% code title="AtKey.public signature" %}
```dart
static PublicKeyBuilder public(String key,
    {String? namespace, String sharedBy = ''})
```
{% endcode %}

The `build` method on `PublicKeyBuilder` takes no parameters.

**Example**

`public:phone.wavi@alice`

{% code overflow="wrap" %}
```dart
AtKey myPublicID = AtKey.public('phone', namespace: 'wavi', sharedBy: '@alice').build();
```
{% endcode %}

#### Self atID

To create a self atID, first use the `AtKey.self` builder to configure it, then call `.build` to create it.

{% code title="AtKey.self signature" %}
```dart
static SelfKeyBuilder self(String key,
    {String? namespace, String sharedBy = ''})
```
{% endcode %}

The `build` method on `SelfKeyBuilder` takes no parameters.

**Example**

`phone.wavi@alice`

{% code overflow="wrap" %}
```dart
AtKey mySelfID = AtKey.self('phone', namespace: 'wavi', sharedBy: '@alice').build();
```
{% endcode %}

#### Private atID

To create a private atID, first use the `AtKey.private` builder to configure it, then call `.build` to create it.

{% hint style="info" %}
The difference between a private and a self atID is that the private atID is hidden by default when using the [atProtocol scan verb](https://github.com/atsign-foundation/at\_protocol/blob/trunk/specification/at\_protocol\_specification.md#the-scan-verb).
{% endhint %}

{% code title="AtKey.private signature" %}
```dart
static PrivateKeyBuilder private(String key, {String? namespace})
```
{% endcode %}

The `build` method on `PrivateKeyBuilder` takes no parameters.

**Example**

`privatekey:phone.wavi@alice`

{% code overflow="wrap" %}
```dart
AtKey myPrivateID = AtKey.private('phone', namespace: 'wavi').build();
```
{% endcode %}

#### Shared atID

To create a shared atID, first use the `AtKey.shared` builder to configure it, then call `.build` to create it.

{% code title="AtKey.shared signature" %}
```dart
static SharedKeyBuilder shared(String key,
    {String? namespace, String sharedBy = ''})
```
{% endcode %}

The `build` method on `SharedKeyBuilder` takes no parameters.

**Example**

`@bob:phone.wavi@alice`

{% code overflow="wrap" %}
```dart
AtKey sharedKey = (AtKey.shared('phone', 'wavi')
    ..sharedWith('@bob')).build();
```
{% endcode %}

**Caching shared atIDs**

To cache a shared atID, you can do a [cascade](https://dart.dev/language/operators#cascade-notation) call on `SharedKeyBuilder.cache`.

{% code title="Caching example" %}
```dart
AtKey atKey = (AtKey.shared('phone', namespace: 'wavi', sharedBy: '@alice')
 ..sharedWith('@bob')
 ..cache(1000, true))
 .build();
```
{% endcode %}

### API Docs

You can find the API reference for the entire package available on [pub](https://pub.dev/documentation/at\_commons/latest/).

The `AtKey` class API reference is available [here](https://pub.dev/documentation/at\_commons/latest/at\_commons/AtKey-class.html).
{% endtab %}

{% tab title="Java" %}
Coming soon!
{% endtab %}

{% tab title="Other Clients" %}
Coming soon!
{% endtab %}
{% endtabs %}
