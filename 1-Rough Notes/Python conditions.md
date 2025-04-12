comparison operators
== vs is 
```python 
== checks value 
!=
'>'
'<'
'>='
'<='
is -> check value and memory id 
# it is used to compare but with respect to the mem id plus the value
in -> compares partially "a" in apple --> true "a" in car --> true 
it looks a the "a" in the string it doesn't compare the whole word 

2     == “2”      \#output: False
True  == “True”   \#output: False
False == 0        \#output: True
True  == 1        \#output: True
True  == 2        \#output: False

True == 1         # True
True is 1         # False
list1 = [1,2,3]
list2 = [1,2,3]
list1 == list2    # True
list1 is list2    # False

```

**False values in pyton**
x= none 
x= false 
x= 0
x= empty collection " " () [] {}

```
if x==1:
	print("ana zh2t")
elif x==3:
	print (x)
else:
	print("2o3d fe 7eta nashfa")

if x!=7 
if not x!=7
if not (a > 10 and b > 10):

# Checking for an element in a list 
	my_list = [1, 2, 3, 4, 5]
	element = 6
	if not element in my_list:
	print(f"{element} is not in the list.")

# Checking an empty list
	my_list = []
	if not my_list:
    print("List is empty.")

# Checking a zero value
	my_number = 0
	if not my_number:
    print("Number is zero.")

# Checking None
	my_value = None
	if not my_value:
	    print("Value is None.")
```

logical operators  
```
	True and False                  #output: False
	True or False                  #output: True
	not False                     #output: True
	not (True == 2)              #output: True
	(False == 0) and (True == 1)#output: True
```


**shorthand condition** 
CanFly=true 
bird = "dove" if CanFly else "penguin"



