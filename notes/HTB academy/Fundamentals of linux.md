
Use Tags

<mark style="background: #FF5582A6;">Q:</mark> Find out the machine hardware name and submit it as the answer.
<mark style="background: #ADCCFFA6;">A: </mark> Ref: https://www.man7.org/linux/man-pages/man1/uname.1.html
       Print certain system information.  With no OPTION, same as **-s**.
              **-m**, **--machine**
              print the machine hardware name

<mark style="background: #FF5582A6;">Q:</mark> What is the path to htb-student's home directory?
<mark style="background: #ADCCFFA6;">A: </mark> pwd is command that is going to print the working directory
	 htb-student@nixfund:~$ pwd
	/home/htb-student

<mark style="background: #FF5582A6;">Q:</mark> What is the path to the htb-student's mail?
<mark style="background: #ADCCFFA6;">A: </mark> In Linux everything is a file so we do have a directory for htb-Student's mail we can navigate to the root directory '/' and then if we do ls we do have a mail directory
```bash
htb-student@nixfund:/var$ ls
backups  crash  local  log   opt  snap   tmp
cache    lib    lock   mail  run  spool  www
```
then first i thought the answer is /var/mail no, 
 where is htb-student in /var/mail/? /var/mail/htb-student.
<mark style="background: #FFB8EBA6;">The usual style in Linux is that every user with a home directory has their mail stored in the /var/mail/$USER directory.</mark>
Refer [[Fundamentals of linux#Linux Mail System Basics]]

<mark style="background: #FF5582A6;">Q:</mark>Which shell is specified for the htb-student user?
<mark style="background: #ADCCFFA6;">A:</mark>refer: https://phoenixnap.com/kb/linux-shells
**prints all the environment variables** currently set for the shell session of the user (in this case, `htb-student`). contains our output
SHELL=/bin/bash

<mark style="background: #FF5582A6;">Q:</mark> Which kernel release is installed on the system? (Format: 1.22.3)
<mark style="background: #ADCCFFA6;">A: </mark> again for this we can use the Uname command uname -r gives us the version that system is running
```bash
htb-student@nixfund:/var/mail$ uname -r
4.15.0-123-generic
```

<mark style="background: #FF5582A6;">Q: </mark>What is the name of the network interface that MTU is set to 1500?
<mark style="background: #ADCCFFA6;">A: </mark>MTU: is the maximum transfer unit for the specific network interface 
- In Linux, the Maximum Transmission Unit (MTU) is the largest packet size that can be transmitted over a network interface without fragmentation. 
- The default MTU size for Ethernet is 1500 bytes, but it can be changed for specific needs, such as using jumbo frames with an MTU size of 9000 bytes to improve performance on VLANs.

```bash
ip a | grep mtu
```
used to check the mtu value for network interfaces

```bash
htb-student@nixfund:/var/mail$ ip a | grep mtu
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
2: ens192: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
htb-student@nixfund:/var/mail$ 

```
in this case mtu value is 1500 for ens192

<mark style="background: #FF5582A6;">Q: </mark>What is the name of the hidden "history" file in the htb-user's home directory?
<mark style="background: #ADCCFFA6;">A:</mark> bash stores all the history in .bash_history file  in the home directory all 3 users contain the bash_history file  whcih can seen with the command ls -la

```bash
htb-student@nixfund:~$ ls -la
total 32
drwxr-xr-x 4 htb-student htb-student 4096 Aug  3  2021 .
drwxr-xr-x 5 root        root        4096 Aug  3  2021 ..
-rw------- 1 htb-student htb-student    5 Sep 23  2020 .bash_history
-rw-r--r-- 1 htb-student htb-student  220 Apr  4  2018 .bash_logout
-rw-r--r-- 1 htb-student htb-student 3771 Apr  4  2018 .bashrc
drwx------ 2 htb-student htb-student 4096 Aug  3  2021 .cache
drwx------ 3 htb-student htb-student 4096 Aug  3  2021 .gnupg
-rw-r--r-- 1 htb-student htb-student  807 Apr  4  2018 .profile
htb-student@nixfund:~$ 
```

#### Mail question explanation

## Linux Mail System Basics

 🔹 1. Where is mail stored?

In traditional Linux systems (especially on Debian-based ones like Ubuntu), **local email for system users** is stored in:

bash

CopyEdit

`/var/mail/`

This is a **directory** where each file is named after the **username** of the recipient.

So if there’s a user `htb-student`, their mail is stored at:

bash

CopyEdit

`/var/mail/htb-student`

---

🔹 2. So what is `/var/mail`?

Think of `/var/mail` as:

> 📁 A folder that contains **inbox files** for every user on the system.

`$ ls /var/mail root       htb-student       alice       bob`

Each file inside `/var/mail/` holds the **mail messages** for that user.

---

 🔹 3. Why is it `/var/mail/htb-student` and not just `/var/mail`?

Because:

- `/var/mail` is just the **folder**.
    
- `/var/mail/htb-student` is the **file** that holds **htb-student’s inbox**.
    

Each user has their **own file** in there:

`/var/mail/$USER`

So:

- For `root` → `/var/mail/root`
    
- For `htb-student` → `/var/mail/htb-student`
    


**Q:** What is the path to the htb-student’s mail?  
**A:**`/var/mail/htb-student`

This file contains all mail received by the user `htb-student`.


#### environment question

### What are environment variables?

They are **key-value pairs** that define how processes run in your shell. For example:

|Variable|Value|Meaning|
|---|---|---|
|`USER`|`htb-student`|The username of the current user|
|`HOME`|`/home/htb-student`|The user's home directory|
|`SHELL`|`/bin/bash`|The default shell the user is using|
|`PATH`|`/usr/local/sbin:/usr/local/bin:...`|Tells the shell where to look for commands|
|`MAIL`|`/var/mail/htb-student`|The path to the user’s mail file|
|`PWD`|`/var/mail`|Present working directory|
|`TERM`|`xterm-256color`|Terminal type (used for formatting output)|
|`LANG`|`en_US.UTF-8`|System language and encoding|
|`SSH_CLIENT`|`10.10.14.105 35848 22`|SSH client IP and port info (you're connected over SSH)|
|`LS_COLORS`|(long color code string)|Used to define colors for file types in terminal|

---

### 🧠 Use Cases for `env`

- Debugging environment issues (e.g., wrong `$PATH`)
    
- Checking where your mail is (`$MAIL`)
    
- Finding out default language (`$LANG`)
    
- Verifying if you're in an SSH session (`$SSH_CLIENT`, `$SSH_CONNECTION`)
    
- Checking what shell or terminal you're using (`$SHELL`, `$TERM`)


## CHEAT SHEET

| **Command**              | **Description**                                                                                                                                            |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `man <tool>`             | Opens man pages for the specified tool.                                                                                                                    |
| `<tool> -h`              | Prints the help page of the tool.                                                                                                                          |
| `apropos <keyword>`      | Searches through man pages' descriptions for instances of a given keyword.                                                                                 |
| `cat`                    | Concatenate and print files.                                                                                                                               |
| `whoami`                 | Displays current username.                                                                                                                                 |
| `id`                     | Returns users identity.                                                                                                                                    |
| `hostname`               | Sets or prints the name of the current host system.                                                                                                        |
| `uname`                  | Prints operating system name.                                                                                                                              |
| `pwd`                    | Returns working directory name.                                                                                                                            |
| `ifconfig`               | The `ifconfig` utility is used to assign or view an address to a network interface and/or configure network interface parameters.                          |
| `ip`                     | Ip is a utility to show or manipulate routing, network devices, interfaces, and tunnels.                                                                   |
| `netstat`                | Shows network status.                                                                                                                                      |
| `ss`                     | Another utility to investigate sockets.                                                                                                                    |
| `ps`                     | Shows process status.                                                                                                                                      |
| `who`                    | Displays who is logged in.                                                                                                                                 |
| `env`                    | Prints environment or sets and executes a command.                                                                                                         |
| `lsblk`                  | Lists block devices.                                                                                                                                       |
| `lsusb`                  | Lists USB devices.                                                                                                                                         |
| `lsof`                   | Lists opened files.                                                                                                                                        |
| `lspci`                  | Lists PCI devices.                                                                                                                                         |
| `sudo`                   | Execute command as a different user.                                                                                                                       |
| `su`                     | The `su` utility requests appropriate user credentials via PAM and switches to that user ID (the default user is the superuser). A shell is then executed. |
| `useradd`                | Creates a new user or update default new user information.                                                                                                 |
| `userdel`                | Deletes a user account and related files.                                                                                                                  |
| `usermod`                | Modifies a user account.                                                                                                                                   |
| `addgroup`               | Adds a group to the system.                                                                                                                                |
| `delgroup`               | Removes a group from the system.                                                                                                                           |
| `passwd`                 | Changes user password.                                                                                                                                     |
| `dpkg`                   | Install, remove and configure Debian-based packages.                                                                                                       |
| `apt`                    | High-level package management command-line utility.                                                                                                        |
| `aptitude`               | Alternative to `apt`.                                                                                                                                      |
| `snap`                   | Install, remove and configure snap packages.                                                                                                               |
| `gem`                    | Standard package manager for Ruby.                                                                                                                         |
| `pip`                    | Standard package manager for Python.                                                                                                                       |
| `git`                    | Revision control system command-line utility.                                                                                                              |
| `systemctl`              | Command-line based service and systemd control manager.                                                                                                    |
| `ps`                     | Prints a snapshot of the current processes.                                                                                                                |
| `journalctl`             | Query the systemd journal.                                                                                                                                 |
| `kill`                   | Sends a signal to a process.                                                                                                                               |
| `bg`                     | Puts a process into background.                                                                                                                            |
| `jobs`                   | Lists all processes that are running in the background.                                                                                                    |
| `fg`                     | Puts a process into the foreground.                                                                                                                        |
| `curl`                   | Command-line utility to transfer data from or to a server.                                                                                                 |
| `wget`                   | An alternative to `curl` that downloads files from FTP or HTTP(s) server.                                                                                  |
| `python3 -m http.server` | Starts a Python3 web server on TCP port 8000.                                                                                                              |
| `ls`                     | Lists directory contents.                                                                                                                                  |
| `cd`                     | Changes the directory.                                                                                                                                     |
| `clear`                  | Clears the terminal.                                                                                                                                       |
| `touch`                  | Creates an empty file.                                                                                                                                     |
| `mkdir`                  | Creates a directory.                                                                                                                                       |
| `tree`                   | Lists the contents of a directory recursively.                                                                                                             |
| `mv`                     | Move or rename files or directories.                                                                                                                       |
| `cp`                     | Copy files or directories.                                                                                                                                 |
| `nano`                   | Terminal based text editor.                                                                                                                                |
| `which`                  | Returns the path to a file or link.                                                                                                                        |
| `find`                   | Searches for files in a directory hierarchy.                                                                                                               |
| `updatedb`               | Updates the locale database for existing contents on the system.                                                                                           |
| `locate`                 | Uses the locale database to find contents on the system.                                                                                                   |
| `more`                   | Pager that is used to read STDOUT or files.                                                                                                                |
| `less`                   | An alternative to `more` with more features.                                                                                                               |
| `head`                   | Prints the first ten lines of STDOUT or a file.                                                                                                            |
| `tail`                   | Prints the last ten lines of STDOUT or a file.                                                                                                             |
| `sort`                   | Sorts the contents of STDOUT or a file.                                                                                                                    |
| `grep`                   | Searches for specific results that contain given patterns.                                                                                                 |
| `cut`                    | Removes sections from each line of files.                                                                                                                  |
| `tr`                     | Replaces certain characters.                                                                                                                               |
| `column`                 | Command-line based utility that formats its input into multiple columns.                                                                                   |
| `awk`                    | Pattern scanning and processing language.                                                                                                                  |
| `sed`                    | A stream editor for filtering and transforming text.                                                                                                       |
| `wc`                     | Prints newline, word, and byte counts for a given input.                                                                                                   |
| `chmod`                  | Changes permission of a file or directory.                                                                                                                 |
| `chown`                  | Changes the owner and group of a file or directory.                                                                                                        |