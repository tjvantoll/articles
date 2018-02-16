# Announcing NativeScript-Vue 1.0

Last week, Jen Looper and Igor Randjelovic announced a 1.0 release of the [NativeScript-Vue plugin](https://nativescript-vue.org/) (TODO: link or picture here), which allows you to build native iOS and Android apps using [NativeScript](https://www.nativescript.org/) and [Vue.js](https://vuejs.org/).

<img src="site.png">

In this article we’ll talk about what this release means, how you can get started, what’s next for the integration, and how you can get involved.

There’s a lot to cover, so let’s dive right in.

## Getting Started

The easiest place to get started with NativeScript-Vue is in [NativeScript Playground](https://play.nativescript.org/), a browser-based NativeScript development environment that lets you start coding without setting up native iOS and Android SDKs on your development machine.

Start by visiting https://play.nativescript.org/?template=play-vue, which opens a Playground with a Vue template preloaded. The first thing you’ll see is a prompt that looks like this.

![](qr.png)

Follow the instructions to download and install the “NativeScript Playground” app on an iOS or Android device.

> **NOTE**: You’ll also have to download and install the “NativeScript Preview” app, and the Playground will instruct you to do that if you don’t have that app already installed. The Playground app has the ability to scan QR codes, and the Preview app actually renders the code that you write in the browser.

Next, open the NativeScript Playground app on your device and tap the “Scan QR Code” option.

-- TODO: image --

Go ahead and scan your QR code in Playground (not the one in this article), and you should see an app that looks like this.

-- TODO: image --

What you’re seeing is a completely native iOS and Android app, using native user interface components, all built with JavaScript and Vue.

What’s cool about Playground is you can now start coding your app, and as you save changes you’ll see updates on your device automatically. For example, try dragging a button into your app’s template.

-- TODO:  gif --

Use `Cmd` + `S` (`Ctrl` + `S` on Windows) to save your changes, and you should see a button automatically appear on your device. Cool, huh?

Try dragging other components into your app to get a feel for how Playground works.

> **TIP**: Read through [Building Native iOS and Android Apps With Vue and NativeScript](https://developer.telerik.com/products/nativescript/native-ios-android-vue-nativescript/) for more a thorough guide to the NativeScript-Vue syntax and integration.

## Common questions

Now that you have the basics down, let’s look at some common questions related to NativeScript-Vue.

### How do I start developing locally?

Although Playground is great for trying the basics of NativeScript-Vue, eventually you’ll want to set up a local development environment. To do that you’ll need to [install the NativeScript CLI and set up the appropriate native iOS and Android dependencies](https://nativescript-vue.org/en/docs/getting-started/installation/) on your machine.

After that, you’ll be able to use the NativeScript CLI to build, run, and deploy NativeScript-Vue applications. For example the following command creates a new NativeScript-Vue app.

```
tns create sample-app --template nativescript-vue-template
```

The following command to run your app on Android.

```
tns run android
```

And the following command to run your app on iOS.

```
tns run ios
```

There are also [additional NativeScript-Vue templates](https://nativescript-vue.org/en/docs/getting-started/templates/) that you might want to check out depending on your personal preferences and project requirements.

### What samples are out there?

Tiago Alves has an excellent recreation of the [NativeScript Groceries sample built with Vue](https://github.com/tralves/groceries-ns-vue).

-- TODO: image of Groceries --

TODO: more technical background on the sample and how to use it.

### Is this Progress supported?

NativeScript-Vue is a community initiative led by Igor Randjelovic. Although many members of the NativeScript team are involved in the NativeScript-Vue project in one way or another, NativeScript-Vue is not an officially supported Progress product—meaning, for example, that NativeScript-Vue is not covered by [NativeScript’s developer support](https://www.nativescript.org/enterprise).

That being said, the NativeScript team is 100% committed to ensuring that NativeScript-Vue is successful. Meaning, we will continue to address bugs and issues that are blockers for the NativeScript-Vue project, as well as provide help working through integration issues as necessary.

NativeScript is an open platform, and helping integrations such as NativeScript-Vue is incredibly important to us.

-- image --

### Is this ready for production?

TODO: Ask Igor

### What’s next for this integration?

TODO: Ask Igor

### How do I get involved?

The NativeScript-Vue team hangs out in the #vue channel in the [NativeScript community Slack](https://developer.telerik.com/wp-login.php?action=slack-invitation). The Slack channel is a great place to meet other NativeScript-Vue users, ask any questions you might have, and even get involved with the development of the integration.

The entirety of NativeScript-Vue is [open source and on GitHub](https://github.com/nativescript-vue) and contributions are very much welcome.

## What’s next?

Excited and want to learn more? Excellent! Next month we’re holding an online event where we’ll talk about NativeScript-Vue in detail. We’ll have interviews with Igor, as well as some prominent Vue community members. (We might even have one very special surprise.)

[Sign up now! 🎉]()

