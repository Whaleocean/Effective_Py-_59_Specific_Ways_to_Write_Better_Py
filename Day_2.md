u" " 用uicode编码的字符串，可以包含中文字符  
r" " 普通字符串，对内部不进行转义
b" " bytes字符串  16进制数表示utf-8就会出现'\x'  \x(XX)

### item6: avoid Using start,end,stibe in a single slice
somelist[start:end:stribe]
to take every nth item from item.
a = ['a','b','c','d','e','f','g','h']
print(a[-2:2:-2]
stribe is much confusing....

### item7: Using List comprehensions instead of map and filter.

a = [1,2,3,4,5,6,7,8,9]
suqares = \[i\*\*2 for i in a]

a = [1,2,3,4,5,6,7,8,9]
squares = map(lambda x: x\*\*2, a)

result = filter(lambda x: x%2 == 0,map(lambda x: x\*\*2, a)) 
result = \[i\*\*2 for i in a if i %2 == 0]
The filter build-in function can be used along with map to chieve the same outcome but is much harder to read
字典生成式也OJBK

### item8: Avoid more than two expression in List comprehensions
List comprehensions support **mutiple levels of looping**.
matrix = [[1,2,3],[4,5,6],[7,8,9]]
[ x for row in marix for x in row]
>>> [1,2,3,4,5,6,7,8,9]

However, if it contains anther loop, the list comprehension would get so long that you\`d have to split it over multiple lines.
my_lists = [[[1,2,3],[4,5,6]],[[7,8,9],[10,11,12]]]
[item for row in my_lists for col in row for item in col]
at this point, the multiline comprehension isn\`t much shorter than the alternative
```
for row in my_lists:
    for col in row:
        for i in col:
             lst.appen(i)
```          
### item9: Consider Generator Expressions for large Conprehensions
For large input this could consume signigicant amounts of memory and cause your program to crash
e.g. read a file or a never-ending network socket. 
Instead of materializing the whole output sequence when they\`re run, generator evaluate to an iterator that yields one item at a time from the expression.
() def - yield
your code will consume as much of the generator expression as you want without risking a blowup in memory usage.

Another pwerful outcome of generator expression is that they can be composed together. 
一个generator里也可以调用另外一个generator. 
Generator expression execute very quickly when chained together.
### item10: Prefer enumerate over range()
enumerate wraps any iterator with a lazy generator. This generator yields pairs of the loop index and the next value from the iterator.
enumerate就是用来遍历所有item给其加上index的.
enumerate(itertor, startIndex = 0)
can supply a second parameter to enumerate to specify the number from which to begin counting.
### item11: Use zip to process Iterators in Parallel
zip wraps two or more iterators with a lazy generator.
the zip generator yields tuples containing the next value from each iterators.
if input iterators are of different lengths, it keeps yielding tuples until a wrapped iterator is exhausted
### item12: aviod "else" Blocks After for and while loops


