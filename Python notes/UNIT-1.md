
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
#### 2.6 Built-in Functions for Numbers

- abs(x): Absolute value (e.g., abs(-5) → 5).
- round(x, n): Rounds to n decimal places (e.g., round(3.14159, 2) → 3.14).
- pow(x, y): x raised to y (e.g., pow(2, 3) → 8).
- divmod(x, y): Returns (x // y, x % y) (e.g., divmod(10, 3) → (3, 1)).
- int(x), float(x), complex(x): Type conversions.

#### Related Modules

- math: Mathematical functions (e.g., math.sqrt(16) → 4.0).
- random: Random number generation (e.g., random.randint(1, 10)).
- decimal: Precise decimal arithmetic (e.g., decimal.Decimal("0.1")).