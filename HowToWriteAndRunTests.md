# Introduction #

Incorporating RhinoUnit into your project is pretty easy, and writing the tests is even easier.  This guide gives a little introduction to using Rhino and RhinoUnit.

# Using Rhino #

If you are using Java1.6 then you should already have Rhino available, and the ANT scripts will work out of the box.

If you are using something earlier, or want to use a more modern version of Rhino, then you'll need to download [Rhino](http://www.mozilla.org/rhino/download.html) and a package called [BSF](http://jakarta.apache.org/site/downloads/downloads_bsf.cgi), or Bean Shell Framework.

Copy both these files to your ANT classpath and Rhinounit should just start working.

# Running RhinoUnit #

Once you've checked out the RhinoUnit project you will already have a runnable project.  Simply run 'ant' from the directory you checked out to.  This will pick up the build.xml file and run the default 'run-all-tests' target.

This target currently runs jslint against all files in the project, and also runs all unit tests in the test directory.

It should be a simple case to copy these targets into your Ant build and modify them for your own use.  I would suggest using the second jsLint invocation example, as this is more applicable for production code, whereas the first example has a lot of get-outs to allow the unittesting framework itself to pass.

# Writing Tests #

Check out the tests in the /test directory, especially the simpleTest.js file.  For a more detailed example, have a look in the example directory.

The general pattern for test files is as follows

  * include the unit you are testing (IncludingFiles)
  * set up global variables (don't forget to 'var' them or the tests will fail, see GlobalVars)
  * call 'testCases' passing in 'test' as the first variable
  * write a setUp function to mock all your dependencies.  JavascriptMocking is easy!
  * write some tests, using assert.that to assert conditions, and assert.mustCall to make sure that functions are called (see APIDescription and especially AssertMustCall)

And that's about that