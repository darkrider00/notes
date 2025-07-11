
 UNIT-II Files: 
File Objects, File Built-in Function [ open() ], File Built-in Methods, File Built-in Attributes, Standard Files, Command-line Arguments, File System, File Execution Exceptions: Exceptions in Python, Detecting and Handling Exceptions, Context Management, Exceptions as Strings, Raising Exceptions, Assertions, Standard Exceptions, Creating Exceptions, Why Exceptions (Now)?, Why Exceptions at All?, Exceptions and the sys Module, Related Modules Modules: Modules and Files, Namespaces, Importing Modules, Importing Module Attributes, Module Built-in Functions, Packages, Other Features of Modules


File Objects in Python

A file object allows us to use, access and manipulate all the user accessible files. One can read and write any such files. When a file operation fails for an I/O-related reason, the exception IOError is raised. This includes situations where the operation is not defined for some reason, like seek() on a tty device or writing a file opened for reading. Files have the following methods:

📌 **Why Use File Objects?**

- To **store** data persistently (beyond program execution).
- To **read from** or **write to** files such as `.txt`, `.csv`, `.json`, etc.
- To interact with the **file system** for data manipulation.


 File Built-in Function 
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
    
    Reading a file
```python
Reading a file
f = open(__file__, 'r')

#read()
text = f.read(10)

print(text)
f.close()
```
    
- **readline([size])**: It reads the first line of the file i.e till a newline character or an EOF in case of a file having a single line and returns a string. If the size argument is present and non-negative, it is a maximum byte count (including the trailing newline) and an incomplete line may be returned. An empty string is returned only when EOF is encountered immediately.
    
    Reading a line in a file
    
```python
Reading a line in a file
f = open(__file__, 'r')

#readline()
text = f.readline(20)
print(text)
f.close()
```
    
- **readlines([sizehint])**: It reads the entire file line by line and updates each line to a list which is returned.Read until EOF using readline() and return a list containing the lines thus read. If the optional sizehint argument is present, instead of reading up to EOF, whole lines totalling approximately sizehint bytes (possibly after rounding up to an internal buffer size) are read.
    
    Reading a file
 ```python
 Reading a file
f = open(__file__, 'r')

#readline()
text = f.readlines(25)
print(text)
f.close()
```
    
- **write(string)**: It writes the contents of string to the file. It has no return value. Due to buffering, the string may not actually show up in the file until the flush() or close() method is called.
    
    Writing a file
    
```python
Writing a file
f = open(__file__, 'w')
line = 'Welcome Geeks\n'

#write()
f.write(line)
f.close()
```

**More Examples in different modes:**

```python
Reading and Writing a file
f = open(__file__, 'r+')
lines = f.read()
f.write(lines)
f.close()
```

```python
Writing and Reading a file
f = open(__file__, 'w+')
lines = f.read()
f.write(lines)
f.close()
```

```python
Appending a file
f = open(__file__, 'a')
lines = 'Welcome Geeks\n'
f.write(lines)
f.close()
```

```python
Appending and reading a file
f = open(__file__, 'a+')
lines = f.read()
f.write(lines)
f.close()
```

**writelines(sequence)**: It is a sequence of strings to the file usually a list of strings or any other iterable data type. It has no return value.

```python
Writing a file
f = open(__file__, 'a+')
lines = f.readlines()

#writelines()
f.writelines(lines)
f.close()
```

**tell()**: It returns an integer that tells us the file object’s position from the beginning of the file in the form of bytes

```python
Telling the file object position
f = open(__file__, 'r')
lines = f.read(10)

#tell()
print(f.tell())
f.close()
```

**seek(offset, from_where)**: It is used to change the file object’s position. Offset indicates the number of bytes to be moved. from_where indicates from where the bytes are to be moved.

```python
Setting the file object position
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
Clearing the internal buffer before closing the file
f = open(__file__, 'r')
lines = f.read(10)

#flush()
f.flush()
print(f.read())
f.close()
```

**fileno()**: Returns the integer file descriptor that is used by the underlying implementation to request I/O operations from the operating system.

```python
Getting the integer file descriptor
f = open(__file__, 'r')

#fileno()
print(f.fileno())
f.close()
```

**isatty()**: Returns True if the file is connected to a tty(-like) device and False if not.

```python
Checks if file is connected to a tty(-like) device
f = open(__file__, 'r')

#isatty()
print(f.isatty())
f.close()
```

**next()**: It is used when a file is used as an iterator. The method is called repeatedly. This method returns the next input line or raises StopIteration at EOF when the file is open for reading( behaviour is undefined when opened for writing).

```python
Iterates over the file
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
Truncates the file
f = open(__file__, 'w')

#truncate()
f.truncate(10)
f.close()
```

**close()**: Used to close an open file. A closed file cannot be read or written any more.

```python
Opening and closing a file
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

Python File Methods

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


Best Practices

- Always close the file using `f.close()` or use `with` statement.
- Use `'b'` mode for binary files like images, PDFs, etc.
- Use encoding for non-ASCII text: `open('file.txt', 'r', encoding='utf-8')`.

📌 **With Statement Example (Recommended)**:

```python
with open("file.txt", "r") as f:
    data = f.read()
    print(data)
File is automatically closed
```



**Standard Files in Python**

Python provides three **standard file objects** that are automatically available when a Python program starts. These are used for basic input/output operations and error handling.

|Standard File|Description|Typical Use|Example|
|---|---|---|---|
|`sys.stdin`|Standard input stream. Usually the keyboard.|Used for reading input|`input_data = sys.stdin.read()`|
|`sys.stdout`|Standard output stream. Usually the screen.|Used for printing output|`sys.stdout.write("Hello\n")`|
|`sys.stderr`|Standard error stream. Usually the screen.|Used for outputting error messages|`sys.stderr.write("Error occurred\n")`|

```
> 💡 **Note**: These are part of the `sys` module, so you need to `import sys` to use them.
```


**How to Redirect Standard Files**


You can **redirect** these streams to files or other destinations.

```python
import sys

Redirect stdout to a file
with open('output.txt', 'w') as f:
    sys.stdout = f
    print("This will go to the file, not console.")

Restore stdout
sys.stdout = sys.__stdout__
print("This goes to the console again.")
```


|Task|Standard File Used|
|---|---|
|Reading user input|`sys.stdin`|
|Printing to terminal|`sys.stdout`|
|Logging or error tracing|`sys.stderr`|
|File redirection in automation|All three|
**Best Practices**

- Use `print()` for simple output; under the hood, it uses `sys.stdout`.
- Use `sys.stderr` to log errors without mixing them with normal output.
- Always restore standard streams after redirecting if needed.



Python Command Line Arguments

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


Passing Arguments at the Time of Execution

Very often, you may need to put the data to be used by the program in the command line itself and use it inside the program. An example of giving the data in the command line could be any DOS commands in Windows or Linux.

In Windows, you use the following DOS command to rename a file hello.py to hi.py.

```
C:\Python311>ren hello.py hi.py
```

In Linux you may use the mv command −

```
$ mv hello.py hi.py
```

Here ren or mv are the commands which need the old and new file names. Since they are put in line with the command, they are called command-line arguments.

You can pass values to a Python program from command line. Python collects the arguments in a list object. Python's sys module provides access to any command-line arguments via the sys.argv variable. sys.argv is the list of command-line arguments and sys.argv[0] is the program i.e. the script name.


Example

The hello.py script used input() function to accept user input after the script is run. Let us change it to accept input from command line.

```python
import sys print ('argument list', sys.argv) name = sys.argv[1] print ("Hello {}. How are you?".format(name))
```

Run the program from command-line as shown in the following figure −

![[Pasted image 20250711161656.png]]

The **output** is shown below −

```
C:\Python311>python hello.py Rajan
argument list ['hello.py', 'Rajan']
Hello Rajan. How are you?
```

The command-line arguments are always stored in string variables. To use them as numerics, you can them suitably with type conversion functions.

Example

In the following example, two numbers are entered as command-line arguments. Inside the program, we use int() function to parse them as integer variables.

```python
import sys print ('argument list', sys.argv) first = int(sys.argv[1]) second = int(sys.argv[2]) print ("sum = {}".format(first+second))
```

It will produce the following **output** −
```
C:\Python311>python hello.py 10 20 argument list ['hello.py', '10', '20'] sum = 30
```

Python's standard library includes a couple of useful modules to parse command line arguments and options −

```
- **getopt** − C-style parser for command line options.
    
- **argparse** − Parser for command-line options, arguments and sub-commands.
```

Python getopt Module

Python provides a **getopt** module that helps you parse command-line options and arguments. This module provides two functions and an exception to enable command line argument parsing.

getopt.getopt() method

This method parses the command line options and parameter list. Following is a simple syntax for this method −

```
getopt.getopt(args, options, [long_options])
```

detail of the parameters
```
- **args** − This is the argument list to be parsed.
    
- **options** − This is the string of option letters that the script wants to recognize, with options that require an argument should be followed by a colon (:).
    
- **long_options** − This is an optional parameter and if specified, must be a list of strings with the names of the long options, which should be supported. Long options, which require an argument should be followed by an equal sign ('='). To accept only long options, options should be an empty string.
```

This method returns a value consisting of two elements − the first is a list of (option, value) pairs, the second is a list of program arguments left after the option list was stripped.

Each option-and-value pair returned has the option as its first element, prefixed with a hyphen for short options (e.g., '-x') or two hyphens for long options (e.g., '--long-option').


Exception getopt.GetoptError

This is raised when an unrecognized option is found in the argument list or when an option requiring an argument is given none.

The argument to the exception is a string indicating the cause of the error. The attributes msg and opt give the error message and related option.


Example

Suppose we want to pass two file names through command line and we also want to give an option to check the usage of the script. Usage of the script is as follows −

```
Exception getopt.GetoptError This is raised when an unrecognized option is found in the argument list or when an option requiring an argument is given none. 

The argument to the exception is a string indicating the cause of the error. 

The attributes msg and opt give the error message and related option. usage: test.py -i <inputfile> -o <outputfile>
```

Here is the following script to test.py −

```python
import sys
import getopt


def parse_arguments(argv):
    """
    Parse command-line arguments for input and output files.

    Args:
        argv (list): List of command-line arguments.

    Returns:
        tuple: A tuple containing inputfile and outputfile names.

    Raises:
        SystemExit: If argument parsing fails or help option is used.
    """
    inputfile = ''
    outputfile = ''

    try:
        opts, _ = getopt.getopt(argv, "hi:o:", ["ifile=", "ofile="])
    except getopt.GetoptError:
        print('Usage: python structured_script.py -i <inputfile> -o <outputfile>')
        sys.exit(2)

    for opt, arg in opts:
        if opt == '-h':
            print('Usage: python structured_script.py -i <inputfile> -o <outputfile>')
            sys.exit()
        elif opt in ("-i", "--ifile"):
            inputfile = arg
        elif opt in ("-o", "--ofile"):
            outputfile = arg

    return inputfile, outputfile


def main(argv):
    """
    Main function to process input and output file arguments.

    Args:
        argv (list): List of command-line arguments.
    """
    inputfile, outputfile = parse_arguments(argv)
    print(f'Input file is "{inputfile}"')
    print(f'Output file is "{outputfile}"')


if __name__ == "__main__":
    main(sys.argv[1:])

```

Now, run the above script as follows −

```python
$ test.py -h
usage: test.py -i <inputfile> -o <outputfile>
$ test.py -i BMP -o
usage: test.py -i <inputfile> -o <outputfile>
$ test.py -i inputfile -o outputfile
Input file is " inputfile
Output file is " outputfile
```

Python argparse Module

The **argparse** module provides tools for writing very easy to use command line interfaces. It handles how to parse the arguments collected in **sys.argv** list, automatically generate help and issues error message when invalid options are given.

First step to design the command line interface is to set up parser object. This is done by _ArgumentParser()_ function in argparse module. The function can be given an explanatory string as description parameter.

To start with our script will be executed from command line without any arguments. Still use **parse_args()** method of parser object, which does nothing because there aren't any arguments given.

```python
import argparse 
parser=argparse.ArgumentParser(description="sample argument parser") args=parser.parse_args()

```

When the above script is run −


```
C:\Python311>python parser1.py 
C:\Python311>python parser1.py -h 
usage: parser1.py [-h] 
sample argument parser 
options: -h, --help show this help message and exit
```


The second command line usage gives **−help** option which produces a help message as shown. The **−help** parameter is available by default.

Now let us define an argument which is mandatory for the script to run and if not given script should throw error. Here we define argument 'user' by add_argument() method.

```python
import argparse

  
  

def setup_parser():

"""

Set up the argument parser for the command-line interface.

  

Returns:

argparse.ArgumentParser: Configured argument parser.

"""

parser = argparse.ArgumentParser(description="Sample argument parser for user authentication")

parser.add_argument("user", help="Username to check for admin privileges")

return parser

  
  

def main():

"""

Main function to process user argument and print appropriate greeting.

"""

parser = setup_parser()

args = parser.parse_args()

  

if args.user == "Admin":

print("Hello Admin")

else:

print("Hello Guest")

  
  

if __name__ == "__main__":

main()
```


This script's help now shows one positional argument in the form of 'user'. The program checks if it's value is 'Admin' or not and prints corresponding message.

```
C:\Python311>python parser2.py --help usage: parser2.py [-h] user sample argument parser positional arguments: user options: -h, --help show this help message and exit
```


Use the following command −

```
C:\Python311>python parser2.py Admin
Hello Admin
```

The add_argument() method

We can assign default value to an argument in add_argument() method.


```python
import argparse 
parser=argparse.ArgumentParser(description="sample argument parser") 
parser.add_argument("user", nargs='?',default="Admin") args=parser.parse_args()
if args.user=="Admin": 
	print ("Hello Admin") 
else: 
	print ("Hello Guest")
```


Here nargs is the number of command-line arguments that should be consumed. '?'. One argument will be consumed from the command line if possible, and produced as a single item. If no command-line argument is present, the value from default will be produced.

By default, all arguments are treated as strings. To explicitly mention type of argument, use type parameter in the add_argument() method. All Python data types are valid values of type.


```python
import argparse


def setup_parser():
    """
    Set up the argument parser for the command-line interface.

    Returns:
        argparse.ArgumentParser: Configured argument parser for two integers.
    """
    parser = argparse.ArgumentParser(description="Add two numbers")
    parser.add_argument("first", type=int, help="First integer to add")
    parser.add_argument("second", type=int, help="Second integer to add")
    return parser


def main():
    """
    Main function to parse two integer arguments, add them, and print the result.
    """
    parser = setup_parser()
    args = parser.parse_args()

    x = args.first
    y = args.second
    z = x + y

    print(f'Addition of {x} and {y} = {z}')


if __name__ == "__main__":
    main()
```


It will produce the following **output** −

```
C:\Python311>python parser3.py 10 20
addition of 10 and 20 = 30
```

In the above examples, the arguments are mandatory. To add optional argument, prefix its name by double dash --. In following case surname argument is optional because it is prefixed by double dash (--surname).

```python
import argparse
parser=argparse.ArgumentParser()
parser.add_argument("name")
parser.add_argument("--surname")
args=parser.parse_args()
print ("My name is ", args.name, end=' ')
if args.surname:
   print (args.surname)
```


A one letter name of argument prefixed by single dash acts as a short name option.

```
C:\Python311>python parser3.py Anup

My name is Anup

C:\Python311>python parser3.py Anup --surname Gupta

My name is Anup Gupta
```

If it is desired that an argument should value only from a defined list, it is defined as choices parameter.

```python
import argparse

parser=argparse.ArgumentParser()

parser.add_argument("sub", choices=['Physics', 'Maths', 'Biology'])

args=parser.parse_args()

print ("My subject is ", args.sub)

```

Note that if value of parameter is not from the list, invalid choice error is displayed.
```
C:\Python311>python parser3.py Physics

My subject is Physics

C:\Python311>python parser3.py History

usage: parser3.py [-h] {Physics,Maths,Biology}

parser3.py: error: argument sub: invalid choice: 'History' (choose from

'Physics', 'Maths', 'Biology')
```


File System in Python


In python, the file system contains the files and directories. To handle these files and directories python supports “os” module. Python has the “os” module, which provides us with many useful methods to work with directories (and files as well).

The os module provides us the methods that are involved in file processing operations and directory processing like renaming, deleting, get current directory, changing directory etc.


Renaming the file - rename()

The os module provides us the rename() method which is used to rename the specified file to a new name.

_==Syntax:==_  

```python
os.rename (“current-name”, “new-name”)
```

**Example:**

```python
import os;  
#rename file2.txt to file3.txt  
os.rename("file2.txt","file3.txt")
```

Removing the file – remove()

The os module provides us the remove() method which is used to remove the specified file.

_==Syntax:==_  

```python
os.remove(“file-name”)
```

  

**Example:**

```python
import os;  
#deleting the file named file3.txt   
os.remove("file3.txt")
```

Creating the new directory – mkdir()

The mkdir() method is used to create the directories in the current working directory.

_==Syntax:==_  

```python
os.mkdir(“directory-name”)
```

  

**Example:**

```python
import os;  
#creating a new directory with the name new  
os.mkdir("dirnew") 
```

Changing the current working directory – chdir()

The chdir() method is used to change the current working directory to a specified directory.

_==Syntax:==_  

```python
os.chdir("new-directory")
```

  

**Example:**

```python
import os;  
#changing the current working directory to new   
os.chdir("dir2")
```

Get current working directory – getpwd()

This method returns the current working directory.

_==Syntax:==_  

```python
os.getcwd()
```

  

**Example:**

```python
import os;  
#printing the current working directory   
print(os.getcwd())
```

Deleting directory - rmdir()

The rmdir() method is used to delete the specified directory.

_==Syntax:==_  

```python
os.rmdir(“directory name”)
```

  

**Example:**

```python
import os;  
#removing the new directory   
os.rmdir("dir2")
```

List Directories and Files – listdir()

All files and sub directories inside a directory can be known using the listdir() method. This method takes in a path and returns a list of sub directories and files in that path. If no path is specified, it returns from the current working directory.

_==Syntax:==_  

```python
os.listdir([“path”])
```

  

**Example:**

```python
import os;  
#list of files and directories in current working directory   
print(os.listdir())
#list of files and directories in specified path   
print(os.listdir(“D:\\”))
```

# Working with Files and Directories in Python

This guide provides a comprehensive overview of Python's file and directory operations, covering reading/writing files, directory listings, file attributes, archiving, and more. Each section includes practical code examples and explanations to help you understand and apply these concepts effectively.

## Reading and Writing Files with `with open()`

Python's `with open(...) as ...` pattern is a clean and efficient way to handle file operations, ensuring files are properly closed after use. The `open()` function takes a filename and mode (`'r'` for reading, `'w'` for writing) as arguments.

### Example: Reading a File

```python
# Reading the entire content of a text file
with open('data.txt', 'r') as f:
    data = f.read()
    print(data)
```

**Explanation**:

- The `with` statement ensures the file is automatically closed after reading.
- `'r'` mode opens the file for reading.
- `f.read()` retrieves the entire file content as a string.

### Example: Writing to a File

```python
# Writing data to a text file
with open('data.txt', 'w') as f:
    data = 'some data to be written to the file'
    f.write(data)
```

**Explanation**:

- `'w'` mode opens the file for writing, overwriting it if it exists.
- `f.write()` writes the string `data` to the file.
- The `with` statement ensures the file is closed after writing.

For more details, refer to [Reading and Writing Files in Python](https://realpython.com/read-write-files-python/).

## Getting Directory Listings

Python provides multiple ways to list directory contents using the `os` and `pathlib` modules. Modern Python prefers `os.scandir()` or `pathlib.Path()` for efficiency and additional file attribute access.

### Example: Using `os.listdir()`

```python
import os

# List all entries in a directory
entries = os.listdir('my_directory/')
for entry in entries:
    print(entry)
```

**Explanation**:

- `os.listdir()` returns a list of all files and directories in the specified path.
- The example loops through the entries and prints their names.

### Example: Using `os.scandir()`

```python
import os

# List directory contents with scandir()
with os.scandir('my_directory/') as entries:
    for entry in entries:
        print(entry.name)
```

**Explanation**:

- `os.scandir()` returns an iterator of directory entries, which is more memory-efficient than a list.
- The `with` statement ensures the iterator is closed, freeing resources.
- `entry.name` accesses the name of each file or directory.

### Example: Using `pathlib.Path()`

```python
from pathlib import Path

# List directory contents with pathlib
basepath = Path('my_directory/')
for entry in basepath.iterdir():
    print(entry.name)
```

**Explanation**:

- `Path.iterdir()` yields `Path` objects for each entry in the directory.
- `pathlib` provides an object-oriented approach, making it intuitive for file system operations.

## Filtering Files and Directories

To list only files or directories, you can filter the results using `os.path`, `os.scandir()`, or `pathlib.Path()`.

### Example: Listing Files with `os.listdir()`

```python
import os

# List only files using os.listdir()
basepath = 'my_directory/'
for entry in os.listdir(basepath):
    if os.path.isfile(os.path.join(basepath, entry)):
        print(entry)
```

**Explanation**:

- `os.path.isfile()` checks if the entry is a file (not a directory).
- `os.path.join()` constructs the full path to the entry for accurate checking.

### Example: Listing Files with `os.scandir()`

```python
import os

# List only files using scandir()
basepath = 'my_directory/'
with os.scandir(basepath) as entries:
    for entry in entries:
        if entry.is_file():
            print(entry.name)
```

**Explanation**:

- `entry.is_file()` directly checks if the entry is a file.
- This approach is cleaner and more efficient than using `os.listdir()` with `os.path`.

### Example: Listing Files with `pathlib.Path()`

```python
from pathlib import Path

# List only files using pathlib
basepath = Path('my_directory/')
files = [entry.name for entry in basepath.iterdir() if entry.is_file()]
for file in files:
    print(file)
```

**Explanation**:

- Uses a generator expression to filter files with `entry.is_file()`.
- Combines filtering and iteration in a concise, readable way.

## Getting File Attributes

File attributes like size and modification time can be retrieved using `os.scandir()` or `pathlib.Path()`.

### Example: Retrieving File Modification Times

```python
from datetime import datetime
import os

def convert_date(timestamp):
    """Convert timestamp to human-readable date."""
    d = datetime.utcfromtimestamp(timestamp)
    return d.strftime('%d %b %Y')

# Get file attributes with scandir()
with os.scandir('my_directory/') as entries:
    for entry in entries:
        if entry.is_file():
            info = entry.stat()
            print(f'{entry.name}\tLast Modified: {convert_date(info.st_mtime)}')
```

**Explanation**:

- `entry.stat()` retrieves file attributes like `st_mtime` (last modification time).
- `convert_date()` formats the timestamp into a readable date (e.g., "04 Oct 2018").
- Only files are processed, checked with `entry.is_file()`.

## Creating Directories

Python supports creating single or multiple directories using `os` and `pathlib`.

### Example: Creating a Single Directory

```python
from pathlib import Path

# Create a single directory with pathlib
directory = Path('example_directory/')
directory.mkdir(exist_ok=True)
```

**Explanation**:

- `Path.mkdir()` creates a directory at the specified path.
- `exist_ok=True` prevents an error if the directory already exists.

### Example: Creating Multiple Directories

```python
import os

# Create nested directories
os.makedirs('2023/10/05', mode=0o770, exist_ok=True)
```

**Explanation**:

- `os.makedirs()` creates a directory tree, including intermediate directories.
- `mode=0o770` sets permissions (owner and group read/write/execute).
- `exist_ok=True` avoids errors if the directories exist.

## Filename Pattern Matching

Python provides tools like `fnmatch`, `glob`, and `pathlib` for matching filenames against patterns.

### Example: Using `fnmatch` for Pattern Matching

```python
import os
import fnmatch

# Find all .txt files
for file_name in os.listdir('some_directory/'):
    if fnmatch.fnmatch(file_name, '*.txt'):
        print(file_name)
```

**Explanation**:

- `fnmatch.fnmatch()` matches filenames against a wildcard pattern (e.g., `*.txt`).
- Iterates over directory contents to find matching files.

### Example: Using `glob` for Recursive Search

```python
import glob

# Find all .py files recursively
for file in glob.iglob('**/*.py', recursive=True):
    print(file)
```

**Explanation**:

- `glob.iglob()` searches for files matching the pattern recursively.
- `recursive=True` includes subdirectories in the search.

## Creating and Extracting Archives

Python supports ZIP and TAR archives using `zipfile` and `tarfile` modules, with high-level utilities in `shutil`.

### Example: Creating a ZIP Archive

```python
import zipfile

# Create a new ZIP archive
file_list = ['file1.py', 'file2.py']
with zipfile.ZipFile('archive.zip', 'w') as zipobj:
    for name in file_list:
        zipobj.write(name)
```

**Explanation**:

- Opens a ZIP file in write mode (`'w'`), which creates a new archive.
- Adds each file in `file_list` to the archive using `zipobj.write()`.

### Example: Extracting a TAR Archive

```python
import tarfile

# Extract all files from a TAR archive
with tarfile.open('example.tar', 'r') as tar_file:
    tar_file.extractall(path='extracted/')
```

**Explanation**:

- Opens a TAR file in read mode (`'r'`).
- `extractall()` extracts all files to the specified `path`.

## Deleting Files and Directories

Python provides methods to delete files and directories using `os`, `pathlib`, and `shutil`.

### Example: Deleting a File

```python
from pathlib import Path

# Delete a file with pathlib
data_file = Path('data.txt')
try:
    data_file.unlink()
except FileNotFoundError as e:
    print(f'Error: {data_file} : {e.strerror}')
```

**Explanation**:

- `Path.unlink()` deletes the specified file.
- Handles `FileNotFoundError` to avoid crashes if the file doesn't exist.

### Example: Deleting a Directory Tree

```python
import shutil

# Delete a directory and its contents
trash_dir = 'bad_dir'
try:
    shutil.rmtree(trash_dir)
except OSError as e:
    print(f'Error: {trash_dir} : {e.strerror}')
```

**Explanation**:

- `shutil.rmtree()` deletes a directory and all its contents recursively.
- Handles errors like non-empty directories or permissions issues.

## Copying and Moving Files

The `shutil` module provides functions for copying and moving files and directories.

### Example: Copying a File

```python
import shutil

# Copy a file
shutil.copy2('source.txt', 'destination.txt')
```

**Explanation**:

- `shutil.copy2()` copies the file and preserves metadata (e.g., timestamps, permissions).

### Example: Moving a Directory

```python
import shutil

# Move a directory
shutil.move('dir_1/', 'backup/')
```

**Explanation**:

- `shutil.move()` moves the directory to the specified destination.
- If the destination exists, the directory is moved inside it; otherwise, it is renamed.

## Reading Multiple Files with `fileinput`

The `fileinput` module allows reading multiple files sequentially, useful for processing multiple inputs.

### Example: Reading Multiple Files

```python
import fileinput

# Read multiple files and print their contents
for line in fileinput.input(['file1.txt', 'file2.txt']):
    if fileinput.isfirstline():
        print(f'\n--- Reading {fileinput.filename()} ---')
    print(f' -> {line}', end='')
```

**Explanation**:

- `fileinput.input()` accepts a list of files to read.
- `fileinput.isfirstline()` detects the start of a new file.
- `fileinput.filename()` retrieves the current file's name.

## Temporary Files and Directories

The `tempfile` module creates temporary files and directories that are automatically deleted when closed.

### Example: Creating a Temporary File

```python
from tempfile import TemporaryFile

# Create and use a temporary file
with TemporaryFile('w+t') as fp:
    fp.write('Hello universe!')
    fp.seek(0)
    print(fp.read())
```

**Explanation**:

- `TemporaryFile` creates a temporary file in write+text mode (`'w+t'`).
- The file is automatically deleted when the `with` block ends.

### Example: Creating a Temporary Directory

```python
import tempfile
import os

# Create and use a temporary directory
with tempfile.TemporaryDirectory() as tmpdir:
    print(f'Created temporary directory: {tmpdir}')
    print(f'Exists: {os.path.exists(tmpdir)}')
print(f'Exists after context: {os.path.exists(tmpdir)}')
```

**Explanation**:

- `TemporaryDirectory` creates a temporary directory.
- The directory is deleted when the `with` block ends, confirmed by `os.path.exists()`.


## File Exception in Python

Python Exception Handling handles errors that occur during the execution of a program. Exception handling allows to respond to the error, instead of crashing the running program. It enables you to catch and manage errors, making your code more robust and user-friendly. Let's look at an example:

### Handling a Simple Exception in Python

Exception handling helps in preventing crashes due to errors. Here’s a basic example demonstrating how to catch an exception and handle it gracefully:

```python
# Simple Exception Handling Example
n = 10
try:
    res = n / 0  # This will raise a ZeroDivisionError
    
except ZeroDivisionError:
    print("Can't be divided by zero!")
```

**Output**
Can't be divided by zero!

****Explanation:**** In this example, dividing number by 0 raises a [****ZeroDivisionError****](https://www.geeksforgeeks.org/zerodivisionerror-float-division-by-zero-in-python/). The try block contains the code that might cause an exception and the except block handles the exception, printing an error message instead of stopping the program.


## Difference Between Exception and Error

- Error: Errors are serious issues that a program should not try to handle. They are usually problems in the code's logic or configuration and need to be fixed by the programmer. Examples include syntax errors and memory errors.

- Exception: Exceptions are less severe than errors and can be handled by the program. They occur due to situations like invalid input, missing files or network issues.


```python
# Syntax Error (Error)
print("Hello world"  # Missing closing parenthesis

# ZeroDivisionError (Exception)
n = 10
res = n / 0
```

****Explanation:**** A syntax error is a coding mistake that prevents the code from running. In contrast, an exception like ZeroDivisionError can be managed during the program's execution using exception handling.


### Syntax and Usage

Exception handling in Python is done using the try, except, else and finally blocks.

```python
try:  
# Code that might raise an exception  
except SomeException:  
# Code to handle the exception  
else:  
# Code to run if no exception occurs  
finally:  
# Code to run regardless of whether an exception occurs

```

## try, except, else and finally Blocks

- ****try Block****: [try block](https://www.geeksforgeeks.org/python-try-except/) lets us test a block of code for errors. Python will "try" to execute the code in this block. If an exception occurs, execution will immediately jump to the except block.
- ****except Block:**** [except block](https://www.geeksforgeeks.org/python-try-except/) enables us to handle the error or exception. If the code inside the try block throws an error, Python jumps to the except block and executes it. We can handle specific exceptions or use a general except to catch all exceptions.
- ****else Block:**** [else block](https://www.geeksforgeeks.org/try-except-else-and-finally-in-python/) is optional and if included, must follow all except blocks. The else block runs only if no exceptions are raised in the try block. This is useful for code that should execute if the try block succeeds.
- ****finally Block:**** [finally block](https://www.geeksforgeeks.org/finally-keyword-in-python/) always runs, regardless of whether an exception occurred or not. It is typically used for cleanup operations (closing files, releasing resources).

****Example:****

```python
try:
    n = 0
    res = 100 / n
    
except ZeroDivisionError:
    print("You can't divide by zero!")
    
except ValueError:
    print("Enter a valid number!")
    
else:
    print("Result is", res)
    
finally:
    print("Execution complete.")
```

**Output**

You can't divide by zero!
Execution complete.

****Explanation:****

- ****try block**** asks for user input and tries to divide 100 by the input number.
- ****except blocks**** handle ZeroDivisionError and ValueError.
- ****else block**** runs if no exception occurs, displaying the result.
- ****finally block**** runs regardless of the outcome, indicating the completion of execution.

## Common Exceptions in Python

Python has many [built-in exceptions](https://www.geeksforgeeks.org/built-exceptions-python/), each representing a specific error condition. Some common ones include:

|Exception Name|Description|
|---|---|
|`BaseException`|The base class for all built-in exceptions.|
|[`Exception`](https://www.geeksforgeeks.org/python-exception-handling/)|The base class for all non-exit exceptions.|
|`ArithmeticError`|Base class for all errors related to arithmetic operations.|
|[`ZeroDivisionError`](https://www.geeksforgeeks.org/zerodivisionerror-float-division-by-zero-in-python/)|Raised when a division or modulo operation is performed with zero as the divisor.|
|[`OverflowError`](https://www.geeksforgeeks.org/python-overflowerror-math-range-error/)|Raised when a numerical operation exceeds the maximum limit of a data type.|
|[`FloatingPointError`](https://www.geeksforgeeks.org/floating-point-error-in-python/)|Raised when a floating-point operation fails.|
|[`AssertionError`](https://www.geeksforgeeks.org/python-assertion-error/)|Raised when an assert statement fails.|
|[`AttributeError`](https://www.geeksforgeeks.org/python-attributeerror/)|Raised when an attribute reference or assignment fails.|
|[`IndexError`](https://www.geeksforgeeks.org/python-list-index-out-of-range-indexerror/)|Raised when a sequence subscript is out of range.|
|[`KeyError`](https://www.geeksforgeeks.org/how-to-handle-keyerror-exception-in-python/)|Raised when a dictionary key is not found.|
|[`MemoryError`](https://www.geeksforgeeks.org/how-to-handle-the-memoryerror-in-python/)|Raised when an operation runs out of memory.|
|[`NameError`](https://www.geeksforgeeks.org/handling-nameerror-exception-in-python/)|Raised when a local or global name is not found.|
|[`OSError`](https://www.geeksforgeeks.org/handling-oserror-exception-in-python/)|Raised when a system-related operation (like file I/O) fails.|
|[`TypeError`](https://www.geeksforgeeks.org/handling-typeerror-exception-in-python/)|Raised when an operation or function is applied to an object of inappropriate type.|
|[`ValueError`](https://www.geeksforgeeks.org/how-to-fix-valueerror-exceptions-in-python/)|Raised when a function receives an argument of the right type but inappropriate value.|
|[`ImportError`](https://www.geeksforgeeks.org/importerror-unknown-location-in-python/)|Raised when an import statement has issues.|
|[`ModuleNotFoundError`](https://www.geeksforgeeks.org/how-to-fix-the-module-not-found-error/)|Raised when a module cannot be found.|

## Python Catching Exceptions

When working with exceptions in Python, we can handle errors more efficiently by specifying the types of exceptions we expect. This can make code both safer and easier to debug.

### Catching Specific Exceptions

Catching specific exceptions makes code to respond to different exception types differently.

****Example:****

```python
try:
    x = int("str")  # This will cause ValueError
    
    #inverse
    inv = 1 / x
    
except ValueError:
    print("Not Valid!")
    
except ZeroDivisionError:
    print("Zero has no inverse!")
```

**Output**

Not Valid!

****Explanation:****

- The ValueError is caught because the string "str" cannot be converted to an integer.
- If x were 0 and conversion successful, the ZeroDivisionError would be caught when attempting to calculate its inverse.

### Catching Multiple Exceptions

We can catch multiple exceptions in a single block if we need to handle them in the same way or we can separate them if different types of exceptions require different handling.

****Example:****
```python
a = ["10", "twenty", 30]  # Mixed list of integers and strings
try:
    total = int(a[0]) + int(a[1])  # 'twenty' cannot be converted to int
    
except (ValueError, TypeError) as e:
    print("Error", e)
    
except IndexError:
    print("Index out of range.")
```

**Output**

Error invalid literal for int() with base 10: 'twenty'

****Explanation:****

- The ValueError is caught when trying to convert "twenty" to an integer.
- TypeError might occur if the operation was incorrectly applied to non-integer types, but it's not triggered in this specific setup.
- IndexError would be caught if an index outside the range of the list was accessed, but in this scenario, it's under control.

### Catch-All Handlers and Their Risks

Here's a simple calculation that may fail due to various reasons.

****Example:****
```python
try:
    # Simulate risky calculation: incorrect type operation
    res = "100" / 20
    
except ArithmeticError:
    print("Arithmetic problem.")
    
except:
    print("Something went wrong!")
```

  
**Output**

Something went wrong!

****Explanation:****

- An ArithmeticError (more specific like ZeroDivisionError) might be caught if this were a number-to-number division error. However, TypeError is actually triggered here due to attempting to divide a string by a number.
- ****catch-all except:**** is used to catch the TypeError, demonstrating the risk that the programmer might not realize the actual cause of the error (type mismatch) without more detailed error logging.

## Raise an Exception

We [raise](https://www.geeksforgeeks.org/python-raise-keyword/) an exception in Python using the raise keyword followed by an instance of the exception class that we want to trigger. We can choose from built-in exceptions or define our own custom exceptions by inheriting from Python's built-in Exception class.

****Basic Syntax:****

> raise ExceptionType("Error message")

****Example:****
```python
def set(age):
    if age < 0:
        raise ValueError("Age cannot be negative.")
    print(f"Age set to {age}")

try:
    set(-5)
except ValueError as e:
    print(e)
```

**Output**

Age cannot be negative.

****Explanation:****

- The function set checks if the age is negative. If so, it raises a ValueError with a message explaining the issue.
- This ensures that the age attribute cannot be set to an invalid state, thus maintaining the integrity of the data.

### Advantages of Exception Handling:

- ****Improved program reliability****: By handling exceptions properly, you can prevent your program from crashing or producing incorrect results due to unexpected errors or input.
- ****Simplified error handling****: Exception handling allows you to separate error handling code from the main program logic, making it easier to read and maintain your code.
- ****Cleaner code:**** With exception handling, you can avoid using complex conditional statements to check for errors, leading to cleaner and more readable code.
- ****Easier debugging****: When an exception is raised, the Python interpreter prints a traceback that shows the exact location where the exception occurred, making it easier to debug your code.

### Disadvantages of Exception Handling:

- ****Performance overhead:**** Exception handling can be slower than using conditional statements to check for errors, as the interpreter has to perform additional work to catch and handle the exception.
- ****Increased code complexity****: Exception handling can make your code more complex, especially if you have to handle multiple types of exceptions or implement complex error handling logic.
- ****Possible security risks:**** Improperly handled exceptions can potentially reveal sensitive information or create security vulnerabilities in your code, so it's important to handle exceptions carefully and avoid exposing too much information about your program.


### Context Manager in Python

In any programming language, the usage of resources like file operations or database connections is very common. But these resources are limited in supply. Therefore, the main problem lies in making sure to release these resources after usage. If they are not released then it will lead to resource leakage and may cause the system to either slow down or crash.  
Python’s ****context managers**** provide a neat way to automatically set up and clean up resources, ensuring they’re properly managed even if errors occur

## Using the with Statement for File Handling

The simplest way to manage a file resource is using the ****with**** keyword:

```python
with open("test.txt") as f:
    data = f.read()

```

This ensures the file is automatically closed once the block is exited, even if an error occurs.

## What Happens Without Proper Closing?

If files aren’t closed, you can run out of ****available file descriptors****. For example:

```python
file_descriptors = []
for x in range(100000):
    file_descriptors.append(open('test.txt', 'w'))
```

****This will raise:****

> Traceback (most recent call last):  
> File "context.py", line 3, in  
> OSError: [Errno 24] Too many open files: 'test.txt'


Because too many files remain open, exhausting system resource

## Why Use Context Managers?

In complex programs, especially those with multiple exit points or exceptions, manually closing files or connections everywhere is ****error-prone****. Context managers automate this cleanup using the ****with keyword****.

## Creating a Custom Context Manager Class

A class-based context manager needs two methods:

- ****__enter__():**** sets up the resource and returns it.
- ****__exit__():**** cleans up the resource (e.g., closes a file).

```python
class ContextManager:
    def __init__(self):
        print('init method called')
        
    def __enter__(self):
        print('enter method called')
        return self
    
    def __exit__(self, exc_type, exc_value, exc_traceback):
        print('exit method called')

with ContextManager() as manager:
    print('with statement block')
```

Output:

> init method called  
> enter method called  
> with statement block  
> exit method called

The above sequence shows how Python initializes the object, enters the context, runs the block, and then exits while cleaning up.

## File Management Using Context Manager

Let's apply the above concept to create a class that helps in file resource management. The ****FileManager**** class helps in ****opening**** a file, ****writing/reading**** contents, and then ****closing**** it. 

```python
class FileManager:
    def __init__(self, filename, mode):
        self.filename = filename
        self.mode = mode
        self.file = None
        
    def __enter__(self):
        self.file = open(self.filename, self.mode)
        return self.file
    
    def __exit__(self, exc_type, exc_value, exc_traceback):
        self.file.close()

with FileManager('test.txt', 'w') as f:
    f.write('Test')

print(f.closed)
```

****Output:****

> True

****Explanation:****

- ****__enter__()**** opens the file and returns it.
- Inside the with block, you can use the file object.
- ****__exit__()**** ensures the file is closed automatically.
- ****print(f.closed)**** confirms the file is closed.

## Database Connection Management with Context Manager

Let's create a simple database connection management system. The number of database connections that can be opened at a time is also limited(just like file descriptors). Therefore context managers are helpful in managing connections to the database as there could be chances that the programmer may forget to close the connection. 

```python
from pymongo import MongoClient

class MongoDBConnectionManager:
    def __init__(self, hostname, port):
        self.hostname = hostname
        self.port = port
        self.connection = None

    def __enter__(self):
        self.connection = MongoClient(self.hostname, self.port)
        return self.connection

    def __exit__(self, exc_type, exc_value, exc_traceback):
        self.connection.close()

with MongoDBConnectionManager('localhost', 27017) as mongo:
    collection = mongo.SampleDb.test
    data = collection.find_one({'_id': 1})
    print(data.get('name'))
```

****Explanation:****

- ****__enter__()**** opens the MongoDB connection.
- mongo inside the with block is the client object.
- You can perform database operations safely.
- ****__exit__()**** closes the connection automatically.


### Python Exception to string


#### What kind of information can you get from Exceptions?

You can get the following 3 pieces of data from exceptions

- Exception Type,
- Exception Value a.k.a Error Message, and
- Stack-trace or _Traceback_ Object.

All three of the above information is printed out by the Python Interpreter when our program crashes due to an exception as shown in the following example

```python
#Example 1

`>> my_list = [1,2] 
>> print (my_list[3]) 
Traceback (most recent call last):    
		 File "<ipython-input-35-63c7f9106be5>", line 1, in <module>
		 print (my_list[3])  
IndexError: list index out of range`
```

Lines 3,4,5,6 shows the **Stack-trace**  
Line 7 shows the **Exception type** and **Error Message**.

Our focus in this article is to learn **how to extract the above 3 pieces** **individually** in our _except_ clauses and print them out as needed.

Hence, the rest of the article is all about answering the following questions

- what does each of the information in the above list mean,
- how to extract each of these 3 pieces individually and
- how to use these pieces in our programs.

## Piece#1: Printing Exception Type

**The Exception Type refers to _the class_ to which the Exception that you have just caught belongs to**.

### Extracting Piece#1 (Exception Type)

Let us improve our Example 1 above by putting the problematic code into _try_ and _except_ clauses.

```python
```python

def access_list_element():

"""

Attempts to access an element from a list and prints the type of exception if it occurs.

  

Raises:

IndexError: If the index accessed is out of range.

Exception: Catches any other unexpected exceptions.

"""

try:

my_list = [1, 2]

print(my_list[3]) # Attempt to access an index that doesn't exist

except Exception as e:

print(f"Exception type: {type(e).__name__}")

  
  

if __name__ == "__main__":

access_list_element()

```


### Explanation

- **Function Definition**: The code is encapsulated in a function access_list_element() for better modularity and reusability.
- **Docstring**: Added a docstring explaining the function's purpose and possible exceptions.
- **Exception Handling**: The try block attempts to access an out-of-range index (my_list[3]), which raises an IndexError. The except block catches the exception and prints its type using type(e).__name__ for a cleaner output (e.g., IndexError).
- **Main Guard**: The if __name__ == "__main__": block ensures the function runs only when the script is executed directly.
- **Output**: When run, this code will output Exception type: IndexError because the list index is out of range.


Here, in the _try_ clause, we have declared a List named _my_list_ and initialized the list with 2 items. Then we have tried to print the 3rd/non-existent item in the list.

The _except_ clause catches the _IndexError_ exception and prints out Exception type.

On running the code, we will get the following output

```python
<class 'IndexError'>
```

As you can see we just extracted and printed out the information about the class to which the exception that we have just caught belongs to!

But how exactly did we do that?  
If you have a look at the _except_ clause. In the line

```python
except Exception as e:
```


what we have done is, we have assigned the caught exception to an object named “_e”._ Then by using the built-in python function _type()_, we have printed out the class name that the object _e_ belongs to.

```python
print(type(e))
```

### Where to get more details about Exception Types

Now that we have the “Exception Type”, next we will probably need to get some information about that particular type so that we can get a better understanding of why our code has failed. In order to do that, the best place to start is the official documentation.

For built in exceptions you can have a look at the [Python Documentation](https://docs.python.org/3/library/exceptions.html#bltin-exceptions)

For Exception types that come with the libraries that you use with your code, refer to the documentation of your library.

## Piece#2: Printing Exception Value a.k.a Error message

The Exception type is definitely useful for debugging, but, a message like _IndexError_ might sound cryptic and a good understandable error-message will make our job of debugging easier without having to look at the documentation.

In other words, if your program is to be run on the command line and you wish to log why the program just crashed then it is better to use an “Error message” rather than an “Exception Type”.

The example below shows how to print such an Error message.

```pythpn
# Example 3: Print Default Error message
try:
  my_list = [1,2]
  print (my_list[3])
except Exception as e:
  print(e)
```


This will print the default error message as follows

```python
list index out of range
```

Each Exception type comes with its own error message. This can be retrieved using the built-in function _print()_.

Say your program is going to be run by a not-so-tech-savvy user, in that case, you might want to print something friendlier. You can do so by passing in the string to be printed along with the constructor as follows.

```python
# Example 4: Print Custom Error message

try:

raise IndexError('Custom message about IndexError')

except Exception as e:

print(e)
```

This will print

```python
Custom message about IndexError
```

To understand how the built-in function _print()_ does this magic, and see some more examples of manipulating these error messages, I recommend reading my other article in the link below.

If you wish to print both the Error message and the Exception type, which I recommend, you can do so like below.

```python
# Example 5: Print Error message and Exception type

try:

my_list = [1,2]

print (my_list[3])

except Exception as e:

print(repr(e))
```

This will print something like

```python
IndexError('list index out of range')
```

Now that we have understood how to get control over the usage of Pieces 1 and 2, let us go ahead and look at the last and most important piece for debugging, **the stack-trace** which tells us where exactly in our program have the Exception occurred.

## Piece#3: Printing/Logging the stack-trace using the traceback object

Stack-trace in Python is packed into an object named _traceback_ object.

This is an interesting one as the _traceback_ class in Python comes with several useful methods to exercise complete control over what is printed.

Let us see how to use these options using some examples!

```python
# Example 6: Print or Log the entire traceback Message

import traceback

try:

my_list = [1,2]

print (my_list[3])

except Exception:

traceback.print_exc()
```

This will print something like

```python
Traceback (most recent call last):
  File "<ipython-input-38-f9a1ee2cf77a>", line 5, in <module>
    print (my_list[3])
IndexError: list index out of range
```


which contains the entire error messages printed by the Python interpreter if we fail to handle the exception.

Here, instead of crashing the program, we have printed this entire message using our exception handler with the help of the _print_exc()_ method of the _traceback_ class.

The above Example-6 is too simple, as, in the real-world, we will normally have several nested function calls which will result in a deeper stack. Let us


```python
# Example 7: A Deeper Stack with several function calls

def func3():

my_list = [1,2]

print (my_list[3])

def func2():

print('calling func3')

func3()

def func1():

print('calling func2')

func2()

try:

print('calling func1')

func1()

except Exception as e:

traceback.print_exc()
```

Here in the _try_ clause we call _func1()_, which in-turn calls _func2()_, which in-turn calls _func3()_, which produces an IndexError. Running the code above we get the following output

```python
calling func1
calling func2
calling func3
Traceback (most recent call last):
  File "<ipython-input-42-2267707e164f>", line 15, in <module>
    func1()
  File "<ipython-input-42-2267707e164f>", line 11, in func1
    func2()
  File "<ipython-input-42-2267707e164f>", line 7, in func2
    func3()
  File "<ipython-input-42-2267707e164f>", line 3, in func3
    print (my_list[3])
IndexError: list index out of range
```

Say we are not interested in some of the above information. Say we just want to print out the Traceback and skip the error message and Exception type (the last line above), then we can modify the code like shown below.

# Example 8: Skipping the last line of Traceback

```python
# Example 8: Skipping the last line of Traceback

def func3():

my_list = [1,2]

print (my_list[3])

def func2():

func3()

def func1():

func2()

try:

func1()

except Exception as e:

traceback_lines = traceback.format_exc().splitlines()

for line in traceback_lines:

if line != traceback_lines[-1]:

print(line)
```

Here we have used the _format_exc()_ method available in the _traceback_ class to get the traceback information as a string and used _splitlines()_ method to transform the string into a list of lines and stored that in a list object named _traceback_lines_

Then with the help of a simple _for_ loop we have skipped printing the last line with index of -1 to get an output like below

```python
Traceback (most recent call last):
  File "<ipython-input-43-aff649563444>", line 3, in <module>
    func1()
  File "<ipython-input-42-2267707e164f>", line 11, in func1
    func2()
  File "<ipython-input-42-2267707e164f>", line 7, in func2
    func3()
  File "<ipython-input-42-2267707e164f>", line 3, in func3
    print (my_list[3])
```

Another interesting variant of formatting the information in the traceback object is to control the depth of stack that is actually printed out.

If your program uses lots of external library code, odds are the stack will get very deep, and printing out each and every level of function call might not be very useful. If you ever find yourself in such a situation you can set the _limit_ argument in the _print_exc()_ method like shown below.

```python
traceback.print_exc(limit=2, file=sys.stdout)
```

This will limit the number of levels to 2. Let us use this line of code in our Example and see how that behaves


## Best Practices while Printing Exception messages

### When to Use Which Piece

- **Use Piece#1 only on very short programs and only during the development/testing phase** to get some clues on the Exceptions without letting the interpreter crash your program. Once finding out, implement specific handlers to do something about these exceptions. If you are not sure how to handle the exceptions have a look at my other article below where I have explained 3 ways to handle Exceptions  
    [Exceptions in Python: Everything You Need To Know!](https://embeddedinventor.com/exceptions-in-python-everything-you-need-to-know/)
- **Use Piece#2 to print out some friendly information either for yourself or for your user** to inform them what exactly is happening.
- **Use all 3 pieces on your finished product**, so that if an exception ever occurs while your program is running on your client’s computer, you can log the errors and have use that information to fix your bugs.

### Where to print

One point worth noting here is that the default file that _print()_ uses is the _stdout_ file stream and not the _stderr_ stream. To use _stderr_ instead, you can modify the code like this

```python
Example 10: Where to print error messages

`import sys try:   #some naughty statements that irritate us with exceptions except Exception as e:   print(e, file=sys.stderr)`

```


The above code is considered better practice, as errors are meant to go to _stderr_ and not _stdout_.

You can always print these into a separate log file too if that is what you need. This way, you can organize the logs collected in a better manner by separating the informational printouts from the error printouts.


**Why exceptions at all?** 

Python exceptions provide a mechanism for handling errors that occur during the execution of a program. Unlike syntax errors, which are detected by the parser, Python raises exceptions when an error occurs in syntactically correct code.

Knowing how to raise, catch, and handle exceptions effectively helps to ensure your program behaves as expected, even when encountering errors.

- Exceptions in Python occur when **syntactically correct code** results in an **error**.
- **The `try` … `except` block** lets you execute code and handle exceptions that arise.
- You can use the `else`, and `finally` **keywords** for more refined **exception handling**.
- It’s **bad practice** to **catch all exceptions** at once using `except Exception` or the bare `except` clause.
- Combining `try`, `except`, and `pass` allows your program to **continue silently** without handling the exception.


### sys Module

The ****sys module**** in [Python](https://www.geeksforgeeks.org/python-programming-language-tutorial/) provides access to variables and functions that interact closely with the Python interpreter and runtime environment. It allows developers to manipulate various aspects of program execution and the interpreter itself. It's Key capabilities include:

- Accessing command-line arguments.
- Fetching the Python interpreter version.
- Redirecting input/output streams, such as sys.stdin, sys.stdout and sys.stderr.
- Exiting the program gracefully.
- Handling exceptions and configuring interpreter settings.

```python
import sys
print(sys.version)
```

****Output****

3.6.9 (default, Oct  8 2020, 12:12:24)  
[GCC 8.4.0]

****Explanation:**** This code prints the version of the Python interpreter currently in use, which helps in identifying compatibility and environment details.

## Input and Output using Python sys

The ****sys module**** controls program input, output, and error streams, enabling precise data handling beyond standard input and print functions.

****1. sys.stdin:**** Reads input directly from the standard input stream and supports reading multiple lines or redirected input.

```python
import sys

for line in sys.stdin:
    if 'q' == line.rstrip():
        break
    print(f'Input : {line}')
print("Exit")

```

****2. sys.stdout:**** Writes output to the standard output stream and allows low-level control over printed output.

```python
import sys
sys.stdout.write('Geeks')
```

****Output****
Geeks

****3. sys.stderr:**** Writes messages to the standard error stream and separates error messages from regular output

```python
import sys
def fun(*args):
    print(*args, file=sys.stderr)

fun("Hello World")
```

## Command-Line Arguments

Command-line arguments are those which are passed during the calling of the program along with the calling statement. To achieve this using the sys module, the sys module provides a variable called sys.argv. It's main purpose are:

- It is a list of command-line arguments.
- len(sys.argv) provides the number of command-line arguments.

```python
import sys
n = len(sys.argv)

print("Total arguments passed:", n)
print("Name of Python script:", sys.argv[0])
print("Arguments passed:", end=" ")

for i in range(1, n):
    print(sys.argv[i], end=" ")

Sum = 0
for i in range(1, n):
    Sum += int(sys.argv[i])

print(Sum)
```

![[Pasted image 20250711170502.png]]
****Explanation:**** This code sums the command-line arguments passed to the script by converting each to an integer and adding them up using the sys module.

### Exiting the Program

****sys.exit([arg])**** can be used to exit the program. The optional argument arg can be an integer giving the exit or another type of object. If it is an integer, zero is considered "successful termination".

> Note: A string can also be passed to the sys.exit() method.

```python
import sys
age = 17
if age < 18:
    sys.exit("Age less than 18")
else:
    print("Age is not less than 18")
```


****Output****
An exception has occurred, use %tb to see the full traceback.   
SystemExit: Age less than 18

****Explanation:**** This code uses sys****.exit()**** to terminate the program if age is less than 18, displaying a message otherwise, it prints that the age is not less than 18.

## Working with Modules

[sys.path](https://www.geeksforgeeks.org/sys-path-in-python/) is a list in the sys module that defines directories Python searches for modules after checking built-ins. As a regular list, it can be modified at runtime to add, remove or reorder paths.
> ****Note:**** sys.path is an ordinary list and can be manipulated.

****Example 1:**** Listing all paths
```python
import sys

print(sys.path)
```

![[Pasted image 20250711170726.png]]


****Explanation:**** This code will print the system paths that Python uses to search for modules. The ****sys.path**** list contains the directories that Python will search for modules when it imports them.

****Example 2:**** Truncating sys.path
```python
import sys
sys.path = []
import pandas
```

ModuleNotFoundError: No module named 'pandas'

****Explanation:**** This code will raise an error because the pandas module cannot be found if sys.path is emptied. By setting ****sys.path**** to an empty list, Python is prevented from locating any modules outside built-ins.

## sys.modules()

****sys.modules**** is a dictionary that contains all the modules currently imported in the Python interpreter. The keys are module names, and the values are the corresponding module objects. Example:


```python
import sys
print(sys.modules)
```

output:

![[Pasted image 20250711170806.png]]

****Explanation:**** This code will print a dictionary of all the modules that have been imported by the current Python interpreter. The dictionary keys are the module names, and the dictionary values are the module objects.

## Reference Count

****sys.getrefcount()**** method is used to get the reference count for any given object. This value is used by Python as when this value becomes 0, the memory for that particular value is deleted. Example:

```python
import sys
a = 'Geeks'
print(sys.getrefcount(a))
```

**Output**

4

****Explanation:****This code prints the reference count of the object a, which indicates how many times it is referenced. When the count reaches 0, the object is no longer used and is garbage collected.

## More Functions in Python sys

|Function|Description|
|---|---|
|[sys.setrecursionlimit()](https://www.geeksforgeeks.org/python-sys-setrecursionlimit-method/)|sys.setrecursionlimit() method is used to set the maximum depth of the Python interpreter stack to the required limit.|
|[sys.getrecursionlimit() method](https://www.geeksforgeeks.org/python-sys-getrecursionlimit-method/)|sys.getrecursionlimit() method is used to find the current recursion limit of the interpreter or to find the maximum depth of the Python interpreter stack.|
|[sys.settrace()](https://www.geeksforgeeks.org/python-sys-settrace/)|It is used for implementing debuggers, profilers and coverage tools. This is thread-specific and must register the trace using threading.settrace(). On a higher level, sys.settrace() registers the traceback to the Python interpreter|
|[sys.setswitchinterval() method](https://www.geeksforgeeks.org/python-sys-setswitchinterval-method/)|sys.setswitchinterval() method is used to set the interpreter’s thread switch interval (in seconds).|
|[sys.maxsize()](https://www.geeksforgeeks.org/sys-maxsize-in-python/)|It fetches the largest value a variable of data type Py_ssize_t can store.|
|[sys.maxint](https://www.geeksforgeeks.org/sys-maxint-in-python/)|maxint/INT_MAX denotes the highest value that can be represented by an integer.|
|[sys.getdefaultencoding() method](https://www.geeksforgeeks.org/python-sys-getdefaultencoding-method/)|sys.getdefaultencoding() method is used to get the current default string encoding used by the Unicode implementation.|


# Python Modules and File Operations

This guide covers Python modules, namespaces, file operations, and related concepts, with practical examples and exercise solutions. It is designed to help you understand how to create and use modules, manage namespaces, work with files, and apply these concepts to solve problems.

## 1. Understanding Modules

A **module** is a Python file (`.py`) containing definitions and statements that can be imported into other programs. Python's standard library includes many modules, such as `doctest` and `string`, which provide reusable functionality.

### Example: Using the `keyword` Module

```python
from keyword import iskeyword, kwlist

# Check if a string is a Python keyword
print(iskeyword('for'))  # True
print(iskeyword('all'))  # False

# List all Python keywords
print(kwlist)
# Output: ['and', 'as', 'assert', 'break', 'class', 'continue', 'def', ...]
```

**Explanation**:

- The `keyword` module provides `iskeyword()`, a boolean function that checks if a string is a Python keyword.
- `kwlist` is a data attribute containing a list of all Python keywords.
- Use `pydoc` to explore other standard library modules (e.g., `pydoc -g` or `pydoc -p 7464`).

## 2. Creating Modules

You can create a module by saving a `.py` file with functions, variables, or other definitions.

### Example: Creating and Using a `seqtools` Module

```python
# seqtools.py
def remove_at(pos, seq):
    """
    Remove character at position pos from sequence seq.
    >>> remove_at(4, 'A string!')
    'A sting!'
    """
    return seq[:pos] + seq[pos+1:]
```

**Usage in Python Shell**:

```python
# Option 1: Import specific function
from seqtools import remove_at
s = "A string!"
print(remove_at(4, s))  # Output: A sting!

# Option 2: Import module
import seqtools
print(seqtools.remove_at(4, s))  # Output: A sting!
```

**Explanation**:

- Save the code in a file named `seqtools.py`.
- Import the module or specific functions without the `.py` extension.
- Use the dot operator (`.`) to access module attributes or functions.

## 3. Namespaces

A **namespace** is a container that allows the same name to be used in different contexts without ambiguity. Modules and functions each have their own namespaces.

### Example: Namespaces in Modules

```python
# module1.py
question = "What is the meaning of life, the Universe, and everything?"
answer = 42

# module2.py
question = "What is your quest?"
answer = "To seek the holy grail."

# namespace_test.py
import module1
import module2

print(module1.question)  # What is the meaning of life, the Universe, and everything?
print(module2.question)  # What is your quest?
print(module1.answer)    # 42
print(module2.answer)    # To seek the holy grail.
```

**Explanation**:

- Each module (`module1`, `module2`) has its own namespace, preventing naming collisions.
- Use `import module` to preserve namespaces, avoiding conflicts compared to `from module import *`.

### Example: Namespaces in Functions

```python
def f():
    n = 7
    print(f"printing n inside of f: {n}")

def g():
    n = 42
    print(f"printing n inside of g: {n}")

n = 11
print(f"printing n before calling f: {n}")
f()
print(f"printing n after calling f: {n}")
g()
print(f"printing n after calling g: {n}")
```

**Output**:

```
printing n before calling f: 11
printing n inside of f: 7
printing n after calling f: 11
printing n inside of g: 42
printing n after calling g: 11
```

**Explanation**:

- Each function (`f`, `g`) has its own namespace, so `n` inside `f` and `g` doesn't affect the global `n`.
- Namespaces isolate variables, allowing multiple programmers to work without collisions.

## 4. Attributes and the Dot Operator

Module attributes (variables, functions) are accessed using the dot operator (`.`).

### Example: String Module Functions

```python
import string

print(string.capitalize('maryland'))  # Output: Maryland
print(string.capwords("what's all this, then, amen?"))  # Output: What's All This, Then, Amen?
print(string.center('How to Center Text', 70))  # Output: centered text
print(string.upper('angola'))  # Output: ANGOLA
```

**Explanation**:

- The `string` module provides functions like `capitalize`, `capwords`, `center`, and `upper`.
- Access them using `string.function_name()`.

### Example: String and List Methods

```python
# String methods
s = 'maryland'
print(s.capitalize())  # Output: Maryland
print(s.upper())  # Output: MARYLAND

# List methods
mylist = []
mylist.append(5)
mylist.append(27)
mylist.append(3)
mylist.append(12)
print(mylist)  # Output: [5, 27, 3, 12]
mylist.insert(1, 12)
print(mylist.count(12))  # Output: 2
mylist.extend([5, 9, 5, 11])
print(mylist.index(9))  # Output: 6
mylist.reverse()
mylist.sort()
mylist.remove(12)
print(mylist)  # Output: [3, 5, 5, 5, 9, 11, 12, 27]
```

**Explanation**:

- String methods (e.g., `capitalize`, `upper`) are invoked on string objects.
- List methods (e.g., `append`, `insert`, `count`, `extend`, `index`, `reverse`, `sort`, `remove`) modify or query lists.

## 5. Reading and Writing Text Files

Files store data in non-volatile memory. Python uses the `open()` function to read or write files.

### Example: Writing to a File

```python
# Write to a file
with open('test.dat', 'w') as myfile:
    myfile.write("Now is the time")
    myfile.write("to close the file")
```

**Explanation**:

- `'w'` mode creates or overwrites the file.
- The `with` statement ensures the file is closed after writing.

### Example: Reading from a File

```python
# Read from a file
with open('test.dat', 'r') as myfile:
    text = myfile.read()
    print(text)  # Output: Now is the timeto close the file
```

**Explanation**:

- `'r'` mode opens the file for reading.
- `read()` retrieves the entire file content as a string.

### Example: Copying a File

```python
def copy_file(oldfile, newfile):
    """
    Copy content from oldfile to newfile, 50 characters at a time.
    """
    with open(oldfile, 'r') as infile, open(newfile, 'w') as outfile:
        while True:
            text = infile.read(50)
            if text == "":
                break
            outfile.write(text)
```

**Explanation**:

- Reads 50 characters at a time until the file ends (`text == ""`).
- Uses `with` to handle file closing automatically.

## 6. Processing Text Files

Text files are processed line by line using methods like `readline()` and `readlines()`.

### Example: Writing and Reading Lines

```python
# Write lines to a file
with open("test.dat", "w") as outfile:
    outfile.write("line one\nline two\nline three\n")

# Read lines
with open("test.dat", "r") as infile:
    print(infile.readline())  # Output: line one
    print(infile.readlines())  # Output: ['line two\n', 'line three\n']
```

**Explanation**:

- `write()` adds newline characters (`\n`) to separate lines.
- `readline()` reads one line, including the newline.
- `readlines()` returns remaining lines as a list.

### Example: Filtering Lines

```python
def filter(oldfile, newfile):
    """
    Copy oldfile to newfile, omitting lines starting with '#'.
    """
    with open(oldfile, 'r') as infile, open(newfile, 'w') as outfile:
        while True:
            text = infile.readline()
            if text == "":
                break
            if text[0] == '#':
                continue
            outfile.write(text)
```

**Explanation**:

- `readline()` reads one line at a time.
- `continue` skips lines starting with `#`.
- The loop ends when an empty string is read.

## 7. Directories and File Paths

Files are organized in directories, and paths specify their location.

### Example: Reading a File with a Path

```python
with open('/usr/share/dict/words', 'r') as wordsfile:
    wordlist = wordsfile.readlines()
    print(wordlist[:6])  # Output: ['\n', 'A\n', "A's\n", 'AOL\n', "AOL's\n", 'Aachen\n']
```

**Explanation**:

- The path `/usr/share/dict/words` points to a file in a Unix system.
- `readlines()` reads all lines into a list.

## 8. Counting Letters with `ord` and `chr`

The `ord()` function returns a character's ASCII code, and `chr()` converts an integer to a character.

### Example: Using `ord` and `chr`

```python
print(ord('a'))  # Output: 97
print(chr(65))   # Output: A
```

**Explanation**:

- `ord('a')` returns 97, the ASCII code for lowercase 'a'.
- `chr(65)` returns 'A', the character for ASCII code 65.

## 9. The `sys` Module and Command Line Arguments

The `sys` module provides access to system-specific variables and functions, including `argv` for command-line arguments.

### Example: Using `sys.argv`

```python
# demo_argv.py
import sys

print(sys.argv)  # Output: ['demo_argv.py', 'this', 'and', 'that', '1', '2', '3']
```

**Command Line**:

```bash
$ python demo_argv.py this and that 1 2 3
```

**Explanation**:

- `sys.argv` is a list where the first element is the script name, followed by command-line arguments.
- Arguments with spaces must be quoted (e.g., `"this and"`).

## 10. Exercise Solutions

Below are solutions to the exercises, structured as Python scripts with explanations.

### Exercise 1: Exploring the `calendar` Module

**Task**: Use `pydoc` to explore the `calendar` module and test `calendar` and `isleap`.

```python
import calendar

# Print a yearly calendar
year = calendar.calendar(2008)
print(year)  # Outputs a formatted calendar for 2008

# Test isleap
print(calendar.isleap(2008))  # Output: True (2008 is a leap year)
print(calendar.isleap(2007))  # Output: False
```

**Explanation**:

- `calendar.calendar(year)` generates a text calendar for the given year.
- `calendar.isleap(year)` takes an integer year and returns `True` if it's a leap year, `False` otherwise.
- **Notes**: A leap year is divisible by 4, except for century years not divisible by 400.

### Exercise 2: Exploring the `math` Module

**Task**: Use `pydoc` to explore the `math` module.

```python
import math

# Test ceil and floor
print(math.ceil(4.2))   # Output: 5.0
print(math.floor(4.2))  # Output: 4.0

# Square root equivalent
x = 16
sqrt = x ** 0.5  # Same as math.sqrt(16)
print(sqrt)  # Output: 4.0

# Data constants
print(math.pi)  # Output: 3.141592653589793
print(math.e)   # Output: 2.718281828459045
```

**Explanation**:

- **Functions**: `math.ceil(x)` rounds up to the nearest integer; `math.floor(x)` rounds down.
- **Square Root**: `x ** 0.5` computes the square root without `math.sqrt`.
- **Constants**: `math.pi` and `math.e` are predefined constants.
- **Total Functions**: The `math` module has around 50 functions (check `pydoc math`).

### Exercise 3: Exploring the `copy` Module

**Task**: Investigate `deepcopy` and identify where it would be useful.

```python
import copy

nested_list = [[1, 2], [3, 4]]
shallow_copy = nested_list.copy()
deep_copy = copy.deepcopy(nested_list)

shallow_copy[0][0] = 99
print(nested_list)  # Output: [[99, 2], [3, 4]]
print(deep_copy)    # Output: [[1, 2], [3, 4]]
```

**Explanation**:

- `copy.deepcopy()` creates a fully independent copy of an object, including nested structures.
- Useful in exercises involving complex data structures (e.g., matrix multiplication from the previous chapter) to avoid modifying the original data.
- **Note**: Shallow copies only copy the top-level structure, leaving nested objects shared.

### Exercise 4: Creating Modules and Testing Namespaces

**Task**: Create `mymodule1.py`, `mymodule2.py`, and `namespace_test.py`.

```python
# mymodule1.py
myage = 30  # Your current age
year = 2025  # Current year
print("My name is %s" % __name__)

if __name__ == '__main__':
    print("This won't run if I'm imported.")
```

```python
# mymodule2.py
myage = 0    # Age at birth
year = 1995  # Year of birth
print("My name is %s" % __name__)

if __name__ == '__main__':
    print("This won't run if I'm imported.")
```

```python
# namespace_test.py
import mymodule1
import mymodule2

print((mymodule2.myage - mymodule1.myage) == (mymodule2.year - mymodule1.year))
print("My name is %s" % __name__)
```

**Explanation**:

- **Output**: Running `namespace_test.py` prints `True` or `False` based on age/year differences, followed by `My name is __main__` for `namespace_test.py` and `My name is mymodule1`/`mymodule2` for imports.
- `__name__` is `__main__` when a script is run directly, otherwise it’s the module name when imported.
- The `if __name__ == '__main__':` block in `mymodule1.py` only runs when executed directly, not when imported.

### Exercise 5: Exploring `this` Module

**Task**: Import `this` and note Tim Peters' comments on namespaces.

```python
import this
```

**Explanation**:

- The `this` module prints "The Zen of Python" by Tim Peters.
- On namespaces, it says: "Namespaces are one honking great idea -- let's do more of those!"
- This emphasizes the importance of namespaces for organizing code and avoiding naming conflicts.

### Exercise 6: Exploring `string` Module Functions

**Task**: Test three functions from the `string` module.

```python
import string

print(string.lower('ANGOLA'))  # Output: angola
print(string.strip('  hello  '))  # Output: hello
print(string.replace('hello world', 'world', 'Python'))  # Output: hello Python
```

**Explanation**:

- `string.lower(s)` converts a string to lowercase.
- `string.strip(s)` removes leading/trailing whitespace.
- `string.replace(s, old, new)` replaces all occurrences of `old` with `new`.

### Exercise 7: Rewriting `matrix_mult` with List Methods

**Task**: Rewrite `matrix_mult` using list methods (assuming a matrix multiplication function from a previous chapter).

```python
def matrix_mult(A, B):
    """
    Multiply two matrices A and B.
    >>> matrix_mult([[1, 2], [3, 4]], [[5, 6], [7, 8]])
    [[19, 22], [43, 50]]
    """
    result = []
    for i in range(len(A)):
        row = []
        for j in range(len(B[0])):
            product = sum(A[i][k] * B[k][j] for k in range(len(B)))
            row.append(product)
        result.append(row)
    return result
```

**Explanation**:

- Uses `append` to build rows and the result matrix.
- `sum()` with a generator expression computes the dot product for each element.
- List methods simplify matrix construction compared to manual indexing.

### Exercise 8: Exploring `str` and `list` Methods with `dir`

**Task**: Use `dir(str)` and `dir(list)` to find new methods.

```python
# String methods
s = "hello world"
print(s.join(['a', 'b']))  # Output: ahello worldb
print(s.find('o'))  # Output: 4
print(s.rjust(15))  # Output:     hello world

# List methods
lst = [1, 2, 3]
lst.pop(1)
print(lst)  # Output: [1, 3]
lst.clear()
print(lst)  # Output: []
lst.extend([4, 5])
print(lst)  # Output: [4, 5]
```

**Explanation**:

- **String Methods**:
    - `join(iterable)`: Joins iterable elements with the string as a separator.
    - `find(sub)`: Returns the lowest index of `sub` or -1 if not found.
    - `rjust(width)`: Right-justifies the string to the specified width.
- **List Methods**:
    - `pop(index)`: Removes and returns the item at `index`.
    - `clear()`: Removes all items from the list.
    - `extend(iterable)`: Adds all items from `iterable` to the list.

### Exercise 9: Implementing `myreplace`

**Task**: Implement `myreplace` using `split` and `join`.

```python
def myreplace(old, new, s):
    """
    Replace all occurrences of old with new in the string s.
    >>> myreplace(',', ';', 'this, that, and, some, other, thing')
    'this; that; and; some; other; thing'
    >>> myreplace(' ', '**', 'Words will now be separated by stars.')
    'Words**will**now**be**separated**by**stars.'
    """
    return new.join(s.split(old))
```

**Explanation**:

- `s.split(old)` splits the string into a list at each occurrence of `old`.
- `new.join(...)` joins the list elements with `new` as the separator.
- Passes all doctests by correctly replacing all instances of `old` with `new`.

### Exercise 10: Creating `wordtools.py` Module

**Task**: Implement functions in `wordtools.py` with doctests.

```python
# wordtools.py
def cleanword(word):
    """
    Remove non-alphabetic characters from a word.
    >>> cleanword('what?')
    'what'
    >>> cleanword('"now!"')
    'now'
    >>> cleanword('?+="word!,@$()"')
    'word'
    """
    return ''.join(c for c in word if c.isalpha())

def has_dashdash(s):
    """
    Check if a string contains '--'.
    >>> has_dashdash('distance--but')
    True
    >>> has_dashdash('several')
    False
    >>> has_dashdash('spoke--fancy')
    True
    """
    return '--' in s

def extract_words(s):
    """
    Extract alphabetic words from a string, converting to lowercase.
    >>> extract_words('Now is the time!  "Now", is the time? Yes, now.')
    ['now', 'is', 'the', 'time', 'now', 'is', 'the', 'time', 'yes', 'now']
    >>> extract_words('she tried to curtsey as she spoke--fancy')
    ['she', 'tried', 'to', 'curtsey', 'as', 'she', 'spoke', 'fancy']
    """
    return [cleanword(word).lower() for word in s.split() if cleanword(word)]

def wordcount(word, wordlist):
    """
    Count occurrences of a word in a wordlist.
    >>> wordcount('now', ['now', 'is', 'time', 'is', 'now', 'is', 'is'])
    ['now', 2]
    >>> wordcount('is', ['now', 'is', 'time', 'is', 'now', 'is', 'the', 'is'])
    ['is', 4]
    """
    return [word, wordlist.count(word)]

def wordset(wordlist):
    """
    Return a sorted list of unique words.
    >>> wordset(['now', 'is', 'time', 'is', 'now', 'is', 'is'])
    ['is', 'now', 'time']
    >>> wordset(['I', 'a', 'a', 'is', 'a', 'is', 'I', 'am'])
    ['I', 'a', 'am', 'is']
    """
    return sorted(set(wordlist))

def longestword(wordset):
    """
    Return the length of the longest word in wordset.
    >>> longestword(['a', 'apple', 'pear', 'grape'])
    5
    >>> longestword(['a', 'am', 'I', 'be'])
    2
    """
    return max(len(word) for word in wordset) if wordset else 0

if __name__ == '__main__':
    import doctest
    doctest.testmod()
```

**Explanation**:

- **Doctest Integration**: The `if __name__ == '__main__':` block runs doctests when `wordtools.py` is executed directly, but not when imported. `__name__` is `wordtools` when imported, `__main__` when run directly.
- **Function Details**:
    - `cleanword`: Removes non-alphabetic characters using a list comprehension.
    - `has_dashdash`: Checks for `'--'` using the `in` operator.
    - `extract_words`: Splits the string, cleans each word, and converts to lowercase.
    - `wordcount`: Returns a list with the word and its count in `wordlist`.
    - `wordset`: Uses `set` to get unique words and `sorted` to order them.
    - `longestword`: Uses `max` with a generator to find the longest word length.

### Exercise 11: Sorting Fruits

**Task**: Write `sort_fruits.py` to sort fruits from `unsorted_fruits.txt` into `sorted_fruits.txt`.

```python
# sort_fruits.py
with open('unsorted_fruits.txt', 'r') as infile:
    fruits = infile.readlines()
    fruits = [fruit.strip() for fruit in fruits]  # Remove newlines
    fruits.sort()  # Sort alphabetically
    with open('sorted_fruits.txt', 'w') as outfile:
        for fruit in fruits:
            outfile.write(fruit + '\n')
```

**Explanation**:

- Reads all lines from `unsorted_fruits.txt`.
- Strips newlines, sorts the list, and writes to `sorted_fruits.txt` with newlines.
- Assumes `unsorted_fruits.txt` contains one fruit per line.

### Exercise 12: Analyzing `countletters.py`

**Task**: Answer questions about `countletters.py`.

```python
# countletters.py
def display(i):
    if i == 10: return 'LF'
    if i == 13: return 'CR'
    if i == 32: return 'SPACE'
    return chr(i)

with open('alice_in_wonderland.txt', 'r') as infile:
    text = infile.read()

counts = 128 * [0]
for letter in text:
    counts[ord(letter)] += 1

with open('alice_counts.dat', 'w') as outfile:
    outfile.write("%-12s%s\n" % ("Character", "Count"))
    outfile.write("=================\n")
    for i in range(len(counts)):
        if counts[i]:
            outfile.write("%-12s%d\n" % (display(i), counts[i]))
```

**Answers**:

1. **Reading the File**:
    
    - `infile = open('alice_in_wonderland.txt', 'r')`: Opens the file in read mode.
    - `text = infile.read()`: Reads the entire file into a string.
    - `infile.close()`: Closes the file to free resources.
    - `type(text)` returns `<class 'str'>` (a string).
2. **Purpose of `128 * [0]`**:
    
    - `128 * [0]` creates a list of 128 zeros, representing counts for ASCII characters (0-127).
    - ASCII has 128 standard characters, so `counts` tracks occurrences of each character.
3. **Counting Loop**:
    
    - `for letter in text: counts[ord(letter)] += 1`: Iterates over each character in `text`, increments the count at index `ord(letter)` (ASCII value) in `counts`.
4. **Purpose of `display` Function**:
    
    - Converts ASCII values to readable representations.
    - Checks for special characters: 10 (line feed, LF), 13 (carriage return, CR), 32 (space, SPACE).
    - These are non-printable or special characters in ASCII, so they’re labeled for clarity.
5. **Writing Header**:
    
    - `outfile = open('alice_counts.dat', 'w')`: Opens the output file in write mode.
    - `outfile.write("%-12s%s\n" % ("Character", "Count"))`: Writes a header with "Character" left-aligned in 12 spaces, followed by "Count".
    - `outfile.write("=================\n")`: Writes a separator line.
    - Output in `alice_counts.dat`: `Character Count\n=================\n`.
6. **Writing Counts**:
    
    - `for i in range(len(counts))`: Loops over indices 0-127 (ASCII range).
    - `if counts[i]`: Only writes characters with non-zero counts.
    - `outfile.write("%-12s%d\n" % (display(i), counts[i]))`: Writes the character (via `display(i)`) and its count.
    - Purpose of `if counts[i]`: Skips characters that don’t appear in the text to keep the output concise.

### Exercise 13: Calculating Mean

**Task**: Write `mean.py` to compute the mean of numbers from the command line.

```python
# mean.py
from sys import argv

nums = [float(x) for x in argv[1:]]
print(sum(nums) / len(nums))
```

**Explanation**:

- Converts command-line arguments (`argv[1:]`) to floats.
- Computes the mean as `sum(nums) / len(nums)`.
- Matches sample outputs (e.g., `python mean.py 3 4` outputs `3.5`).

### Exercise 14: Calculating Median

**Task**: Write `median.py` to compute the median of numbers from the command line.

```python
# median.py
from sys import argv

nums = sorted([float(x) for x in argv[1:]])
n = len(nums)
if n % 2 == 0:
    median = (nums[n//2 - 1] + nums[n//2]) / 2
else:
    median = nums[n//2]
print(median)
```

**Explanation**:

- Converts and sorts command-line arguments.
- For odd `n`, the median is the middle number; for even `n`, it’s the average of the two middle numbers.
- Matches sample outputs (e.g., `python median.py 3 7 11` outputs `7`).

### Exercise 15: Modifying `countletters.py`

**Task**: Modify `countletters.py` to take the input file as a command-line argument.

```python
# countletters.py
import sys

def display(i):
    if i == 10: return 'LF'
    if i == 13: return 'CR'
    if i == 32: return 'SPACE'
    return chr(i)

def count_letters(input_file, output_file):
    with open(input_file, 'r') as infile:
        text = infile.read()
    
    counts = 128 * [0]
    for letter in text:
        counts[ord(letter)] += 1
    
    with open(output_file, 'w') as outfile:
        outfile.write("%-12s%s\n" % ("Character", "Count"))
        outfile.write("=================\n")
        for i in range(len(counts)):
            if counts[i]:
                outfile.write("%-12s%d\n" % (display(i), counts[i]))

if __name__ == '__main__':
    if len(sys.argv) != 2:
        print("Usage: python countletters.py <input_file>")
        sys.exit(1)
    input_file = sys.argv[1]
    output_file = input_file.replace('.txt', '_counts.dat')
    count_letters(input_file, output_file)
```

**Explanation**:

- Takes the input file from `sys.argv[1]`.
- Generates the output file name by replacing `.txt` with `_counts.dat`.
- Checks for correct argument count and prints usage instructions if invalid.
- Encapsulates logic in `count_letters` for reusability.

## 11. Glossary

- **argv**: A list in the `sys` module containing command-line arguments.
- **attribute**: A variable or function defined in a module, accessed via the dot operator.
- **command line**: The interface where commands are entered.
- **delimiter**: A character separating parts of a path or text (e.g., `/` in paths).
- **directory**: A folder containing files or other directories.
- **dot operator**: `.` used to access module attributes or methods.
- **file**: A named storage unit for data.
- **file system**: A method for organizing files and directories.
- **import statement**: Makes module contents available (e.g., `import module` or `from module import name`).
- **method**: A function-like attribute of an object, invoked with the dot operator.
- **mode**: File operation mode (`'r'`, `'w'`, `'a'`).
- **module**: A `.py` file with reusable code.
- **namespace**: A container for names to avoid conflicts.
- **pydoc**: A tool to generate documentation for Python modules.
- **standard library**: Python’s built-in collection of modules.
- **text file**: A file with printable characters and newlines.
- **volatile memory**: Memory (e.g., RAM) that loses data when power is off.

## Module Attributes

These are **special variables** defined by default in every module.

|Attribute|Description|
|---|---|
|`__name__`|Name of the module. Set to `"__main__"` if run directly.|
|`__doc__`|Documentation string of the module (if provided).|
|`__file__`|Path of the file from which the module was loaded.|
|`__package__`|Name of the package the module belongs to (for relative imports).|
|`__cached__`|Location of the cached bytecode file (usually `.pyc`).|

```python
# Example
import math
print(math.__name__)     # 'math'
print(math.__doc__)      # Description of the module
print(math.__file__)     # Path to the math module binary
```

