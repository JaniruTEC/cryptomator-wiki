# Command Line Options
Cryptomator supports the following command line options:
* `-Dcryptomator.settingsPath` to set the path to the folder containing the settings file
* `-Dcryptomator.logPath` to set the path of the file to which Cryptomator should write its log
* `-Duser.language=en` to set the interface language to `en` for English, `de` German, `fr` French and so forth.

# Windows options
All of the above command line options can also be added to a Cryptomator installation on Windows. Configuration is done in a text file located under `C:\Program Files\Cryptomator\app\Cryptomator.cfg` or wherever you installed Cryptomator.

E.g. to switch the UI language to Hungarian add the command line option from above to the `[JVMOptions]` section:

```
[JVMOptions]
-Dcryptomator.logPath=%appdata%/Cryptomator/cryptomator.log
-Duser.language=hu
```