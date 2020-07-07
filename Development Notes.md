# Clutch Development Notes

## Clutch Goals - 
  - A modern GUI interface to the [Transmission Bitorrent daemon](https://transmissionbt.com/) 
  that fully implements the [API](https://github.com/transmission/transmission/blob/master/extras/rpc-spec.txt). 
  It should be mobile and desktop friendly and -
  - Allow *nix, MacOS, and Windows users to install as a local application.
    - For *nix distributed via several popular repos (Fedora, Ubuntu, more?).
  - Allow iOS and Android users to install from their respective app stores.
  - Allow any user to run Clutch privately as a web service and connect with and modern desktop or mobile browser. 

## Cross Platform Development - 
This is my first attempt at cross-platform development. 
The hope was I could archive these goals with *a single code base that doesn't require any "if platform == x then;" loops.*

Some terms - 
  - [Progressive Web Apps (PWA)](https://web.dev/what-are-pwas/)
    - tl; dr, Clutch can't be used as a PWA. 
    - It looks to me that a PWA is a website that can be made to look like a traditionally 
    installed application. This functionality is sometimes surfaced to 
    users as a "Add to Home Screen" pop-up in the browser.
    - PWA's require the use of TLS with trusted certificates for all 
    connections. This means users would need to setup the Transmission 
    daemon to support this. That's heavy lifting I don't want to ask users
    to do.
  - "Native APIs" - In this context a native API is a iOS or Android specific 
  API used to access some device features. Clutch requires access to the 
  local file-system so users can add `.torrent` files. Optionally it would be
  nice to support notifications for users that want them. Both of these use 
  native APIs. 

A quick look around at the "cross-platform" development space -

- [Electron](https://www.electronjs.org/)
  - Great option for desktop installs, no mobile options. 

- [NativeScript](https://nativescript.org)
  - Only supports PWAs on the desktop, Clutch can't work as a PWA. 

- [Xamarim](https://dotnet.microsoft.com/apps/xamarin)
  - Doesn't support *nix on the desktop. 
  - Looks like it would require lots of those dreaded `if platform == x then;` loops.

- [Flutter](https://flutter.dev/)
  - From the homepage - "...toolkit for building beautiful, natively compiled 
  applications for mobile, web, and desktop from a single code-base." 
  Sounds perfect!
  - Unfortunately, as of July 2020 (Flutter version 1.17.5) -
    - Web support is in [beta](https://flutter.dev/docs/get-started/web)
    - MacOS desktop support is [alpha](https://flutter.dev/desktop)
    - Windows desktop support is [pre-alpha](https://github.com/flutter/flutter/wiki/Desktop-shells)
    - Linux desktop support is [pre-alpha](https://github.com/flutter/flutter/wiki/Desktop-shells)
  - They have a big vision but it's too early.

- [React (i.e. Reactjs)](https://reactjs.org/) or [React Native](https://reactnative.dev/)?
  - Seems to me that these solve entirely different problems and shouldn't share a name. 
  - See https://www.quora.com/Whats-the-main-difference-between-ReactJS-and-React-Native
    - React - "...JavaScript library that makes highly dynamic and responsive 
    web pages.
    - React Native - "...a mobile development framework for building hybrid 
    iOS and Android apps."
  - There is [react-native-web](https://github.com/necolas/react-native-web) 
  but it appears to have limitations

- [Ionic](https://ionicframework.com/)
  - They have [a write-up](https://ionicframework.com/resources/articles/ionic-vs-react-native-a-comparison-guide) 
  that does an good job of explaining the space using 
  "Hybrid-Native vs. Hybrid-Web" language. Then I got confused again. 
  - What is [Ionic React](https://ionicframework.com/react)?
    - Reading Ionic's [release announcement](https://ionicframework.com/blog/announcing-ionic-react/) 
    I got the sense that Ionic React (as in Reactjs, not React Native) is an
    attempt to add "real" PWA support to Reactjs. But PWAs won't work for Clutch.
    - So does Ionic React do what react-native-web is trying to do?
  - [Ionic Capacitor](https://capacitorjs.com/) is an abstraction layer for Ionic to 
  mobile native APIs. 

## How we're doing it -
tl; dr, it's all in the packaging.
We can write a single code-base then package it differently based on the target platform. Taking this approach gives us some flexibility WRT language for the core code-base. I like the Ionic + Reactjs + Capacitor stack, it has wide community support and I'm not asking it to do anything it doesn't already do. 

- Packaging - 
  - iOS and Android are supported natively with this stack. 
  - For the desktop we can package Clutch using Electron. 
    - https://www.youtube.com/watch?v=Jrj2qMPWCZ0
  - For the web server it can be a direct download as well as a Docker container. 

