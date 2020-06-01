# Let’s Build a Financial Dashboard With React

The great thing about building financial apps is that there’s very little data, and therefore very little complexity.

...

Ok fine, financial apps are hard. They typically they deal with a ton of data, and displaying that data in a meaningful way is critical to making your users happy and productive.

In this article you’ll build a sample financial dashboard in three steps. First, you’ll create the dashboard’s layout, and learn a bit about CSS grid syntax in the process. Next, you’ll add UI components from [KendoReact](https://www.telerik.com/kendo-react-ui/), our UI library that makes it easy to display data in charts, grids, and more. And finally, you’ll learn how to customize you dashboard, including how to handling theming, and how to tweak the KendoReact components to meet your requirements.

When you’re done you’ll have a dashboard that looks like this.

![](dashboard.png)

Let’s get started!

> **OPTIONAL:** If you want to code along with this article, you’ll need to clone [this article’s GitHub repository](https://github.com/tjvantoll/financial-dashboard) and switch to its `start` branch. You can do that by running the following set of commands in your terminal or command prompt.
> ```
> git clone https://github.com/tjvantoll/financial-dashboard.git
> cd financial-dashboard
> git checkout start
> ```

## Step 1: Building out your initial layout

Like most large software development projects, doing a bit of planning before jumping straight into coding your dashboard is a good idea. In this section we’ll start by looking at a quick wireframe of our dashboard’s layout, and then look at how to scaffold out that layout  with CSS.

### Building a wireframe

A wireframe is a visual representation of what your final app will look like. It’s important to have some representation of your app before you start coding, but the wireframe doesn’t to show every last feature, and it doesn’t need to be professionally designed.

As an example, here’s the sketch I created in [Balsamiq](https://balsamiq.com/) for this article’s dashboard.

![](wireframe.png)

From this wireframe you can see our sample has a header and four distinct panels, which I’ve labeled in the image below.

![](wireframe-annotated.png)

The main purpose of a wireframe is to give you a rough idea of how to lay out elements in your app before you start coding. For example, because I know my app will have four panels, I created four boilerplate components in the sample app’s starting code. You can view them in the `src/panels` folder.

![](panels-files.png)

Later in this article we’ll start filing out those components with UI code, but before that lets scaffold out this app’s layout with CSS.

### Implementing your layout with CSS

There are a variety of ways you can layout an app with CSS nowadays. One of the most common approaches is to use a framework like [Bootstrap](https://getbootstrap.com/), which provides a variety of class names to help divide your UI into a series of rows and columns.

For example, you could create a Bootstrap layout with three columns using the following markup.

``` HTML
<div class="container">
  <div class="row">
    <div class="col-sm">
      One of three columns
    </div>
    <div class="col-sm">
      One of three columns
    </div>
    <div class="col-sm">
      One of three columns
    </div>
  </div>
</div>
```

Although this is a reasonable way of implementing a layout, personally I’m not a huge fan of this approach in large apps like dashboards—and that’s because real-world apps tend to get complicated really fast, and before you know it, your markup goes from being fairly semantic, to a complicated mess of class names that are difficult to decipher.

![](bootstrap-mess.png)

Because of this I tend to prefer to layout my dashboards using CSS alone. To see what this looks like, take a look at the sample’s `src/Dashboard.tsx` file, which contains the markup of the sample’s four panels.

``` HTML
<div className="panels">
  <div className="panel-info">
    <InfoPanel />
  </div>
  <div className="panel-allocation">
    <AllocationPanel />
  </div>
  <div className="panel-balance">
    <PerformancePanel />
  </div>
  <div className="panel-positions">
    <PositionsPanel />
  </div>
</div>
```

Our task is to take this markup, and to make it look like our wireframe, which as a reminder looks like this.

![](wireframe.png)

To do that, open your `src/styles/_layout.scss` file, and replace its contents with the following code.

``` SCSS
.panels > div {
  // Add a black border around each panel for debugging
  border: 1px solid black;
}

.panels {
  display: grid;
  grid-template-columns: 225px auto auto;
  grid-template-rows: auto auto;
}
.panel-info {
  grid-row: span 2;
}
.panel-positions {
  grid-column: span 2;
}
```

After adding this code you’ll want to head to your terminal or command prompt and run `npm run start`, which will start up your React app in your browser. When it’s done, you should see a UI that looks like this.

![](starting-layout.png)

The syntax we’re using here is called [CSS grid layout](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout), and it’s [shockingly well supported by web browsers](https://caniuse.com/#feat=css-grid) today.

> **TIP**: If you’re new to CSS grid, check out [this video intro on YouTube](https://www.youtube.com/watch?v=0-DY8J_skZ0). And when you’ve got the basics down, bookmark CSS Tricks’ [_A Complete Guide to Grid_](https://css-tricks.com/snippets/css/complete-guide-grid/), as it’s an excellent reference when you inevitably need to look up the various grid CSS properties.

What makes CSS grid appealing is its brevity. Instead of cluttering up you markup with a myriad of class names, you get a powerful way of dividing your UI into rows and columns.

CSS grid also makes it easy to make your dashboards responsive. To see this in action, add the following bit of CSS to your `src/styles/_layout.scss` file.

``` CSS
@media (max-width: 750px) {
  .panels {
    grid-template-columns: 225px auto;
    grid-template-rows: auto auto auto;
  }
  .panel-positions {
    grid-column: span 2;
  }
}

@media (max-width: 500px) {
  .panels {
    grid-template-columns: auto;
  }
  .panel-positions {
    grid-column: span 1;
  }
}
```

This code reorients your grid as the user’s screen gets smaller. For example, at 750px it changes the `.panels` container from using three columns (`grid-template-columns: 225px auto auto`), to two (`grid-template-columns: 225px auto`). And then at 500px it reduces that same container to using a single column (`grid-template-columns: auto`), so that all of app’s panels stack on top of each other.

You can see what this looks like in the gif below.

![](media-queries.gif)

And with that—we’re done! CSS grid really does make it that easy to configure a dashboard layout, all without cluttering up your markup. Now that you have the layout in place, let’s look at adding in some UI components.

## Step 2: Adding UI components

Perhaps the most challenging part of building a dashboard is the finding high-quality UI components to display your data. The React world is big, so luckily there are tons of components out there, but dashboards often require a wide variety of controls, and making a disparate set of components that you’ve found around the web work together can be a real challenge.

That’s where KendoReact comes in. 

## Step 3: Customizing your UI

## Wrapping up