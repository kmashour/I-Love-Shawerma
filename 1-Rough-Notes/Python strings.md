strings 
- ''
```pyhton
'i dont \'t''
'i dont 't'' -> error
```

- ""
   print('"hello world"')
   
- """"" """"" -> doc string used in commenting 

**concatenate strings** 
name = "koks"
full_name = "mohamed" + name * 3 + "Ali"
print ("my name is" + name )
**print (f"my name is {name}")**

**slicing** 
name = "ahmed"
print (name[1:3])  ---> hm i will count 1 2
print (name[:4])   ---> ahme i will count 0 1 2 3 
print (name[6]) **index error , ours to handle for security issues** 

**string built-in methods is booooom tarsh el tarsh** 
- order.replace("info","",2) -> replace info in string called order two times the first two occurrence
- digits.containDigits = "3242432" , "tel2343243252353"
- digits.isdigit --> true a string of digits only 
- digits.isdigit --> false the string contains characters 
- name.capitalize() --> 1st letter become uppercase 
- str.format(\*args,\*\*kwargs)
```
		intro = “My Name is {0}”
		intro.format(‘Ahmed’)
		My Name is Ahmed
		intro = “My Name is {1}, I work at {0}”
		intro.format(‘ITI’,‘Ali’)
		My Name is Ali, I work at ITI
		intro = “My Name is {name}, I work at {place}”
		intro.format(name=‘Ahmed’, place=‘ITI’)
		My Name is Ahmed, I work at ITI
```
		

**join** 
takes list return string with delimiter between indexes 
**split**
takes string and return list 

```
	“:”.join([“1”,“Ali”,“grp”])
	Tips and Tricks
	colon is the separator
	‘1:Ali:grp’
	“ ”.join(“ITI”)
	space is the separator
	‘I T I’
	“Sara Mohamed”.split(“ ”)
	space is the delimiter
	[“Sara” , “Mohamed”]
	“django:flask”.split(“:”)
	[“django” , “flask”]
	colon is
```
