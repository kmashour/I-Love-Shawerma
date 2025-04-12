##### **Redirection of stdout**  < > << >>
If we look at a command like ls, we can see that it displays its results
and its error messages on the screen. Keeping with the Unix theme of “everything is a file,” programs such as ls actually send their results to a special file called standard output (often expressed as stdout) and their status messages to another file called standard error (stderr). **By default, both standard output and standard error are linked to the screen and not saved into a disk file** ( #themoreyoufuckaroundthemoreyouknow ) . In addition, many programs take input from a facility called standard input (stdin), which is, by default, attached to the keyboard. I/O redirection allows us to change where output goes and where input comes from. Normally, output goes to the screen and input comes from the keyboard, but with I/O redirection, we can change that.

==If the file does not already exist, > , >> using redirection creates it ==
###### Redirecting Standard Output
```bash 
     ls -l /usr/bin > ls-output.txt
```


```bash 
		ls -l /bin/usr > ls-output.txt
```

ls -l /bin/usr this file or directory doesn't exist so the the are rewritten now it will have 0 bytes since the stdout was empty only the error where redirected to stderr so the file was truncated ,,, always remember ya kimo any well written unix program are probably handled in a way that the out is sent to stdout and the error it redirected to stderr so  > only redirect stdout so it generated nothing so the .txt is truncated 


In fact, if we ever need to actually truncate a file (or create a new, empty file), we can use a
```bash 
[me@linuxbox ~]$ > ls-output.txt
```

we append redirected output to a file instead of overwriting the file from the beginning
```bash 
[me@linuxbox ~]$ ls -l /usr/bin >> ls-output.txt
```

###### Redirecting Standard Error
we have referred to the first **three of these file streams** as standard input, output,
and error, the shell references them internally as file descriptors 0, 1, and 2
the shell references **them internally as file descriptors** 0, 1, and 2, respectively.
```bash 
[me@linuxbox ~]$ ls -l /bin/usr 2> ls-error.txt
```
The file descriptor 2 is placed immediately before the redirection operator

###### Redirecting Standard Output and Standard Error to One File
Traditional way  the old shell way 
```bash 
[me@linuxbox ~]$ ls -l /bin/usr > ls-output.txt 2>&1
```

The order must like this first the stdout is redirect then we redirect the stdout to descriptor file &1 which is the srdout ...... syntax order sensitive we cant redirect the stderr before the stdout 2>&1 cant come before the command > txt ....

Recent versions of bash provide a second, more streamlined method for performing this combined redirection

```bash 
[me@linuxbox ~]$ ls -l /bin/usr &> ls-output.txt
```
to append both 
```bash 
[me@linuxbox ~]$ ls -l /bin/usr &>> ls-output.txt
```

###### Disposing of Unwanted Output ||| THE --->  /dev/null
Sometimes “silence is golden” and we don’t want output from a command;
we just want to throw it away. This applies particularly to error and status
messages. The system provides a way to do this by redirecting output to a
special file called /dev/null. This file is a system device often referred to as
a bit bucket, which accepts input and does nothing with it. To suppress error
messages from a command, we do this:
```bash 
[me@linuxbox ~]$ ls -l /bin/usr 2> /dev/null

```

