## 1.Inception

program on our computer designed to be easy for you to talk to 

every program on computer has ability to do vast range of devices 
- read files, start other programs, math, control devices
- bash is not programmed to perform a certain task 
- bash is programmed to take commands from user 

a "language" was created which allows users to "speak" to the bash program and tell it what to do. This language is the bash shell language.

shell program is one that provides users with interface to interact with other programs 
- a large variety of shell programs, each with their own language. Some popular ones are the C shell (csh), Z shell (zsh), Korn shell (ksh), Bourne shell, Debian's Almquist shell (dash), etc.

Bash uses a method directly counter to the ideas of graphical user interfaces:
 - it runs in a text-only "console" where interaction is mainly limited to displaying characters on your screen and reading them from your keyboard.
 -  **bash is a tool**, a single tool in a huge toolbox of programs. Bash alone will only let you do basic things with files and other programs.
 - will need to understand all the other tools in the toolbox of your system. This knowledge is vast and will come slowly, it is important that you **take the time to learn them well**


**Interactive mode**
In interactive mode, the bash shell waits for your commands before performing them. 

Each command you pass it is executed. While a command is being executed, you cannot interact with the bash shell. 

As soon as the command is finished, you can interact with bash again while bash awaits your next command.

**non-interactive mode**
The bash shell can also execute scripts. 

A script is a pre-written series of commands which bash can execute without needing to ask you what to do next. 

Scripts are generally saved in files and subsequently used to automate a wide range of tasks.

```bash
perplex@pop-os:~$ echo $BASH_VERSION
5.1.16(1)-release
perplex@pop-os:~$ 
```

![[Pasted image 20250110203747.png]]

In a terminal, many terminal-based programs can run simultaneously, forming a chain through which your input and their output flows.

![[Pasted image 20250110210531.png]]

a program is a set of pre-written instructions that can be executed by your system's kernel. 

A program gives instructions to the kernel directly. The kernel is technically also a program, but one that runs constantly and communicates with your hardware instead.

A program generally lives on your disk, waiting to be started. When you "run" or "execute" a program, your kernel loads its pre-written instructions (its code) by creating a process for your program to work in.

if a chocolate cake recipe is a program, then your process of baking a chocolate cake with it is the program's process. A process relays the instructions in your program to the kernel

 process also has a few hooks to the outside world via something called file descriptors.

These are essentially plugs we use to connect processes to files, devices or other processes. Most chocolate cake recipes won't, but some might have, for instance, a table for looking up the amounts of ingredients based on the desired number of servings.

 These recipes take input and their output will differ depending on the input given. File descriptors are identified by numbers, though the first three also have standard names:
 
standard input

**File descriptor 0** is also called standard input. This is where most processes receive their input from. By default, processes in your terminal will have their standard input "connected" to your keyboard. More specifically, to the input your terminal program receives.

standard output

**File descriptor 1** is also called standard output. This is where most processes send their output to. By default, processes in your terminal will have their standard output "connected" to your display. More specifically, your terminal program will display this output in its window.


standard error

**File descriptor 2** is also called standard error. This is where most processes send their error and informational messages to. By default, processes in your terminal will have their standard error "connected" to your display, just like standard output. It's important to understand that standard error is just another plug, just like standard output, which leads to your terminal's display. It isn't dedicated to errors, in fact bash uses it for most of its informational messages _as well as your prompt_!

A process isn't limited to just these three file descriptors, it can create new ones with their own number and connect them to other files, devices or processes as it sees fit.

f a program needs its output to go to another program's input, as opposed to your display, it will instruct the kernel to connect its standard output to the other program's standard input. Now all the information it sends to its standard output file descriptor will flow into the other program's standard input file descriptor. These flows of information between files, devices and processes are called streams.


Stream - information flowing through links b/w files, devices  process in running system  can transport any kind of bytes and receiving end only consume their bytes in order they were sent 

If I have a program that outputs names connected to another program, the second program can only see the second name after first reading the first name from the stream.

Reading a name from the stream consumes those bytes from the stream and the stream advances. The stream cannot be rewound and the name cannot be re-read.

### **How Do Programs Use Streams?**

Imagine you have two programs:

1. **Program A** generates a list of names.
2. **Program B** processes these names.

You can connect **Program A's output** directly to **Program B's input** using streams. So instead of showing the names on the screen, Program A sends them into Program B.

- **Example**: `ls | grep "file"`
    - `ls`: Lists all files in a directory.
    - `grep "file"`: Searches for names containing "file."
    - The output of `ls` flows into `grep` as a stream, and `grep` processes it

### **Important Points About Streams**

1. **Order Matters**: Streams flow in a sequence. If Program A sends names, Program B will see:
    - First name → then second → then third → and so on.
2. **No Going Back**: Once a name is read from the stream, it's gone unless you save it somewhere. The stream can't "rewind."
    - Like reading a paper tape: you can't re-read what's already been pulled through.

![[Pasted image 20250111162937.png]]In the above example, two bash processes are linked via a stream. The first bash process reads its input from the keyboard. It sends output on both standard output and standard error. Output on standard error is connected to the terminal display, while output on standard output is connected to the second process. Notice how the first process' `FD 1` connects to the second process' `FD 0`. The second process therefore consumes the first process' standard output when it reads from its standard input. The second process' standard output in turn is connected to the terminal's display.

[#](https://guide.bash.academy/inception/?=So_what_exactly_is_a_program_and_how_does_it_connect_to_other_programs?#p2.3.0_8)To try out this dynamic, you can run the following code in a terminal, where `(` and `)` symbols create two sub-shells and the `|` symbol connects the former's `FD 1` to the latter's `FD 0`:

```bash
 echo "Your name?" >&2; read name; echo "$name" ) | ( while read name; do echo "Hello, $name"; done )
```

File descriptors (FDs) are integral components of an operating system, especially in Unix-like systems. They represent references to files, devices, or communication channels (like sockets or pipes) that a program interacts with. Think of them as "handles" or pointers for the OS to know which file or stream a process is working on.

### Key Points About File Descriptors

1. **What Are File Descriptors?**
    
    - A file descriptor is simply an integer that uniquely identifies an open file or resource for a running process.
    - When a process opens a file, the operating system assigns a file descriptor to track the file.
2. **Standard File Descriptors** Every process has three standard file descriptors by default:
    
    - **Standard Input (stdin)**: FD 0
        - Used to read input, typically from the keyboard.
        - Example: `read` in Bash reads from stdin.
    - **Standard Output (stdout)**: FD 1
        - Used to write output, typically to the terminal/screen.
        - Example: `echo "Hello"` writes to stdout.
    - **Standard Error (stderr)**: FD 2
        - Used to write error messages, typically to the terminal.
        - Example: `echo "Error!" >&2` writes to stderr.
3. **File Descriptor Numbers**
    
    - When a process opens additional files, it gets higher numbers (starting from 3).
    - These numbers are unique to the process but are reused after a file is closed.
4. **File Descriptors Can Represent**
    
    - Regular files (e.g., `.txt`, `.log`)
    - Devices (e.g., `/dev/null`, `/dev/sda`)
    - Pipes or sockets (used for inter-process communication)
    - Other resources like terminals or network connections.
5. **Redirection with File Descriptors** File descriptors can be redirected, allowing input/output to go to files, devices, or other programs. Examples:
    
    - Redirect stdout to a file: `command > file.txt`
    - Append stdout to a file: `command >> file.txt`
    - Redirect stderr to a file: `command 2> errors.txt`
    - Redirect both stdout and stderr to the same file: `command > file.txt 2>&1`
6. **Advanced Usage**
    
    - Duplication: Use the same file descriptor for multiple purposes. Example: `command 3>&1` duplicates FD 1 (stdout) into FD 3.
    - Closing FDs: `command >&-` closes an FD, ensuring no output/input flows through it.
    - Piping: Pass the output of one command as input to another. Example: `ls | grep "file"`

### Why Are File Descriptors Useful?

- **Efficiency**: Instead of managing strings or filenames, the OS tracks resources using integers.
- **Flexibility**: Redirection and piping let you combine processes and manage streams easily.
- **Control**: Allows processes to work with multiple files, sockets, or devices simultaneously.

### Example: Redirecting Input/Output

Suppose we have a file `input.txt` with some text:

bash

Copy code

`echo "Hello World" > input.txt`

#### Read from File:

bash

Copy code

`cat < input.txt # Redirects stdin from input.txt to the cat command.`

#### Write Output to File:

bash

Copy code

`echo "Logging" > output.txt # Redirects stdout to the file output.txt`

#### Redirect Both Stdout and Stderr:

bash

Copy code

`ls non_existent_file > out.txt 2> err.txt # stdout goes to out.txt, stderr goes to err.txt`

#### Combine Both:

bash

Copy code

`ls non_existent_file > combined.txt 2>&1 # Both stdout and stderr go to combined.txt`


t is important to understand that **file descriptors are process specific**: to speak of "standard output" only makes sense when referring to a specific process. In the example above, you'll notice that the first process' standard input is not the same as the second process' standard input. You'll also notice that the first process' FD 1 (standard output) is connected to the second process' FD 0 (standard input). File descriptors do not describe the streams that connect processes, they only describe the process' plugs where these streams can be connected to.


## 2.commands and arguments 
bash waits for instructions from you and then executes them to the best of its abilities

- Synchronous command execution : Bash generally takes one command from you at a time, executes the command, and when completed returns to you for the next command.
- while bash is busy with a command that you give it, you cannot interact with bash directly
-  While you're interacting with the file editor, bash takes a back-seat and waits for the file editor to end (which generally means you quit it)
- the file editor program stops running, the command ends and bash resumes operation by asking you for the next thing to do
- while your editor is running, you are no longer at the bash prompt. As soon as your editor exits, your bash prompt re-appears

![[Pasted image 20250111195153.png]]

```bash
perplex@pop-os:~$ cat hello.txt 
Hello santhosh!
:)
```

```bash
 $ ex    #bash command to run the "ex" program._
: i      #command to "insert" some text.
Hello!
.        # A line with just a dot tells ex to stop inserting text._
: w greeting.txt  #command to "write" the text to a file._
"greeting.txt" [New] 1L, 7C written
: q      #command to "quit" the program._
$ cat greeting.txt   #And now we're back in bash!_
Hello!     #The "cat" program shows the contents of the file._
$
```

![[Pasted image 20250111200153.png]]

Logically, bash cannot execute a command until it has enough information to do its job. The first line of the `if` command in the example above (we'll cover what these commands do in more detail later on) doesn't contain enough information for bash to know what to do if the test succeeds or if it fails. As a result, bash shows a special prompt: `>`. This prompt essentially means: the command you gave me is not yet at an end. We keep on providing extra lines for the command, until we reach the `fi` construct. When we end that line, bash knows that you're done providing conditional result cases. It immediately begins running all the code in the entire block, from `if` to `fi`.

We will soon see the different kinds of commands defined in bash's grammar, but the `if` command we just saw is called a Compound Command, because it compounds a bunch of basic commands into a larger logical block.


we're passing our commands to an interactive bash session. As we explained before, bash can also run in non-interactive mode where it reads commands from a file or stream rather than asking you for them.

This second bash process will execute all the commands it finds in the file `hello.txt`, non-interactively. When it's done (there are no commands left in the file), the non-interactive bash process ends and the interactive bash process is ready with your bash hello.txt command; it shows a new prompt asking you for the next command to run.

[#](https://guide.bash.academy/commands/?=How_do_I_give_bash_a_command?#p1.2.0_8)It's only a small step from a file with a list of commands in it to a veritable bash script. Open your `hello.txt` file again using your favourite text editor and add a hashbang to the top of it, as the first line of the script: #!/usr/bin/env bash

```bash
#!/usr/bin/env bash
$ bash hello.txt_
Your name? Maarten Billemont
Hello, Maarten Billemont._
$
```


```
**`/usr/bin/env`, which isn't really a program that understands the bash language. It's a program that can find and start other programs. In our case, we use an argument to tell it to find the `bash` program and use that for interpreting the language in our script. Why do we use this "inbetween" program called `env`? It has everything to do with what comes before the name: the path. We know with relative certainty that the `env` program lives in the `/usr/bin` path. Given the large variety of operating systems and configurations, however, we don't have any good certainty about where the `bash` program is installed. Which is why we use the `env` program to find it for us. That was a little complicated! But now, what's the difference between our file before and after adding the hashbang?**
```

[#](https://guide.bash.academy/commands/?=How_do_I_give_bash_a_command?#p1.2.0_10)Most systems require you to mark a file as executable before the kernel is willing to allow you to run it as a program. Once we do that, we can start the `hello.txt` program like we would any other program. The kernel will look inside the file, find the hashbang, use that to track down the bash interpreter, and finally use the bash interpreter to start running the instructions in the file. You have your first real bash program!

```bash

$ chmod +x hello.txt_
$ ./hello.txt

```

### What is Syntax Sugar?

**Syntax sugar** refers to a feature in programming languages that makes the code easier to read or write but doesn't add new functionality.

sugar that sweetens the experience for developers , providing cleaner way to express something that could already be achieved with longer or complex syntax.

### Examples of Syntax Sugar

#### **1. Python List Comprehension**

Instead of:

python

Copy code

`result = [] for i in range(10):     result.append(i * 2)`

You can write:

python

Copy code

`result = [i * 2 for i in range(10)]`

#### **2. JavaScript Arrow Functions**

Instead of:

javascript

Copy code

`function add(a, b) {     return a + b; }`

You can write:

javascript

Copy code

`const add = (a, b) => a + b;`

Arrow functions are _syntax sugar_ for writing shorter function expressions.

#### **3. Ternary Operator**

Instead of:

javascript

Copy code

`let result; if (x > 0) {     result = "positive"; } else {     result = "non-positive"; }`

You can write:

javascript

Copy code

`let result = (x > 0) ? "positive" : "non-positive";`

### Syntax Sugar in Bash

1. **Arithmetic Shorthand**  
    Instead of writing `expr` or `$((...))`, Bash provides operators like `+=`, `-=`, `++`, etc.
    
    bash
    
    Copy code
    
    `# Without syntax sugar: i=$((i + 1))  # With syntax sugar: ((i++)) i+=1`
    
2. **Command Substitution with `$()`**  
    `$()` is a cleaner and more modern way to capture the output of a command, replacing backticks (`` `command` ``).
    
    bash
    
    Copy code
    
    ``# Without syntax sugar (old style): result=`ls`  # With syntax sugar: result=$(ls)``
    
3. **Brace Expansion for Generating Sequences**  
    Bash allows you to use braces to create sequences or repetitive text quickly.
    
    bash
    
    Copy code
    
    `# Without syntax sugar (manual list creation): echo file1 file2 file3  # With syntax sugar: echo file{1..3}`
    
4. **String Length and Substring Operations**  
    Bash provides concise ways to get string length or extract substrings.
    
    bash
    
    Copy code
    
    `str="Hello World"  # Length of string: echo ${#str}    # Outputs: 11  # Substring (first 5 characters): echo ${str:0:5} # Outputs: Hello`
    
5. **Array Syntax**  
    Arrays are easier to define and use compared to manually managing variables.
    
    bash
    
    Copy code
    
    `# Without syntax sugar: var1="value1" var2="value2"  # With syntax sugar: arr=("value1" "value2") echo ${arr[0]} # Outputs: value1`
    
6. **Double Brackets `[[ ]]` for Conditionals**  
    `[[ ]]` is a more powerful, syntax-sugared version of `[ ]`, allowing for advanced string comparison, regex, and logical operators.
    
    bash
    
    Copy code
    
    ``# Without syntax sugar (basic `[ ]`): if [ "$var" = "hello" ]; then echo "Match"; fi  # With syntax sugar (`[[ ]]`): if [[ $var =~ ^hel ]]; then echo "Match"; fi``
    
7. **Ternary-Like Syntax**  
    You can use the `&&` and `||` operators as shorthand for if-else statements.
    
    bash
    
    Copy code
    
    `# Without syntax sugar: if [ "$var" = "yes" ]; then echo "OK"; else echo "Not OK"; fi  # With syntax sugar: [[ $var = "yes" ]] && echo "OK" || echo "Not OK"`
    
8. **Default Values with `${VAR:-DEFAULT}`**  
    This provides a concise way to use a variable with a fallback value if it's unset.
    
    bash
    
    Copy code
    
    `# Without syntax sugar: if [ -z "$var" ]; then var="default"; fi  # With syntax sugar: echo ${var:-default}`
    
9. **Looping Constructs**  
    Bash offers concise loop syntax.
    
    bash
    
    Copy code
    
    `# Without syntax sugar (using a counter manually): i=0 while [ $i -lt 3 ]; do     echo "Hello"     i=$((i + 1)) done  # With syntax sugar: for i in {1..3}; do     echo "Hello" done`
    
10. **Chaining Commands with `;`, `&&`, and `||`**  
    These operators allow you to execute multiple commands on a single line, conditionally or sequentially.
    
    bash
    
    Copy code
    
    `# Without syntax sugar: mkdir dir cd dir touch file  # With syntax sugar: mkdir dir && cd dir && touch file`
    

### Why Learn Syntax Sugar?

- **Faster scripting:** Write concise, elegant, and expressive scripts.
- **Readability:** Other developers (or your future self) can understand your code more easily.
- **Efficiency:** Less code means fewer chances for bugs and easier debugging.
Inbetween the two commands goes the `|` symbol. This is also called the "pipe" symbol, and it tells bash to connect the output of the first to the input of the second command

we can use the `|&` symbol inbetween the commands to indicate that we want not only the standard output of the first command, but also its standard error to be connected to the second command's input.

### list
- sequence of commands 
- after the command comes control operator 
- ; equivalent to telling it starts a new line tells bash just to run the command wait for it to end 
- | | control operator  tells bash to run the command as it normally would but after finishing move to next command only command before it failed.
- | | if it didn't fail will make bash skip ommand after it
- above is useful for showing error messages whn command fails

#### Compound commands 

- special syntax can do lot of diff things but behave as single command in command list 
- block in programming -single big command

```
 if list [  ; | <newline> ]  then  list [  ; | <newline> ]  fi
      { list ; }

```

```bash
if ! rm hello.txt; then echo "Couldn't delete hello.txt." >&2; exit 1; fi

rm hello.txt || { echo "Couldn't delete hello.txt." >&2; exit 1; }
```

above commans both perform same operation 1st - compound command 2nd - compound command in command list 

The compound command in the second example begins at `{` and continues until the next `}`, as a result everything inside the braces is considered a single command

If we were to forget the braces, we would get a command list of _three_ commands: the `rm` command followed by the `echo` command, followed by the `exit` command.
- If the `rm` succeeds, `||` will skip the command after it, which, if we leave out the braces,
- would be only the `echo` command. The braces combine the `echo` and `exit` commands into a single compound command, allowing `||` to skip both of them when `rm` succeeds.

like an or operator if one succeeds other one won't execute if one fails other executes

#### Coprocesses
- allows to easily run a command asynchronously (without making bash wait for it to end (in the background))
- set up new file descriptor plugs connects directly to new commands input and output.

Syntax:
```
    coproc [ name ] command [ redirection ... ]
```

```bash
coproc auth { tail -n1 -f /var/log/auth.log; }
read latestAuth <&"${auth[0]}"
echo "Latest authentication attempt: $latestAuth"
```

- starts an asynchronous `tail` command.
- While it runs in the background, the rest of the script continues
- First the script reads a line of output from the coprocess called `auth` (which is the first line of the `tail` command output)
- we write a message showing the latest authentication attempt we read from the coprocess
- script can continue and each time it reads from the coprocess pipe, it will get the next line from the `tail` command.
### **Simple Analogy**
- Think of the coprocess as a **live reporter** constantly keeping an eye on `/var/log/auth.log` and giving updates whenever you ask.
- The script is free to do other things but can **interrupt the reporter** anytime to get the latest update.

### Functions

- When you declare a function in bash, you're essentially creating a temporary new command which you can invoke later in the script.

syntax:
```
    name **()** compound-command [ redirection ]
```


```bash
exists() { [[ -x $(type -P "$1" 2>/dev/null) ]]; }
exists gpg || echo "Please install GPG." <&2
```

- You begin by specifying a `name` for your function. This is the name of your new command, you'll be able to run it later on by writing a simple command with that name.
- After the command name go the `()` parentheses.
- Some languages use these parentheses to declare the arguments the function accepts: **bash does not**.
- parentheses should always be empty.
- To change the file descriptors of the script for the duration of running the function, you can optionally specify the function's custom file redirections.

```
Bash commands tell bash to perform a certain unit of work. These units of work cannot be subdivided: bash needs to know the whole command to be able to execute it. There are different kinds of commands for different types of operations. Some commands group other commands into blocks or test their result. Many command types are syntax sugar: their effect can be achieved differently, but they exist to make the job easier.
```

### ## Command names and running programs

```
    [ var**=**value ... ] ==name== [ arg ... ] [ redirection ... ]
```

We're first going to focus on the command's name. The name tells bash what the job is that you want this command to perform. To figure out what you want your command to do, bash performs a _search_ to find out what to execute. In order, bash uses the `name` to try and find a:

![[Pasted image 20250112102558.png]]

- if bash finds no way to execute a command by the name you gave it, your command will result in an error and bash will show an error message:

```bash
$ buy beer
bash: buy: command not found
```

Aliases are only rarely useful, only work in interactive sessions and are almost completely superseded by functions. You should avoid using them in almost all cases.

#### The `PATH` to a program

reference : https://refspecs.linuxfoundation.org/fhs.shtml

- On a standard UNIX system, there are [a few standardized locations](http://refspecs.linuxfoundation.org/fhs.shtml) for programs to go
-  Some programs will be installed in `/bin`, others in `/usr/bin`, yet others in `/sbin` and so on
- To the rescue comes the `PATH` environment variable. Your `PATH` variable contains a set of directories that should be searched for programs.

```
$ ping 127.0.0.1

    **PATH=**/bin**:**/sbin**:**/usr/bin**:**/usr/sbin
           │     │
           │     ╰──▶ ==/sbin==/ping ?  **found!**
           ╰──▶ ==/bin==/ping ?  not found.
```

you're trying to start the `ping` program which is installed at `/sbin/ping`.
 -  If your `PATH` is set to `/bin:/sbin:/usr/bin:/usr/sbin` then bash will first try to start `/bin/ping`
 - which doesn't exist. Failing that, it will try `/sbin/ping`. It finds the `ping` program
 - records its location in case you need `ping` again in the future and goes ahead and runs the program for you.
```bash
$ type ping
ping is /sbin/ping
$ type -a echo
echo is a shell builtin
echo is /bin/echo
```

if you run the echo command in bash, even before bash tries a `PATH` search, it will notice there's a built-in by that name and use it.
- `type` is a great way to visualize this lookup process.

Sometimes you'll need to run a program that isn't installed in any of the `PATH` directories. In that case, you'll have to manually specify the path to where bash can find the program, rather than just its name

```bash
$ /sbin/ping -c 1 127.0.0.1
PING 127.0.0.1 (127.0.0.1): 56 data bytes
64 bytes from 127.0.0.1: icmp_seq=0 ttl=64 time=0.075 ms

--- 127.0.0.1 ping statistics ---
1 packets transmitted, 1 packets received, 0.0% packet loss
round-trip min/avg/max/stddev = 0.075/0.075/0.075/0.000 ms
$ ./hello.txt_  #Remember our hello.txt script?_
Your name?
```

```
[#](https://guide.bash.academy/commands/?=The_PATH_to_a_program#a3.2.0_1)Bash only performs a `PATH` search on command names that do not contain a / character. Command names with a slash are always considered direct pathnames to the program to execute.
```

You can add more directories to your `PATH`. A common practice is to have a `/usr/local/bin` and a `~/bin` (where `~` represents your user's home directory). Remember that `PATH` is an environment variable: you can update it like this

```bash
$ PATH=~/bin:/usr/local/bin:/bin:/usr/bin
$
```

This will change the variable in your current bash shell. As soon as you close the shell, the change will be lost, though. We'll go more in-depth on how environment variables work and how you should configure them in a later section.

To find out where `bash` will locate the `ls` program when you execute it, you can use the `type` command. In your case, the output of `type ls` shows:

bash

Copy code

``ls is aliased to `ls --color=auto'``

This means:

1. `ls` is **aliased** to `ls --color=auto`, which ensures colored output for better readability in the terminal.
2. An **alias** is essentially a shortcut for a command.

---

### To Find the Actual Location of `ls`

If you want to know the actual path of the `ls` program, bypassing the alias, you can:

1. **Use the `type` command with the `-a` option**:
    `type -a ls`


perplex@pop-os:~/Documents$ chmod +x myscript
perplex@pop-os:~/Documents$ PATH=$PATH:.
perplex@pop-os:~/Documents$ my
myscript              mysqld_qslower-bpfcc  
perplex@pop-os:~/Documents$ myscript
my bash script
perplex@pop-os:~/Documents$ 


```bash
perplex@pop-os:~/Documents$ ex
E1187: Failed to source defaults.vim 
perplex@pop-os:~/Documents$ chmod +x script 
perplex@pop-os:~/Documents$ PATH=$PATH:.
perplex@pop-os:~/Documents$ script
Script started, output log file is 'typescript'.
perplex@pop-os:~/Documents$ type script

perplex@pop-os:~/Documents$ mv script myscript
perplex@pop-os:~/Documents$ chmod +x myscript 
perplex@pop-os:~/Documents$ PATH=$path:.
perplex@pop-os:~/Documents$ myscript 
bash script new :)
perplex@pop-os:~/Documents$ 
```

### Command arguments and quoting literals

**The gross part of all bugs in bash shell scripts are the direct result of their authors not properly understanding command arguments.**

To the bash shell, blank space is syntax just like anything else. It means: break the previous apart from the next thing. Bash calls this: word splitting.

There are two ways in bash to make characters literal: quoting and escaping. Quoting is the practice of wrapping " or ' characters around the text that we want to make literal. Escaping is the practice of placing a single \ character in front of the character that we want to make literal.

```bash
way 1:
mplayer ==05\ Between\ Angels\ and\ Insects.ogg== ==07\ Wake\ Up.ogg==

way 2:
ls -l ==hello.txt==
-rw-r--r--  1 lhunath  staff  131 29 Apr 17:07 hello.txt
$ ls -l =='hello.txt'==
-rw-r--r--  1 lhunath  staff  131 29 Apr 17:07 hello.txt
$ ls -l =='05 Between Angels and Insects.ogg'== =='07 Wake Up.ogg'==
```

  
You should use =="double quotes"== for any argument that contains expansions (such as `$variable` or `$(command)` expansions) and =='single quotes'== for any other arguments.
 - Single quotes make sure that everything in the quotes remains literal, while double quotes still allow some bash syntax such as expansions:

```bash
echo =="Good morning, $USER."==_Double quotes allow bash to expand `$USER`_
echo =='You have won SECOND PRIZE in a beauty contest.'== \_Single quotes prevent even the `$`-syntax_
     =='Collect $10'==_from triggering expansion._
```


```bash
$ ls -l ==05== ==Between== ==Angels== ==and== ==Insects.ogg==
ls: 05: No such file or directory
ls: Angels: No such file or directory
ls: Between: No such file or directory
ls: Insects.ogg: No such file or directory
ls: and: No such file or directory
```

#### dangers:
```bash
$ read -p 'Which user would you like to remove from your system? ' username
Which user would you like to remove from your system?  lhunath
$ rm -vr /home/$username
removed '/home/lhunath/somefile'
removed directory: '/home/lhunath'
removed '/home/bob/bobsfiles'
removed directory: '/home/bob'
removed '/home/victor/victorsfiles'
removed directory: '/home/victor'
removed directory: '/home'
rm: cannot remove 'lhunath': No such file or directory
```

What happened here, is that on input, because you accidentally put a `space` character before the name of the user to delete, the `rm` command expanded into `rm -vr ==/home/== ==lhunath==`, which resulted in a situation that is likely to upset both Victor and Bob:
```bash
$ rm -vr "/home/$username"
rm: cannot remove '/home/ lhunath': No such file or directory
```


### Managing a command's input and output using redirection
syntax:
```
    [ var=value ... ] name [ arg ... ] ==[ redirection ... ]==
```

**How Bash Sets Up File Descriptors**
When you open a terminal, the **terminal program** sets up file descriptors for the Bash shell:

- The **terminal** connects:
    - Your keyboard input to **Standard Input (FD 0)** of Bash.
    - The terminal window (your screen) to **Standard Output (FD 1)** and **Standard Error (FD 2)**.

This means:
- **What you type** into the terminal goes to Bash.
- **What Bash outputs (or errors)** appears in your terminal window.
### **What Happens When Bash Starts a New Program?**

When you run a program or command in Bash (e.g., `ls`), here’s what happens:

1. **Bash Creates File Descriptors for the New Program**:
    
    - The program inherits the file descriptors of Bash. So:
        - The program’s Standard Input is connected to the terminal (FD 0).
        - The program’s Standard Output and Standard Error are connected to the terminal (FD 1 and FD 2).
2. **Result**:
    
    - The program behaves like Bash:
        - Your keyboard input goes to the program (e.g., if it needs input).
        - The program’s output or error messages appear in your terminal.

### **Example**

- Open a terminal and type:
    `echo "Hello, World!"`
    
    - Bash starts the `echo` command.
    - Bash connects the terminal (keyboard/screen) to the `echo` command’s file descriptors:
        - Standard Input (FD 0) is ignored (not needed for `echo`).
        - Standard Output (FD 1) prints `Hello, World!` to the terminal.

- **File descriptors create "streams"** that connect programs, files, and devices.
- Bash **inherits** these streams from the terminal and **passes them to programs it starts**.
- This inheritance allows commands to:
    - Read from your keyboard.
    - Write to your screen.
    - Display errors on your screen separately.

![[Pasted image 20250112160541.png]]

- When `bash` starts an `ls` process, it first looks at its own file descriptors. It then creates file descriptors for the `ls` process, connected to the same streams as its own: FD 1 and FD 2 leading to the `Display`,
- FD 0 coming from the `Keyboard`. As a result, `ls`' error message (emitted on FD 2) and its regular output (emitted on FD 1) both end up on your terminal display.

```
If we want to gain control over where our commands connect to, we need to employ redirection: it is the practice of changing the source or destination of a file descriptor. One thing we could do with redirection is write `ls`' result to a file instead of to the terminal display:
```

![[Pasted image 20250112160700.png]]
Redirecting standard output is done using the `>` operator.
arrow sending output from the command to the file. This is by far the most common and useful form of redirection.

Another common thing redirection is used for is hiding error messages. You'll notice that our redirected `ls` command is still displaying an error message. Usually this is a good thing. Sometimes, though, we might find that error messages produced by some commands in our scripts are unimportant to the user and should be hidden. To do this, we can use file redirection again, in a similar fashion as redirecting standard output caused `ls`' result to disappear:

![[Pasted image 20250112160818.png]]

if we wanted to save all the output that would normally appear on the terminal to our `myfiles.ls` file; both the results and error messages?

![[Pasted image 20250112161001.png]]

### **What Happened in the Command?**

The command you used was:

bash

Copy code

`ls -l a b >myfiles.ls 2>myfiles.ls`

This is **intended** to redirect:

- **Standard Output (FD 1)** to `myfiles.ls` (`>myfiles.ls`).
- **Standard Error (FD 2)** to `myfiles.ls` (`2>myfiles.ls`).

However, both `FD 1` and `FD 2` are **independently** writing to the same file.

This creates an issue because **each file descriptor has its own stream** to the file. These streams aren't synchronized.

### **The Problem: Unsynchronized Writes**

Here’s what happens internally:

1. When a program like `ls` outputs data to **both streams** (stdout and stderr):
    - **FD 1** writes its data to `myfiles.ls`.
    - **FD 2** writes its data to `myfiles.ls`.
2. These writes occur **independently**, and since they are asynchronous, their outputs might:
    - Overlap.
    - Be written in unpredictable orders.
    - Cause "garbled" or interleaved output in `myfiles.ls`.

Streams (used by file descriptors) use internal **buffers** to optimize data writes:

- Data is stored in the buffer until it’s full or flushed.
- Both `FD 1` and `FD 2` have separate buffers.
- When their buffers are flushed to the same file, the content can overlap in unpredictable ways.

  
To solve this problem, you need to send both your output and error bytes on the same stream. And to do that, you're going to need to know how to duplicate file descriptors:

![[Pasted image 20250112161324.png]]

- act of copying one file descriptor's stream connection to another file descriptor.
-  both file descriptors are connected to the same stream. We use the `>&` operator
- You will use this operator fairly frequently, and in most cases it'll be to copy FD 1 to FD 2 as is done above. You can translate the syntax `2>&1` as Make FD `2` write(`>`) to where FD(`&`) `1` is currently writing.
- redirections are evaluated from left to right, conveniently the same way as we read them.

```bash
ls -l a b 2>&1 >myfiles.ls
```

```
FD 1 (stdout) → Writes to `myfiles.ls` 
FD 2 (stderr) → Redirected to FD 1 (stdout)``
```

- **Result**: Both outputs share the same stream, ensuring ordered and predictable writes.

```bash
ls -l a b >myfiles.ls 2>&1
```
We now first change FD 1's target to stream to `myfiles.ls`. Then, we make FD 2 target the same stream FD 1 is currently using

Both file descriptors are now targeting `myfiles.ls` and any output written by `ls` on either FD 1 or FD 2 will end up in the file.

### file redirection
syntax:
```
    [x]>file, [x]<file
```

- x> file - opens a file and connects to file descriptor x for writing
- any output written to FD x goes to specified file
- x< file - opens file and connects to file descriptor `x` for reading
- if x is not specified it defaults to FD 0(std input)
- this allows process to read input from file instead of terminal or keyboard
### **Examples in Your Code**

#### **1. `echo Hello >~/world`**

- This redirects **standard output (FD 1)** to the file `~/world`.
- The `>` operator implicitly means `1>`, so it's the same as:

    `echo Hello 1>~/world`
    
- What happens:
    - A new file `~/world` is created (or overwritten if it already exists).
    - The text `Hello` is written into the file.

#### **`rm file 2>/dev/null`**

- This redirects **standard error (FD 2)** to `/dev/null`, a special file that discards all data written to it.
What happens:
- The `rm` command tries to delete a file named `file`.
- If `file` doesn't exist, `rm` generates an error message on **stderr**.
- The `2>/dev/null` part ensures this error message is discarded instead of being displayed in the terminal.

#### **`read line <file`**

- This redirects **standard input (FD 0)** to the file named `file`.
- What happens:
    - The `read` command normally reads from the keyboard (standard input).
    - The `<file` part makes `read` take input from the file instead of the keyboard.
    - The first line of `file` is read and stored in the variable `line`.

- **File Descriptors and Defaults**:
    
    - `>` or `<` without a specified `x` will default to:
        - **FD 1** for `>` (writing).
        - **FD 0** for `<` (reading).
- **Overwriting and Appending**:
    
    - `>` overwrites the file.
    - `>>` appends to the file (without overwriting).
- **Connecting Streams**:
    
    - `[x]>file` opens a file for writing and connects it to `FD x`.
    - `[x]<file` opens a file for reading and connects it to `FD x`.

### File descriptor copying
```
    [x]**>&**y, [x]**<&**y
```

```bash
ping 127.0.0.1 >results 2>&1
exec 3>&1 >mylog; echo moo; exec 1>&3 3>&-
```
1. **`>results`**: Redirects **standard output (FD 1)** of the `ping` command to the file `results`.
2. **`2>&1`**: Redirects **standard error (FD 2)** to **standard output (FD 1)**.
    - Now both **stdout** and **stderr** go to the same file (`results`).

**What’s happening?**
- Normally, `ping` outputs regular messages to **stdout** and error messages to **stderr**.
- With `2>&1`, you combine both streams, so everything (both errors and results) goes into `results`.

2nd example:
- #### **`exec 3>&1`**
- Creates **file descriptor 3** and copies the current **standard output (FD 1)** to it.
- Now, FD 3 is a duplicate of FD 1.
- FD 3 will act as a "backup" of the original standard output.
- #### **`>mylog`**
- Redirects **standard output (FD 1)** to the file `mylog`.
- Now, anything that writes to FD 1 will go to `mylog`
- #### **`echo moo`**
- Writes `"moo"` to **standard output (FD 1)**.
- Since FD 1 is redirected to `mylog`, `"moo"` is written to the `mylog` file
- #### **`exec 1>&3`**
- Restores the original **standard output (FD 1)** by copying FD 3 back to FD 1.
- Now, anything written to FD 1 will once again go to the terminal.
- #### **`3>&-`**
- Closes FD 3.
- This removes the "backup" of the original standard output.

```
- exec changes file descriptors for the current shell session.

- File descriptor copying (`[x]>&y`)** allows you to duplicate streams.

- Using temporary file descriptors (like FD 3) is useful for saving and restoring streams during advanced redirections.
```

### Appending file redirection

syntax:
```
    [x]**>>**file
```
Make FD x append to the end of file.
- A stream to file is opened for writing in append mode and is connected to file descriptor x
- The regular file redirection operator `>` empties the file's contents when it opens the file so that only your bytes will be in the file. In append mode (`>>`), the file's existing contents is left and your stream's bytes are added to the end of it.

### Redirecting standard output and standard error
syntax:
```
    &>file
```

```bash
ping 127.0.0.1 &>results
```
-   Make both FD 1 (standard output) and FD 2 (standard error) write to file.
- This is a convenience operator which does the same thing as `>file 2>&1` but is more concise. Again, you can append rather than truncate by doubling the arrow: `&>>file`

### Here Documents
syntax:
```
<<[-]delimiter
        here-document
    delimiter
```

```bash
cat <<.
We choose `.` as the end delimiter
Hello world.
Since I started learning bash, you suddenly seem so much bigger than you were before.
.
```
- Make FD 0 (standard input) read from the string between the delimiters.
- Here documents are a great way to feed large blocks of text to a command's input. They begin on the line after your delimiter and end when bash encounters a line with _just_ your delimiter on it.
- delimiter cannot be indented, because then it is no longer _just_ your delimiter on that line.
- You can prefix your initial delimiter declaration with a `-`, this will tell bash to ignore any tabs you put in front of your heredoc. That way, you can indent the heredoc without the indenting showing in your input string.
-  you need to put quotes around your `'delimiter'`'s initial declaration.

### Here Strings
syntax:
```
    <<<string
```

```bash
cat <<<"Hello world.
Since I started learning bash, you suddenly seem so much bigger than you were before."==
```

Make FD 0 (standard input) read from the string.

Here strings are very similar to here documents but more concise. They are generally preferred over here documents.

### Moving file descriptors
syntax: 
```
    [x]>&y-, [x]<&y-
```

```bash
exec 3>&1- >mylog; echo moo; exec >&3-
```

Replace FD x with FD y.

The file descriptor at y is copied to x and y is closed. Effectively, it replaces x with y. It is a convenience operator for `[x]>&y y>&-`. Again, you will rarely use this operator.

### Reading and writing with a file descriptor

syntax:
```
    [x]<>file
```

```bash
exec ==5<>/dev/tcp/ifconfig.me/80==
echo "GET /ip HTTP/1.1
Host: ifconfig.me
" >&5
cat <&5
```

- The file descriptor at x is opened with a stream to the file that can be used for writing as well as reading bytes
- you'll use two file descriptors for this. One of the rare cases where this is useful is when setting up a stream with a read/write device such as a network socket.

few lines of HTTP to the `ifconfig.me` host at port `80` (the standard HTTP port) and subsequently reads the bytes coming back from the network, both using the same file descriptor `5` set up for this by `exec`.

```bash
echo >&2 "Usage: exists name"
echo >&2 "   Check to see if the program 'name' is installed."
echo >&2
echo >&2 "RETURN"
echo >&2 "   Success if the program exists in the user's PATH and is executable.  Failure otherwise."
```

```
By default, new commands inherit the shell's current file descriptors. We can use redirections to change where a command's input comes from and where its output should go to. File redirection (e.g. `2>errors.log`) allows us to stream file descriptors to files. We can copy file descriptors (e.g. `2>&1`) to make them share a stream. There are also many other more advanced redirection operators.
```

### Questions 
#### REDIR.4. Send only the last command's standard error messages to a file called `errors.log`. Then show the contents of `errors.log` on the terminal

```bash
perplex@pop-os:~/Documents$ cat myscript super.tlkd 2>errors.log && cat errors.log
echo "bash script new :)"
perplex@pop-os:~/Documents$ cat errors.log 
cat: super.tlkd: No such file or directory
perplex@pop-os:~/Documents$ 
```

#### REDIR.5. Append the last command's standard output and error messages to the file called `errors.log`. Then show the contents of `errors.log` on the terminal again.

```bash
perplex@pop-os:~/Documents$ cat myscript  supet.kja>new.log 2>&1 && new.log
perplex@pop-os:~/Documents$ cat new.log 
echo "bash script new :)"
cat: supet.kja: No such file or directory
perplex@pop-os:~/Documents$ 
```

#### REDIR.6. Use a here-string to show the string Hello world. on the terminal.

```bash
perplex@pop-os:~/Documents$ cat <<<'santhosh'
santhosh
perplex@pop-os:~/Documents$ 

```

#### REDIR.7. Fix this command so that the message is properly saved into the `log` file and such that FD 3 is properly closed afterwards: exec 3>&2 2>log; echo 'Hello!'; exec 2>&3

```bash
perplex@pop-os:~/Documents$ exec 3>&1 >log; echo 'santhosh'; exec 1>&3 3>&-
perplex@pop-os:~/Documents$ cat log
santhosh
perplex@pop-os:~/Documents$ 
```

## 3.Variables and Expansions

#### Pathname expansion

```bash
$ cd ~/Downloads
$ rm -v *
removed '05 Between Angels and Insects.ogg'
removed '07 Wake Up.ogg'
$ ls
$
```

We've replaced them with a pattern that tells bash to _expand the pathnames for us_. Expansion is the practice of replacing a part of our command code with a situationally specific piece of code.

we want to replace `*` with the pathname of every single file in our downloads directory. Replacing patterns with pathnames is therefore known as pathname expansion.

It so happens, that the pattern `*` matches the name of every single file in the current directory

Once bash replaces our `*` with `'05 Between Angels and Insects.ogg' '07 Wake Up.ogg'`, bash proceeds to invoke the `rm` command with the full set of arguments: `-v '05 Between Angels and Insects.ogg' '07 Wake Up.ogg'`. As a result, our downloads directory is emptied as intended. Brilliant.

the `rm` command will never even see our pathname expansion pattern.
- pattern is evaluated and expanded by bash well before `rm` is even started.
- As far as `rm` knows, it simply receives a `-v` argument followed by the exact and full name of every single file in the directory. Expansion is always performed by _bash_ itself, and always _before_ actually running the command!
-  To perform a pathname expansion, we simply write a syntactical glob pattern in the place where we want to expand pathnames.
-  A glob is the name of the type of pattern supported by the bash shell. Here are the various basic glob patterns supported by the bash shell:

| Glob              | Meaning                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `*`               | A star or asterix matches any kind of text, even no text at all.                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `?`               | A question mark matches any one single character.                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `[ characters ]`  | A set of characters within rectangular braces matches a single character, only if it's in the given set.                                                                                                                                                                                                                                                                                                                                                                                                   |
| `[[:classname:]]` | When there is a set of colons directly inside the rectangular braces, you can specify the name of a class of characters instead of having to enumerate each character yourself.  <br>Bash knows about various kinds of character classes. For example, if you use the `[[:alnum:]]` pattern, bash will match it against a character only if it is alphanumeric. Supported character classes include:  <br>alnum, alpha, ascii, blank, cntrl, digit, graph, lower, print, punct, space, upper, word, xdigit |

![[Pasted image 20250112204237.png]]

- It is also important to understand that these globs will never jump into subdirectories.
- If we want a glob to go looking at the pathnames in a different directory, we need to explicitly tell it with a literal pathname

example:
```bash
ls ~/Downloads/*.txt

ls ~/*/hello.txt
```

bash has also built support in for more advanced glob patterns. These globs are called: extended globs.

By default, support for them is disabled, but we can easily enable it in our current shell with the command:

```bash
shopt -s extglob
```

Shopt is ==a built-in command in the Bash shell that controls the shell session's options==

| xtended Glob                   | Meaning                                                                                                                   |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------- |
| `+(pattern[ \| pattern ... ])` | Matches when any of the patterns in the list appears, once or many times over. Reads: at least one of ....                |
| `*(pattern[ \| pattern ... ])` | Matches when any of the patterns in the list appears, once, _not at all_, or many times over. Reads: however many of .... |
| `?(pattern[ \| pattern ... ])` | Matches when any of the patterns in the list appears, once or not at all. Reads: maybe one of ....                        |
| `@(pattern[ \| pattern ... ])` | Matches when any of the patterns in the list appears just once. Reads: one of ....                                        |
| `!(pattern[ \| pattern ... ])` | Matches only when none of the patterns in the list appear. Reads: none of ....                                            |

![[Pasted image 20250112204928.png]]

bash will happily match this part of the pattern against the `m` at the beginning (which is not the same as `my`) or even empty space at the start of the filename. This means that in order for the pathname to still be eligible for expansion,
-  the _rest of our pattern_ needs to match against the remainder of our pathname
- we have a `*` glob right after the `!(my)` glob which will happily match the entirety of the filename.
- the `!(my)` part matches against the `m` character in the beginning of the name, the `*` matches against the `yscript` part, and the `.txt` suffix of the pattern matches against the trailing `.txt` of our pathname.
- The pattern matches the name, so the name is expanded! When we include the `*` inside the `!()` pattern, this no longer works and the match fails against this pathname:

```bash
$ ls !(my)*.txt
myscript.txt
hello.txt
$ ls !(my*).txt
hello.txt
```

### Tilde Expansion
 a tilde (`~`) in a pathname with the path to the current user's home directory:

```bash
$ echo 'I live in: ' ~ #Note that expansions must not be quoted or they will become **literal**!

I live in: /Users/lhunath
```
```bash 
echo "The file <hello.txt> contains: $(cat hello.txt)"
The file <hello.txt> contains: ==Hello world.==
```

using $ () we can use commands in b/w brackets

- syntax is a combination of the value-expansion prefix `$` followed by the subshell to expand: `(...)`.
- subshell - small bash process that is used to run a command while main bash shell wait for result

***  
Never leave a value expansion unquoted. If you do, bash will tear the value apart using word-splitting, delete all whitespace from it and perform hidden pathname expansion on all the words in it!
***

### shell variables

- bash parameter that has a name , 
- u can store and use it later as normal variable in programming 
![[Pasted image 20250128100655.png]]

name = something  (bad syntax)

we can combine the variables with expansion

```bash
$ contents="$(cat hello.txt)"
```

$ - expansion wheever u see in bash


```
Parameter expansions (and all other value expansions) should **always** be double-quoted.
```

```bash
$ name=Britta time=23.73 #We want to expand `time` and add an `s` for seconds_

$ echo "$name's current record is $times." #but bash mistakes the name for `times` which holds nothing_
Britta's current record is .

$ echo "$name's current record is ${time}s." #Braces explicitly tell bash where the name ends_
Britta's current record is 23.73s.

```

| url='https://guide.bash.academy/variables.html'                                                                                                                                    |                              |                                                                                                             |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------- | ----------------------------------------------------------------------------------------------------------- |
| Operator                                                                                                                                                                           | Example                      | Result                                                                                                      |
| `**${**parameter**#**pattern**}**`                                                                                                                                                 | "${url#==*/==}"              | ==https:/==/guide.bash.academy/variables.html<br>    ↓<br>/guide.bash.academy/variables.html                |
| Remove the _shortest_ string that matches the pattern if it's at the start of the value.                                                                                           |                              |                                                                                                             |
| `**${**parameter**##**pattern**}**`                                                                                                                                                | "${url##==*/==}"             | ==https://guide.bash.academy/==variables.html<br>    ↓<br>variables.html                                    |
| Remove the _longest_ string that matches the pattern if it's at the start of the value.                                                                                            |                              |                                                                                                             |
| `**${**parameter**%**pattern**}**`                                                                                                                                                 | "${url%==/*==}"              | https://guide.bash.academy==/variables.html==<br>    ↓<br>https://guide.bash.academy                        |
| Remove the _shortest_ string that matches the pattern if it's at the end of the value.                                                                                             |                              |                                                                                                             |
| `**${**parameter**%%**pattern**}**`                                                                                                                                                | "${url%%==/*==}"             | https:==//guide.bash.academy/variables.html==<br>    ↓<br>https:                                            |
| Remove the _longest_ string that matches the pattern if it's at the end of the value.                                                                                              |                              |                                                                                                             |
| `**${**parameter**/**pattern**/**replacement**}**`                                                                                                                                 | "${url/==.==/==-==}"         | https://guide==.==bash.academy/variables.html<br>    ↓<br>https://guide-bash.academy/variables.html         |
| Replace _the first_ string that matches the pattern with the replacement.                                                                                                          |                              |                                                                                                             |
| `**${**parameter**//**pattern**/**replacement**}**`                                                                                                                                | "${url//==.==/==-==}"        | https://guide==.==bash==.==academy/variables==.==html<br>    ↓<br>https://guide-bash-academy/variables-html |
| Replace _each_ string that matches the pattern with the replacement.                                                                                                               |                              |                                                                                                             |
| `**${**parameter**/#**pattern**/**replacement**}**`                                                                                                                                | "${url/#==*:==/==http:==}"   | ==https:==//guide.bash.academy/variables.html<br>    ↓<br>http://guide.bash.academy/variables.html          |
| Replace the string that matches the pattern at the _beginning_ of the value with the replacement.                                                                                  |                              |                                                                                                             |
| `**${**parameter**/%**pattern**/**replacement**}**`                                                                                                                                | "${url/%==.html==/==.jpg==}" | https://guide.bash.academy/variables==.html==<br>    ↓<br>https://guide.bash.academy/variables.jpg          |
| Replace the string that matches the pattern at the _end_ of the value with the replacement.                                                                                        |                              |                                                                                                             |
| `**${#**parameter**}**`                                                                                                                                                            | "${#url}"                    | https://guide.bash.academy/variables.html<br>    ↓<br>40                                                    |
| Expand the length of the value (in bytes).                                                                                                                                         |                              |                                                                                                             |
| `**${**parameter**:**start[**:**length]**}**`                                                                                                                                      | "${url:==8==}"               | https://==guide.bash.academy/variables.html==<br>    ↓<br>guide.bash.academy/variables.html                 |
| Expand a part of the value, starting at start, length bytes long. You can even count start from the end rather than the beginning by using a (space followed by a) negative value. |                              |                                                                                                             |
| `**${**parameter[**^**\|**^^**\|**,**\|**,,**][pattern]**}**`                                                                                                                      | "${url^^==[ht]==}"           | ==htt==p://guide.bas==h==.academy/variables.==ht==ml<br>    ↓<br>HTTps://guide.basH.academy/variables.HTml  |
| Expand the transformed value, either upper-casing or lower-casing the first or all characters that match the pattern. You can omit the pattern to match any character.             |                              |                                                                                                             |

#### EXPAN.1. Assign hello to the variable greeting.

#### EXPAN.2. Show the contents of the variable greeting.

![[Pasted image 20250128101958.png]]


#### EXPAN.3. Assign the string  world to the end of the variable's current contents.

![[Pasted image 20250128102344.png]]

#### EXPAN.4. Show the last word in the variable greeting.

![[Pasted image 20250128102553.png]]

#### EXPAN.5. Show the contents of the variable greeting with the first character upper-cased and a period (`.`) at the end.

### Difference Between `^`, `^^`, `,`, and `,,`:

| Syntax            | Function                                                                      | Example Output              |
| ----------------- | ----------------------------------------------------------------------------- | --------------------------- |
| `${var^}`         | Capitalizes the **first character** of the string.                            | `hello -> Hello`            |
| `${var^^}`        | Capitalizes **all characters** in the string.                                 | `hello -> HELLO`            |
| `${var,}`         | Lowercases the **first character** of the string.                             | `HELLO -> hELLO`            |
| `${var,,}`        | Lowercases **all characters** in the string.                                  | `HELLO -> hello`            |
| `${var^pattern}`  | Capitalizes the **first occurrence** of any character that matches `pattern`. | `heLlo` with `[e] -> hELlo` |
| `${var^^pattern}` | Capitalizes **all occurrences** of any character that matches `pattern`.      | `hello` with `[o] -> hellO` |
| `${var,pattern}`  | Lowercases the **first occurrence** of any character that matches `pattern`.  | `Hello` with `[H] -> hello` |
| `${var,,pattern}` | Lowercases **all occurrences** of any character that matches `pattern`.       | `HeLLo` with `[L] -> Hello` |
### Key Concepts:

1. **Parameter Expansion with Case Modifiers**:
    
    - `${var^}`: Capitalizes the **first character** of the string in `var`.
    - `${var^^}`: Capitalizes **all occurrences** of matching characters in the string.
    - `${var,}`: Lowercases the **first character** of the string in `var`.
    - `${var,,}`: Lowercases **all occurrences** of matching characters in the string.
2. **Bracket Matching with Patterns**:
    
    - You can specify a pattern or characters in brackets (`[ ]`) to apply case modification selectively.
    - If you don't specify a pattern, the default behavior applies to all characters (for `^^` and `,,`) or just the first character (for `^` and `,`).

![[Pasted image 20250128104340.png]]
#### EXPAN.6. Replace the first space characther in the variable's contents with  big .

### **Bash String Substitution Syntax**

bash

CopyEdit

`${variable/pattern/replacement}`

- This replaces **the first occurrence** of `pattern` in `$variable` with `replacement`.
- If you want to replace **all occurrences**, you use:
    
    bash
    
    CopyEdit
    
    `${variable//pattern/replacement}`
    

Now, let's analyze your command:

### **Your Example**

bash

CopyEdit

`perplex@pop-os:~$ echo ${greeting/. / namasthe! }`

**Expected output:** `"hello namasthe!i am batman."`  
**Actual output:** `"hello i am batman."` (No replacement happened)

---

### **Why Didn't It Work?**

1. **Literal Matching in Bash Substitution**
    
    - The pattern `.` (dot followed by space) must match **exactly** in `$greeting`.
    - In Bash substitution, the `.` (dot) **does not act as a wildcard** (unlike in regex).
    - It must be explicitly present in the variable.
2. **Check `$greeting` Value**  
    Run:
    
    bash
    
    CopyEdit
    
    `echo "$greeting"`
    
    If your `$greeting` is:
    
    css
    
    CopyEdit
    
    `hello i am batman.`
    
    Notice there is no `". "` (dot-space) sequence before `"i am batman"`, so Bash doesn't find it to replace.
    

---

### **How to Fix It?**

1. If you meant to replace **just `.`**, you should do:
    
    bash
    
    CopyEdit
    
    `echo ${greeting/. /namasthe! }`
    
    (Notice I removed the space before `namasthe!`.)
    
2. If you meant to replace all dots (`.`), use:
    
    bash
    
    CopyEdit
    
    `echo ${greeting//./namasthe!}`
    
    This will replace **every dot** in `$greeting` with `"namasthe!"`.

  ![[Pasted image 20250129150038.png]]

### **3️⃣ Third Command**

bash

CopyEdit

`echo ${greeting/ / . }`

**Output:**

bash

CopyEdit

`hello . i am batman.`

✅ **Explanation:**

- This replaces **the first space (" ")** with **a dot and a space (". ")**.
- The updated string (temporarily) is:
    
    css
    
    CopyEdit
    
    `hello . i am batman.`
    

---

### **4️⃣ Fourth Command**

bash

CopyEdit

`echo ${greeting/. / namasthe\!}`

**Output:**

bash

CopyEdit

`hello i am batman.`

⚠️ **Why didn't the replacement happen?**

- **Bash is looking for `.` (dot-space), but the actual string still contains "hello i am batman".**
- **The previous command's output (`hello . i am batman.`) was not stored permanently.**
- The **original `greeting`** still does not contain `.` , so Bash finds **no match** to replace.

---

### **🛠️ Fix for Replacing `.` with "namasthe!"**

#### **1. If you want `.` to be replaced in the current session, store it in `greeting`:**

bash

CopyEdit

`greeting="hello . i am batman." echo ${greeting/. / namasthe!}`

**Output:**

bash

CopyEdit

`hello namasthe!i am batman.`

Now the replacement works because `.` exists in `greeting`.

#### **2. Escape `!` properly**

If you want to print `!` literally, you need:

bash

CopyEdit

`echo ${greeting/. / namasthe\!}`

or

bash

CopyEdit

`echo "${greeting/. / namasthe!}"`

Using double quotes prevents Bash from interpreting `!`.

![[Pasted image 20250129151425.png]]
#### EXPAN.6. Replace the first space character in the variable's contents with  big .

![[Pasted image 20250129151627.png]]

#### EXPAN.7. Redirect the contents of the variable greeting into a file whose name is the value of the variable with the spaces replaced by underscores (`_`) and a `.txt` at the end.

![[Pasted image 20250129152137.png]]
#### EXPAN.8. Show the contents of the variable greeting with the middle word fully upper-cased.

![[Pasted image 20250129152815.png]]

The environment is something every process has, while the shell space is only available to bash processes.

```
    ╭─── bash ─────────────────────────╮
    │             ╭──────────────────╮ │
    │ ENVIRONMENT │ SHELL            │ │
    │             │ shell_var1=value │ │
    │             │ shell_var2=value │ │
    │             ╰──────────────────╯ │
    │ ENV_VAR1=value                   │
    │ ENV_VAR2=value                   │
    ╰──────────────────────────────────╯

```

- when u run a new process from shell bash will run this program in a new process when it does , new process do not have shell variables .
- when new process is created  env is populated by making copy of env of creating process

```
    ╭─── bash ───────────────────────╮
    │             ╭────────────────╮ │
    │ ENVIRONMENT │ SHELL          │ │
    │             │ greeting=hello │ │
    │             ╰────────────────╯ │
    │ HOME=/home/lhunath             │
    │ PATH=/bin:/usr/bin             │
    ╰─┬──────────────────────────────╯
      ╎  ╭─── ls ─────────────────────────╮
      └╌╌┥                                │
         │ ENVIRONMENT                    │
         │                                │
         │ HOME=/home/lhunath             │
         │ PATH=/bin:/usr/bin             │
         ╰────────────────────────────────╯
```

