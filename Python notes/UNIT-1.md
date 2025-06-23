
**Unit 1:** 
Python basics, Objects- Python Objects, Standard Types, Other Built-in Types, Internal Types, Standard Type Operators, Standard Type Built-in Functions, Categorizing the Standard Types, Unsupported Types Numbers - Introduction to Numbers, Integers, Floating Point Real Numbers, Complex Numbers, Operators, Built-in Functions, Related Modules Sequences - Strings, Lists, and Tuples, Dictionaries and Set Types Control Flow, Truthiness, Sorting, List Comprehensions, Generators and Iterators

#### Python Basics:

**Python** is a **high-level**, **interpreted**, and **general-purpose** programming language created by **Guido van Rossum** and first released in **1991**. It is known for its:

- **Simple and readable syntax**, which resembles English, making it beginner-friendly.
- **Versatility**, supporting multiple programming paradigms: **procedural**, **object-oriented**, and **functional** programming.
- **Wide range of applications**, including web development, data science, automation, artificial intelligence, and more.

Python is **interpreted**, meaning the code is executed line-by-line by the **Python Interpreter** without needing compilation, which simplifies debugging and development.

#### Key Features of Python

1. **Easy to Learn and Read**: Python’s syntax is clear and concise, reducing the learning curve for beginners.
2. **Dynamically Typed**: No need to declare variable types; Python assigns types at runtime.
    - Example: x = 10 (Python infers x is an integer).
3. **Portable**: Python runs on multiple platforms (Windows, Linux, macOS) without modification.
4. **Extensive Standard Library**: Python comes with a large collection of modules and packages for tasks like file handling, networking, and more.
5. **Open Source**: Free to use and modify, with a strong community for support.
6. **Interpreted**: Executes code directly, making it easier to test and debug.
7. **Supports Multiple Paradigms**: Allows procedural (function-based), object-oriented (class-based), and functional (using functions as objects) programming.
8. **Garbage Collection**: Automatically manages memory, freeing developers from manual memory management.

#### Python Execution

Python code can be executed in two ways:

1. **Interactive Mode**: Using the Python shell (IDLE or command-line), where you type and run code instantly.
    - Example: Open Python shell, type print("Hello"), and see output immediately.
2. **Script Mode**: Writing code in a **.py** file and running it using the command python filename.py.
    - Example: Save print("Hello, World!") in hello.py and run it.


#### Variables and Data Types

- **Variables**: Containers for storing data. Created when a value is assigned, e.g., x = 10.
    - No need to declare type; Python infers it dynamically.
    - Variable names are **case-sensitive** (X and x are different) and follow rules:
        - Start with a letter or underscore (_).
        - Contain letters, numbers, or underscores.
        - Avoid reserved words (e.g., if, for, while).
- **Data Types**: Python supports various built-in data types:
    - **Numbers**: Integers (10), Floating-point (3.14), Complex (3+4j).
    - **Sequences**: Strings ("hello"), Lists ([1, 2, 3]), Tuples ((1, 2, 3)).
    - **Mappings**: Dictionaries ({"name": "Alice"}).
    - **Sets**: Sets ({1, 2, 3}), Frozen sets.
    - **Boolean**: True, False.
    - **NoneType**: None (represents null or no value).

```python
x = 10          # Integer
y = 3.14        # Float
name = "Alice"  # String
is_student = True  # Boolean
print(x, y, name, is_student)  # Output: 10 3.14 Alice True
```

#### Basic Syntax

- **Comments**: Used to add notes in code, ignored by the interpreter.
    - Single-line: `# This is a comment.`
    - Multi-line: `This is a multi-line comment.`
- **Indentation**: Python uses spaces (usually 4) to define code blocks instead of braces {}.
```python
if True:
    print("Indented block")  # 4 spaces
```

- **Statements**: A line of code that performs an action, e.g., x = 5.
- **Multi-line Statements**: Use a backslash (\) or parentheses to continue a statement.
```python
total = 1 + 2 + \
        3 + 4
print(total)  # Output: 10
```
#### Input and Output

- **Output**: Use print() to display data.
```python
print("Hello, World!")  # Output: Hello, World!
```
    
- **Input**: Use input() to get user input (returns a string).
```python
name = input("Enter your name: ")
print("Hello,", name)
```
#### Basic Operators

Operators perform operations on variables and values:

1. **Arithmetic**: + (add), - (subtract), * (multiply), / (divide), // (floor division), % (modulus), ** (exponentiation).
```python
x = 10
y = 3
print(x + y)  # 13
print(x // y)  # 3
print(x ** 2)  # 100
```

2. **Comparison**: == (equal), != (not equal), <, >, <=, >=.
```python
print(x > y)  # True
```

3. **Logical**: and, or, not.
```python
print(x > 5 and y < 5)  # True
```

4. **Assignment**: =, +=, -=, *=, /=, etc.
```python
x += 5  # x = x + 5
print(x)  # 15
```


### Objects

## 1. Python Objects

In Python, **everything is an object**, including numbers, strings, lists, functions, and even modules. An object is an instance of a **class**, and it has:

- **Identity**: A unique identifier for the object, accessed using id().
- **Type**: The data type or class of the object, accessed using type().
- **Value**: The actual data stored in the object.

```python
x = 10
print(id(x))    # Unique ID (e.g., 140723123456)
print(type(x))  # <class 'int'>
print(x)        # Value: 10
```

- Objects can be **mutable** (changeable, e.g., lists) or **immutable** (unchangeable, e.g., strings, tuples).
- Python manages objects using **reference counting** and **garbage collection** to handle memory.

A Class is like an object constructor, or a "blueprint" for creating objects.
#### Create a Class

To create a class, use the keyword `class`:
```python
#Create a class named MyClass, with a property named x:
class MyClass:  
  x = 5
```
#### Create Object

Now we can use the class named MyClass to create objects:
```python
p1 = MyClass()  
print(p1.x)
```

#### The __init__() Function

The examples above are classes and objects in their simplest form, and are not really useful in real life applications.

To understand the meaning of classes we have to understand the built-in __init__() function.

All classes have a function called __init__(), which is always executed when the class is being initiated.

Use the __init__() function to assign values to object properties, or other operations that are necessary to do when the object is being created:
```python
Create a class named Person, use the `__init__()` function to assign values for name and age:

class Person:  
  def __init__(self, name, age):  
    self.name = name  
    self.age = age  
  
p1 = Person("John", 36)  
  
print(p1.name)  
print(p1.age)
```

#### Standard Types

Python’s **standard types** are the built-in data types used to store and manipulate data. They are categorized as:

1. **Numbers**:
    - Integers (int): Whole numbers, e.g., 5, -10.
    - Floating-point (float): Decimal numbers, e.g., 3.14.
    - Complex (complex): Numbers with real and imaginary parts, e.g., 3 + 4j.
2. **Sequences**:
    - Strings (str): Immutable sequence of characters, e.g., "hello".
    - Lists (list): Mutable sequence of items, e.g., [1, 2, 3].
    - Tuples (tuple): Immutable sequence of items, e.g., (1, 2, 3).
3. **Mappings**:
    - Dictionaries (dict): Key-value pairs, e.g., {"name": "Alice", "age": 20}.
4. **Sets**:
    - Sets (set): Mutable collection of unique elements, e.g., {1, 2, 3}.
    - Frozen sets (frozenset): Immutable sets, e.g., frozenset([1, 2, 3]).
5. **Boolean**:
    - True and False for logical operations.
6. **NoneType**:
    - None: Represents null or no value.

```python
x = 10          # Integer
s = "hello"     # String
lst = [1, 2]    # List
d = {"a": 1}    # Dictionary
s1 = {1, 2}     # Set
print(type(x), type(s), type(lst), type(d), type(s1))  
# Output: <class 'int'> <class 'str'> <class 'list'> <class 'dict'> <class 'set'>
```

#### Other Built-in Types

Besides standard types, Python includes additional built-in types used in specific contexts:
1. **NoneType**: Represents None, used to indicate no value or null.
    - Example: x = None; print(x) → None.
2. **Boolean**: True and False, used in logical operations.
    - Example: x = 5 > 3; print(x) → True.
3. **Functions**: Reusable code blocks defined using def
	```python
	def greet(): return "Hello"
print(type(greet))  # <class 'function'>
```


#### Internal Types

**Internal types** are used by Python’s interpreter for its internal operations and are rarely manipulated directly by programmers:

1. **Code Objects**: Represent compiled Python code, used by functions.
    - Example: Access via function.__code__.
2. **Frame Objects**: Represent execution frames for function calls, used during runtime.
3. **Traceback Objects**: Store information about exceptions for debugging.
    - Example: Seen in exception handling with try-except.

These types are low-level and typically accessed only in advanced scenarios (e.g., debugging or creating interpreters).

#### Standard Type Operators

**Operators** are symbols used to perform operations on objects. Python supports several types of operators for standard types:

1. **Arithmetic Operators** (for numbers):
    - + (addition), - (subtraction), * (multiplication), / (division), // (floor division), % (modulus), ** (exponentiation).
    - Example: 5 + 3 → 8; 10 // 3 → 3.
2. **Comparison Operators** (for numbers, sequences, etc.):
    - == (equal), != (not equal), <, >, <=, >=.
    - Example: 5 == 5 → True; "abc" < "def" → True.
3. **Logical Operators** (for booleans):
    - and, or, not.
    - Example: True and False → False; not True → False.
4. **Membership Operators** (for sequences, sets, dictionaries):
    - in, not in.
    - Example: 2 in [1, 2, 3] → True; "a" not in "xyz" → True.
5. **Identity Operators** (for objects):
    - is, is not.
    - Example: x = 10; y = 10; print(x is y) → True (small integers share the same object in Python).
6. **Sequence Operators** (for strings, lists, tuples):
    - Concatenation: + (e.g., "hello" + "world" → "helloworld").
    - Repetition: * (e.g., "ha" * 3 → "hahaha").
    - Slicing: [start:end] (e.g., "hello"[1:4] → "ell").

#### Standard Type Built-in Functions

Standard type built-in functions are predefined functions in Python that operate on standard types (e.g., numbers, strings, lists, tuples, dictionaries, sets, booleans). These functions help perform common tasks like checking types, converting data, finding lengths, or manipulating values. They are available without importing any modules.

## Key Built-in Functions

Here’s a concise list of the most important built-in functions for standard types, with their purpose and examples:

1. **type(obj)**
    - **Purpose**: Returns the data type (class) of an object.
```python
print(type(10))      # <class 'int'>
print(type("hello"))  # <class 'str'>
```

        
2. **id(obj)**
    - **Purpose**: Returns the unique identity (memory address) of an object.
```python
x = 5
print(id(x))  # Unique ID (e.g., 140723123456)
```
        
3. **len(seq)**
    - **Purpose**: Returns the number of items in a sequence (string, list, tuple, dictionary, set).
 ```python
 print(len("hello"))     # 5
print(len([1, 2, 3]))   # 3
```
        
4. **str(obj)**
    - **Purpose**: Converts an object to its string representation.
```python
print(str(10))      # "10"
print(str([1, 2]))  # "[1, 2]"
```
        
5. **int(x)**
    - **Purpose**: Converts a string or number to an integer (truncates decimals for floats).
```python
print(int("10"))    # 10
print(int(3.14))    # 3
```
        
6. **float(x)**
    - **Purpose**: Converts a string or number to a floating-point number.
```python
print(float("3.14"))  # 3.14
print(float(10))      # 10
```

        
7. **complex(x, [y])**
    
    - **Purpose**: Converts numbers or strings to a complex number (x + yj).
```python
print(complex(3, 4))  # (3+4j)
print(complex("3+4j")) # (3+4j)
```
    
8. **abs(x)**
    - **Purpose**: Returns the absolute (positive) value of a number (integer, float, or complex).
```python
print(abs(-5))      # 5
print(abs(-3.14))   # 3.14
```
        
9. **max(iterable) and min(iterable)**
    - **Purpose**: Returns the maximum or minimum value in an iterable (sequence or set).
```python
print(max([1, 5, 2]))  # 5
print(min("hello"))    # 'e' (based on ASCII order)
```
        
10. **ord(c)**
    - **Purpose**: Returns the ASCII value (integer) of a single character.

```
print(ord('A'))  # 65
```
        
11. **chr(x)**
    - **Purpose**: Returns the character corresponding to an ASCII value (integer).
```
print(chr(65))  # 'A'
```

        
12. **bool(x)**
    - **Purpose**: Converts an object to a boolean (True or False). Falsy values include 0, "", [], None; others are True.

```
print(bool(0))      # False
print(bool("hi"))  # True
```
        
13. **repr(obj)**
    - **Purpose**: Returns a string representation of an object, often used for debugging.
```
print(repr([1, 2]))  # '[1, 2]'
```

#### Categorizing the Standard Types

Standard types can be categorized based on their properties:

1. **Mutable vs. Immutable**:
    - **Mutable**: Can be changed after creation.
        - Examples: Lists, dictionaries, sets.
        - Example: lst = [1, 2]; lst.append(3) → [1, 2, 3].
    - **Immutable**: Cannot be changed after creation.
        - Examples: Integers, floats, strings, tuples, frozen sets.
        - Example: s = "hello"; s[0] = "H" → Error (strings are immutable).
2. **Ordered vs. Unordered**:
    - **Ordered**: Maintains insertion order.
        - Examples: Lists, tuples, strings.
        - Example: lst = [1, 2, 3]; print(lst[0]) → 1.
    - **Unordered**: No specific order (before Python 3.7 for dictionaries).
        - Examples: Sets, dictionaries (pre-Python 3.7).
        - Example: {1, 2, 3} does not guarantee order.
3. **Sequence vs. Non-Sequence**:
    - **Sequence**: Supports indexing and slicing.
        - Examples: Strings, lists, tuples.
    - **Non-Sequence**: Does not support indexing/slicing.
        - Examples: Dictionaries, sets.
4. **Iterable vs. Non-Iterable**:
    - **Iterable**: Can be looped over (e.g., using a for loop).
        - Examples: Strings, lists, tuples, dictionaries, sets.
    - **Non-Iterable**: Cannot be looped over.
        - Examples: Integers, floats.

```python
lst = [1, 2, 3]  # Mutable, ordered, sequence, iterable
s = "hello"       # Immutable, ordered, sequence, iterable
d = {"a": 1}      # Mutable, unordered (pre-3.7), non-sequence, iterable
s1 = {1, 2}       # Mutable, unordered, non-sequence, iterable
```
#### Unsupported Types

Python does not natively support certain data types found in other languages:
- **Fixed-size Arrays**: Python uses lists or the array module/NumPy for array-like functionality.
- **Pointers**: Python does not support direct memory manipulation like C/C++.
- **Character Type**: Single characters are treated as strings of length 1 (e.g., "a").
- **Why Unsupported**: Python’s design prioritizes simplicity and abstraction, using higher-level types like lists and strings.

## Numbers

Numbers in Python represent numerical data and include **integers**, **floating-point real numbers**, and **complex numbers**.

#### Introduction to Numbers

- Numbers are **immutable** types used for arithmetic and calculations.
- Types: Integers (whole numbers), floats (decimals), and complex (real + imaginary).

#### Integers

- Whole numbers, positive, negative, or zero (e.g., 5, -10, 0).
- No size limit in Python 3 (no overflow).
- Example: x = 100; print(type(x)) → <class 'int'>.

#### Floating-Point Real Numbers

- Numbers with decimal points (e.g., 3.14, -0.001).
- Stored with limited precision (IEEE 754 standard).
- Example: y = 2.5; print(type(y)) → <class 'float'>.

#### Complex Numbers

- Numbers with real and imaginary parts, denoted by j (e.g., 3 + 4j).
- Attributes: .real (real part), .imag (imaginary part).
- Example: z = 3 + 4j; print(z.real, z.imag) → 3.0 4.0.

#### Operators for Numbers

- **Arithmetic**: +, -, *, / (true division), // (floor division), % (modulus), ** (exponentiation).
- **Comparison**: ==, !=, <, >, <=, >=.
```python
x = 10; y = 3
print(x / y)   # 3.333...
print(x // y)  # 3
print(x ** 2)  # 100
```
#### Built-in Functions for Numbers

- abs(x): Absolute value (e.g., abs(-5) → 5).
- round(x, n): Rounds to n decimal places (e.g., round(3.14159, 2) → 3.14).
- pow(x, y): x raised to y (e.g., pow(2, 3) → 8).
- divmod(x, y): Returns (x // y, x % y) (e.g., divmod(10, 3) → (3, 1)).
- int(x), float(x), complex(x): Type conversions.

#### Related Modules

Python provides **modules** (libraries) to extend functionality for various types, especially for sequences, dictionaries, and sets. Common modules relevant to Unit-I include:

- **string**: Utilities for string operations.
    - Example: string.ascii_letters → "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ".
- **collections**: Advanced data structures for sequences and mappings.
    - Example: collections.Counter("hello") → Counter({'l': 2, 'h': 1, 'e': 1, 'o': 1}).
- **itertools**: Tools for efficient iteration (used with sequences, generators).
    - Example: itertools.chain([1, 2], [3, 4]) → iterator yielding 1, 2, 3, 4.
- **random**: Random operations on sequences.
    - Example: random.choice(["a", "b"]) → random item ("a" or "b").
- **math**: Mathematical operations (sometimes used with sequences of numbers).
    - Example: math.prod([2, 3]) → 6 (Python 3.8+).
```python
import string
print(string.digits)  # 0123456789
import random
print(random.shuffle([1, 2, 3]))  # Shuffles list in place
```

#### Sequences

A [sequence](https://docs.python.org/3/glossary.html#term-sequence) is a data structure that contains items arranged in order, and you can access each item using an integer index that represents its position in the sequence. You can always find the length of a sequence. Here are some examples of sequences from Python’s basic built-in data types:
```python
>>> # List
>>> countries = ["USA", "Canada", "UK", "Norway", "Malta", "India"]
>>> for country in countries:
...     print(country)
...
USA
Canada
UK
Norway
Malta
India
>>> len(countries)
6
>>> countries[0]
'USA'

>>> # Tuple
>>> countries = "USA", "Canada", "UK", "Norway", "Malta", "India"
>>> for country in countries:
...     print(country)
...
USA
Canada
UK
Norway
Malta
India
>>> len(countries)
6
>>> countries[0]
'USA'

>>> # Strings
>>> country = "India"
>>> for letter in country:
...     print(letter)
...
I
n
d
i
a
>>> len(country)
5
>>> country[0]
'I'
```

Lists, tuples, and strings are among Python’s most basic data types. Even though they’re different types with distinct characteristics, they have some common traits. You can summarize the characteristics that define a Python sequence as follows:

- A sequence is an [iterable](https://realpython.com/python-iterators-iterables/), which means you can iterate through it.
- A sequence has a length, which means you can pass it to [`len()`](https://realpython.com/len-python-function/) to get its number of elements.
- An element of a sequence can be accessed based on its position in the sequence using an integer index. You can use the square bracket notation to index a sequence.

There are other built-in data types in Python that also have all of these characteristics. One of these is the [`range` object](https://realpython.com/python-range/):

```python
>>> numbers = range(5, 11)
>>> type(numbers)
<class 'range'>

>>> len(numbers)
6

>>> numbers[0]
5
>>> numbers[-1]
10

>>> for number in numbers:
...     print(number)
...
5
6
7
8
9
10
```


#### Strings

- **Immutable** sequence of characters (e.g., "hello", 'world', """multiline""").
- **Operations**:
    - Concatenation: "a" + "b" → "ab".
    - Repetition: "ha" * 2 → "haha".
    - Slicing: "hello"[1:4] → "ell".
    - Membership: "e" in "hello" → True.
- **Methods**:
    - upper(), lower(): Change case.
    - strip(): Remove whitespace.
    - split(delim): Split into list (e.g., "a,b".split(",") → ["a", "b"]).
    - join(seq): Join sequence (e.g., ",".join(["a", "b"]) → "a,b").

```python
s = "Hello, World"
print(s.lower())      # hello, world
print(s.split(", "))  # ['Hello', 'World']
```

#### Lists

- **Mutable**, ordered sequence of items (e.g., [1, "hi", 3.14]).
- **Operations**:
    - Append: lst.append(item).
    - Remove: lst.remove(item).
    - Indexing: lst[0].
    - Slicing: lst[1:3].
- **Methods**:
    - pop(): Remove and return item.
    - extend(seq): Add multiple items.
```python
lst = [1, 2]
lst.append(3)
print(lst[0:2])  # [1, 2]
```

### Tuples

- **Immutable**, ordered sequence (e.g., (1, 2, "hi")).
- Faster than lists due to immutability.
- **Operations**: Indexing, slicing, concatenation.
```python
tup = (1, 2, 3)
print(tup[1])  # 2
```

#### Dictionaries and Set Types

#### 1. Dictionaries

A **dictionary** is a **mutable**, unordered (before Python 3.7) collection of **key-value pairs**. It stores data as mappings where each **key is **unique** and **immutable** (e.g., strings, numbers, tuples), and each key is associated with a **value** (any type).

- **Syntax**: {key1: value1, key2: value2}.
- **Properties**:
    - Keys must be immutable (e.g., str, int, tuple); values can be mutable or immutable.
    - Unordered in Python 3.6 and earlier; maintains insertion order since Python 3.7.
    - Access time is fast (O(1) average) due to hashing.
- **Operations**:
    - Access: dict[key] (e.g., d["name"]).
    - Update/Add: dict[key] = value (e.g., d["age"] = 20).
    - Delete: del dict[key] (e.g., del d["key"]).
    - Check key: key in dict (e.g., "name" in d → True).
- **Methods**:
    - keys(): Returns all keys (e.g., d.keys()).
    - values(): Returns all values (e.g., d.values()).
    - items(): Returns key-value pairs (e.g., d.items()).
    - get(key, default): Returns value for key or default if key doesn’t exist (e.g., d.get("age", 0)).
    - pop(key): Removes and returns value for key (e.g., d.pop("key")).
- **Example:
```python
d = {"name": "Alice", "age": 20}
d["age"] = 21  # Update
d["city"] = "Delhi"  # Add
print(d)  # {'name': 'Alice', 'age': 21, 'city': 'Delhi'}
del d["city"]           # Delete
print(d.get("name"))  # Alice
print(d.keys())      # dict_keys(['name', 'age'])
```

## 2. Set Types

A **set is a **mutable**, **unordered** collection of **unique** elements (no duplicates). A **frozen set** is an **immutable** version of a set.

- **Syntax**:
    - Set: {1, 2, 3} or set() (empty set).
    - Frozen set: frozenset([1, 2, 3]).
- **Properties**:
    - Elements must be **immutable** (e.g., numbers, strings, tuples).
    - Unordered, no duplicates.
    - Fast membership testing (O(1) average).
    - Used for mathematical set operations.
- **Operations**:
    - Add: set.add(item) (e.g., s.add(4)).
    - Remove: set1 | set2 (union), set1 & set2 (intersection), set1 - set2 (difference).
    - Discard: set.discard(item) (no error if item doesn’t exist).
    - Remove: set.remove(item) (raises error if item doesn’t exist).
- **Methods**:
    - union() or | (e.g., s1.union(s2)).
    - intersection() or & (e.g., s1.intersection(s2)).
    - difference() or - (e.g., s1.difference(s2)).
    - issubset(), issuperset(): Check subset/superset relations.
```python
s = {1, 2, 2}  # Duplicates ignored: {1, 2}
s.add(3)
print(s)  # {1, 2, 3}
s2 = {2, 3, 4}
print(s | s2)  # {1, 2, 3, 4} (union)
print(s & s2)  # {2, 3} (intersection)
fs = frozenset([1, 2])
print(fs)  # frozenset({1, 2})
```

#### Control Flow

**Control flow** determines the order in which Python executes code using conditionals and loops.

- **Conditional Statements**:
    - if, elif, else: Execute code based on conditions.
```python
x = 5
if x > 0:
    print("Positive")  # Positive
elif x == 0:
    print("Zero")
else:
    print("Negative")
```

**Loops**:
- for: Iterates over a sequence (e.g., list, string).
```python
for i in [1, 2, 3]:
    print(i)  # 1, 2, 3
```
  - while: Repeats while a condition is true.
  ```python
  x = 1
while x <= 3:
    print(x)  # 1, 2, 3
    x += 1
```

**Break and Continue**:
- break: Exits the loop.
- continue: Skips to the next iteration.
```python
for i in range(5):
    if i == 3:
        break
    print(i)  # 0, 1, 2
```

#### Truthiness

**Truthiness** refers to how Python evaluates objects as True or False in conditions (e.g., if statements).
- **Falsy Values**: Evaluate to False:
    - 0, 0.0, "" (empty string), [] (empty list), {} (empty dict), () (empty tuple), None, False.
- **Truthy Values**: Evaluate to True:
    - Non-zero numbers (e.g., 1, -1, 3.14), non-empty sequences (e.g., "hi", [1]), True.
```python
x = ""
if x:
    print("Truthy")
else:
    print("Falsy")  # Falsy
y = [1]
if y:
    print("Truthy")  # Truthy
```

refer: https://www.pythonmorsels.com/truthiness/

#### Sorting

**Sorting** arranges elements in a sequence in ascending or descending order.
- **sorted(iterable)**: Returns a new sorted list from any iterable.
    - Parameters: key (custom sorting function), reverse=True (descending).
- **list.sort()**: Sorts a list in place (modifies original).

```python
lst = [3, 1, 2]
print(sorted(lst))      # [1, 2, 3]
lst.sort(reverse=True)
print(lst)              # [3, 2, 1]
print(sorted("hello"))  # ['e', 'h', 'l', 'l', 'o']
```

#### List Comprehensions

**List comprehensions** provide a concise way to create lists using a single line.

- **Syntax**: [expression for item in iterable if condition].
- More readable and efficient than traditional loops.
```python
squares = [x**2 for x in range(5) if x % 2 == 0]
print(squares)  # [0, 4, 16]
# Equivalent loop:
# squares = []
# for x in range(5):
#     if x % 2 == 0:
#         squares.append(x**2)
```

## List Comprehensions

**List comprehensions** provide a concise way to create lists using a single line of code. They are more readable and efficient than traditional loops.

- **Syntax**: [expression for item in iterable if condition]
    - expression: Operation on item.
    - item: Variable representing each element in iterable.
    - iterable: A sequence (e.g., list, string, range).
    - if condition: Optional filter.
- **Purpose**: Generate lists by applying an expression to each item in an iterable, optionally filtering items.

```python
squares = [x**2 for x in range(5)]  # [0, 1, 4, 9, 16]
evens = [x for x in range(10) if x % 2 == 0]  # [0, 2, 4, 6, 8]
```
- **Advantages**:
    - Shorter code compared to loops.
    - Faster execution for simple operations.
- **Example with Loop Equivalent**:
```python
# List comprehension
odds = [x for x in range(5) if x % 2 != 0]  # [1, 3]
# Equivalent loop
odds = []
for x in range(5):
    if x % 2 != 0:
        odds.append(x)
```

## Generators

**Generators** are functions that produce values one at a time, saving memory by not storing the entire sequence in memory at once. They are iterators, created using the yield keyword.
- **Syntax**: Use def with yield to return values incrementally.
- **Purpose**: Efficiently handle large datasets or infinite sequences.
- **Key Features**:
    - Lazy evaluation: Values are generated only when requested.
    - Single-use: Can be iterated over once.
```python
def my_gen():
    yield 1
    yield 2
    yield 3
g = my_gen()
print(next(g))  # 1
print(next(g))  # 2
# Or use a loop
for i in my_gen():
    print(i)  # 1, 2, 3
```
- **Generator Expression**: Similar to list comprehension, but uses () instead of [].
    - Example: squares = (x**2 for x in range(3)) → generates 0, 1, 4 one at a time.

**Iterators** are objects that allow iteration over a sequence (e.g., lists, strings) using iter() and next() functions.

- **Key Functions**:
    - iter(obj): Returns an iterator object for an iterable.
    - next(iterator): Retrieves the next item; raises StopIteration when exhausted.
- **Purpose**: Provide a standard way to traverse sequences.
```python
lst = [1, 2, 3]
it = iter(lst)      # Create iterator
print(next(it))     # 1
print(next(it))     # 2
print(next(it))     # 3
# print(next(it))   # Raises StopIteration
```

- **Relation to Generators**: Generators are a type of iterator, but not all iterators are generators.
- **For Loops**: Internally use iterators to traverse sequences.
  ```python
for x in [1, 2, 3]:  # Uses iter() and next() internally
    print(x)         # 1, 2, 3
```

