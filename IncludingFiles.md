# Including Files for Testing #

Use the following code to include an external JS file

```
  eval(loadFile("path/to/my/file.js"));
```

You will have to do this at the top of your test file, so that the JS is all ready for the tests to run against.  There is no reason to not put in multiple includes.