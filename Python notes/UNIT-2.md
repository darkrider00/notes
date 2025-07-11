
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

