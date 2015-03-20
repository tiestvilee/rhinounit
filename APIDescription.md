# RhinoUnit API #

RhinoUnit supplies many functions that are generally useful, as well as functions that make it easy to specify assertions.  Short descriptions of these follow.

# RhinoUnit Assert Object #

### assert.that(actual, predicate) ###

This is the basic way of making an assertion in RhinoUnit.  The `actual` value is the value we are testing, and the `predicate` defines the actual test.  Use one of the many tests listed below.

`assert.that("hello", eq("hello"));`

### assert.mustCall(onThisObject, thisMethod) ###

Use this to assert that a function called `thisMethod` on `onThisObject` is called at least once, sometime during the current test.  The named function will also be called.

`assert.mustCall(myObject, "funcThatMustBeCalled");`

See AssertMustCall for more information.

### assert.mustCallNTimes(onThisObject, numberOfTimes, thisMethod) ###

This works the same as `mustCall`, but specifies an exact number of times the function must be called.

### assert.functionThatMustBeCalled(thisMethod, originalFunction) ###

This provides a function that must be called at least once within the current test, otherwise the test will fail.  It uses the `thisMethod` string as a name for the function (so you can tell what function was not called).  These tests are usually used when passing in functions as callbacks.

The optional `originalFunction` is wrapped by the function this assert returns, and will be executed.

```
function myCallback(parameter) {
  assert.that(parameter, eq("aValue"));
}
function_I_am_testing(assert.functionThatMustBeCalled("callback1", myCallback));
```

See AssertMustCall for more information.

### assert.functionThatMustBeCalledNTimes(thisMethod, numberOfTimes, originalFunction) ###

This is the same as `functionThatMustBeCalled`, but must be called an exact number of times.

### assert.mustNotCall(onThisObject, thisMethod) ###

This works the opposite of `mustCall`, failing the test if the specified function is called.

### assert.functionThatMustNotBeCalled(thisMethod) ###

This works the opposite of `functionThatMustBeCalled`, failing the test if the function this method returns is called.

### assert.fail(message) ###

Fails the test instantly.

### assert.callStack(optionalIgnoreAfterMatching) ###

Returns a string that contains a listing of the current callStack.  Only pass in the `optionalIgnoreAfterMatching` regularExpression if you have already identified a particular point that you don't want to display the callstack after.

# RhinoUnit Tests #

### function eq(expected) ###

Uses === to compare `actual` and `expected` values.

### function similar(expected) ###

Uses == to compare `actual` and `expected` values.

### function matches(regExp) ###

Assumes that `regExp` is a regular expression, and tests the `actual` against that regular expression

### function isTrue(message) ###

Tests that the `actual` is true, displaying optional `message` if it is not.

### function isFalse(message) ###

Tests that the `actual` is false, displaying optional `message` if it is not.

### function not(predicate) ###

Inverts the `predicate`

### function hasConstructor(expected) ###

Tests that the constructor name of the `actual` object equals the `expected` string.

### function isA(expected) ###

Tests that the `actual` object is an instance of `expected`

### function isOfType(expected) ###

Tests that the type of `actual` is equal to `expected`

### function isCollectionContaining(value, value, value...) ###

Checks that `actual` is a collection (array) containing at least the parameters.

### function isCollectionContainingOnly(value, value, value...) ###

Checks that `actual` is a collection (array) containing exactly the parameters.

### function containsInOrder(value, value, value...) ###

Checks that `actual` is a collection (array) containing at least the parameters, in the same order.

### function isNull(message) ###

Tests that the `actual` is null, returning the `message` if it isn't.

### function eqFloat(expected, accuracy) ###

Test that `actual` is within accuracy of `expected`.

### function shouldThrowException(theTest, message, checkException) ###

Runs `theTest` function, and fails with `message` if no exception was thrown.  Can also specify an optional `checkException` which details what exception to expect.

# RhinoUnit General Functions #

### function getFunctionNameFor(theFunction) ###

Returns a string that is the name of `theFunction`.

### function getConstructorNameFor(theObject) ###

Returns a string that is the name of the constructor of `theObject`.

### function inspectObject(theObject, depth) ###

Prints out a detailed description of `theObject`.  An optional `depth` parameter can be used to recurse into the object (to a maximum of `depth` levels)

### function forEachElementOf(list, doThis) ###

Steps through the `list`, performing `doThis`.

```
forEachElementOf([ "a", "b", "c"], function(element, index) {
  if(element === "a" && index === 1) {
    print("first element was indeed 'a'");
  } else {
    print(element);
  }
});
```

### function forEachElementOfReversed(list, doThis) ###

Same as forEachElementOf, but steps through in reverse.