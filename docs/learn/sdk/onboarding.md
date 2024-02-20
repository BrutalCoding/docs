---
description: Authenticate the atClient with the atServer
---

# Onboarding

## Overview

Onboarding is the process of authenticating to the atServer using it's associated atSign. Instead of the traditional username and password, this process uses the atSign's secret cryptographic keys to perform authentication.

## Setup Process

Depending on the SDK you are using, the process for onboarding varies.

{% tabs %}
{% tab title="Dart" %}
### Dart

In Dart we provide the[ at\_onboarding\_cli](https://pub.dev/packages/at\_onboarding\_cli) package which handles onboarding to the atServer via files stored in the \~/.atsign/keys directory

#### Manual Configuration

**Installation**

First add the package to your project

```dart
dart pub add at_onboarding_cli
```

Or add the package to your `pubspec.yaml` manually:

```yaml
dependencies:
  at_onboarding_cli: ^1.3.0
```

#### Usage

Set up the [preferences](https://pub.dev/documentation/at\_onboarding\_cli/latest/at\_onboarding\_cli/AtOnboardingPreference-class.html) to onboard to the atServer.&#x20;

```dart
 AtOnboardingPreference atOnboardingConfig = AtOnboardingPreference()
    ..hiveStoragePath = '$homeDirectory/.$nameSpace/$fromAtsign/storage'
    ..namespace = nameSpace
    ..downloadPath = '$homeDirectory/.$nameSpace/files'
    ..isLocalStoreRequired = true
    ..commitLogPath = '$homeDirectory/.$nameSpace/$fromAtsign/storage/commitLog'
    ..rootDomain = rootDomain
    ..fetchOfflineNotifications = true
    ..atKeysFilePath = atsignFile
    ..atProtocolEmitted = Version(2, 0, 0);
```

Next get the onBoardingService&#x20;

```dart
  AtOnboardingService onboardingService = AtOnboardingServiceImpl(
      fromAtsign, atOnboardingConfig,
      atServiceFactory: atServiceFactory);
```

Finally wait to be onboarded, this returns true once complete.&#x20;

```dart
await onboardingService.authenticate();
```

This can be wrapped to check that the onboard was successful with the code snippet below.

```dart

bool onboarded = false;
  Duration retryDuration = Duration(seconds: 3);
  while (!onboarded) {
    try {
      stdout.write('\r\x1b[KConnecting ... ');
      await Future.delayed(Duration(
          milliseconds:
          1000)); // Pause just long enough for the retry to be visible
      onboarded = await onboardingService.authenticate();
    } catch (exception) {
      stdout.write(
          '$exception. Will retry in ${retryDuration.inSeconds} seconds');
    }
    if (!onboarded) {
      await Future.delayed(retryDuration);
    }
  }
  stdout.writeln('Connected');
```
{% endtab %}

{% tab title="Flutter" %}
### Flutter

In Flutter, we provide the [at\_onboarding\_flutter](https://pub.dev/packages/at\_onboarding\_flutter) package which handles secure management of these secret keys.

{% hint style="info" %}
If you are developing a new Flutter app, we recommend that you use [at\_app](https://pub.dev/packages/at\_app) to generate an app skeleton with the at\_onboarding\_flutter package preconfigured.
{% endhint %}

#### Manual Configuration

**Installation**

First add the package to your project:

```
flutter pub add at_onboarding_flutter
```

Or add the package to your `pubspec.yaml` manually:

{% code title="pubspec.yaml" %}
```yaml
dependencies:
  flutter:
    sdk: flutter
  at_client_mobile: ^3.2.9
  at_onboarding_flutter: ^6.0.3
```
{% endcode %}

**Usage**

Simply call the [`onboard`](https://pub.dev/documentation/at\_onboarding\_flutter/latest/at\_onboarding/AtOnboarding/onboard.html) method whenever you want your app to open the onboarding widget.

```dart
AtOnboarding.onboard(
  context: context, // BuildContext
  config: AtOnboardingConfig(
    atClientPreference: AtClientPreference()
      ..rootDomain = AtEnv.rootDomain // access AtEnv from the `at_app_flutter` package
      ..namespace = AtEnv.appNamespace
      ..hiveStoragePath = dir.path
      ..commitLogPath = dir.path
      ..isLocalStoreRequired = true,
    rootEnvironment: AtEnv.rootEnvironment,
    domain: AtEnv.rootDomain,
    appAPIKey: AtEnv.appApiKey,
  ),
);
```

{% hint style="info" %}
`dir` is a variable from holding data retrieved from the [path\_provider](https://pub.dev/packages/path\_provider) package: `var dir = await getApplicationSupportDirectory();`
{% endhint %}

{% hint style="info" %}
`AtEnv` comes from [at\_app\_flutter](https://pub.dev/packages/at\_app\_flutter) which also comes in the preconfigured app skeleton from [at\_app](https://pub.dev/packages/at\_app).
{% endhint %}

**API Docs**

You can find the API reference for the entire package available on [pub](https://pub.dev/documentation/at\_onboarding\_flutter/latest/).

The `AtOnboarding` class API reference is available [here](https://pub.dev/documentation/at\_onboarding\_flutter/latest/at\_onboarding/AtOnboarding-class.html).


{% endtab %}
{% endtabs %}





