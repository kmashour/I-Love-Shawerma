Let's go deeper into how **UMASK interacts with file copying** and **why the owner (karim) lost write permission** even though UMASK 022 shouldn't affect the owner.

---

**Understanding UMASK and `cp` Behavior**
### **1️⃣ Default UMASK Behavior**

- The default file permission for a newly created file is **666 (`rw-rw-rw-`)**.
    
- UMASK **022** removes **write (w) permission** from **group and others**.
    
    ```
    666 (rw-rw-rw-)  
    ```
    
- 022 (--- -w- -w-)
    

---

644 (rw-r--r--)

````

👉 This means when you create a new file, it should always **retain write permission for the owner**.

---

### **2️⃣ Why Does `cp` Remove Write Permission for the Owner?**
By default, `cp` **creates a new file** instead of duplicating an existing one. This is important:

- Since `cp` creates a new file, the **new file's permissions depend on:**
1. **The original file's permissions** (`/etc/passwd` in this case).
2. **UMASK settings** of the current user (`karim`).
3. **How `cp` was executed** (whether `-p` was used).

Let's analyze step by step.

---

### **3️⃣ What Happens When You Copy `/etc/passwd`?**
Command:
```bash
cp /etc/passwd ~/
````

1. **Original file permissions (`/etc/passwd`):**
    
    ```
    -rw-r--r-- 1 root root 2986 Mar 25 21:08 /etc/passwd
    ```
    
2. **New file is created by `cp`** in `karim`'s home directory.
    
    - The system applies **UMASK (022)**.
        
    - Expected default permissions: **644 (`rw-r--r--`)**.
        

💡 **But your actual output was:**

```plaintext
-r--r----- 1 karim karim 2986 Mar 25 21:08 passwd
```

👀 **Owner lost the write permission (`rw` → `r--`). Why?**

---

### **4️⃣ Special Case: `cp` and Read-Only Files**

The reason is that **`/etc/passwd` is owned by `root` and doesn't give write access to others**.

- **`cp` tries to preserve the file mode as much as possible**.
    
- Since you **do not have write access to the original file**, `cp` creates the new file **without write permission** for you.
    

**🔹 Proof: Try copying a writable file**

```bash
touch testfile
chmod 644 testfile
cp testfile ~/testcopy
ls -l ~/testcopy
```

✔ Output:

```plaintext
-rw-r--r-- 1 karim karim 0 Mar 25 21:30 testcopy
```

**This time, the write permission is there!** 🎯

So the problem isn't UMASK alone—**it's how `cp` treats a read-only source file.**

---

### **5️⃣ Solution: Force Write Permission**

To keep the same permissions but ensure you can write, you have two options:

#### ✅ **Option 1: Use `cp -p` to preserve permissions**

```bash
cp -p /etc/passwd ~/
ls -l ~/passwd
```

This will keep permissions exactly as in `/etc/passwd`.

#### ✅ **Option 2: Manually Change Permissions After Copy**

```bash
cp /etc/passwd ~/
chmod u+w ~/passwd
ls -l ~/passwd
```

This explicitly **grants write permission** back to the owner.

---


### - **To ensure write access, manually change permissions or use `cp -p`.**
