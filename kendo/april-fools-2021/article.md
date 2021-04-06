# A Surprise Release of KendoReact

Today we have a monumental new update of [KendoReact](https://www.telerik.com/kendo-react-ui/) to share. There’s a lot to cover, so let’s dive right in.

## Scheduler updates

One of the most popular KendoReact components is our [Scheduler](https://www.telerik.com/kendo-react-ui/components/scheduler/), which allows you to build an Outlook-like or Google-Calendar-like calendar experience in your browser.

And today we’re announcing a new feature that’s sure to make your scheduling experience a lot more interesting—randomization.

``` tsx
<Scheduler
  ...
  enableRandomize={true}>
```

Try using the Randomize button in the demo below to see this exciting feature in action. After that, try the new prop in your company’s HR system—and let us know how it goes!

<iframe
  width="100%"
  height="750"
  src="https://stackblitz.com/edit/react-neq8uv?embed=1&file=app/main.jsx&hideExplorer=1&view=preview"></iframe>

## Gantt updates

Our [Gantt component](https://www.telerik.com/kendo-react-ui/components/gantt/) can bounce now. You’re welcome!

``` jsx
<Gantt
  ...
  bounce={true}
  bounceSpeed={10}>
```

<iframe
  src="https://stackblitz.com/edit/react-qiv86i?embed=1&file=app/main.jsx&hideExplorer=1&view=preview"
  height="700"
  width="100%"
 ></iframe>

## Grid updates

The biggest updates in this release are to our [world-class Data Grid](https://www.telerik.com/kendo-react-ui/components/grid/). Our Grid does so much that many of you complained that you were constrained by the nature of two-dimensional space—well no more.

```jsx
<Grid
  ...
  flipped={true}
  back={<div>You can put stuff here!</div>}>
```

The demo below shows how to use a new `flipped` prop to place a Grid and a Chart in the same space. Your UX team will love it!

<iframe
  src="https://stackblitz.com/edit/react-xu1hjg?embed=1&file=app/main.jsx&hideExplorer=1&view=preview"
  height="700"
  width="100%">
  </iframe>

And finally, because our Grid is so majestic, we felt it was about time to give it the entrance it deserves—which is why we’re announcing a new mandatory `grandEntrance` prop.

``` jsx
<Grid
  ...
  {/* No extra code necessary—the animation is mandatory! */}>
```

To see the grand entrance in all its glory, try the demo below (with your volume turned up).

<iframe
  src="https://stackblitz.com/edit/react-1w1zc9-fxn9uz?embed=1&file=app/main.jsx&hideExplorer=1&view=preview"
  height="700"
  width="100%">
  </iframe>

> **NOTE**: A `skipIntro` prop is coming in our next release.

That’s it for now, but feel free to share ideas for our next release in the comments. And if you want to build fun things like this yourself, check out all of the [90+ KendoReact UI components](https://www.telerik.com/kendo-react-ui/components/).
