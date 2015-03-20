Assert Must Call function is one of the most useful assertions in RhinoUnit.  For more assertions and functions, see APIDescription.

# Assert Must Call method #

To cover all scenarios, it is often useful to assert that a function is called.  This is easily accomplished using the `assert.mustCall(object, functionName)` function which will ensure that the function with the name 'functionName' is called on the supplied object.

Note that this wraps the actual function, it doesn't replace it, so you can still perform useful tests within the function.  For example

```
  function shouldPass1IntoFunction() {
    var mockedObject = {};
    mockedObject.func = function (argument) {
      assert.that(argument, eq(1));
    }
    assert.mustCall(mockedObject, 'func');

    functionBeingTested();
  }
```

The above code snippet is testing `functionBeingTested`.  It ensures that, not only does functionBeingTested pass a '1' into the mockedObject.func function, but also makes sure that that function is called.

This is necessary because the assert.that will not fail is the function is not called!  So, to be sure this test passes, we must make sure that the function is called AND that 1 is passed in.

# Assert functionThatMustBeCalled #

This is very closely related to `assert.mustCall`, but is used to ensure that 'anonymous' functions passed in to functions are called.  For example, when you are passing in a callback.

```
  function shouldCallCallback() {
    functionBeingTested(assert.functionThatMustBeCalled());
  }
```