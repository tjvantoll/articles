# How to Build a Simple Dialog for Your NativeScript Apps

There are a few different ways to implement dialogs in NativeScript apps. The [NativeScript dialog module](https://docs.nativescript.org/ui/dialogs) lets you show a variety of dialogs using built-in APIs, and is great for simple use cases.

![](https://raw.githubusercontent.com/NativeScript/code-samples/master/screens/dialogs-ios.gif)
_[Try this example in NativeScript Playground](https://play.nativescript.org/?template=play-ng&id=dWQhV7&v=5)_

On the other end of the spectrum, you can also create dialogs that are completely modal pages, complete with native transitions. These are great when you want to have full control over how the dialogs look and work.

-- show it --

In my experience though, sometime you want something in between these two options. That is, you want a simple dialog that you can style... without going through the hassle of creating an entire page. Basically you want something that looks like this.

<img src="dialog.gif" style="height: 450px;">

In this article I’m going to walk you through how to create a simple dialog like the one above. I’ll be using Angular for my explanations, but the techniques are roughly the same whether you’re using Angular, Vue.js, or NativeScript Core.

> **TIP**: You can view the final state of this example in NativeScript Playground. Here’s the code for Angular, the code for Vue.js, and the code for NativeScript Core.

## Building the markup

Here is what the markup to make this simple dialog looks like at a high level.

``` XML
<GridLayout class="page">
  <GridLayout class="content">
    <StackLayout>
      <!-- Page content goes here -->
    </StackLayout>
  </GridLayout>

  <AbsoluteLayout>
    <StackLayout class="dialog">
      <!-- Dialog content goes here -->
    </StackLayout>
  </AbsoluteLayout>
</GridLayout>
```

To start, you have an outer `<GridLayout>` that contains your entire page. If you’re using Angular this would be the root element of your page component, and if you’re not using Angular, this would be a child of the root `<Page>` element.

Your page has two children, a `<GridLayout>` that will contain the content of your app, and an `<AbsoluteLayout>` that will serve as a container for your dialog. The idea here is that you’ll write your content exactly as you normally would, and show and hide the dialog as necessary in your app. In order to do that let’s write a little bit of code and CSS.

## Showing and hiding the dialog

In your code you’ll need to create a property that tracks whether the dialog is open or not, as well as a few methods for manipulating the dialog’s state. If you’re using Angular, that code will look something like this.

``` TypeScript
import { Component } from "@angular/core";

@Component({
  selector: "Home",
  moduleId: module.id,
  templateUrl: "./home.component.html",
  styleUrls: ['./home.component.css']
})
export class HomeComponent {
  dialogOpen = false;

  showDialog() {
    this.dialogOpen = true;
  }

  closeDialog() {
    this.dialogOpen = false;
  }
}
```

The `dialogOpen` property, as its name implies, tracks whether the dialog is currently open or not. You set it to a default value of `false`, as you usually don’t want the dialog to show when your page loads.

Now that you have the property in place, your next step is to use that property in your markup. One way to do so is with the following markup.

``` XML
<GridLayout class="page" [class.dialogOpen]="dialogOpen">
  <GridLayout class="content">
    <StackLayout>
      <Button class="btn btn-primary" text="Show Dialog" (tap)="showDialog()"></Button>
    </StackLayout>
  </GridLayout>

  <AbsoluteLayout>
    <StackLayout class="dialog">
      <Label textWrap="true" text="Are you sure you want to continue?"></Label>
      <Button class="btn btn-primary" text="Yes"></Button>
      <Button class="btn" text="No" (tap)="closeDialog()"></Button>
    </StackLayout>
  </AbsoluteLayout>
</GridLayout>
```

There are a few changes in this markup to use your new property. First, you add two `tap` event handlers, one to a button in your main content to show the dialog, and another in the dialog to close the dialog.

Second, you use Angular’s `[]` syntax to conditionally apply a `dialogOpen` CSS class name to your main page element. This class name will serve as the hook you need to make your dialog behave like a dialog. To see how it’ll all work let’s look at the CSS you’ll need to make all this come together.

## Adding styling

Believe it or not you already have all the markup and code you need to make this example work, as the real magic of this example happens in CSS. Here’s the minimum CSS code you’ll need.

``` CSS
.dialogOpen .content {
  opacity: 0.2;
}
.dialog {
  opacity: 0;
  border-width: 1 0 1 0;
  border-color: black;
  width: 100%;
  margin-top: 100;
}
.dialogOpen .dialog {
  opacity: 1;
}
```

By default the dialog element is set to an `opacity` of `0`, which hides it from the user.

But when the `dialogOpen` class gets applied, the `.dialogOpen .dialog` selector now applies, and the dialog’s `opacity` is set to `1`, which shows the dialog to the user. Additionally, the `.dialogOpen .content` now applies and changes the `opacity` of the main content to `0.2`, which gives it a bit of a dim appearance so the user’s attention gets focused on the dialog itself.

When you put this all together you should now have a dialog that looks a little something like this.

--- gif ---

## Further improvements

There are a few different ways you can improve on this simple design. First, you can toss in a little animation to give the dialog a nice fade-in effect. That code looks a little something like this.

``` CSS
@keyframes show {
  from { opacity: 0; }
  to { opacity: 1; }
}

.dialogOpen .content {
  opacity: 0.2;
}
.dialogOpen .dialog {
  animation-name: show;
  animation-duration: 0.3s;
  animation-fill-mode: forwards;
}
.dialog {
  opacity: 0;
  border-width: 1 0 1 0;
  border-color: black;
  width: 100%;
  margin-top: 100;
}
```

Now, when you open your dialog you’ll see a little face-in effect that looks like this.

--- gif ---

One downside of using the technique described in this article is that your dialogs are not modal. That is, the user is still able to access content that lives underneath the dialog when the dialog displays. To work around this, you will need to guard other actions the user can take in your UI.

For example, suppose you had an `<ActionItem>` in your app that performed a sharing action. Something like this.

``` XML
<ActionItem text="Share" (tap)="share()"></ActionItem>
```

``` TypeScript
import { Component } from "@angular/core";

@Component({
  ...
})
export class HomeComponent {
  dialogOpen = false;

  share() {
    // Sharing code here
  }

  showDialog() { ... }
  closeDialog() { ... }
}
```

To prevent the sharing action from happening when your dialog is open, you could add a simple `if` check like this.

``` TypeScript
import { Component } from "@angular/core";

@Component({
  ...
})
export class HomeComponent {
  dialogOpen = false;

  share() {
    if (this.dialogOpen) {
      return;
    }
    // Sharing code here
  }

  showDialog() { ... }
  closeDialog() { ... }
}
```

Another approach you could take is hiding the dialog when the user taps outside of the dialog. You can do that by adding a `tap` event handler to your content that closes the dialog.

``` XML
<GridLayout class="page">
  <GridLayout class="content" (tap)="closeDialog()">
    <StackLayout>
      <!-- Page content goes here -->
    </StackLayout>
  </GridLayout>

  <AbsoluteLayout>
    <StackLayout class="dialog">
      <!-- Dialog content goes here -->
    </StackLayout>
  </AbsoluteLayout>
</GridLayout>
```

Ultimately how you choose to configure is up to you based on the needs of you app. Feel free to copy this approach verbatim, or to customize this structure to meet your needs.

A polished version of this sample is available for Angular, Vue.js, and NativeScript Core using the links below. Feel free to use them, and if you come up with any fun customizations, please list them in the comments below.

* [Final code for Angular]()
* [Final code for Vue.js]()
* [Final code for NativeScript Core]()