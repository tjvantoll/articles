# When to Build a Native App, Not a PWA

I don’t believe [Progressive Web Apps](https://developers.google.com/web/progressive-web-apps/) (PWAs) are the solution to every mobile development problem. I think most people would agree with that statement to some extent, but the challenge comes where you draw the line—that is, what are the specific situations where you should build a native iOS and Android app, and what are the use cases that are best served by a PWA?

As a developer advocate for Progress, a company that makes both [Kendo UI](https://www.telerik.com/kendo-ui) (a collection of web user interface widgets) and [NativeScript](https://www.nativescript.org/) (a framework for building native iOS and Android apps) it’s a question I get a _lot_, so I thought I’d take some time to write down my opinion on the topic.

One important note before we dive in—I recommended making the web your default deployment platform. Meaning, in the case of mobile app development, I believe you should build a PWA unless you have a compelling reason not to. The web platform is the easiest platform to deploy to (by a lot); the web immediately gives the entire world access to your app; and the web’s wild popularity means it’s far easier to find talented web developers to work with.

That being said, I think many PWA enthusiasts ignore the benefits that come with building for native mobile platforms—benefits I’ve seen first-hand from working with the NativeScript community over the last three years. With this in mind, here’s the way this post works: the following sections are the specific reasons you should consider building a native iOS or Android app instead of, or in addition to, building a PWA. Hopefully you’ll find this discussion interesting if you find yourself on the fence between native and web app development for your next project.

Sound good? Ok, let’s get started.

## Situation #1: You need to do something the web can’t do

The web has made numerous advances over the past few years, but the web can’t keep up with proprietary platforms that can ship features without needing to go through a standards body. Sometimes these