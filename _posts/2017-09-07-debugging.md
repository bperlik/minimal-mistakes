---
layout: single
title:  "Debugging"
---
>Fix the cause, not the symptom. 
>                 -- Steve Maguire

## Steps ##
1.	Identify – what is actually happening vs. what you expected
2.	Reproduce – outline exact reproduction steps
3.	Isolate – where is the bug happening in your code (trace where it goes awry). This is MUCH easier if using small steps and TDD.
4.	Understand – carefully analyze that line to see what is wrong
5.	Solve – find a solution to fix that wrong area/line
6.	Test again – to verify it works

## JavaScript ##
1.	Chrome DevTools (Cmd + Option + J OR right click and select inspect)
- console – note line number, google error messages
- stack trace: check values in console like irb for ruby
- check areas by highlighting area and code highlights to match
- check smaller viewports by clicking on ipad/iphone icon in upper left
- switch mini-fied error messages to full by clicking on () in lower left
- check nodes in Properties in top menu
- console.log(“to check values with output”)
- debugger, step and break
2.	linters – esLinter.com is a good one

## Ruby ##
1.	irb
2.	pry
3.	byebug
4.	test it in repl.it
5.	console.log(“ Test input: #{value}, expect: #{value2} " ) 
6.	Rails – monitor rails server responses
7.  Logs
8.	RSpec 
9.	Rubocop
