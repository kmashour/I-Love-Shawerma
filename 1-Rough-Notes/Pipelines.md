##### **Pipelines**
Using the pipe operator |, the standard output of one command can be piped into the standard input of another. think of it ya kimo as the standard input it's o/p is passed to another command 

```bash 
command1 | command2
```

```bash 
[me@linuxbox ~]$ ls -l /usr/bin | less
```

---------------
It is possible to put several commands together into a pipeline. Frequently, the commands used this way are referred to as filters. Filters take input, change it somehow, and then output it. The first one we will try is sort. Imagine we wanted to make a combined list of all the executable programs in ==/bin and/usr/bin== in order to put them in sorted order, and view the resulting list.

```bash 
[me@linuxbox ~]$ ls /bin /usr/bin | sort | less
```

> [!NOTE] 
> Because we specified two directories (/bin and /usr/bin), the output of ls would have consisted of two sorted lists, one for each directory. By including sort in our pipeline, we changed the data to produce a single, sorted list.A
> **sort concatenate files content** 
> 

****##### **Pipes and Redirection operator warning**


> [!NOTE] The Difference Between > and |
> At first glance, it may be hard to understand the redirection performed by the pipeline operator | versus the redirection operator >. Simply put, **the redirection operator connects a command with a file**, **while the pipeline operator connects the output of one command with the input of a second command.**
						command1 > file1
						command1 | command2
A lot of people will try the following when they are learning about pipe-lines, “just to see what happens”:
						command1 > command2
**Answer: sometimes something really bad.**
Here is an actual example submitted by a reader who was administering
a Linux-based server appliance. As the superuser, 
 he did this:# cd /usr/bin   
			             # ls > less
The first command put him in the directory where most programs are stored, and the second command told the shell to overwrite the file less with the output of the ls command. Since the /usr/bin directory already contained a file named less (the less program), the second command overwrote the less program file with the text from ls, thus destroying the less program on his system.The lesson here is that the redirection operator silently creates or overwrites files, so you need to treat it with a lot of respect.
