Great topic — **Lexical Scope** is a core concept in Python (and many other programming languages), especially when dealing with functions, closures, and variable visibility.

---

### 🧠 What is Lexical Scope?

**Lexical scope** (also called _static scope_) means **a variable’s scope is determined by its position in the written code**, not by the flow of the program during execution.

In Python, when you refer to a variable inside a function, Python looks for that variable in a specific order, known as the **LEGB rule**:

---

### 🔍 LEGB Rule (Scope Resolution Order):

1. **L**ocal → Inside the current function
    
2. **E**nclosing → Any enclosing function's scope (only applies to nested functions)
    
3. **G**lobal → At the top level of the module (file)
    
4. **B**uilt-in → Python's built-in names like `len`, `sum`, etc.
    

---

### 🧪 Example:

```python
x = "global"

def outer():
    x = "enclosing"

    def inner():
        x = "local"
        print(x)

    inner()

outer()
```

#### Output:

```
local
```

Python sees `x = "local"` in the innermost scope, so it uses that.

---

### Now, remove the local assignment:

```python
x = "global"

def outer():
    x = "enclosing"

    def inner():
        print(x)  # No local x, so it looks up to the enclosing one

    inner()

outer()
```

#### Output:

```
enclosing
```

This is **lexical scope** in action: the function `inner()` "remembers" the variable `x` from where it was _written_, not from where it’s called.

---

### 🚫 What Lexical Scope Is _Not_:

It’s **not** dynamic scope. Python does **not** look at where a function was called from to find variables — only at where it was **defined**.

---

Alright! Let’s **shadow** a built-in function like `len()` and then see how to **still access the original** if needed.

---

### 🧪 Shadowing a Built-in Example:

```python
# Shadowing the built-in 'len'
def len(x):
    return "This is not the real length!"

print(len([1, 2, 3]))  # Will call our version, not the built-in
```

#### Output:

```
This is not the real length!
```

---

### 🛡️ Accessing the Real Built-in Anyway:

If you ever accidentally (or intentionally) shadow a built-in, you can still access the real one using the `builtins` module.

```python
import builtins

# Our shadowed version
def len(x):
    return "Fake length!"

# Using the real built-in 'len'
real_length = builtins.len([1, 2, 3])
print(real_length)  # Output: 3
```

---

### ✅ Summary:

- You can shadow built-in names, but it’s usually best **not to**.
    
- If you do, use `import builtins` to get back the original function safely.
    

---
Awesome — let's dive into the **`global`** and **`nonlocal`** keywords. These let you _modify_ variables that live outside your current function, breaking the usual "read-only" nature of outer scopes.

---

## 🔁 `global`: Reaching for the Module-Level Variable

### 🔍 Use `global` when you want to **assign** to a variable declared outside all functions (in the global scope).

#### 🧪 Example:

```python
x = 10

def update():
    global x
    x = 42

update()
print(x)  # Output: 42
```

Without `global`, you'd create a **local** variable `x`, not touch the global one.

---

## 🔁 `nonlocal`: Reaching for the Enclosing Function's Variable

### 🔍 Use `nonlocal` when you're inside a **nested function** and want to **modify** a variable from the _enclosing_ function’s scope.

#### 🧪 Example:

```python
def outer():
    x = 10

    def inner():
        nonlocal x
        x = 99

    inner()
    print(x)  # Output: 99

outer()
```

Without `nonlocal`, the `inner()` function would create its own local `x`, and the `outer()` function’s `x` would stay unchanged.

---

## 🚫 What Happens Without Them?

### Without `global`:

```python
x = 10

def update():
    x = 99  # This just creates a new local x

update()
print(x)  # Output: 10 (not 99)
```

### Without `nonlocal`:

```python
def outer():
    x = 10

    def inner():
        x = 99  # New local x, doesn't affect the outer one

    inner()
    print(x)  # Output: 10
```

---

# **simple visual diagram** that shows how Python’s **scope layers** work, and how `global` and `nonlocal` let you reach into outer layers:

---

```
+-----------------------+
| Built-in Scope        |  (e.g., len, sum, print)
+-----------------------+
| Global Scope          |  (Variables defined at the top level of your script)
| x = 10                |
| def outer():          |
+-----------------------+
| Enclosing Scope       |  (Variables in enclosing functions)
|     x = 20            |
|     def inner():      |
+-----------------------+
| Local Scope           |  (Current function’s variables)
|         x = 30        |
+-----------------------+
```

### 🛠 What You Can Do:

- ✅ You can **read** from outer scopes.
    
- ❌ You **cannot assign** to outer variables _unless_ you use:
    
    - `nonlocal` → for enclosing function's variable
        
    - `global` → for module-level variable
        

---

### ✅ Example Using Both:

```python
x = "global"

def outer():
    x = "enclosing"
    
    def inner():
        nonlocal x
        print("Before:", x)
        x = "modified by inner"
        print("After:", x)
    
    inner()
    print("Outer sees:", x)

outer()
print("Global still sees:", x)
```

#### Output:

```
Before: enclosing
After: modified by inner
Outer sees: modified by inner
Global still sees: global
```

---

### 🧠 Want to Practice?

Try writing a mini function like this:

> Create an `outer()` function that defines `count = 0`, and an `inner()` function that increases `count` by 1 each time it's called. Use `nonlocal` so it actually updates the count.

Let me know when you're ready and I’ll walk you through it!