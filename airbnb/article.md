# Would Airbnb Have Fared Better With NativeScript?

> **BACKGROUND**: Last week, Airbnb’s engineering team published a [5-part series on why they’re moving away from React Native](https://medium.com/airbnb-engineering/react-native-at-airbnb-f95aa460be1c). It’s well written, and worth reading through if you’re looking for some context for this article’s discussion. All quotes you see in this article are from the Airbnb writeup.

Airbnb’s announcement piqued our interest on the NativeScript team. NativeScript and React Native share a similar architecture, so oftentimes feedback about React Native applies equally to NativeScript, especially when it’s how companies structure their team to handle both web and mobile development.

But in this case a lot of Airbnb’s feedback was very technical, and delved into areas where React Native and NativeScript are quite different. Therefore as we read through the series we couldn’t help but wonder—would Airbnb have fared better with NativeScript?

![](logos.png)

Now, this is the NativeScript blog, so of course I’d love to tell you that NativeScript would have _totally_ worked way better. That NativeScript would’ve helped Airbnb built 300% faster apps that helped them acquire 500% more users.

But, the truth is... NativeScript would almost certainly have suffered the same fate as React Native at Airbnb. Per their own words, Airbnb is trying to build “world-class apps” with a team of “more than 100 mobile engineers”. And, building the _absolute best_ applications is not easy with any cross-platform tool. That rule applies with NativeScript; it applies with React Native; and it even applies with tools like Electron.

Nevertheless, we think the topic of NativeScript at Airbnb is an interesting way to compare the architectures of React Native and NativeScript—something we get a lot of requests to do. Therefore, in this article we’ll walk through Airbnb’s complaints in detail, and talk about how some of those same problems could’ve been handled in NativeScript.

We’ll start with the things NativeScript does well (this is the NativeScript blog after all), and move on to some of the things NativeScript does, well, less well 🙂

## The bridge

>  “React Native has a bridge API to communicate between native and React Native. While it works as expected, it is extremely cumbersome to write.”

The way that React Native and NativeScript allow developers to access native APIs is the perhaps the single biggest architectureal difference between the two frameworks.

Both React Native and NativeScript provide a series of cross-platform APIs for common mobile tasks. For example in [React Native you use an API named `Animated`](https://facebook.github.io/react-native/docs/network.html) for animations, and in [NativeScript you use an API named `Animation`](https://docs.nativescript.org/angular/ui/animation-code), however they provide very similar functionality (animating user interface components). In some cases the NativeScript and React Native cross-platform APIs are identical, for example, both frameworks provide support for the web’s `fetch()` and `XMLHttpRequest` APIs.

The architectural differences come when you need to do something that isn’t a super common mobile task—aka, when you need to perform some native action not provided by the cross-platform APIs. In React Native to access native iOS and Android APIs you need to use a series of bridge APIs (here’s are [docs for iOS](https://facebook.github.io/react-native/docs/native-modules-ios.html); here are the [docs for Android](https://facebook.github.io/react-native/docs/native-modules-android.html)).

A full breakdown of these APIs is out of the scope of this article, but what I want you to note is how these documentation pages contain both native and JavaScript code. For example, here’s the first example from React Native’s iOS bridging documentation

![](react-native-example.png)

> “ We also experienced many issues in which the types coming from JavaScript were unexpected. For example, integers were often wrapped by strings, an issue that isn’t realized until it is passed over a bridge. To make matters worse, sometimes iOS will fail silently while Android will crash. We began to investigate automatically generating bridge code from TypeScript definitions towards the end of 2017 but it was too little too late.”

## Type safety

## Lists

## JavaScript VMs

## 


The Bad

Hot reload
No React support
Integrating into native apps