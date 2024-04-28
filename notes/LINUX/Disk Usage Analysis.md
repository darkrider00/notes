Disk usage analysis is crucial for monitoring and managing your system’s storage. Two commonly used command-line tools for disk usage analysis in Unix-like operating systems are df and du. Here’s how you can use them and interpret their output:

1. df (Disk Free):

– df is used to display information about the amount of disk space available and used on mounted filesystems.

– Basic usage: df

– By default, df shows disk space statistics in kilobytes and lists all mounted filesystems.

– Common options:

– -h or –human-readable: Display sizes in a more human-readable format (e.g., MB, GB).

– -T or –print-type: Show the filesystem type along with the other information.

– Example output:

Filesystem     1K-blocks    Used Available Use% Mounted on

/dev/sda1       10238448 4487960   5239164  47% /

tmpfs             102400       4    102396   1% /dev/shm

/dev/sdb1       20480000  456792  19042312   3% /data

– Interpretation:

– Filesystem: The name of the filesystem.

– 1K-blocks: Total size in 1-kilobyte blocks.

– Used: Used space in 1-kilobyte blocks.

– Available: Available space in 1-kilobyte blocks.

– Use%: The percentage of used space.

– Mounted on: The mount point of the filesystem.

2. du (Disk Usage):

– du is used to estimate the disk space usage of files and directories.

– Basic usage: du [options] [directory or file]

– By default, du displays sizes in kilobytes and recursively scans directories.

– Common options:

– -h or –human-readable: Display sizes in a more human-readable format (e.g., MB, GB).

– -s or –summarize: Display only the total size for the specified directory.

– Example output:

4.0K    /home/user/documents

12K     /home/user/pictures

28K     /home/user

– Interpretation:

– The output shows the disk space usage for each specified directory or file.

– 4.0K, 12K, and 28K represent the sizes in kilobytes.

– The last line, 28K, represents the total size of all specified directories and files.

Here are some tips for disk usage analysis:

– Use df to get an overview of your filesystems and identify how much space is available and used.

– Use du to investigate which directories or files are consuming the most space within a specific location.

– Be cautious when using du on large filesystems, as it can take some time to complete its scan.

– You can combine du with other commands, such as sort, to identify the largest directories or files in a given location.

– Remember that df reports on filesystems, while du reports on individual files and directories within those filesystems.

– Regularly monitor disk usage to prevent running out of space, which can lead to system instability or data loss.