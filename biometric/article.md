# Biometric Authentication for Enterprise Apps

> “My favorite part of development is building login screens.” - No developer, ever

> “My favorite part of this app is the login screen.” - No user, ever

Login screens are the worst. They’re mundane to build, full of potential security vulnerabilities, and often require developers to make complex integrations they don’t want to make. Add enterprise terms like SAML and Sharepoint to the login process and you’ll quickly have a developer riot on your hands.

But here’s the thing—login screens are important, and designing a solid login experience can be an enormous productivity boost for your organization. Specifically, biometric authentication, aka logging in with something like your fingerprint or face, can greatly streamline the login process for your internal apps.

In this article we’ll look at how to build enterprise login screens that leverage biometric authentication driven by [NativeScript](https://www.nativescript.org/) and [Kinvey](https://www.progress.com/kinvey). We’ll also look at how to connect to existing enterprise auth providers like Active Directory, so that you can see how to build a complete enterprise authentication workflow for your companies’ apps. Here’s a gif showing this article’s final app in action.

-- image --

One note—don’t feel the need to follow along with every step of this article step-by-step, as the full source code is available on GitHub for you to peruse at any time. With that out of the way, let’s get started.

* [Step #1: Getting an app up and running](#step-1)
* [Step #2: Setting up enterprise auth](#step-2)
* [Step #3: Tying in biometric auth](#step-3)

<h2 id="step-1">Step #1: Getting an app up and running</h2>

One of the first decisions you have when building any app is deciding which platforms the app should run on. When it comes to biometric authentication this decision is rather simple, as mobile platforms are currently the only platforms that allow developers to access fingerprint and face sensors.

With that in mind, in this article you’ll use two technologies to make building this login screen as easy as possible: NativeScript, a framework for building native iOS and Android apps using JavaScript, and Kinvey, a powerful backend that will help you automate a number of the trickier authentication tasks.

> **TIP**: If you’re new to NativeScript and Kinvey, you might want to read [_How to Get Started With Kinvey and NativeScript—Fast_](https://www.progress.com/blogs/how-to-get-started-with-kinvey-and-nativescript-fast), for some background on each of the technologies.

In this step you’ll learn about the starter apps NativeScript provides, and then look at how to run those apps locally using the NativeScript command-line interface.

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

With that setup complete, you now have the ability to run your NativeScript app on iOS or Android devices. To do so, connect your mobile device to your machine via USB, and then run either `tns run android` or `tns run ios` (depending on your device’s operating system) to deploy your new app.

```
tns run android
tns run ios
```

> **NOTE** By default you can only build iOS apps on macOS machines. NativeScript does allow you to build and deploy iOS apps on Windows using [NativeScript Sidekick](https://www.nativescript.org/nativescript-sidekick).

After you run your app you should see the following UI on your device.

-- images --

At this point you now have your app set up and ready to go. With this out of the way, let’s look at how to set up the enterprise auth.

<h2 id="step-2">Step #2: Setting up enterprise auth</h2>

In this step we’ll look at how to perform the authentication piece of the login workflow. Although there are tons of potential login workflows, it’s uncommon for enterprise apps completely new authentication mechanisms. That is, most companies already have an auth provider in place, with one of the more common solutions being Active Directory.

To make connecting to your existing authentication provider as easy as possible, in this step we’ll use Progress Kinvey. Kinvey offers a feature called Mobile Identity Connect, which allows you to connect to a wide variety of existing authentication providers, such as Active Directory, Facebook, or really, any provider that supports common protocols like SAML, OpenID or OAuth.

### Setting up Mobile Identity Connect

Mobile Identity Connect (MIC) is a service that bridges mobile applications with existing enterprise identity and single sign-on solutions. MIC enables mobile applications to integrate with a variety of identity solutions using a single OAuth2-based interface.

To set up MIC for your own apps you’ll have to set up a new service in [Kinvey Console](https://console.kinvey.com), your dashboard for doing all things Kinvey. Here are a few resources that will help you set that up as easily as possible.

* [Kinvey documentation on MIC](https://devcenter.kinvey.com/nativescript/guides/mobile-identity-connect)—Start here, as the documentation walks you through background information on MIC, as well as the steps you need to take to set up your own connection.
* [Enterprise Authentication with Kinvey](https://www.progress.com/blogs/enterprise-authentication-kinvey)—Read this next, as it’s a tutorial that walks you through setting up MIC with a sample Azure Active Directory instance.

When you have your MIC service set up and ready to go, let’s look at how to connect your Kinvey backend to your NativeScript app.

### Connecting your app to Kinvey

Connecting NativeScript apps to Kinvey is simple, especially if your apps come NativeScript Playground (which if you’ll recall our login sample did), as Kinvey is already set up in these apps by default.

Because of this, the only step you need to take is adding your Kinvey **App Key** and **App Secret** in the appropriate place so that NativeScript can make the connection. To do that, open your NativeScript app’s `app/package.json` file, and a new `"pluginsData"` key with the following contents.

```
"pluginsData": {
    "kinvey-nativescript-sdk": {
        "config": {
            "appKey": "YOUR APP KEY HERE",
            "appSecret": "YOUR APP SECRET HERE",
            "redirectUri": "sde://"
        }
    }
}
```

Next, you’ll need to replace the two placeholder values in the configuration above with your own values. To get them, visit [Kinvey Console](https://console.kinvey.com/) for your app, and tap the three vertical dots in the top-left corner. There you’ll see both the **App Key** and **App Secret** values you need.

![](config-values.png)

When you’re done, you complete `app/package.json` file should look something like this.

```
{
    "android": {
        "v8Flags": "--expose_gc",
        "forceLog": true
    },
    "main": "main.js",
    "name": "tns-template-blank-ng",
    "version": "3.1.1",
    "pluginsData": {
        "kinvey-nativescript-sdk": {
            "config": {
                "appKey": "kid_rkDJUINIQ",
                "appSecret": "17282f9d91da4af7b398855e32ea4dd0",
                "redirectUri": "sde://"
            }
        }
    }
}
```

To see what this authentication setup looks like in action, let’s move on to the final step and add some code to tie everything together.

<h2 id="step-3">Step #3: Tying in biometric auth</h2>

In this step you’ll use NativeScript to build a login screen that can both leverage your Kinvey MIC setup, as well as add in biometric auth to allow users to login with their fingerprint or face. Let’s start by getting the authentication workflow working, and then move on to the biometric piece.

### Wiring up the login process

The default app that you downloaded from NativeScript Playground is set up for a login process where the user provides a user name and password, and currently looks like this.

-- same images from earlier--

In this case though, you’re delegating the login process to your own enterprise auth mechanism, and as such, you can simply the current login code considerably. To do so, start by opening up your `app/login/login.component.html` file and replacing its contents with the following code.

``` XML
<GridLayout>
    <StackLayout class="form">
        <Image class="logo" src="~/images/logo.png"></Image>
        <Label class="header" text="APP NAME"></Label>

        <Button text="Log In" [isEnabled]="!processing"
            (tap)="login()" class="btn btn-primary m-t-20"></Button>
    </StackLayout>
</GridLayout>
```

Next, open your `app/login/login.component.css` file and replace its contents with the following code.

``` CSS
.form {
  margin-left: 30;
  margin-right: 30;
  vertical-align: middle;
}

.logo {
  margin-bottom: 12;
  height: 90;
  font-weight: bold;
}
.header {
  horizontal-align: center;
  font-size: 25;
  font-weight: 600;
  margin-bottom: 70;
  text-align: center;
  color: #D51A1A;
}

.btn-primary {
  margin: 30 5 15 5;
}
```

If your NativeScript app is still running you should see these changes immediately. If not, head back to your terminal or command prompt and use `tns run ios` or `tns run android` to redeploy the app to your device. When you’re done, you’ll see that the app now has a simplified look.

-- images --

> **NOTE**: The diamond logo and “APP NAME” heading are placeholders. Feel free to replace these with your own company logo and name.

Next, open your `app/shared/user.service.ts` file and replace its contents with the following code, which adds a few new methods you’ll need for MIC and for biometric authentication. Specifically, the `Kinvey.User.loginWithMIC()` function is what actually integrates this app with the Kinvey auth service you made for connecting to your authentication provider.

``` TypeScript
import { Injectable } from "@angular/core";
import { Kinvey } from "kinvey-nativescript-sdk";
import { getBoolean, setBoolean } from "tns-core-modules/application-settings";

@Injectable()
export class UserService {
    isLoggedIn() {
        return !!Kinvey.User.getActiveUser();
    }

    login() {
        return Kinvey.User.loginWithMIC()
            .catch(this.handleErrors);
    }

    logout() {
        return Kinvey.User.logout()
            .catch(this.handleErrors);
    }

    handleErrors(error: Kinvey.BaseError) {
        console.error(error.message);
        return Promise.reject(error.message);
    }

    setBiometricAuthOptIn(isOptedIn: boolean) {
        setBoolean("biometricAuthOptIn", isOptedIn);
    }

    getBiometricAuthOptIn() {
        return getBoolean("biometricAuthOptIn");
    }
}
```

Finally, open your `app/login/login.component.ts` file, and replace its contents with the following code.

> **TODO**: Add note about what changed.

``` TypeScript
// TODO: Add this
```

When you save these changes the NativeScript CLI should automatically update your app on your device. When it does, try your new app out. If all went well, you should now have a mobile app that leverages your existing auth provider.

-- gifs --

You now have a cross-platform iOS and Android app that reuses your existing authentication system. Pretty cool, huh?

Let’s look at how you can add even more power to this setup by integrating biometric authentication.

### Adding biometric auth

## Wrapping up