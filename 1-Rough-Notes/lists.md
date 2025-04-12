 
exception halts the execution of the program 
we were introduced to index error
newList = [1, “hi”, True] - > newList[3] \#Index Error

-------

https://www.w3schools.com/python/python_lists.asp

newlist = [] 
mylist = ["c","javascript","python","java","php"]


- mylist.pop(4)
- mylist.append("go")
- mylist.insert(3,"scala")
- mylist.remove("c")
- yourlist = ["Ruby" , "RUST"]
- mylist.extend(yourlist) --> append list 
- mylist.clear() --> empty list
- mylist.delete() ---> delete from existence 


The `del` keyword also removes the specified index:
thislist = ["apple", "banana", "cherry"]  
del thislist[0]  
print(thislist)

The `del` keyword can also delete the list completely. 
thislist = ["apple", "banana", "cherry"]  
del thislist

Clear the List
The `clear()` method empties the list.
The list still remains, but it has no content 
thislist = ["apple", "banana", "cherry"]  
thislist.clear()  
print(thislist)

traceback means exception 

- list are overloaded accepts + --> mylist=mylist+yourlist
--------



**List class constructor**
```
thislist = list(("apple", "banana", "cherry")) # note the double round-brackets  
print(thislist)

```

The outer and inner parentheses are **not** redundant — they serve two different purposes:
- This creates a **tuple**. -> ("apple", "banana", "cherry")
- This is a call to the built-in `list()` function. -> It **converts** the tuple into a **list**
--------


**enumerate function** 
languages = [“JavaScript”, “Python”, “Java”]
for i , l in enumerate(languages):
print(“Element Value: ” , l, end=“, ”)
print(“Element Index: ” , i)
Output:
Element Value: JavaScript, Element index: 0
Element Value: Python, Element index: 1
Element Value: Java, Element index: 2

------------------


**all** check if all items in an iterable object hold a true value
**any** check if one item at least in an iterable object holds a true value 

L = [0,5,9,7,8]
all(L)#False
any(L)#True

--------------------


**slicing** 
mylist = ["c","javascript","python","java","php"]
print(mylist[1:3])

| **Slicing Syntax**   | **Description**                                                  | **Example** | **Output**             |
| -------------------- | ---------------------------------------------------------------- | ----------- | ---------------------- |
| `l[start:end]`       | Extracts a sublist from `start` (inclusive) to `end` (exclusive) | `l[1:4]`    | `[20, 30, 40]`         |
| `l[:end]`            | Extracts from the beginning to `end` (exclusive)                 | `l[:3]`     | `[10, 20, 30]`         |
| `l[start:]`          | Extracts from `start` (inclusive) to the end                     | `l[2:]`     | `[30, 40, 50]`         |
| `l[:]`               | Extracts the entire list                                         | `l[:]`      | `[10, 20, 30, 40, 50]` |
| `l[start:end:step]`  | Extracts a sublist with a step (skips elements)                  | `l[::2]`    | `[10, 30, 50]`         |
| `l[start:end:-step]` | Extracts a sublist with a negative step (reverses)               | `l[::-1]`   | `[50, 40, 30, 20, 10]` |
| `l[-index]`          | Extracts from the end of the list (negative index)               | `l[-1]`     | `50`                   |
| `l[start:-1]`        | Extracts from `start` to second last element                     | `l[1:-1]`   | `[20, 30, 40]`         |

---

Key Points:
- **Start**: Where to begin slicing. 
- **End**: Where to stop slicing (exclusive). 
- **Step**: How to step through the list (e.g., every 2nd element).
- **Negative indices**: Counting from the end of the list.

------------


**list comprehension** 

In list comprehension, you need to **define what you're iterating over** and **what you're collecting**.

- **`item for item in mylist[1:3]`**:
    - The first `item` is the **variable** representing each element in `mylist[1:3]`.
    - The second `item` is the **element** that gets added to the new list.

In list comprehension, the **left side variable** like `item` acts as an **intermediary** — it temporarily holds the value of each element as the loop runs. But it's also the value that gets **added to the new list**.

```python
mylist = ["c", "javascript", "python", "java", "php"]

# Using a list as the variable name in list comprehension
sliced_list = [language for language in mylist[1:3]]

print(sliced_list)  # Output: ['javascript', 'python']
```
- **`mylist[1:3]`**: Slices the list to get `["javascript", "python"].
- **`language`**: The loop variable that temporarily holds each element (`"javascript"` and `"python"`) as we iterate over the sliced list.
- **Result**: Creates a new list `['javascript', 'python']`.
