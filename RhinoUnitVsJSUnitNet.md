# RhinoUnit vs JSUnit net #

There are a couple of JSUnit's out there, this compares RhinoUnit to the one found at JSUnit.net.

I am using a standard set of tests for a simple object, called StandardTest.

The biggest advantage I see in using RhinoUnit is that it easily runs as part of the build, and runs very fast.  It also introduces a few nice features such as global namespace pollution (GlobalVars), AssertMustCall, jslinting of the code (JSLint), and no HTML (or DOM) to get in the way!

Here is the JSUnit version of the test

```
<html>
 <head>
  <title>Test Page for rhinounit.smallController</title>
  <script language="javascript" src="jsUnitCore.js"></script>
  <script language="javascript" src="standard.js"></script>
 </head>
 <body>
  <script language="javascript">
var controller;
var view;
var service;
var aValue;

	function setUp() {
		view = {
			addClickListener : function () {}
		};
		service = {
			incrementCounterBy : function () {},
			getCount : function () {
				return 1;
			}
		};
		controller = new rhinounit.smallController(view, service);
	},
	
	function testShouldAddClickListenerWhenCreated() {
		var called = false;
		view.addClickListener = function () {
			called = true;
		};
		controller = new rhinounit.smallController(view, service);
		assertTrue(called);
	}

	function testShouldIncrementByOne() {
		view.addClickListener = function (aFunction) {
			aFunction();
		};		
		var called = false;
		service.incrementCounterBy = function (by) {
			assertEquals(1, by);
			called = true;
		};
		
		controller = new rhinounit.smallController(view, service);
		assertTrue(called);
	}
		
	function serviceGetCountReturnsAValue() {
		service.getCount = function () {
			return aValue;
		};
	},
	
	function shouldRetrieveCountFromService() {
		aValue = 456;
		service.getCount = function () {
			return aValue;
		};
		assertEquals(aValue, controller.getCount());
	},
	
	function shouldReturnRedForCountDivisibleBy3() {
		aValue = 9;
		service.getCount = function () {
			return aValue;
		};
		assertEquals(controller.red, controller.colouring());
	},
	
	function shouldReturnGreenForCountDivisibleBy3Plus1() {
		aValue = 10;
		service.getCount = function () {
			return aValue;
		};
		assertEquals(controller.green, controller.colouring());
	},

	function shouldReturnBlueForCountDivisibleBy3Plus2() {
		aValue = 11;
		service.getCount = function () {
			return aValue;
		};
		assertEquals(controller.blue, controller.colouring());
	},

	function shouldReturnGreenForCountDivisibleBy3RotatedBy1() {
		aValue = 9;
		service.getCount = function () {
			return aValue;
		};
		assertEquals(controller.green, controller.colouring());
	}

  </script>
 </body>
</html>
```

and here is the RhinoUnit version, as copied from the example file

```
eval(loadFile("test/standard.js"));

var controller;
var view;
var service;
var aValue;

testCases(test,

	function setUp() {
		view = {
			addClickListener : function () {}
		};
		service = {
			incrementCounterBy : function () {},
			getCount : function () {
				return 1;
			}
		};
		controller = new rhinounit.smallController(view, service);
	},
	
	function shouldAddClickListenerWhenCreated() {
		assert.mustCall(view, 'addClickListener');
		controller = new rhinounit.smallController(view, service);
	},
	
	when(
		function addClickListenerShouldImediatelyCallCallback() {
			view.addClickListener = function (aFunction) {
				aFunction();
			};		
		},
		function shouldIncrementByOne() {
			service.incrementCounterBy = function (by) {
				assert.that(by, eq(1));
			};
			assert.mustCall(service, 'incrementCounterBy');
			
			controller = new rhinounit.smallController(view, service);
		}
	),
		
	when(
		function serviceGetCountReturnsAValue() {
			service.getCount = function () {
				return aValue;
			};
		},
	
		function shouldRetrieveCountFromService() {
			aValue = 456;
			assert.that(controller.getCount(), eq(aValue));
		},
	
			function shouldReturnRedForCountDivisibleBy3() {
				aValue = 9;
				assert.that(controller.colouring(), eq(controller.red));
			},
	
			function shouldReturnGreenForCountDivisibleBy3Plus1() {
				aValue = 10;
				assert.that(controller.colouring(), eq(controller.green));
			},
	
			function shouldReturnBlueForCountDivisibleBy3Plus2() {
				aValue = 11;
				assert.that(controller.colouring(), eq(controller.blue));
			},
	
			function shouldReturnGreenForCountDivisibleBy3RotatedBy1() {
				aValue = 9;
				assert.that(controller.colouring(1), eq(controller.green));
			}
	)

);
```
(the funny indenting is due to a bug in the Crockford's formatter)