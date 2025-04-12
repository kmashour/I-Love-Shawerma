##### **Links** 
###### Soft links
As we look around, we are likely to see a directory listing 
(for example,/lib) with an entry like this:
```bash 
lrwxrwxrwx 1 root root 11 2018-08-11 07:34 libc.so.6 -> libc-2.6.so
```
This is a special kind of a file called a symbolic link
**(also known as a soft link or symlink).**

While the value of this might not be obvious, it is really a useful feature. Picture this scenario: a program requires the use of a shared resource of some kind contained in a file named “foo,” but “foo” has frequent version changes. It would be good to include the version number in the filename so the administrator or other interested party could see what version of “foo” is installed. This presents a problem. If we change the name of the shared resource, we have to track down every program that might use it and change it to look for a new resource name every time a new version of the resource is
installed. That doesn’t sound like fun at all.

==foo -> foo-2.6 ---- foo -> foo-2.7 ,,,,,, foo is what the symbolic links points to ==

Not only does this solve the problem of
the version upgrade, it also allows us to keep both versions on our machine.
Imagine that “foo-2.7” has a bug (damn those developers!), and we need to
revert to the old version. Again, we just delete the symbolic link pointing to
the new version and create a new symbolic link pointing to the old version.

Symbolic links were created to overcome the limitations of hard links. They work by creating a special type of file that contains a text pointer to the referenced file or directory. In this regard, ==they operate in much the same way as a Windows shortcut, though of course they predate theWindows feature by many years.== **A file pointed to by a symbolic link and the symbolic link itself are largely indistinguishable from one another.** ==For example, if you write something to the symbolic link, the referenced file is written to==. **When you delete**
**a symbolic link, however, only the link is deleted, not the file itself**. If the file is deleted before the symbolic link, the link will continue to exist but will point to nothing. In this case, **the link is said to be broken**. In many implementations, the ls command will display broken links in a distinguishing color, such as red, to reveal their presence. The concept of links can seem confusing, but hang in there. We’re going to try all this stuff, and it will, ideally, become clear.

```bash 
	The following creates a symbolic link:
	ln -s item link
```
###### Hard Links
Hard links are the original Unix way of creating links, compared to symbolic links, which are more modern. By default, every file has a single hard link that gives the file its name. When we create a hard link, we create an additional directory entry for a file. Hard links have two important limitations.

- **A hard link cannot reference a file outside its own file system. This**
  **a link cannot reference a file that is not on the same disk partition as the link itself.**
- A hard link may not reference a directory.

==A hard link is indistinguishable from the file itself. Unlike a symbolic link, when you list a directory containing a hard link, you will see no special indication of the link. When a hard link is deleted, the link is removed, but the contents of the file itself continue to exist (that is, its space is not deallocated) until all links to the file are deleted.It is important to be aware of hard links because you might encounter them from time to time, but modern practice prefers symbolic links==

**link command : ln**

Hard links command :
**ln file link**
```bash 
cp /etc/passwd .
mv passwd fun
```
Creating Hard Links
Now we’ll try some links. We’ll first create some hard links to our data file,
like so:
```bash 
[me@linuxbox playground]$ ln fun fun-hard
[me@linuxbox playground]$ ln fun dir1/fun-hard
[me@linuxbox playground]$ ln fun dir2/fun-hard
```
So now we have four instances of the file fun. Let’s take a look at our
playground directory.
```bash 
[me@linuxbox playground]$ ls -l
total 16
drwxrwxr-x 2 me me 4096 2018-01-14 16:17 dir1
drwxrwxr-x 2 me me 4096 2018-01-14 16:17 dir2
-rw-r--r-- 4 me me 1650 2018-01-10 16:33 fun
-rw-r--r-- 4 me me 1650 2018-01-10 16:33 fun-hard
```
One thing we notice is that ==both the second fields in the listings for fun
and fun-hard contain ==**a 4**, **which is the number of hard links that now exist** for
the file. Remember that a file will always have at least one link because the
file’s name is created by a link. So, how do we know that fun and fun-hard are,

in fact, the same file? In this case, ls is not very helpful. While we can see that
fun and fun-hard are both the same size (field 5), our listing provides no way
to be sure. To solve this problem, we’re going to have to dig a little deeper.
When thinking about hard links, it is helpful to imagine that files are made up of two parts.

	The data part containing the file’s contents
	The name part that holds the file’s name created with any file

When we **create** hard links, we are actually creating additional name parts** that all refer to the same data part. **The system assigns a chain of disk blocks to what is called an inode**, **which is then associated with the name part**. Each hard link therefore refers to a specific inode(**only one inode for a file and all hard links points to it)** containing the file’s contents

![[6-Attachments/Pasted image 20250222125845.png]]









> 				Creating Symlinks with the GUI
> The file managers in both GNOME and KDE provide an easy and automatic method of creating symbolic links. With GNOME, holding the **ctrl- shift** keys while dragging a file will create a link rather than copying (or moving) the file. In KDE, a small menu appears whenever a file is dropped, offering a choice of copying, moving, or linking the file.


#LinuxCommandBook1 playground page 31 