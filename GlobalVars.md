# Global Vars are not allowed #

It is bad practice to allow your variable definitions to bleed into the global namespace by not defining them with 'var' in front of them.  RhinoUnit checks that you don't do this by comparing the globally defined variables before and after the unittests, and throws an error if there are any differences.