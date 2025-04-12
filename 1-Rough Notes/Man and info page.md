##### **How to use Linux Documentation Man / Help**

###### **--help** 
A note on notation: When square brackets appear in the description of a command's syntax, they indicate optional items. A vertical bar ( | )character indicates mutually exclusive items. In the case of the cd command above:
```bash 
                 cd [-L| [-P[-e]]] [dir]
```
This notation says that the command cd may be followed optionally by either a -L or a -P and further, if the -P option is specified the -e option may also be included followed by the optional argument dir. While the output of help for the cd commands is concise and accurate, it is by no means tutorial and as we can see, it also seems to mention

###### **man** 

Without specifying a section number, we will always get the first instance of a match 


```bash
man section search_term
man 5 passwd
```
![[6-Attachments/Screenshot from 2025-02-22 13-33-38 1.png]]

 **apropos**—Display Appropriate Commands
It is also possible to search the list of man pages for possible matches based on a search term. It’s crude but sometimes helpful.

```bash 
[me@linuxbox ~]$ apropos partition
addpart (8) - simple wrapper around the "add partition" ioctl
all-swaps (7) - event signalling that all swap partitions have been ac...
cfdisk (8) - display or manipulate disk partition table
cgdisk (8) - Curses-based GUID partition table (GPT) manipulator
delpart (8) - simple wrapper around the "del partition" ioctl
........```

==The first field in each line of output is the name of the man page, andthe second field shows the section.==


> [!NOTE] -k option 
> Note that the man command with the -k
option performs the same function as apropos.

```
