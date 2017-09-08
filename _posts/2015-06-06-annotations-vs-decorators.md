---
layout: post
title: decorators vs annotations
author: Ren
---

I've been thinking a lot lately about the differences between [annotations in Java](https://docs.oracle.com/javase/tutorial/java/annotations/) and [decorators in Python](https://www.python.org/dev/peps/pep-0318/). They're both concepts I recently picked up and it's started to bother me that I don't understand them too well.

1. [Python Decorators](#python-decorators)
2. [Java Annotations](#java-annotations)
3. [Comparison](#comparison)

##Python Decorators
Python's decorators are described in the Python glossary as, "A function returning another function". It's a clean way to wrap functions in other functions without the tendency to end up with nasty nested code like JavaScript. Let's go through some examples and then write our own decorators.

###@classmethod
This is simply the decorator form of classmethod(), a builtin function in Python. Classmethods enable one to access properties and methods of the class it's contained in. Here's a common usage of classmethods without decorators:

```python
class SomeClass:
	def __init__(self, a, b):
		self.a = a
		self.b = b
		
	def fromdict(cls, d):
		return cls(d['a'], d['b'])
	fromdict = classmethod(fromdict)

	def __eq__(self, other):
		return self.a == other.a and self.b == other.b

print(SomeClass.fromdict({'a':1, 'b':2}) == SomeClass(1, 2))
# >>> True
```

By wrapping ```fromdict()``` with ```classmethod()``` I created a second constructor that takes in a dictionary and calls its own class' ```__init__``` constructor. Alternatively, instead of manually wrapping ```fromdict()``` I can simply apply the ```@classmethod``` decorator and let the interpreter do the wrapping for me:

```python
class SomeClass:
	...
	@classmethod
	def fromdict(cls, d):
		return cls(d['a'], d['b'])
	...
```

I prefer to use the ```@classmethod``` decorator because I think it's much clearer that it's a class method. Especially with syntax highlighting you clearly see that it's a special method. The Python glossary perfectly describes the decorator syntax as being "merely syntactic sugar".

###@property
This is another fun one that reveals a little bit about Python itself. You may have noticed that I used ```__init__``` and ```__eq__``` in the example above. There are many special functions that are mapped to operators which can be overloaded. ```__set__``` and ```__get__``` are two very cool operators to overload:

```python
class AnotherClass:
	def __init__(self, x):
		self.x = x

	def __get__( self, instance, owner ):
		return self.value
	def __set__( self, instance, value ):
		self.value= float(value)

```

####Descriptors are a special

##Java Annotations
##Comparisons