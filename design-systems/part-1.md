# The Ultimate Guide to Building a UI Component Library: Creating a Plan

**Every company should have a standard library of UI components**. Component libraries enforce consistency throughout your organization, both visually (how your company’s apps look), and technologically (which frameworks and dependencies your company’s apps use).

But building a corporate component library is also hard, as you have to deal with both organizational problems, like getting permission from management to work on components, as well as development problems, like determining which frameworks you’re going to use (if any), and how are you going to distribute components to your company’s applications.

I’ve spent over a decade working with UI components on the web, both as a member of the jQuery UI team, and now as a member of the [Kendo UI](https://www.telerik.com/kendo-ui) team at Progress. In this article series I will share advice and strategies I’ve learned that can help you build your own corporate component library—whether you’re building your own components from scratch, or whether you’re building on top of an existing set of components. Here’s what you can expect from this series:

* **Part 1—Creating a Plan**: (you’re here) You’ll learn how to plan a component library, including how to convince management and your coworkers that building a component library is a good idea, and how to select a JavaScript framework to use.

* **Part 2—Establishing a Development Environment**: (coming soon) You’ll learn how to set up your component library, with a focus on setting up a productive development environment.

* **Part 3—Building Robust Components**: (coming soon) You’ll learn how to approach building individual components, including a discussion on whether you should build your own components from scratch, add dependencies on existing libraries, or do some combination of both.

Let’s start by looking at how to get the process started.

## How to get started

Starting a new corporate component library can seem like a daunting task. Your end goal is to have a set of components your entire organization can use, but most companies have a disparate set of apps built with a variety of different frameworks and technologies.

With that challenge in mind, my recommendation is to start small. Pick two or three components that your company already has (button, headers, footers), and build them a in library that exists outside of any individual application. (You’ll learn the workflow I prefer to use for this in part 2.)

To help find the specific components to build, I recommend starting by doing an [interface inventory](https://bradfrost.com/blog/post/interface-inventory/), which has you catalog every permutation of components your company uses in a single document.

-- image of lots of components --

Creating an interface inventory serves two purposes. First, it can help you recognize which components you should start building in your library. (Look for simple components that many applications use.) But more importantly, an interface inventory is a great way to convince management that building a component library is worthwhile. The reason being—most companies that do an inventory discover that they have a mess of similar-yet-different components, and seeing 17 different button permutations can help change a hesitant manager into someone happy to devote development time on a project that establishes a standard set of components.

-- image of lots of different buttons --

Once you have a handful of simple components selected, you’re ready to start building. But before you start writing code you have one additional problem to address.

> **TIP**: I highly recommend checking out [Kathryn Grayson Nanz](https://twitter.com/kathryngrayson)’s [writeup on building components libraries](https://dev.to/kathryngrayson/case-study-building-a-component-library-e90), as it has several additional tips & tricks on starting a component library successfully.

## How to choose a JavaScript framework

One of the most challenging parts of writing components for an entire organization is deciding on which JavaScript framework to use, if any. At large companies it’s common to have apps built with a variety of front-end frameworks—both because enterprise apps tend to stick around for a long time, and because developers have different opinions on what the “best” framework is.

This fragmentation is a problem when it comes to building components that you intend to use in a standard way throughout an organization. You have three options for how to deal with this situation.

**Option 1: Choose one framework**

With this option you build all your components with one framework—aka you build either all React components, or all Angular components, or all Vue components.

This option makes the most sense for companies that have either standardized on a single framework for all of their applications, or have picked a single framework as their preferred option for new app development.

If your company is moving all apps towards a single framework, having a standard component library can help you migrate apps faster, as you’ll have a set of ready-to-use components.

**Option 2: Support multiple frameworks** 

With this option you build your components multiple times, once for each framework you need to support.

This option sounds bad—what developer wants to write anything multiple times?—but even though you’re writing components multiple times, you do get to share a surprising amount of code, such as your markup structure, and the CSS to style your components.

**Option 3: Write framework-agnostic components**

With this option you build all your components without frameworks like React, Angular or Vue, and you instead build your components on top of the browser’s web component APIs.

Although this option seems appealing—who wouldn’t want components that can work in any app?—the downside is most developers have a lot more experience working with their framework of choice than they do with web components. And although web components have come a long way in the last decade, they still don’t offer many of the features that frameworks like React, Angular, and Vue offer out of the box.

## Making a framework decision

The correct option for your company depends on your team and the applications you support. That being said, I recommend that most companies start with #1 (choose one framework), and moving on to #2 (support multiple frameworks) if necessary.

Over the years I’ve found that developers are most productive when they get to use a framework they’re familiar with—aka React developers are most productive when they use React components, Angular developers are most productive when they use Angular components, and so on.

At Progress we also use this approach for Kendo UI. Specifically, instead of offering one Kendo UI that works with any framework, we offer [Kendo UI for jQuery](https://www.telerik.com/kendo-jquery-ui), [Kendo UI for Angular](https://www.telerik.com/kendo-angular-ui), [KendoReact](https://www.telerik.com/kendo-react-ui/), and [Kendo UI for Vue](https://www.telerik.com/kendo-vue-ui)—each built from the ground up with their respective framework. As you might imagine this is a lot of work, but our users have consistency told us they prefer framework-specific components over framework-agnostic components. And we do get to share some code across all frameworks, for example [Kendo UI’s robust theming system](https://themebuilder.telerik.com/) works the same regardless of which JavaScript framework you use.

If you’re still struggling to decide on a framework, I’d encourage you to think about the type of components you yourself like to use. For example, if you’re a React developer that needs a datepicker, which are you more likely to use—a web-component-based datepicker that you have to figure out how to use in React, or a datepicker that was built by React developers with APIs you recognize?

Because I feel strongly that building framework-specific components is the right choice, that’s the approach you’ll use in the next article in this series. Specifically, you’ll learn how to build a component library with approach #1 (choose one framework), and you’ll build the components themselves with React.

Although you’ll be using React, you’ll learn how to build a project structure that can support approach #2 (support multiple frameworks), as oftentimes that’s a necessity for companies that have apps built with several different frameworks.

## Next steps

At this point, you’ve decided on a small handful of components to build, and you’ve decided on a JavaScript framework you’ll use to build your components with—so it’s time to start coding!

In this next part of this article series, you’ll learn how to create a development environment for building components from scratch. Stay tuned 🙂
