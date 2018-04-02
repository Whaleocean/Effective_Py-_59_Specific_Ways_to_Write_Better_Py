### item 13: Take Advantage of Each Block in try\except\else\finally
**try\finally**
run cleanup code even when exceptions occur

**One common usage of try\finally BLOCK** if for reliably closing file handles
handle = open("pathway/filename.filetype")
```
try:
    data = handle.read() #May raise UnicodeDecodeError
finally:
    handle.close()       # always run after TRY BLOCK
```
**"open" should be called before "try" block**, because exceptions that occur when opening the file (IOError or the file does not exist) should skip the  "finally" block

**else**
```
def load_jason_key(data,key):
    try:
      result_dict = jason.loads(data)
    except ValueError as e:
      raise KeyError from e\
    else:
      return result_dict[key]
```
If "try" block is successful, "else" block will work. While the "except" handles exception, "else" block will be ignored.

**Everything together**
```
def divide_jason(path):

#open before "try" block

    handle = open(path,"r+")     #May raise IOError        
    try:
        data = handle.read()     #May raise UnicodeError
        op = jason.loads(date)   #May raise ValueError
        value = (op['numberator'] /
                 op['denominator']) #May raise ZeroDivisionError
                 
#handle ZeroDivisionError

    except ZeroDivisionError as e:
        return UNDEFINED
        
# when no ZeroDvisionError

    else:
        op['result'] = value
        result = json.dumps(op)
        handle.seek(0)
        handle.write(result)     #May raise IOError
        return value
# "finally" block is used to clean up the file handle
    finally:
        handle.close()
```
This layout is especially useful because all of the blocks work together in intuitive ways. For example, if an exception gets raised in the else block while rewriting the result data, the finally block will still run and close the file handle

