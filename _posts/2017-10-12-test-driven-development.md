---
layout: single
title:  "TDD"
---

>First solve the problem, then write the code. 
>                            __ John Johnson

*I love Test Driven Development (TDD) because it makes you focus your coding efforts to a specific task, like mini Agile Scrum sprints. Having written some code years ago before TDD was used, I noted how much it speeds up the process and saves a lot of wasted effort in writing and debugging.*

## Solve the Problem First ##
I solve the problem first:
Before writing any tests, one must fully understand the feature needed. I consider the following 
1. INPUT - What is the data required for input or being passed, including data type and method of receiving 
2. OUTPUT - What is the expected result, including type of object
3. HOW - What process, data structure, logic, and/or iteration, but just brute force, nothing fancy at this point.

## White Board, Paper or REPL ##
REPL = Read, Evaluate, Print, Loop, an interactive console environment where one can enter commands and immediately see results displayed.
I prefer a white board for looking at big picture planning, but I find that using a repl, such as repl.it is very helpful in testing in very low level, what logic will be required. Simply writing the output, such as console.log() or puts, to see the results quicky tests the code.
Once the basic data structure, iteration and/or algorithm is chosen, then I move to write the test in code.

Only after solving the basic problem using pencil/paper, a repl or pseudocode, one is ready to start writing a test. Otherwise, the test itself may be testing something other than the target feature.

## Test-driven development cycle ##
The following sequence is based on the book Test-Driven Development by Example.

1. **Add a test**
Write a test that defines the function or feature in a very small step, in narrow, succinct terms. Only the requirements for the feature or function, including exception conditions, should be covered. It can be written in whatever framework is chosen for the software environment. The test should pass if the requirements are met.

2. **Run all tests.**
All the tests are run, expecting the new one to fail. It must fail if it truly tests the feature/function that is not yet implemented. The failure proves that the test is functioning and that the object it tests is not working yet. This is commonly referred to as the red phase because the new test should fail. All tests are run to show that other previous tests are still passing and that part of the code is still functioning.

3. **Write the code.**
Now write the minimum code to cause the test to pass. The goal is not to write the most elegant code at this point, but to meet the test, even using "brute force". In a later stage, this code will improved to meet higher standards. Do not write code that does anything more than what is required to pass the test. 

4. **Run all tests again.**
Now expect all tests, including the new one to pass. This shows that the new feature/function is met and that it didn't break any existing feature. If any tests do not pass the new code section must be adjusted until all test pass again. Repeat steps 3 and 4 until the test passes. This is commonly called the green phase, all tests passing.

5. **Refactor code.**
Now the code is cleaned up and honed to higher standards,usually best practices or to meet a linter requirements. Duplication should be removed, i.e. DRY up the code. All object names should clearly indicating purpose to improve readability. Extension of code to meet edge cases. Moving code to more appropriate areas if required to meet design conventions or more logical placement. Continually re-running the test cases after each or small group of changes, to make sure that the code didn't break the tests, altering any existing functionality.

6. **Repeat.**
Repeating steps 1-5, starting with a new test for a new feature. The steps should be small, with 1-10 edits between each test run. This prevents excessive debugging time, trying to hunt down the changes in a small amount of code is much faster and efficient. It's usually not rquired to test external libraries unless it one believes they are buggy or not meeting standards required for the current purpose. 

## BEST PRACTICES ##
1.	Keep the unit small
2.	Test Structure
3.	Avoid Anti-patterns
    -  	Dependencies between test cases
    - 	Interdependent tests
    -	Testing precise timing or performance
    -	Inspecting more than necessary
    -   Slow running tests
    -	Testing implementation details

### My preferred RSpec settings ###
I use these settings to add color and report test speeds
.rspec file
```
--color
--require rails_helper
--format documentation 
--profile
```

### Example of Functional Testing and Refactoring ###
Set up test data and expected results before writing each step of function. Attain success using "brute force" if required at first. Then add tests to include edge cases and hard cases, and refactor code to be more efficient and effective depending on goals. Check that the function didn't effect outside of desired effect. 

```
<!DOCTYPE html>
<html>
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
    <title>Refactored date examples</title>
    <script src="prettydate.js"></script>
    <script>
    function test(then, expected) {
        results.total++;
        var result = prettyDate("2008-01-28T22:25:00Z", then);
        if (result !== expected) {
            results.bad++;
            console.log("Expected " + expected + ", but was " + result);
        }
    }
    var results = {
        total: 0,
        bad: 0
    };
    test("2008/01/28 22:24:30", "just now");
    test("2008/01/28 22:23:30", "1 minute ago");
    test("2008/01/28 21:23:30", "1 hour ago");
    test("2008/01/27 22:23:30", "Yesterday");
    test("2008/01/26 22:23:30", "2 days ago");
    test("2007/01/26 22:23:30", undefined);
    console.log("Of " + results.total + " tests, " + results.bad + " failed, "
        + (results.total - results.bad) + " passed.");
    </script>
</head>
<body>
</body>
</html>
```

### Refactoring ### 
The assertions are currently somewhat incomplete because we aren’t yet testing the n weeks ago variant. Before adding it, we should consider refactoring the test code. Currently, this is calling prettyDate for each assertion and passing the now argument. You could easily refactor this into a custom assertion method:

```
test("prettydate basics", function() {
    function date(then, expected) {
        equal(prettyDate("2008/01/28 22:25:00", then), expected);
    }
    date("2008/01/28 22:24:30", "just now");
    date("2008/01/28 22:23:30", "1 minute ago");
    date("2008/01/28 21:23:30", "1 hour ago");
    date("2008/01/27 22:23:30", "Yesterday");
    date("2008/01/26 22:23:30", "2 days ago");
    date("2007/01/26 22:23:30", undefined);
});
```

