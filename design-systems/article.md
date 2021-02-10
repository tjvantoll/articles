# An Opinionated Guide to Starting a UI Component Library

Building a custom component UI library is a great way to create consistent user interfaces throughout your organization.

But building component libraries is also hard, as you immediately have to solve a number of problems—like, what technologies are you going to use to build the components, how are you going to document those components, and how are you going to distribute everything throughout your organization?

In this article I’m going to walk you through an opinionated set of steps to get a component library up and running fast. My focus will be on helping you set up a development environment that allows to develop your components, and also see those components running in a live app. I’ll also cover builds, so that you can have a built npm package ready to distribute to other developers at your company.

If you follow the tutorial to the end, you’ll have a development environment that looks like this.

![](whole-workflow.gif)

Let’s get started.

## Getting started

For the purposes of this article we’re going to assume we work for a fictitious company named ACME, and we’re creating a handful of components that ACME will use throughout their organization.

Let’s start by creating the npm package that will contain all of ACME’s components. To do so, run the following commands from your terminal or command prompt to create a directory for your project.

```
mkdir acme-components
cd acme-components
```

Next, create two new subdirectories named `demo` and `src`.

```
mkdir demo src
```

The idea here is the `src` directory will contain all of your company’s components, aka the actual component source code, and the `demo` directory will contain a demo app that lets you test your components in a live running app.

At this point you should have a folder structure that looks like this.

```
acme-components
├── demo
└── src
```

In the next two sections we’ll look at how to start writing your components, and then how to build a demo app so that you can test your components as you write them. Let’s start with the components themselves, and discuss one of the first questions you’ll have to answer: which framework to use?

## Choosing a framework

One of the most challenging parts of writing components for an entire organization is deciding on a framework to use, if any. At large companies it’s fairly common to have apps built with a variety of front-end frameworks—both because enterprise apps stick around for a long time, and also because developers have different opinions on what the “best” framework is.

This fragmentation is a problem when it comes to building components that you intend to use in a standard way throughout an organization. When building a component library you have three options for how to deal with this situation.

1) **Choose one framework**

* With this option you build all of your components with one framework—aka you build either React components, or Angular components, or whatever other framework.
* This option makes the most sense for companies that have standardized on a single framework for all of their applications.

2) **Support multiple frameworks** 

* With this option you build your components multiple times, once for each framework you need to support.
* This option is not as bad as it sounds, as even though your are writing the same components multiple times, you do get to share code, such as your markup structure, and the CSS to style your components.

3) **Write framework-agnostic components**

* With this option you build all of your components without frameworks like React, Angular or Vue, and you building your components on top of the browser’s web component APIs.
* Although this seems appealing—who wouldn’t want components that can work in any app?—the downside is most developers have a lot more experience working with their framework of choice than they do with web components. And although web components have come a long way in the last decade, they still don’t offer many of the features that frameworks like React, Angular, and Vue offer out of the box.

Like any software decision, the correct option is highly dependent on your team and the applications you support, but for most organizations I recommend starting with #1 (choose one framework), and moving on to #2 (support multiple frameworks) as necessary.

For this article we’ll use approach #1 and build our component suite with React. You can use the same basic project structure and workflow with frameworks like Angular and Vue, but some of the specifics, such as how you build your demo app, will be slightly different. I’ll make a note of those differences as we cover them.

Let’s start building.

## Creating your components

Let’s return to your project, which remember current has the following directory structure.

```
acme-components
├── demo
└── src
```

In this section you’ll start building in the `src` directory, which will contain the components’ source code.

To start, go ahead and `cd` into the `src` directory on your terminal or command prompt.

```
cd src
```

Next, run `npm init` to generate a `package.json` file for your components.

```
npm init
```

The `init` command will first prompt you for a package name. When it does, type in `"acme-components"`, as otherwise npm will make the package name `src`, as it’s the name of the folder.

![](package-name.png)

Feel free to accept the defaults for all subsequent questions, which you can do by hitting the Enter key a bunch.

Now that you have your `package.json` file, let’s create a few new files that you’ll use to write the components themselves. While still in the `src` directory, create three new files, `Button.js`, `Input.js` and `theme.css`. Your directory structure should now look like this.

```
acme-components/
├── demo
└── src
    ├── Button.js
    ├── Input.js
    ├── package.json
    └── theme.css
```

Next, open your three new files and paste in the code below.

> **NOTE**:
> * These components are purposefully simple so we can focus on the workflow.
* * If you use Angular or Vue, you would write these components with those frameworks instead of using React syntax. 

``` JavaScript
// Button.js
import React from 'react';

const Button = (props) => {
  const { type } = props;
  return (
    <button
      type={type || "submit"}
      className="acme-button">
      {props.children}
    </button>
  )
}

export default Button;
```

``` JavaScript
// Input.js
import React from 'react';

const Input = (props) => {
  return (
    <input {...props} className="acme-input" />
  )
}

export default Input;
```

``` CSS
/* theme.css */
.acme-button {
  color: #444;
  background: lightblue;
  padding: 0.5em;
  border-radius: 4px;
  text-shadow: 0 1px 1px rgba(0, 0, 0, 0.2);
  font-size: 1.1em;
}
.acme-input {
  padding: 0.5em;
  color: #444;
  font-size: 1.1em;
  border-radius: 4px;
}
```

The idea here is that these Button and Input components are standard components to be used throughout ACME, and the `theme.css` file provides a way to style these components (and any future ones) consistently.

As a next step, you’ll need to be able to run these components in a browser, and to do that you’ll need to run them through a build.

## Building your components

Pretty much every modern JavaScript framework requires you to use a build package your files. For React, you need a build process that can take syntax like JSX, and turn it into code that the browser can interpret and run.

Although you have options for how you do this compilation, the most standard way to handle this in React is with [Babel](https://babeljs.io/). In this section you’ll add Babel to your component project, and use it to build an npm package that you distribute to other projects.

Your first step is to install Babel in your project, which you can do by running the following command in your terminal or command prompt. (And make sure you’re in your project’s `src` directory when you run this.)

```
npm install --save-dev @babel/cli @babel/core @babel/preset-env @babel/preset-react
```

Along with Babel itself, this command also installs [Babel presets](https://babeljs.io/docs/en/presets), which are set of configuration options. In this case you’re using `@babel/preset-env`, which is a common set of JavaScript defaults, and `@babel/preset-react`, which is a common set of React defaults.

> **TIP**: There is also a [popular Babel preset for Vue](https://cli.vuejs.org/core-plugins/babel.html#configuration).

To tell Babel to use these presets, go ahead and create a `.babelrc` file within your `src` directory.

```
acme-components/
├── demo
└── src
    ├── .babelrc   <-- HERE
    ├── Button.js
    ├── Input.js
    ├── package.json
    └── theme.css
```

Next, open your newly created `.babelrc` file and paste in the following configuration.

``` JavaScript
{
  "presets": ["@babel/react", "@babel/env"]
}
```

> **TIP**: You can read about [more advanced ways of configuring Babel](https://babeljs.io/docs/en/config-files) on their docs.

With the presets in place, you now have everything you need to build your components with Babel. To do so, open your `package.json` file, and replace the current `"scripts"` key-value pair with the code below.

``` JavaScript
"scripts": {
  "build": "babel *.js *.css package.json --out-dir ../dist --copy-files"
},
```

Let’s break down what’s happening here. First, adding a new script to your `package.json` gives you a new command that you can use with `npm run`—meaning, after you save you `package.json` file with this change, you can run your new `"build"` script by executing `npm run build`.

The build command itself tells Babel to operate on all JavaScript files (`*.js`), all CSS files (`*.css`), and your `package.json` file. The command says to place your built files in a new `dist` directory (`--out-dir ../dist`), and to copy all the files it operates on to that new directory (`--copy-files`).

> **NOTE**: By default Babel copies all JavaScript files it builds to the `--out-dir`. The `--copy-files` option is necessary for copying over your CSS files and `package.json` file.

To see this for yourself, go ahead and run your build by executing the following command in your terminal or command prompt.

```
npm run build
```

After the build runs, you should have a new `dist` directory that contains built versions of your JavaScript files.

```
acme-components
├── demo
├── dist
│   ├── Button.js
│   ├── Input.js
│   ├── package.json
│   └── theme.css
└── src
    └── ...
```

At this point you have an npm package that’s ready to distribute to other applications. However, what you have is still far from ideal. There’s currently no way to test these components in a real app, which makes it difficult to develop new features without a lot of manual steps.

Let’s look at how to build a development environment for these reusable components.

## Building your demo

In this section you’re going to add a demo app to your project for testing your components. You can build your demo app with any technology you’d like, but for this guide we’ll use [Create React App](https://github.com/facebook/create-react-app) so that we have a standard React environment.

> **TIP**: If your components will be used in multiple types of environments, it might make sense to create multiple demo apps so you can test your components in each. In that case I’d recommend creating multiple demo directories with descriptive names, for example `demo-react` and `demo-angular`.

To get started, return to your terminal or command prompt and `cd` into your project’s root directory.

```
acme-components <-- go here
├── demo
├── dist
│   └── ...
└── src
    └── ...
```

Next, run the following command, which uses Create React App to build a new app named “demo”.

```
npx create-react-app demo
```

In order to use your components in this new demo app, you’ll have to install them. To do that, start by switching to your `demo` directory.

```
cd demo
```

Next, run the following command (which we’ll discuss momentarily), to do the actual install.

```
npm install ../dist
```

When you use `npm install` you almost always want to install npm packages from the global npm registry. For example, `npm install react` tells npm to look for a package named "react" in its registry, and to install it into your application.

However, npm can also install local packages (aka a directory on your local machine that has a `package.json` file in it), and you can do so by passing npm a path to the directory to install. So in this case, `npm install ../dist` tells npm to install the package in `../dist` in your demo app.

And if you open your demo application’s `package.json` file, you’ll see a new dependency for `"acme-components"`.

```
"acme-components": "file:../dist",
```

This link gives you the ability to use your components and CSS files in your demo app. To do so, open your project’s `demo/src/App.js` file, and replace its contents with the following code.

``` JavaScript
import Button from 'acme-components/Button';
import Input from 'acme-components/Input';

import 'acme-components/theme.css';

function App() {
  return (
    <>
      <h1>ACME’s Components</h1>
      <Input value="Input component" />
      <Button>Button component</Button>
    </>
  );
}

export default App;
```

To see this code running in your browser, return to your terminal or command prompt, and execute `npm run start`, which is Create React App’s built-in way of starting up your application.

```
npm run start
```

After the command finishes, open your browser and go to `http://localhost:3000/`, where you should see your components in an app that looks like this.

-- browser image --

At this point you now have a set of reusable components, as well as a demo app for testing these components in a live app. This is pretty powerful, but we still have one last big problem to solve.

Consider what happens if you make an update to your `src/Button.js` file. Currently, in order to see that change, you’d have to `cd` into your `src` folder and re-execute `npm run build`. Although you _can_ do this, it’s a very manual and error-prone process.

Let’s look at how you can optimize this.

## Establishing a development workflow

In this section you’ll learn how to set up a development workflow that lets you see component updates live in your demo app.

To do so you’ll set up a watcher that listens for changes to files in your `src` directory, and then triggers a build that updates your project’s `dist` directory.

To implement this first `cd` back into your project’s `src` directory.

```
acme-components
├── demo
├── dist
│   └── ...
└── src <-- go here
    └── ...
```

Next, use the command below to install the [`npm-watch` package](https://github.com/M-Zuber/npm-watch).

```
npm install --save-dev npm-watch
```

npm-watch is a simple utility package that lets you watch files and take action when those files change. To use it you’ll need to make two changes in your project’s `src/package.json` file.

First, replace package’s existing "scripts" with the code below, which adds a new `watch` command that runs `npm-watch`.

```
"scripts": {
  "build": "babel *.js *.css package.json --out-dir ../dist --copy-files",
  "watch": "npm-watch"
},
```

Next, use the code below to add a new top-level "watch" key-value pair.

```
"watch": {
  "build": {
    "patterns": ["*"],
    "extensions": "css, js"
  }
},
```

The first bit of configuration `"watch": "npm-watch"` makes it so `npm run watch` invokes your newly installed `npm-watch` command.

The second bit of configuration tells `npm-watch` what files to watch, and what command to run when those files change. In this case the above configuration tells `npm-watch` to run your "build" command anytime `.css` or `.js` files change within any directory.

To test this, return to your terminal or command prompt, ensure you’re still in your project’s `src` directory, and then execute `npm run watch`.

```
npm run watch
```

With the watcher running, open your `src/theme.css` file and change `color: #444` to `color: black`. When you save your change, your watcher should detect the change, trigger a new build, and copy the updated file to `dist/theme.css`.

Now that you have a watcher in place for your components, let’s put together. Your end goal is to have a workflow that allows you to develop your components while seeing them running in a live application. To do that you’re going to need to have two terminals running—one that watches your components, and another that runs your demo application. Specifically, you need to have `npm run watch` executing in your `src` directory, while also having `npm run start` executing in your `demo` directory.

There are many ways you can accomplish this depending on your terminal or command prompt client, but personally I like setting up this workflow entirely within Visual Studio Code.

Visual Studio Code has an [integrated terminal](https://code.visualstudio.com/docs/editor/integrated-terminal) that you can open with `Ctrl` + <code>`</code> (backtick). With the terminal open, you can use the button below to split the terminal, which creates two terminal instances that appear side by side.

![](split.png)

With this split I navigate the left terminal to my `src` directory and run `npm run watch`, and then I navigate my right terminal to my `demo` directory and run `npm run start`.

![](workflow.png)

Next, I use VS Code’s [side-by-side editing](https://code.visualstudio.com/docs/getstarted/userinterface#_side-by-side-editing), and open my component files in editing column that lines up with my `src` terminal, and open my demo files in an editing column that lines up with my `demo` terminal.

![](side-by-side-editing.png)

With all of these steps in place, I now have the ability to change files in either my components or my demo, and to see those changes instantly.

![](whole-workflow.gif)

I like using Visual Studio Code because I really like the side-by-side interface for both editing and terminals, but you can accomplish the same workflow in other environments—all you need to do is execute `npm run watch` in your `src` directory and execute `npm run start` in your `demo` directory.

## Common questions

In this article you learned an opinionated workflow for building custom component libraries, but component libraries tend to get complex, so I wanted to wrap up by answering some common questions about the next steps you can take. (And let me know in the comments if you’d like to see me expand on any of these topics in future articles 🙂 )

### How do I distribute my components?

If you use this article’s workflow your `dist` folder is a complete npm package that you can immediately use in other applications.

You you choose to distribute that depends on your company’s infrastructure. If you want the package to be publicly available you can [publish the package to npm](https://docs.npmjs.com/cli/v6/commands/npm-publish). If your company uses a [private npm registry](https://docs.npmjs.com/creating-and-publishing-private-packages) you can publish your there.

### How do I document my components?

Documentation is vital when building a set of components. _How_ exactly you document the components is up to you.

One thing I see people commonly do is turn their demo application into documentation. For example you could create a one page per component, and document the syntax and different ways you can use each component. Then you can deploy your demo app to a web server that other in your company can view. The advantage of this approach is it encourages you to maintain your documentation as you develop your components.

There are other options as well. You could reuse a documentation system your company might already be using, such as a Wiki. You could also check out a framework like [Storybook](https://storybook.js.org/), which allows you to build visual documentation for your components within the same project.

### Should I add dependencies to my components?

Although it’s relatively easy to build your own inputs and buttons, things get harder when you need more complex components like datepickers or dialogs.

In these situations I’m a big proponent of wrapping existing component libraries that have already solved these problems. Aka, you write a DatePicker component using this article’s workflow, but under the hood you use a third-party datepicker from an existing library.

Any library you trust works, but as a member of the KendoReact team I have to put in a recommendation for [KendoReact](https://www.telerik.com/kendo-react-ui/components/) here. We built the [KendoReact components](https://www.telerik.com/kendo-react-ui/components/) with modularity and extensibility in mind, so you should find our components easy to build on top of in your own libraries.

### Can I unit test my components?

The great thing about this article’s workflow is, at the end of the day, it’s just a JavaScript project, so there’s nothing stopping you from adding other functionality such as unit testing. You can add unit tests directly in your component’s `src` directory, you could implement the tests in your demo application, or you could do some combination of both.

### Are there better ways of doing this?

There are a lot of different ways of writing component libraries. The recommendations I give in this article are based on my own experience for building these types of libraries, but like anything in the software world, what works best for you depends on your company and your requirements.

With that in mind I’d love to hear from you. Are you building a custom component library for your company? If so what has worked for you? What hasn’t? Let me know because I’d love to incorporate your experiences into future articles.
