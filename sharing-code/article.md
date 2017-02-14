# A Guide to Sharing Angular Code Across Web and Native Apps

One of Angular’s most compelling new features is its ability to run in multiple environments. But although you _can_ run Angular code on the web and in native apps, the specific of actually doing so are still not especially clear.

In this article I’m going to compare and contrast two options for sharing code across environments, and make some recommendations on when each approach works best.

## The scenario

For the sake of this article suppose you are the Pokémon Company, you need to build a new Pokémon viewing app, and you need the app to be available on the web, the iOS App Store, and Google Play. You have decided to use Angular and [NativeScript](https://www.nativescript.org/) to build your apps, and you’ve also decided to drive your apps off of the [pokéapi](https://pokeapi.co/)—a popular RESTful API that provides access to all things Pokémon.

Although you would expect some of the code for these apps to be different between the web and native, a whole lot of it is going to be the same. There’s no need to write your model objects twice, or your services that hit the backend API.

## Approach #1: Use a shared npm package

