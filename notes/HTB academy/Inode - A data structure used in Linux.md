Create a index

- Everything in a file is linux 
- contains several files , which includes datafiles, directories , systemfiles, library files etc
- file are stored in hierarchical format (directories and sub directories)
- inode or index node is a linux DS that describe objects of file sytems , their names owner account and permissions (metadata)
- directory structure and inode provide a framework to store file and directory metadata
-  It’s a unique number for files and directories under a disk block/partition.

![[Pasted image 20250517144847.png]]

## **What are the important** **attrib****utes** **included in inode?**

The below mentioned keys are the different attributes in Unix file system and are included in inode.

- File type.
- File permission.
- Ownership and group.
- Size.
- Access, change and modification time.
- Deletion time.
- Number of links.

## **How do I check the inode details of a file or directory?**

Do you have a shell access to your server? If so, yes, you can simply check the inode number by using the following commands:

1. **ls -i**
2. **stat**

**See the sample outputs**

### **1. By using ls command.**

The switch “i” uses with ls command to find out the inode number of a file or directory. See the sample output pasted below:

**arunlal@localhost:~$ touch inode.check

arunlal@localhost:~$ ls -i inode.check
1179765 inode.check**

Here the inode for the file “inode.check” is **1179765**.

### **2. By using stat command.**

The “stat” command will display the inode number along with a lot of other attributes. See the output:

**arunlal@localhost:~$ stat inode.check
  File: 'inode.check'
  Size: 0         	Blocks: 0          IO Block: 4096   regular empty file
Device: 806h/2054d	Inode: 1179765     Links: 1
Access: (0664/-rw-rw-r--)  Uid: ( 1000/ arunlal)   Gid: ( 1000/ arunlal)
Access: 2016-11-15 20:00:07.548968280 +0530
Modify: 2016-11-15 20:00:07.548968280 +0530
Change: 2016-11-15 20:00:07.548968280 +0530
 Birth: -**

In this output you can see a lot of attributes of the file “inode.check.”

> ## [_**Top command usages and examples in Unix/Linux**_](https://www.crybit.com/top-uses-of-top-command/)
> 
> _Top command has an important role in Unix/Linux system/server administration side. The command “top” displays a dynamic view of process that are currently running under the system. Here I’m explaining some of the useful usage of top command for my Admin friends._

You can also use these commands to check the details of directories. See one example pasted below:

**arunlal@localhost:~$ mkdir inode.check.dir

arunlal@localhost:~$ stat inode.check.dir
  File: 'inode.check.dir'
  Size: 4096      	Blocks: 8          IO Block: 4096   directory
Device: 806h/2054d	Inode: 1314947     Links: 2
Access: (0775/drwxrwxr-x)  Uid: ( 1000/ arunlal)   Gid: ( 1000/ arunlal)
Access: 2016-11-15 20:09:21.734325138 +0530
Modify: 2016-11-15 20:09:21.734325138 +0530
Change: 2016-11-15 20:09:21.734325138 +0530
 Birth: -**

Total inode usage on the Linux machine can be calculated from the ”df” command along with the usage of switch “i.” Please see the details pasted below:

**$ df -i
Filesystem      Inodes  IUsed   IFree IUse% Mounted on
udev            489347    557  488790    1% /dev
tmpfs           494198    802  493396    1% /run
/dev/sda6      3932160 238966 3693194    7% /
tmpfs           494198    150  494048    1% /dev/shm**

That’s it! Try it and add comments if you have any other ideas on it.

## Inode and Hard/Soft Links

When you create hard or soft links, a new file is created. However, the inode works differently for both hard and soft links. 

When you create a soft link for a file or directory, the link file has a different inode number than the original file. Whereas, in the case of a hard link, the original file and the link file both have the same inode number. This is because the hard link provides a new name to the same data and thus can be accessed using the same inode number.


## What Are Hard Links and Soft Links?

In Linux, you can create two types of links to files:

|Type|Also Known As|Analogy|
|---|---|---|
|**Hard Link**|Actual Clone|Multiple names for **same file**|
|**Soft Link**|Symbolic Link / Symlink|Shortcut or alias to the file|
## 🔗 Hard Link

### ✅ Behavior:

- **Points directly to the same inode** as the original file.
    
- **Shares** the same content (not a copy).
    
- Even if the original file is deleted, the data remains accessible via the hard link.

### 📌 Inode Info:

- **Same inode number** for both original and hard link.
### 📁 Example:

`touch file.txt ln file.txt hardlink.txt ls -i`

`123456 file.txt 
`123456 hardlink.txt

Same inode → they are really the same file with **different names**.

## Soft Link (Symbolic Link)

### ✅ Behavior:

- Like a **shortcut**.
    
- Points to the **filename**, not directly to the inode.
    
- If the original file is deleted, the soft link breaks (becomes a "dangling link").
    
### 📌 Inode Info:

- **Different inode number** than the original file.
    
### 📁 Example:

`touch file.txt ln -s file.txt softlink.txt ls -li`

`123456 file.txt 
`789101 softlink.txt -> file.txt

Different inodes → softlink is a separate file that **points to the original by name**.

## Summary Table

|Feature|Hard Link|Soft Link (Symlink)|
|---|---|---|
|Inode|Same as original|Different from original|
|Points to|The actual file (inode)|The file name/path|
|File Type|Real file|Shortcut/alias|
|Works across filesystems?|❌ No|✅ Yes|
|Breaks if original deleted?|❌ No|✅ Yes (becomes broken link)|
|Usage|For backups, mirror names|For shortcuts (e.g. `/usr/bin/python`)|
## Inode of a File

Every file is assigned an inode number when you create it. This inode number refers to the metadata information stored in the inode table. Use the following command to display inode information of a file:

```
stat users.txt
```

![[Pasted image 20250517145344.png]]
## Inode of a Directory

The Linux file system treats every object as a file and thus similar to a file, the inode number is also assigned to a directory when it is first created. Use the stat command to display inode information of a directory:

```
stat Pictures/
```

![[Pasted image 20250517145431.png]]

## Inode System Level

When a Linux or UNIX-like file system is created, an inode table is also created along with it. This inode is an index of every file in the particular file system.

Every computer contains many inodes and usually does not occupy all inodes. However, there are two numbers that you must watch for. First is the maximum number of inodes, which is generally almost 1 percent of the total disk space allocated to the file system. Second is the number of occupied inodes on your system.

At the system level, Linux labels even the smallest units of data and indexes them using inodes. When an application or system utilities require to open or read these indexed files, they go to the inode table and find out the location of the particular file on the disk. So this is one of the most important data structures that are extremely important for the inner working of the Linux operating system.