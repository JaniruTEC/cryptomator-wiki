## unable to paste passphrase from keepass

installing `xsel` supposedly fixes this. See issue [#226](https://github.com/cryptomator/cryptomator/issues/226).

## apt-get remove fails

when trying to uninstall Cryptomator using `apt-get remove cryptomator` I get an error:
```
xdg-mime: file '/opt/Cryptomator/cryptomator.org-Cryptomator-MimeInfo.xml' does not exist
...
E: Sub-process /usr/bin/dpkg returned an error code (1)
```

This is due to a bug in our uninstall script.

A Workaround is:
```
sudo cp /opt/Cryptomator/cryptomator-vault-metadata.xml /opt/Cryptomator/cryptomator.org-Cryptomator-MimeInfo.xml
sudo apt-get remove cryptomator
sudo rm /opt/Cryptomator/cryptomator.org-Cryptomator-MimeInfo.xml
```