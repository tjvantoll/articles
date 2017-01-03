# Let’s Learn NativeScript Layouts by Implementing a Design

Positioning UI elements is one of the hardest things to learn in any software environment. On the web you need to learn the difference between non-intuitive display mechanisms like `block`, `inline-block`, `inline`, and `flex`; on iOS you pretend to understand ideas like [auto layout](https://developer.apple.com/library/content/documentation/UserExperience/Conceptual/AutolayoutPG/) and layout constraints; and on Android you write a bunch of confusing XML and hope for the best.

In [NativeScript](https://www.nativescript.org/) we have the interesting challenge of coming up with a layout mechanism that can translate to native iOS and Android code.


A few fun layout changes shipped in [NativeScript 2.4](https://www.nativescript.org/blog/nativescript-2.4-announcement), most notably [flexbox](https://www.nativescript.org/blog/a-quick-introduction-to-flexbox-in-nativescript) and the ability to apply [per-side CSS borders](https://www.nativescript.org/blog/per-side-borders-in-nativescript-css). In this article we’ll look at how to use some of these features by implementing a few design specifications in a NativeScript app. You’ll learn about the many different ways you can use NativeScript’s layout mechanisms, some fun ways to leverage borders, and how to put all of this to use in real apps. Let’s get started.

## Implementing a first design

Suppose you were tasked with implementing the following design.

<img src="initial-border-design.png" style="border: 1px solid black; max-height: 450px;">

The first and easiest task when implementing a NativeScript design is choosing which UI components to use. On the web these components are tags like `<input>`, `<select>` and `<div>`, and in NativeScript you’ll need to use tags like `<TextField>`, `<Slider>` and `<ActivityIndicator>`. Although there are [many NativeScript UI components](https://docs.nativescript.org/ui/components), there are several common ones you’ll use to do most of your application development.

In the case of this design you’ll only need two—`<Label>`, a tag for displaying text, and `<Image>`, a tag for displaying images. Once you know what UI components to use your next step is to figure out how to align those components on the screen, and that’s where things get a little trickier.

### NativeScript Layouts

On the web layout is done by applying a handful of CSS properties like `display` to `<div>`s and calling it a day. In NativeScript, there is no HTML and there is no DOM—so those same mechanisms for aligning UI components is not available.

Instead, NativeScript provides a series of layout components that you add directly to your markup. These components handle the tricky business of positioining in a new that works both for native iOS and native Android apps, all without you having to know the messy details of what’s going on under the hood.

The simplest of the NativeScript layouts is the `<StackLayout>`, as it’s somewhat similar to a `<div>` that you’d use on the web. Any UI components you add to a `<StackLayout>` are stacked—vertically by default, and horizontally if you apply a `orientation="horizontal"` attribute on the component.

For instance, as a first stab at our design, let’s start by getting everything on the screen.

``` XML
<Page>
  <ScrollView>
    <StackLayout>
      <Label text="WONDERS OF ITALY" textWrap="true"></Label>
      <Image src="https://i.imgur.com/Dx6zCYo.jpg"></Image>

      <Image src="https://i.imgur.com/oIAWen4h.jpg"></Image>
      <Label text="HIGHLIGHTS OF SOUTH AFRICA" textWrap="true"></Label>

      <Label text="IMPERIAL CHINA" textWrap="true"></Label>
      <Image src="https://i.imgur.com/swUkmIy.jpg"></Image>
    </StackLayout>
  </ScrollView>
</Page>
```

> **NOTE**: If you’re using NativeScript with Angular 2 the outer `<Page>` tag is unnecessary, as it’s assumed in NativeScript Angular templates. Copy only the contents of `<Page>` in these examples and you’ll be able to follow along.

This isn’t the world’s 
