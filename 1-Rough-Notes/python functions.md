
**input function taking input from user** 
name = input("enter your fuck'n name":)
**by default any input is a string**
number =int(input("enter your fuck'n number":))

defining a function 
```python
def funcName:
	implementation 
	return x

```

def doSum(x , y = 2 , z = 3)
	sum = x + y + z 
	print sum 

function overloading workaround
**default arguments is useful in function overloading since its not supported by python its some sort of work around** 



def deSum(\*arg): --> * allow you pass any number of arguments to the function  
def deSum(\*\*kwarg): --> * allow you pass dictionary key,value  In Python, `**` is used to collect **arbitrary keyword arguments** into a dictionary.

```
def magic_function(a, \*args, \*\*kwargs):
    print("a =", a)
    print("args =", args)
    print("kwargs =", kwargs)
magic_function(1, 2, 3, 4, x=10, y=20)
 💡 Tip:
The order **always matters**:
```




```
built-in  function core in python
user defined function
``` pyhton
def calculate_area():
def calculate_area(x,y):
	output=x*y
	return output
		or
	return x*y

```


**Enumerate function**
languages = [“JavaScript”, “Python”, “Java”]
for i , l in enumerate(languages):
print(“Element Value: ” , l , end=“,”)
print(“Element Index: ” , i)