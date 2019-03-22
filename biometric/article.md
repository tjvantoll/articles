# Biometric Authentication for Enterprise Apps

> “My favorite part of development is building login screens.” - No developer, ever

> “My favorite part of this app is the login screen.” - No user, ever

Login screens are the worst. They’re mundane to build, full of potential security vulnerabilities, and often require developers to make complex integrations they don’t want to make. Add enterprise terms like SAML and Sharepoint into the mix, and you’ll quickly have a developer riot on your hands.

But here’s the thing—login screens are important, and designing a solid login experience can be an enormous productivity boost for your organization. Specifically, biometric authentication, aka logging in with something like your fingerprint or face, can greatly streamline the login process for your internal apps.

In this article we’ll look at how to build enterprise login screens that leverage biometric authentication driven by [NativeScript](https://www.nativescript.org/) and [Kinvey](https://www.progress.com/kinvey). We’ll also look at how to connect to existing enterprise auth providers like Active Directory, so that you can see how to build a viable enterprise authentication workflow for you own apps. Here’s a gif showing this article’s final app in action.

-- image --

One note—don’t feel the need to follow along with every step of this article step-by-step, as the full source code is available on GitHub for you to peruse at any time. With that out of the way, let’s get started.

* [Step #1: Getting up and running](#step-1)
* [Step #2: Setting up enterprise auth](#step-2)
* [Step #3: Tying in biometric auth](#step-3)

<h2 id="step-1">Step #1: Getting up and running</h2>

In this article you’ll be using two different technologies: NativeScript, a framework for building native iOS and Android apps using JavaScript, and Kinvey, Progress’ powerful backend that will help you automate a number of the trickier authentication tasks.

> **TIP**: If you’re new to NativeScript and Kinvey, you might want to read [_How to Get Started With Kinvey and NativeScript—Fast_](https://www.progress.com/blogs/how-to-get-started-with-kinvey-and-nativescript-fast), for some background on each of the technologies.

In this step you’ll learn about the sample apps NativeScript provides, and then look at how to run those apps locally using the NativeScript command-line interface.

### Finding NativeScript samples

NativeScript offers a number of templates and samples to help you get apps up and running quickly on the [NativeScript Marketplace](https://market.nativescript.org/?tab=templates&category=all_templates).

![](marketplace.png)

On the listing you’ll see an app for building a good-looking login form. Clicking on that listing will take you to [this sample on NativeScript Playground](https://play.nativescript.org/?template=play-ng&id=Hqp5UQ&v=3073), a browser-based environment for developing apps.

NativeScript Playground is a powerful environment that’s worth experimenting with, especially if you’re interested in building iOS and Android apps with JavaScript. But for today’s purposes you’ll want to use the **Download** button (see image below) to get sample’s files locally.

![](playground.png)

When the download finishes, go ahead and unzip the `NSPlayground.zip` folder. (Feel free to rename the folder to the name of your project.) At this point, you’re ready to run this app on your development machine, and to do that, you’ll need the NativeScript command-line interface.

### Using the NativeScript CLI

The NativeScript CLI allows you to build, install, and run NativeScript apps on iOS and Android devices. You can install the NativeScript CLI by installing [Node.js](https://nodejs.org/en/), and running the following command on your terminal or command prompt.

```
npm install -g nativescript
```

> **TIP**: You can develop NativeScript apps using the NativeScript CLI on Windows, macOS, and Linux.

Next, you’ll need to install the appropriate iOS and Android dependencies that allow NativeScript to perform builds of your apps. The full instructions on how to set this up are out of scope for this article, but you can find a thorough guide on the NativeScript documentation.

* [NativeScript CLI Setup Documentation](https://docs.nativescript.org/angular/start/quick-setup#step-1-install-ios-and-android-requirements)

With that setup complete, you now have the ability to run your NativeScript app on iOS or Android devices. To do so, connect your device to your machine via USB, and use `tns run android` or `tns run ios` to deploy your new app.

```
tns run android
tns run ios
```

> **NOTE** By default you can only build iOS apps on macOS machines. NativeScript does allow you to build and deploy iOS apps on Windows using [NativeScript Sidekick](https://www.nativescript.org/nativescript-sidekick).

After you run your app you should see the following UI on your device.

-- images --

At this point you now have your app set up and ready to go. With this out of the way, let’s look at how to set up the enterprise auth.

<h2 id="step-2">Step #2: Setting up enterprise auth</h2>

Now that you have your app in place, let’s look at how to work with the backend. Progress Kinvey offers a feature called Mobile Identity Connect, which allows you to connect to a wide variety of existing authentication providers, such as LDAP, Active Directory, Facebook, or really, any provider that supports common protocols like SAML, OpenID or OAuth.

A full guide 

<h2 id="step-3">Step #3: Tying in biometric auth</h2>

lalalalal