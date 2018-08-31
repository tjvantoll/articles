# How to Build a PWA, an iOS App, and an Android App—From One Codebase

I have a long history of choosing between web and native, often wrongly. I’ve built web apps that were scraped for outsourced native apps, and I’ve wasted time building native apps that found no audience.

Choosing between web and native is hard, and in my experience, oftentimes you won’t know which platform better meets your needs until after the fact. The good news is JavaScript developers no longer have to choose.

In this article I’m going to show how to use the recently announced [NativeScript and Angular integration](https://blog.angular.io/apps-that-work-natively-on-the-web-and-mobile-9b26852495e7) to build a PWA, a native iOS app, and a native Android app from one codebase. You’ll learn the steps you’ll need to take, as well as some tips and tricks I learned from building an Angular app for all three platforms.

## Starting your app

Over the last month I built an app called ShinyDex and deployed it the App Store, Google Play, and the web. The app is a purposely simple checklist app designed to help teach how the NativeScript and Angular technology stack work.

![](apps.png)

