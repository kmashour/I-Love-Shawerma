##### **Redirection of stdin** \ cat :concatenate command** 
- ***==The cat command reads one or more files and copies them to standard output==***
- You can use it to display files without paging
- at can accept more than one file as an argument
- it can also be used to join files together.
Long video "media" that was downloaded on sections so can use cat to join them together
ex:
movie.mpeg.001 movie.mpeg.002 ... movie.mpeg.099 
```bash 
cat movie.mpeg.0* > movie.mpeg.0
```
Because wildcards always expand in sorted order, the arguments will be
arranged in the correct order.

Nice part ya koki el gai dah 
since cat reads the files and copies them to stdout when we write use cat without argument it by default wait for stdin which is the (keyboard) so it takes whatever in the keyboard buffer until it parse 
EOF (end of text)  ---> ctrl+D

``` bash 
cat 
why so serious "then you press ctrl + D "
why so serous 
```

In the absence of filename arguments, cat copies standard input to standard output, so we see our line of text repeated. We can use this behavior to create short text files
```bash 
cat > magic.txt
```

> [!quote]
 >Using the command line, we have implemented the world’s dumbest word processor!


```bash 
[me@linuxbox ~]$ cat < magic.txt
```

Using the < redirection operator, we change the source of standard input
from the keyboard to the file magic.txt .. its not very useful bas mograd demo lel input redirection



```
cat filename1 | cat filename2
```

**Expected Behavior:**

- The **first `cat filename1`** reads and outputs the content of `filename1`.  
- The **pipe (`|`)** takes this output and passes it as input to the second `cat`.
- The **second `cat filename2`** does **not** read from standard input (which comes from `filename1`) because `cat filename2` explicitly reads from a file (`filename2`).
**Actual Behavior:**
- Instead of printing `filename1`, the second `cat` completely ignores the piped input and **only prints `filename2`**.
**Why Does This Happen?**
- ==`cat filename2` is **not** reading from standard input (stdin).== It directly opens `filename2` and prints its contents.
- The piped output from `cat filename1` is discarded because `cat filename2` is reading from an actual file instead.