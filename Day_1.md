
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

### Wrtite Helper Function instead of Complex Expression
```
from urllib.parse import parse_qs
my_values = parse_qs("red=5&blue=0&green=",keep_blank_values=True)
print(my_values)
print("red",my_values.get("red"))
print("blue",my_values.get("blue"))
print("green",my_values.get("green"))
```

empty string, empty list, Zero all evaluate to False implicitly.
A or B - If A is True, return A, else, return B.
```
red = my_values.get("red")[0] or 0
green = my_values.get("green")[0] or 0
blue = my_values.get("blue")[0] or 0
print("red: %s" % red)
print("green: %s" % green)
print("blue: %s" % blue)
```
Also it might be thought not to merit a whole if statement or helper gunction quite yet
*But it extremely to read*
So we can use **ternary expression**
blue = my_values.get("blue")
blue = int(blue[0]) if blue[0] else 0
For less comlicated situation, conditional expression/ ternary expression can make things very clear.
Best recommomdation is writing a helper function if need to use some logic repeatly
def get_first_int(values,color,defalut = 0)
    find = value.get("color")
    if find[0]:
        find = int(find[0])
    else:
        find = 0
    return find
 green = get_firtst_int(my_values,'green'):
 As soon as your expressions get complicated, it is time to **condider splitting them into smaller pieces and moving logic into helper functions**
 
 ### Slice sequence
 sequence[start:end] start is inclusive and the end is exclusive
 sequence[2:-1]
 Slicing deals properly with **start and end indees that are beyond the boundaries** of the list.
 In coantrast, accessing the same index directly causes an exception
 
