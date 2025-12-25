## Python Notes

### 1. Python Basics

#### 1.1 Basic Syntax & Operations

#### Variables & Data Types
Variables are dynamically typed. Common types: `int`, `float`, `str`, `bool`, `list`, `tuple`, `dict`, `set`.

```python
x = 10          # int
y = 3.14        # float
name = "Alice"  # str
is_valid = True # bool
```

You can check types with `type()`:
```python
print(type(x))  # <class 'int'>
```

#### Operators
- Arithmetic: `+`, `-`, `*`, `/`, `//`, `%`, `**`
- Comparison: `==`, `!=`, `<`, `>`, `<=`, `>=`
- Logical: `and`, `or`, `not`

```python
a, b = 5, 2
print(a + b)    # 7
print(a ** b)   # 25
print(a > b)    # True
print(a > 0 and b < 10)  # True
```

#### Strings and String Methods
Strings are immutable sequences of characters.
```python
s = "hello world"
print(s.upper())      # 'HELLO WORLD'
print(s.capitalize()) # 'Hello world'
print(s[1:4])         # 'ell'
print("a" in s)       # True
print(s.replace("l", "*", 2)) # 'he**o world'
```

#### Input/Output
```python
name = input("Enter your name: ")
print("Hello,", name)
```

#### Type Casting
Convert between types using built-in functions:
```python
x = "123"
y = int(x)    # 123
z = float(x)  # 123.0
s = str(456)  # "456"
```

#### 1.2 Control Flow

#### if/elif/else
Conditional branching:
```python
x = 10
if x > 0:
	print("Positive")
elif x == 0:
	print("Zero")
else:
	print("Negative")
```

#### while & for loops
`while` repeats as long as a condition is true. `for` iterates over sequences.
```python
# while loop
n = 3
while n > 0:
	print(n)
	n -= 1

# for loop
for i in range(3):
	print(i)

# Iterating over a list
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
	print(fruit)
```

#### break, continue, pass
```python
for i in range(5):
	if i == 3:
		break   # exits loop
	if i == 1:
		continue # skips to next iteration
	print(i)

def foo():
	pass  # placeholder for future code
```

#### Loop-else statements
The `else` block runs if the loop wasn't terminated by `break`.
```python
for i in range(3):
	print(i)
else:
	print("Done")  # runs if no break occurred

for n in range(2, 10):
	for x in range(2, n):
		if n % x == 0:
			print(n, 'equals', x, '*', n//x)
			break
	else:
		print(n, 'is a prime number')
```

#### 1.3 Basic Data Structures

#### Lists
Mutable, ordered collections.
```python
lst = [1, 2, 3]
lst.append(4)
print(lst[0])      # 1
print(lst[-1])     # 4
lst[1] = 20        # modify element
print(lst)         # [1, 20, 3, 4]
```

#### Tuples
Immutable, ordered collections.
```python
t = (1, 2, 3)
print(t[1])        # 2
# t[0] = 5  # Error: tuples are immutable
```

#### Dictionaries
Key-value pairs, mutable.
```python
d = {"a": 1, "b": 2}
print(d["a"])      # 1
d["c"] = 3
for key, value in d.items():
	print(key, value)
# Dictionary methods
print(d.get("d", 0))  # 0 (default if key not found)
```

#### Sets
Unordered, unique elements.
```python
s = {1, 2, 3}
s.add(4)
print(2 in s)      # True
s.remove(1)
print(s)           # {2, 3, 4}
# Set operations
a = {1, 2, 3}
b = {3, 4, 5}
print(a | b)  # Union: {1, 2, 3, 4, 5}
print(a & b)  # Intersection: {3}
print(a - b)  # Difference: {1, 2}
```

#### Comprehensions (list, dict, set)
Concise way to create collections.
```python
# List comprehension
squares = [x**2 for x in range(5)]  # [0, 1, 4, 9, 16]

# Dict comprehension
d = {x: x**2 for x in range(3)}     # {0: 0, 1: 1, 2: 4}

# Set comprehension
evens = {x for x in range(6) if x % 2 == 0}  # {0, 2, 4}
```

### 2. Core Object-Oriented Programming (OOP)

#### 2.1 OOP Principles

##### Encapsulation
Encapsulation is the bundling of data (attributes) and methods that operate on that data within a class. Access modifiers are by convention:
- Public: `self.x`
- Protected: `self._x`
- Private: `self.__x`

```python
class Person:
	def __init__(self, name, age):
		self.name = name      # public
		self._age = age       # protected (by convention)
		self.__secret = 'xyz' # private (name mangling)

	def get_secret(self):
		return self.__secret

p = Person("Alice", 30)
print(p.name)      # Alice
print(p._age)      # 30
# print(p.__secret) # AttributeError
print(p.get_secret()) # xyz
```

##### Abstraction
Abstraction means hiding complex implementation details and exposing only the necessary parts.
```python
from abc import ABC, abstractmethod

class Shape(ABC):
	@abstractmethod
	def area(self):
		pass

class Circle(Shape):
	def __init__(self, radius):
		self.radius = radius
	def area(self):
		return 3.14 * self.radius ** 2

c = Circle(5)
print(c.area())  # 78.5
```

##### Inheritance
Inheritance allows a class to inherit attributes and methods from another class.
```python
class Animal:
	def speak(self):
		print("Animal speaks")

class Dog(Animal):
	def speak(self):
		print("Woof!")

d = Dog()
d.speak()  # Woof!
```

##### Polymorphism
Polymorphism allows different classes to be treated as instances of the same class through a common interface.
```python
class Cat(Animal):
	def speak(self):
		print("Meow!")

def animal_sound(animal):
	animal.speak()

animal_sound(Dog())  # Woof!
animal_sound(Cat())  # Meow!
```

---

#### 2.2 Classes & Objects

##### Attributes & Methods
```python
class Car:
	wheels = 4  # class variable
	def __init__(self, brand):
		self.brand = brand  # instance variable
	def drive(self):
		print(f"{self.brand} is driving")

car1 = Car("Toyota")
car1.drive()  # Toyota is driving
print(car1.wheels)  # 4
```

##### Class vs Instance Variables
Class variables are shared across all instances. Instance variables are unique to each object.
```python
class Counter:
	count = 0  # class variable
	def __init__(self):
		Counter.count += 1
		self.id = Counter.count  # instance variable

a = Counter()
b = Counter()
print(a.id, b.id)  # 1 2
print(Counter.count)  # 2
```

---

#### 2.3 Inheritance

##### Single Inheritance
```python
class Parent:
	def greet(self):
		print("Hello from Parent")

class Child(Parent):
	pass

c = Child()
c.greet()  # Hello from Parent
```

##### Multiple Inheritance
```python
class A:
	def foo(self):
		print("A")
class B:
	def foo(self):
		print("B")
class C(A, B):
	pass
c = C()
c.foo()  # A (MRO: C, A, B)
```

##### super()
`super()` is used to call methods from a parent class.
```python
class Base:
	def hello(self):
		print("Hello from Base")
class Derived(Base):
	def hello(self):
		super().hello()
		print("Hello from Derived")
d = Derived()
d.hello()
# Output:
# Hello from Base
# Hello from Derived
```

#### 2.4 Special (Dunder) Methods

##### __init__, __str__, __repr__
```python
class Point:
	def __init__(self, x, y):
		self.x = x
		self.y = y
	def __str__(self):
		return f"({self.x}, {self.y})"
	def __repr__(self):
		return f"Point({self.x}, {self.y})"

p = Point(1, 2)
print(str(p))   # (1, 2)
print(repr(p))  # Point(1, 2)
```

##### Operator overloading (__add__, __eq__, etc.)
```python
class Vector:
	def __init__(self, x, y):
		self.x = x
		self.y = y
	def __add__(self, other):
		return Vector(self.x + other.x, self.y + other.y)
	def __eq__(self, other):
		return self.x == other.x and self.y == other.y
	def __repr__(self):
		return f"Vector({self.x}, {self.y})"

v1 = Vector(1, 2)
v2 = Vector(3, 4)
print(v1 + v2)  # Vector(4, 6)
print(v1 == Vector(1, 2))  # True
```

#### 2.5 Advanced OOP Concepts

##### Method Resolution Order (MRO)
Determines the order in which base classes are searched when executing a method.
```python
class X: pass
class Y: pass
class Z(X, Y): pass
print(Z.mro())
# [<class '__main__.Z'>, <class '__main__.X'>, <class '__main__.Y'>, <class 'object'>]
```

##### Properties & Descriptors
Properties allow managed attribute access.
```python
class Celsius:
	def __init__(self, temp=0):
		self._temp = temp
	@property
	def temp(self):
		return self._temp
	@temp.setter
	def temp(self, value):
		if value < -273.15:
			raise ValueError("Too cold!")
		self._temp = value

c = Celsius(25)
c.temp = 30
print(c.temp)  # 30
# c.temp = -300  # Raises ValueError
```

##### Abstract base classes (abc module)
See Abstraction above. Abstract base classes define interfaces.

##### Data classes (dataclasses module)
Automatically generate special methods for classes.
```python
from dataclasses import dataclass
@dataclass
class Item:
	name: str
	price: float

i = Item("Pen", 1.5)
print(i)  # Item(name='Pen', price=1.5)
```

##### Slots (__slots__)
Restrict instance attributes and save memory.
```python
class Point:
	__slots__ = ['x', 'y']
	def __init__(self, x, y):
		self.x = x
		self.y = y
p = Point(1, 2)
# p.z = 3  # AttributeError: 'Point' object has no attribute 'z'
```

### 3. Advanced Data Structures & Standard Library

#### 3.1 Collections Module

##### namedtuple
Immutable, tuple-like objects with named fields.
```python
from collections import namedtuple
Point = namedtuple('Point', ['x', 'y'])
p = Point(1, 2)
print(p.x, p.y)  # 1 2
```

##### deque
Double-ended queue, fast appends/pops from both ends.
```python
from collections import deque
d = deque([1, 2, 3])
d.appendleft(0)
d.append(4)
print(d)  # deque([0, 1, 2, 3, 4])
d.pop()   # 4
d.popleft() # 0
```

##### Counter
Counts hashable objects.
```python
from collections import Counter
c = Counter('banana')
print(c)  # Counter({'a': 3, 'n': 2, 'b': 1})
print(c.most_common(1))  # [('a', 3)]
```

##### defaultdict
Like dict, but provides a default value for missing keys.
```python
from collections import defaultdict
d = defaultdict(int)
d['a'] += 1
print(d['a'])  # 1
print(d['b'])  # 0 (default)
```

##### OrderedDict
Dict that remembers insertion order (Python 3.7+ dicts do this by default).
```python
from collections import OrderedDict
od = OrderedDict()
od['a'] = 1
od['b'] = 2
print(list(od.keys()))  # ['a', 'b']
```

##### ChainMap
Groups multiple dicts (or mappings) together.
```python
from collections import ChainMap
a = {'x': 1}
b = {'y': 2}
cm = ChainMap(a, b)
print(cm['x'], cm['y'])  # 1 2
```

#### 3.2 Other Data Structure Tools

##### heapq
Heap queue (priority queue) algorithms.
```python
import heapq
nums = [3, 1, 4]
heapq.heapify(nums)
heapq.heappush(nums, 2)
print(heapq.heappop(nums))  # 1 (smallest)
```

##### bisect
Maintain sorted lists, do fast binary search.
```python
import bisect
l = [1, 3, 4]
bisect.insort(l, 2)
print(l)  # [1, 2, 3, 4]
print(bisect.bisect_left(l, 3))  # 2
```

##### array
Efficient arrays of basic values (numbers, chars).
```python
import array
a = array.array('i', [1, 2, 3])
a.append(4)
print(a)  # array('i', [1, 2, 3, 4])
```

##### memoryview
Access the memory of other binary objects without copying.
```python
b = bytearray(b'abc')
mv = memoryview(b)
print(mv[0])  # 97 (ASCII for 'a')
mv[0] = 65
print(b)  # bytearray(b'Abc')
```

#### 3.3 Sets & Frozensets

##### Set operations
```python
a = {1, 2, 3}
b = {3, 4, 5}
print(a | b)  # Union: {1, 2, 3, 4, 5}
print(a & b)  # Intersection: {3}
print(a - b)  # Difference: {1, 2}
print(a ^ b)  # Symmetric difference: {1, 2, 4, 5}
```

##### Immutability use cases
`frozenset` is an immutable set, useful as dict keys or set elements.
```python
fs = frozenset([1, 2, 3])
# fs.add(4)  # AttributeError
d = {fs: "frozen"}
print(d[fs])  # frozen
```

### 4. Functions & Functional Programming

#### 4.1 Functions

##### First-class functions
Functions can be assigned to variables, passed as arguments, and returned from other functions.
```python
def greet(name):
	return f"Hello, {name}!"
say_hello = greet
print(say_hello("Alice"))  # Hello, Alice!
```

##### Closures
A closure is a function that remembers the environment in which it was created.
```python
def make_multiplier(n):
	def multiplier(x):
		return x * n
	return multiplier
times3 = make_multiplier(3)
print(times3(10))  # 30
```

##### Scope: LEGB
Python uses Local, Enclosing, Global, Built-in scope resolution.
```python
x = 'global'
def outer():
	x = 'enclosing'
	def inner():
		x = 'local'
		print(x)
	inner()
	print(x)
outer()
print(x)
# Output:
# local
# enclosing
# global
```

#### 4.2 Higher-Order Functions

##### map, filter, reduce
Apply a function to a sequence (map), filter items, or reduce to a single value.
```python
nums = [1, 2, 3, 4]
print(list(map(lambda x: x * 2, nums)))  # [2, 4, 6, 8]
print(list(filter(lambda x: x % 2 == 0, nums)))  # [2, 4]
from functools import reduce
print(reduce(lambda x, y: x + y, nums))  # 10
```

##### Lambda functions
Anonymous, inline functions.
```python
add = lambda x, y: x + y
print(add(2, 3))  # 5
```

##### functools.partial
Fixes some arguments of a function and returns a new function.
```python
from functools import partial
def power(base, exp):
	return base ** exp
square = partial(power, exp=2)
print(square(5))  # 25
```

##### Decorators (function + class decorators)
Decorators modify the behavior of functions or classes.
```python
def my_decorator(func):
	def wrapper(*args, **kwargs):
		print("Before call")
		result = func(*args, **kwargs)
		print("After call")
		return result
	return wrapper

@my_decorator
def say_hi():
	print("Hi!")

say_hi()
# Output:
# Before call
# Hi!
# After call
```

### 5. Iterators, Generators & Async Concepts

#### 5.1 Iteration Protocol

##### __iter__, __next__
An object is iterable if it implements `__iter__()`, and an iterator if it also implements `__next__()`.
```python
class Count:
	def __init__(self, n):
		self.n = n
		self.i = 0
	def __iter__(self):
		return self
	def __next__(self):
		if self.i < self.n:
			val = self.i
			self.i += 1
			return val
		else:
			raise StopIteration

c = Count(3)
for x in c:
	print(x)  # 0 1 2
```

#### 5.2 Generators

##### yield, yield from
Generators are functions that yield values one at a time, pausing between each.
```python
def countdown(n):
	while n > 0:
		yield n
		n -= 1
for i in countdown(3):
	print(i)  # 3 2 1
```

`yield from` delegates part of its operations to another generator.
```python
def gen():
	yield from range(3)
for x in gen():
	print(x)  # 0 1 2
```

##### Generator expressions
Compact way to create generators.
```python
gen = (x*x for x in range(3))
print(list(gen))  # [0, 1, 4]
```

#### 5.3 Coroutines & Async Programming

##### async/await basics
Coroutines are defined with `async def` and use `await` to pause for asynchronous operations.
```python
import asyncio
async def main():
	print('Hello')
	await asyncio.sleep(1)
	print('World')
# asyncio.run(main())
```

##### Event loop mechanics
The event loop runs and schedules async tasks.
```python
import asyncio
async def say(msg, delay):
	await asyncio.sleep(delay)
	print(msg)
async def main():
	await asyncio.gather(say('A', 1), say('B', 2))
# asyncio.run(main())
```

##### asyncio tasks, futures
Tasks wrap coroutines for concurrent execution. Futures represent a result not yet available.
```python
import asyncio
async def foo():
	return 42
async def main():
	task = asyncio.create_task(foo())
	result = await task
	print(result)
# asyncio.run(main())
```

##### Async context managers & iterators
Use `async with` and `async for` for asynchronous resource management and iteration.
```python
import asyncio
class AsyncCM:
	async def __aenter__(self):
		print('Enter')
	async def __aexit__(self, exc_type, exc, tb):
		print('Exit')
async def main():
	async with AsyncCM():
		print('Inside')
# asyncio.run(main())
```

### 6. Context Managers

#### with statement
The `with` statement ensures resources are properly acquired and released.
```python
with open('file.txt', 'w') as f:
	f.write('Hello')
# File is automatically closed
```

#### Writing custom context managers
Implement `__enter__` and `__exit__` methods.
```python
class MyContext:
	def __enter__(self):
		print('Entering')
		return self
	def __exit__(self, exc_type, exc_val, exc_tb):
		print('Exiting')
with MyContext():
	print('Inside')
# Output: Entering, Inside, Exiting
```

#### contextlib utilities (closing, contextmanager, ExitStack)
`contextlib` provides helpers for context managers.
```python
from contextlib import closing, contextmanager, ExitStack
import socket
with closing(socket.socket()) as s:
	pass  # socket closed automatically

@contextmanager
def simple_cm():
	print('Enter')
	yield
	print('Exit')
with simple_cm():
	print('Inside')

with ExitStack() as stack:
	f1 = stack.enter_context(open('a.txt', 'w'))
	f2 = stack.enter_context(open('b.txt', 'w'))
# Both files closed automatically
```

### 7. Metaprogramming

#### 7.1 Reflection & Introspection

##### getattr, setattr, hasattr, delattr
Manipulate object attributes dynamically.
```python
class Foo:
	x = 10
f = Foo()
print(getattr(f, 'x'))  # 10
setattr(f, 'y', 20)
print(f.y)  # 20
print(hasattr(f, 'x'))  # True
delattr(f, 'x')
print(hasattr(f, 'x'))  # False
```

##### Inspect module
The `inspect` module provides introspection utilities.
```python
import inspect
def func(a, b=2): pass
print(inspect.signature(func))  # (a, b=2)
print(inspect.getmembers(str))  # List of str's members
```

#### 7.2 Metaclasses

##### type()
`type` can be used to create classes dynamically.
```python
MyClass = type('MyClass', (object,), {'x': 5})
obj = MyClass()
print(obj.x)  # 5
```

##### Custom metaclasses
Metaclasses customize class creation.
```python
class Meta(type):
	def __new__(cls, name, bases, dct):
		dct['y'] = 100
		return super().__new__(cls, name, bases, dct)
class A(metaclass=Meta):
	x = 10
a = A()
print(a.x, a.y)  # 10 100
```

##### __new__ and __init_subclass__
`__new__` customizes instance creation; `__init_subclass__` customizes subclassing.
```python
class B:
	def __new__(cls):
		print('Creating instance')
		return super().__new__(cls)
	def __init_subclass__(cls):
		print('Subclass created:', cls)
class C(B):
	pass
c = C()  # Triggers both methods
```

##### Dynamic class creation
Classes can be created and modified at runtime.
```python
def make_class(name):
	return type(name, (), {})
D = make_class('D')

print(type(d))  # <class '__main__.D'>
```

### 8. Modules, Packages & Import System

#### Absolute vs relative imports
```python
# Absolute import
from mypackage import module
# Relative import
from . import sibling_module
```

#### Understanding __init__.py, __main__.py
`__init__.py` marks a directory as a package. `__main__.py` allows running a package as a script.

#### Namespace packages
Packages without `__init__.py` can be spread across directories.

#### __all__, __file__, sys.path
`__all__` controls what is imported with `from module import *`.
```python
# In mymodule.py
__all__ = ['foo', 'bar']
```
`__file__` is the path to the module file. `sys.path` is the list of import search paths.
```python
import sys
print(__file__)
print(sys.path)
```

#### Creating & distributing packages (setuptools, pip)
Use `setuptools` to package and distribute Python projects. Install with `pip`.
```python
# setup.py example
from setuptools import setup
setup(name='mypkg', version='0.1', packages=['mypkg'])
# pip install .
```

### 9. Typing & Static Analysis

#### Type hints (typing module)
Add type annotations to function signatures and variables for static analysis and better code clarity.
```python
def greet(name: str, age: int) -> str:
	return f"Hello {name}, you are {age} years old."

x: int = 10
y: list[str] = ["a", "b"]
```

#### TypeVar, Generic, Protocols
**TypeVar**: Create generic types for functions/classes.
```python
from typing import TypeVar, List
T = TypeVar('T')
def first(lst: List[T]) -> T:
	return lst[0]
```
**Generic**: Create generic classes.
```python
from typing import Generic
class Box(Generic[T]):
	def __init__(self, value: T):
		self.value = value
box = Box(123)  # Box[int]
```
**Protocols**: Define structural subtyping (duck typing for interfaces).
```python
from typing import Protocol
class Flyer(Protocol):
	def fly(self) -> None: ...
class Bird:
	def fly(self): print("Flap!")
def let_fly(f: Flyer):
	f.fly()
let_fly(Bird())  # OK
```

#### NewType, Literal, Union
**NewType**: Create distinct types for type checking.
```python
from typing import NewType
UserId = NewType('UserId', int)
def get_user(user_id: UserId):
	pass
uid = UserId(123)
get_user(uid)
```
**Literal**: Restrict values to specific literals.
```python
from typing import Literal
def move(direction: Literal["up", "down"]):
	print(direction)
move("up")  # OK
# move("left")  # Type checker error
```
**Union**: Accept multiple possible types.
```python
from typing import Union
def stringify(val: Union[int, float]) -> str:
	return str(val)
```

#### Checking with mypy, pyright
Use static type checkers to catch type errors before runtime.
- **mypy**: `mypy script.py`
- **pyright**: `pyright script.py` or use in VS Code for real-time feedback.
```python
# Example: mypy will catch this error
def add(x: int, y: int) -> int:
	return x + y
add("a", 2)  # Error: str passed instead of int
```

#### Typed dictionaries, dataclasses with types
**TypedDict**: Dicts with fixed key types.
```python
from typing import TypedDict
class Movie(TypedDict):
	title: str
	year: int
m: Movie = {"title": "Inception", "year": 2010}
```
**Dataclasses with types**: Classes with type annotations and auto-generated methods.
```python
from dataclasses import dataclass
@dataclass
class Point:
	x: float
	y: float
p = Point(1.0, 2.0)
print(p.x, p.y)
```

### 10. Concurrency & Parallelism

#### GIL (Global Interpreter Lock)
The GIL is a mutex that allows only one thread to execute Python bytecode at a time (in CPython). This means CPU-bound threads do not run in true parallel, but I/O-bound threads can still be useful.
```python
import threading
import time
def count():
	x = 0
	for _ in range(10**7):
		x += 1
threads = [threading.Thread(target=count) for _ in range(2)]
for t in threads: t.start()
for t in threads: t.join()
# Both threads run, but not in true parallel for CPU-bound work due to GIL.
```

#### Threading
Use threads for I/O-bound tasks (network, file I/O). Threads share memory space.
```python
import threading
import time
def worker(n):
	print(f"Thread {n} starting")
	time.sleep(1)
	print(f"Thread {n} done")
threads = [threading.Thread(target=worker, args=(i,)) for i in range(3)]
for t in threads: t.start()
for t in threads: t.join()
# Output: Threads run concurrently (overlap in time)
```

#### Multiprocessing
Use for CPU-bound tasks. Each process has its own Python interpreter and memory space (bypasses GIL).
```python
from multiprocessing import Process
def f(x):
	print(f"Process {x}")
procs = [Process(target=f, args=(i,)) for i in range(2)]
for p in procs: p.start()
for p in procs: p.join()
# True parallelism for CPU-bound tasks
```

#### concurrent.futures (ThreadPoolExecutor, ProcessPoolExecutor)
High-level interface for running tasks concurrently using threads or processes.
```python
from concurrent.futures import ThreadPoolExecutor, ProcessPoolExecutor
def square(x):
	return x * x
# Thread pool (good for I/O-bound)
with ThreadPoolExecutor(max_workers=2) as executor:
	results = list(executor.map(square, [1, 2, 3]))
	print(results)  # [1, 4, 9]
# Process pool (good for CPU-bound)
with ProcessPoolExecutor(max_workers=2) as executor:
	results = list(executor.map(square, [1, 2, 3]))
	print(results)  # [1, 4, 9]
```

#### Asyncio vs threads vs processes comparisons
- **asyncio**: Best for many I/O-bound tasks (network, disk) that spend time waiting. Single-threaded, uses event loop.
- **Threads**: Good for I/O-bound tasks that use blocking APIs. Shared memory, but GIL limits CPU-bound parallelism.
- **Processes**: Best for CPU-bound tasks. True parallelism, but higher memory usage and inter-process communication overhead.

**Example: asyncio for concurrent I/O**
```python
import asyncio
async def fetch(n):
	print(f"Fetching {n}")
	await asyncio.sleep(1)
	print(f"Done {n}")
async def main():
	await asyncio.gather(fetch(1), fetch(2), fetch(3))
# asyncio.run(main())
```


### 11. File I/O & Serialization

#### Text & binary file operations
**Text files:**
```python
# Writing text
with open('hello.txt', 'w') as f:
	f.write('Hello, world!\n')
# Reading text
with open('hello.txt', 'r') as f:
	content = f.read()
	print(content)
```
**Binary files:**
```python
# Writing binary
with open('data.bin', 'wb') as f:
	f.write(b'\x00\x01\x02')
# Reading binary
with open('data.bin', 'rb') as f:
	data = f.read()
	print(data)
```

#### Working with pathlib
`pathlib` provides an object-oriented interface for filesystem paths.
```python
from pathlib import Path
p = Path('hello.txt')
print(p.exists())
print(p.read_text())
p.write_text('New content')
for file in Path('.').glob('*.txt'):
	print(file)
```

#### JSON, Pickle, CSV, YAML, XML
**JSON:**
```python
import json
data = {'a': 1, 'b': 2}
# Write JSON
with open('data.json', 'w') as f:
	json.dump(data, f)
# Read JSON
with open('data.json', 'r') as f:
	obj = json.load(f)
	print(obj)
```
**Pickle:** (Python object serialization)
```python
import pickle
nums = [1, 2, 3]
with open('nums.pkl', 'wb') as f:
	pickle.dump(nums, f)
with open('nums.pkl', 'rb') as f:
	nums2 = pickle.load(f)
	print(nums2)
```
**CSV:**
```python
import csv
# Write CSV
with open('data.csv', 'w', newline='') as f:
	writer = csv.writer(f)
	writer.writerow(['name', 'age'])
	writer.writerow(['Alice', 30])
# Read CSV
with open('data.csv', 'r') as f:
	reader = csv.reader(f)
	for row in reader:
		print(row)
```
**YAML:** (requires PyYAML)
```python
# pip install pyyaml
import yaml
data = {'a': 1, 'b': 2}
with open('data.yaml', 'w') as f:
	yaml.dump(data, f)
with open('data.yaml', 'r') as f:
	obj = yaml.safe_load(f)
	print(obj)
```
**XML:**
```python
import xml.etree.ElementTree as ET
tree = ET.ElementTree(ET.fromstring('<root><a>1</a></root>'))
root = tree.getroot()
print(root.tag)
for child in root:
	print(child.tag, child.text)
```

#### File context managers
Use `with` to ensure files are properly closed, even if errors occur.
```python
with open('file.txt', 'w') as f:
	f.write('Hello')
# File is closed automatically
```

12. Error Handling & Exceptions
try/except/else/finally
Custom exception classes
Exception chaining
Logging with logging module
Contextual & defensive error handling

13. Testing & Debugging
13.1 Testing
unittest
pytest (fixtures, markers, parametrize)
doctest
Mocks & patching
13.2 Debugging Tools
pdb
logging configuration
Tracebacks & profiling
14. Performance & Optimization
Big-O awareness
Profiling: cProfile, timeit, line_profiler
Optimization techniques
functools.lru_cache
Memory management & gc module
Cython, Numba, writing C extensions
15. Popular Python Libraries (Ecosystem Mastery)
15.1 Data Science Stack
NumPy
Arrays, broadcasting
Vectorization
Indexing, slicing
Universal functions (ufuncs)
Pandas
Series & DataFrame
Indexing (loc, iloc)
GroupBy, merges, joins
Handling missing data
Time series
File formats (CSV, Excel, Parquet)
Matplotlib
Basic plotting
Subplots
Styles & customization
Integration with NumPy & Pandas
15.2 Visualization Add-ons (optional)
Seaborn
Plotly
16. Python Tooling & Developer Workflow
16.1 Code Quality & Formatting
black (auto-formatter)
isort (import sorting)
flake8 and pylint (linting)
mypy (type checking)
16.2 Environment & Dependency Management
venv
pip
pip-tools
Poetry
Virtualenvwrapper
16.3 Build & Packaging
setuptools
wheels
pipx
17. Software Design & Architecture in Python
Design patterns (factory, strategy, adapter, observer, etc.)
Modular design
Separation of concerns
Dependency injection
Clean architecture concepts
18. Networking, APIs & Web Development (Optional but Common)
HTTP basics
requests library
Web scraping (BeautifulSoup, Selenium)
REST API design
FastAPI, Flask basics
Async web services (FastAPI async, aiohttp)
19. Databases (Optional but Very Common)
SQLite, PostgreSQL drivers
ORM concepts
SQLAlchemy
Transactions & sessions
20. Automation & Scripting
CLI tools with argparse, click, typer
Batch file processing
Scheduling

