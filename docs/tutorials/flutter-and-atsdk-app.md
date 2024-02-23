---
description: Create a Flutter application initialized for use with the atSDK
---

# Flutter & atSDK app

#### **1. Create a new Flutter app**

First, generate a new Flutter app (replace `at_app` with the name of your application).

```sh
flutter create at_app
cd at_app
```

#### 2. Add dependencies

Then add the following dependencies to your project:

```sh
flutter pub add at_client_mobile at_onboarding_flutter flutter_dotenv path_provider
```

#### 3. Replace main.dart

Now copy the contents of `main.dart` from below into `lib/main.dart` into your project.

<details>

<summary>main.dart</summary>

```dart
import 'dart:async';

import 'package:flutter/material.dart';
import 'package:at_onboarding_flutter/at_onboarding_flutter.dart';
import 'package:flutter_dotenv/flutter_dotenv.dart';
import 'package:path_provider/path_provider.dart'
    show getApplicationSupportDirectory;

import 'home_screen.dart';

Future<void> main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await dotenv.load();
  runApp(const MyApp());
}

Future<AtClientPreference> loadAtClientPreference() async {
  var dir = await getApplicationSupportDirectory();

  return AtClientPreference()
    ..rootDomain = 'root.atsign.org'
    ..namespace = dotenv.env['NAMESPACE']
    ..hiveStoragePath = dir.path
    ..commitLogPath = dir.path
    ..isLocalStoreRequired = true;
  // * By default, this configuration is suitable for most applications
  // * In advanced cases you may need to modify [AtClientPreference]
  // * Read more here: https://pub.dev/documentation/at_client/latest/at_client/AtClientPreference-class.html
}

class MyApp extends StatefulWidget {
  const MyApp({Key? key}) : super(key: key);
  @override
  MyAppState createState() => MyAppState();
}

class MyAppState extends State<MyApp> {
  // * load the AtClientPreference in the background
  Future<AtClientPreference> futurePreference = loadAtClientPreference();

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      // * The onboarding screen (first screen)
      home: Scaffold(
        appBar: AppBar(
          title: const Text('MyApp'),
        ),
        body: Builder(
          builder: (context) => Center(
            child: ElevatedButton(
              onPressed: () async {
                AtOnboardingResult onboardingResult =
                    await AtOnboarding.onboard(
                  context: context,
                  config: AtOnboardingConfig(
                    atClientPreference: await futurePreference,
                    rootEnvironment: RootEnvironment.Production,
                    domain: 'root.atsign.org',
                  ),
                );
                if (mounted) {
                  switch (onboardingResult.status) {
                    case AtOnboardingResultStatus.success:
                      Navigator.push(
                        context,
                        MaterialPageRoute(builder: (_) => const HomeScreen()),
                      );
                      break;
                    case AtOnboardingResultStatus.error:
                      ScaffoldMessenger.of(context).showSnackBar(
                        const SnackBar(
                          backgroundColor: Colors.red,
                          content: Text('An error has occurred'),
                        ),
                      );
                      break;
                    case AtOnboardingResultStatus.cancel:
                      break;
                  }
                }
              },
              child: const Text('Onboard an @sign'),
            ),
          ),
        ),
      ),
    );
  }
}

```

</details>

#### 4. Add home\_screen.dart

Create a second file in `lib/` called `home_screen.dart`. Copy the contents of `home_screen.dart` from below into your project.

<details>

<summary>home_screen.dart</summary>

```dart
import 'package:at_client_mobile/at_client_mobile.dart';
import 'package:flutter/material.dart';

// * Once the onboarding process is completed you will be taken to this screen
class HomeScreen extends StatelessWidget {
  const HomeScreen({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    // * Getting the AtClientManager instance to use below
    AtClientManager atClientManager = AtClientManager.getInstance();
    // * Getting the AtClient instance to use below
    AtClient atClient = atClientManager.atClient;

    // * From this widget onwards, you are fully onboarded!
    // * You can use the AtClient instance to perform operations as the onboared atSign
    return Scaffold(
      appBar: AppBar(
        title: const Text('What\'s my current @sign?'),
      ),
      body: Center(
        child: Column(children: [
          const Text('Successfully onboarded and navigated to FirstAppScreen'),

          // * Use the AtClient to get the current @sign
          Text('Current @sign: ${atClient.getCurrentAtSign()}')
        ]),
      ),
    );
  }
}

```

</details>

#### 5. Setup the .env file

**5.a. gitignore the .env file**

Add the following line to the top of `.gitignore`:

```
.env
```

This will prevent accidentally uploading the secret values stored in `.env` to any git repositories associated with your app.

**5.b. Add and populate the .env file**

Create a new file in the root of the project (next to `pubspec.yaml`) called `.env`. Add the following lines to it:

```sh
NAMESPACE=
API_KEY=
```

These values should be populated with your unique app namespace, and registrar API key.

**5.c. Register the .env file in pubspec.yaml**

In `pubspec.yaml` there should be a `flutter:` key, under this key, we want to create and add `.env` the `assets:` list:

```yaml
...
flutter:
  ...
  assets:
    - .env
  ...
...
```

#### 6. Start developing!

Start your application with the following command:

```sh
flutter run
```

Now you are ready to begin developing!

### Additional Notes

#### Onboarding

To authenticate an atSign, we will use `at_onboarding_flutter`. You can register an atSign [through the registrar](https://my.atsign.com/go) or through the widget in the app.

```dart
AtOnboardingResult onboardingResult = await AtOnboarding.onboard(
  context: context,
  config: AtOnboardingConfig(
    atClientPreference: futurePreference,
    rootEnvironment: RootEnvironment.Production,
    appAPIKey: dotenv.env['API_KEY'],
    domain: 'root.atsign.org',
  ),
);
```

#### Other atPlatform Packages

View other packages from Atsign [here](https://pub.dev/publishers/atsign.org/packages)
