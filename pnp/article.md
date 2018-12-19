# Portable North Pole—Your Go-To NativeScript App This Holiday Season

The holidays are busy times for many, myself included, but for most of us, holiday planning doesn’t including architecting an app that can handle more than 100,000 simultaneous users.

This is the challenge [uGroupMedia](http://ugroupmedia.com/) faces every year with their absurdly popular [Portable North Pole app](https://www.portablenorthpole.com), which allows users to create personalized Santa video content in a number of really cool ways.

![](banner.png)

UGroupMedia uses NativeScript to build and deploy Portable North Pole from a single JavaScript codebase. And it seems to be working, as the app’s reviews have been consistently high throughout the holiday season.

<div style="display: flex">
    <img src="ios-ratings.png" style="border: 1px solid black;">
    <img src="play-ratings.png" style="border: 1px solid black;">
</div>

## Architecture

Portable North Pole uses [xplat](https://nstudio.io/xplat/), a free-to-use code-sharing solution from [nStudio](https://nstudio.io/). xplat is an Angular-based solution that allows you to build for web, iOS, and Android, simultaneously. Richard Smith, the Lead Mobile & Web Lead Application Developer at UGroupMedia had this to say of the approach.

> “We needed the ability to develop and maintain our app for iOS, Android, and Web, but with a small team, an efficient and reliable code-sharing solution was necessary. With NativeScript, the shared xplat code-base allows developers with diverse backgrounds to contribute comfortably to all 3 platforms, while still being able to utilize their previous experience and specializations. It is a great environment to work in and enables us to deliver much more with our existing team.”

You can see this in action in many different parts of the app, such as the main screen where you pick between their video options.

![](three-apps.png)

Or the form you use to customize those videos before they get processed on the Portable North Pole backend.

![](three-apps-2.png)

> **TIP**: Interested in getting started with your own code-sharing app using NativeScript? Check out our [documentation hub on the topic](https://docs.nativescript.org/angular/start/introduction).

Even though UGroupMedia used a code-sharing approach to boost their productivity, they still managed to provide really custom experiences on each platform they build for.

For example, both the web and mobile versions of PNP allow you to upload images, but the mobile version allows you to crop the image you select.

![](camera-in-action.gif)

Being able to perform small little tweaks like this can really enhance the user’s experience, and with NativeScript you can easily add this polish while remaining in a code-sharing structure.

There are a ton of these nice little tweaks throughout the app. For example, the app can detect when your volume is low and give a helpful message.

![](volume-warning.png)

The video sharing integrates with a device’s native sharing capabilities.

![](sharing.png)

And you can pay for the premium videos using your device’s built-in in-app purchase APIs.

![](in-app-payments.png)

And really, we’re just scratching of the cool things that Portable North Pole is doing in their NativeScript app. (They’re also doing some cool things with video; they support four languages; and they have a neat integration with Zendesk built-in.)

To see it all in action you’re just going to have to check out the app for yourself.

## Try it out

Portable North Pole is a great app to experiment with if you want to see what NativeScript makes possible, or, if you just want to make a fun video for the children in your life.

To try it, head to [portablenorthpole.com](https://www.portablenorthpole.com/), or, use one of the links below to try the app out on your iOS or Android device.

[![](app-store.png)](https://itunes.apple.com/us/app/pnp-2016-portable-north-pole-create-santa-videos/id902026228?mt=8)
[![](google-play.png)](https://play.google.com/store/apps/details?id=com.ugroupmedia.pnp14&hl=en&pcampaignid=MKT-Other-global-all-co-prtnr-py-PartBadge-Mar2515-1)

And look forward to more technical writeups from the Portable North Pole team in the coming months!
