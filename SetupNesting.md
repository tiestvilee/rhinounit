# Setup Nesting #

To reduce the amount of setup required in individual tests, but also make the setup code local to particular tests, you can use the 'when' clause to nest your set up.

```
var mockObject = {
  returnSomething = function() {}
};

testCases(test,
  function setUp() {
    mockObject.returnSomething = function() {return 1};
  },
  function basicSetUp() {
    assert.that(mockObject.returnSomething(), eq(1));
  },
  when(
    function returnSomethingReturnsHello() {
      var whenLevel1 = mockObject.returnSomething();
      mockObject.returnSomething = function() {return "hello" + whenLevel1;};
    },
    function insideFirstWhen() {
      assert.that(mockObject.returnSomething(), eq("hello1"));
    },
    when(
      function returnSomethingReturnsObject() {
        var whenLevel2 = mockObject.returnSomething();
        mockObject.returnSomething = function() {return {prop : whenLevel2}};
      },
      function insideSecondWhen() {
        assert.that(mockObject.returnSomething().prop, eq("hello1"));
      }
    )
  ),
  function testStillUsingOnlyFirstSetup() {
    assert.that(mockObject.returnSomething(), eq(1));
  }
);
```

In the above code snipet we have three levels of nesting; the original SetUp, and then two nested 'when's.