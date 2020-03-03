# The Bizarre Economics of Open Source, and What We Can Do About It

<!--
# Why are the Economics of Open Source Mind-Bogglingly Absurd?
-->

If you’re a software developer, you might not realize that the economics behind open source make zero sense to most people.

For example, consider this conversation I had with a normal person a few days ago.

> Me: “Sorry I’m a bit late. Crazy day at work”.

> Friend: “Ah, no worries, what’s up though?”

> Me: “We’re just trying to decide between three different JavaScript frameworks for that project, and the deadline is next week so we have to pick soon.

> Friend: “Ah, gotcha. Well which framework is the cheapest?”

> Me: “Oh they’re all free.”

> Friend: 🤯

In most industries you pay for tools that help you do your job, yet in the software world—a world where there’s an absolute ton of money involved—most of us build apps using a variety of free tools.

The most popular text editor? Visual Studio Code—free. The most popular source-control provider? git—free. The most popular JavaScript libraries? React, Angular, Vue, and their competitors—all free. Although paid software very much exists, it’s amazing how much of our critical infrastructure has moved to free and open-source software over the last handful of years.

And although this switch to open source has been enormously beneficial for developers, and for software in general, the shift to open source has also had consequences. In this article I’ll discuss one of those consequences, a problematic economic and funding model, and I’ll discuss what I think we can do about it.

Let’s start this discussion by taking a brief look at how we ended up with the open-source model we have today.

## How did this happen?

To give you a sense of how much times have changed, here are a few [quotes from Microsoft executives](https://www.cnet.com/news/microsoft-raps-open-source-approach/) from the early 2000s that haven’t aged well.

> “Open source is an intellectual-property destroyer. I can't imagine something that could be worse than this for the software business and the intellectual-property business.”
> - Jim Allchin (Former Windows Chief)

> “As history has shown, while this type of model [open source] may have a place, it isn't successful in building a mass market and making powerful, easy-to-use software broadly accessible to consumers”
> - Craig Mundie (Former Microsoft Senior Vice President)

Although it’s easy to laugh at these quotes today, they weren’t very radical opinions at the time. Even though open source was already an established and growing concept, most companies primarily used paid solutions to build applications.

I started my career in software in the early 2000s, and my first job involved an IBM-based IDE for writing Java code, a proprietary source-control solution that I’d prefer not to remember, and an IBM mainframe to host our production apps.

![](rad-developer.jpg)
_IBM’s Rational Application Developer. I used it in the early 2000s, and it’s still around today._

All of these tools cost money—a lot of money actually—but they were deemed an acceptable expense because the tools provided enough value to warrant their cost.

The switch to open source happened slowly through the 90s and into the 2000s. Companies increasingly realized that open source tools like MySQL and Apache were not only viable, but oftentimes better than the commercial products they were paying big money for.

My personal experience for this transformation was on the web, which in the mid 2000s was the wild west compared to the web we have today. Web developers were tasked with supporting a dizzying set of browsers, ranging from the newly released Internet Explorer 7, to the venerable IE6, as well as Firefox, an open-source browser that was starting to challenge Microsoft’s stranglehold on the browser market.

The tools developers built to manage the complexity of cross-browser development included the likes of Dojo, MooTools, jQuery, and many others.

![](jquery-2007.png)
_The jQuery homepage in June of 2007_

And while these frameworks took different approaches and used different APIs, they had one important thing in common: they were all free and open source.

Whereas more established development ecosystems—Java, .NET, etc—were still conflicted about open source, the web was built on free and open-source software from its onset.

This was a boon to web developers like me, as it meant I could instantly start tinkering with Dojo and jQuery at home, and even start using them at my corporate day job—a place where I was used to paying for the software tools I needed.

And it wasn’t just me that jumped on the chance to use these new libraries. jQuery usage exploded in the late 2000s, and created an enormous ecosystem of jQuery plugins that built upon what jQuery had started. The overwhelming majority of these plugins were free and open source, as that had become the expectation for any web framework or plugin by this point.

This new generation of web software inspired a lot of developers—myself included—and helped build the web into the dominant platform it is today. But this expectation that all software must be free and open-source helped to create what I see as an unexpected problem we have with open source today: a bizarre economic and funding structure.

## Open source and economics

Open source projects often start as a passion project for an individual or a small group, which they then share with the world for free. The fact that this is commonplace in the software world is actually kind of awesome.

But, that doesn’t mean that the work these developers do is 100% altruistic. The primary incentive to working on an open-source project today is career advancement. For example, many former members of the jQuery team now have prominent roles at major tech companies. Several [MooTools contributors now work on React at Facebook](https://www.freecodecamp.org/news/between-the-wires-an-interview-with-mootools-contributors-33d764957575/). Personally, I was on the jQuery UI team for two years, and that involvement helped me get the job I have today at Progress.

There’s nothing inherently wrong with career advancement being the primary incentive to work on open source, but it can become problematic when the project author(s) achieve some success. Because as it turns out, once you’ve achieved whatever notoriety you had in mind, suddenly dealing with random GitHub issues no longer feels like the best way to spend your Saturday nights.

In this situation, many developers try to gather donations to cover their time and effort. For example, if you look back at jQuery’s site from 2007, notice how there was already a donation button on the bottom-left corner of the screen.

![](jquery-donate.png)

The Dojo project had a similar donation on their site dating back to the same time frame.

![](dojo.png)

Today, these calls for donations more typically happen though Patreon, or through some form of “sponsorship”, which projects like ESLint and Vue.js use. Perhaps the most notorious example occurs in the popular [core-js library](https://github.com/zloirock/core-js), which includes overt donation requests every time you install the library, and which has generated [some controversy](https://github.com/zloirock/core-js/issues/548).

```
Thank you for using core-js ( https://github.com/zloirock/core-js ) for polyfilling JavaScript standard library!

The project needs your help! Please consider supporting of core-js on Open Collective or Patreon: 
> https://opencollective.com/core-js 
> https://www.patreon.com/zloirock 

Also, the author of core-js ( https://github.com/zloirock ) is looking for a good job -)
```

In an even more controversial move, last year the [Standard JavaScript project](https://github.com/standard/standard) [started showing ads every time you installed its package](https://www.zdnet.com/article/popular-javascript-library-starts-showing-ads-in-its-terminal/).

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">I guess we now live in the post-&quot;ads in the npm install log&quot; era <a href="https://t.co/pSnBnMDNSg">pic.twitter.com/pSnBnMDNSg</a></p>&mdash; Quine atom (@qntm) <a href="https://twitter.com/qntm/status/1165344132728066048?ref_src=twsrc%5Etfw">August 24, 2019</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script> 

As you might expect [developers weren’t too happy about the ad](https://github.com/standard/standard/issues/1381), and [npm quickly took action](https://www.zdnet.com/article/npm-bans-terminal-ads/)—banning any package that “display ads at runtime, on installation, or at other stages of the software development lifecycle, such as via npm scripts.”

Regardless what your think about ads in your npm logs, there’s one thing we can probably all agree on: from an economics perspective this development shouldn’t be surprising at all. 

In today’s open-source world there’s a massive disconnect between the amount of value projects like Standard provide, and the financial proceeds maintainers earn in return for their work. Programs like Patreon rely on the generosity of random individuals, which can never generate enough revenue to compensate a project maintainer for their time.

With that background in mind, let’s look at what I believe are three different ways we could attempt to 

## Solution #1: Foundations

- Foundations
  - .NET foundation
  - JS foundation
  - https://www.finos.org/
  - https://openjsf.org/
  - https://tidelift.com/

## Solution #2: GitHub Sponsors

## Solution #3: Paying for software

We here at Progress sell software, and increasingly our competition is not other paid tools, but rather, it’s software developers’ collective mentality that all software be free.

To be clear at Progress we heavily support open source. We’ve spent a bunch of time money on the [NativeScript](https://www.telerik.com/open) project and let developers build awesome apps with it for free. We’re a member of the [.NET Foundation](https://dotnetfoundation.org/). We 

But we also believe there’s still a place for paid software in developers lives. With paid software you get certain assurances, such as knowing the software will receive updates, and that you have a company you can reach out to when you run into issues and actually hear back. That doesn’t mean all software should be paid,



## Wrapping up


