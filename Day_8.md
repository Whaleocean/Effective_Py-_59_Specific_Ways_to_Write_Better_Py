Item 23: Accept Functions for Simple Interfaces Instead Classes. 
Outline：
- Instead of dining and instantiating classes, functions are often all you need for simple interfaces between componets in Python.
- References to functions and methods in Pyhton are first class, meaning they can be used in expression like any other type.
- The \_\_cal\_\_ special method enables instances of a class to be called like plain Python function.
- When you need a functions to maintain state, consider defining a class that provides the \_\_call\_\_ method instead of defining a stateful closure.

