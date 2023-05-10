---
description: A unique identifier which serves as the address of the atServer
---

# atSign

## What is an atSign?

An atSign (e.g. @alice) is simply a resolvable address (kind of like an email address) for an atServer. Anything can have an atSign, a person, organization, or thing (IoT), even individual songs or videos could have atSign addresses.

### What's it used for?

An atSign is used to protect and securely exchange information with other atSigns without any chance of surveillance, impersonation, or theft of the information by anyone.

### What characters can be used in an atSign?

An atSign supports any combination of UTF-7 characters up to 55 characters in length to be used. This provides an enormous name space of 10^224 atSigns.

### How do I get an atSign?

Head to [the registrar site](https://my.atsign.com/go). It is recommended that you login with your email. One email can hold up to 10 free atSigns and unlimited paid atSigns.

### How do I generate my associated keys?

There are multiple ways to generate the associated `.atKeys` of an atSign.&#x20;

* [Using AtmospherePro](https://www.youtube.com/watch?v=8xJnbsuF4C8) (3 minute video)
* [Java Registration CLI](https://github.com/atsign-foundation/at\_java/blob/trunk/getting\_started\_guide.md)
* Dart [at\_onboarding\_cli/at\_activate](https://github.com/atsign-foundation/at\_libraries/tree/trunk/packages/at\_onboarding\_cli#activate\_cli) to activate an owned atSign or [at\_onboarding\_cli/at\_register](https://github.com/atsign-foundation/at\_libraries/tree/trunk/packages/at\_onboarding\_cli#register\_cli) to generate a new free atSign.

### Paid atSigns

You can purchase custom atSigns from [the registrar site](https://my.atsign.com/go).&#x20;

| Cost  | Examples                                                                              | Description                                                                                                                                               |
| ----- | ------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| $10   | `jeremy_0`                                                                            | A hybrid atSign that contains an underscore and up to four numbers                                                                                        |
| $100  | <p><code>atsignexample</code><br><code>atest</code><br><code>tes5</code></p>          | A custom atSign that is any combination of words, numbers, or even emojis (at least five characters, or four characters if it includes a number or emoji) |
| $1000 | <p><code>test</code><br><code>four</code><br><code>tes</code><br><code>dog</code></p> | A custom atSign that is only three or four characters (no numbers).                                                                                       |
| $5000 | <p><code>007</code><br><code>te5</code><br><code>r4n</code></p>                       | A custom atSign that is only three characters                                                                                                             |

