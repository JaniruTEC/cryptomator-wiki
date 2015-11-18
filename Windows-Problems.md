# Known issues on Windows

## Slow virtual drives
As Cryptomator drives are WebDAV mounts, Windows talks to a WebDAV server on localhost. For some reason Windows tries to find a proxy even for localhost. This is not only a security issue (as anyone in the network can claim to be a proxy), but also slows down read/write request.

Microsoft provides [instructions on how to disable Web Proxy Autodiscovery](https://support.microsoft.com/en-us/kb/2445570).

## Cache not deleted on Win 7 and Win Server 2008 R2
Windows keeps a local copy of WebDAV files, usually inside `C:\Windows\ServiceProfiles\LocalService\AppData\Local\Temp\TfsStore\`. Normally this cache gets evicted, when the user is done working with the files. This is not the case on Windows 7 and Windows Server 2008 R2.

Microsoft provides a [hotfix for this issue](https://support.microsoft.com/en-us/kb/2790804), as this is also a security problem.

## Drive always shows capacity of system drive (C:)
Nothing we can influence. This is just the way, MS wants it to be.

> "Research on WebDAV protocol RFCs and verification from Microsoft's product team confirmed WebDAV protocol doesn’t support querying server’s disk capacity" - [Microsoft](https://support.microsoft.com/en-us/kb/2386902)

Apparently they haven't heard of RFC 4331 and thus show the capacity of the system drive.