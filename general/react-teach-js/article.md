# How React Taught Me JavaScript

Having children is a great way to discover everything you’ve pretended to know all your life. It’s amazing how questions like, “Where do peanuts come from?”, or “Why is water blue and snow white?”, or “Why does the moon glow?”, can make you re-evaluate whether you’re actually an adult that knows things.

In much the same way, learning React has exposed how much I’ve pretended to understand new JavaScript.

For a bit of context, I’ve used JavaScript for well over 15 years, and have deployed JavaScript applications on multiple platforms for multiple organizations. I was a member of the jQuery UI team for two years and a member of the NativeScript team for four. Despite this, React’s non-trivial usage of modern JavaScript features forced me to learn new things about a language I’ve been using for years.

In this article I want to share a few things I’ve picked up while learning React. Hopefully hearing my experiences can help you learn (and use!) some of these features as well—especially if you’re learning React for the first time.

## Feature #1: Destructuring

Before trying React I had heard the term destructuring, and had even seen demos of it in talks and such, but I never understood why I should care. And then I saw my [very first example of React hooks](https://reactjs.org/docs/hooks-intro.html), which looks like this.

``` JavaScript
import React, { useState } from 'react';

function Example() {
  // This is destructuring! 🔽
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

For our purposes only worry about the line of code below, as it’s the one that leverages destructuring.

``` JavaScript
const [count, setCount] = useState(0);
```

`React.useState()` is a weird API (more on that in a minute), but because `useState()` is a common API in React codebases it’s important to understand what’s happening here.

React’s `useState()` method returns an array with two entries, and `const [count, setCount] = useState(0)` _destructures_ those two entries into two constants, `count`, and `setCount`, respectively.

This confused me at first, so I’ll try stating this another way. In essence, the above line of code is a nicer way of manually creating local constants from an array, which you might have traditionally done like this.

``` JavaScript
// This is the same...
const results = useState(0);
const count = results[0];
const setCount = results[1];

// ...as this
const [count, setCount] = useState(0);
```

Personally I think `React.useState` isn’t the best example of destructuring, just because the `useState` method is such an oddly designed API. (I’m genuinely curious why it makes sense to have a method that returns an array with two entries.)

To me, a far better example of destructuring is a function that takes an object as an argument. For example, suppose you have the following function that processes a user.

``` JavaScript
function processUser(user) {
  console.log(user.name);
  console.log(user.address);
}
```

With destructuring, you can place the object properties you expect to receive directly in your function definition, as such.

``` JavaScript
function processUser({ name, address }) {
  console.log(name);
  console.log(address);
}
```

In this case, destructuring cleans up your code a bit, and also makes your function easier for other developers to consume, as you’re listing the object properties you expect in your function definition.

**Summary**: Destructuring doesn’t fundamentally change the way you write JavaScript, but can be a handy way to keep your code concise—especially in areas of your codebase where you need to pass around objects a lot.

## Feature #2: Computed property names

Two weeks ago I had no idea computed property names were a JavaScript thing, and had never seen an example of them in real-world code. Then, on the [React forms documentation](https://reactjs.org/docs/forms.html) I saw this code.

``` JavaScript
handleInputChange(event) {
  const target = event.target;
  const value = target.type === 'checkbox' ? target.checked : target.value;
  const name = target.name;

  this.setState({
    // This is the computed property name! 🔽
    [name]: value
  });
}
```

As with the previous example, let’s only focus on the bit using the feature we’re interested in, which in this case is the following use of a computed property.

``` JavaScript
this.setState({
  [name]: value
});
```

This code passes an object to React’s `setState()` method with a single name-value pair. The important bit here (and where computed properties come into play), is that the property is dynamically created based on the `name` variable. This all might make more sense if you look at the code below, which shows how to accomplish the same task with and without computed property names.

``` JavaScript
// This is the same...
this.setState({
  [name]: value
});

// ... as this
var myObject = {};
myObject[name] = value;
this.setState(myObject);
```

As I mentioned earlier, I hadn’t seen this syntax before learning React, and I think that’s because it’s a fairly uncommon thing to need to do. In fact, I’m really struggling to think of a non-React scenario where I’d ever use this syntax. (Maybe you could tell me in the comments?)

That being said, it’s important for React developers to understand this syntax because it comes up a lot when dealing with state. React’s `setState` method accepts a partial object—aka an object that contains a portion of your state, which React takes care of merging with the rest of your state under the hood—and in that scenario it’s fairly common to need to dynamically create an object with a dynamic key.

**Summary**: You can dynamically create property names by placing `[]` around a property name when creating object literals. You probably won’t need to use it unless you’re working with state in React.

## Feature #3: Spread syntax

Spread syntax is the official name for JavaScript’s `...` operator. Interestingly enough I was somewhat familiar with `...` only because I knew of it from Java (yes, Java), where it’s known as Variable Arguments, or varargs, and looks a little something like this.

``` Java
public class MyClass {
  public void message(String foo, String bar, String ...bang) {
    System.out.print(foo);
    System.out.print(bar);
    for (String myString : bang) {
      System.out.print(myString);
    }
  }
}

// This prints "abcde". Isn’t Java fun?
new MyClass().message("a", "b", "c", "d", "e");
```

As you might expect, JavaScript’s implementation of this feature is similar to Java’s but better. First of all, you can replicate the preceding Java code using the JavaScript code below.

``` JavaScript
function message(a, b, ...c) {
  console.log(a + b + c.join(""));
}

// This prints "abcde".
message("a", "b", "c", "d", "e");
```

Here, `c` is known as a [rest parameter](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters), and it contains an array of all arguments the user provides beyond the formally defined parameters, so in this case `["c", "d", "e"]`. Rest parameters are true JavaScript arrays, meaning all JavaScript array functions are available on them, and it’s the reason why `c.join()` works in the above example.

All that being said, I’ve never used variable arguments in Java, and I’ll probably never use rest parameters in JavaScript. In my experience, designing a function that takes a variable number of arguments is a great way to ensure your coworkers dislike you a non-variable amount.

But JavaScript’s spread syntax can be used for more than rest parameters. The most useful, in my opinion, is using spread syntax in object literals. For example, consider the following [example from MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax#Spread_in_object_literals), showing how to use the spread syntax to clone and merge objects.

``` JavaScript
var obj1 = { foo: 'bar', x: 42 };
var obj2 = { foo: 'baz', y: 13 };

var clonedObj = { ...obj1 };
// Object { foo: "bar", x: 42 }

var mergedObj = { ...obj1, ...obj2 };
// Object { foo: "baz", x: 42, y: 13 }
```

This is about the only pragmatic example of the spread operator I’ve seen, as cloning and merging objects is a common task in your average JavaScript app.

**Summary**: The `...` operator is known as spread syntax in JavaScript. It can be used in function definitions or when managing objects or arrays, and is especially useful when merging objects.

## Feature #4: Short-circuit evaluation

Let’s start this section off with a question: would you write code that looks like this?

``` JavaScript
const isLoading = determineIfLoading();
if (isLoading && console.log("Your application is loading"));
```

I wouldn’t, and you probably wouldn’t either. But this technique is something that virtually every React app uses in its `render()` method. (It’s even [recommended in the official React documentation](https://reactjs.org/docs/conditional-rendering.html).)

The approach is called conditional rendering, and it works because JavaScript does something known as short-circuit evaluation. To explain what short-circuit evaluation is let’s return to the above `if` statement.

``` JavaScript
if (isLoading && console.log("Your application is loading"));
```

This is a JavaScript expression with two operands—`isLoading` and `console.log("...")`. If the first operand in this expression is `true`, the JavaScript interpreter will proceed to the second operand, in this case the `console.log` statement, and execute it. But, and this is where short-circuit evaluation comes into play, if the first operand is `false`, the interpreter will skip (or short circuit) the second operand, and will never execute the `console.log` statement.

At the end of the day what you’re consolidating a more traditional way of writing an `if` statement. Something like this, which does the same thing.

``` JavaScript
const isLoading = determineIfLoading();
if (isLoading) {
  console.log("Your application is loading");
}
```

I consider the short-circuit approach to be hacky in most code, as it’s usually worth making code more verbose to make it more readable.

However, I do find how React uses short-circuit evaluation to be rather elegant. For example, here’s an example of using short-circuit evaluation in a React `render()` method to render some UI.

``` JavaScript
return (
  <div class="page">
    { this.state.isLoading && <div>Loading...</div> }
    <div class="everything-else">...</div>
  </div>
);
```

Here, React uses the `this.state.isLoading` variable to conditionally determine render some UI, which in this case is `<div>Loading...</div>`.

This code works because of short-circuit evaluation. Specifically, the `<div>Loading...</div>` only gets rendered when `this.state.isLoading` is `true`. And I have to admit, this code is surprisingly clean, especially if you compare this to a functionally identical implementation using a more traditional `if` statement, which looks like this.

``` JavaScript
var loadingContent = this.state.isLoading ? 
  <div>Loading...</div> : "";

return (
  <div class="page">
    {loadingContent}
    <div class="everything-else">...</div>
  </div>
);
```

In almost all situations I favor verbose-yet-readable code over concise-yet-illegible code, but I have to say in this specific situation short-circuit evaluation really does clean up the component logic.

Plus, because the `{conditional && <Component>}` syntax is used so consistently in React documentation and tutorials, the approach becomes increasingly readable once you understand what it’s doing, and once you start to use the syntax yourself.

**Summary**: Understanding how short-circuit evaluation works is important for understanding how JavaScript works, and can be useful in writing clean React `render()` methods.

## Wrapping up

Between destructing, computed property names, spread syntax and short-circuit evaluation, learning React has forced me to learn new things about a language I’ve been using for years.

That’s one reason why it’s fun to experiment with new languages and frameworks periodically, as it can open your mind to new ways of thinking, and new ways of tackling coding problems that you might not have thought of before.

So if you haven’t already, [give React a shot](https://reactjs.org/), even if it’s just to build a silly app to see what you think. And if you do, try out [KendoReact](https://www.telerik.com/kendo-react-ui/), our premium set of UI components that make building rich React components super easy 🙂
