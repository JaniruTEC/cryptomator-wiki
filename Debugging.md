# WebDAV Implementation

The plain WebDAV implementation can be launched using `InMemoryWebDavServer` or `NioWebDavServer` which use either an in-memory file system or delegate to a folder on the physical filesystem whose path must be entered after startup.

## Request Logging

The WebDAV servers log all requests and response headers by default. To log request and response bodies the Java system property `-Dcryptomator.LoggingHttpFilter.methodsToLogDetailed` can be used. For example passing

```
-Dcryptomator.LoggingHttpFilter.methodsToLogDetailed=MOVE,PROPFIND,PROPPATCH
```

to the Java process will log request/response bodies for `MOVE`, `PROPFIND` and `PROPPATCH` requests.