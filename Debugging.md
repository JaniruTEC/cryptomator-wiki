# WebDav Implementation

The plain WebDav implementation can be launched using InMemoryWebDavServer or NioWebDavServer which use either a in memory file system or delegate to a folder on the physical filesystem whoose path must be entered after startup.

## Request logging

The WebDav servers log by default all requests and response headers. To log request and response bodies the java system property -Dcryptomator.LoggingHttpFilter.methodsToLogDetailed can be used. For example passing
> -Dcryptomator.LoggingHttpFilter.methodsToLog=MOVE,PROPFIND,PROPPATCH
to the java process will log request/response bodies for MOVE, PROPFIND and PROPPATCH requests.