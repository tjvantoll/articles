# How to Build a PWA, an iOS App, and an Android App—From One Codebase

I have a long history of choosing between web and native, often wrongly. I’ve built web apps that were scraped for native apps, and I’ve wasted time building native apps that found no audience.

In my current job as a mobile-focused developer advocate at [Progress](https://www.progress.com/), I talk to developers that regret their web or native decision every week. Sometimes you don’t realize you need a native app until you hit the limitations of the web, and conversely, sometimes you realize a web app meets your needs only after you’ve went through the lengthy process of building multiple native apps.

The good news is JavaScript developers no longer have to make this difficult choice. Through the use of the recently announced [NativeScript and Angular integration](https://blog.angular.io/apps-that-work-natively-on-the-web-and-mobile-9b26852495e7), it’s now quite easy to build a PWA (Progressive Web App), a native iOS app, and a native Android app from one codebase.

In this article I’ll show you how it works. You’ll learn the steps you’ll need to take, as well as some tips and tricks I learned from building an Angular app for all three platforms.

## Starting your app

Over the last month I built an app called Pokémon-based checklist app and deployed it to [Google Play](https://play.google.com/store/apps/details?id=com.tjvantoll.ShinyDex) and [the web](https://shinydex.app). The app is a purposely simple app designed to help teach how the NativeScript and Angular technology stack work.

![](apps.png)

For this article I’ll walk you through building a similar checklist-style app. Feel free to follow along as a way of starting your own code-sharing application.

Your first step is to install the Angular CLI, NativeScript, and NativeScript schematics, all of which are available on npm.

```
npm install -g @angular/cli
npm install -g nativescript
npm install -g @nativescript/schematics
```

* The [**Angular CLI**](https://cli.angular.io/) is a command-line interface for building and running [Angular](https://angular.io/) apps.
* [**NativeScript**](https://www.nativescript.org/) is an open-source framework for building iOS and Android apps with JavaScript or TypeScript.
* [**NativeScript schematics**](https://github.com/NativeScript/nativescript-schematics) is an Angular CLI extension that adds the ability to do NativeScript-related things. As you’ll see in a minute, this is what makes it possible to run your Angular apps on iOS and Android.

With installation out of the way, your next step is to start an app. To do that, run the following command from your terminal or command prompt.

```
ng new Checklist --collection @nativescript/schematics --shared
```

Let’s break down what’s happening here.

* `ng new` is the Angular CLI command you use to start new Angular apps.
* `Checklist` is your app name. You’ll want to switch this to the name of the app you want to build.
* The `--collection @nativescript/schematics` flag tells the Angular CLI about NativeScript schematics, which is going to make it possible for this app to run on iOS and Android through NativeScript.
* The `--shared` flag tells the Angular CLI you wish to share code between your web and native apps.

We’ll look through the files in your new app here in a minute, but first let’s look at how you can see what this new app looks like.

## Running your app

The first thing you’ll want to do is `cd` into the new app you just built.

```
cd Checklist
```

From here there three different commands you can use to run your app.

![](running.png)

First, `ng serve` is how you run your newly created app on the web. After you run this command you’ll see a message about an Angular Live Development Server listening.

![](terminal.png)

If you following the instructions and visit `localhost:4200`, you’ll see the default web app running, which is a simple little master-detail app showing soccer ⚽ players.

![](default-web-app.png)

If you’ve done any Angular development before this will feel very familiar, as it’s the same command and workflow you use to build Angular web apps. The real magic happens when you bring NativeScript into the picture.

Before I show how to run this app on iOS and Android, there’s one big warning I need to give: because NativeScript apps are truly native iOS and Android apps, there are an additional set of system requirements you need to build these apps. Check out [this page on the NativeScript docs](https://docs.nativescript.org/angular/start/general-requirements) for the necessary steps to set up your machine for building iOS and Android apps.

> **NOTE**: The next version of NativeScript, NativeScript 5.0, has some fun changes coming up that will allow you to run apps without any local setup. You can [learn more on GitHub](https://github.com/NativeScript/nativescript-cli/issues/3813).

With the setup out of the way, return to your terminal or command prompt, use `Ctrl` + `C` to stop your `ng serve` command, and next execute `npm run android`. The command will take a minute to run, as under the hoods NativeScript is building a completely native Android app, but when it finishes you’ll see the following screen.

<img src="android-1.png" style="height: 450px;">

If you’re developing on macOS, you can also try running `npm run ios`, which runs through a similar process, but instead builds and runs your app on iOS. When it finishes you’ll see this screen.

<img src="ios-1.png" style="height: 450px;">

Now that you have an idea of how to run your apps on all three platforms, let’s dig into the code behind this app to see what’s going on.

## Looking through the code

Starting at the root of your project, here are the top-level folders you need to know about.

```
Checklist/
├── App_Resources
├── platforms
└── src
```

* The `App_Resources` folder is where NativeScript stores iOS and Android configuration files and image resources, such as your app’s icons and splash screens. Later in your app development, you’ll want to switch your app to your own image assets using the NativeScript CLI’s `tns resources generate` command.
* The `platforms` folder is where NativeScript stores your generated iOS and Android apps; you can think of it as a `dist` folder for your native projects.
* The `src` folder is where your source code lives, and it’s where you’ll be spending 95% of your time.

> **NOTE**: There are a bunch of other configuration files in the root folder, such as an `angular.json` file for Angular CLI customization, a `package.json` file for managing dependencies, and a series of `tsconfig.json` files for configuring TypeScript. When getting started feel it’s best to leave these files alone; when you’re further along you can come back to these files and further customize your project to meet your needs.

Since the `src` folder is where you’ll be spending most of your time, let’s dig into the contents of that folder in more detail.

```
src/
├── app
│   ├── app.component.css
│   ├── app.component.html
│   ├── app.component.tns.html
│   ├── app.component.ts
│   ├── app.module.tns.ts
│   ├── app.module.ts
│   ├── app.routes.ts
│   ├── app.routing.tns.ts
│   ├── app.routing.ts
│   └── barcelona
│       └── ...
├── app.css
├── assets
├── index.html
├── main.tns.ts
├── main.ts
├── package.json
└── styles.css
```

If you’ve built Angular web apps before a lot of this structure will look very familiar. All Angular apps have a `main.ts` file for initialization, an `app.module.ts` file for [module declarations](https://angular.io/guide/ngmodules), a series of `app.routing.ts` files for [setting up routing](https://angular.io/guide/router), and an `app.component.ts` file to use as the [app’s first component](https://angular.io/guide/entry-components).

> **TIP**: If you’re new to Angular and would like a more in-depth introduction to these concepts, check out the [Angular quick-start tutorial](https://angular.io/guide/quickstart). All of the concepts you learn there directly apply to the code-sharing structure in this article.

One concept unique to NativeScript’s code-sharing workflow is the `.tns` naming convention you see on some of your app’s files (for example `app.routing.tns.ts`).

By default, NativeScript schematics uses all files in your project in both your web and mobile apps. In most cases that’s exactly what you want, but sometimes you need to create web- or mobile-specific files, and that’s where the `.tns` extension comes in.

For example take the `app.module.ts` and `app.module.tns.ts` files. When you run your app on the web, the Angular CLI uses your `app.module.ts` file as you’d expect. However, when you run your app on iOS or Android, NativeScript schematics instead grabs and uses your `app.module.tns.ts` file. This convention is a powerful way to split your web and mobile code as necessary, and you’ll use it frequently as you build your own apps using this setup.

Now that you have a bit of background on how your project is structured, let’s build something new.

## Building your web UI

In the starter app, the vast majority of your code is in a `src/app/barcelona` folder, as that’s the code that builds up the player list you saw in your app earlier. In this section you’re going to create a brand-new component for the web, and in the next section you’ll just how easy it is to get that same component working in a native iOS and Android app.

Let’s start by scaffolding some files. To do so, start by using the `cd` command to navigate to your 

`cd /src/app`

Create list folder.

Create...

list.common.ts

```
import { Routes } from '@angular/router';

import { ListComponent } from "./list.component";
import { ListService } from './list.service';

export const COMPONENT_DECLARATIONS: any[] = [
  ListComponent
];

export const PROVIDERS_DECLARATIONS: any[] = [
  ListService
];

export const ROUTES: Routes = [
  { path: 'list', component: ListComponent },
];
```

list.component.css
list.component.html
list.module.ts

```
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { HttpClientModule } from '@angular/common/http';
import { RouterModule } from '@angular/router';

import { ROUTES, COMPONENT_DECLARATIONS, PROVIDERS_DECLARATIONS } from './list.common';

@NgModule({
  imports: [
    CommonModule,
    HttpClientModule,
    RouterModule.forRoot(ROUTES)
  ],
  exports: [
    RouterModule
  ],
  declarations: [
    ...COMPONENT_DECLARATIONS
  ],
  providers: [
    ...PROVIDERS_DECLARATIONS
  ]
})
export class ListModule { }

```

list.service.ts

```
import { Injectable } from '@angular/core';
import { HttpClient } from "@angular/common/http";

@Injectable()
export class ListService {

  constructor(private http: HttpClient) { }

  get() {
    return this.http.get("https://pokeapi.co/api/v2/pokemon/?limit=151");
  }
}

```

Change routing in `app.routes.ts`.

```
import { Routes } from '@angular/router';

export const ROUTES: Routes = [
  { path: '', redirectTo: '/list', pathMatch: 'full' },
];

```




`styles.css`
```
html, body { margin: 0; }
```