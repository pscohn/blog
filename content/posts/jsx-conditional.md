---
title: "A Reminder on JSX Conditionals"
date: 2017-08-14T23:02:58-04:00
categories: ["react"]
---

I've always defaulted to ternary expressions when trying to conditionally render something in JSX. Something like so:

```
const Foo = ({ shouldRenderBar }) => (
  <div>
    {shouldRenderBar ? <Bar /> : null}
  </div>
);
```

But I always forget there's a slightly cleaner way to do it, something the [React Docs](https://facebook.github.io/react/docs/jsx-in-depth.html#booleans-null-and-undefined-are-ignored) suggest:

```
const Foo = ({ shouldRenderBar }) => (
  <div>
    {shouldRenderBar && <Bar />}
  </div>
);
```

Since in this case we're only deciding whether to render something or not, we can use a simple `&&` conditional to check for truthy values and return the last one. A ternary is still useful if deciding between two components to render, but here the logical [AND](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_Operators) is enough.

As the docs mention, you should make sure that the expression uses only `true` or `false` values before your component, since it will render a falsy value like `0`. You might expect this to render nothing since a normal Javascript conditional using `0` would evaluate to `false`, but in this case it renders the `0`:

```
const Foo = ({ shouldRenderBar }) => (
  <div>
    {0 && <Bar />}
  </div>
);

// renders `<div>0</div>`
```

Now I should be able to remember to do this in my own code!

[Here is a fiddle](https://jsfiddle.net/6vrc30kf/1/) you can fiddle with.
