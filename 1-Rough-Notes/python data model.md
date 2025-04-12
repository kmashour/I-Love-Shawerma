Every object has an identity, a type and a value. An object’s _identity_ never changes once it has been created; you may think of it as the object’s address in memory. The [`is`](https://docs.python.org/3.13/reference/expressions.html#is) operator compares the identity of two objects; the [`id()`](https://docs.python.org/3.13/library/functions.html#id "id") function returns an integer representing its identity.

**An object’s type determines the operations that the object supports (e.g., “does it have a length?”)** and also defines the possible values for objects of that type. The [`type()`](https://docs.python.org/3.13/library/functions.html#type "type") function returns an object’s type (which is an object itself). Like its identity, an object’s _type_ is also unchangeable. 

The _value_ of some objects can change. Objects whose value can change are said to be _mutable_; objects whose value is unchangeable once they are created are called _immutable_. (The value of an immutable container object that contains a reference to a mutable object can change when the latter’s value is changed; however the container is still considered immutable, because the collection of objects it contains cannot be changed. So, immutability is not strictly the same as having an unchangeable value, it is more subtle.) An object’s mutability is determined by its type; for instance, numbers, strings and tuples are immutable, while dictionaries and lists are mutable

Objects are never explicitly destroyed; however, when they become unreachable they may be garbage-collected. An implementation is allowed to postpone garbage collection or omit it altogether — it is a matter of implementation quality how garbage collection is implemented, as long as no objects are collected that are still reachable 


Note that the use of the implementation’s tracing or debugging facilities may keep objects alive that would normally be collectable. Also note that catching an exception with a [`try`](https://docs.python.org/3.13/reference/compound_stmts.html#try)…[`except`](https://docs.python.org/3.13/reference/compound_stmts.html#except) statement may keep objects alive.

Some objects contain references to “external” resources such as open files or windows. It is understood that these resources are freed when the object is garbage-collected, but since garbage collection is not guaranteed to happen, such objects also provide an explicit way to release the external resource, usually a `close()` method. Programs are strongly recommended to explicitly close such objects. The [`try`](https://docs.python.org/3.13/reference/compound_stmts.html#try)…[`finally`](https://docs.python.org/3.13/reference/compound_stmts.html#finally) statement and the [`with`](https://docs.python.org/3.13/reference/compound_stmts.html#with) statement provide convenient ways to do this.

Some objects contain references to other objects; these are called _containers_. Examples of containers are tuples, lists and dictionaries. The references are part of a container’s value. In most cases, when we talk about the value of a container, we imply the values, not the identities of the contained objects; however, when we talk about the mutability of a container, only the identities of the immediately contained objects are implied. So, if an immutable container (like a tuple) contains a reference to a mutable object, its value changes if that mutable object is changed.

Types affect almost all aspects of object behavior. Even the importance of object identity is affected in some sense: for immutable types, operations that compute new values may actually return a reference to any existing object with the same type and value, while for mutable objects this is not allowed. For example, after `a = 1; b = 1`, _a_ and _b_ may or may not refer to the same object with the value one, depending on the implementation. This is because [`int`](https://docs.python.org/3.13/library/functions.html#int "int") is an immutable type, so the reference to `1` can be reused. This behaviour depends on the implementation used, so should not be relied upon, but is something to be aware of when making use of object identity tests. However, after `c = []; d = []`, _c_ and _d_ are guaranteed to refer to two different, unique, newly created empty lists. (Note that `e = f = []` assigns the _same_ object to both _e_ and _f_.)


#### The standard type hierarchy
None ->  It is used to signify the absence of a value in many situations,**it is returned from functions that don’t explicitly return anything. Its truth value is false**

NotImplemented -> Numeric methods and rich comparison methods should return this value if they do not implement the operation for the operands provided.**It should not be evaluated in a boolean context.**

> [!warning]
> Changed in version 3.9: Evaluating in a boolean context is deprecated. While it currently evaluates as true, it will emit a [`DeprecationWarning`]. It will raise a [`TypeError`] in a future version of Python.

`numbers.Number` #themoreyoufuckaroundthemoreyouknow 

`numbers.Integral ->` There are two types of integers:
- Integers int
- float

`numbers.real` 
`numbers.complex`

`Sequences ->` These represent finite ordered sets indexed by non-negative numbers. The built-in function [`len()`](https://docs.python.org/3.13/library/functions.html#len "len") returns the number of items of a sequence

`immutable sequences ->` An object of an immutable sequence type cannot change once it is created. (If the object contains references to other objects, these other objects may be mutable and may be changed; however, the collection of objects directly referenced by an immutable object cannot change.)
- Strings
- Tuples
- Bytes - >The items are 8-bit bytes, represented by integers in the range 0 <= x < 256. Bytes literals (like `b'abc'`)
`Mutable sequences ->` There are currently two intrinsic mutable sequence types: 
- lists 
- Byte Arrays #themoreyoufuckaroundthemoreyouknow 

Set types 
Mappings
Dictionaries 

----------------------------

Python is datatypes are dynamic , python is case sensitive , names should be expressive, variable naming rules are the same here as in C , C++

name="hello"
age=5 
bool -> true / false
if true == 5 ----> true is one
age = 17.5

**casting object**
int(age)
float (number)
str (number)

**swapping variables** 

Traditional Way
x = 4
y = 5
temp = x
x = y
y = temp
Python Way
x,y = 4,5
x,y = y,x
**vscode extension pylint -> syntax organizer** 



# Monkey ass sniffing 
#themoreyoufuckaroundthemoreyouknow 

**CPython implementation detail:** CPython currently uses a reference-counting scheme with (optional) delayed detection of cyclically linked garbage, which collects most objects as soon as they become unreachable, but is not guaranteed to collect garbage containing circular references. See the documentation of the [`gc`](https://docs.python.org/3.13/library/gc.html#module-gc "gc: Interface to the cycle-detecting garbage collector.")???? module for information on controlling the collection of cyclic garbage. Other implementations act differently and CPython may change. Do not depend on immediate finalization of objects when they become unreachable (so you should always close files explicitly). ???