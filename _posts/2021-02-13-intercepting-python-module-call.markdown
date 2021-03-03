---
layout: post
title:  "Intercepting python module __call__()"
date:   2021-2-10 12:27:14 -0800
categories: python
---
Python provides the `__call__()` magic method to allow an object instance to behave as a function in that you could
now call the object directly.

I ran into the case where we needed to override a value previously initialized instance variable being used within 
the `__call__()` in a 3rd party module - specifically the ProxyFix middleware in the Werkzeug library. I'll keep this
example more generic though - I wanted to set up the scenario though in that I really don't want replace the original
class's `__call__()` with my own, but I want to alter some of the instance variables that control the call's behavior.

The solution is straight forward: 
 * Override the class
 * In child class, modify the instance variable
 * call the rest of the logic in base class via `super.__call__()`

Here's a simple gist with example:

<script src="https://gist.github.com/vschmidt94/a0863048ea5f3c9d9400298b3f826082.js"></script>

Note in that gist, the original instance value has been completely replaced, but would be easy enough to save off and restore.
