# Python Concepts for Rookies

### 1. Reference Behavior of Python 

read this - https://medium.com/@devyjoneslocker/understanding-pythons-pass-by-assignment-in-the-backdrop-of-pass-by-value-vs-9f5cc602f943

In Python, variables are references to object and their behaviour depends on if they are mutable or immutable.

for mutable objects (like lists, dictionaries, sets), changes made to the object via one reference will be reflected in all references to that object.
for immutable objects (like integers, strings, tuples), any operation that modifies the object will create a new object, leaving the original object unchanged.


```python
v1 = [1, 2, 3]
result = []
result.append(v1)  # Adds a REFERENCE in result to v1
v1.append(4)       # Changes both v1 AND the list in result!
print(result)
print(v1)
```

    [[1, 2, 3, 4]]
    [1, 2, 3, 4]


it should be kept in mind because when we use references to objects in form of variables, our data might change based on the object's actual value

it is hence suggested to create explicit copies when needed:


```python
v1 = [1, 2, 3]
result = []
result.append(v1.copy())  # or result.append(v1[:])
v1.append(10)
print(result) # result didn't get changed because we created an explicit copy
```

    [[1, 2, 3]]


2D Matrix


```python
matrix = [[0, 0, 0], [0, 0, 0], [0, 0, 0]]
copy = matrix.copy()  # Only copies outer list - inner lists are shared!
copy[0][0] = 1        # Only changes copy's first row reference
copy[0][1] = 2        # Changes affect BOTH matrices!
print(matrix)
print(copy)
```

    [[1, 2, 0], [0, 0, 0], [0, 0, 0]]
    [[1, 2, 0], [0, 0, 0], [0, 0, 0]]


solution: create explicit copies


```python
matrix = [[0, 0, 0], [0, 0, 0], [0, 0, 0]]
deep_copy = [row[:] for row in matrix]
deep_copy[0][0] = 1
print(matrix)           # matrix didn't change
print(deep_copy)        # only the deep copy changed
```

    [[0, 0, 0], [0, 0, 0], [0, 0, 0]]
    [[1, 0, 0], [0, 0, 0], [0, 0, 0]]


Creating 2D Arrays

Wrong Way (creates reference issue)


```python
matrix = [[0] * 3] * 3  # All rows reference THE SAME LIST!
matrix[0][0] = 1        # Changes first element in ALL rows!
print(matrix)
```

    [[1, 0, 0], [1, 0, 0], [1, 0, 0]]


Right Way


```python
# Each creates independent rows
matrix = [[0 for _ in range(3)] for _ in range(3)]
# or
matrix = [[0] * 3 for _ in range(3)]

matrix[0][0]= 1
print(matrix)
```

    [[1, 0, 0], [0, 0, 0], [0, 0, 0]]


3D Matrix


```python
# Define the dimensions of the 3D array (depth, rows, columns)
depth = 2
rows = 3
columns = 4

# Initialize all elements to 0
three_d_array = [[[0 for _ in range(columns)] for _ in range(rows)] for _ in range(depth)]

# Print the resulting 3D array
print(three_d_array)
```

    [[[0, 0, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0]], [[0, 0, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0]]]


### 2. String immutability in Python

- strings are immutable in python, so once generated they cannot be modified


```python
str = "*" * 5
print(str[0])
# str[0]= "67" (x) cannot modify

# list of strings however can be modified
l= ["*"] * 5
print(l)
l[0]= "#"
print(l)

# join all elements to form a single string
print("".join(l))

# list of list of strings (ex- a chess board with only queens)
board= [["."] * 8 for _ in range(8)]
print(board)
print(["".join(row) for row in board])
```

    *
    ['*', '*', '*', '*', '*']
    ['#', '*', '*', '*', '*']
    #****
    [['.', '.', '.', '.', '.', '.', '.', '.'], ['.', '.', '.', '.', '.', '.', '.', '.'], ['.', '.', '.', '.', '.', '.', '.', '.'], ['.', '.', '.', '.', '.', '.', '.', '.'], ['.', '.', '.', '.', '.', '.', '.', '.'], ['.', '.', '.', '.', '.', '.', '.', '.'], ['.', '.', '.', '.', '.', '.', '.', '.'], ['.', '.', '.', '.', '.', '.', '.', '.']]
    ['........', '........', '........', '........', '........', '........', '........', '........']


Key Python Concepts to Remember

- Variables are references to objects, not containers for values
- Assignment (=) never copies data, it creates a new reference
- Mutable objects (lists, dicts, etc.) can be modified through any reference
- .copy() creates shallow copies (one level deep)
- For nested structures, use copy.deepcopy() or manual copying

### 3. Data Structures in python

- #### Heap

Python has min-heap via heapq module, not max-heap. For max-heap, negate values or use custom objects

quick recap:
- min heap stores the min element at the top, so when we pop we get the min element and then the next min and so on!
- max heap does the same but opposite, so it stores the max element at the top

this concept is extremeently useful in many DSA problems!


```python
import heapq
heap = []

# push
heapq.heappush(heap, 5)
heapq.heappush(heap, 10)
print(heap)

 # pop
item = heapq.heappop(heap)
print(heap)

# create a heap from a list
h = [10, 20, 15, 30, 40]
heapq.heapify(h)

# append an element to the heap
heapq.heappush(h, 5)

# pop the smallest element from the heap
min = heapq.heappop(h)

print(h)

# print the length of the heap
print(len(h))
```

    [5, 10]
    [10]
    [10, 20, 15, 30, 40]
    5


- #### Stack

There is no inbuilt stack data structure use a list using append and pop to mimic push and pop operations


```python
stack= []
stack.append(5) # push
stack.append(10) # pop
stack.pop()
print(stack)
```

    [5]


- #### Set

1. for storing and searching unique elements in O(1)
2. elements in set are immutable, however a set itself it mutable


```python
set= {1, 2, 3}

set.add(10)
print(set)
print(10 in set)
set.remove(10)
print(set)
```

    {10, 1, 2, 3}
    True
    {1, 2, 3}


- #### Queue (LIFO)

use deque from the collections library

functions in deque:
- append(x): Add x to the right side of the deque.
- appendleft(x): Add x to the left side of the deque.
- pop(): Remove and return an element from the right side of the deque. If no elements
    are present, raises an IndexError.
- popleft(): Remove and return an element from the left side of the deque. If no elements
    are present, raises an IndexError.


```python
from collections import deque

q = deque()

q.append(5)
q.append(10)
print(q)
q.popleft()
print(q)
```

    deque([5, 10])
    deque([10])


- #### Dictionary

1. key value pairs
2. keys are immutable, values can be mutable or immutable
3. average O(1) time complexity for search, insert and delete


```python
dict = {}

dict["one"] = 1 # add key-value pair
dict["two"] = 2 
print(dict)  # print the entire dictionary
print(dict["one"]) # access value by key
print("two" in dict)  # check if key is present
```

    {'one': 1, 'two': 2}
    1
    True


- #### DefaultDict

defaultdict is a subclass of the built-in dict class from the collections module. It is used to provide a default value for a nonexistent key in the dictionary, eliminating the need for checking if the key exists before using it.

Key Features of defaultdict:
- When we access a key that doesn’t exist in the dictionary, defaultdict automatically creates it and assigns it a default value based on a function we provide.
- We need to specify the default value type by passing a function (like int, list or set) when initializing the defaultdict.


```python
from collections import defaultdict

d = defaultdict(list)

d['fruits'].append('apple')
d['vegetables'].append('carrot')
print(d)

print(d['juices'])
```

    defaultdict(<class 'list'>, {'fruits': ['apple'], 'vegetables': ['carrot']})
    []



```python
# defaultfactory - It is a function returning the default value for the dictionary defined. If this argument is absent then the dictionary raises a KeyError.

from collections import defaultdict

d = defaultdict(lambda: "default value")
print(d['missing_key'])  # Will print "default value" instead of raising KeyError

# defaultdict with int as default factory
d = defaultdict(int)
d['count'] += 1  # Automatically initializes 'count' to 0 and then increments it
print(d['count'])  # Will print 1

# defaultdict with a list as default factory
d = defaultdict(list)
d['key'].append('value')  # Automatically initializes 'key' to an empty list and appends 'value'
print(d['key'])  # Will print ['value']

# defaultdict with a set as default factory
d = defaultdict(set)
d['key'].add('value')  # Automatically initializes 'key' to an empty set and adds 'value'
print(d['key'])  # Will print {'value'}

# defaultdict with string as default factory
d = defaultdict(str)
d['key'] += 'value'  # Automatically initializes 'key' to an empty string and concatenates 'value'
print(d['key'])  # Will print 'value'
```

    default value
    1
    ['value']



    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    Cell In[17], line 19
         16 print(d['key'])  # Will print ['value']
         18 # defaultdict with a set as default factory
    ---> 19 d = defaultdict(set)
         20 d['key'].add('value')  # Automatically initializes 'key' to an empty set and adds 'value'
         21 print(d['key'])  # Will print {'value'}


    TypeError: first argument must be callable or None


### Miscellaneous concepts

- to get the min and max value use "sys.maxsize" and "-sys.maxsize-1"


```python
import sys
print(sys.maxsize)
print(-sys.maxsize-1)
```

    9223372036854775807
    -9223372036854775808


- Slicing in lists and strings

    ```[start:end:step]```
    - start: Index where the slice begins (inclusive). Defaults to 0 if omitted.
    - stop: Index where the slice ends (exclusive). Defaults to the sequence's length if omitted.
    - step: Determines the interval between elements. Defaults to 1 if omitted.

Note: in real word scenario for example if you want to fetch the last 1000 logs of a large dataset

```
logs = load_large_dataset()  
recent_logs = logs[-1000:]
```


```python
b = "Hello, World!"

# slice from start
print(b[:5])

# slice to end
print(b[2:])

# -ve slicing
print(b[-5:-2]) 
```

    Hello
    llo, World!
    orl



```python
numbers = [10, 20, 30, 40, 50, 60]  

print(numbers[1:4])   

print(numbers[:3])

print(numbers[::2]) 

print(numbers[-1:-5:-1])

print(numbers[::-1])
```

    [20, 30, 40]
    [10, 20, 30]
    [10, 30, 50]
    [60, 50, 40, 30]
    [60, 50, 40, 30, 20, 10]


### List Comprehensions

concise way to build a new list from an existing list (or any "iterable" like a range of numbers) in a single line

```python
[expression for item in iterable if condition]
```


```python
# generate a list of numbers from 0 to 9

numbers = [i for i in range(10)]
```


```python
# generate a list of squares of numbers from 0 to 9

squares = [i**2 for i in range(10)]
```


```python
# 2d list

matrix= [[0 for _ in range(10)] for _ in range(10)]
print(matrix)
```

    [[0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 0, 0, 0, 0]]



```python
# why not this?

bad_matrix= [[0]*10]*10
print(bad_matrix)
```

    [[0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 0, 0, 0, 0]]


#### why [[0] * m] * n is problematic?
[0] * m: This creates one single list [0, 0, ..., 0] of length m.
[...] * n: This creates a list containing n references to that exact same single list.


```python
# so if you change any cell in a row, it will affect other rows as well

bad_matrix[0][0]= 10
print(bad_matrix)

# note how all the 0th index of each row turned into 10
```

    [[10, 0, 0, 0, 0, 0, 0, 0, 0, 0], [10, 0, 0, 0, 0, 0, 0, 0, 0, 0], [10, 0, 0, 0, 0, 0, 0, 0, 0, 0], [10, 0, 0, 0, 0, 0, 0, 0, 0, 0], [10, 0, 0, 0, 0, 0, 0, 0, 0, 0], [10, 0, 0, 0, 0, 0, 0, 0, 0, 0], [10, 0, 0, 0, 0, 0, 0, 0, 0, 0], [10, 0, 0, 0, 0, 0, 0, 0, 0, 0], [10, 0, 0, 0, 0, 0, 0, 0, 0, 0], [10, 0, 0, 0, 0, 0, 0, 0, 0, 0]]



```python
# common functions

# sort
arr= [1, 3, 2, 4, 1]
arr.sort()
print(arr)

# reverse sort
arr.sort(reverse=True)
print(arr)

# a function that returns the length of the value:
def myFunc(e):
  return len(e)

cars = ['Ford', 'Mitsubishi', 'BMW', 'VW']
cars.sort(key=myFunc)
print(cars)
```

    [1, 1, 2, 3, 4]
    [4, 3, 2, 1, 1]
    ['VW', 'BMW', 'Ford', 'Mitsubishi']


### lambda functions

A lambda function is a small anonymous function.

A lambda function can take any number of arguments, but can only have one expression.

```
lambda arguments : expression
```


```python
x = lambda a : a + 10
print(x(5)) 
```

    15


### Collection Utilities


```python
# counter

from collections import Counter

# 1. Counting elements in a list
my_list = [1, 2, 2, 3, 3, 3, 4, 4, 4, 4]
list_counter = Counter(my_list)
print(f"Counter from list: {list_counter}")

# 2. Counting characters in a string
my_string = "abracadabra"
string_counter = Counter(my_string)
print(f"Counter from string: {string_counter}")

# 3. Counting elements from a dictionary (keyword arguments)
word_counts = Counter(a=4, b=2, c=0, d=2)
print(f"Counter from keyword arguments: {word_counts}")
```

    Counter from list: Counter({4: 4, 3: 3, 2: 2, 1: 1})
    Counter from string: Counter({'a': 5, 'b': 2, 'r': 2, 'c': 1, 'd': 1})
    Counter from keyword arguments: Counter({'a': 4, 'b': 2, 'd': 2, 'c': 0})

