---
description: Basic create, read, update and delete operations with atRecords
---

# CRUD Operations

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

#### atKey

Before you can do anything with an atRecord, you need an [atKey](../core/atrecord.md#atidentifier) to represent it.

If you don't know how to create an atKey, please see the [reference](atid-reference.md) first.

{% hint style="info" %}
The following examples use the self atKey `phone.wavi@<current atSign>`

It is up to the developer to modify the atKey according to their use case.
{% endhint %}

#### Creating / Updating Data

To create data the `put` method is used, this method accepts text (`String`) or binary (`List<int>`).

{% code overflow="wrap" %}
```dart
String currentAtSign = atClient.getCurrentAtSign()!;
AtKey myID = AtKey.self('phone', namespace: 'wavi',
                        sharedBy: currentAtSign).build();
String dataToStore = "123-456-7890";
bool res = await atClient.put(myID, dataToStore);
```
{% endcode %}

<pre class="language-dart" data-title="put signature"><code class="lang-dart">Future&#x3C;bool> put(
    AtKey key,
    dynamic value,
    {bool <a data-footnote-ref href="#user-content-fn-1">isDedicated</a> = false,
<strong>    PutRequestOptions? putRequestOptions});
</strong></code></pre>

**Strongly Typed Methods**

Since `put` accepts both `String` or `List<int>` as a value, the typing is dynamic. atClient also contains the strongly typed `putText` which only accepts `String` for the value, or `putBinary` which only accepts `List<int>` for the value.

**To update existing data**

Updating existing data is done by doing a put to the same atKey, this will overwrite any existing data stored in the atRecord.

```dart
List<int> binaryData = [1, 2, 3, 4];
bool res = await atClient.put(myID, binaryData);
```

The bytes `[1, 2, 3, 4]` have now replaced the string `"123-456-7890"`.

#### Reading Data

There are two parts to reading data using the atClient SDK:

1. Scanning for and listing out the atKeys for atRecords that can be retrieved
2. Retrieving the atRecord for a given atKey

**1. Scanning and listing** atKey**s**

There are two methods available for scanning and listing atKeys:

1. `getAtKeys` which provides the list in Class format (i.e. `List<AtKey>`)
2. `getKeys` which provides the list in String format (i.e. `List<String>`)

Both methods accept the same parameters, only the return type is different. So we will show the more commonly used getAtKeys signature:

{% code title="getAtKeys signature" %}
```dart
Future<List<AtKey>> getAtKeys(
    {String? regex,
    String? sharedBy,
    String? sharedWith,
    bool showHiddenKeys = false});
```
{% endcode %}

_regex_

A regular expression used to filter the list of atKeys.

_sharedBy_

Filter the list of atKeys to only include ones shared by a particular atSign.

_sharedWith_

Filter the list of atKeys to only include ones shared with a particular atSign.

_showHiddenKeys_

A boolean flag to enable the inclusion of hidden atKeys (default = `false`)

**Usage**

Get all available (non-hidden) atKeys:

```dart
List<AtKey> allIDs = await atClient.getAtKeys();
```

All atKeys which end with ".wavi" in the record identifier part:

```dart
List<AtKey> waviIDs = await atClient.getAtKeys(regex: '^.*\.wavi@.+$');
```

**2. Retrieving atRecords by** atKey

To retrieve an atRecord, you must know the atKey and pass it to the `get` method.

{% code title="get signature" %}
```dart
Future<AtValue> get(
    AtKey key,
    {bool isDedicated = false,
    GetRequestOptions? getRequestOptions});
```
{% endcode %}

Calling this function will return an AtValue, and update the atKey passed to it with any changes to the metadata.

**Usage**

<pre class="language-dart"><code class="lang-dart">AtValue atValue = await atClient.get(myID);
String? text = atValue.<a data-footnote-ref href="#user-content-fn-2">value</a>;
</code></pre>

#### Deleting Data

To delete data, simply call the `delete` method with the atKey for the atRecord to delete.

{% code title="delete signature" %}
```dart
Future<bool> delete(
    AtKey key,
    {bool isDedicated = false});
```
{% endcode %}

**Usage**

```dart
bool res = await atClient.delete(myID);
```

### API Docs

You can find the API reference for the entire package available on [pub](https://pub.dev/documentation/at\_client/latest/).

The `AtClient` class API reference is available [here](https://pub.dev/documentation/at\_client/latest/at\_client/AtClient-class.html).
{% endtab %}
{% endtabs %}



[^1]: This has been deprecated, and will be ignored.

[^2]: If metaData.isBinary is true, then this will be a List\<int>.
