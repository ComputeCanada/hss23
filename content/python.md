+++
title = "Introduction to programming in Python"
slug = "python"
+++
**February 14, 2023, 3:00-4:20pm EST**

**Presented by**: Alex Razoumov

**Duration**: 80 minutes

**Description**: In this very short (1h20m) introduction to Python, we will cover the basics of running Python
inside Jupyter notebooks, basic use of variables, lists, dictionaries, talk about defining functions and using
external libraries. We will provide Python in the cloud, so there is no need to install it on your own
computer for this session.

Register {{<a "https://www.eventbrite.ca/e/512983085217" "here">}}

Le même séminaire [en français](/pythonfr).

#### Biographies

**Alex Razoumov**: Alex earned his PhD in computational astrophysics from the University of British Columbia
and held postdoctoral positions in Urbana–Champaign, San Diego, Oak Ridge, and Halifax. He has worked on
numerical models ranging from galaxy formation to core-collapse supernovae and stellar hydrodynamics, and has
developed a number of computational fluid dynamics and radiative transfer codes and techniques. He spent five
years as HPC Analyst in SHARCNET helping researchers from diverse backgrounds to use large clusters, and in
2014 moved back to Vancouver to focus on scientific visualization and training researchers to use advanced
computing tools. He is now with Simon Fraser University.

**Mohamed Jabir**: Détenant une maîtrise en intelligence d’affaire, Mohamed a travaillé pendant plus de 20 ans
dans un laboratoire de recherche où il offrait son support aux professeurs et étudiants de 2ème cycle. Il a
rejoint récemment Calcul Québec où il fait partie des analystes de support aux utilisateurs des ressources de
calcul.

<!-- {{< vimeo 690948795 >}} -->
<!-- <br> -->

<!-- - [Watch this session on Vimeo](https://vimeo.com/690948795) -->

# Course notes

**Disclaimer**: These notes started few years ago from the {{<a "https://software-carpentry.org/lessons"
"official SWC lesson">}} but then evolved quite a bit to include other topics.

## Why Python?

Python is a free, open-source programming language developed in the 1980s and 90s that became really popular
for scientific computing in the past 15 years.

#### Python vs. Excel

- Unlike Excel, Python can essentially read any type of data, both structured and unstructured.
- Python is free and open-source.
- Data manipulation is much easier in Python. There are thousands of data processing, machine learning, and
  visualization libraries.
- Python can handle much larger amounts of data: limited not by Python, but by your available computing
  resources. In addition, Python can run at scale on larger systems.
- Python is more reproducible (rerun / modify the script).
- Python can run on any platform (Windows, Mac, Linux).

<!-- Python code is easier to reproduce -->
<!-- Python is faster doing difficult calculations. -->
<!-- Python is easier than vba. -->
<!-- Python works better with big data. -->
<!-- Python is open source and has access to an enormous amount of libraries. -->
<!-- On the other hand. -->
<!-- Excel is known by more people. -->
<!-- Excel is faster for simple calculations, graphs etc. -->

#### Python vs. other programming languages

Python pros                                 | Python cons
--------------------------------------------|------------------------
elegant scripting language                  | slow (interpreted, dynamically typed)
powerful, compact constructs for many tasks |
very popular across all fields              |
huge number of external libraries           |

## Starting Python

There are many ways to run Python commands:

* from a Unix shell you can start a Python shell and type commands there,
* you can launch Python scripts saved in plain text *.py files,
* you can execute Python cells inside Jupyter notebooks; the code is stored inside JSON files, displayed as HTML

Today we will be using a Jupyter notebook at https://jupyter.pyten.calculquebec.cloud (English) or
https://jupyter.pytfr.calculquebec.cloud (French).
1. we will distribute the usernames and password now
1. please login with your unique username
1. start a new Python 3 notebook

**Local option** for more advanced users: if you have Python + Jupyter installed locally on your computer, and
you know what you are doing, you can start a Jupyter notebook locally from your shell by typing `jupyter
notebook`.

<!-- ## Virtual Python environments -->

<!-- We talk about creating Virtual Python environments in the HPC course. These environment are very useful, as -->
<!-- not only can you install packages into your directories without being root, but they also let you create -->
<!-- sandbox Python environments with your custom set of packages -- perfect when you work on multiple projects, -->
<!-- each with a different list of dependencies. -->

<!-- To create a Python environment (you do this only once): -->

<!-- ```sh -->
<!-- module avail python               # several versions available -->
<!-- module load python/3.8.10 -->
<!-- virtualenv --no-download astro    # install Python tools in your $HOME/astro -->
<!-- source astro/bin/activate -->
<!-- pip install --no-index --upgrade pip -->
<!-- pip install --no-index numpy jupyter pandas            # all these will go into your $HOME/astro -->
<!-- avail_wheels --name "*tensorflow_gpu*" --all_versions   # check out the available packages -->
<!-- pip install --no-index tensorflow_gpu==2.2.0            # if needed, install a specific version -->
<!-- ... -->
<!-- deactivate -->
<!-- ``` -->

<!-- Once created, you would use it with: -->

<!-- ```sh -->
<!-- source ~/astro/bin/activate -->
<!-- python -->
<!-- ... -->
<!-- deactivate -->
<!-- ``` -->

<!-- We'll talk more about virtual Python environments in -->
<!-- [Section 10](../python-10-libraries#virtual-environments-and-packaging). -->

## Navigating Jupyter interface

- File | Save As - to rename your notebook
- File | Download - download the notebook to your computer
- File | New Launcher - to open a new launcher dashboard, e.g. to start a terminal
- File | Logout - to terminate your job (everything is running inside a Slurm job!)

Explain: tab completion, annotating code, displaying figures inside the notebook.

* <font size="+2">Esc</font> - leave the cell (border changes colour) to the control mode
* <font size="+2">A</font> - insert a cell above the current cell
* <font size="+2">B</font> - insert a cell below the current cell
* <font size="+2">X</font> - delete the current cell
* <font size="+2">M</font> - turn the current cell into the markdown cell
* <font size="+2">H</font> - to display help
* <font size="+2">Enter</font> - re-enter the cell (border becomes green) from the control mode
* can enter Latex equations in a markdown cell, e.g. $int_0^\infty f(x)dx$

```py
print(1/2)   # to run all commands in the cell, either use the Run button, or press shift+return
```

## Variables and Assignment

- Python is a dynamically typed language: all variables have types, but types can change on the fly
- possible names for variables
  - don't use built-in function names for variables, e.g. declaring `sum` will prevent you from using sum(), same for
    `print`
- Python is case-sensitive

```py
age = 100
name = 'Jason'
print(name, 'is', age, 'years old')
a = 1; b = 2   # can use ; to separate multiple commands in one line
a, b = 1, 2    # assign variables in a tuple notation; same as last line
a = b = 10     #  assign a value to multiple variables at the same time
b = "now I am a string"    # variables can change their type on the fly
```

* variables persist between cells
* variables must be defined before use
* variables can be used in calculations

```py
age = age + 3   # another syntax: age += 3
print('age in three years:', age)
```

{{< question num=1 >}}
What is the final value of `position` in the program below? (Try to predict the value without running the program, then
check your prediction.)
```py
initial = 1
position = initial
initial = 2
print(position)
```
{{< /question >}}

With simple variables in Python, assigning `var2 = var1` will create a new object in memory `var2`. Here we have two
distinct objects in memory: `initial` and `position`.

> Note: With more complex objects, its name could be a pointer. E.g. when we study lists, we'll see that `initial` and
> `new` below really point to the same list in memory:
> ```py
> initial = [1,2,3]
> new = initial        # create a pointer to the same object
> initial.append(4)    # change the original list to [1, 2, 3, 4]
> print(new)           # [1, 2, 3, 4]
> new = initial[:]     # one way to create a new object in memory
> import copy
> new = copy.deepcopy(initial)   # another way to create a new object in memory
> ```

Use square brackets to get a substring:
```py
element = 'helium'
print(element[0])     # single character
print(element[0:3])   # a substring
```

{{< question num=2 >}}
If you assign `a=123`, what happens if you try to get the second digit of `a`?
{{< /question >}}

* Python is case-sensitive
* use meaningful variable names

## Data Types and Type Conversion

```py
print(type(52))
print(type(52.))
print(type('52'))
```

```py
print(name+' Smith')   # can add strings
print(name*10)         # can replicate strings by mutliplying by a number
print(len(name))       # strings have lengths
```

```py
print(1+'a')        # cannot add strings and numbers
print(str(1)+'a')   # this works
print(1+int('2'))   # this works
```

## Builtin libraries

* Python comes with a number of built-in functions
* a function may take zero or more arguments

```py
print('hello')
print()
```

```py
print(max(1,2,3,10))
print(min(5,2,10))
print(min('a', 'A', '0'))   # works with characters, the order is (0-9, A-Z, a-z)
print(max(1, 'a'))    # can't compare these
round(3.712)      # to the nearest integer
round(3.712, 1)   # can specify the number of decimal places
help(round)
round?   # Jupyter Notebook's additional syntax
```

* every function returns something, whether it is a variable or None
```py
result = print('example')
print('result of print is', result)   # what happened here? Answer: print returns None
```

## Conditionals

Python implements conditionals via `if`, `elif` (short for "else if") and `else`. Use an `if` statement to
control whether some block of code is executed or not. Let's consider the boundary between the Antiquity and
the Middle Ages:

```py
year = 830
if year > 476:
    print('year', year, 'falls into the medieval era')
```

Let's modify the year:

```py
year = 205
if year > 476:
    print('year', year, 'falls into the medieval era')
```

Add an `else` statement:

```py
year = 205
if year > 476:
    print('year', year, 'falls into the medieval era')
else:
    print('year', year, 'falls into the classical antiquity period')
```

Add an `elif` statement:

```py
x = 5
if x > 0:
    print(x, 'is positive')
elif x < 0:
    print(x, 'is negative')
else:
    print(x, 'is zero')
```

What is the problem with the following code?

```py
grade = 85
if grade >= 70:
    print('grade is C')
elif grade >= 80:
    print('grade is B')
elif grade >= 90:
    print('grade is A')
```

## Lists

A list stores many values in a single structure.

```py
T = [27.3, 27.5, 27.7, 27.5, 27.6]   # array of temperature measurements
print('temperature:', T)
print('length:', len(T))
```

```py
print('zeroth item of T is', T[0])
print('fourth item of T is', T[4])
```

```py
T[0] = 21.3
print('temperature is now:', T)
```

```py
primes = [2, 3, 5]
print('primes is initially', primes)
primes.append(7)   # append at the end
primes.append(11)
print('primes has become', primes)
```

```py
print('primes before', primes)
primes.pop(4)      # remove element #4
print('primes after', primes)
primes.remove(2)   # remove first value 2
```

```py
a = []   # start with an empty list
a.append('Vancouver')
a.append('Toronto')
a.append('Kelowna')
print(a)
```

```py
a[99]   # will give an error message (past the end of the array)
a[-1]   # display the last element; what's the other way?
a[:]    # will display all elements
a[1:]   # starting from #1
a[:1]   # ending with but not including #1
```

Lists can be heterogeneous and nested:

```py
a = [11, 21, 31]
b = ['Mercury', 'Venus', 'Earth']
c = 'hello'
nestedList = [a, b, c]
print(nestedList)
```

You can search inside a list:

```py
'Venus' in b      # returns True
'Mars' in b       # returns False
b.index('Venus')      # returns 1 (position index)
```

And you sort lists alphabetically:

```py
b.sort()
b             # returns ['Earth', 'Mercury', 'Venus']
```

To delete an item from a list:

```py
b.pop(2)             # you can use its index
b.remove('Earth')       # or you can use its value
```

{{< question num=2b >}}
Write a script to find the second largest number in the list [77,9,23,67,73,21].
{{< /question >}}

<!-- ```py -->
<!-- a = [77, 9, 23, 67, 73, 21] -->
<!-- a.sort(); a[-2]                    # should print 73 -->
<!-- a.sort(reverse=True); a[1]         # should print 73 -->
<!-- sorted(a)[-2]                      # should print 73 -->
<!-- ``` -->

## Loops

<!-- # For Loops -->

*For* loops are very common in Python and are similar to *for* in other languages, but one nice twist with Python is
that you can iterate over any collection, e.g., a list, a character string, etc.

```py
for number in [2, 3, 5]:    # number is the loop variable; [...] is a collection
    print(number)          # Python uses indentation to show the body of the loop
```

This is equivalent to:
```py
print(2)
print(3)
print(5)
```

What will this do:
```py
for number in [2, 3, 5]:
    print(number)
print(number)
```

* the loop variable could be called anything
* the body of a loop can contain many statements
* use range to iterate over a sequence of numbers

```py
for i in 'hello':
    print(i)
```

```py
for i in range(0,3):
    print(i)
```
	
Let's sum numbers 1 to 10:

```py
total = 0
for number in range(10):
    total = total + (number + 1)   # what's the other way to sum numbers 1 to 10? how about range(1,11)?
print(total)
```

{{< question num=3a >}}
Write a Python code to revert a string, e.g. 'computer' should become 'retupmoc'.
{{< /question >}}

<!-- **Solution 1:** -->
<!-- ```py -->
<!-- n = '' -->
<!-- for i in 'computer': -->
<!--     n = i + n -->
<!-- print(n) -->
<!-- ``` -->
<!-- **Solution 2:** -->
<!-- ```py -->
<!-- a = list('computer') -->
<!-- a.reverse() -->
<!-- ''.join(a)      # convert the list to a string -->
<!-- help(''.join)   # concatenate all strings in the iterable with the separator from the original string -->
<!-- ``` -->
<!-- **Solution 3:** -->
<!-- ```py -->
<!-- 'computer'[::-1] -->
<!-- ``` -->

{{< question num=3b >}}
Print a difference between two lists, e.g. [1, 2, 3, 4] and [1, 2, 5].
{{< /question >}}

{{< question num=3c >}}
Write a script to get the frequency of the elements in the list `a = [77, 9, 23, 67, 73, 21, 23, 9]`. You can google
this problem :)
{{< /question >}}

<!-- **Solution 1:** -->
<!-- ```py -->
<!-- a = [77, 9, 23, 67, 73, 21, 23, 9] -->
<!-- a.count(77)        # prints 1 -->
<!-- a.count(9)         # prints 2 -->
<!-- for i in a: -->
<!--     a.count(i)    # counts the frequency of 'i' in list 'a' -->
<!-- ``` -->
<!-- **Solution 2:** -->
<!-- ```py -->
<!-- a = [77, 9, 23, 67, 73, 21, 23, 9] -->
<!-- for i in set(a): -->
<!--     print(i, "is seen", a.count(i))   # no redundant output -->
<!-- ``` -->
<!-- **Solution 3:** -->
<!-- ```py -->
<!-- a = [77, 9, 23, 67, 73, 21, 23, 9] -->
<!-- import collections -->
<!-- print(collections.Counter(a)) -->

## While loops

Since we talk about loops, we should also briefly mention *while* loops, e.g.

```py
x = 2
while x > 1.:
    x /= 1.1
    print(x)
```

## More on lists in loops

You can also form a *zip* object of tuples from two lists of the same length:

```py
for i, j in zip(a,b):
    print(i,j)
```

And you can create an *enumerate* object from a list:

```py
for i, j in enumerate(b):    # creates a list of tuples with an iterator as the first element
    print(i,j)
```

<!-- **Exercise:** Write a script to sort a list in increasing order by the last element in each tuple, e.g., -->
<!-- input = [(2, 5), (1, 2), (4, 4), (2, 3), (2, 1)] should result in -->
<!-- [(2, 1), (1, 2), (2, 3), (4, 4), (2, 5)]. -->

## List comprehensions

It's a compact way to create new lists based on existing lists/collections. Let's list squares of numbers
from 1 to 10:

```py
[x**2 for x in range(1,11)]
```

Of these, list only odd squares:

```py
[x**2 for x in range(1,11) if x%2==1]
```

You can also use list comprehensions to combine information from two or more lists:

```py
week = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
weekend = ['Sat', 'Sun']
print([day for day in week])                         # the entire week
print([day for day in week if day not in weekend])   # only the weekdays
print([day for day in week if day in weekend])       # in both lists
```

The syntax is:

```py
[something(i) for i in list1 if i [not] in list2 if i [not] in list3 ...]
```

{{< question num=4a >}}
Write a one-line code to sum up the squares of numbers from 1 to 100.
{{< /question >}}

{{< question num=4b >}}
Write a script to build a list of words that are shorter than `n` from a given list of words
`['red', 'green', 'white', 'black', 'pink', 'yellow']`.
{{< /question >}}

## Dictionaries

**Lists** in Python are ordered sets of objects that you access via their position/index. **Dictionaries** are unordered
sets in which the objects are accessed via their keys. In other words, dictionaries are unordered key-value pairs.

```py
favs = {'mary': 'orange', 'john': 'green', 'eric': 'blue'}
favs
favs['john']      # returns 'green'
favs['mary']      # returns 'orange'
list(favs.values()).index('blue')     # will return the index of the first value 'blue'
```

```py
for key in favs:
	print(key)            # will print the names (keys)
	print(favs[key])      # will print the colours (values)
for k in favs.keys():
	print(k, favs[k])     # the same as above
for v in favs.values():
	print(v)              # cycle through the values
for i, j in favs.items():
	print(i,j)            # both the names and the colours
```

Now let's see how to add items to a dictionary:

```py
concepts = {}
concepts['list'] = 'an ordered collection of values'
concepts['dictionary'] = 'a collection of key-value pairs'
concepts
```

Let's modify values:

```py
concepts['list'] = 'simple: ' + concepts['list']
concepts['dictionary'] = 'complex: ' + concepts['dictionary']
concepts
```

Deleting dictionary items:

```py
concepts.pop('list')   # remove the key 'list' and its value
```

Values can also be numerical:

```py
grades = {}
grades['mary'] = 5
grades['john'] = 4.5
grades
```

And so can be the keys:

```py
grades[1] = 2
grades
```

Sorting dictionary items:

```py
favs = {'mary': 'orange', 'john': 'green', 'eric': 'blue', 'jane': 'orange'}
sorted(favs)             # returns the sorted list of keys
sorted(favs.keys())      # the same
for k in sorted(favs):
	print(k, favs[k])         # full dictionary sorted by key
sorted(favs.values())         # returns the sorted list of values
```

{{< question num=4c >}}
Write a script to print the full dictionary sorted by the value.

**Hint**: create a list comprehension looping through all (key,value) pairs and then try sorting the result.
{{< /question >}}

<!-- ```py -->
<!-- sorted([(v,k) for (k,v) in favs.items()])   # notice the order-->
<!-- ``` -->

Similar to list comprehensions, we can form a dictionary comprehension:

```py
{k:'.'*k for k in range(10)}
{k:v*2 for (k,v) in zip(range(10),range(10))}
{j:c for j,c in enumerate('computer')}
```

## Functions

* functions encapsulate complexity so that we can treat it as a single thing
* functions enable re-use: write one time, use many times

First define:

```py
def greeting():
    print('Hello!')
```

and then we can run it:

```py
greeting()
```

```py
def printDate(year, month, day):
    joined = str(year) + '/' + str(month) + '/' + str(day)
    print(joined)
printDate(1871, 3, 19)
```

Every function returns something, even if it's None.

```py
a = printDate(1871, 3, 19)
print(a)
```

How do we actually return a value from a function?

```py
def average(values):   # the argument is a list
    if len(values) == 0:
        return None
    return sum(values) / len(values)
print('average of actual values:', average([1, 3, 4]))
```

Here is an example of a more complex calendar function returning an alphabetical day of the week:

```sh
def dayOfTheWeek(year, month, day):
    import datetime
    week = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
    return week[datetime.datetime(year, month, day).weekday()]
dayOfTheWeek(2022, 11, 10)   # 'Thu'
```





{{< question num=5 >}}
Write a function to convert from Fahrenheit to Celsius, e.g. typing `celsius(77)` would produce 25.
<!-- ```sh -->
<!-- def celsius(f): -->
<!--     return (f-32)*5/9 -->
<!-- ``` -->
{{< /question >}}

{{< question num=6 >}}
Write a function to convert from Celsius to Fahrenheit. Test it with celcius(), e.g. by converting Fahrenheit → Celsius
→ Fahrenheit, or Celsius → Fahrenheit → Celsius.
{{< /question >}}

{{< question num=7 >}}
Now modify celsius() to take a list of Fahrenheit temperatures, e.g., `celcius([70,80,90,100])`, to return a list of
Celsius temperatures.
<!-- ```py -->
<!-- def celsius(fs): -->
<!--     c = [] -->
<!--     for f in fs: -->
<!--         c.append((f-32.)*5./9.) -->
<!--     return c -->
<!-- ``` -->
{{< /question >}}

Function arguments in Python can take default values becoming optional:

```py
def addNumber(a, b=1):
    return a+b
print(addNumber(5))
print(addNumber(5,3))
```

With several optional arguments it is important to be able to differentiate them:

```py
def modify(a, b=1, coef=1):
    return a*coef + b
print(modify(10))
print(modify(10, 1))   # which argument did we add?
print(modify(10, coef=2))
print(modify(10, coef=2, b=5))
```

Any complex python function will have many optional arguments, for example:

```py
?print
```

## Variable scope

The scope of a variable is the part of a program that can see that variable.

```py
a = 5
def adjust(b):
	sum = a + b
    return sum
adjust(10)   # what will be the outcome?
```

* `a` is the global variable &nbsp;⇨&nbsp; visible everywhere
* `b` and `sum` are local variables &nbsp;⇨&nbsp; visible only inside the function

Inside a function we can access methods of global variables:

```py
a = []
def add():
    a.append(5)   # modify global `a`
add()
print(a)          # [5]
```

However, from a local scope we cannot assign to a global variable directly:

```py
a = []
def add():
    a = [1,2,3]   # this will create a local copy of `a` inside the function
    print(a)      # [1,2,3]
add()
print(a)          # []
```

## If we have time

How would you [explain](./solau.md) the following:

```py
1 + 2 == 3              # returns True (makes sense!)
0.1 + 0.2 == 0.3        # returns False -- be aware of this when you use conditionals
abs(0.1+0.2 - 0.3) < 1.e-8   # compare floats for almost equality
import numpy as np
np.isclose(0.1+0.2, 0.3, atol=1e-8)
```

## Libraries

Most of the power of a programming language is in its libraries. This is especially true for Python which is an
interpreted language and is therefore very slow (compared to compiled languages). However, the libraries are often
compiled (can be written in compiled languages such as C/C++) and therefore offer much faster performance than native
Python code.

A library is a collection of functions that can be used by other programs. Python's *standard library* includes many
functions we worked with before (print, int, round, ...) and is included with Python. There are many other additional
modules in the standard library such as math:

```py
print('pi is', pi)
import math
print('pi is', math.pi)
```

You can also import math's items directly:

```py
from math import pi, sin
print('pi is', pi)
sin(pi/6)
cos(pi)
help(math)   # help for libraries works just like help for functions
from math import *
```

You can also create an alias from the library:

```py
import math as m
print m.pi
```

{{< question num=8 >}}
What function from the math library can you use to calculate a square root without using `sqrt`?
{{< /question >}}

{{< question num=9 >}}
You want to select a random character from the string `bases='ACTTGCTTGAC'`. What standard library would you most expect
to help? Which function would you select from that library? Are there alternatives?
{{< /question >}}

{{< question num=10 >}}
A colleague of yours types `help(math)` and gets an error: `NameError: name 'math' is not defined`. What has your
colleague forgotten to do?
{{< /question >}}

{{< question num=11 >}}
Convert the angle 0.3 rad to degrees using the math library.
{{< /question >}}

## Virtual environments and packaging

<!-- Something that comes up often when trying to get people to use python is virtual environments and packaging - it would -->
<!-- be nice if there could be a discussion on this as well. -->

To install a package into the current Python environment from inside a Jupyter notebook, simply do (you will
probably need to restart the kernel before you can use the package):

```sh
%pip install packageName   # e.g. try bson
```

In Python you can create an isolated environment for each project, into which all of its dependencies will be
installed. This could be useful if your several projects have very different sets of dependencies. On the computer
running your Jupyter notebooks, open the terminal and type:

(**Important**: on a cluster you must do this on the login node, not inside the JupyterLab terminal.)

```sh
module load python/3.9.6    # specific to HPC clusters
pip install virtualenv
virtualenv --no-download climate   # create a new virtual environment in your current directory
source climate/bin/activate
which python && which pip
pip install --no-index netcdf4 ...
pip install --no-index ipykernel    # install ipykernel (IPython kernel for Jupyter) into this environment
python -m ipykernel install --user --name=climate --display-name "My climate project"   # add your environment to Jupyter
...
deactivate
```

Quit all your currently running Jupyter notebooks and the Jupyter dashboard. If running on syzygy.ca, logout from your
session and then log back in.

Whether running locally or on syzygy.ca, open the notebook dashboard, and one of the options in `New` below `Python 3`
should be `climate`.

To delete the environment, in the terminal type:

```sh
jupyter kernelspec list                  # `climate` should be one of them
jupyter kernelspec uninstall climate     # remove your environment from Jupyter
/bin/rm -rf climate
```

##  Quick overview of some of the libraries

- `pandas` is a library for working with 2D tables / spreadsheets
- `numpy` is a library for working with large, multi-dimensional arrays, along with a large collection of
  linear algebra functions
  - provides missing uniform collections (arrays) in Python, along with a large number of ways to quickly
    process these collections ⮕ great for speeding up calculations in Python
- `matplotlib` and `plotly` are two plotting packages for Python
- `scikit-image` is a collection of algorithms for image processing
- `xarray` is a library for working with labelled multi-dimensional arrays and datasets in Python
  - "`pandas` for multi-dimensional arrays"
  - great for large scientific datasets; writes into NetCDF files

**Coming up**: 2-part
{{<a "https://training.westdri.ca/events/upcoming-training-winter-spring-2023/#online-courses" "Scientific Python course">}}
on Feb-23, Mar-02 (not part of the Winter HSS Series) will cover most of these libraries.

<!-- {{<a "link" "text">}} -->

## Pandas quick example

<!-- # data from https://domohelp.domo.com/hc/en-us/articles/360043931814-Fun-Sample-DataSets -->

Let's try reading some public-domain data about Jeopardy games with `pandas`:

```py
import pandas as pd
data = pd.read_csv("https://raw.githubusercontent.com/razoumov/publish/master/jeopardy.csv")
data.shape      # 216930 rows, 7 columns
data.head(10)   # first 10 rows
data.columns    # names of the columns
data.loc[data['Category']=='HISTORY'].shape   # 349 matches
data.loc[data['Category']=='HISTORY'].to_csv("history.csv")   # write to a file
```
