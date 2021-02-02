# Object Oriented Programming in Python

## Contents
1. [Class](#Class)
2. [Object](#Object)
3. [Constructor](#Constructor)
4. [Python Packages and modules using OOPs](#Modules-and-Packages-in-Python')
    1. [Module](#Module)
    2. [Packages](#Packages)

****************************
Python is a multi-paradigm programming language. Meaning, it supports different programming approach.

One of the popular approach to solve a programming problem is by creating objects. This is known as Object-Oriented Programming (OOP).

An object has two characteristics:
- attributes
- behavior

Let's take an example:

If `student` is an object then,

- name, age, color are `attributes`
- singing, Writing, Playing are `behavior`

## Class
Class is a collection of attributes and methods

syntax:
```python
class student:
  attributes
  methods
```
#### Attributes
Attributes are variables of a class that are shared between all of its instances

#### Methods
Methods are functions defined inside the body of a class. They are used to define the behaviors of an object

## Objects
An object is an instance of a class. When class is defined, only the description for the object is defined. Therefore, no memory or storage is allocated.

The example for object of student class can be:
```python
obj = student()
 ```
Here, `obj` is object of class `student`
**************
## Constructor

### \_\_init__
We use the **__init__()** method to initialize (e.g., specify) an object’s initial attributes by giving them their default value (or state). This method must have at least one argument as well as the self variable, which refers to the object itself (e.g.: student)

**`Note:`** We will never have to call the `__init__()` method; it gets called automatically when we create a new `class` instance.
```python
class student:
    # Initializer / Instance Attributes
    def __init__(self, name, rollnumber):
        self.name = name
        self.rollnumber = rollnumber
```
## Types of Attributes
1. **Instance variables**:
They are owned by the specific instances of a class. This means for two different instances the instance attributes are usually different

2. **Class variable or Static Variable**:
Class attributes are attributes which are owned by the class itself. They will be shared by all the instances of the class. Therefore they have the same value for every instance. We define class attributes outside of all the methods, usually they are placed at the top, right below the class header.
example:
```python
class student:
  college = 'APSSDC'
  def __init__(self, name, rollnumber):
    self.name = name
    self.rollnumber = rollnumber
std1 = student('Student1', '123456')
std2 = student('Student2', '654321')
print("Instance variables are:")
print(std1.name)
print(std2.name)
print("Class variables are:")
print(std1.college)
print(std2.college)
```
After Execution the output is
```python
Instance variables are:
Student1
Student2
Class variables are:
APSSDC
APSSDC
```
## Types of Methods
1. **Instance methods**

Instance methods are defined inside a class and are used to get the contents of an instance. They can also be used to perform operations with the attributes of our objects. Like the `__init__` method, the first argument is always `self`

Example:
```python
class student:
    college = 'APSSDC'
    
    def __init__(self, subject1, subject2, subject3):
        self.subject1 = subject1
        self.subject2 = subject2
        self.subject3 = subject3

    def average(self):
        return (self.subject1 + self.subject2 + self.subject3) / 3
        
std1 = student(58,92,45)
std2 = student(96,91,85)

print('Average marks of std1 is:', std1.average())
print('Average marks of std2 is:', std2.average())
```
After Executing the output is
```output
Average marks of std1 is: 65.0
Average marks of std2 is: 90.66666666666667
```
The Instance methods are classified in two types

**i. Accessor method**

An `accessor` method is a function that returns a copy of an internal variable or computed value. A common practice is to name these with the word `get`. 

**ii. Mutator method**

A `mutator` method is a function that modifies the value of an internal data variable in some way. The simplest form of mutator function is one that sets a variable directly to a new value. A common practice is to name these with the word `set`.

Example:
```python
class student:
    college = 'APSSDC'
    
    def __init__(self, subject1, subject2, subject3):
        self.subject1 = subject1
        self.subject2 = subject2
        self.subject3 = subject3

    def average(self):
        return (self.subject1 + self.subject2 + self.subject3) / 3
        
    def get_subject1(self):
        return self.subject1
        
    def set_subject1(self):
        return self.subject1 + 5
        
std1 = student(58,92,45)
std2 = student(96,91,85)

print('Subject1 marks of before adding grace marks is:', std1.get_subject1())
print('Subject1 marks of after addding grace marks is:', std2.get_subject1())
```
After Executing instance method output is:
```output
Subject1 marks of before adding grace marks is: 58
Subject1 marks of after addding grace marks is: 96
```

2. **Class methods**

A class method is a method that is bound to a class rather than its object. It doesn't require creation of a class instance
```python
class student:
    college = 'APSSDC'
    
    def __init__(self, subject1, subject2, subject3):
        self.subject1 = subject1
        self.subject2 = subject2
        self.subject3 = subject3

    def average(self):
        return (self.subject1 + self.subject2 + self.subject3) / 3
        
    @classmethod
    def get_college_name(cls):
        return cls.college


print('College name of students is:', student.get_college_name())


```
After excuting class method the output is
```output
College name of students is: APSSDC
```
3. **Static methods**

Static methods, much like class methods, are methods that are bound to a class rather than its object.

They do not require a class instance creation. So, they are not dependent on the state of the object.

The difference between a static method and a class method is:
- Static method knows nothing about the class and just deals with the parameters.
- Class method works with the class since its parameter is always the class itself.

```python
class student:
    college = 'APSSDC'
    
    def __init__(self, subject1, subject2, subject3):
        self.subject1 = subject1
        self.subject2 = subject2
        self.subject3 = subject3

    def average(self):
        return (self.subject1 + self.subject2 + self.subject3) / 3
        
    @classmethod
    def get_college_name(cls):
        return cls.college
        
    @staticmethod
    def about_us():
        print('APSSDC is non profit Government Organisation')
 
print('About APSSDC:\n', student.about_us())
```
After executing static method output is
```output
APSSDC is non profit Government Organisation
```
************
## Modules and Packages in Python

### Module

Modules in Python are simply Python files with a `.py` extension. The name of the module will be the name of the file. A Python module can have a set of functions, classes or variables defined and implemented.

Example of module with name factorial is shown below.
```python
def fact(num):
  result = 1
  for i in range(1,num + 1):
      result *= i
  return result
  
pi = 3.14
```
1. **Importing module objects to the current namespace**
```python
from factorial import fact
```
2. **Importing all objects from a module**
```python
from factorial import *
```
3. **Importing object with Custom import name**
```python
from factorial import fact as f
```

We can look for which `functions` are implemented in each module by using the `dir` function:
```python
dir(factorial)
```

### Packages
Packages are namespaces which contain multiple packages and modules themselves. They are simply directories, but with a twist.

Each package in Python is a directory which MUST contain a special file called `__init__.py`. This file can be empty, and it indicates that the directory it contains is a Python package, so it can be imported the same way a module can be imported.

If we create a directory called `calculator`, which marks the package name, we can then create a module inside that package called `factorial`. We also must not forget to add the `__init__.py` file inside the `calculator` directory.

To use the module `factorial` from package `calculator`, we can import it in two ways

1. **Method - 1**
```python
import calculator.factorial
```
2. **Method - 2**
```python
from calculator import factorial
```
