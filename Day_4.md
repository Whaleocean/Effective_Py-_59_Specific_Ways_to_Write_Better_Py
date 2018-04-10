
### Item 14: Prefer Exception to Returning None
Utility functions - it is helpful if you can give special meanings to return value: None
``` 
def devide(a,b):
  if b == 0:
      return None
  else:
      return a/b

result = devide(3,0)
if not result:
    print('Invalid inputs')
```
However, when the numerator is zero. the result 0 will be regard as None

There are two ways to solve the problem
1. return flag for True or Flase, result
2. raise Error

Things to remember
- Functions taht return None to indicate special meaning are error prone because None and other values (zero, the empty list and so on) all evaluate to False in conditional expression
- Raise exceptions to indicate special situations instead of returning None. Except the calling code to handle exceptions properly when thery\`re documented

### item 15: Know How Closures Interact with Variable Scope
sort a list of numbers but priortize one group of numbers to come first. 
```
def sort_priorty(values,group):
    def helper(x):
        if x in group:
            return (0,x)
        return (1,x)
    values.sort(key = helper)
values = [8,3,1,2,5,4,7,6]
group = {2,3,5,7}
sort_priority(values,group)
print(values)
>>> [2,3,5,7,1,4,6,8]
```
The following part will raise BUG
```
def sort_priorty(values,group):
    flag = False
    def helper(x):
        if x in group:
            return (0,x)
            flag = Turee
        return (1,x)
    values.sort(key = helper)
    return flag
values = [8,3,1,2,5,4,7,6]
group = {2,3,5,7}
print(sort_priority(values,group))
>>> False
print(values)
>>> [2,3,5,7,1,4,6,8]
```
It is related to variable Scope.

When **reference a variable**, the python interperter will traverse the scope to resolve the reference in this order
1. The current fuction\`s scope
2. Any enclosing scopes (Like other containing fucntions)
3. The scope of the module that contains the code (also called the global scope)
4. The built-in scope

But assigning a value to a variable works differently. 
If the varibale is already defined in the current scope, then it will just take on the new value. 
If the variable doesn\`t exist in the current scope, the Python treats the assignment as a vatiable definition.
The scope of the newly defined variable is **the functions that contains the assignment**

Encoutering this problem is sometimes called the scoping bug.
But it has benefits : preventing local variables in a function from poluting the containing model. Otherwise, every assignment within a function would put garbage into the global module scope. Not only would that be noise, but interplay of the resulting global variables could cause obscure bugs.

**Getting Data Out**
nonlocal statement



