# Command Line Options

Cryptomator supports the following command line options:

| Option Name | Description                               | Alias(es) | OS         |
|-------------|-------------------------------------------|-----------|------------|
| --version   | Prints the Cryptomator version and exits. | -v        | Linux, Mac |

# Properties

Cryptomator allows configuring parts of the environment using *properties.* For information on using properties, see [
*Setting Properties.*](#setting-properties)
The following properties are available for use:

| Argument Name                                               | Description                                                                                                                                   | OS    |
|-------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------|-------|
| java.net.useSystemProxies=[Boolean]                         | Whether Cryptomator should use the system proxy settings (true) or no proxy (false) when connecting to the internet (e.g. for update checks). | All   |
| cryptomator.logDir=[DirPath]                                | The directory where Cryptomator stores it’s log files (e.g. application log, migration log).                                                  | All   |
| cryptomator.pluginDir=[DirPath]                             | The directory where Cryptomator discovers plugins.                                                                                            | All   |
| cryptomator.settingsPath=[FilePath]                         | The json-file to use for application settings.                                                                                                | All   |
| cryptomator.p12Path=[FilePath]                              | The path to your device key.                                                                                                                  | All   |
| cryptomator.ipcSocketPath=[FilePath]                        | The path to the IPC socket used for checking for an already running application instance.                                                     | All   |
| cryptomator.mountPointsDir=[DirPath]                        | The directory where Cryptomator mounts vaults if no per-vault location has been set.                                                          | All   |
| cryptomator.showTrayIcon=[Boolean]                          | Whether Cryptomator should show an icon in the system tray (true) or not (false).                                                             | All   |
| cryptomator.integrationsWin.autoStartShellLinkName=[String] | The name of the link created for starting Cryptomator at system startup.                                                                      | Win   |
| cryptomator.integrationsWin.keychainPaths=[FilePathList]    | The paths to load keychains from.                                                                                                             | Win   |
| cryptomator.integrationsMac.keychainServiceName=[String]    | The name of the keychain service.                                                                                                             | Mac   |
| cryptomator.integrationsLinux.trayIconsDir=[DirPath]        | The directory where Cryptomator looks for icons to use for the system tray.                                                                   | Linux |
| cryptomator.loopbackAlias=[String]                          | The name of the WebDAV loopback alias.                                                                                                        | Win   |
| user.language=[Language]                                    | The language to use for the application interface.                                                                                            | All   |
| user.region=[Region]                                        | The optional region/dialect to use for the application interface. Requires `user.language=[Language]` to be set.                              | All   |

## Property Argument Types

Cryptomator's properties come with the following types:

| Argument Type | Valid values                                                                            | Example                                                             | Notes                                                                                                                        |
|---------------|-----------------------------------------------------------------------------------------|---------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| Boolean       | "true", "false"                                                                         | cryptomator.showTrayIcon=true                                       | Boolean values are not quoted.                                                                                               |
| String        | Quoted text                                                                             | cryptomator.loopbackAlias="Cryptomator"                             | Accepted characters/values are not defined by this document.                                                                 |
| DirPath       | Quoted full path to a folder in the style of your OS, but always using "/" as separator | cryptomator.logDir="/Users/Admin/Logs"                              | Might use [substitutions.](#substitutions)                                                                                   |
| FilePath      | Quoted full path to a file in the style of your OS, but always using "/" as separator   | cryptomator.settingsPath="C:/settings.json"                         | Might use [substitutions.](#substitutions)                                                                                   |
| FilePathList  | List of `FilePaths` divided by ":" (Linux, macOS) or ";" (Windows).                     | cryptomator.integrationsWin.keychainPaths="C:\file.one;C:\file.two" | The entire list is quoted instead of individual entries. Might use [substitutions.](#substitutions)                          |
| Language      | Unquoted ISO 639 alpha-2 or alpha-3 language code                                       | user.language=de                                                    | See paragraph "language" [here.](https://docs.oracle.com/en/java/javase/20/docs/api/java.base/java/util/Locale.html)         |
| Region        | Unquoted ISO 3166 alpha-2 country code                                                  | user.region=CH                                                      | See paragraph "country (region)" [here.](https://docs.oracle.com/en/java/javase/20/docs/api/java.base/java/util/Locale.html) |

## Substitutions

Substitutions are used to dynamically resolve the content of some properties depending on the environment Cryptomator is
started in, e.g. by inserting the path to the user's home folder. They may **only** be used in properties that start
with `cryptomator.` (mind the dot) like `cryptomator.logDir`.
All occurrences of the following substitution keys – in supported properties – are replaced by their respective variable
values:

| Substitution key  | Variable value                          |
|-------------------|-----------------------------------------|
| `@{appdir}`       | The application installation directory. |
| `@{appdata}`      | `%APPDATA%` (Windows only).             |
| `@{localappdata}` | `%LOCALAPPDATA%` (Windows only).        |
| `@{userhome}`     | The user's home directory.              |

Unknown substitution keys remain unchanged; a key without a value is replaced with an empty string.

## Setting Properties

All of the above properties can only be set in the advanced configuration file `Cryptomator.cfg`; they are *not*
available on the command line.
Each user can have
[their own advanced configuration file ("per-user advanced configuration"),](#locating-the-per-user-advanced-configuration)
which takes precedence over
[the advanced configuration of the system ("system-wide advanced configuration")](#locating-the-system-wide-advanced-configuration)
for that user.

> [!WARNING]
> Editing the advanced configuration is not officially supported.
> - Changes to the _system-wide advanced configuration_ may be overwritten by updates.
> - A user's _per-user advanced configuration_ may quietly become outdated after an update.
> - Properties may be changed or removed without warning.
> - Changes to the advanced configuration may break your installation or yield unexpected behavior.

> [!NOTE]
> A user's _per-user advanced configuration_ and the _system-wide advanced configuration_ are **not** merged.
> - The _per-user advanced configuration_ needs to contain all common properties _as well as_ differing ones.
> - Changes to the _system-wide advanced configuration_ will not have any effect if a _per-user advanced configuration_
    exists for that user.
> 
> If it exists, the usage of a user's _per-user advanced configuration_ can not currently be disabled.
> Please see [this issue](https://github.com/cryptomator/cryptomator/issues/3119) for more information.

For a more technical explanation of the structure and location of the advanced configuration,
please see the [upstream specification.](https://bugs.openjdk.org/browse/JDK-8287060)

### Locating the _system-wide advanced configuration_

> [!NOTE]
> Editing the _system-wide advanced configuration_ may require elevated privileges (i.e. admin or root
> permissions).

The following table lays out instructions to access the _system-wide advanced configuration_ for your Operating System.
The location may differ depending on Cryptomator's installation location:

| OS      | Default path                                                 | Notes                                                                                                    |
|---------|--------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|
| Windows | `C:\Program Files\Cryptomator\app\Cryptomator.cfg`           |                                                                                                          |
| macOS   | `/Applications/Cryptomator.app/Contents/app/Cryptomator.cfg` | Might be located in the "User Application Folder": `~/Applications/...`                                  |
| Linux   | `/opt/cryptomator/lib/app/cryptomator.cfg`                   | Alternatively use the command: `open $(dirname $(dirname $(readlink -f $(which cryptomator))))/lib/app/` |

### Locating the _per-user advanced configuration_

The following table lays out instructions to access the _per-user advanced configuration_ for your Operating System.  
You may need to create the file or its containing folder. If at least one _per-user advanced configuration_ exists, it
takes precedence over the _system-wide advanced configuration_ for that user:

| OS      | Path                                                                                          | Notes                                                      |
|---------|-----------------------------------------------------------------------------------------------|------------------------------------------------------------|
| Windows | `%LocalAppData%\Cryptomator\Cryptomator.cfg` (\*)<br/>`%AppData%\Cryptomator\Cryptomator.cfg` | If both exist, the path marked with (\*) takes precedence. |
| macOS   | `~/Library/Application Support/Cryptomator/Cryptomator.cfg`                                   |                                                            |
| Linux   | `~/.local/cryptomator/Cryptomator.cfg` (\*)<br/>`~/.cryptomator/Cryptomator.cfg`              | If both exist, the path marked with (\*) takes precedence. |

### Editing the advanced configuration

To replace a property, change the value after the equals sign in the corresponding entry in the `[JavaOptions]` section.

**Example:** To disable the tray icon change the line as follows

```diff
- java-options=-Dcryptomator.showTrayIcon=true
+ java-options=-Dcryptomator.showTrayIcon=false
```  

To add a property, add a line in the `[JavaOptions]` section of the form `java-options=-D[Name]=[Value]` (mind the "
-D").

**Example:** To switch the UI language to Hungarian, add the property `user.language` with the value `hu`:

```
[JavaOptions]
# ... Other options ...
java-options=-Duser.language=hu
```