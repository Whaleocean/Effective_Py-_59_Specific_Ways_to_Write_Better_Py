
### PEP 8 style guide
**Whitespace**
sharing a common style with other programmers in the larger community facilitates collaboration on projects.
Use spaces instead of tabs for indentation. Tabs should be used solely to remain consistent with code that is already indented with tabs.
**Python 3 disallows mixing the use of tabs and spaces for indentation.**
Use four spaces for each level of syntacitically significant indenting
Continuation lines should align wrapped elements either vertically using Python’s implicit line joining inside parentheses, brackets and braces, or using a hanging indent
```
foo = long_function_name(variable1,variable2
                         variable3,variable4)
Put one and only one space before and after variable assignment
```
**naming**
### difference between bytes, sytr, and unicode
bytes - raw 8-bit value
str   - Unicode value
instances of bytes and str can not be used together with operator
