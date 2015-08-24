

# Coding Style
## Basic Rules
We strictly use two spaces instead of tabs.

# Guidelines
Because SimulationCraft is a open-source project mainly developed by hobby programmers, we try to focus strongly on code readability. Always try to make your code as easy to read as possible and don't hold back on white-space.

Try to put as many meaningful comments into the code as possible, as it makes it much easier for other/new developers to understand the meaning and intention of a code block.

Try to document game mechanics, especially non-intuitive behavior and bugs with information on who tested/implemented it and add a date to it.

Avoid hard coded numbers if possible. If they are absolutely necessary, document it and include a date.


---


> ~~C++11~~ `suspended`
While C++11 offers a range of nice and useful features, supporting a broad range of compilers, including the slightly olders ones, is a high priority.
Thus the accepted features roughly consist of what a union of the oldest supported compilers allow.

As of this writing, the Constraints of GCC 4.4, Clang 2.9 and Microsoft Visual Studio 11 ( 2012 ) leaves `auto`, `static_assert` and `Right Angle Brackets`.
A complete list of compiler support for various features can be found [here](http://wiki.apache.org/stdcxx/C%2B%2B0xCompilerSupport)

> ~~auto specifier~~
  * Use for:
    * Iterators
  * DO NOT use them for:
    * when assigning from literals, eg. auto x = 1.0; ( x would be of type double )
    * When not knowing the type of the object decreases understandability of the subsequent code.