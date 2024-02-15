---
description: A unique identifier which serves as the address of the atServer
---

# atSign

## What is an atSign?

An atSign (e.g. @alice) is simply a resolvable address (kind of like an email address) for an atServer. Anything can have an atSign, a person, organization, or thing (IoT), even individual songs or videos could have atSign addresses.

### What's it used for?

An atSign is used to protect and securely exchange information with other atSigns without any chance of surveillance, impersonation, or theft of the information by anyone.

### What characters can be used in an atSign?

An atSign supports any combination of Unicode UTF-8 characters that are translated to UTF-7 and must have less than characters 55 characters in length. This provides an enormous name space of 10^224 atSigns.

### How do I get an atSign?

Head to [the registrar site](https://my.atsign.com/go). It is recommended that you login with your email. One email can hold up to 10 free atSigns and unlimited paid atSigns.

### How do I generate my associated cryptographic keys?

There are multiple ways to generate the associated `.atKeys` file for an atSign. Within applications the .atKeys are stored in encrypted keychains that the OS provides.  Using the command line .atKeys files are produced and put in the directory `~/.atsign/keys`.&#x20;

Most applications have a way to export the .atkeys to a file if you need to keep them safe or use them on another device.

* [Using atmospherePro](https://www.youtube.com/watch?v=8xJnbsuF4C8) (3 minute video)
* Dart [at\_onboarding\_cli/at\_activate](https://github.com/atsign-foundation/at\_libraries/tree/trunk/packages/at\_onboarding\_cli#activate\_cli) to activate an owned atSign or [at\_onboarding\_cli/at\_register](https://github.com/atsign-foundation/at\_libraries/tree/trunk/packages/at\_onboarding\_cli#register\_cli) to generate a new free atSign.
* [Java Registration CLI](https://github.com/atsign-foundation/at\_java/blob/trunk/getting\_started\_guide.md)

### Paid atSigns

You can purchase custom atSigns from [the registrar site](https://my.atsign.com/go).

<table><thead><tr><th width="106.33333333333331">Cost</th><th width="195">Examples</th><th width="447">Description</th></tr></thead><tbody><tr><td>$10</td><td><code>jeremy_0</code></td><td>A hybrid atSign that contains an underscore and up to four numbers</td></tr><tr><td>$100</td><td><code>atsignexample</code><br><code>atest</code><br><code>tes5</code></td><td>A custom atSign that is any combination of words, numbers, or even emojis (at least five characters, or four characters if it includes a number or emoji)</td></tr><tr><td>$1000</td><td><code>test</code><br><code>four</code><br><code>tes</code><br><code>dog</code></td><td>A custom atSign that is only three or four characters (no numbers).</td></tr><tr><td>$5000</td><td><code>007</code><br><code>te5</code><br><code>r4n</code></td><td>A custom atSign that is only three characters</td></tr></tbody></table>
