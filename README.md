# Node Debugger

## Overview

This lesson teaches how to use built-in Node debugger.

## Objectives

1. Describe how to start Node debugger
1. Describe debugger and the commands

## Describe how to start Node debugger

Have you ever had a pesky bug that you couldn't track with simple print or log statements? It's painful not to be able to stop the execution process to look around the scope and investigate further. Node comes with a built-in debugger. All you need to do is to start the program in a debug mode:

```
$ node debug program.js
```



## Describe debugger and the commands

The debugger commands won't be new to a person familiar with debugging in other languages like Ruby or browser JavaScript (with the help of DevTools). There are:

* run: run program
* cont (c): proceed with the execution
* next (s): next step
* step (s): step in
* out (o): step out
* backtrace (bt) 
* setBreakpoint (sb): put the break point
* clearBreakpoint (cb): remove the break point

Other commands are: watch, unwatch, watchers, repl, restart, kill, list, scripts, breakOnException, breakpoints, version

Consider this example of a program which generate head or tail similar to a coin flip, only there is a bug:

```js
var a = Math.floor(Math.random())
if (a>=0.5) {
  console.log('head')
} else {
  console.log('tail')
}
```

The bug is that we get tail every time. How can you debug it? Lauch the script in the debug mode with `$ node debug program.js`. You'd see this:

```
$ node debug program.js
< Debugger listening on port 5858
debug> . ok
break in program.js:1
> 1 var a = Math.floor(Math.random())
  2 if (a>=0.5) {
  3   console.log('head')
```

Type `n` and hit enter to proceed to the next statement:

```
debug> n
break in program.js:2
  1 var a = Math.floor(Math.random())
> 2 if (a>=0.5) {
  3   console.log('head')
  4 } else {
debug>
```

Now enter REPL with `repl` and check for value of `a`:

```
debug> repl
Press Ctrl + C to leave debug repl
> a
0
>
```  

The value is 0. You can restart the program with `restart`. Upon closer examination of the first line, we can detect that `Math.floor` will always round to the lowers integer which is 0 in this case. What we want to use in this program is `Math.round()`, not `Math.floor()`. 

You can exit the debugger with `.exit`.

Note: You can also use REPL in debugger to change values. For example, we can manually change the value of `a` to 1 and the program will print `head`.

## Resources

1. 

---

<a href='https://learn.co/lessons/node-overview' data-visibility='hidden'>View this lesson on Learn.co</a>
