
#linux #bash #hackthebox #linux_fundamentals

Index:
1. System Information [[Fundamentals of linux#System Information]]
2. Navigation [[Fundamentals of linux#Navigation]]
3. working with files and directories [[Fundamentals of linux#Working with Files and Directories]]
4. Find files and Directories [[Fundamentals of linux#Find Files and Directories]]
5. File Descriptors and Redirections [[Fundamentals of linux#File Descriptors and Redirections]]
6. Filter Contents [[Fundamentals of linux#Filter Contents]]
7. Regular Expressisons [[Fundamentals of linux#Regular Expressions]]
8. Permission management [[Fundamentals of linux#Permission management]]
9. User Management [[Fundamentals of linux#User Management]]
10. Package Management [[Fundamentals of linux#Package Management]]
11. Service and Process Management [[Fundamentals of linux#Service and Process Management]]
12. Task Scheduling [[Fundamentals of linux#Task Scheduling]]
13. Network Services [[Fundamentals of linux#Network Services]]
14. working with web services [[Fundamentals of linux#Working with Web Services]]
15. Backup and Restore [[Fundamentals of linux#Backup and Restore]]
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

<mark style="background: #FF5582A6;">Q: </mark>Determine what user the ProFTPd server is running under. Submit the username as the answer.
<mark style="background: #ADCCFFA6;">A: </mark>in linux everything is a file including services so i google where wis the ProFTPd file is present it's in /etc/proftpd, in tht there is afile named ProFTPd.conf whcih contain information about the services running which includes the user of tht service 

![[Pasted image 20250518174146.png]]


Q:  Use cURL from your Pwnbox (not the target machine) to obtain the source code of the "https://www.inlanefreight.com" website and filter all unique paths (https://www.inlanefreight.com/directory" or "/another/directory") of that domain. Submit the number of these paths as the answer.

A: 34 

```bash
curl [https://www.inlanefreight.com/](https://www.inlanefreight.com/) | grep –Po https://www.inlanefreight.com[^’\]*” |sort –u | wc — l
```

### Regular Expressions 

## Grouping

Among other things, regex offers us the possibility to group the desired search patterns. Basically, regex follows three different concepts, which are distinguished by the three different brackets:

### Grouping Operators

||**Operators**|**Description**|
|---|---|---|
|1|`(a)`|The round brackets are used to group parts of a regex. Within the brackets, you can define further patterns which should be processed together.|
|2|`[a-z]`|The square brackets are used to define character classes. Inside the brackets, you can specify a list of characters to search for.|
|3|`{1,10}`|The curly brackets are used to define quantifiers. Inside the brackets, you can specify a number or a range that indicates how often a previous pattern should be repeated.|
|4|`\|`|Also called the OR operator and shows results when one of the two expressions matches|
|5|`.*`|Operates similarly to an AND operator by displaying results only when both expressions are present and match in the specified order|

#### OR operator

  Regular Expressions

```shell-session
cry0l1t3@htb:~$ grep -E "(my|false)" /etc/passwd

lxd:x:105:65534::/var/lib/lxd/:/bin/false
pollinate:x:109:1::/var/cache/pollinate:/bin/false
mysql:x:116:120:MySQL Server,,:/nonexistent:/bin/false
```

Since one of the two search parameters always occurs in the three lines, all three lines are displayed accordingly. However, if we use the `AND` operator, we will get a different result for the same search parameters.

#### AND operator

  Regular Expressions

```shell-session
cry0l1t3@htb:~$ grep -E "(my.*false)" /etc/passwd

mysql:x:116:120:MySQL Server,,:/nonexistent:/bin/false
```

Basically, what we are saying with this command is that we are looking for a line where we want to see both `my` and `false`. A simplified example would also be to use `grep` twice and look like this:

  Regular Expressions

```shell-session
cry0l1t3@htb:~$ grep -E "my" /etc/passwd | grep -E "false"

mysql:x:116:120:MySQL Server,,:/nonexistent:/bin/false
```

---

Here are some optional tasks to help you practice RegEx and improve your ability to handle them more effectively. These exercises will use the `/etc/ssh/sshd_config` file on your `Pwnbox` instance, allowing you to explore real-world applications of RegEx in a configuration file. By completing these tasks, you'll gain hands-on experience in working with patterns, searching, and manipulating text in practical scenarios.

<mark style="background: #FF5582A6;">Q: </mark>Show all lines that do not contain the # character.
<mark style="background: #ADCCFFA6;">A: </mark>
```bash
grep -v '#' filename
```
-v inverts the match print non matching stuff

<mark style="background: #FF5582A6;">Q: </mark>Search for all lines that contain a word that starts
<mark style="background: #ADCCFFA6;">A: </mark>grep '\bPermit' [filename]

- `\b` matches a **word boundary**, ensuring that "Permit" is the start of a word.
    
- `grep` interprets `*` differently — it matches **zero or more of the preceding character**, so `permit*` means "permi" followed by zero or more "t"s

<mark style="background: #FF5582A6;">Q: </mark>Search for all lines that contain a word ending with `Authentication`.
<mark style="background: #ADCCFFA6;">A: </mark>
`grep '\<.*Authentication\>' filename`

---

### 🔍 Explanation:

- `\<` — start of a word boundary
    
- `.*Authentication` — any characters ending in "Authentication"
    
- `\>` — end of a word boundary
    

Alternatively, you can use:

`grep -E '\b\w*Authentication\b' filename`

- `-E` enables **extended regex**
    
- `\b` matches a **word boundary**
    
- `\w*Authentication` matches any word ending in "Authentication"

<mark style="background: #FF5582A6;">Q: </mark>Search for all lines containing the word `Key`.
<mark style="background: #ADCCFFA6;">A: </mark>grep '\<Key\>' filename

 To match "Key" regardless of case (key, Key, KEY, etc):
 
`grep -i -E '\bKey\b' filename`

Let me know if you're using macOS or Linux — I’ll tailor it exactly to your setup.

Q: Search for all lines beginning with `Password` and containing `yes`.
A: 
grep understands three different  versions  of  regular  expression
       syntax:  “basic” (BRE), “extended” (ERE) and “perl” (PCRE).  In GNU
       grep there is no  difference  in  available  functionality  between
       basic  and  extended  syntaxes.   In  other  implementations, basic
       regular expressions are less powerful. 

```bash
grep '^Password.*yes' filename
```

Q: Search for all lines that end with 'yes'
A: 
grep 'yes$' filename
Explanation:

yes$ matches lines that end with the word yes.
$ asserts end of line.

If you're looking for exactly the word "yes" at the end (not "always" or "notyes"), you can make it stricter:

grep '\<yes\>$' filename
\< — start of the word
\> — end of the word
\<yes\>$ ensures only 'yes' as a whole word appears at the end of the line.

### Permission management

## SUID & SGID

- Linux allows us to configure special permissions on files through the Set User ID (`SUID`) and Set Group ID (`SGID`) bits.
- function like temporary access passes, enabling users to run certain programs with the privileges of another user or group
- administrators can use `SUID` or `SGID` to grant users elevated rights for specific applications, allowing tasks to be performed with the necessary permissions, even if the user themselves doesn’t normally have them.
```shell-session
cry0l1t3@htb[/htb]$ ls -l shell

-rwxr-x--x   1 cry0l1t3 htbteam 0 May  4 22:12 shell
```

| Field | Meaning                                  |
| ----- | ---------------------------------------- |
| `-`   | Regular file                             |
| `rwx` | Owner (`cry0l1t3`): read, write, execute |
| `r-x` | Group (`htbteam`): read, execute         |
| `--x` | Others: execute only                     |

One common risk is when administrators, unfamiliar with an application's full functionality, assign `SUID` or `SGID` bits indiscriminately. For example, if the `SUID` bit is applied to a program like `journalctl`, which includes a function to launch a shell from within its interface, any user running this program could execute a shell as root. This grants them complete control over the system, presenting a significant security vulnerability. More information about this and other such applications can be found at [GTFObins](https://gtfobins.github.io/gtfobins/journalctl/).

## Sticky Bit
- Sticky bits in Linux are like locks on files within shared spaces
- ensures only certain users can modify or delete files , even if other have access to the directory
- This feature is especially useful in shared environments, like public directories, where multiple users are working together.
By setting the sticky bit, you ensure that important files aren’t accidentally or maliciously altered by someone who shouldn’t have the authority to do so, adding an important safeguard to collaborative workspaces.

```shell-session
cry0l1t3@htb[/htb]$ ls -l

drw-rw-r-t 3 cry0l1t3 cry0l1t3   4096 Jan 12 12:30 scripts
drw-rw-r-T 3 cry0l1t3 cry0l1t3   4096 Jan 12 12:32 reports
```

In this example, we see that both directories have the sticky bit set. However, the `reports` folder has an uppercase `T`, and the `scripts` folder has a lowercase `t`.

If the sticky bit is capitalized (`T`), then this means that all other users do not have `execute` (`x`) permissions and, therefore, cannot see the contents of the folder nor run any programs from it. The lowercase sticky bit (`t`) is the sticky bit where the `execute` (`x`) permissions have been set.

# User Management
-  Administrators frequently need to create new user accounts or assign existing users to specific groups to enforce appropriate access controls. Additionally, executing commands as a different user is often necessary for tasks that require different privileges.
- example: certain groups need permissions to modify files or directories essential for maintaining system security and integrity 
- allows us to gather more detailed info locally on that machine 
- imp for troubleshooting and auditing purposes

```
imagine a new employee named Alex joins your company and is provided with a Linux-based workstation to perform their tasks. As a system administrator, you need to create a user account for Alex and add them to the appropriate groups that grant access to necessary resources, such as project files or development tools. Additionally, there may be situations where Alex needs to execute commands with elevated privileges or as a different user to complete certain tasks.
```

#### Execution as a user
```shell-session
perplex007@htb[/htb]$ cat /etc/shadow

cat: /etc/shadow: Permission denied
```
- /etc/shadow file is a critical system stores encrypted password information for all user accounts
- For security reasons it is readable and writable only by the root user to prevent unauthorized access to sensitive data 
-  users can utilize the `sudo` command. The `sudo` command, short for "superuser do," allows permitted users to execute commands with the security privileges of another user, typically the superuser or root.
- enables users to perform administrative tasks without logging in as the root user, which is a best practice for maintaining system security. We will explore sudo permissions in greater detail in the `Linux Security` section

#### Execution as root

```shell-session
perplex007@htb[/htb]$ sudo cat /etc/shadow

root:<SNIP>:18395:0:99999:7:::
daemon:*:17737:0:99999:7:::
bin:*:17737:0:99999:7:::
<SNIP>
```

Here is a list that will help us to better understand and deal with user management.

|**ommand**|**Description**|
|---|---|
|`sudo`|Execute command as a different user.|
|`su`|The `su` utility requests appropriate user credentials via PAM and switches to that user ID (the default user is the superuser). A shell is then executed.|
|`useradd`|Creates a new user or update default new user information.|
|`userdel`|Deletes a user account and related files.|
|`usermod`|Modifies a user account.|
|`addgroup`|Adds a group to the system.|
|`delgroup`|Removes a group from the system.|
|`passwd`|Changes user password.|

The most effective way to gain proficiency in user management is to practice using the individual commands along with their various options in a controlled environment.

<mark style="background: #FF5582A6;"> Q: </mark>Which option needs to be set to create a home directory for a new user using "useradd" command?
<mark style="background: #ADCCFFA6;">A: </mark>-m

<mark style="background: #FF5582A6;">Q:  </mark>Which option needs to be set to lock a user account using the "usermod" command? (long version of the option)
<mark style="background: #ADCCFFA6;">A:-</mark>-lock

<mark style="background: #FF5582A6;">Q:</mark>Which option needs to be set to execute a command as a different user using the "su" command? (long version of the option)
<mark style="background: #ADCCFFA6;">A:</mark>--command

# Package Management
- packages are archives of binaries of software, configuration files, information about dependencies, keep track of updates and upgrades.
The features that most package management systems provide are:
- Package downloading
- Dependency resolution
- A standard binary package format
- Common installation and configuration locations
- Additional system-related configuration and functionality
- Quality control

The package management software retrieves the necessary changes for system installation fro the package and implement  changes to install software or tht package 
- if the package management software recognizes the additional packages are required for proper functioning of the package that has not been installed , a dependency is included and either warns the admin or reload the missing software from the repository 
- if installed software has been deleted the package management system then retakes the package's information modifies it's configuration and deletes files
There are different package management programs that we can use for this. Here is a list of examples of such programs:

|**Command**|**Description**|
|---|---|
|`dpkg`|The `dpkg` is a tool to install, build, remove, and manage Debian packages. The primary and more user-friendly front-end for `dpkg` is aptitude.|
|`apt`|Apt provides a high-level command-line interface for the package management system.|
|`aptitude`|Aptitude is an alternative to apt and is a high-level interface to the package manager.|
|`snap`|Install, configure, refresh, and remove snap packages. Snaps enable the secure distribution of the latest apps and utilities for the cloud, servers, desktops, and the internet of things.|
|`gem`|Gem is the front-end to RubyGems, the standard package manager for Ruby.|
|`pip`|Pip is a Python package installer recommended for installing Python packages that are not available in the Debian archive. It can work with version control repositories (currently only Git, Mercurial, and Bazaar repositories), logs output extensively, and prevents partial installs by downloading all requirements before starting installation.|
|`git`|Git is a fast, scalable, distributed revision control system with an unusually rich command set that provides both high-level operations and full access to internals.|
#### Advanced Package Manager (APT)
- Debain based linux use APT package manager 
- A package is an archive file containing multiple .deb files
- dpkg utility is used to install programms from associated .deb file
- when we install a standard .deb file we may run into dependency issues and needed to download and install one or multiple additional packages
- Repositories can be labeled as stable , testing or unstable
- APT uses a database called APT cache , this provide info about packages in our system installed in offline 
- we can search APT cache 

```shell-session
perplex007@htb[/htb]$ apt-cache search impacket

impacket-scripts - Links to useful impacket scripts examples
polenum - Extracts the password policy from a Windows system
python-pcapy - Python interface to the libpcap packet capture library (Python 2)
python3-impacket - Python3 module to easily build and dissect network protocols
python3-pcapy - Python interface to the libpcap packet capture library (Python 3)
```

We can then view additional information about a package.

  Package Management

```shell-session
perplex007@htb[/htb]$ apt-cache show impacket-scripts

Package: impacket-scripts
Version: 1.4
Architecture: all
Maintainer: Kali Developers <devel@kali.org>
Installed-Size: 13
Depends: python3-impacket (>= 0.9.20), python3-ldap3 (>= 2.5.0), python3-ldapdomaindump
Breaks: python-impacket (<< 0.9.18)
Replaces: python-impacket (<< 0.9.18)
Priority: optional
Section: misc
Filename: pool/main/i/impacket-scripts/impacket-scripts_1.4_all.deb
Size: 2080
<SNIP>
```

We can also list all installed packages.

  Package Management

```shell-session
perplex007@htb[/htb]$ apt list --installed

Listing... Done
accountsservice/rolling,now 0.6.55-2 amd64 [installed,automatic]
adapta-gtk-theme/rolling,now 3.95.0.11-1 all [installed]
adduser/rolling,now 3.118 all [installed]
adwaita-icon-theme/rolling,now 3.36.1-2 all [installed,automatic]
aircrack-ng/rolling,now 1:1.6-4 amd64 [installed,automatic]
<SNIP>
```

If we are missing some packages, we can search for it and install it using the following command.

  Package Management

```shell-session
perplex007@htb[/htb]$ sudo apt install impacket-scripts -y

Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following NEW packages will be installed:
  impacket-scripts
0 upgraded, 1 newly installed, 0 to remove and 0 not upgraded.
Need to get 2,080 B of archives.
After this operation, 13.3 kB of additional disk space will be used.
Get:1 https://euro2-emea-mirror.parrot.sh/mirrors/parrot rolling/main amd64 impacket-scripts all 1.4 [2,080 B]
Fetched 2,080 B in 0s (15.2 kB/s)
Selecting previously unselected package impacket-scripts.
(Reading database ... 378459 files and directories currently installed.)
Preparing to unpack .../impacket-scripts_1.4_all.deb ...
Unpacking impacket-scripts (1.4) ...
Setting up impacket-scripts (1.4) ...
Scanning application launchers
Removing duplicate launchers from Debian
Launchers are updated
```


## DPKG
- we can also download the programs and tools from the repositories 
In this example, we download 'strace' for Ubuntu 18.04 LTS.

```shell-session
perplex007@htb[/htb]$ wget http://archive.ubuntu.com/ubuntu/pool/main/s/strace/strace_4.21-1ubuntu1_amd64.deb

--2020-05-15 03:27:17--  http://archive.ubuntu.com/ubuntu/pool/main/s/strace/strace_4.21-1ubuntu1_amd64.deb
Resolving archive.ubuntu.com (archive.ubuntu.com)... 91.189.88.142, 91.189.88.152, 2001:67c:1562::18, ...
Connecting to archive.ubuntu.com (archive.ubuntu.com)|91.189.88.142|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 333388 (326K) [application/x-debian-package]
Saving to: ‘strace_4.21-1ubuntu1_amd64.deb’

strace_4.21-1ubuntu1_amd64.deb       100%[===================================================================>] 325,57K  --.-KB/s    in 0,1s    

2020-05-15 03:27:18 (2,69 MB/s) - ‘strace_4.21-1ubuntu1_amd64.deb’ saved [333388/333388]
```

 now we can use both `apt` and `dpkg` to install the package. Since we have already worked with `apt`, we will turn to `dpkg` in the next example.

```shell-session
perplex007@htb[/htb]$ sudo dpkg -i strace_4.21-1ubuntu1_amd64.deb 

(Reading database ... 154680 files and directories currently installed.)
Preparing to unpack strace_4.21-1ubuntu1_amd64.deb ...
Unpacking strace (4.21-1ubuntu1) over (4.21-1ubuntu1) ...
Setting up strace (4.21-1ubuntu1) ...
Processing triggers for man-db (2.8.3-2ubuntu0.1) ...
```

With this, we have already installed the tool and can test if it works properly.

```shell-session
perplex007@htb[/htb]$ strace -h

usage: strace [-CdffhiqrtttTvVwxxy] [-I n] [-e expr]...
              [-a column] [-o file] [-s strsize] [-P path]...
              -p pid... / [-D] [-E var=val]... [-u username] PROG [ARGS]
   or: strace -c[dfw] [-I n] [-e expr]... [-O overhead] [-S sortby]
              -p pid... / [-D] [-E var=val]... [-u username] PROG [ARGS]

Output format:
  -a column      alignment COLUMN for printing syscall results (default 40)
  -i             print instruction pointer at time of syscall
```

# Service and Process Management
- Services known as daemons 
- daemons are fundamental components of a linux system that run silently in the background without directt user interaction
- perform crucial tasks that keep the system operational and provide additional functionalities 

Services can be classified into two types 
- System services
- User installed Services
The system services are required during the system startup ,
Perform essential hardware related tasks and initialize system components are required to run the operating system and to function properly

The user installed services are added by the users and typically include server applications and other background process provide specific features or capabilities.

- Daemons are often identified by the letter `d` at the end of their program names, such as `sshd` (SSH daemon) or `systemd`.
-  Linux system utilizes both system and user-installed services to function efficiently and meet user needs.

In general, there are just a few goals that we have when we deal with a service or a process:

1. Start/Restart a service/process
2. Stop a service/process
3. See what is/was happening with a service/process
4. Enable/Disable a service/process on boot
5. Find a service/process

Most modern Linux distributions have adopted `systemd` as their initialization system (init system). It is the first process that starts during the boot process and is assigned the Process ID (`PID`).

- All process are assigned a PID and views under /proc/ directory contains info about each process
- Processes may also have a Parent Process ID PPID indicating that they were started by another processmaking them child process

## Systemctl

After installing `OpenSSH` on our VM, we can start the service with the following command.

  Service and Process Management

```shell-session
perplex007@htb[/htb]$ systemctl start ssh
```

After we have started the service, we can now check if it runs without errors.

  Service and Process Management

```shell-session
perplex007@htb[/htb]$ systemctl status ssh

● ssh.service - OpenBSD Secure Shell server
   Loaded: loaded (/lib/systemd/system/ssh.service; enabled; vendor preset: enabled)
   Active: active (running) since Thu 2020-05-14 15:08:23 CEST; 24h ago
   Main PID: 846 (sshd)
   Tasks: 1 (limit: 4681)
   CGroup: /system.slice/ssh.service
           └─846 /usr/sbin/sshd -D

Mai 14 15:08:22 inlane systemd[1]: Starting OpenBSD Secure Shell server...
Mai 14 15:08:23 inlane sshd[846]: Server listening on 0.0.0.0 port 22.
Mai 14 15:08:23 inlane sshd[846]: Server listening on :: port 22.
Mai 14 15:08:23 inlane systemd[1]: Started OpenBSD Secure Shell server.
Mai 14 15:08:30 inlane systemd[1]: Reloading OpenBSD Secure Shell server.
Mai 14 15:08:31 inlane sshd[846]: Received SIGHUP; restarting.
Mai 14 15:08:31 inlane sshd[846]: Server listening on 0.0.0.0 port 22.
Mai 14 15:08:31 inlane sshd[846]: Server listening on :: port 22.
```

To add OpenSSH to the SysV script to tell the system to run this service after startup, we can link it with the following command:

  Service and Process Management

```shell-session
perplex007@htb[/htb]$ systemctl enable ssh

Synchronizing state of ssh.service with SysV service script with /lib/systemd/systemd-sysv-install.
Executing: /lib/systemd/systemd-sysv-install enable ssh
```

Once we reboot the system, the OpenSSH server will automatically run. We can check this with a tool called `ps`.

  Service and Process Management

```shell-session
perplex007@htb[/htb]$ ps -aux | grep ssh

root       846  0.0  0.1  72300  5660 ?        Ss   Mai14   0:00 /usr/sbin/sshd -D
```

We can also use `systemctl` to list all services.

  Service and Process Management

```shell-session
perplex007@htb[/htb]$ systemctl list-units --type=service

UNIT                                                       LOAD   ACTIVE SUB     DESCRIPTION              
accounts-daemon.service                                    loaded active running Accounts Service         
acpid.service                                              loaded active running ACPI event daemon        
apache2.service                                            loaded active running The Apache HTTP Server   
apparmor.service                                           loaded active exited  AppArmor initialization  
apport.service                                             loaded active exited  LSB: automatic crash repor
avahi-daemon.service                                       loaded active running Avahi mDNS/DNS-SD Stack  
bolt.service                                               loaded active running Thunderbolt system service
```

It is quite possible that the services do not start due to an error. To see the problem, we can use the tool `journalctl` to view the logs.

## Kill a Process

A process can be in the following states:

- Running
- Waiting (waiting for an event or system resource)
- Stopped
- Zombie (stopped but still has an entry in the process table).

Processes can be controlled using `kill`, `pkill`, `pgrep`, and `killall`. To interact with a process, we must send a signal to it. We can view all signals with the following command:

  Service and Process Management

```shell-session
perplex007@htb[/htb]$ kill -l

 1) SIGHUP       2) SIGINT       3) SIGQUIT      4) SIGILL       5) SIGTRAP
 2) SIGABRT      7) SIGBUS       8) SIGFPE       9) SIGKILL     10) SIGUSR1
3) SIGSEGV     12) SIGUSR2     13) SIGPIPE     14) SIGALRM     15) SIGTERM
4) SIGSTKFLT   17) SIGCHLD     18) SIGCONT     19) SIGSTOP     20) SIGTSTP
5) SIGTTIN     22) SIGTTOU     23) SIGURG      24) SIGXCPU     25) SIGXFSZ
6) SIGVTALRM   27) SIGPROF     28) SIGWINCH    29) SIGIO       30) SIGPWR
7) SIGSYS      34) SIGRTMIN    35) SIGRTMIN+1  36) SIGRTMIN+2  37) SIGRTMIN+3
8) SIGRTMIN+4  39) SIGRTMIN+5  40) SIGRTMIN+6  41) SIGRTMIN+7  42) SIGRTMIN+8
9) SIGRTMIN+9  44) SIGRTMIN+10 45) SIGRTMIN+11 46) SIGRTMIN+12 47) SIGRTMIN+13
10) SIGRTMIN+14 49) SIGRTMIN+15 50) SIGRTMAX-14 51) SIGRTMAX-13 52) SIGRTMAX-12
11) SIGRTMAX-11 54) SIGRTMAX-10 55) SIGRTMAX-9  56) SIGRTMAX-8  57) SIGRTMAX-7
12) SIGRTMAX-6  59) SIGRTMAX-5  60) SIGRTMAX-4  61) SIGRTMAX-3  62) SIGRTMAX-2
13) SIGRTMAX-1  64) SIGRTMAX
```

The most commonly used signals are:

|**Signal**|**Description**|
|---|---|
|`1`|`SIGHUP` - This is sent to a process when the terminal that controls it is closed.|
|`2`|`SIGINT` - Sent when a user presses `[Ctrl] + C` in the controlling terminal to interrupt a process.|
|`3`|`SIGQUIT` - Sent when a user presses `[Ctrl] + D` to quit.|
|`9`|`SIGKILL` - Immediately kill a process with no clean-up operations.|
|`15`|`SIGTERM` - Program termination.|
|`19`|`SIGSTOP` - Stop the program. It cannot be handled anymore.|
|`20`|`SIGTSTP` - Sent when a user presses `[Ctrl] + Z` to request for a service to suspend. The user can handle it afterward.|

For example, if a program were to freeze, we could force to kill it with the following command:

  Service and Process Management

```shell-session
perplex007@htb[/htb]$ kill 9 <PID> 
```

---

## Background a Process

Sometimes it will be necessary to put the scan or process we just started in the background to continue using the current session to interact with the system or start other processes. As we have already seen, we can do this with the shortcut `[Ctrl + Z]`. As mentioned above, we send the `SIGTSTP` signal to the kernel, which suspends the process.

  Service and Process Management

```shell-session
perplex007@htb[/htb]$ ping -c 10 www.hackthebox.eu

perplex007@htb[/htb]$ vim tmpfile
[Ctrl + Z]
[2]+  Stopped                 vim tmpfile
```

Now all background processes can be displayed with the following command.

  Service and Process Management

```shell-session
perplex007@htb[/htb]$ jobs

[1]+  Stopped                 ping -c 10 www.hackthebox.eu
[2]+  Stopped                 vim tmpfile
```

The `[Ctrl] + Z` shortcut suspends the processes, and they will not be executed further. To keep it running in the background, we have to enter the command `bg` to put the process in the background.

  Service and Process Management

```shell-session
perplex007@htb[/htb]$ bg

perplex007@htb[/htb]$ 
--- www.hackthebox.eu ping statistics ---
10 packets transmitted, 0 received, 100% packet loss, time 113482ms

[ENTER]
[1]+  Exit 1                  ping -c 10 www.hackthebox.eu
```

Another option is to automatically set the process with an AND sign (`&`) at the end of the command.

  Service and Process Management

```shell-session
perplex007@htb[/htb]$ ping -c 10 www.hackthebox.eu &

[1] 10825
PING www.hackthebox.eu (172.67.1.1) 56(84) bytes of data.
```

Once the process finishes, we will see the results.

  Service and Process Management

```shell-session
perplex007@htb[/htb]$ 

--- www.hackthebox.eu ping statistics ---
10 packets transmitted, 0 received, 100% packet loss, time 9210ms

[ENTER]
[1]+  Exit 1                  ping -c 10 www.hackthebox.eu
```

## Foreground a Process
we can use JOb command to list all background process
- background process do not require user interaction and use same shell session without waiting until the process finishes forst 
- once scan or process finish we can get the notification by terminal that process is finished

```shell-session
perplex007@htb[/htb]$ jobs

[1]+  Running                 ping -c 10 www.hackthebox.eu &
```

If we want to get the background process into the foreground and interact with it again, we can use the `fg <ID>` command.

  Service and Process Management

```shell-session
perplex007@htb[/htb]$ fg 1
ping -c 10 www.hackthebox.eu

--- www.hackthebox.eu ping statistics ---
10 packets transmitted, 0 received, 100% packet loss, time 9206ms
```

## Execute Multiple Commands

There are three possibilities to run several commands, one after the other. These are separated by:

- Semicolon (`;`)
- Double `ampersand` characters (`&&`)
- Pipes (`|`)

The semicolon (`;`) is a command separator and executes the commands by ignoring previous commands' results and errors.

  Service and Process Management

```shell-session
perplex007@htb[/htb]$ echo '1'; echo '2'; echo '3'

1
2
3
```

 if we execute the same command but replace it in second place, the command `ls` with a file that does not exist, we get an error, and the third command will be executed nevertheless.

  Service and Process Management

```shell-session
perplex007@htb[/htb]$ echo '1'; ls MISSING_FILE; echo '3'

1
ls: cannot access 'MISSING_FILE': No such file or directory
3
```

However, it looks different if we use the double AND characters (`&&`) to run the commands one after the other. If there is an error in one of the commands, the following ones will not be executed anymore, and the whole process will be stopped.

  Service and Process Management

```shell-session
perplex007@htb[/htb]$ echo '1' && ls MISSING_FILE && echo '3'

1
ls: cannot access 'MISSING_FILE': No such file or directory
```

Pipes (`|`) depend not only on the correct and error-free operation of the previous processes but also on the previous processes' results.

<mark style="background: #FF5582A6;">Q: </mark>Use the "systemctl" command to list all units of services and submit the unit name with the description "Load AppArmor profiles managed internally by snapd" as the answer.
<mark style="background: #ADCCFFA6;">A: </mark>using systemctl to list all the services and grepping required text gives us the answer
![[Pasted image 20250519101658.png]]

# Task Scheduling

- allows users and administrators to automate tasks by running them at specific or regular intervals
- eliminating need for manual initiation
- BY sheduling tasks it ensures they are performed consistently and reliably 
- alerts can be configured to notify admin or users when certain events occur

## Systemd

Systemd is a service used in Linux systems such as Ubuntu, Redhat Linux, and Solaris to start processes and scripts at a specific time.

we can set up processes and scripts to run at a specific time or time interval and can also specify specific events and triggers that will trigger a specific task

1. Create a timer (schedules when your `mytimer.service` should run)
2. Create a service (executes the commands or script)
3. Activate the timer

#### Create a Timer

To create a timer for systemd, we need to create a directory where the timer script will be stored.

  Task Scheduling

```shell-session
perplex007@htb[/htb]$ sudo mkdir /etc/systemd/system/mytimer.timer.d
perplex007@htb[/htb]$ sudo vim /etc/systemd/system/mytimer.timer
```

Next, we need to create a script that configures the timer. The script must contain the following options: "Unit", "Timer" and "Install". The "Unit" option specifies a description for the timer. The "Timer" option specifies when to start the timer and when to activate it. Finally, the "Install" option specifies where to install the timer.

#### Mytimer.timer

Code: txt

```txt
[Unit]
Description=My Timer

[Timer]
OnBootSec=3min
OnUnitActiveSec=1hour

[Install]
WantedBy=timers.target
```

Here it depends on how we want to use our script. For example, if we want to run our script only once after the system boot, we should use `OnBootSec` setting in `Timer`. However, if we want our script to run regularly, then we should use the `OnUnitActiveSec` to have the system run the script at regular intervals. Next, we need to create our `service`.

#### Create a Service

  Task Scheduling

```shell-session
perplex007@htb[/htb]$ sudo vim /etc/systemd/system/mytimer.service
```

Here we set a description and specify the full path to the script we want to run. The "multi-user.target" is the unit system that is activated when starting a normal multi-user mode. It defines the services that should be started on a normal system startup.

Code: txt

```txt
[Unit]
Description=My Service

[Service]
ExecStart=/full/path/to/my/script.sh

[Install]
WantedBy=multi-user.target
```

After that, we have to let `systemd` read the folders again to include the changes.

#### Reload Systemd

  Task Scheduling

```shell-session
perplex007@htb[/htb]$ sudo systemctl daemon-reload
```

After that, we can use `systemctl` to `start` the service manually and `enable` the autostart.

#### Start the Timer & Service

  Task Scheduling

```shell-session
perplex007@htb[/htb]$ sudo systemctl start mytimer.timer
perplex007@htb[/htb]$ sudo systemctl enable mytimer.timer
```

This way, `mytimer.service` will be launched automatically according to the intervals (or delays) you set in `mytimer.timer`.

## Cron
- allows users and admins to exec tasks at a specific time or within time intervals
- we can use cron to automate same tasks
- need to create a script then tell cron daemon to call it at a specific time

Process for for setting up Cron daemon is little differnt than systemd
TO setup Cron daemon we need to store tasks in file called crontab

 The structure of Cron consists of the following components

| **Time Frame**         | **Description**                                                       |
| ---------------------- | --------------------------------------------------------------------- |
| Minutes (0-59)         | This specifies in which minute the task should be executed.           |
| Hours (0-23)           | This specifies in which hour the task should be executed.             |
| Days of month (1-31)   | This specifies on which day of the month the task should be executed. |
| Months (1-12)          | This specifies in which month the task should be executed.            |
| Days of the week (0-7) | This specifies on which day of the week the task should be executed.  |

 such a crontab could look like this:
Code: txt
```txt
# System Update
0 */6 * * * /path/to/update_software.sh

# Execute scripts
0 0 1 * * /path/to/scripts/run_scripts.sh

# Cleanup DB
0 0 * * 0 /path/to/scripts/clean_database.sh

# Backups
0 0 * * 7 /path/to/scripts/backup.sh
```
The "System Update" should be executed once every sixth hour. This is indicated by the entry `0 */6` in the hour column. The task is executed by the script `update_software.sh`, whose path is given in the last column.

The task `execute scripts` is to be executed every first day of the month at midnight. This is indicated by the entries `0` and `0` in the minute and hour columns and `1` in the days-of-the-month column. The task is executed by the `run_scripts.sh` script, whose path is given in the last column.

The third task, `Cleanup DB`, is to be executed every Sunday at midnight. This is specified by the entries `0` and `0` in the minute and hour columns and `0` in the days-of-the-week column. The task is executed by the `clean_database.sh` script, whose path is given in the last column.

The fourth task, `backups`, is to be executed every Sunday at midnight. This is indicated by the entries `0` and `0` in the minute and hour columns and `7` in the days-of-the-week column. The task is executed by the `backup.sh` script, whose path is given in the last column.

It is also possible to receive notifications when a task is executed successfully or unsuccessfully. In addition, we can create logs to monitor the execution of the tasks.

## Systemd vs. Cron

Systemd and Cron are both tools that can be used in Linux systems to schedule and automate processes. The key difference between these two tools is how they are configured. With Systemd, you need to create a timer and services script that tells the operating system when to run the tasks. On the other hand, with Cron, you need to create a `crontab` file that tells the cron daemon when to run the tasks.

<mark style="background: #FF5582A6;">Q:  </mark>What is the Type of the service of the "dconf.service"?
<mark style="background: #ADCCFFA6;">A:</mark>

![[Pasted image 20250519103930.png]]

using find we can find the service file which contains the type

# Network Services
ssh
NFS- network file system
 - allows user to store and manage files on remote systems as if they were stored on local system
 ```
 For example, administrators use NFS to store and manage files centrally (for Linux and Windows systems) to enable easy collaboration and management of data. For Linux, there are several NFS servers, including NFS-UTILS (`Ubuntu`), NFS-Ganesha (`Solaris`), and OpenNFS (`Redhat Linux`).
```

used to replicate to replicate the file systems between servers
- also offers features such as access controls real time file transfer , support for multiple users accessing data simultaneously
- we can use this service just like FTP in case
- in case there is not FTP client is installed on target system, NFS is running instead of FTP

We can install NFS on Linux with the following command:

#### Install NFS

  Network Services

```shell-session
perplex007@htb[/htb]$ sudo apt install nfs-kernel-server -y
```

To check if the server is running, we can use the following command:

#### Server Status

  Network Services

```shell-session
perplex007@htb[/htb]$ systemctl status nfs-kernel-server

● nfs-server.service - NFS server and services
     Loaded: loaded (/lib/system/system/nfs-server.service; enabled; vendor preset: enabled)
     Active: active (exited) since Sun 2023-02-12 21:35:17 GMT; 13s ago
    Process: 9234 ExecStartPre=/usr/sbin/exportfs -r (code=exited, status=0/SUCCESS)
    Process: 9235 ExecStart=/usr/sbin/rpc.nfsd $RPCNFSDARGS (code=exited, status=0/SUCCESS)
   Main PID: 9235 (code=exited, status=0/SUCCESS)
        CPU: 10ms
```

We can configure NFS via the configuration file `/etc/exports`. This file specifies which directories should be shared and the access rights for users and systems. It is also possible to configure settings such as the transfer speed and the use of encryption. NFS access rights determine which users and systems can access the shared directories and what actions they can perform. Here are some important access rights that can be configured in NFS:

|**Permissions**|**Description**|
|---|---|
|`rw`|Gives users and systems read and write permissions to the shared directory.|
|`ro`|Gives users and systems read-only access to the shared directory.|
|`no_root_squash`|Prevents the root user on the client from being restricted to the rights of a normal user.|
|`root_squash`|Restricts the rights of the root user on the client to the rights of a normal user.|
|`sync`|Synchronizes the transfer of data to ensure that changes are only transferred after they have been saved on the file system.|
|`async`|Transfers data asynchronously, which makes the transfer faster, but may cause inconsistencies in the file system if changes have not been fully committed.|

For example, we can create a new folder and share it temporarily in NFS. We would do this as follows:

#### Create NFS Share

  Network Services

```shell-session
cry0l1t3@htb:~$ mkdir nfs_sharing
cry0l1t3@htb:~$ echo '/home/cry0l1t3/nfs_sharing hostname(rw,sync,no_root_squash)' >> /etc/exports
cry0l1t3@htb:~$ cat /etc/exports | grep -v "#"

/home/cry0l1t3/nfs_sharing hostname(rw,sync,no_root_squash)
```

If we have created an NFS share and want to work with it on the target system, we have to mount it first. We can do this with the following command:

#### Mount NFS Share

  Network Services

```shell-session
cry0l1t3@htb:~$ mkdir ~/target_nfs
cry0l1t3@htb:~$ mount 10.129.12.17:/home/john/dev_scripts ~/target_nfs
cry0l1t3@htb:~$ tree ~/target_nfs

target_nfs/
├── css.css
├── html.html
├── javascript.js
├── php.php
└── xml.xml

0 directories, 5 files
```

So we have mounted the NFS share (`dev_scripts`) from our target (`10.129.12.17`) locally to our system in the mount point `target_nfs` over the network and can view the contents just as if we were on the target system. There are even some methods that can be used in specific cases to escalate our privileges on the remote system using NFS.

---

## Web Server

Understanding the operation of web servers is essential for penetration testers, as these servers are integral to web applications and frequently serve as primary targets during security assessments. A web server is software that delivers data, documents, applications, and various functions over the Internet. It utilizes the Hypertext Transfer Protocol (`HTTP`) to transmit data to clients such as web browsers and to receive requests from these clients. The received data is then rendered as Hypertext Markup Language (`HTML`) within the client's browser, facilitating the creation of dynamic web pages that respond interactively to user requests. Consequently, a thorough comprehension of web server functionalities is vital for developing secure and efficient web applications and for maintaining overall system security. Among the most widely used web servers on Linux platforms are Apache, Nginx, Lighttpd, and Caddy, with Apache being particularly popular due to its broad compatibility with operating systems including Ubuntu, Solaris, and Red Hat Linux.

For penetration testers, web servers offer various utilities. They can be employed to facilitate file transfers, enabling testers to log in and interact with target systems through HTTP or HTTPS ports. Additionally, web servers can be leveraged to conduct phishing attacks by hosting replicas of target pages, thereby attempting to capture user credentials. Beyond these applications, web servers provide numerous other opportunities for testing and exploiting vulnerabilities within a network.

Apache web server has a variety of features that allow us to host a secure and efficient web application. Moreover, we can also configure logging to get information about the traffic on our server, which helps us analyze attacks. We can install Apache using the following command:

#### Install Apache Web Server

  Network Services

```shell-session
perplex007@htb[/htb]$ sudo apt install apache2 -y
```

For Apache2, to specify which folders can be accessed, we can edit the file `/etc/apache2/apache2.conf` with a text editor. This file contains the global settings. We can change the settings to specify which directories can be accessed and what actions can be performed on those directories.

#### Apache Configuration

Code: txt

```txt
<Directory /var/www/html>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
</directory>
```

This section specifies that the default `/var/www/html` folder is accessible, that users can use the `Indexes` and `FollowSymLinks` options, that changes to files in this directory can be overridden with `AllowOverride All`, and that `Require all granted` grants all users access to this directory. For example, if we want to transfer files to one of our target systems using a web server, we can put the appropriate files in the `/var/www/html` folder and use `wget` or `curl` or other applications to download these files on the target system.

It is also possible to customize individual settings at the directory level by using the `.htaccess` file, which we can create in the directory in question. This file allows us to configure certain directory-level settings, such as access controls, without having to customize the Apache configuration file. We can also add modules to get features like `mod_rewrite`, `mod_security`, and `mod_ssl` that help us improve the security of our web application.

Python Web Server is a simple, fast alternative to Apache and can be used to host a single folder with a single command to transfer files to another system. To install Python Web Server, we need to install Python3 on our system and then run the following command:

#### Install Python & Web Server

  Network Services

```shell-session
perplex007@htb[/htb]$ sudo apt install python3 -y
perplex007@htb[/htb]$ python3 -m http.server
```

When we run this command, our Python Web Server will be started on the `TCP/8000` port, and we can access the folder we are currently in. We can also host another folder with the following command:

  Network Services

```shell-session
perplex007@htb[/htb]$ python3 -m http.server --directory /home/cry0l1t3/target_files
```

This will start a Python web server on the `TCP/8000` port, and we can access the `/home/cry0l1t3/target_files` folder from the browser, for example. When we access our Python web server, we can transfer files to the other system by typing the link in our browser and downloading the files. We can also host our Python web server on a port other than the default port:

  Network Services

```shell-session
perplex007@htb[/htb]$ python3 -m http.server 443
```

This will host our Python web server on port 443 instead of the default `TCP/8000` port. We can access this web server by typing the link in our browser.

---

## VPN

A Virtual Private Network (`VPN`) functions like a secure, invisible tunnel that connects us to another network, allowing seamless and protected access as if we were physically present within it. This is achieved by establishing an encrypted tunnel between the client and the server, ensuring that all data transmitted through this connection remains confidential and safeguarded from unauthorized access.

Organizations primarily utilize VPNs to grant their employees secure access to the internal network without requiring them to be on-site. This flexibility enables employees to reach internal resources and applications from any location, enhancing productivity and mobility. Additionally, VPNs serve to anonymize internet traffic and block external intrusions, further bolstering security.

Among the most widely used VPN solutions for Linux servers are OpenVPN, L2TP/IPsec, PPTP, SSTP, and SoftEther. OpenVPN stands out as a popular open-source option compatible with various operating systems, including Ubuntu, Solaris, and Red Hat Linux. Administrators leverage OpenVPN to facilitate secure remote access to corporate networks, encrypt network traffic, and maintain user anonymity online.

For penetration testers, OpenVPN offers invaluable capabilities. It allows testers to securely connect to internal networks, especially when direct access is not feasible due to geographical constraints. By utilizing OpenVPN, penetration testers can perform comprehensive security assessments of internal systems, identifying and addressing potential vulnerabilities. The versatility of OpenVPN, with features such as encryption, tunneling, traffic shaping, network routing, and adaptability to dynamic network environments, makes it an essential tool in the arsenal of both network administrators and security professionals. We can install the server and client with the following command:

#### Install OpenVPN

  Network Services

```shell-session
perplex007@htb[/htb]$ sudo apt install openvpn -y
```

OpenVPN can be customized and configured by editing the configuration file `/etc/openvpn/server.conf`. This file contains the settings for the OpenVPN server. We can change the settings to configure certain features such as encryption, tunneling, traffic shaping, etc.

If we want to connect to an OpenVPN server, we can use the `.ovpn` file we received from the server and save it on our system. We can do this with the following command on the command line:

#### Connect to VPN

  Network Services

```shell-session
perplex007@htb[/htb]$ sudo openvpn --config internal.ovpn
```

After the connection is established, we can communicate with the internal hosts on the internal network.


# Working with Web Services

Another important aspect of working with web servers is learning how to communicate with them using command-line tools like curl and wget. These tools are incredibly useful when we want to systematically analyze the content of a webpage hosted on a web server. Think of them as your personal web browsers within the terminal, allowing you to fetch and interact with web content directly from the command line.

## Wget

An alternative to curl is the tool `wget`. With this tool, we can download files from FTP or HTTP servers directly from the terminal, and it serves as a solid download manager. If we use wget in the same way, the difference to curl is that the website content is downloaded and stored locally, as shown in the following example.

  Working with Web Services

```shell-session
perplex007@htb[/htb]$ wget http://localhost

--2020-05-15 17:43:52--  http://localhost/
Resolving localhost (localhost)... 127.0.0.1
Connecting to localhost (localhost)|127.0.0.1|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 10918 (11K) [text/html]
Saving to: 'index.html'

index.html                 100%[=======================================>]  10,66K  --.-KB/s    in 0s      

2020-05-15 17:43:52 (33,0 MB/s) - ‘index.html’ saved [10918/10918]
```

---

## Python 3

Another option that is often used when it comes to data transfer is the use of Python 3. In this case, the web server's root directory is where the command is executed to start the server. For this example, we are in a directory where WordPress is installed and contains a "readme.html." Now, let us start the Python 3 web server and see if we can access it using the browser.

  Working with Web Services

```shell-session
perplex007@htb[/htb]$ python3 -m http.server

Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
```

![WordPress welcome page with logo, titled 'Semantic Personal Publishing Platform'. Includes a message from Matt Mullenweg about WordPress's significance and a section on 'Installation: Famous 5-minute install'.](https://academy.hackthebox.com/storage/modules/18/python3-browser.png)

We can see what requests were made if we now look at our Python 3 web server's events.

  Working with Web Services

```shell-session
perplex007@htb[/htb]$ python3 -m http.server

Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
127.0.0.1 - - [15/May/2020 17:56:29] "GET /readme.html HTTP/1.1" 200 -
127.0.0.1 - - [15/May/2020 17:56:29] "GET /wp-admin/css/install.css?ver=20100228 HTTP/1.1" 200 -
127.0.0.1 - - [15/May/2020 17:56:29] "GET /wp-admin/images/wordpress-logo.png HTTP/1.1" 200 -
127.0.0.1 - - [15/May/2020 17:56:29] "GET /wp-admin/images/wordpress-logo.svg?ver=20131107 HTTP/1.1" 200 -
```

In penetration testing, we often find ourselves facing challenges that require creative problem solving and out-of-the-box thinking. You'll encounter scenarios you haven't dealt with before, which means not only learning something new but also figuring out solutions on your own through research and innovative thinking.

Remember, this is a learning process, not an exam. Doing your own research and investigating different approaches is essential for expanding your skill set. In fact, these efforts will be key in building your expertise and adaptability in the field. From this point onward, the exercises you encounter will intentionally push you beyond your comfort zone. This is by design—to accelerate your learning and help you improve more quickly.

As you face these challenges, you'll develop the skills needed to tackle real-world situations, where there’s often no one-size-fits-all solution. Embrace this process of exploration and discovery, as it's the best way to grow

<mark style="background: #FF5582A6;">Q: </mark>Find a way to start a simple HTTP server inside Pwnbox or your local VM using "npm". Submit the command that starts the web server on port 8080 (use the short argument to specify the port number).

<mark style="background: #ADCCFFA6;">A: </mark>http-server -p 8080 after installing npm refer to the manpage to get the answer

<mark style="background: #FF5582A6;">Q:</mark> Find a way to start a simple HTTP server inside Pwnbox or your local VM using "php". Submit the command that starts the web server on the localhost (127.0.0.1) on port 8080.
<mark style="background: #ADCCFFA6;">A: </mark>php -S 127.0.0.1:8080, refer to the man page 

# Backup and Restore

When backing up data on an Ubuntu system, we have several options, including:

- Rsync
- Deja Dup
- Duplicity
Rsync - opensource tool allows for fast and secure backups locally or remotely 
- it only transfers portions of the files that have changed, efficient when dealing with large data
- useful for network transfers (syncing files b/w servers and creating incremental backups over the internet)
- Duplicity - builds on Rsync , adds encruption feature to protect backups 
- allows us to encrypt backup copies ensuring sensitive data remains secure even if stored on remote servers,
- provides extra layers of security while maintaining Rsync's efficient data transfer capabilities
- Deja Dup is a simple, accessible safe that anyone can operate, while still offering the same level of protection. Encrypting your backups adds an additional lock on your safe, ensuring that even if someone finds it, they can't get inside.

Deja Dup offers a graphical interface that makes the backup process straightforward. Behind the scenes, it also uses Rsync, and like Duplicity, it supports encrypted backups. Deja Dup is ideal for users who want quick, easy access to backup and restore options without needing to dive into the command line.

-  On Ubuntu systems, you can use additional encryption tools like GnuPG, eCryptfs, or LUKS to add another layer of protection to your backups.
- sing tools like Rsync, Duplicity, and Deja Dup, you can ensure that your data is securely stored and easily retrievable, giving you confidence that, in case of an unexpected data loss, your information can be restored quickly and reliably.

In order to install Rsync on Ubuntu, we can use the `apt` package manager:

#### Install Rsync
```shell-session
perplex007@htb[/htb]$ sudo apt install rsync -y
```

This will install the latest version of Rsync on the system. Once the installation is complete, we can begin using the tool to back up and restore data. To backup an entire directory using `rsync`, we can use the following command:

#### Rsync - Backup a local Directory to our Backup-Server

  Backup and Restore

```shell-session
perplex007@htb[/htb]$ rsync -av /path/to/mydirectory user@backup_server:/path/to/backup/directory
```

This command will copy the entire directory (`/path/to/mydirectory`) to a remote host (`backup_server`), to the directory `/path/to/backup/directory`. The option `archive` (`-a`) is used to preserve the original file attributes, such as permissions, timestamps, etc., and using the `verbose` (`-v`) option provides a detailed output of the progress of the `rsync` operation.

We can also add additional options to customize the backup process, such as using compression and incremental backups. We can do this like the following:

  Backup and Restore

```shell-session
perplex007@htb[/htb]$ rsync -avz --backup --backup-dir=/path/to/backup/folder --delete /path/to/mydirectory user@backup_server:/path/to/backup/directory
```

With this, we back up the `mydirectory` to the remote `backup_server`, preserving the original file attributes, timestamps, and permissions, and enabled compression (`-z`) for faster transfers. The `--backup` option creates incremental backups in the directory `/path/to/backup/folder`, and the `--delete` option removes files from the remote host that is no longer present in the source directory.

If we want to restore our directory from our backup server to our local directory, we can use the following command:

#### Rsync - Restore our Backup

  Backup and Restore

```shell-session
perplex007@htb[/htb]$ rsync -av user@remote_host:/path/to/backup/directory /path/to/mydirectory
```

---

## Encrypted Rsync

To ensure the security of our `rsync` file transfer between our local host and our backup server, we can combine the use of SSH and other security measures. By using SSH, we are able to encrypt our data as it is being transferred, making it much more difficult for any unauthorized individual to access it. Additionally, we can also use firewalls and other security protocols to ensure that our data is kept safe and secure during the transfer. By taking these steps, we can be confident that our data is protected and our file transfer is secure. Therefore we tell `rsync` to use SSH like the following:

#### Secure Transfer of our Backup

  Backup and Restore

```shell-session
perplex007@htb[/htb]$ rsync -avz -e ssh /path/to/mydirectory user@backup_server:/path/to/backup/directory
```

The data transfer between our local host and the backup server occurs over the encrypted SSH connection, which provides confidentiality and integrity protection for the data being transferred. This encryption process ensures that the data is protected from any potential malicious actors who would otherwise be able to access and modify the data without authorization. The encryption key itself is also safeguarded by a comprehensive set of security protocols, making it even more difficult for any unauthorized person to gain access to the data. In addition, the encrypted connection is designed to be highly resistant to any attempts to breach security, allowing us to have confidence in the protection of the data being transferred.

---

## Auto-Synchronization

To enable auto-synchronization using `rsync`, you can use a combination of `cron` and `rsync` to automate the synchronization process. Scheduling the cron job to run at regular intervals ensures that the contents of the two systems are kept in sync. This can be especially beneficial for organizations that need to keep their data synchronized across multiple machines. Furthermore, setting up auto-synchronization with `rsync` can be a great way to save time and effort, as it eliminates the need for manual synchronization. It also helps to ensure that the files and data stored in the systems are kept up-to-date and consistent, which helps to reduce errors and improve efficiency.

Therefore we create a new script called `RSYNC_Backup.sh`, which will trigger the `rsync` command to sync our local directory with the remote one. However, because we are using a script to perform SSH for the rsync connection, we need to configure key-based authentication. This is to bypass the need to input our password when connecting with SSH.

First, we generate a key pair for our user.

  Backup and Restore

```shell-session

perplex007@htb[/htb]$ ssh-keygen -t rsa -b 2048

```

Follow the prompts to specify the location (default is `~/.ssh/id_rsa`) and optionally provide a passphrase (leave it empty for no passphrase). Then, we need to copy our public key to the remote server.

  Backup and Restore

```shell-session

perplex007@htb[/htb]$ ssh-copy-id user@backup_server

```

Now, we can create our script to automate the rsync backup.

#### RSYNC_Backup.sh

Code: bash

```bash
#!/bin/bash

rsync -avz -e ssh /path/to/mydirectory user@backup_server:/path/to/backup/directory
```

Then, in order to ensure that the script is able to execute properly, we must provide the necessary permissions. Additionally, it's also important to make sure that the script is owned by the correct user, as this will ensure that only the correct user has access to the script and that the script is not tampered with by any other user.

  Backup and Restore

```shell-session
perplex007@htb[/htb]$ chmod +x RSYNC_Backup.sh
```

After that, we can create a crontab that tells `cron` to run the script every hour at the 0th minute.

  Backup and Restore

```shell-session

perplex007@htb[/htb]$ cronjob -e

```

We can adjust the timing to suit our needs. To do so, the crontab needs the following content:

#### Auto-Sync - Crontab

  Backup and Restore

```shell-session
0 * * * * /path/to/RSYNC_Backup.sh
```

With this setup, `cron` will be responsible for executing the script at the desired interval, ensuring that the `rsync` command is run and the contents of the local directory are synchronized with the remote host.

We encourage you to try out rsync using Pwnbox. Instead of syncing files with a remote server, you can use Pwnbox as both your source and destination, which makes testing simpler. To do this, create two directories on Pwnbox:

1. `to_backup` (where your original data is stored) and another called
2. `synced_backup` (where the synchronized data will be copied)

You will then transfer the data from the `to_backup` directory to the `synced_backup` directory using `rsync`. To automate this process, set up a `cron` job that runs every minute to ensure continuous synchronization. Remember, because we are testing this locally, we can use the loopback IP address 127.0.0.1 as the address for the "remote" host.

# File System Management

- `ext2` is an older file system with no journaling capabilities, which makes it less suited for modern systems but still useful in certain low-overhead scenarios (like USB drives).
    
- `ext3` and `ext4` are more advanced, with journaling (which helps in recovering from crashes), and ext4 is the default choice for most modern Linux systems because it offers a balance of performance, reliability, and large file support.
    
- `Btrfs` is known for advanced features like snapshotting and built-in data integrity checks, making it ideal for complex storage setups.
    
- `XFS` excels at handling large files and has high performance. It is best suited for environments with high I/O demands
    
- `NTFS`, originally developed for Windows, is useful for compatibility when dealing with dual-boot systems or external drives that need to work on both Linux and Windows systems.

Linux's file system architecture is based on the Unix model, organized in a hierarchical structure. This structure consists of several components, the most critical being `inodes`. `Inodes` are data structures that store metadata about each file and directory, including permissions, ownership, size, and timestamps. Inodes do not store the file’s actual data or name, but they contain pointers to the blocks where the file’s data is stored on the disk.

The `inode` table is a collection of these inodes, essentially acting as a database that the Linux kernel uses to track every file and directory on the system. This structure allows the operating system to efficiently access and manage files. Understanding and managing inodes is a crucial aspect of file system management in Linux, especially in scenarios where a disk is running out of inode space before running out of actual storage capacity.

Let's use an analogy, think of the Linux file system like a library. The `inodes` are like index cards in the library’s catalog system (`inode table`). Each card contains detailed information about a book (file) its title, author, location, and other details but not the actual book. The `inode` table is the entire catalog that helps the library (operating system) quickly find and manage the books (files).

In Linux, files can be stored in one of several key types:

- Regular files
- Directories
- Symbolic links

## Disks & Drives

managing physical storage devices, including hard drives, solid-state drives, and removable storage devices. The main tool for disk management on Linux is the `fdisk`, which allows us to create, delete, and manage partitions on a drive. It can also display information about the partition table, including the size and type of each partition. Partitioning a drive on Linux involves dividing the physical storage space into separate, logical sections. Each partition can then be formatted with a specific file system, such as ext4, NTFS, or FAT32, and can be mounted as a separate file system. The most common partitioning tool on Linux is also `fdisk`, `gpart`, and `GParted`.

#### Fdisk

  File System Management

```shell-session
perplex007@htb[/htb]$ sudo fdisk -l

Disk /dev/vda: 160 GiB, 171798691840 bytes, 335544320 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x5223435f

Device     Boot     Start       End   Sectors  Size Id Type
/dev/vda1  *         2048 158974027 158971980 75.8G 83 Linux
/dev/vda2       158974028 167766794   8792767  4.2G 82 Linux swap / Solaris

Disk /dev/vdb: 452 KiB, 462848 bytes, 904 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
```

## Mounting
-each logical partition or storage drive must be assigned to specific directory in the file system it is known as mounting 
- involves linking a drive or partition making contents accessbile from the direcoty drive is mounted to 
- used to manually mount the filesystems on linux
if you want certain file systems or partitions to be automatically mounted when the system boots, you can define them in the `/etc/fstab` file. This file lists the file systems and their associated mount points, along with options like read/write permissions and file system types, ensuring that specific drives or partitions are available upon startup without needing manual intervention.

#### Mounted File systems at Boot

  File System Management

```shell-session
perplex007@htb[/htb]$ cat /etc/fstab

# /etc/fstab: static file system information.
#
# Use 'blkid' to print the universally unique identifier for a device; this may
# be used with UUID= as a more robust way to name devices that works even if
# disks are added and removed. See fstab(5).
#
# <file system>                      <mount point>  <type>  <options>  <dump>  <pass>
UUID=3d6a020d-...SNIP...-9e085e9c927a /              btrfs   subvol=@,defaults,noatime,nodiratime,nodatacow,space_cache,autodefrag 0 1
UUID=3d6a020d-...SNIP...-9e085e9c927a /home          btrfs   subvol=@home,defaults,noatime,nodiratime,nodatacow,space_cache,autodefrag 0 2
UUID=21f7eb94-...SNIP...-d4f58f94e141 swap           swap    defaults,noatime 0 0

```

#### List Mounted Drives

  File System Management

```shell-session
perplex007@htb[/htb]$ mount

sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime)
proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)
udev on /dev type devtmpfs (rw,nosuid,relatime,size=4035812k,nr_inodes=1008953,mode=755,inode64)
devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,gid=5,mode=620,ptmxmode=000)
tmpfs on /run type tmpfs (rw,nosuid,nodev,noexec,relatime,size=814580k,mode=755,inode64)
/dev/vda1 on / type btrfs (rw,noatime,nodiratime,nodatasum,nodatacow,space_cache,autodefrag,subvolid=257,subvol=/@)
```

To mount a file system, we can use the `mount` command followed by the device name and the mount point. For example, to mount a USB drive with the device name `/dev/sdb1` to the directory `/mnt/usb`, we would use the following command:

#### Mount a USB drive

  File System Management

```shell-session
perplex007@htb[/htb]$ sudo mount /dev/sdb1 /mnt/usb
perplex007@htb[/htb]$ cd /mnt/usb && ls -l

total 32
drwxr-xr-x 1 root root   18 Oct 14  2021 'Account Takeover'
drwxr-xr-x 1 root root   18 Oct 14  2021 'API Key Leaks'
drwxr-xr-x 1 root root   18 Oct 14  2021 'AWS Amazon Bucket S3'
drwxr-xr-x 1 root root   34 Oct 14  2021 'Command Injection'
drwxr-xr-x 1 root root   18 Oct 14  2021 'CORS Misconfiguration'
drwxr-xr-x 1 root root   52 Oct 14  2021 'CRLF Injection'
drwxr-xr-x 1 root root   30 Oct 14  2021 'CSRF Injection'
drwxr-xr-x 1 root root   18 Oct 14  2021 'CSV Injection'
drwxr-xr-x 1 root root 1166 Oct 14  2021 'CVE Exploits'
...SNIP...
```

#### Unmount

  File System Management

```shell-session
perplex007@htb[/htb]$ sudo umount /mnt/usb
```

It is important to note that we must have sufficient permissions to unmount a file system. We also cannot unmount a file system that is in use by a running process. To ensure that there are no running processes that are using the file system, we can use the `lsof` command to list the open files on the file system.

- if we find any process using the file system we must stop before unmounting 
- we can unmount a file system automatically when system is shutdown by adding entry to the /etc/fstab file
- /etc/fstab file contains info about all file system mounted on the system
- to unmount a file system automatically shutdown we need to add noauto option to the entry in the /etc/fstab file for that system

#### Fstab File

Code: txt

```txt
/dev/sda1 / ext4 defaults 0 0
/dev/sda2 /home ext4 defaults 0 0
/dev/sdb1 /mnt/usb ext4 rw,noauto,user 0 0
192.168.1.100:/nfs /mnt/nfs nfs defaults 0 0
```

## SWAP

Swap space is an essential part of memory management in Linux and plays a critical role in ensuring smooth system performance, especially when the available physical memory (RAM) is fully utilized. When the system runs out of physical memory, the kernel moves inactive pages of memory (data not immediately in use) to the swap space, freeing up RAM for active processes. This process is known as swapping.

#### Creating Swap Space

Swap space can be set up either during the installation of the operating system or added later using the mkswap and swapon commands.

- `mkswap` is used to prepare a device or file to be used as swap space by creating a Linux swap area
    
- `swapon` activates the swap space, allowing the system to use it

The size of the `swap space` is not fixed and depends on your system's physical memory and intended usage. For example, a system with less RAM or running memory-intensive applications might need more swap space. However, modern systems with large amounts of RAM may require less or even no swap space, depending on specific use cases.

When setting up swap space, it’s important to allocate it on a dedicated partition or file, separate from the rest of the file system. This prevents fragmentation and ensures efficient use of the swap area when needed. Additionally, because sensitive data can be temporarily stored in swap space, it's recommended to encrypt the swap space to safeguard against potential data exposure.

#### Swap Space for Hibernation

Besides extending physical memory, swap space is also used for `hibernation`. Hibernation is a power-saving feature that saves the system’s state (including open applications and processes) to the swap space and powers off the system. When the system is powered back on, it restores its previous state from the swap space, resuming exactly where it left off.

<mark style="background: #FF5582A6;">Q:  </mark>How many partitions exist in our Pwnbox? (Format: 0)
<mark style="background: #ADCCFFA6;">A: </mark>3

# Containerization

Docker - open source patform for automating the deployment of applications as self contained units called containers
- uses layerd filesystem and resource isolation features to provide flexibility and portability 
- provides tools for createing deploying and managing applications
#### Install Docker-Engine

Installing Docker is relatively straightforward. We can use the following script to install it on a Ubuntu host:

Code: bash

```bash
#!/bin/bash

# Preparation
sudo apt update -y
sudo apt install ca-certificates curl gnupg lsb-release -y
sudo mkdir -m 0755 -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Install Docker Engine
sudo apt update -y
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y

# Add user htb-student to the Docker group
sudo usermod -aG docker htb-student
echo '[!] You need to log out and log back in for the group changes to take effect.'

# Test Docker installation
docker run hello-world
```

- The Docker engine and specific Docker images are needed to run a container. These can be obtained from the [Docker Hub](https://hub.docker.com/), a repository of pre-made images, or created by the user
- The Docker Hub is a cloud-based registry for software repositories or a library for Docker images.
- divided into public and private areas where public allows to upload and share images with the community 
- contains official images from docker from docker dev team , established open source projects 

- creating a dockerimage is done by creating a dockerfile contains all instructions to create a container
- we can use containers as our file hosting server ehrn transferring specific file to target
- we must create a `Dockerfile` based on Ubuntu 22.04 with `Apache` and `SSH` server running. With this, we can use `scp` to transfer files to the docker image,
- Apache allows us to host files and use tools like curl , wget and othets

#### Dockerfile

```bash
# Use the latest Ubuntu 22.04 LTS as the base image
FROM ubuntu:22.04

# Update the package repository and install the required packages
RUN apt-get update && \
    apt-get install -y \
        apache2 \
        openssh-server \
        && \
    rm -rf /var/lib/apt/lists/*

# Create a new user called "docker-user"
RUN useradd -m docker-user && \
    echo "docker-user:password" | chpasswd

# Give the docker-user user full access to the Apache and SSH services
RUN chown -R docker-user:docker-user /var/www/html && \
    chown -R docker-user:docker-user /var/run/apache2 && \
    chown -R docker-user:docker-user /var/log/apache2 && \
    chown -R docker-user:docker-user /var/lock/apache2 && \
    usermod -aG sudo docker-user && \
    echo "docker-user ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

# Expose the required ports
EXPOSE 22 80

# Start the SSH and Apache services
CMD service ssh start && /usr/sbin/apache2ctl -D FOREGROUND
```

After we have defined our Dockerfile, we need to convert it into an image. With the `build` command, we take the directory with the Dockerfile, execute the steps from the `Dockerfile`, and store the image in our local Docker Engine. If one of the steps fails due to an error, the container creation will be aborted. With the option `-t`, we give our container a tag, so it is easier to identify and work with later.

#### Docker Build

  Containerization

```shell-session
perplex007@htb[/htb]$ docker build -t FS_docker .
```

Once the Docker image has been created, it can be executed through the Docker engine, making it a very efficient and easy way to run a container. It is similar to the virtual machine concept, based on images

- container can be considerd a running process of image 
- when container is started on system , a package with respective image is loaded if unavailable locally 

#### Docker Run - Syntax

  Containerization

```shell-session
perplex007@htb[/htb]$ docker run -p <host port>:<docker port> -d <docker container name>
```

#### Docker Run

  Containerization

```shell-session
perplex007@htb[/htb]$ docker run -p 8022:22 -p 8080:80 -d FS_docker
```

In this case, we start a new container from the image `FS_docker` and map the host ports 8022 and 8080 to container ports 22 and 80, respectively. The container runs in the background, allowing us to access the SSH and HTTP services inside the container using the specified host ports.

#### Docker Management

When managing Docker containers, Docker provides a comprehensive suite of tools that enable us to easily create, deploy, and manage containers.

, we can list, start and stop containers and effectively manage them, ensuring seamless execution of applications. Some of the most commonly used Docker management commands are:

|**Command**|**Description**|
|---|---|
|`docker ps`|List all running containers|
|`docker stop`|Stop a running container.|
|`docker start`|Start a stopped container.|
|`docker restart`|Restart a running container.|
|`docker rm`|Remove a container.|
|`docker rmi`|Remove a Docker image.|
|`docker logs`|View the logs of a container.|

Once the Dockerfile is ready, you can use the `docker build` command to build the new image and assign it a unique tag to identify it. This process ensures that the original image remains unchanged, while the new image reflects the updates.

Docker containers are stateless by design, meaning that any changes made inside a running container (e.g., modifying files) are lost once the container is stopped or removed. For this reason, it's best practice to use volumes to persist data outside of the container or store application state.

## Linux Containers

- allows us to run multiple isolated linux systems called containers
- LXC uses key resource features such as control groups and namespaces
- provides comprehensive set of tools and Apis for managing configuring containers , making it as a popular choice for containerization linux systems

LXC and Docker are both containerization technologies, they serve different purposes and have unique features.

|**Category**|**Description**|
|---|---|
|`Approach`|LXC is often seen as a more traditional, system-level containerization tool, focusing on creating isolated Linux environments that behave like lightweight virtual machines. Docker, on the other hand, is application-focused, meaning it is optimized for packaging and deploying single applications or microservices.|
|`Image building`|Docker uses a standardized image format (Docker images) that includes everything needed to run an application (code, libraries, configurations). LXC, while capable of similar functionality, typically requires more manual setup for building and managing environments.|
|`Portability`|Docker excels in portability. Its container images can be easily shared across different systems via Docker Hub or other registries. LXC environments are less portable in this sense, as they are more tightly integrated with the host system’s configuration.|
|`Easy of use`|Docker is designed with simplicity in mind, offering a user-friendly CLI and extensive community support. LXC, while powerful, may require more in-depth knowledge of Linux system administration, making it less straightforward for beginners.|
|`Security`|Docker containers are generally more secure out of the box, thanks to additional isolation layers like AppArmor and SELinux, along with its read-only filesystem feature. LXC containers, while secure, may need additional configurations to match the level of isolation Docker offers by default. Interestingly enough, when misconfigured, both Docker and LXC can present a vector for local privilege escalation (these techniques are covered in depth in our [Linux Local Privlege Escalation module](https://academy.hackthebox.com/module/details/51).|
To install LXC on a Linux distribution, we can use the distribution's package manager. For example, on Ubuntu, we can use the `apt` package manager to install LXC with the following command:

#### Install LXC

  Containerization

```shell-session
perplex007@htb[/htb]$ sudo apt-get install lxc lxc-utils -y
```

Once LXC is installed, we can start creating and managing containers on the Linux host. It is worth noting that LXC requires the Linux kernel to support the necessary features for containerization. Most modern Linux kernels have built-in support for containerization, but some older kernels may require additional configuration or patching to enable support for LXC.

#### Creating an LXC Container

To create a new LXC container, we can use the `lxc-create` command followed by the container's name and the template to use. For example, to create a new Ubuntu container named `linuxcontainer`, we can use the following command:

  Containerization

```shell-session
perplex007@htb[/htb]$ sudo lxc-create -n linuxcontainer -t ubuntu
```

#### Managing LXC Containers

When working with LXC containers, several tasks are involved in managing them. These tasks include creating new containers, configuring their settings, starting and stopping them as necessary, and monitoring their performance. Fortunately, there are many command-line tools and configuration files available that can assist with these tasks. These tools enable us to quickly and easily manage our containers, ensuring they are optimized for our specific needs and requirements. By leveraging these tools effectively, we can ensure that our LXC containers run efficiently and effectively, allowing us to maximize our system's performance and capabilities.

|Command|Description|
|---|---|
|`lxc-ls`|List all existing containers|
|`lxc-stop -n <container>`|Stop a running container.|
|`lxc-start -n <container>`|Start a stopped container.|
|`lxc-restart -n <container>`|Restart a running container.|
|`lxc-config -n <container name> -s storage`|Manage container storage|
|`lxc-config -n <container name> -s network`|Manage container network settings|
|`lxc-config -n <container name> -s security`|Manage container security settings|
|`lxc-attach -n <container>`|Connect to a container.|
|`lxc-attach -n <container> -f /path/to/share`|Connect to a container and share a specific directory or file.|

configure LXC container security to prevent unauthorized access or malicious activities inside the container. This can be achieved by implementing several security measures, such as:

- Restricting access to the container
- Limiting resources
- Isolating the container from the host
- Enforcing mandatory access control
- Keeping the container up to date

LXC containers can be accessed using various methods, such as SSH or console. It is recommended to restrict access to the container by disabling unnecessary services, using secure protocols, and enforcing strong authentication mechanisms.

 we can disable SSH access to the container by removing the `openssh-server` package or by configuring SSH only to allow access from trusted IP addresses. Those containers also share the same kernel as the host system, meaning they can access all the resources available on the system. We can use resource limits or quotas to prevent containers from consuming excessive resources. For example, we can use `cgroups` to limit the amount of CPU, memory, or disk space that a container can use.

#### Securing LXC

Let us limit the resources to the container. In order to configure `cgroups` for LXC and limit the CPU and memory, a container can create a new configuration file in the `/usr/share/lxc/config/<container name>.conf` directory with the name of our container. For example, to create a configuration file for a container named `linuxcontainer`, we can use the following command:

  Containerization

```shell-session
perplex007@htb[/htb]$ sudo vim /usr/share/lxc/config/linuxcontainer.conf
```

In this configuration file, we can add the following lines to limit the CPU and memory the container can use.

Code: txt

```txt
lxc.cgroup.cpu.shares = 512
lxc.cgroup.memory.limit_in_bytes = 512M
```

When working with containers, it is important to understand the `lxc.cgroup.cpu.shares` parameter. This parameter determines the CPU time a container can use in relation to the other containers on the system. By default, this value is set to 1024, meaning the container can use up to its fair share of CPU time. However, if we set this value to 512, for example, the container can only use half of the CPU time available on the system. This can be a useful way to manage resources and ensure all containers have the necessary access to CPU time.

One of the key parameters in controlling the resource allocation of a container is the `lxc.cgroup.memory.limit_in_bytes` parameter. This parameter allows you to set the maximum amount of memory a container can use. It's important to note that this value can be specified in a variety of units, including bytes, kilobytes (K), megabytes (M), gigabytes (G), or terabytes (T), allowing for a high degree of granularity in defining container resource limits. After adding these two lines, we can save and close the file by typing:

- `[Esc]`
- `:`
- `wq`

To apply these changes, we must restart the LXC service.

  Containerization

```shell-session
perplex007@htb[/htb]$ sudo systemctl restart lxc.service
```

LXC use `namespaces` to provide an isolated environment for processes, networks, and file systems from the host system. Namespaces are a feature of the Linux kernel that allows for creating isolated environments by providing an abstraction of system resources.

Namespaces are a crucial aspect of containerization as they provide a high degree of isolation for the container's processes, network interfaces, routing tables, and firewall rules. Each container is allocated a unique process ID (`pid`) number space, isolated from the host system's process IDs. This ensures that the container's processes cannot interfere with the host system's processes, enhancing system stability and reliability. Additionally, each container has its own network interfaces (`net`), routing tables, and firewall rules, which are completely separate from the host system's network interfaces. Any network-related activity within the container is cordoned off from the host system's network, providing an extra layer of network security.

Moreover, containers come with their own root file system (`mnt`), which is entirely different from the host system's root file system. This separation between the two ensures that any changes or modifications made within the container's file system do not affect the host system's file system. However, it is important to remember that while namespaces provide a high level of isolation, they do not provide complete security. Therefore, it is always advisable to implement additional security measures to further protect the container and the host system from potential security breaches.


# Network Configuration

network access control (`NAC`). As penetration testers, we need to be well-versed in how NAC can enhance network security and the various technologies available. Key NAC models include:

| **Type**                             | **Description**                                                                                                           |
| ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------- |
| Discretionary Access Control (`DAC`) | This model allows the owner of the resource to set permissions for who can access it.                                     |
| Mandatory Access Control (`MAC`)     | Permissions are enforced by the operating system, not the owner of the resource, making it more secure but less flexible. |
| Role-Based Access Control (`RBAC`)   | Permissions are assigned based on roles within an organization, making it easier to manage user privileges.               |
#### Network Settings

  Network Configuration

```shell-session
cry0l1t3@htb:~$ ifconfig

eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 178.62.32.126  netmask 255.255.192.0  broadcast 178.62.63.255
        inet6 fe80::88d9:faff:fecf:797a  prefixlen 64  scopeid 0x20<link>
        ether 8a:d9:fa:cf:79:7a  txqueuelen 1000  (Ethernet)
        RX packets 7910  bytes 717102 (700.2 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 7072  bytes 24215666 (23.0 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

eth1: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 10.106.0.66  netmask 255.255.240.0  broadcast 10.106.15.255
        inet6 fe80::b8ab:52ff:fe32:1f33  prefixlen 64  scopeid 0x20<link>
        ether ba:ab:52:32:1f:33  txqueuelen 1000  (Ethernet)
        RX packets 14  bytes 1574 (1.5 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 15  bytes 1700 (1.6 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 15948  bytes 24561302 (23.4 MiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 15948  bytes 24561302 (23.4 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0


cry0l1t3@htb:~$ ip addr

1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 8a:d9:fa:cf:79:7a brd ff:ff:ff:ff:ff:ff
    altname enp0s3
    altname ens3
    inet 178.62.32.126/18 brd 178.62.63.255 scope global dynamic eth0
       valid_lft 85274sec preferred_lft 85274sec
    inet6 fe80::88d9:faff:fecf:797a/64 scope link 
       valid_lft forever preferred_lft forever
3: eth1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether ba:ab:52:32:1f:33 brd ff:ff:ff:ff:ff:ff
    altname enp0s4
    altname ens4
    inet 10.106.0.66/20 brd 10.106.15.255 scope global dynamic eth1
       valid_lft 85274sec preferred_lft 85274sec
    inet6 fe80::b8ab:52ff:fe32:1f33/64 scope link 
       valid_lft forever preferred_lft forever
```

When it comes to activating network interfaces, `ifconfig` and `ip` commands are two commonly used tools. These commands allow users to modify and activate settings for a specific interface, such as `eth0`. We can adjust the network settings to suit our needs by using the appropriate syntax and specifying the interface name.

#### Activate Network Interface

  Network Configuration

```shell-session
perplex007@htb[/htb]$ sudo ifconfig eth0 up     # OR
perplex007@htb[/htb]$ sudo ip link set eth0 up
```

One way to allocate an IP address to a network interface is by utilizing the `ifconfig` command. We must specify the interface's name and IP address as arguments to do this. This is a crucial step in setting up a network connection. The IP address serves as a unique identifier for the interface and enables the communication between devices on the network.

#### Assign IP Address to an Interface

  Network Configuration

```shell-session
perplex007@htb[/htb]$ sudo ifconfig eth0 192.168.1.2
```

To set the netmask for a network interface, we can run the following command with the name of the interface and the netmask:

#### Assign a Netmask to an Interface

  Network Configuration

```shell-session
perplex007@htb[/htb]$ sudo ifconfig eth0 netmask 255.255.255.0
```

When we want to set the default gateway for a network interface, we can use the `route` command with the `add` option. This allows us to specify the gateway's IP address and the network interface to which it should be applied. By setting the default gateway, we are designating the IP address of the router that will be used to send traffic to destinations outside the local network. Ensuring that the default gateway is set correctly is important, as incorrect configuration can lead to connectivity issues.

#### Assign the Route to an Interface

  Network Configuration

```shell-session
perplex007@htb[/htb]$ sudo route add default gw 192.168.1.1 eth0
```

When configuring a network interface in Linux, it is often necessary to set Domain Name System (`DNS`) servers to ensure proper network functionality. DNS servers are responsible for translating domain names (like example.com) into IP addresses, which allows devices to locate and connect to one another on the internet. Proper DNS configuration is crucial for enabling devices to access websites, online services, and other networked resources. Without correctly configured DNS servers, devices may experience issues such as the inability to resolve domain names, leading to network connectivity problems.

On Linux systems, this can be achieved by updating the `/etc/resolv.conf` file, which is a simple text file containing the system’s DNS information. By adding the appropriate DNS server addresses (Google's public DNS - `8.8.8.8` or `8.8.4.4`), the system can correctly resolve domain names to IP addresses, ensuring smooth communication over the network.

#### Editing DNS Settings

  Network Configuration

```shell-session
perplex007@htb[/htb]$ sudo vim /etc/resolv.conf
```

#### /etc/resolv.conf

Code: txt

```txt
nameserver 8.8.8.8
nameserver 8.8.4.4
```

After completing the necessary modifications to the network configuration, it is essential to ensure that these changes are saved to persist across reboots. This can be achieved by editing the `/etc/network/interfaces` file, which defines network interfaces for Linux-based operating systems. Thus, it is vital to save any changes made to this file to avoid any potential issues with network connectivity.

It’s important to note that changes made directly to the `/etc/resolv.conf` file are not persistent across reboots or network configuration changes. This is because the file may be automatically overwritten by network management services like `NetworkManager` or `systemd-resolved`. To make DNS changes permanent, you should configure DNS settings through the appropriate network management tool, such as editing network configuration files or using network management utilities that store persistent settings.

#### Editing Interfaces

  Network Configuration

```shell-session
perplex007@htb[/htb]$ sudo vim /etc/network/interfaces
```

This will open the `interfaces` file in the vim editor. We can add the network configuration settings to the file like this:

#### /etc/network/interfaces

Code: txt

```txt
auto eth0
iface eth0 inet static
  address 192.168.1.2
  netmask 255.255.255.0
  gateway 192.168.1.1
  dns-nameservers 8.8.8.8 8.8.4.4
```

By setting the `eth0` network interface to use a static IP address of `192.168.1.2`, with a netmask of `255.255.255.0` and a default gateway of `192.168.1.1`, we can ensure that your network connection remains stable and reliable. Additionally, by specifying DNS servers of `8.8.8.8` and `8.8.4.4`, we can ensure that our computer can easily access the internet and resolve domain names. Once we have made these changes to the configuration file, saving the file and exiting the editor is important. After that, we must restart the networking service to apply the changes.

#### Restart Networking Service

  Network Configuration

```shell-session
perplex007@htb[/htb]$ sudo systemctl restart networking
```

---

## Network Access Control

Network access control (NAC) is a crucial component of network security, especially in today's era of increasing cyber threats. As a penetration tester, it is vital to understand the significance of NAC in protecting the network and the various NAC technologies that can be utilized to enhance security measures. NAC is a security system that ensures that only authorized and compliant devices are granted access to the network, preventing unauthorized access, data breaches, and other security threats. By implementing NAC, organizations can be confident in their ability to protect their assets and data from cybercriminals who always seek to exploit system vulnerabilities. The following are the different NAC technologies that can be used to enhance security measures:

- Discretionary access control (DAC)
- Mandatory access control (MAC)
- Role-based access control (RBAC)

These technologies are designed to provide different levels of access control and security. Each technology has its unique characteristics and is suitable for different use cases. As a penetration tester, it is essential to understand these technologies and their specific use cases to test and evaluate the network's security effectively.

#### Discretionary Access Control

DAC is a crucial component of modern security systems as it helps organizations provide access to their resources while managing the associated risks of unauthorized access. It is a widely used access control system that enables users to manage access to their resources by granting resource owners the responsibility of controlling access permissions to their resources. This means that users and groups who own a specific resource can decide who has access to their resources and what actions they are authorized to perform. These permissions can be set for reading, writing, executing, or deleting the resource.

#### Mandatory Access Control

MAC is used in infrastructure that provides more fine-grained control over resource access than DAC systems. Those systems define rules that determine resource access based on the resource's security level and the user's security level or process requesting access. Each resource is assigned a security label that identifies its security level, and each user or process is assigned a security clearance that identifies its security level. Access to a resource is only granted if the user's or process's security level is equal to or greater than the security level of the resource. MAC is often used in operating systems and applications that require a high level of security, such as military or government systems, financial systems, and healthcare systems. MAC systems are designed to prevent unauthorized access to resources and minimize the impact of security breaches.

#### Role-based Access Control

RBAC assigns permissions to users based on their roles within an organization. Users are assigned roles based on their job responsibilities or other criteria, and each role is granted a set of permissions that determine the actions they can perform. RBAC simplifies the management of access permissions, reduces the risk of errors, and ensures that users can access only the resources necessary to perform their job functions. It can restrict access to sensitive resources and data, limit the impact of security breaches, and ensure compliance with regulatory requirements. Compared to Discretionary Access Control (DAC) systems, RBAC provides a more flexible and scalable approach to managing resource access. In an RBAC system, each user is assigned one or more roles, and each role is assigned a set of permissions that define the user's actions. Resource access is granted based on the user's assigned role rather than their identity or ownership of the resource. RBAC systems are typically used in environments with many users and resources, such as large organizations, government agencies, and financial institutions.

---

## Monitoring

Network monitoring involves capturing, analyzing, and interpreting network traffic to identify security threats, performance issues, and suspicious behavior. The primary goal of analyzing and monitoring network traffic is identifying security threats and vulnerabilities. For example, as penetration testers, we can capture credentials when someone uses an unencrypted connection and tries to log in to an FTP server. As a result, we will obtain this user’s credentials that might help us to infiltrate the network even further or escalate our privileges to a higher level. In short, by analyzing network traffic, we can gain insights into network behavior and identify patterns that may indicate security threats. Such analysis includes detecting suspicious network activity, identifying malicious traffic, and identifying potential security risks. However, we cover this vast topic in the [Intro to Network Traffic Analysis](https://academy.hackthebox.com/module/details/81) module, where we use several tools for network monitoring on Linux systems like Ubuntu and Windows systems, like Wireshark, tshark, and Tcpdump.

---

## Troubleshooting

Network troubleshooting is an essential process that involves diagnosing and resolving network issues that can adversely affect the performance and reliability of the network. This process is critical for ensuring the network operates optimally and avoiding disruptions that could impact business operations during our penetration tests. It also involves identifying, analyzing, and implementing solutions to resolve problems. Such problems include connectivity problems, slow network speeds, and network errors. Various tools can help us identify and resolve issues regarding network troubleshooting on Linux systems. Some of the most commonly used tools include:

1. Ping
2. Traceroute
3. Netstat
4. Tcpdump
5. Wireshark
6. Nmap

By using these tools and others like them, we can better understand how the network functions and quickly diagnose any issues that may arise. For example, `ping` is a command-line tool used to test connectivity between two devices. It sends packets to a remote host and measures the time to return them. To use `ping`, we can enter the following command:

#### Ping

  Network Configuration

```shell-session
perplex007@htb[/htb]$ ping <remote_host>
```

For example, pinging the Google DNS server will send ICMP packets to the Google DNS server and display the response times.

  Network Configuration

```shell-session
perplex007@htb[/htb]$ ping 8.8.8.8

PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=119 time=1.61 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=119 time=1.06 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=119 time=0.636 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=119 time=0.685 ms
^C
--- 8.8.8.8 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3017ms
rtt min/avg/max/mdev = 0.636/0.996/1.607/0.388 ms
```

Another tool is the `traceroute`, which traces the route packets take to reach a remote host. It sends packets with increasing Time-to-Live (TTL) values to a remote host and displays the IP addresses of the devices that the packets pass through. For example, to trace the route to the Google DNS server, we would enter the following command:

#### Traceroute

  Network Configuration

```shell-session
perplex007@htb[/htb]$ traceroute www.inlanefreight.com

traceroute to www.inlanefreight.com (134.209.24.248), 30 hops max, 60 byte packets
 1  * * *
 2  10.80.71.5 (10.80.71.5)  2.716 ms  2.700 ms  2.730 ms
 3  * * *
 4  10.80.68.175 (10.80.68.175)  7.147 ms  7.132 ms 10.80.68.161 (10.80.68.161)  7.393 ms
```

This will display the IP addresses of the devices that the packets pass through to reach the Google DNS server. The output of a traceroute command shows how it is used to trace the path of packets to the website [www.inlanefreight.com](http://www.inlanefreight.com/), which has an IP address of 134.209.24.248. Each line of the output contains valuable information.

When setting up a network connection, it's important to specify the destination host and IP address. In this example, the destination host is 134.209.24.248, and the maximum number of hops allowed is 30. This ensures that the connection is established efficiently and reliably. By providing this information, the system can route traffic to the correct destination and limit the number of intermediate stops the data needs to make.

The second line shows the first hop in the traceroute, which is the local network gateway with the IP address 10.80.71.5, followed by the next three columns show the time it took for each of the three packets sent to reach the gateway in milliseconds (2.716 ms, 2.700 ms, and 2.730 ms).

Next, we see the second hop in the traceroute. However, there was no response from the device at that hop, indicated by the three asterisks instead of the IP address. This could mean the device is down, blocking ICMP traffic, or a network issue caused the packets to drop.

In the fourth line, we can see the third hop in the traceroute, consisting of two devices with IP addresses 10.80.68.175 and 10.80.68.161, and again the next three columns show the time it took for each of the three packets to reach the first device (7.147 ms, 7.132 ms, and 7.393 ms).

#### Netstat

`Netstat` is used to display active network connections and their associated ports. It can be used to identify network traffic and troubleshoot connectivity issues. To use `netstat`, we can enter the following command:

  Network Configuration

```shell-session
perplex007@htb[/htb]$ netstat -a

Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address           Foreign Address         State      
tcp        0      0 localhost:5901          0.0.0.0:*               LISTEN     
tcp        0      0 0.0.0.0:sunrpc          0.0.0.0:*               LISTEN     
tcp        0      0 0.0.0.0:http            0.0.0.0:*               LISTEN     
tcp        0      0 0.0.0.0:ssh             0.0.0.0:*               LISTEN
...SNIP...
```

We can expect to receive detailed information about each connection when using this tool. This includes the protocol used, the number of bytes received and sent, IP addresses, port numbers of both local and remote devices, and the current connection state. The output provides valuable insights into the network activity on the system, highlighting four specific connections currently active and listening on specific ports. These connections include the VNC remote desktop software, the Sun Remote Procedure Call service, the HTTP protocol for web traffic, and the SSH protocol for secure remote shell access. By knowing which ports are used by which services, users can quickly identify any network issues and troubleshoot accordingly. The most common network issues we will encounter during our penetration tests are as follows:

- Network connectivity issues
- DNS resolution issues (it's always about DNS)
- Loss of data packets
- Network performance issues

The most common causes for them are:

- Incorrectly configured firewalls or routers,
- damaged network cables or connections,
- incorrect network settings,
- hardware failures,
- incorrect DNS server settings or DNS server failures
- incorrectly configured DNS entries,
- network congestion,
- outdated network hardware or incorrectly configured network settings,
- unpatched software or firmware and missing security controls.

Understanding these common network issues and their causes is important for effectively identifying and exploiting vulnerabilities in network systems during our testing.

---

## Hardening

Several mechanisms are highly effective in securing Linux systems in keeping our and other companies' data safe. Three such mechanisms are SELinux, AppArmor, and TCP wrappers. These tools are designed to safeguard Linux systems against various security threats, from unauthorized access to malicious attacks. This is critical not only during penetration tests, where systems are intentionally stressed to uncover vulnerabilities, but also in real-world scenarios where an actual compromise could have serious consequences (few situations are as severe as a real-life breach.) By implementing these security measures and ensuring that we set up corresponding protection against potential attackers, we can significantly reduce the risk of data leaks and ensure our systems remain secure. While these tools share some similarities, they also have important differences.

#### Security-Enhanced Linux

Security-Enhanced Linux (`SELinux`) is a mandatory access control (`MAC`) system integrated into the Linux kernel. It provides fine-grained control over access to system resources and applications by enforcing security policies. These policies define the permissions for each process and file on the system, significantly limiting the damage that a compromised process or service can do. SELinux operates at a low level, and though it offers strong security, it can be complex to configure and manage due to its granular controls.

#### AppArmor

Like SELinux, `AppArmor` is a MAC system that controls access to system resources and applications, but it operates in a simpler, more user-friendly manner. AppArmor is implemented as a Linux Security Module (`LSM`) and uses application profiles to define what resources an application can access. While it may not provide the same level of fine-grained control as SELinux, AppArmor is often easier to configure and is generally considered more straightforward for day-to-day use.

#### TCP Wrappers

`TCP wrappers` are a host-based network access control tool that restricts access to network services based on the IP address of incoming connections. When a network request is made, TCP wrappers intercept it, checking the request against a list of allowed or denied IP addresses. This is a simple yet effective way to control access to services, especially for blocking unauthorized systems from accessing networked resources. While it does not offer the fine-grained control of SELinux or AppArmor, TCP wrappers are an excellent tool for basic network-level protection.

Regarding similarities, the three security mechanisms share the common goal of ensuring the safety and security of Linux systems. In addition to providing extra protection, they can restrict access to resources and services, thus reducing the risk of unauthorized access and data breaches. It's also worth noting that these mechanisms are readily available as part of most Linux distributions, making them accessible to us to enhance their systems' security. Furthermore, these mechanisms can be easily customized and configured using standard tools and utilities, making them a convenient choice for Linux users.

Although both `SELinux` and `AppArmor` are MAC systems that provide fine-grained control, they work in different ways. SELinux is deeply integrated into the kernel and offers more detailed security controls, but it can be more complex to configure and maintain. In contrast, AppArmor operates as a kernel module and uses profile-based security, making it easier to manage, though it may not offer the same level of granularity as SELinux.

On the other hand, `TCP wrappers` focus on controlling access to network services based on client IP addresses, which makes it simpler but limited to network-level access control. It doesn't offer the broader system resource protections that SELinux and AppArmor provide, but it’s useful for restricting access to services from unauthorized systems.

---

## Setting Up

As we navigate the world of Linux, we inevitably encounter a wide range of technologies, applications, and services that we need to become familiar with. This is a crucial skill, particularly if we work in cybersecurity and strive to improve our expertise continuously. For this reason, we highly recommend dedicating time to learning about configuring important security measures such as `SELinux`, `AppArmor`, and `TCP wrappers` on your own. By taking on this (optional but highly efficient) challenge, you'll deepen your understanding of these technologies, build up your problem-solving skills, and gain valuable experience that will serve you well in the future. We highly recommend to use a personal VM and make snapshots before making changes.

When it comes to implementing cybersecurity measures, there is no one-size-fits-all approach. It is important to consider the specific information you want to protect and the tools you will use to do so. However, you can practice and implement several optional tasks with others in the Discord channel to increase your knowledge and skills in this area. By taking advantage of the helpfulness of others and sharing your own expertise, you can deepen your understanding of cybersecurity and help others do the same. Remember, explaining concepts to others is essential to teaching and learning.


## Iptables

The iptables utility provides a flexible set of rules for filtering network traffic based on various criteria such as source and destination IP addresses, port numbers, protocols, and more. There also exist other solutions like nftables, ufw, and firewalld. `Nftables` provides a more modern syntax and improved performance over iptables. However, the syntax of nftables rules is not compatible with iptables, so migration to nftables requires some effort. `UFW` stands for “Uncomplicated Firewall” and provides a simple and user-friendly interface for configuring firewall rules. UFW is built on top of the iptables framework like nftables and provides an easier way to manage firewall rules. Finally, FirewallD provides a dynamic and flexible firewall solution that can be used to manage complex firewall configurations, and it supports a rich set of rules for filtering network traffic and can be used to create custom firewall zones and services. It consists of several components that work together to provide a flexible and powerful firewall solution. The main components of iptables are:

|**Component**|**Description**|
|---|---|
|`Tables`|Tables are used to organize and categorize firewall rules.|
|`Chains`|Chains are used to group a set of firewall rules applied to a specific type of network traffic.|
|`Rules`|Rules define the criteria for filtering network traffic and the actions to take for packets that match the criteria.|
|`Matches`|Matches are used to match specific criteria for filtering network traffic, such as source or destination IP addresses, ports, protocols, and more.|
|`Targets`|Targets specify the action for packets that match a specific rule. For example, targets can be used to accept, drop, or reject packets or modify the packets in another way.|

#### Tables

When working with firewalls on Linux systems, it is important to understand how tables work in iptables. Tables in iptables are used to categorize and organize firewall rules based on the type of traffic that they are designed to handle. These tables are used to organize and categorize firewall rules. Each table is responsible for performing a specific set of tasks.

|**Table Name**|**Description**|**Built-in Chains**|
|---|---|---|
|`filter`|Used to filter network traffic based on IP addresses, ports, and protocols.|INPUT, OUTPUT, FORWARD|
|`nat`|Used to modify the source or destination IP addresses of network packets.|PREROUTING, POSTROUTING|
|`mangle`|Used to modify the header fields of network packets.|PREROUTING, OUTPUT, INPUT, FORWARD, POSTROUTING|

In addition to the built-in tables, iptables provides a fourth table called the raw table, which is used to configure special packet processing options. The raw table contains two built-in chains: PREROUTING and OUTPUT.

#### Chains

In iptables, chains organize rules that define how network traffic should be filtered or modified. There are two types of chains in iptables:

- Built-in chains
- User-defined chains

The built-in chains are pre-defined and automatically created when a table is created. Each table has a different set of built-in chains. For example, the filter table has three built-in chains:

- INPUT
- OUTPUT
- FORWARD

These chains are used to filter incoming and outgoing network traffic, as well as traffic that is being forwarded between different network interfaces. The nat table has two built-in chains:

- PREROUTING
- POSTROUTING

The PREROUTING chain is used to modify the destination IP address of incoming packets before the routing table processes them. The POSTROUTING chain is used to modify the source IP address of outgoing packets after the routing table has processed them. The mangle table has five built-in chains:

- PREROUTING
- OUTPUT
- INPUT
- FORWARD
- POSTROUTING

These chains are used to modify the header fields of incoming and outgoing packets and packets being processed by the corresponding chains.

`User-defined chains` can simplify rule management by grouping firewall rules based on specific criteria, such as source IP address, destination port, or protocol. They can be added to any of the three main tables. For example, if an organization has multiple web servers that all require similar firewall rules, the rules for each server could be grouped in a user-defined chain. Another example is when a user-defined chain could filter traffic destined for a specific port, such as port 80 (HTTP). The user could then add rules to this chain that specifically filter traffic destined for port 80.

#### Rules and Targets

Iptables rules are used to define the criteria for filtering network traffic and the actions to take for packets that match the criteria. Rules are added to chains using the `-A` option followed by the chain name, and they can be modified or deleted using various other options.

Each rule consists of a set of criteria or matches and a target specifying the action for packets that match the criteria. The criteria or matches match specific fields in the IP header, such as the source or destination IP address, protocol, source, destination port number, and more. The target specifies the action for packets that match the criteria. They specify the action to take for packets that match a specific rule. For example, targets can accept, drop, reject, or modify the packets. Some of the common targets used in iptables rules include the following:

|**Target Name**|**Description**|
|---|---|
|`ACCEPT`|Allows the packet to pass through the firewall and continue to its destination|
|`DROP`|Drops the packet, effectively blocking it from passing through the firewall|
|`REJECT`|Drops the packet and sends an error message back to the source address, notifying them that the packet was blocked|
|`LOG`|Logs the packet information to the system log|
|`SNAT`|Modifies the source IP address of the packet, typically used for Network Address Translation (NAT) to translate private IP addresses to public IP addresses|
|`DNAT`|Modifies the destination IP address of the packet, typically used for NAT to forward traffic from one IP address to another|
|`MASQUERADE`|Similar to SNAT but used when the source IP address is not fixed, such as in a dynamic IP address scenario|
|`REDIRECT`|Redirects packets to another port or IP address|
|`MARK`|Adds or modifies the Netfilter mark value of the packet, which can be used for advanced routing or other purposes|

Let us illustrate a rule and consider that we want to add a new entry to the INPUT chain that allows incoming TCP traffic on port 22 (SSH) to be accepted. The command for that would look like the following:

  Firewall Setup

```shell-session
perplex007@htb[/htb]$ sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```

#### Matches

`Matches` are used to specify the criteria that determine whether a firewall rule should be applied to a particular packet or connection. Matches are used to match specific characteristics of network traffic, such as the source or destination IP address, protocol, port number, and more.

|**Match Name**|**Description**|
|---|---|
|`-p` or `--protocol`|Specifies the protocol to match (e.g. tcp, udp, icmp)|
|`--dport`|Specifies the destination port to match|
|`--sport`|Specifies the source port to match|
|`-s` or `--source`|Specifies the source IP address to match|
|`-d` or `--destination`|Specifies the destination IP address to match|
|`-m state`|Matches the state of a connection (e.g. NEW, ESTABLISHED, RELATED)|
|`-m multiport`|Matches multiple ports or port ranges|
|`-m tcp`|Matches TCP packets and includes additional TCP-specific options|
|`-m udp`|Matches UDP packets and includes additional UDP-specific options|
|`-m string`|Matches packets that contain a specific string|
|`-m limit`|Matches packets at a specified rate limit|
|`-m conntrack`|Matches packets based on their connection tracking information|
|`-m mark`|Matches packets based on their Netfilter mark value|
|`-m mac`|Matches packets based on their MAC address|
|`-m iprange`|Matches packets based on a range of IP addresses|

In general, matches are specified using the '-m' option in iptables. For example, the following command adds a rule to the 'INPUT' chain in the 'filter' table that matches incoming TCP traffic on port 80:

  Firewall Setup

```shell-session
perplex007@htb[/htb]$ sudo iptables -A INPUT -p tcp -m tcp --dport 80 -j ACCEPT
```

This example rule matches incoming TCP traffic (`-p tcp`) on port 80 (`--dport 80`) and jumps to the accept target (`-j ACCEPT`) if the match is successful.

# Shortcuts

---

There are many shortcuts that we can use to make working with Linux easier and faster. After we have familiarized ourselves with the most important of them and have made them a habit, we will save ourselves much typing. Some of them will even help us to avoid using our mouse in the terminal.

---

#### Auto-Complete

`[TAB]` - Initiates auto-complete. This will suggest to us different options based on the `STDIN` we provide. These can be specific suggestions like directories in our current working environment, commands starting with the same number of characters we already typed, or options.

---

#### Cursor Movement

`[CTRL] + A` - Move the cursor to the `beginning` of the current line.

`[CTRL] + E` - Move the cursor to the `end` of the current line.

`[CTRL] + [←]` / `[→]` - Jump at the beginning of the current/previous word.

`[ALT] + B` / `F` - Jump backward/forward one word.

---

#### Erase The Current Line

`[CTRL] + U` - Erase everything from the current position of the cursor to the `beginning` of the line.

`[Ctrl] + K` - Erase everything from the current position of the cursor to the `end` of the line.

`[Ctrl] + W` - Erase the word preceding the cursor position.

---

#### Paste Erased Contents

`[Ctrl] + Y` - Pastes the erased text or word.

---

#### Ends Task

`[CTRL] + C` - Ends the current task/process by sending the `SIGINT` signal. For example, this can be a scan that is running by a tool. If we are watching the scan, we can stop it / kill this process by using this shortcut. While not configured and developed by the tool we are using. The process will be killed without asking us for confirmation.

---

#### End-of-File (EOF)

`[CTRL] + D` - Close `STDIN` pipe that is also known as End-of-File (EOF) or End-of-Transmission.

---

#### Clear Terminal

`[CTRL] + L` - Clears the terminal. An alternative to this shortcut is the `clear` command you can type to clear our terminal.

---

#### Background a Process

`[CTRL] + Z` - Suspend the current process by sending the `SIGTSTP` signal.

---

#### Search Through Command History

`[CTRL] + R` - Search through command history for commands we typed previously that match our search patterns.

`[↑]` / `[↓]` - Go to the previous/next command in the command history.

---

#### Switch Between Applications

`[ALT] + [TAB]` - Switch between opened applications.

---

#### Zoom

`[CTRL] + [+]` - Zoom in.

`[CTRL] + [-]` - Zoom out.

 [Previous](https://academy.hackthebox.com/module/18/section/2101)