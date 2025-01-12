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
    
    bash
    
    Copy code
    
    `type -a ls`


