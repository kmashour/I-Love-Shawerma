##### **mkdir—Create Directories**
The mkdir command is used to create directories. It works like this:
```bash 
mkdir directory...
Note that when three periods... follow an argument in the description of
a command (as in the preceding example), it means that the argument can
be repeated
```
==Thus, the following command:
	mkdir dir1
would create a single directory named dir1. This command
	mkdir dir1 dir2 dir3
would create three directories named dir1, dir2, and dir3.==

   - Create specific directories:
    mkdir path/to/directory1 path/to/directory2 ...
  - Create specific directories and their parents if needed:
    mkdir -p|--parents path/to/directory1 path/to/directory2 ...
  - Create directories with specific permissions:
    mkdir -m|--mode rwxrw-r-- path/to/directory1 path/to/directory2 ...


