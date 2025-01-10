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

