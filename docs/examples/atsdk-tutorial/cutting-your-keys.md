---
description: It takes two to tango!
---

# Cutting your atSigns keys

To run through the tutorial you will need at least two atSigns, so you can send and receive. You can get your atSigns for free at [atsign.com](https://atsign.com/) or if you like purchase some that are more personal to you.&#x20;

Once you have you atsigns you are ready to activate them, which means spinning up your atServer per atSign and cutting your cryptographic keys for each atSign. Sounds complicated but it is easy ! In fact just a single command. In the terminal window type:

```
dart run .\bin\at_activate.dart 
```

You will get an error message telling you to add the `-a` flag and your atsign, so if you atSign was @crunchfrog you would type:

```
dart run .\bin\at_activate.dart -a "@crunchyfrog"
```

\*Note on windows the atSign needs to be in double quotes so the shell does not get confused with the @ symbol. Below you can see the activation process for two atSigns @energetic22 and @7capricon. Once the command is run you will get and email with the one time password, enter that and the program will create an atKeys file for that atSign. Any atKeys files you create will be located in your home directory then .atsign/keys.

These keys are important to be kept safe, as they are the only keys to your atSign and your data. Talking of data lets send some between the two atSigns next.

<figure><img src="../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>
