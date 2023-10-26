Since version 1.11.0, Cryptomator uses a fixed JDK version for production, which is checked periodically for updates and updated manually.

The currently used JDK can be found in the release build artifacts workflow files (e.g., mac-dmg.yml, win-exe.yml, etc). Since Cryptomator is additionally build in external repositories (e.g. flatpak), those need to be updated as well. Hence, the places to update are:
* coffeelibs JDK (https://github.com/coffeelibs/ppa-openjdk)
* Release artifacts workflow files (https://github.com/cryptomator/cryptomator/tree/develop/.github/workflows)
* Debian build script (https://github.com/cryptomator/cryptomator/tree/develop/dist/linux/debian)
* flathub (https://github.com/flathub/org.cryptomator.Cryptomator)
* AUR (https://aur.archlinux.org/packages/cryptomator)