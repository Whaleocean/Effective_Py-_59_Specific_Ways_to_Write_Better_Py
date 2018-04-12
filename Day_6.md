### Item 18: Reducing Visual Noise with Variable Positional Arguments
Outling:
- Function can accept a variable number of postional arguments by using \*args in the def statement
- Use the items from a sequence as the positional arguments for a function with the * operator
- Using the * operator may cause your program to run out of memory and crash
- Sdding new positional parameters to functions that accept \*args can introduce hard-to-find bug

Detail
1. 
2. The drawback of using * operator to pass items as positional arguments
The first issue is that the variable arguments are always turned into a tuple before they are passed to function. This mean that if the caller of your functions uses the * operator on a generator, it will be iterated untill it\`s exhausted. The resulting tuple will also include every value from the generator, which could consume a lot of memory and cause your program to crash.
So it is best to pass the input\`sequence whose numbers of elements are known, and reasonly small.
The second issue with \*args is that you can\`t add new positional arguments to your function in the future without migrating every caller. 

### Item 19: Providing Optional Behavior with Keyword Argument
Outline:
- Fucntion arguments can be specified by postion or by keyword
- Keywords make it clear what the purpose of each argument is when it would be confusing with only positioanl arugments
- Keywords arguments with default values make it easy to add new behaviors to a fucntion, espacially when the fucntion has existing callers
- Optional keyword arguments should always be passed by keyword instead of by postion

Detail
1. The keyword arguments can be passed in any order as long as all of the required positional argumetns are specific. It is feasible to mix and match keyword an positional argumetns 
**Positional arguments must be specific before keyword arguments**
Using keyword argument can provide a pwerful wat yo extend a function\`s parameters wile remaining backwards compatible with existing callers. This let you provide additonal functionality without having migrating a lot of code, reducing the chance of introducing bug.
```
def flow_rate(weight,time,period=1, units=1): # former
def flow_rate(weight, time, period=1, units=1, other_parameter = 1): # later
```
### Item 20: Use None and Docstring to Specify Dynamic Default Argument.
Outline:
- Default arguments are only evaluated once: during function definition at module load time. This can cause odd behaviors for dynamic values (like{} or [])
- Use None as the default value for keyword argumetns that have a dynamic value. Document the actual default behaviors in the function\`s docstring.

Details:
```
def log(message, when=datetime.now()):
  print("%s,%s", % (when,message))
log("hi there!")
sleep(1)
log("Hi there!")
>>> 2018-4-13-00:25:13.371431,hi there!
    2018-4-13-00:25:13.371431,Hi there!
```
datetime.now() is only excuted a single time: when the function is defined. **Default argument values are evaluated only once per module load, which usually happens when a program starts up. After the module containing this code is loaded, the datetime.now default argument will never be evaluated**

The convention for achieving the desired result in Pyhton is to provide a dafault value of None and to document the actuall behavior in the doscting.
```
def log(message, when=None):
  when = datetime.now()
  print("%s,%s", % (when,message))
```

**Using None for default argument values is especially important when the arguments are mutable.**
```
def decode(date, default={}):
    try:
        return json.loads(data)
    except ValueError:
        return default
foo = decode("bad date")
bar = decode("also bad")
foo['stuff'] = 1
bar['meep'] = 5
print("Foo:",foo,"\n","Bar:",bar)
>>> Foo:{"stuff": 1, "meep": 5}
    Bar:{"stuff": 1, "meep": 5}
assert foo is bar
```
The foo and bar are both equal to the default dictionary parameter. They are same in every sense

Improvement 
```
def decode(date, default=None):
    if default = None:
        default = {}
    try:
        return json.loads(data)
    except ValueError:
        return default
```




