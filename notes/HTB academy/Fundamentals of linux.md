
#linux #bash #hackthebox #linux_fundamentals

Index:
1. System Information [[Fundamentals of linux#System Information]]
2. Navigation [[Fundamentals of linux#Navigation]]
3. working with files and directories [[Fundamentals of linux#Working with Files and Directories]]
4. Find files and Directories [[Fundamentals of linux#Find Files and Directories]]
5. File Descriptors and Redirections [[Fundamentals of linux#File Descriptors and Redirections]]
6. Filter Contents [[Fundamentals of linux#Filter Contents]]
7. 
# System Information

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

# Navigation

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

<mark style="background: #FF5582A6;">Q:</mark> What is the index number of the "sudoers" file in the "/etc" directory?
<mark style="background: #ADCCFFA6;">A: </mark>we can check the inode or index number of a file using "'ls -i [filename]"
```bash
htb-student@nixfund:/etc$ ls -i sudoers
147627 sudoers
htb-student@nixfund:/etc$ 
```

# Working with Files and Directories

<mark style="background: #FF5582A6;">Q: </mark> What is the name of the last modified file in the "/var/backups" directory?
<mark style="background: #ADCCFFA6;">A:  </mark> refer to : https://linuxcommandlibrary.com/man/ls
-it is used to sort the resut by modification date , newest comes first 
```
htb-student@nixfund:/var/backups$ ls -lt
total 2160
-rw-r--r-- 1 root root    41872 Nov 12  2020 apt.extended_states.0
-rw-r--r-- 1 root root     4437 Nov 12  2020 apt.extended_states.1.gz
-rw-r--r-- 1 root root   742750 Nov 11  2020 dpkg.status.0
-rw-r--r-- 1 root root   206270 Nov 11  2020 dpkg.status.1.gz
-rw-r--r-- 1 root root   206270 Nov  5  2020 dpkg.status.2.gz
-rw-r--r-- 1 root root   206270 Nov  5  2020 dpkg.status.3.gz
-rw-r--r-- 1 root root   206270 Nov  5  2020 dpkg.status.4.gz
-rw-r--r-- 1 root root   206270 Nov  5  2020 dpkg.status.5.gz
-rw-r--r-- 1 root root   206270 Nov  5  2020 dpkg.status.6.gz
-rw-r--r-- 1 root root    51200 Oct 29  2020 alternatives.tar.0
-rw-r--r-- 1 root root     4623 Oct 22  2020 apt.extended_states.2.gz
-rw-r--r-- 1 root root     2497 Oct 16  2020 alternatives.tar.1.gz
-rw-r--r-- 1 root root     4601 Oct 15  2020 apt.extended_states.3.gz
-rw-r--r-- 1 root root     2492 Sep 24  2020 alternatives.tar.2.gz
-rw-r--r-- 1 root root      367 Sep 23  2020 dpkg.statoverride.0
-rw-r--r-- 1 root root      229 Sep 23  2020 dpkg.statoverride.1.gz
-rw-r--r-- 1 root root      229 Sep 23  2020 dpkg.statoverride.2.gz
-rw-r--r-- 1 root root      229 Sep 23  2020 dpkg.statoverride.3.gz
-rw-r--r-- 1 root root      229 Sep 23  2020 dpkg.statoverride.4.gz
-rw-r--r-- 1 root root      229 Sep 23  2020 dpkg.statoverride.5.gz
-rw-r--r-- 1 root root      229 Sep 23  2020 dpkg.statoverride.6.gz
-rw-r--r-- 1 root root     4572 Sep 23  2020 apt.extended_states.4.gz
-rw------- 1 root root     2014 Sep 23  2020 passwd.bak
-rw------- 1 root shadow   1362 Sep 23  2020 shadow.bak
-rw------- 1 root shadow    716 Sep 23  2020 gshadow.bak
-rw------- 1 root root      860 Sep 23  2020 group.bak
-rw-r--r-- 1 root root      437 Aug  5  2019 dpkg.diversions.0
-rw-r--r-- 1 root root      202 Aug  5  2019 dpkg.diversions.1.gz
-rw-r--r-- 1 root root      202 Aug  5  2019 dpkg.diversions.2.gz
-rw-r--r-- 1 root root      202 Aug  5  2019 dpkg.diversions.3.gz
-rw-r--r-- 1 root root      202 Aug  5  2019 dpkg.diversions.4.gz
-rw-r--r-- 1 root root      202 Aug  5  2019 dpkg.diversions.5.gz
-rw-r--r-- 1 root root      202 Aug  5  2019 dpkg.diversions.6.gz
htb-student@nixfund:/var/backups$
```
according to the date newest is `apt.extended_states.0`

<mark style="background: #FF5582A6;">Q: </mark>What is the inode number of the "shadow.bak" file in the "/var/backups" directory?
A: using -i we can get the inode or index number of a specific file 
```bash
htb-student@nixfund:/var/backups$ ls -lt -i | grep shadow.bak 
265293 -rw------- 1 root shadow   1362 Sep 23  2020 shadow.bak
265817 -rw------- 1 root shadow    716 Sep 23  2020 gshadow.bak
htb-student@nixfund:/var/backups$ 

```

# Find Files and Directories

<mark style="background: #FF5582A6;">Q: </mark>What is the name of the config file that has been created after 2020-03-03 and is smaller than 28k but larger than 25k?
<mark style="background: #ADCCFFA6;">A: </mark>
```bash
perplex007@htb[/htb]$ find / -type f -name *.conf -user root -size +20k -newermt 2020-03-03 -exec ls -al {} \; 2>/dev/null

-rw-r--r-- 1 root root 136392 Apr 25 20:29 /usr/src/linux-headers-5.5.0-1parrot1-amd64/include/config/auto.conf
-rw-r--r-- 1 root root 82290 Apr 25 20:29 /usr/src/linux-headers-5.5.0-1parrot1-amd64/include/config/tristate.conf
-rw-r--r-- 1 root root 95813 May  7 14:33 /usr/share/metasploit-framework/data/jtr/repeats32.conf
-rw-r--r-- 1 root root 60346 May  7 14:33 /usr/share/metasploit-framework/data/jtr/dynamic.conf
-rw-r--r-- 1 root root 96249 May  7 14:33 /usr/share/metasploit-framework/data/jtr/dumb32.conf
-rw-r--r-- 1 root root 54755 May  7 14:33 /usr/share/metasploit-framework/data/jtr/repeats16.conf
-rw-r--r-- 1 root root 22635 May  7 14:33 /usr/share/metasploit-framework/data/jtr/korelogic.conf
-rwxr-xr-x 1 root root 108534 May  7 14:33 /usr/share/metasploit-framework/data/jtr/john.conf
-rw-r--r-- 1 root root 55285 May  7 14:33 /usr/share/metasploit-framework/data/jtr/dumb16.conf
-rw-r--r-- 1 root root 21254 May  2 11:59 /usr/share/doc/sqlmap/examples/sqlmap.conf
-rw-r--r-- 1 root root 25086 Mar  4 22:04 /etc/dnsmasq.conf
-rw-r--r-- 1 root root 21254 May  2 11:59 /etc/sqlmap/sqlmap.conf
```
in the above session 
- type |Hereby, we define the type of the searched object. In this case, '`f`' stands for '`file'.|
- |`-name *.conf`|With '`-name`', we indicate the name of the file we are looking for. The asterisk (`*`) stands for 'all' files with the '`.conf`' extension.|
- |`-user root`|This option filters all files whose owner is the root user.|
- |`-size +20k`|We can then filter all the located files and specify that we only want to see the files that are larger than 20 KiB|
- |`-newermt 2020-03-03`|With this option, we set the date. Only files newer than the specified date will be presented.|
- |`-exec ls -al {} \;`|This option executes the specified command, using the curly brackets as placeholders for each result. The backslash escapes the next character from being interpreted by the shell because otherwise, the semicolon would terminate the command and not reach the redirection.|
- |`2>/dev/null`|This is a `STDERR` redirection to the '`null device`', which we will come back to in the next section. This redirection ensures that no errors are displayed in the terminal. This redirection must `not` be an option of the 'find' command.|

### 🔍 The Syntax:


`-exec ls -al {} \;`

This is a way to **execute a command on each file** that `find` matches.

---

### 🧠 What Each Part Means:

|Part|Meaning|
|---|---|
|`-exec`|Tells `find` to **execute a command** on each file it finds|
|`ls -al`|This is the command being run — in this case, it's a **long listing (`-l`) with file details** and `-a` to show hidden files (if any)|
|`{}`|A **placeholder** — this is replaced by the **path to the current file** that `find` is processing|
|`\;`|Ends the `-exec` clause. The semicolon (`;`) tells `find` that the command ends here. The **backslash (`\`) escapes** the semicolon to prevent your **shell from interpreting it too early**|

---

### 📦 Example:

Let’s say you run:

`find /etc -name "*.conf" -exec ls -al {} \;`

And let’s say `find` locates:

- `/etc/ssh/sshd_config`
    
- `/etc/logrotate.conf`
    

What really happens behind the scenes is:

`ls -al /etc/ssh/sshd_config ls -al /etc/logrotate.conf`

It runs the `ls -al` command separately **for each file found**.

---

### 🛡️ Why the Backslash?

In Bash or most shells:

- `;` normally **ends a shell command**
    
- So if you wrote `-exec ls -al {}; ;`, the shell thinks the first command ended **before `find` is finished**
    

✅ `\;` tells the shell:

> "Hey, this semicolon is part of the `find` command — don't interpret it yet."

---

### ✅ Summary:

`-exec ls -al {} \;`

> For every file found by `find`, **run `ls -al` on that file**, with `{}` being replaced by the file path. Use `\;` to end the `-exec` safely.

```bash
htb-student@nixfund:~$ find / -type f -name "*.conf" -user root -size +25k -size -28k -newermt 2020-03-03 -exec ls -al {} \; 2>/dev/null

-rw-r--r-- 1 root root 27422 Jun 12  2020 /usr/share/drirc.d/00-mesa-defaults.conf
htb-student@nixfund:~$ 
```

<mark style="background: #FF5582A6;">Q: </mark>Submit the full path of the "xxd" binary.
<mark style="background: #ADCCFFA6;">A:</mark>  `xxd` – Make a hexdump or do the reverse
- Creates a **hex dump** of a file or stdin.
- Can **revert** a hex dump back to binary.
- Useful for viewing binary files or patching binaries.
refer to [[Fundamentals of linux#hex dump xxd]]
```bash 
htb-student@nixfund:~$ which xxd
/usr/bin/xxd
htb-student@nixfund:~$ 
```


# File Descriptors and Redirections

<mark style="background: #FF5582A6;">Q:</mark>How many files exist on the system that have the ".log" file extension?
<mark style="background: #ADCCFFA6;">A: </mark>
```bash
htb-student@nixfund:~$ find / -type f -name "*.log" 2>/dev/null | wc -l
32
htb-student@nixfund:~$ 
```

<mark style="background: #FF5582A6;">Q: </mark> How many total packages are installed on the target system?
<mark style="background: #ADCCFFA6;">A: </mark>using dpkg -l packages can be listed 
```
htb-student@nixfund:~$ dpkg -l
Desired=Unknown/Install/Remove/Purge/Hold
| Status=Not/Inst/Conf-files/Unpacked/halF-conf/Half-inst/trig-aWait/Trig-pend
|/ Err?=(none)/Reinst-required (Status,Err: uppercase=bad)
||/ Name                Version        Architecture   Description
+++-===================-==============-==============-============================================
ii  accountsservice     0.6.45-1ubuntu amd64          query and manipulate user account informatio
ii  acl                 2.2.52-3build1 amd64          Access control list utilities
ii  acpid               1:2.0.28-1ubun amd64          Advanced Configuration and Power Interface e
ii  adduser             3.116ubuntu1   all            add and remove users and groups
ii  adwaita-icon-theme  3.28.0-1ubuntu all            default icon theme of GNOME (small subset)
ii  amd64-microcode     3.20191021.1+r amd64          Processor microcode firmware for AMD CPUs

```

dpkg starts with the two letters that show the status of the each package.
first -i = the package desired state is install 
second i = the package is currently installed
So if you see:

`ii  nmap   7.80-1  amd64   Network exploration tool and security scanner`

That means:

- `nmap` is **properly installed** and functioning.

`grep '^ii'`: Filters lines where the package is **installed** (marked with `ii`).

```bash
htb-student@nixfund:~$ dpkg -l | grep '^ii' | wc -l
737
htb-student@nixfund:~$ 
```

#### Mail question explanation

## Linux Mail System Basics

 🔹 1. Where is mail stored?

In traditional Linux systems (especially on Debian-based ones like Ubuntu), **local email for system users** is stored in:

`/var/mail/`

This is a **directory** where each file is named after the **username** of the recipient.

So if there’s a user `htb-student`, their mail is stored at:

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

#### hex dump xxd
### 🔹 **Examples**

**Hexdump a file:**
`xxd file`

**Reverse hexdump:**

`xxd -r hexfile > binaryfile`

**Plain hex dump (continuous):**

`xxd -p -c 20 -l 120 file`

**Dump from byte offset 0x30 onward:**
`xxd -s 0x30 file`

**Patch binary file at offset 0x37:**

`echo "0000037: 3574 68" | xxd -r - file`

**Generate C-style hex array:**

`xxd -i file`

**Create a 65537-byte file with last byte = 'A':**
`echo "010000: 41" | xxd -r > file`

---

### 🔹 **Editor Integration (e.g., Vim)**

Hexdump selected lines:

`:'a,'z!xxd`

Reverse hex dump:

`:'a,'z!xxd -r`

---

### 🔹 **Caveats**

- `xxd -r` ignores anything after the needed hex bytes per line.
    
- ASCII column in the dump is ignored during reverse.
    
- `-s` behaves differently with `+` when reading from stdin (due to file pointer behavior).


# Filter Contents

- more - more content of the file 
### `cat /etc/passwd`

- This command **displays the entire content** of `/etc/passwd` file all at once in the terminal.
    
- If the file is large, it will scroll off the screen quickly, and you might miss part of it.

### `cat /etc/passwd | more`

- This command **pipes the output** of `cat /etc/passwd` into the `more` pager.
    
- `more` **lets you scroll one screen at a time**, making it easier to read large files.
    
- You press `Space` to go to the next page or `q` to quit.

### Less

If we now take a look at the tool `less`, we will notice on the man page that it contains many more features than `more`.
it opens like a new screen and wait for input if u give q as input it will quit

ref: https://linux.die.net/man/1/less
ref: https://man7.org/linux/man-pages/man1/more.1.html

### Head

Sometimes we will only be interested in specific issues either at the beginning of the file or the end. If we only want to get the `first` lines of the file, we can use the tool `head`. By default, `head` prints the first ten lines of the given file or input, if not specified otherwise.


### Tail

If we only want to see the last parts of a file or results, we can use the counterpart of `head` called `tail`, which returns the `last` ten lines.

```shell-session
[!bash!]$ tail /etc/passwd

miredo:x:115:65534::/var/run/miredo:/usr/sbin/nologin
usbmux:x:116:46:usbmux daemon,,,:/var/lib/usbmux:/usr/sbin/nologin
rtkit:x:117:119:RealtimeKit,,,:/proc:/usr/sbin/nologin
nm-openvpn:x:118:120:NetworkManager OpenVPN,,,:/var/lib/openvpn/chroot:/usr/sbin/nologin
nm-openconnect:x:119:121:NetworkManager OpenConnect plugin,,,:/var/lib/NetworkManager:/usr/sbin/nologin
pulse:x:120:122:PulseAudio daemon,,,:/var/run/pulse:/usr/sbin/nologin
beef-xss:x:121:124::/var/lib/beef-xss:/usr/sbin/nologin
lightdm:x:122:125:Light Display Manager:/var/lib/lightdm:/bin/false
do-agent:x:998:998::/home/do-agent:/bin/false
user6:x:1000:1000:,,,:/home/user6:/bin/bash
```
### Sort

Depending on which results and files are dealt with, they are rarely sorted. Often it is necessary to sort the desired results alphabetically or numerically to get a better overview. For this, we can use a tool called `sort`.

```shell-session
[!bash!]$ cat /etc/passwd | sort

_apt:x:104:65534::/nonexistent:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
cry0l1t3:x:1001:1001::/home/cry0l1t3:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
dnsmasq:x:107:65534:dnsmasq,,,:/var/lib/misc:/usr/sbin/nologin
dovecot:x:114:117:Dovecot mail server,,,:/usr/lib/dovecot:/usr/sbin/nologin
dovenull:x:115:118:Dovecot login user,,,:/nonexistent:/usr/sbin/nologin
ftp:x:113:65534::/srv/ftp:/usr/sbin/nologin
games:x:5:60:games:/usr/games:/usr/sbin/nologin
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin
htb-student:x:1002:1002::/home/htb-student:/bin/bash
<SNIP>
```
### Grep

In many cases, we will need to search for specific results that match patterns we define. One of the most commonly used tools for this purpose is grep, which provides a wide range of powerful features for pattern searching. For instance, we can use grep to search for users who have their default shell set to `/bin/bash`.

```bash
[!bash!]$ cat /etc/passwd | grep "/bin/bash"

root:x:0:0:root:/root:/bin/bash
mrb3n:x:1000:1000:mrb3n:/home/mrb3n:/bin/bash
cry0l1t3:x:1001:1001::/home/cry0l1t3:/bin/bash
htb-student:x:1002:1002::/home/htb-student:/bin/bash
```
### Cut
To remove unnecessary character from the desired output cut is used -d is used to set the delimiter with -f is used to specify the position in the line we want output 

```shell-session
[!bash!]$ cat /etc/passwd | grep -v "false\|nologin"

root:x:0:0:root:/root:/bin/bash
sync:x:4:65534:sync:/bin:/bin/sync
postgres:x:111:117:PostgreSQL administrator,,,:/var/lib/postgresql:/bin/bash
user6:x:1000:1000:,,,:/home/user6:/bin/bash
```

## Tr
To replace a certain character from a line with characters  the syntax is first option we define character we want to replace  and second option we define character we want to replace with

```shell-session
perplex007@htb[/htb]$ cat /etc/passwd | grep -v "false\|nologin" | tr ":" " "

root x 0 0 root /root /bin/bash
sync x 4 65534 sync /bin /bin/sync
postgres x 111 117 PostgreSQL administrator,,, /var/lib/postgresql /bin/bash
mrb3n x 1000 1000 mrb3n /home/mrb3n /bin/bash
cry0l1t3 x 1001 1001  /home/cry0l1t3 /bin/bash
htb-student x 1002 1002  /home/htb-student /bin/bash
```

## Column

used to diplay results in tabular format using -t

```shell-session
perplex007@htb[/htb]$ cat /etc/passwd | grep -v "false\|nologin" | tr ":" " " | column -t

root         x  0     0      root               /root        		 /bin/bash
sync         x  4     65534  sync               /bin         		 /bin/sync
postgres     x  111   117    PostgreSQL         administrator,,,    /var/lib/postgresql		/bin/bash
mrb3n        x  1000  1000   mrb3n              /home/mrb3n  	     /bin/bash
cry0l1t3     x  1001  1001   /home/cry0l1t3     /bin/bash
htb-student  x  1002  1002   /home/htb-student  /bin/bash
```

## Awk

As we may have noticed, the line for the user "`postgres`" has one column too many. To keep it as simple as possible to sort out such results, the (`g`)`awk` programming is beneficial, which allows us to display the first (`$1`) and last (`$NF`) result of the line.

**`awk`** is a programming language designed for **pattern scanning and processing**. It's mostly used to manipulate and analyze **structured text files**, like CSVs, logs, or any column-based data.

It works line by line, **splitting each line into fields** (usually by whitespace or a specified delimiter), and then lets you perform actions based on those fields.

## Basic `awk` Syntax

`awk '{action}' filename`

Or if you're piping data:

`some_command | awk '{action}'`

- Each line is automatically split into **fields**: `$1`, `$2`, `$3`, ..., `$NF`
    
    - `$1`: first field
        
    - `$2`: second field
        
    - `$NF`: last field (`NF` = Number of Fields)

### 1. Print first column of a file:

`awk '{print $1}' file.txt`

### 2. Print first and third column:

`awk '{print $1, $3}' file.txt`

### 3. Print lines where the second field is greater than 100:

`awk '$2 > 100 {print $0}' file.txt`

### 4. Use custom delimiter (e.g., colon `:` in `/etc/passwd`):


`awk -F ':' '{print $1, $7}' /etc/passwd`

- `-F ':'` tells `awk` to split fields by `:` instead of whitespace.

```shell-session
perplex007@htb[/htb]$ cat /etc/passwd | grep -v "false\|nologin" | tr ":" " " | awk '{print $1, $NF}'

root /bin/bash
sync /bin/sync
postgres /bin/bash
mrb3n /bin/bash
cry0l1t3 /bin/bash
htb-student /bin/bash
```

### `cat /etc/passwd`

- Displays the contents of the `/etc/passwd` file.
    
- This file stores **user account information**.
    
- Each line represents a user and follows this structure:
    

`username:password:UID:GID:comment:home_directory:shell`

`htb-student:x:1001:1001::/home/htb-student:/bin/bash`

---

### 🔹 2. `grep -v "false\|nologin"`

- `grep -v`: Invert match — it **excludes** lines that match the pattern.
    
- `false\|nologin`: This regex matches lines containing either `false` or `nologin` (which are non-interactive shells).
    

So this step **filters out system users** or disabled users like:

`nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin`

---

### 🔹 3. `tr ":" " "`

- `tr` (translate) replaces characters.
    
- Here, it's **replacing colons (`:`) with spaces**, so `awk` can split fields by whitespace.
    

`htb-student:x:1001:1001::/home/htb-student:/bin/bash`

`htb-student x 1001 1001  /home/htb-student /bin/bash`

---

### 🔹 4. `awk '{print $1, $NF}'`

- `awk` processes each line, split into **fields** (default separator is whitespace).
    
- `$1`: First field → **username**
    
- `$NF`: Last field → **shell**
    

So, for:

`htb-student x 1001 1001  /home/htb-student /bin/bash`

We get:

`htb-student /bin/bash`

---

## ✅ Final Output:
`root /bin/bash 
`sync /bin/sync
`postgres /bin/bash 
`mrb3n /bin/bash 
`cry0l1t3 /bin/bash 
`htb-student /bin/bash`

### 💡 Interpretation:

This tells us that:

- These users have valid login shells (`/bin/bash` or `/bin/sync`).
    
- They are **not disabled/system accounts**.
    
- Useful in security auditing or CTFs to identify valid interactive user accounts.



## Sed

a stream editor used to replace a pattern matching with one regular expression with another regular expression pattern 

Let us stick to the last results and say we want to replace the word "`bin`" with "`HTB`."

```shell-session
perplex007@htb[/htb]$ cat /etc/passwd | grep -v "false\|nologin" | tr ":" " " | awk '{print $1, $NF}' | sed 's/bin/HTB/g'

root /HTB/bash
sync /HTB/sync
postgres /HTB/bash
mrb3n /HTB/bash
cry0l1t3 /HTB/bash
htb-student /HTB/bash
```

The "`s`" flag at the beginning stands for the substitute command. Then we specify the pattern we want to replace. After the slash (`/`), we enter the pattern we want to use as a replacement in the third position. Finally, we use the "`g`" flag, which stands for replacing all matches.

## Wc

To avoid counting the lines or characters manually, we can use the tool `wc`. With the "`-l`" option, we specify that only the lines are counted.

  Filter Contents

```shell-session
perplex007@htb[/htb]$ cat /etc/passwd | grep -v "false\|nologin" | tr ":" " " | awk '{print $1, $NF}' | wc -l

6
```

<mark style="background: #FF5582A6;">Q: </mark>How many services are listening on the target system on all interfaces? (Not on localhost and IPv4 only)
<mark style="background: #ADCCFFA6;">A:</mark> 7
netstat -l is going to list the services running on the system 

![[Pasted image 20250518172918.png]]

in the above image among the rcp services mentioned there are total of 7 services on IPV4

Q: Determine what user the ProFTPd server is running under. Submit the username as the answer.
