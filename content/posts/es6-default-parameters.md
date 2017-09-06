---
title: "Accessing Earlier Parameters in ES6 Default Parameters"
date: 2017-09-05T20:19:17-04:00
categories: ["javascript"]
---


I noticed something I hadn't seen before while reading [Functional Light JS](https://github.com/getify/Functional-Light-JS).

It was this function definition in Chapter 3:

```
function curry(fn, arity = fn.length) {
```

The second argument `arity` has a default value that checks the length property of the first parameter. This is a something I didn't know you could do with ES6 default parameters.

As described in the [Mozilla page](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters), default parameters can access any parameter already encountered. So, for example, you could so something like this:

```
function calculateFunMoney(income, expenses, savings = income * .05) {
    return income - expenses - savings;
}

calculateFunMoney(1000, 600); // 350
calculateFunMoney(1000, 600, 250); // 150  
```

Here you could assume you want to save 5% of your income, or let the caller decide exactly how much to save instead. There are probably much better examples, but that shows how it works.

One way to start applying this in your code is to look for functions with a possibly undefined parameter that you give some default value in the body based on the other parameters. If the assignment is simple enough, you could easily inline that as the default parameter!
