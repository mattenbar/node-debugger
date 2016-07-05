# Node Debugger

## Overview

Have you ever had a pesky bug that you couldn't track with simple print or log statements? Console.logs are okay until they are not enough. Sometimes, it's painful not to be able to stop the execution process to look around the scope and investigate further.

This lesson teaches how to use the built-in Node CLI debugger.

## Objectives

1. Start the Node debugger
1. Describe the debugger and its commands

## Starting The Debugger

Node comes with a built-in debugger. All you need to do is to start the program in debug mode:

```
node debug program.js
```

The prompt will turn into `debug>`. You can get the list of commands with the `help` command.


## Debugger Commands

The debugger commands won't be new to a person familiar with debugging in other languages like Ruby or browser JavaScript (with the help of DevTools). There are:

* run: run program
* cont (c): continue, i.e., proceed with the execution until a breakpoint
* next (n): step to the next line
* step (s): step in (go deeper into the execution context)
* out (o): step out (go out of the execution, skipping the deeper context)
* setBreakpoint (sb): put the break point, e.g., `setBreakpoint(20)` sets the break point on line 20
* clearBreakpoint (cb): remove the break point, e.g., `clearBreakpoint('script.js', 1) clears the break point in the `script.js` file on line 1.

Other commands are: backtrace, watch, unwatch, watchers, repl, restart, kill, list, scripts, breakOnException, breakpoints, version. We won't bore you and spend time covering all of them, just the bare minimum to give you the skills to start debugging.

## Using the Debugger

Oftentimes bugs don't cause crashes. If you have a crash, you can examine the stack trace which contains the line numbers of the failed code. However, subtle bugs are harder to trace. They don't crash programs but the results are not what we expect. Consider this example of a program which generates heads or tails similar to a coin flip. But there is a bug:

```js
var a = Math.floor(Math.random())
if (a>=0.5) {
  console.log('head')
} else {
  console.log('tail')
}
```

The bug is that we get tails every time. How can you debug it? Launch the script in the debug mode with `node debug program.js`. You'd see this:

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


To put a breakpoint programmatically, simply write `debugger` in your code akin to the DevTools debugging:

```
var a = Math.floor(Math.random())
debugger
if (a>=0.5) {
  console.log('head')
} else {
  console.log('tail')
}
```



There are other ways to debug. The built-in debugger is the most low-level approach. The benefit is that it's available in any environment as long as you have Node.


## Step vs. Next

The difference between step (`s`) and next (`n`) is that next won't go into inner functions while step will go into each functions all the way to the bottom. This might take some time!

Consider this example where we have two functions. 

```
var users = function(){
  console.log('users')
}
var accounts = function(){
  console.log('accounts')
  users()
}
accounts()
```

If you use next, debugger won't go inside of `accounts` or `users`, but if you use step, then the debugger will go not only inside of these functions but also inside of the `console.log` and whatever `console.log` is calling.

Most likely, you would use some combination of step, next and breakpoints (`debugger` statements) with continue.


## Resources

1. [Official Debugger Docs](https://nodejs.org/dist/latest-v5.x/docs/api/debugger.html)
1. [Quick demonstration of the node.js debugger](https://www.youtube.com/watch?v=V1vwGDVtAkM)
2. [Comparing Node.js Debug Options](http://spin.atomicobject.com/2015/09/25/debug-node-js)
3. [How to debug Node.js?](http://www.100percentjs.com/best-way-debug-node-js)
4. [Node.js Debugging with the Built-in Debugger](http://technosophos.com/2011/10/28/nodejs-debugging-built-debugger.html)

---

<p data-visibility='hidden'>View <a href='https://learn.co/lessons/node-debugger' title='Node Debugger'>Node Debugger</a> on Learn.co and start learning to code for free.</p>

<p class='util--hide'>View <a href='https://learn.co/lessons/node-debugger'>Node Debugger</a> on Learn.co and start learning to code for free.</p>
