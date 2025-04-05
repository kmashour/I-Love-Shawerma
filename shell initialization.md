Here’s a **visual representation** of how **Bash initialization files** are loaded in different scenarios:

---

### **🖥️ Bash Startup Process**

```plaintext
                      +-------------------------------+
                      | User starts a shell session   |
                      +-------------------------------+
                                  │
    ┌─────────────────────────────┴──────────────────────────────┐
    │                      What type of shell?                   │
    └────────────────────────────────────────────────────────────┘
                                  │
              +-------------------+------------------+
              |                                      |
       **Login Shell**                        **Non-login Shell**
   (e.g., SSH, `su - user`)                (e.g., open terminal)
              │                                      │
   +----------+-----------+             +-----------+----------+
   |   Check `/etc/profile`   |             |   Check `/etc/bash.bashrc`   |
   +----------+-----------+             +-----------+----------+
              │                                      │
   +----------+-----------+                         ▼
   |    Check `~/.bash_profile`    |   →   Loads `~/.bashrc`
   |     (or `~/.profile`)        |
   +----------------------+ 
              │
              ▼
  Loads `~/.bashrc` (if sourced manually)

```

---

### **🔍 Explanation of the Flow**

1. **Login Shell**
    
    - **Global settings**: `/etc/profile` runs first.
        
    - **User settings**: `~/.bash_profile` (or `~/.profile`) runs.
        
    - **If `~/.bash_profile` exists**, it **does not** load `~/.bashrc` unless explicitly sourced inside `.bash_profile`.
        
2. **Non-login Shell**
    
    - **Global settings**: `/etc/bash.bashrc` runs first.
        
    - **User settings**: `~/.bashrc` runs.
        

---

### **📌 Key Takeaways**

- **Login shells** load **`~/.bash_profile`**, which may source `~/.bashrc`.
    
- **Non-login shells** load **only** `~/.bashrc`.
    
- **Interactive shells (scripts)** do **not** load either file unless sourced.
    

Would you like a graphical representation as an image? 🎨