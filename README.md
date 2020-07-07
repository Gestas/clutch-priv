# Clutch
## A Modern Interface to Transmission

Clutch is a modern interface to the [Transmission Bitorrent daemon](https://transmissionbt.com/). It fully 
implements the [Transmission API](https://github.com/transmission/transmission/blob/master/extras/rpc-spec.txt).

Clutch is distributed as - 
  - A native app for
    - [Linux]()
    - [MacOS]() 
    - [Windows]()
  - As an app in the
    - [Apple iOS App Store]()
    - [Google Play Marketplace]()
        - The Android app is available for sideloading [from here](). Most users should use the [Google Play 
        Marketplace]().
  - as a [webapp]()
    - as a webapp packaged in a [Docker container]()

  ### Why?
  I like the Transmission daemon; it's fast, scales well, and is efficient.
  I don't like any of the native interfaces, especially the web client. 
  It hides a significant amount of functionality behind a right-click which cripples it on mobile devices. 
  
  I also wanted to get some experience building and distributing a cross-platform app. 
  
  ##### Code quality