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

