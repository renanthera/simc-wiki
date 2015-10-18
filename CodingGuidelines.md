

# Coding Style
## Basic Rules
* Use two spaces for indentation. Do not use tabs.
* Use [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) date-time formatting.

  SimC is used and developed around the world, and there has been enough confusion between American and European date formats in the past.

# Guidelines
* **Readability**

  Because SimulationCraft is a open-source project mainly developed by hobby programmers, we try to focus strongly on code readability. Always try to make your code as easy to read as possible and don't hold back on white-space.

* **Comments**

  Try to add comments for unintuitive or complex code. Not only does it help other/new developers to understand the meaning and intention of a code block, but also your future self.

  Try to document non-intuitive game mechanics and bugs with information on who tested/implemented it and add a date to it.

* **Hardcoded numbers**

  Avoid hard coded numbers if possible. If they are absolutely necessary, document them and include a date.


---

## C++11 support
As of this writing, the Constraints of GCC 4.6, Clang 3.1 and Microsoft Visual Studio 11 ( 2012 ) allows for:
* auto
* static_assert
* range based for loops
* override/final
* default/deleleted functions
* lambdas
* Right Angle Brackets

A complete list of compiler support for various features can be found [here](http://wiki.apache.org/stdcxx/C%2B%2B0xCompilerSupport)