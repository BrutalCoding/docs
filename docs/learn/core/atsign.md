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
