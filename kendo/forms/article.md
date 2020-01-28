# How to Build Forms in React the Easy Way

Forms are hard, regardless of the framework or libraries you use to create them. But in React forms are especially tricky, as the [official React forms documentation](https://reactjs.org/docs/forms.html) is brief, and doesn’t discuss topics real-world forms always need, like form validation.

In this article you’ll learn how to build React forms the easy way using the [newly released](https://www.telerik.com/blogs/whats-new-kendoreact-r1-2020) [KendoReact Form component](https://www.telerik.com/kendo-react-ui/components/form/). You’ll learn how to simplify your form’s state management, how to integrate with custom components like date pickers and drop-down lists, and how to implement robust form validation.

Let’s get started.

## Our demo form

In today’s demo we’ll look at a few different ways to implement the sign-up form below.

![](form.png)

To show some of the challenges with building forms in React today, let’s start by looking at an implementation of this form with no additional helper libraries. The code to implement this is below.

``` JSX
import React, { Component } from "react";
import countries from "./countries";

export default function App() {
  const [email, setEmail] = React.useState("");
  const [password, setPassword] = React.useState("");
  const [country, setCountry] = React.useState("");
  const [acceptedTerms, setAcceptedTerms] = React.useState(false);

  const handleSubmit = (event) => {
    console.log(`
      Email: ${email}
      Password: ${password}
      Country: ${country}
      Accepted Terms: ${acceptedTerms}
    `);
    
    event.preventDefault();
  }

  return (
    <form onSubmit={handleSubmit}>
      <h1>Create Account</h1>

      <label>
        Email:
        <input
          name="email"
          type="email"
          value={email}
          onChange={e => setEmail(e.target.value)}
          required />
      </label>
      
      <label>
        Password:
        <input
          name="password"
          type="password"
          value={password}
          onChange={e => setPassword(e.target.value)}
          required />
      </label>

      <label>
        Country:
        <select
          name="country"
          value={country}
          onChange={e => setCountry(e.target.value)}
          required>
          <option key=""></option>
          {countries.map(country => (
            <option key={country}>{country}</option>
          ))}
        </select>
      </label>

      <label>
        <input
          name="acceptedTerms"
          type="checkbox"
          onChange={e => setAcceptedTerms(e.target.value)}
          required />
        I accept the terms of service
      </label>

      <button>Submit</button>
    </form>
  );
}
```

> **TIP**: You can play with a live version of this form on StackBlitz [here](https://stackblitz.com/edit/react-lknyzq?embed=1&file=App.js).

The first thing to note here is just how much code it takes to track the state of this form’s fields. For example, to track the state of the email address, this example uses a hook.

``` JavaScript
const [email, setEmail] = React.useState("");
```

And then a `value` attribute and `onChange` attribute on the email’s `<input>` to ensure the email remains up-to-date as the user interacts with the form.

```
<input
  name="email"
  type="email"
  value={email}
  onChange={e => setEmail(e.target.value)}
  required />
```

Every field requires the same chunks of code, which can easily get verbose as your forms get more complex. This code is also repetitive, making it difficult to refactor your approach in the future.

And this sign-up form is purposefully a bit simple in an attempt to make this article easy to follow. Most real-world forms have far more fields and far more business logic, and as complexity rises as does the importance of reducing the amount of code you need to write and maintain.

In order to clean up our example form’s logic, let’s look at how to refactor it to use the KendoReact Form component.

## Improving state management

The [KendoReact Form](https://www.telerik.com/kendo-react-ui/components/form/) is a small (5KB minified and gzipped) and fast package for state management with zero dependencies.

You can install the package into your own app from npm.

```
npm install --save @progress/kendo-react-form
```

The package contains two components, Form and Field. The basic idea is you wrap your HTML `<form>` with the Form component, and then use one Field component for each field in your form. For our example form this basic structure looks like this.

``` HTML
<Form ...>
  <form>
    <Field name="email" />
    <Field name="password" />
    ...

    <button>Submit</button>
  </form>
</Form>
```

https://stackblitz.com/edit/react-aj3gtp?file=index.js


- Implement the KendoReact Form and show how it cleans up the form code.

## Form validation

- Implement form validation using the Form component.


## Using custom components

- Add in a handful of KendoReact components—DropDownList, Checkbox, etc.
- Show how to create lightweight custom components and how easy it is to integrate them with the Form.
