### Item 16: Consider Generators Instead of Returning Lists
list(generator) 可以把一个生成器转化成list

- Using generators can be clearer than the alternative of returning lists of accumulated results
- The iterator returned by a generator produces the set of values passed to yeid expressions within the generator\`s functino body
- Gnerators can produce a sequence of outputs for arbitrarily large inputs because their working memory donesn\`t include all inputs and outputs

### Item 17: Be Defensive When Iterating Over Arguments
My example
```
def item17(lst):
    for i in lst:
        yield i
lst1 = [1,2,3,4]
it = item17(lst1)
for i in it:
    print(i)
print(list(it))
>>> 
1
2
3
4
[]
```
official example 
```
def normalize(numbers):
    total = sum(numbers)                   
    result = []
    for value in numbers:
        percent = 100 * value / total
        result.append(percent)
    return result

def read_visit(data_path):
    with open(data_path) ad f:
        for line in f:
            yeild int(f)
it = read_visit('temp/my_numbers.txt')
print(normalize(it))
>>> [] 
```
    total = sum(numbers)               # if numbers is a generator, it will be exhausted        
    result = []
    for value in numbers:              # if exhausted, for loop will have no output
        percent = 100 * value / total
        result.append(percent)
    return result
**An iterator noly produces its results a single time**. If you iterate over an iterator or generator tha has already raised a StopIteration excaption, you won\`nt get get any results

What need attentions is that Error won\`t be raised when iterate over an already exhausted iterator.
For loop, list constructor, and many other functions throughtout Pyhton standard library **can\`t tell the difference between an iterator that has no output and an iterator that had output and is now exhuasted**.

Solution 1
```
def normalize(numbers):
    numbers = list(numbers)   # copy the iterator
    .....
```
Drawback - If the iterator\`s content is too large, program will run out of memmory and crash.

Solution 2
```
def nomalize_func(get_iter):
  total = sum(get_iter())
  result = []
  for i in get_iter():
      percent = 100 * i / total
      result.append(percent)
  return result
  
percentages = nomalize_func(lambda: read_visits(data_path))
```
**pass a lambda expression that calls the generator and produces a new iterator each time.**
不用输参数的函数，直接写函数名就可以了，要输入参数的函数，可以使用lambda函数

Solution 3
**Provide a new container class that implements the *iterator* protocol 

statement like "for x in foo" actually call iter(foo), The iter built-in function calls the foo.\_\_iter\_\_method in turn.
```
class ReadVisit(object):
    def __init__(self,path):
        self.path = path
    def __iter__(self):
        with open(self.path) as f:
            for line in f:
                yield int(line)
it = ReadVist(path)
percentage = normalize(it)
print(percentage)
```
different iteration will call \_\_iter\_\_ to allocate different iterate object.  Each of those iterators will be advanced and ehausted independently, ensuring that each unique iteration sees all of the input data values
Drawback reads the input data several times (won\`t run out of memories and crash)

Summary:
- Beware of functions that iterate over input arguments mutiple times. If these arguments are iterators, you may see strange bahavior and missing values
- Python\`s iterator protocol defines how containers and iterators interact with the iter and next built-in fucntions, for loop, and related expressions
- define your own iterable container type by implementing the \_\_iter\_\_ method

### Item 18: Reduce Visual Noise with Variable Positinal Arguments

