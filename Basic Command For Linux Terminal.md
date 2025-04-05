
[[../Books/The Linux Command Line_ A Complete Introduction ( PDFDrive ).pdf|The Linux Command Line_ A Complete Introduction ( PDFDrive )]] #LinuxCommandBook1 

What Exactly Are Commands?
A command can be one of four different things.

- **An executable program like all those files we saw in /usr/bin.** Within this category, programs can be compiled binaries such as programs written in C and C++, or programs written in scripting languages such as the shell, Perl, Python, Ruby, and so on.
- **A command built into the shell itself.** bash supports a number of commands internally called shell builtins. The cd command, for example, is a shell builtin.
- **A shell function.** Shell functions are miniature shell scripts incorporated into the  environment. We will cover configuring the environment and writing shell functions in later chapters, but for now, just be aware that they exist.
- **An alias.** Aliases are commands that we can define ourselves, built from
  other commands.


### **System Utilities vs. Shell Utilities: Related but Different Categories**

Yes, **system utilities and shell utilities are related but distinct categories**. Let's break it down clearly.

---

**🔹 1. System Utilities** (Compiled Programs)

**Definition**:

- These are compiled **binary executables** (written in C, C++, or other languages).
    
- They interact **directly with the operating system** to perform tasks like user management, process control, or disk operations.
    

**Location**:

- Usually found in:
    
    - `/bin` → Essential commands (e.g., `ls`, `cp`, `mv`)
        
    - `/sbin` → System admin tools (e.g., `fdisk`, `iptables`)
        
    - `/usr/bin` → Common user commands (e.g., `nano`, `wget`, `git`)
        
    - `/usr/sbin` → More system admin commands (e.g., `usermod`, `groupadd`)
        
 **Examples of System Utilities**

|**Category**|**Commands**|
|---|---|
|**User Management**|`useradd`, `passwd`, `gpasswd`|
|**Process Control**|`ps`, `kill`, `top`, `htop`|
|**Networking**|`ping`, `ip`, `netstat`, `ifconfig`|
|**Disk Management**|`fdisk`, `mount`, `df`, `mkfs`|
|**File Operations**|`cp`, `mv`, `rm`, `find`|
 **System utilities are compiled programs and run as separate processes.**

---

**🔹 2. Shell Utilities (Shell Built-ins & Scripts)**

✅ **Definition**:

- **Shell utilities** are either:
    
    1. **Shell built-ins** → Commands built **inside** the shell (like `echo`, `cd`, `alias`, `export`).
        
    2. **Shell scripts** → User-written or system-provided **scripts** (like `/usr/bin/adduser`, which is a script wrapping `useradd`).
        

✅ **Location**:

- Built-in commands are part of the **shell binary itself** (e.g., `bash`, `zsh`).
    
- Scripts are often stored in `/usr/bin`, `/usr/local/bin`, or user directories (`~/bin`).
    

✅ **Examples of Shell Utilities**:

|**Type**|**Examples**|
|---|---|
|**Built-in Commands**|`cd`, `echo`, `alias`, `export`, `set`, `umask`|
|**Shell Scripts**|`/usr/bin/adduser`, `/usr/bin/service`, `/usr/bin/update-grub`|

💡 **Shell utilities run inside the shell process (not as separate processes).**

---

**🔹 Key Differences**

| Feature                 | System Utilities (Binaries)                      | Shell Utilities (Built-ins & Scripts)    |
| ----------------------- | ------------------------------------------------ | ---------------------------------------- |
| **How they work**       | Compiled programs that run as separate processes | Built into the shell or run as scripts   |
| **Execution Speed**     | Usually faster (because they’re compiled)        | Can be slower (especially scripts)       |
| **Location**            | `/bin`, `/sbin`, `/usr/bin`, `/usr/sbin`         | Inside the shell or `/usr/local/bin`     |
| **Examples**            | `useradd`, `ps`, `ls`, `df`                      | `cd`, `alias`, `echo`, `set`             |
| **Runs in a subshell?** | Yes (executes as a new process)                  | No (built-ins run inside the same shell) |

---

**🔹 Which One Takes Priority?**

If a **built-in command** and a **system utility** have the same name, the shell runs the **built-in first**.  
For example:

```bash
$ type echo
echo is a shell builtin   # The shell's internal echo command
```

But if you force execution of the system utility:

```bash
$ /bin/echo "Hello"
Hello  # Running the system utility instead
```

---

**🔹 Are System & Shell Utilities Completely Different?**

🔹 **No, they are related but serve different roles.**

- **System utilities** are standalone programs that work **independently** of the shell.
    
- **Shell utilities** are **integrated into** or run inside the shell environment



--------------------------------------------------


-------- 

# Commands 

> [!info]
> It’s possible to put more than one command on a line by separating each command with a semicolon.


## **system info command 
df / du  / free 
|-> system monitor <-Gui**
## **pwd**
## **cd** 


# [[less command]]
# [[wildcards]]
# [[mkdir command]]
# [[copy cp command]]
# [[move mv command]]
# [[ls command]]
# [[file command]]
# [[remove file and directories rm]]
# [[Links]]



# [[Identifying Commands]]

# [[Man and info page ]]




# [[Identifying Commands]]

# [[Redirection of stdin]]
# [[Redirection of stdout]]
# [[Concatenate command]]
# [[Pipelines]]
# [[uniq command]]