---
layout: post
title: "Annotations to High Performance JavaScript by Zakas"
categories: Annotations
tags: javascript
---

Annotations to [*High Performance JavaScript*](https://www.amazon.com/dp/059680279X) by Nicholas C. Zakas (2010).

{% include toc.html %}

## 1. Loading and Execution
### Script Positioning

When a browser meet a `<script>` tag, it will stop the rendering and switch to download and execute the JavaScript code, because the code may dynamically modify the page. If you put scripts at the `<head>`, the page rendering progress may be blocked, so put all scripts as close to the bottom of the `<body>` tag as possible.

### Grouping Scripts
### Nonblocking Scripts
#### Deferred Scripts
#### Dynamic Script Elements
#### XML HttpRequest Script Injection
#### Recommended Nonblocking Pattern

## 2. Data Access
### Managing Scope
#### Scope Chains and Identifier Resolution
#### Identifier Resolution Performance
#### Scope Chain Augmentation
#### Dynamic Scopes
#### Closures, Scope, and Memory
### Object Members
#### Prototypes
#### Prototype Chains
#### Nested Members
#### Caching Object Member Values

## 3. DOM Scripting
### DOM in the Browser World
#### Inherently Slow
### DOM Access and Modification
#### `innerHTML` Versus DOM methods
#### Cloning Nodes
#### HTML Collections
#### Walking the DOM
### Repaints and Reflows
#### When Does a Reflow Happen?
#### Queuing and Flushing Render Tree Changes
#### Minimizing Repaints and Reflows
#### Caching Layout Information
#### Take Elements Out of the Flow for Animations
#### IE and `:hover`
### Event Delegation

## 4. Algorithms and Flow Control
### Loops
#### Types of Loops
#### Loop Performance
#### Function-Based Iteration
### Conditionals
#### `if-else` Versus `switch`
#### Optimizing `if-else`
#### Lookup Tables
### Recursion
#### Call Stack Limits
#### Recursion Patterns
#### Iteration
#### Memoization

## 5. Strings and Regular Expressions
### String Concatenation
#### Plus(`+`) and Plus-Equals(`+=`) Operators
#### Array Joining
#### `String.prototype.concat`
### Regular Expression Optimization
#### How Regular Expressions Work
#### Understanding Backtracking
#### Runaway Backtracking
#### A Note on Benchmarking
#### More Ways to Improve Regular Expression Efficiency
#### When Not to use Regular Expressions
### String Trimming
#### Trimming with Regular Expressions
#### Trimming without Regular Expressions
#### A Hybrid Solution

## 6. Responsive Interfaces
### The Browser UI Thread
#### Browser Limits
#### How Long Is Took Long?
### Yielding with Timers
#### Timer Basics
#### Timer Precision
#### Array Processing with Timers
#### Splitting Up Tasks
#### Timed Code
#### Timers and Performance
### Web Workers
#### Worker Environment
#### Worker Communication
#### Loading External Files
#### Practical Uses

## 7. Ajax
### Data Transmission
#### Requesting Data
#### Sending Data
### Data Formats
#### XML
#### JSON
#### HTML
#### Custom Formatting
#### Data Format Conclusions
### Ajax Performance Guidelines
#### Cache Data
#### Know the Limitations of Your Ajax Library

## 8. Programming Practices
### Avoid Double Evaluation
### Use Object/Array Literals
### Don't Repeat Work
#### Lazy Loading
#### Conditional Advance Loading
### Use the Fast Parts
#### Bitwise Operators
#### Native Methods

## 9. Building and Deploying High-Performance JavaScript Applications
### Apache Ant
### Combining JavaScript Files
### Preprocessing JavaScript Files
### JavaScript Minification
### Buildtime Versus Runtime Build Processes
### JavaScript Compression
### Caching JavaScript Files
### Working Around Caching Issues
### Using a Content Delivery Network
### Deploying JavaScript Resources
### Agile JavaScript Build Process

## 10. Tools
### JavaScript Profiling
### YUI Profiler
### Anonymous Functions
### Firebug
#### Console Panel Profiler
#### Console API
#### Net Panel
### Internet Explorer Developer Tools
### Safari Web Inspector
#### Profiles Panel
#### Resources Panel
### Chrome Developer Tools
### Script Blocking
### Page Speed
### Fiddler
### YSlow
### dynaTrace Ajax Edition
