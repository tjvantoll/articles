# A Guide to Starting a Component Library for Your Company

Building a custom component library for a company is a great way to create consistent user interfaces throughout your organization.

But building component libraries is also hard, as you immediately have to solve a number of problems—like, what technologies are you going to use to build the components, how are you going to document them, and how are you going to distribute them throughout your organization?

In this article I’m going to walk through an opinionated set of steps you can use to get a component library up and running fast. My focus will be on helping you set up a development environment that allows to develop the components, and also see view those components in a live running app. I’ll also cover builds, so that you can have a built npm package ready to distribute to other developers at your company.

We’ll look at how to start writing the components themselves, how to set up a development environment, and how to distribute the components to other developers at your company.

Let’s get started.

## Getting started

For the purposes of this article we’re going to assume we work for a company fictitious company named ACME, and we’re creating a handful of components that ACME can use throughout their organization.

Let’s start by creating the npm package that will contain all of ACME’s components. To do so, run the following commands from your terminal or command prompt to create a directory for your project.

```
mkdir acme-components
cd acme-components
```

Next, use `npm init` to initialize this new directory as an npm package.

```
npm init -y
```

> **NOTE** The `-y` option tells npm to accept default values for metadata like project name, version, and description. You can change those in your project’s `package.json` file.

After that, create two new subdirectories named `demo` and `src`.

```
mkdir demo src
```

The idea here is the `src` directory will contain all of your company’s components, aka the actual source code, and the `demo` directory will contain a demo app that lets you test your components in a live running app.

At this point you should have a folder structure that looks like this.

```
acme-components
├── demo
├── package.json
└── src
```

In the next two sections we’ll look at how to start writing your components, and then how to build a demo app so that you can test your components as you write them. Let’s start with the components themselves.

## Building your components

One of the most challenging parts of writing components for an entire organization is deciding on frameworks. At large companies it’s fairly common to have a multitude of front-end frameworks in use, both because enterprise apps stick around for a long time (so you might have apps built with whatever was popular two, five, or ten years ago), and also because developers have different opinions on what the “best” framework is—especially when you’re building different types of applications.

This fragmentation, however, is a big problem when it comes to building components intended to used in a standard way throughout a company. When building a component library you have three options for how to deal with this situation.

1) 
