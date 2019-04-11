---
layout: post
title: "Annotations to Understanding ECMAScript 6"
categories: Annotations
tags: javascript ecmascript zakas
---

This post is a set of annotations to [*Understanding ECMAScript 6*](https://www.amazon.com/dp/1593277571) (2016) written by Nicholas C. Zakas.

{% include toc.html %}

## External Links

- [Standard ECMA-262 ECMAScript® Language Specification](https://www.ecma-international.org/publications/standards/Ecma-262.htm)

## Forword

The author of this forword is [Dan Abramov](https://twitter.com/dan_abramov) -- [React](https://reactjs.org/) core team member and creator of [Redux](https://redux.js.org/).

> I set my prejudices aside, opened MDN and StackOverflow, and learned JavaScript in depth for the first time.

He didn't read books. Maybe a good method to get knowledge.

## Chapter 1. Block Bindings

### Block-Level Declarations

#### The Temporal Dead Zone

> When a JavaScript engine looks through an upcoming block and finds a variable declaration, it either hoists the declaration to the top of the function or global scope (for `var`) or places the declaration in the TDZ (for `let` and `const`). Any attempt to access a variable in the TDZ results in a runtime error. That variable is only removed from the TDZ, and therefore is safe to use, once execution flows to the variable declaration.

```javascript
if (condition) {    
  console.log(typeof value);  // ReferenceError: value is not defined  
  let value = "blue";
}
```

```javascript
if (condition) {    
  console.log(typeof value);  // undefined    
  var value = "blue";
}
```

```javascript
console.log(typeof value);    // undefined
if (condition) {  
  let value = "blue";
}
```

In his post [*Why is there a “temporal dead zone” in ES6?*](http://2ality.com/2015/10/why-tdz.html), Axel Rauschmayer explained what is the meaning of "temporal dead zone" and why we need it?

> The time span when that happens, between the creation of a variable’s binding and its declaration, is called the temporal dead zone.
> 
> -- Axel Rauschmayer

### Emerging Best Practices for Block Bindings

> However, as more developers migrated to ECMAScript 6, an alternate approach gained popularity: use `const` by default, and only use `let` when you know a variable’s value needs to change. The rationale is that most variables should not change their value after initialization because unexpected value changes are a source of bugs. This idea has a significant amount of traction and is worth exploring in your code as you adopt ECMAScript 6.

If in the beginning, JavaScript had support block-level scope, there won't be a trouble of choosing `var` or `let`.