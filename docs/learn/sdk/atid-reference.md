# atKey Reference

{% hint style="warning" %}
AtKey

Please note that any reference to the word "AtKey" in this document is not associated with cryptographic keys. The atKey is the "key" of the key-value pair that makes up an atRecord.
{% endhint %}

{% hint style="warning" %}
This article explains how to create an atKey in the atClient SDK.

If you are unfamiliar with atKeys please read [this](../core/atrecord.md#atid) first.
{% endhint %}

{% tabs %}
{% tab title="Flutter / Dart" %}
The [at\_commons](https://pub.dev/packages/at\_commons) package contains common elements used in a number of Atsign's Flutter and Dart packages. This package needs to be included in the application in order to create atKeys.

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

See below for how to create the various types of atKeys.

#### Public atKey

To create a public atKey, first use the `AtKey.public` builder to configure it, then call `.build` to create it.

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

#### Self atKey

To create a self atkeyD, first use the `AtKey.self` builder to configure it, then call `.build` to create it.

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

#### Private atKey

To create a private atKey, first use the `AtKey.private` builder to configure it, then call `.build` to create it.

{% hint style="info" %}
The difference between a private and a self atkey is that the private atKey is hidden by default when using the [atProtocol scan verb](https://github.com/atsign-foundation/at\_protocol/blob/trunk/specification/at\_protocol\_specification.md#the-scan-verb).
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

#### Shared atKey

To create a shared atKey, first use the `AtKey.shared` builder to configure it, then call `.build` to create it.

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

**Caching shared atKeys**

To cache a shared atKey, you can do a [cascade](https://dart.dev/language/operators#cascade-notation) call on `SharedKeyBuilder.cache`.

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
{% endtabs %}
