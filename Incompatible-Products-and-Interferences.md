| OS | Product | Effect | Workaround |
| --- | --- | --- | --- |
| All | ODrive | After sync foldernames end with `(Conflict ...)`. Navigating into folders recursively shows the root folder. | Configure oDrive to sync all files instead of creating placeholder files (**BE AWARE** that the free version does not allow to switch back to placeholder files). |
| Win | Zone Alarm | Unlock fails. Log file shows `System error 67 has occurred`. | Reinstall Cryptomator 1.2.3 or newer |
| Mac | ESET Cyber Security | Unlock fails after timeout and vault doesn't show up in Finder, but log file shows access to files. | Disable real time protection for WebDAV mounts from localhost on Cryptomator's port |
| Mac | XythosDrive | "URLs with the type "http:" are not supported" | Unknown (see [issue 368](/cryptomator/cryptomator/issues/368#issuecomment-264699203)) |
| Linux | mesa‑aco‑git 19.2.0 | Excessive RAM usage | Downgrade mesa (see [issue 953](/cryptomator/cryptomator/issues/953#issuecomment-521999228)) |