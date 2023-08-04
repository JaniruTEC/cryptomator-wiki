# Command Line Options
Cryptomator supports the following command line options:

|Argument Name                                                | Description                                                                                                                                   |OS        |
|-------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------|----------|
|--version                                                    | Prints the Cryptomator version and exits (Alias: `-v`)                                                                                        |Linux, Mac|
|-Djava.net.useSystemProxies=[Boolean]                        | Whether Cryptomator should use the system proxy settings (true) or no proxy (false) when connecting to the internet (e.g. for update checks). |All       |
|-Dcryptomator.logDir=[DirPath]                               | The directory where Cryptomator stores it’s log files (e.g. application log, migration log).                                                  |All       |
|-Dcryptomator.pluginDir=[DirPath]                            | The directory where Cryptomator discovers plugins.                                                                                            |All       |
|-Dcryptomator.settingsPath=[FilePath]                        | The json-file to use for application settings.                                                                                                |All       |
|-Dcryptomator.p12Path=[FilePath]                             | The path to your device key.                                                                                                                  |All       |
|-Dcryptomator.ipcSocketPath=[FilePath]                       | The path to the IPC socket used for checking for an already running application instance.                                                     |All       |
|-Dcryptomator.mountPointsDir=[DirPath]                       | The directory where Cryptomator mounts vaults if no per-vault location has been set.                                                          |All       |
|-Dcryptomator.showTrayIcon=[Boolean]                         | Whether Cryptomator should show an icon in the system tray (true) or not (false).                                                             |All       |
|-Dcryptomator.integrationsWin.autoStartShellLinkName=[String]| The name of the link created for starting Cryptomator at system startup.                                                                      |Win       |
|-Dcryptomator.integrationsWin.keychainPaths=[FilePathList]   | The paths to load keychains from.                                                                                                             |Win       |
|-Dcryptomator.integrationsMac.keychainServiceName=[String]   | The name of the keychain service.                                                                                                             |Mac       |
|-Dcryptomator.loopbackAlias=[String]                         | The name of the WebDAV loopback alias.                                                                                                        |Win       |
|-Duser.language=[Language]                                   | The language to use for the application interface.                                                                                            |All       |
|-Duser.region=[Region]                                       | The optional region/dialect to use for the application interface. Requires `-Duser.language=[Language]` to be set.                            |All       |

The command line options come with the following types:

|Argument Type                                                |Valid values                                                                                                                                 |Example   |Notes                                                                                                                      |
|-------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------|----------|---------------------------------------------------------------------------------------------------------------------------|
|Boolean                                                      |"true", "false"                                                                                                                              |-Dcryptomator.showTrayIcon=true|Boolean values are not quoted.                                                                                             |
|String                                                       |Quoted text                                                                                                                                  |-Dcryptomator.loopbackAlias="Cryptomator"|Accepted characters/values are not defined by this document.                                                               |
|DirPath                                                      |Quoted full path to a folder in the style of your OS, but always using "/" as separator                                                      |-Dcryptomator.logDir="/Users/Admin/Logs"|Properties containing "cryptomator" might use substitutions.                                                               |
|FilePath                                                     |Quoted full path to a file in the style of your OS, but always using "/" as separator                                                        |-Dcryptomator.settingsPath="C:/settings.json"|Properties containing "cryptomator" might use substitutions.                                                               |
|FilePathList                                                 |List of `FilePaths` divided by ":" (Linux, macOS) or ";" (Windows).                                                                          |-Dcryptomator.integrationsWin.keychainPaths="C:\file.one;C:\file.two"|The entire list is quoted instead of individual entries. Properties containing "cryptomator" might use substitutions.      |
|Language                                                     |Unquoted ISO 639 alpha-2 or alpha-3 language code                                                                                            |-Duser.language=de|See paragraph "language" [here](https://docs.oracle.com/en/java/javase/20/docs/api/java.base/java/util/Locale.html)        |
|Region                                                       |Unquoted ISO 3166 alpha-2 country code                                                                                                       |-Duser.region=CH|See paragraph "country (region)" [here](https://docs.oracle.com/en/java/javase/20/docs/api/java.base/java/util/Locale.html)|

# Windows options
All of the above command line options can also be added to a Cryptomator installation on Windows. Configuration is done in a text file located under `C:\Program Files\Cryptomator\app\Cryptomator.cfg` or wherever you installed Cryptomator.

E.g. to switch the UI language to Hungarian add the command line option from above to the `[JavaOptions]` section:

```
[JavaOptions]
java-options=-Dcryptomator.logPath=%appdata%/Cryptomator/cryptomator.log
java-options=-Duser.language=hu
```