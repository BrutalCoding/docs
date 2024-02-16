# Get sample code

## Open Source on GitHub

The atPlaform and the atSDKs are all open souce and the code can be found on GitHub and downloaded from [Atsign Foundation](https://github.com/atsign-foundation). But we will start with some easy sample code to show how data can be shared and notifications can be sent between atSigns. These are the basic building blocks for powerful applications like [SSH No Ports](https://www.noports.com/) and graphical applications like [atmospherePro](https://atsign.com/apps/atmospherepro/), both of which are also opensource so you can see the code in action.

## Clone the demo repo

In VS Code you can click "Clone Git Repository" and enter the URL

```
https://github.com/atsign-foundation/at_demos.git
```

This will copy down all the sample code from GitHub to the directory you select. VS Code will ask you if you want to open the directory you just downloaded and say no. We will pick the one directory we need in the next step.

<figure><img src="../.gitbook/assets/VScode Git.png" alt=""><figcaption><p>Clone code from GitHub</p></figcaption></figure>

## Open at\_getting\_started

Click the Open Folder selection and go to the directory you selected and then at\_demos then finally select the at\_getting\_started directory, then click "select folder". You might get a pop up asking if you trust the authors and if you trust us say yes!

At this point you will have the demo code in the IDE and probably see a bunch of red files, meaning something is wrong with them.&#x20;

<figure><img src="../.gitbook/assets/dart pub get.png" alt=""><figcaption><p>dart pub get</p></figcaption></figure>

VS Code if you have the Dart plugin installed will ask if you want to run `pub get` you can safely say yes.

Next you can open a terminal session from the VS Code menu, and you will get a window with a prompt. At that prompt you can type the following two commands to pull down the required libraries.

```
dart pub get
```

```
dart pub update
```

Once you have run those commands in the terminal window all the red text will have gone and we are ready to run some code.

<figure><img src="../.gitbook/assets/dart update.png" alt=""><figcaption><p>Ready to run.</p></figcaption></figure>
