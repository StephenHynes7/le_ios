

Logentries logging for iOS
==========================


Main features
-------------

* online/offline logging
* dictionary serialization
* secure TLS connection
* thread safety
* application lifecycle logging
* application crash logging with stack traces

Installation
------------

Just add files from lelib group into your project.

Simple example
--------------

```objectivec
#import "lelib.h"

LELog* log = [LELog sharedInstance];
log.token = @"f66815d1-702c-414b-8dcc-bb73de372584";

[log log:@"Hello World"];
```

Early initialization
--------------------

The library automatically hooks up to the exception handler and logs unhandled
exceptions. This means that you should initialize the library as soon as
possible to log all exceptions. Insert following lines to main.m to log
exceptions even before application:didFinishLaunchingWithOptions: is invoked.

```objectivec

#import "lecore.h"

int main(int argc, char * argv[])
{
  @autoreleasepool {

    le_init();
    le_set_token("aaabacad-aeaf-4321-1234-abcdef012345");

    return UIApplicationMain(argc, argv, nil, NSStringFromClass([AppDelegate class]));
  }
}

The token is stored in global variable. You don't have to setup token property
of LELog instance later.

```

Quick questions
---------------

**Any dependencies?** No dependencies. The library uses standard Obj-C and POSIX C.

**How to log an event?** Simply call `[log log:@"Hello world"];`

**No network coverage?** Log entries are stored in a file and sent to Logentries when the network is back.

**When app crashes?** If configured, the library logs information about the application crash with stack trace.

**When app is forced to shut down by OS?** There is no way to log it.

