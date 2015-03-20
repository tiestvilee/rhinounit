This works similarly to other nUnit testing frameworks, though somewhat customized for javascript.  It is exceedingly small, but also surprisingly powerful.

Go to HowToWriteAndRunTests to learn how to use this framework.

# Ant Based Javascript Testing Framework #
In its original form RhinoUnit is run from an ANT scriptdef task using the Rhino engine - and uses all the helpful things that ANT provides for that.  It is intended, however, that in the future the framework can be reused in other forms.

# Unit Testing Javascript #
It will do all the normal tests
  * string and object comparisons
  * regexp comparisons
  * collection comparisons (contains, containsExactly, etc)

And does them in a more natural form.  For example `assert.that("string", not(matches(/somethingelse/)));` checks that the string "string" doesn't match the regular expression /somethingelse/.

## Advanced Tests ##

RhinoUnit provides some more advanced tests.  You can
  * ensure that a function has been called (by wrapping it with `assert.mustCall()`, or using an `assert.functionThatMustBeCalled()`).  See AssertMustCall
  * ensure that an exception is thrown (using `shouldThrowException(...)`
  * ensure that the global namespace isn't polluted by poor variable scoping
See [APIDescription](APIDescription.md) for a list of all assertions and functions that are available.

## Setup Nesting ##
You can use the 'when' construct to nest setup functions to give more obvious context to your tests.  This is like 'chaining' your setUp functions, and means you can reduce the amount of repetition at the top of your tests.  See SetupNesting

# JSLint Integration #
JSLint has been included to ensure that your Javascript files follow (Douglas Crockford's) best practices.  To run the lint js, John Snyder's ant task has also been included.

The original JSLint can be found at

http://www.jslint.com/

and the original Ant script can be found at

http://dev2dev.bea.com/blog/jsnyders/archive/2007/11/using_jslint_from_ant.html

## Comparisons with other Javascript Testing Frameworks ##

[RhinoUnit vs JSUnit.net](RhinoUnitVsJSUnitNet.md)