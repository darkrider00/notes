
 UNIT-II Files: 
File Objects, File Built-in Function [ open() ], File Built-in Methods, File Built-in Attributes, Standard Files, Command-line Arguments, File System, File Execution Exceptions: Exceptions in Python, Detecting and Handling Exceptions, Context Management, Exceptions as Strings, Raising Exceptions, Assertions, Standard Exceptions, Creating Exceptions, Why Exceptions (Now)?, Why Exceptions at All?, Exceptions and the sys Module, Related Modules Modules: Modules and Files, Namespaces, Importing Modules, Importing Module Attributes, Module Built-in Functions, Packages, Other Features of Modules


# File Objects in Python

A file object allows us to use, access and manipulate all the user accessible files. One can read and write any such files. When a file operation fails for an I/O-related reason, the exception IOError is raised. This includes situations where the operation is not defined for some reason, like seek() on a tty device or writing a file opened for reading. Files have the following methods:

### 📌 **Why Use File Objects?**

- To **store** data persistently (beyond program execution).
- To **read from** or **write to** files such as `.txt`, `.csv`, `.json`, etc.
- To interact with the **file system** for data manipulation.


###  File Built-in Function 
- **open():** Opens a file in given access mode.
    
     open(file_address, access_mode) 
    
    Examples of accessing a file: A file can be opened with a built-in function called open(). This function takes in the file’s address and the access_mode and returns a file object. There are different types of access_modes:
    
    **r:** Opens a file for reading only
    **r+:** Opens a file for both reading and writing
    **w:** Opens a file for writing only
    **w+:** Open a file for writing and reading.
    **a:** Opens a file for appending
    **a+:** Opens a file for both appending and reading
    
    When you add 'b' to the access modes you can read the file in binary format rather than the default text format. It is used when the file to be accessed is not in text.
- **read([size])**: It reads the entire file and returns it contents in the form of a string. Reads at most size bytes from the file (less if the read hits EOF before obtaining size bytes). If the size argument is negative or omitted, read all data until EOF is reached.
    
    #### Reading a file
```python
# Reading a file
f = open(__file__, 'r')

#read()
text = f.read(10)

print(text)
f.close()
```
    
- **readline([size])**: It reads the first line of the file i.e till a newline character or an EOF in case of a file having a single line and returns a string. If the size argument is present and non-negative, it is a maximum byte count (including the trailing newline) and an incomplete line may be returned. An empty string is returned only when EOF is encountered immediately.
    
    #### Reading a line in a file
    
```python
# Reading a line in a file
f = open(__file__, 'r')

#readline()
text = f.readline(20)
print(text)
f.close()
```
    
- **readlines([sizehint])**: It reads the entire file line by line and updates each line to a list which is returned.Read until EOF using readline() and return a list containing the lines thus read. If the optional sizehint argument is present, instead of reading up to EOF, whole lines totalling approximately sizehint bytes (possibly after rounding up to an internal buffer size) are read.
    
    #### Reading a file
 ```python
 # Reading a file
f = open(__file__, 'r')

#readline()
text = f.readlines(25)
print(text)
f.close()
```
    
- **write(string)**: It writes the contents of string to the file. It has no return value. Due to buffering, the string may not actually show up in the file until the flush() or close() method is called.
    
    #### Writing a file
    
```python
# Writing a file
f = open(__file__, 'w')
line = 'Welcome Geeks\n'

#write()
f.write(line)
f.close()
```

**More Examples in different modes:**

```python
# Reading and Writing a file
f = open(__file__, 'r+')
lines = f.read()
f.write(lines)
f.close()
```

```python
# Writing and Reading a file
f = open(__file__, 'w+')
lines = f.read()
f.write(lines)
f.close()
```

```python
# Appending a file
f = open(__file__, 'a')
lines = 'Welcome Geeks\n'
f.write(lines)
f.close()
```

```python
# Appending and reading a file
f = open(__file__, 'a+')
lines = f.read()
f.write(lines)
f.close()
```

**writelines(sequence)**: It is a sequence of strings to the file usually a list of strings or any other iterable data type. It has no return value.

```python
# Writing a file
f = open(__file__, 'a+')
lines = f.readlines()

#writelines()
f.writelines(lines)
f.close()
```

**tell()**: It returns an integer that tells us the file object’s position from the beginning of the file in the form of bytes

```python
# Telling the file object position
f = open(__file__, 'r')
lines = f.read(10)

#tell()
print(f.tell())
f.close()
```

**seek(offset, from_where)**: It is used to change the file object’s position. Offset indicates the number of bytes to be moved. from_where indicates from where the bytes are to be moved.

```python
# Setting the file object position
f = open(__file__, 'r')
lines = f.read(10)
print(lines)

#seek()
print(f.seek(2,2))
lines = f.read(10)
print(lines)
f.close()
```

**flush()**: Flush the internal buffer, like stdio‘s fflush(). It has no return value. close() automatically flushes the data but if you want to flush the data before closing the file then you can use this method.

```python
# Clearing the internal buffer before closing the file
f = open(__file__, 'r')
lines = f.read(10)

#flush()
f.flush()
print(f.read())
f.close()
```

**fileno()**: Returns the integer file descriptor that is used by the underlying implementation to request I/O operations from the operating system.

```python
# Getting the integer file descriptor
f = open(__file__, 'r')

#fileno()
print(f.fileno())
f.close()
```

**isatty()**: Returns True if the file is connected to a tty(-like) device and False if not.

```python
# Checks if file is connected to a tty(-like) device
f = open(__file__, 'r')

#isatty()
print(f.isatty())
f.close()
```

**next()**: It is used when a file is used as an iterator. The method is called repeatedly. This method returns the next input line or raises StopIteration at EOF when the file is open for reading( behaviour is undefined when opened for writing).

```python
# Iterates over the file
f = open(__file__, 'r')

#next()
try:
    while f.next():
        print(f.next())
except:
    f.close()
```

**truncate([size])**: Truncate the file's size. If the optional size argument is present, the file is truncated to (at most) that size. The size defaults to the current position. The current file position is not changed. Note that if a specified size exceeds the file's current size, the result is platform-dependent: possibilities include that the file may remain unchanged, increase to the specified size as if zero-filled, or increase to the specified size with undefined new content.

```python
# Truncates the file
f = open(__file__, 'w')

#truncate()
f.truncate(10)
f.close()
```

**close()**: Used to close an open file. A closed file cannot be read or written any more.

```python
# Opening and closing a file
f = open(__file__, 'r')

#close()
f.close()
```


**Attributes**:

- **closed**: returns a boolean indicating the current state of the file object. It returns true if the file is closed and false when the file is open.
- **encoding**: The encoding that this file uses. When Unicode strings are written to a file, they will be converted to byte strings using this encoding.
- **mode**: The I/O mode for the file. If the file was created using the open() built-in function, this will be the value of the mode parameter.
- **name**: If the file object was created using open(), the name of the file.
- **newlines**: A file object that has been opened in universal newline mode have this attribute which reflects the newline convention used in the file. The value for this attribute are "\r", "\n", "\r\n", None or a tuple containing all the newline types seen.
- **softspace**: It is a boolean that indicates whether a space character needs to be printed before another value when using the print statement.

|Attribute|Description|Example|
|---|---|---|
|`name`|Name of the file|`f.name`|
|`mode`|Mode in which the file was opened|`f.mode`|
|`closed`|Boolean – `True` if file is closed|`f.closed`|
|`encoding`|Encoding used (for text files)|`f.encoding` (e.g., `'UTF-8'`)|
|`newlines`|Line ending characters encountered|`f.newlines`


```python
f = open(__file__, 'a+')
print(f.closed)
print(f.encoding)
print(f.mode)
print(f.newlines)
print(f.softspace)
```

# Python File Methods

A file object is created using open() function. The file class defines the following methods with which different file IO operations can be done. The methods can be used with any file like object such as byte stream or network stream.

| Sr.No. | Methods & Description                                                                                                                                                                                                                                                                                       |
| ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1      | file.close()<br><br>Close the file. A closed file cannot be read or written any more.                                                                                                                                                                                                                       |
| 2      | file.flush()<br><br>Flush the internal buffer, like stdio's fflush. This may be a no-op on some file-like objects.                                                                                                                                                                                          |
| 3      | file.fileno()<br><br>Returns the integer file descriptor that is used by the underlying implementation to request I/O operations from the operating system.                                                                                                                                                 |
| 4      | file.isatty()<br><br>Returns True if the file is connected to a tty(-like) device, else False.                                                                                                                                                                                                              |
| 5      | file.next()<br>Returns the next line from the file each time it is being called.                                                                                                                                                                                                                            |
| 6      | file.read([size])<br><br>Reads at most size bytes from the file (less if the read hits EOF before obtaining size bytes).                                                                                                                                                                                    |
| 7      | file.readline([size])<br><br>Reads one entire line from the file. A trailing newline character is kept in the string.                                                                                                                                                                                       |
| 8      | file.readlines([sizehint])<br><br>Reads until EOF using readline() and return a list containing the lines. If the optional sizehint argument is present, instead of reading up to EOF, whole lines totalling approximately sizehint bytes (possibly after rounding up to an internal buffer size) are read. |
| 9      | file.seek(offset[, whence])<br><br>Sets the file's current position                                                                                                                                                                                                                                         |
| 10     | file.tell()<br><br>Returns the file's current position                                                                                                                                                                                                                                                      |
| 11     | file.truncate([size])<br><br>Truncates the file's size. If the optional size argument is present, the file is truncated to (at most) that size.                                                                                                                                                             |
| 12     | file.write(str)<br><br>Writes a string to the file. There is no return value.                                                                                                                                                                                                                               |
| 13     | file.writelines(sequence)<br><br>Writes a sequence of strings to the file. The sequence can be any iterable object producing strings, typically a list of strings.                                                                                                                                          |


### Best Practices

- Always close the file using `f.close()` or use `with` statement.
- Use `'b'` mode for binary files like images, PDFs, etc.
- Use encoding for non-ASCII text: `open('file.txt', 'r', encoding='utf-8')`.

📌 **With Statement Example (Recommended)**:

```python
with open("file.txt", "r") as f:
    data = f.read()
    print(data)
# File is automatically closed
```



### **Standard Files in Python**

Python provides three **standard file objects** that are automatically available when a Python program starts. These are used for basic input/output operations and error handling.

|Standard File|Description|Typical Use|Example|
|---|---|---|---|
|`sys.stdin`|Standard input stream. Usually the keyboard.|Used for reading input|`input_data = sys.stdin.read()`|
|`sys.stdout`|Standard output stream. Usually the screen.|Used for printing output|`sys.stdout.write("Hello\n")`|
|`sys.stderr`|Standard error stream. Usually the screen.|Used for outputting error messages|`sys.stderr.write("Error occurred\n")`|

```
> 💡 **Note**: These are part of the `sys` module, so you need to `import sys` to use them.
```


### **How to Redirect Standard Files**


You can **redirect** these streams to files or other destinations.

```python
import sys

# Redirect stdout to a file
with open('output.txt', 'w') as f:
    sys.stdout = f
    print("This will go to the file, not console.")

# Restore stdout
sys.stdout = sys.__stdout__
print("This goes to the console again.")
```


|Task|Standard File Used|
|---|---|
|Reading user input|`sys.stdin`|
|Printing to terminal|`sys.stdout`|
|Logging or error tracing|`sys.stderr`|
|File redirection in automation|All three|
### **Best Practices**

- Use `print()` for simple output; under the hood, it uses `sys.stdout`.
- Use `sys.stderr` to log errors without mixing them with normal output.
- Always restore standard streams after redirecting if needed.



## Python Command Line Arguments

ython Command Line Arguments provides a convenient way to accept some information at the command line while running the program. We usually pass these values along with the name of the Python script.

To run a Python program, we execute the following command in the command prompt terminal of the operating system. For example, in windows, the following command is entered in Windows command prompt terminal.

```python
$ python script.py arg1 arg2 arg3
```

Here Python script name is **script.py** and rest of the three arguments - arg1 arg2 arg3 are command line arguments for the program.

If the program needs to accept input from the user, Python's input() function is used. When the program is executed from command line, user input is accepted from the command terminal.


```python
name = input("Enter your name: ") print ("Hello {}. How are you?".format(name))
```


![[Pasted image 20250711161534.png]]


## Passing Arguments at the Time of Execution

Very often, you may need to put the data to be used by the program in the command line itself and use it inside the program. An example of giving the data in the command line could be any DOS commands in Windows or Linux.

In Windows, you use the following DOS command to rename a file hello.py to hi.py.

```
```