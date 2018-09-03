# TDD – Test Driven Development #
1.	Add a test
2.	Run all tests & see if new test fails
3.	Write the code
4.	Run Tests
5.	Refactor code
6.	REPEAT

## BEST PRACTICES ##
1.	Keep the unit small
2.	Test Structure
3.	Avoid Anti-patterns
a. 	Dependencies between test cases
b.	Interdependent tests
c.	Testing precise timing or performance
d.	Inspecting more than necessary
e.	Slow running tests
f.	Testing implementation details

## Test-driven development cycle ##
 
A graphical representation of the test-driven development lifecycle
The following sequence is based on the book Test-Driven Development by Example.[2]

1. Add a test
In test-driven development, each new feature begins with writing a test. Write a test that defines a function or improvements of a function, which should be very succinct. To write a test, the developer must clearly understand the feature's specification and requirements. The developer can accomplish this through use cases and user stories to cover the requirements and exception conditions, and can write the test in whatever testing framework is appropriate to the software environment. It could be a modified version of an existing test. This is a differentiating feature of test-driven development versus writing unit tests after the code is written: it makes the developer focus on the requirements before writing the code, a subtle but important difference.


2. Run all tests and see if the new test fails
This validates that the test harness is working correctly, that the new test does not mistakenly pass without requiring any new code, and that the required feature does not already exist. This step also tests the test itself, in the negative: it rules out the possibility that the new test always passes, and therefore is worthless. The new test should also fail for the expected reason. This step increases the developer's confidence that the unit test is testing the correct constraint, and passes only in intended cases.

3. Write the code
The next step is to write some code that causes the test to pass. The new code written at this stage is not perfect and may, for example, pass the test in an inelegant way. That is acceptable because it will be improved and honed in Step 5.
At this point, the only purpose of the written code is to pass the test. The programmer must not write code that is beyond the functionality that the test checks.

4. Run tests
If all test cases now pass, the programmer can be confident that the new code meets the test requirements, and does not break or degrade any existing features. If they do not, the new code must be adjusted until they do.

5. Refactor code
The growing code base must be cleaned up regularly during test-driven development. New code can be moved from where it was convenient for passing a test to where it more logically belongs. Duplicationmust be removed. Object, class, module, variable and method names should clearly represent their current purpose and use, as extra functionality is added. As features are added, method bodies can get longer and other objects larger. They benefit from being split and their parts carefully named to improve readability and maintainability, which will be increasingly valuable later in the software lifecycle. Inheritance hierarchies may be rearranged to be more logical and helpful, and perhaps to benefit from recognised design patterns. There are specific and general guidelines for refactoring and for creating clean code.[6][7] By continually re-running the test cases throughout each refactoring phase, the developer can be confident that process is not altering any existing functionality.
The concept of removing duplication is an important aspect of any software design. In this case, however, it also applies to the removal of any duplication between the test code and the production code—for example magic numbers or strings repeated in both to make the test pass in Step 3.

6. Repeat
Starting with another new test, the cycle is then repeated to push forward the functionality. The size of the steps should always be small, with as few as 1 to 10 edits between each test run. If new code does not rapidly satisfy a new test, or other tests fail unexpectedly, the programmer should undo or revert in preference to excessive debugging. Continuous integration helps by providing revertible checkpoints. When using external libraries it is important not to make increments that are so small as to be effectively merely testing the library itself,[4] unless there is some reason to believe that the library is buggy or is not sufficiently feature-complete to serve all the needs of the software under development.


## Functional Testing ##

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

## Refactoring ##
The assertions are currently somewhat incomplete because we aren’t yet testing the n weeks ago variant. Before adding it, we should consider refactoring the test code. Currently, we are calling prettyDate for each assertion and passing the now argument. We could easily refactor this into a custom assertion method:

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

