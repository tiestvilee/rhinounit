# Javascript Mocking is easy #

As with all dynamic languages, mocking in JS is very easy.  You simply create a new object with the same interface and bob's your uncle.

```
  var myObject = {
    func1 : function (x, y) {
      var resultingPoint = new Point(this.x + 1, y + 1);
      return resultingPoint;
    },
    func2 : function (arg1) {
      this.x = arg1 + 55;
    }
  };

  var mockForMyObject = {
    func1 : function () {
      return {x : 1, y : 2};
    },
    func2 : function () {
    }
  };
```

That's it!  No mocking frameworks, nothing.  Harness the power of Javascript(tm) and dispense with all that guff!