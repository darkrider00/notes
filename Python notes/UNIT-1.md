
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