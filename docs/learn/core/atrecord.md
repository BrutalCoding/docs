---
description: The format atServers use to store and share data.
---

# atRecord

{% hint style="info" %}
At Atsign, whenever we mention the word "key" assume we are talking about a cryptographic key unless otherwise stated.&#x20;

For the time being this is not strictly true, as we are currently migrating the identifier portion of an atRecord from the name "atKey" to the name "atID".
{% endhint %}

atRecords are the data records that are stored by the atServers. We use the common key-value pair format. By this, we mean non-cryptographic key, so we instead call them "identifier-value pairs" to prevent confusion.

## atID

An atID is the identifier half of the "identifier-value" pair. Similar to the primary key of a tabular database, the atID must be a unique string which represents the data.

There are 5 different types of an atID.

| Type    | Purpose                                                                                  |
| ------- | ---------------------------------------------------------------------------------------- |
| Public  | Store and share public data which can be seen by anyone.                                 |
| Self    | Store data which can only be seen by the owner.                                          |
| Shared  | Store and share private data which can only be seen by the owner and intended recipient. |
| Private | Store data which can only be seen by the owner, hidden by default.                       |
| Cached  | Cache shared data from other atSigns for performance and offline mode.                   |

### Structure of an atID

```
[cached:]<visibility scope>:<record ID><owner’s atSign>
```

#### Cached

A marker for whether it is a cached key or not.

#### Visibility Scope

A marker for who has access to the key.

#### Record ID

A unique string used to represent the atRecord.

#### Owner's atSign

The owner (i.e. creator's) atSign for that particular atRecord.

<details>

<summary>Rules for atIDs</summary>

1. Length of an atID should not be more than 240 characters\
   (a limitation of the current implementation of the atServer, not a protocol limitation)
2. A maximum of 55  7-bit characters for the atSign
3. Allowed characters in an entity are: `[\w._,-"']`
4. Namespace is mandatory in the current implementation of the protocol\
   i.e entity must follow the notation: `<identifier>.<namespace>`
5. Cached atIDs should have a different owner than the current atSign
6. Visibility scope and owner cannot be the same for a shared atID
7. Reserved atIDs cannot be [modified](../sdk/crud-operations.md) or [notified](../sdk/events.md)
8. For newly created atIDs, the owner must match the current atSign



</details>

<details>

<summary>Reserved atIDs</summary>

The following is a list of reserved atIDs which the atServer requires to function.

**Don't** try to delete or overwrite these keys, the atServer cannot function without them.

* `privatekey:at_pkam_privatekey`
* `privatekey:at_pkam_publickey`
* `public:publickey`
* `privatekey:privatekey`
* `shared_key`
* `privatekey:self_encryption_key`
* `signing_privatekey`
* `public:signing_publickey`
* `privatekey:at_secret`
* `privatekey:at_secret_deleted`

</details>

<details>

<summary>Example atIDs</summary>

#### Public atID

`public:location@alice`

#### Private atID

`privatekey:pk1@alice`

#### Shared atID

`@bob:phone@alice`

#### Internal atID

`_latestnotificationid.at_skeleton_app@alice`

#### Cached atID

`cached:@bob:phone@alice`

</details>

## atMetadata

Metadata of the atRecord is also stored and describes the following properties of the atValue.

| **Meta Attribute** | **Auto create?** | **Description**                                                                                                                  |
| ------------------ | ---------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| availableFrom      | Yes              | A Date and Time derived from the ttb (now + ttb). A Key should be only available after availableFrom.                            |
| ccd                | No               | Indicates if a cached key needs to be deleted when the atSign user who has originally shared it deletes it.                      |
| createdBy          | Yes              | atSign that has created the key                                                                                                  |
| createdOn          | Yes              | Date and time when the key has been created.                                                                                     |
| expiresOn          | Yes              | A Date and Time derived from the ttl (now + ttl). A Key should be auto deleted once it expires.                                  |
| isBinary           | No               | True if the value is a binary value.                                                                                             |
| isCached           | No               | True if the key can be cached by another atSign user.                                                                            |
| isEncrypted        | No               | True if the value is encrypted                                                                                                   |
| refreshAt          | No               | A Date and Time derived from the ttr. The time at which the key gets refreshed.                                                  |
| sharedWith         | No               | atSign of the user with whom the key has been shared. Can be null if not shared with anyone.                                     |
| updatedOn          | Yes              | Date and time when the key has been last updated.                                                                                |
| ttb                | No               | Time to birth in milliseconds.                                                                                                   |
| ttl                | No               | Time to live in milliseconds.                                                                                                    |
| ttr                | No               | Time in milliseconds after which the cached key needs to be refreshed. A ttr of -1 indicates that the key can be cached forever. |

## atValue

Text or binary values can be saved in an atServer.&#x20;

{% hint style="warning" %}
The size of the value saved in an atServer is bound by the atProtocol's config parameter "maxBufferSize".
{% endhint %}
