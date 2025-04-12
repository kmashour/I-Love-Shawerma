
```python 
l = [1,13,3,7]
a,b,c,d = l
# a=1,b=13,c=3,d=7
a,*b,c = l
# a=1,b=[13,3],c=7
```

**extended unpacking**, using the `*` operator in assignments.
Let’s break it down:

---

#### ✅ What it does:
- `a` gets the **first** element → `1`
- `c` gets the **last** element → `7`
- `*b` gets **everything in between** → `[13, 3]`

So after unpacking:
```python
a = 1
b = [13, 3]
c = 7
```

The `*` tells Python: \* will result in creating a list when used with varaibles   
**“Pack all the remaining middle elements here.”**

 **Rules to remember:**
- You can use `*` only once in a single unpacking.
- The result of `*` is always a **list**, even if it ends up empty.
---

#### examples:

```python
x, *y = [10, 20, 30]
# x = 10, y = [20, 30]

*x, y = [10, 20, 30]
# x = [10, 20], y = 30

a, *b, c, d = [1, 2, 3, 4, 5]
# a = 1, b = [2, 3], c = 4, d = 5
```

#### extended unpacking with return in functions
```python
def generate_numbers():
    return 1, 2, 3, 4, 5

first, *middle, last = generate_numbers()

print(f"First: {first}, Middle: {middle}, Last: {last}")



```
 \*args , \*\*kargs **[[python functions]]** <- extended unpacking with function arguments  
 
#### extended unpacking with loops 
 nos nos msh fahmo awy
---
```python
l = [10, 20, 30, 40]

for first, *rest in [l[i:i+2] for i in range(0, len(l), 2)]:
    print(f"First: {first}, Rest: {rest}")
```

---
 Breakdown:
1. **List `l` Initialization:**
    ```python
    l = [10, 20, 30, 40]
    ```
    We have the list `l` with the elements `[10, 20, 30, 40]`.
2. **List Comprehension with `*`:**
    ```python
    [l[i:i+2] for i in range(0, len(l), 2)]
    ```
    This list comprehension creates sublists from `l` with a step size of 2. It breaks `l` into pairs:
    - When `i = 0`, `l[0:2]` → `[10, 20]` 
    - When `i = 2`, `l[2:4]` → `[30, 40]` 
    So the list comprehension results in:
    ```python
    [[10, 20], [30, 40]]
    ```
3. **Loop with Unpacking:**
    ```python
    for first, *rest in [[10, 20], [30, 40]]:
        print(f"First: {first}, Rest: {rest}")
    ```
    The `for` loop iterates over the sublists `[10, 20]` and `[30, 40]`:
    - **First iteration**: 
        - `first` gets `10`, and `*rest` gets `[20]`.    
        - Prints: `First: 10, Rest: [20]`   
    - **Second iteration**
        - `first` gets `30`, and `*rest` gets `[40]`. 
        - Prints: `First: 30, Rest: [40]`
Output:
```
First: 10, Rest: [20]
First: 30, Rest: [40]
```
---
 Key Points:
- `first` grabs the **first element** of each sublist.
- `*rest` grabs **all remaining elements** in that sublist, even if there's only one element.