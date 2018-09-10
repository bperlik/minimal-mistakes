---
layout: single
title:  "Debugging"
---

>Fix the cause, not the symptom. 
>                 -- Steve Maguire

![Debug in VSCode](/assets/images/debug-menu.png)    

## Follow Best Practices, use Style Guides to help prevent bugs ##
Your employer may have their own requiements.

JavaScript
- [Airbnb JS Style Guide](https://github.com/airbnb/javascript)
- [Github Javascript Style Guide - Standard](https://github.com/standard/standard)
- [Google Javascript Style Guide](https://google.github.io/styleguide/jsguide.html)
- [Airbnb Ruby Style Guide](https://github.com/airbnb/ruby)

## Use Linters to identify problems quickly ##
I use linter plugins in my editor(VSCode) and automated testing on open-source projects
- [ESLint plugin](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
- [RuboCop plugin](https://marketplace.visualstudio.com/items?itemName=misogi.ruby-rubocop)
- [CircleCi](https://circleci.com)
- [TravisCi - Open Source Testing](https://travisci.org)

## Steps ##
1.	Identify – what is actually happening vs. what you expecte
2.	Reproduce – outline exact reproduction steps
3.	Isolate – where is the bug happening in your code (trace where it goes awry). This is MUCH easier if using small steps and TDD.
4.	Understand – carefully analyze that line to see what is wrong
5.	Solve – find a solution to fix that wrong area/line
6.	Test again – to verify it works

## JavaScript ##
1. Use console.log() while testing functions an RPL like rpl.it
2. Use Postman or Firefox to debug ajax requests
3. **Chrome DevTools** - Cmd + Option + J ... or right click and select inspect
-  Check error messages in console tab...note line number, google error messages
-  Unminify code to a more readable format on error codes by clicking the {} Pretty Print button below the source viewer
-  Check areas by highlighting area and code highlights to match
-  Check smaller viewports by clicking on ipad/iphone icon in upper left
-  Check nodes in Properties in top menu
-  Console.log(“to check values with output”)
-  Add debugger; inside a block, step and break
-  Use benchmark loops with console.time()
-  Use a stack trace to check values in the console
```
console.trace('trace <this object')
```
- Use debug(functionName); to find a function to debug
I could 1) find the line in our inspector and add a breakpoint or 2) add a debugger in the script,
but, if it's not a private or anonymous function (we try not to, right?)
I prefer debug(functionName) in the console and 
the script will stop in debug mode when it gets a function call to functionName.
```
  this functionName = function() {
      this.functionName();
  }
```
```
CONSOLE
debug(myobj.functionName)
<<undefinded
>myobj.functionName()
```
- Use monitor() to see which arguments are passed into a function (warning: it doesn't check how many it expects)
- Use $('css-selector') to see the return of the first match on that selector. Use $$('css-selector') to see all.

3. I like to use my own style messages

```
console.todo = function(msg) {
    console.log (' % c % s % s % s', 'color: yellow; background - color: black;', '-', msg '-');
}
console.important = function(msg [
    console.log (' % c % s % s % s', 'color: ; background - color: black;', '-', msg '-');
}

console.todo("This needs to be fixed");
console.important("This is important yada yada.);
```


## Ruby ##
I find that identifying most bugs in Ruby can be relatively easy if using RSpec and TDD and very small code changes in the cycle. The area for error is restricted to a very small amount of code. 

1.	irb
2.	pry
3.	byebug
4.	test ideas in repl.it
5.	console.log(“ Test input: #{value}, expect: #{value2} " ) 
6.	RSpec - gotta love TDD with RSpec
7.	Rails – monitor rails server responses
8.  Logs
