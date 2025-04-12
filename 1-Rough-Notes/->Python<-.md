TOWER OF CODERS
"The Python Docs are the Gospel of Life for those who dare tread the path of the Unknown. As the Seekers say, 'Ask not before you reach, for only by walking shall you reach, and only by reaching shall you understand.

\# <--- used to write comments 

[[notes on the language]]


[[pip]] used to install packages for python package manager for python

swaping in python
x,y = 6,7
x,y = y,x

[[python can create virtual environment]]  
[[python data model]]
[[Python arithmetic Operations]]
[[Python conditions]]
[[Python strings]]
[[python data structures]]
[[python loops]]
[[python functions]]
[[python scoping]] #themoreyoufuckaroundthemoreyouknow 
[[python sequence unpacking]] 
[[python errors and exception]] #themoreyoufuckaroundthemoreyouknow 
[[python REGEX]] #themoreyoufuckaroundthemoreyouknow 
[[python os module]] #themoreyoufuckaroundthemoreyouknow 
[[python request module]] #themoreyoufuckaroundthemoreyouknow 
[[python sys module]] #themoreyoufuckaroundthemoreyouknow 


-----------------
##### python day 2 Highlights
 - data structures in python 
 - exceptions 
 - os module 
 - crontab 
 - python scheduling 




### **2. API/HTTP Errors**

| Error Type                                 | Cause                                  | Handling Example              |
| ------------------------------------------ | -------------------------------------- | ----------------------------- |
| **`requests.exceptions.RequestException`** | General request failure (parent class) | Catch all request errors      |
| **`HTTPError`** (status codes ≥ 400)       | Invalid API request (404, 500, etc.)   | `response.raise_for_status()` |
| **`ConnectionError`**                      | Network issues                         | Retry or notify user          |
| **`Timeout`**                              | Server didn’t respond in time          | Increase timeout or retry     |


- You likely wrote something like `response.json` (without parentheses `()`), which refers to the method itself rather than executing it..

### Explanation:

- **`->`** is used in function annotations to specify the **return type**.
    
- **`None`** means the function does not return anything (similar to `void` in other languages).
def raise_for_status() -> None:
    print("This function does not return anything



1. **`with open("posts.json", "w") as f:`**
    
    - Opens (or creates) a file named `posts.json` in **write mode** (`"w"`).
        
    - The `with` statement ensures the file is **automatically closed** after the block executes (even if errors occur).
        
    - `f` is the file object used to interact with the file.
**`json.dump(data, f, indent=4)`**:

- Takes the Python object (`data`) and writes it to the file (`f`) in **JSON format**.
    
- `indent=4` adds pretty-printing (4-space indentation for readability):

### **Common Pitfalls**:

1. **Missing `with`**:

    f = open("posts.json", "w")  # Danger! Forgot to close the file.
    json.dump(data, f)
    
    - **Fix**: Always use `with` to avoid resource leak



Yes! Python can **read, write, and manipulate files without any external libraries** using built-in functions. Here’s how to do it purely with Python’s core functionality, along with the trade-offs.

---

### **1. Writing to a File (No Libraries)**
#### **Basic File Write**
```python
# Write raw text to a file
with open("output.txt", "w") as f:
    f.write("Hello, world!\nSecond line.")
```
- **`"w"` mode**: Overwrites the file if it exists.
- **`"a"` mode**: Appends to the file.

#### **Writing JSON (Manual Formatting)**
If you avoid the `json` module, you can manually convert data to a JSON-like string:
```python
data = {"name": "Alice", "age": 30}

# Manually format as JSON (no error handling for quotes/escapes)
json_str = '{\n  "name": "' + data["name"] + '",\n  "age": ' + str(data["age"]) + '\n}'

with open("data.json", "w") as f:
    f.write(json_str)
```
**Output in `data.json`**:
```json
{
  "name": "Alice",
  "age": 30
}
```
**Limitations**:  
- Fails if `data["name"]` contains `"` (would break JSON syntax).  
- No support for nested structures (e.g., lists/dicts in `data`).

---

### **2. Reading Files (No Libraries)**
#### **Read Entire File**
```python
with open("output.txt", "r") as f:
    content = f.read()  # Entire file as a string
    print(content)
```

#### **Read Line by Line**
```python
with open("output.txt", "r") as f:
    for line in f:
        print(line.strip())  # strip() removes newline chars
```

---

### **3. Manipulating Files**
#### **Update a File**
```python
# Replace a word in a file
with open("output.txt", "r") as f:
    content = f.read()

new_content = content.replace("Hello", "Hi")

with open("output.txt", "w") as f:
    f.write(new_content)
```

#### **Copy a File**
```python
with open("source.txt", "r") as src, open("copy.txt", "w") as dst:
    dst.write(src.read())
```

---

### **4. Handling JSON Without the `json` Module**
For simple JSON-like data, use string manipulation (but be cautious):
```python
# Parse a JSON-like string manually (very basic)
json_str = '{"name": "Alice", "age": 30}'

# Extract values (naive approach)
name = json_str.split('"name": "')[1].split('"')[0]
age = int(json_str.split('"age": ')[1].split("}")[0])

print(name, age)  # Output: Alice 30
```
**Warning**:  
- **Fragile**: Breaks if the JSON structure changes.  
- **No support** for nested objects/arrays.  

---

### **When to Avoid Libraries**
| Use Case | Pure Python Solution | Risks |
|----------|----------------------|-------|
| **Write text** | `f.write()` | Safe |
| **Read text** | `f.read()` | Safe |
| **Manual JSON** | String manipulation | Prone to errors |
| **Complex JSON** | Not feasible | Use `json` module |

---

### **Key Takeaways**
1. **For text files**: Python’s built-in file I/O is sufficient.  
2. **For JSON/CSV**: Libraries (`json`, `csv`) handle edge cases (quotes, escapes, encoding).  
3. **For binary files**: Use `"wb"`/`"rb"` modes.  

**Example**: Fetch API data and save it *without* the `json` module:
```python
import requests

url = "https://jsonplaceholder.typicode.com/posts"
response = requests.get(url)

if response.status_code == 200:
    with open("posts.json", "w") as f:
        f.write(response.text)  # Directly write raw JSON string
else:
    print("API request failed.")
```

---

### **Your Task**  
Try writing a script that:  
1. Reads a text file.  
2. Replaces all spaces with underscores.  
3. Saves to a new file.  

**Pure Python Solution**:  
```python
with open("input.txt", "r") as f:
    content = f.read()

new_content = content.replace(" ", "_")

with open("output.txt", "w") as f:
    f.write(new_content)
```  


output_path = "C:/Users/YourName/output.json"  # Windows
output_path = "/home/username/output.json"    # Linux/Mac

with open(output_path, "w") as f:
    f.write("Data")