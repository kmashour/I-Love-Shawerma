
[[Basic Command For Linux Terminal]]
[[Bash Manual page Reviewing]]
[[The Linux Filesystem]]
[[Linux Boot]]
[[Notes on packet mangement]]



The **`c`** at the beginning of the file permissions (`crw--w----.`) indicates that `/dev/pts/0` is a **character device file**.
### **Explanation of Each Part**

```
crw--w----.   1 clientvm tty  136, 0 Mar 28 16:36 /dev/pts/0
```

- **`c`** → This indicates a **character device** file.
    
- **`rw--w----`** → These are the file permissions.
    
- **`.`** → Indicates SELinux security context (if enabled).
    
- **`1`** → Number of hard links.
    
- **`clientvm`** → Owner of the file.
    
- **`tty`** → Group associated with the file.
    
- **`136, 0`** → **Major and minor device numbers** (used by the kernel to identify the device).
    
- **`Mar 28 16:36`** → Last modification time.
    
- **`/dev/pts/0`** → File path.
    

---

### **What is a Character Device?**

A **character device** (indicated by `c`) is a special file that represents **hardware or virtual devices** that **process data one character at a time**. Examples:

- **Terminals (`/dev/pts/0`)**
    
- **Serial ports (`/dev/ttyS0`)**
    
- **Sound cards (`/dev/snd/*`)**
    

These devices **do not have a buffer** and **directly communicate with hardware or software interfaces**.

Try to re-dive in its concept to uncover what is under linux hood