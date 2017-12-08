# Choosing Between Progressive Web Apps, React Native, and NativeScript in 2018

If you are a JavaScript developer looking to build a mobile app in 2018, you have never had more options. You can build for the web with a Progressive Web App, build a hybrid app using Cordova, build native iOS and Android apps using frameworks like [React Native](https://facebook.github.io/react-native/) or [NativeScript](https://www.nativescript.org/), or choose some combination of all of these things.

Here at Progress, we’ve been getting a lot of demand for a comparison between Progressive Web Apps and JavaScript-driven native frameworks like React Native and Progress’s own NativeScript, so that will be the focus of this article.

We’ll start by discussing Progressive Web Apps and the JavaScript-driven native approach in detail, and move on to give some clear guidelines on when each approach makes sense. Let’s start the conversation by looking at Progressive Web Apps.

## Progressive Web Apps

[Progressive Web Apps](https://developers.google.com/web/progressive-web-apps/) (PWAs) are a series of new APIs that add a number of new features to web applications. The PWA initiative has received a lot of attention in the JavaScript community in the last year, as Google, Microsoft, and Mozilla have all been pushing the technology heavily through their respective channels. It’s hard to attend a JavaScript conference without accidentally attending at least a few talks on PWAs.

Why all the hype? The PWA APIs open the door to a lot of really useful functionality for web apps, including the following.

* **Home screen placement**—PWAs can appear on the user’s home screen, just like native mobile applications do.
* **Offline**—PWAs work offline by default, and can employ advanced caching strategies.
* **Push notifications**—PWAs give web apps the opportunity to send push notifications, even when the web app is not being actively viewed.

This functionality has the ability to add a lot of value to a traditional web application. The site [pwastats.com](https://www.pwastats.com/) includes an impressive list of case studies from companies that have switched to Progressive Web Apps. As the stats show, many of these companies have not only improved performance metrics like load time, but also business-centric metrics like conversation and customer acquisition rates.

![](twitter-lite.png)
_Twitter Lite case study from pwastats.com_

![](flipkart.png)
_Flipkart case study from pwastats.com_

The design of the Progressive Web App APIs is one of the biggest factors behind the technology’s success. Unlike a lot of web APIs, which require potentially complex polyfills or workarounds for browsers that don’t support the new API, the PWA APIs were designed with graceful degradation in mind.

In practice, that means your app can use the two primary technologies behind PWAs—service workers, and web application manifest files—and and browsers that don’t support those APIs just ignore the relevant files and code.

This design has been key to the success of PWAs, as iOS—aka the second biggest mobile platform out there—still does not support the service worker and web app manifest specifications. But because the PWA approach doesn’t degrade the experience on platforms that don’t support the necessary APIs, PWAs have been able to succeed where many similar technologies have failed. In fact, [many companies have even seen increased iOS conversion rates by rethinking their mobile experiences using a Progressive Web App](https://medium.com/dev-channel/why-progressive-web-apps-vs-native-is-the-wrong-question-to-ask-fb8555addcbb).

![](aliexpress.png)
_A [Google case study](https://developers.google.com/web/showcase/2016/aliexpress) showing how AliExpress improved their conversation rates with a PWA—even on iOS._

But despite being a well designed technology, PWAs are not the solution for all mobile needs. At the end of the day PWAs are web apps, and as such they are subject to the same limitations as any web app—such as having limited device API access, and having performance characteristics that are very reliant on the browser they’re running in.

Running on the web brings a ton of advantages as well, and we’ll discuss all of this in more detail when we compare PWAs with JavaScript-driven native approaches momentarily. For now let’s first take a look at how React Native and NativeScript work.

## JavaScript-driven native

Years ago, JavaScript developers that wanted to build for iOS and Android were forced to learn completely new languages and development approaches. The first technology to change this was Cordova, which allowed web developers to package their web apps into a native binary, and to access device APIs through plugins.

Since Cordova was first released, developers have created a variety of alternative approaches to use JavaScript to drive native iOS and Android applications. In this article we’re going to cover the latest of these approaches, which we call JavaScript-driven native.

What separates JS-driven native frameworks from Cordova-based approaches is that JS-driven native frameworks use native user interface components, and therefore abandon web concepts like HTML and the DOM. This approach was popularized in 2015 by Facebook’s release of React Native, and Progress’s NativeScript, which are the two most popular frameworks for building JavaScript-driven native apps today.

For JavaScript developers, using native user interface components to build your applications is a great and horrible thing. It’s great because using native iOS and Android UI components means your applications automatically fit into the platform you’re building for. You don’t have to worry about styling your app to make your buttons look like an `UIButton` or an `android.widget.Button`, because you’re using those elements already.

Using native user interface components also means you can leverage some really powerful native constructs that aren’t present on the web. For example, suppose you want to build an endless scrolling list with thousand of items. On the web you have to concern yourself with frameworks and concepts like a virtual DOM; in native land this functionality is a built-in feature of `UITable` and (what’s the name of the Android API again).

-- gif of endless lists --

The downside of using native user interface components is that JavaScript developers have a new set of components to learn. For instance, to build the list example in the previous gif you would have to learn how a `<ListView>` works in NativeScript or a `<FlatList>` in React Native.

JavaScript-driven native apps are native apps, and so they also suffer many of the same difficulties inherent to native iOS and Android development. To discuss some of these limitations in detail, let’s shift our discussion to comparing the approaches we’ve discussed thusfar.

## Which to choose

Now that we’ve introduced both approaches to app development, let’s look at some questions you can ask yourself about the app you’re developing to help you decide which approach to take.

* Do you need an API that is not available on the web?

There are situations


PWA

* Strengths
  * Easy deployment and updates
  * The broad reach of the web
  * Linkability
  * Graceful degradation
  * Great online resources, tons of conference talks, etc.
  * Small footprint (when compared to native apps)
* Weaknesses
  * Many features aren’t available on iOS (yet).
  * Can’t use all mobile APIs and features.
  * Can be hard to monetize (currently, web payment APIs are in the works)
  * Limited by the performance of the web

-- {N} + RN

* Intro & background
  * Big players are React Native and NativeScript
  * Large growth of both in npm in 2017.
  * Show big case studies, like SAP using {N}. Give React Native some shout outs.
  * Expanding to new frameworks, like {N} supporting Vue.

* Strengths
  * Familiar tech—JS, CSS, npm
  * Native-like performance and native user interfaces
  * Unlimited device API access
  * Ability to use iOS and Android SDKs
* Weaknesses
  * Need to learn new markup components to build UI
  * Painful iOS and Android deployment processes and update cycles
  * Large footprint (because they’re native apps)

## Web or native—why not both?

🌈 🦄

OMG YOU GET THE BEST OF BOTH WORLD AMIRITE!?

* Intro & background
  * Walk over common approaches to this today.
    * Ionic
    * {N}
    * React Native
  * This whole idea works because it’s all just JavaScript.
  * Twitter lite

* Strengths
  * Building for three platforms from one codebase.
* Weaknesses
  * Building for three platforms from one codebase.



Stats to show increased mobile demand?
  https://techcrunch.com/2017/12/05/consumer-spending-across-app-stores-worldwide-to-top-110-billion-in-2018/?utm_campaign=Fuse%2BWeekly&utm_medium=email&utm_source=Fuse_Weekly_106