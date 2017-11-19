---
layout: post
title:  "Python for Java Programmers - Part 2 - The Nitty Gritty"
subtitle: "Learning Python as a Second Language"
date:   2017-11-19 23:56:45
categories: [Java, Python, Technical, Educational]
---

# Introduction
Hi everyone! This is part two of a series on learning Python when you're already familiar with
Java. If you haven't seen the first part, click [here](https://aryaboudaie.com/java/python/technical/educational/2017/11/13/python-for-java-programmers.html)
to read it, as it will give you a big picture overview of what to expect when learning Python, as well as reasons to learn Python and
a guide to installing and running Python code. I highly recommend giving it just a skim, but I'm biased, as I wrote it.

With the big ideas out of the way, I wanted the second part to just be a quick run through of the details
of each aspect of Python. By the end of this, you should feel fairly comfortable creating your own
Python scripts to do all sorts of fun stuff. There might be some repetition from the first part, but I'd rather be clear than concise (though I'll try to be both).

With that out of the way, let's get started!

# Installing and Running Python Programs

This was discussed in part 1, so if you already have everything installed, sorry for the repetition. You want to first download a distribution of Python online. I recommend the 3.6 version of Anaconda, which is Python plus
a bunch of libraries that are annoying to install. [You can download it from here.](https://www.anaconda.com/download/). If you don't want to download that much stuff, you can also download the vanilla Python from [here](https://www.python.org/downloads/). For either of these, be sure to download the 3.6 version, and when installing, be sure to select the option for adding it to the command line. It's been a while since I installed either of these, so please [email me](mailto:arya@aryaboudaie.com) if you have any questions.  

Once you have it installed, you should be able to open up the Command Prompt (on Windows), or the Terminal (on Mac or Linux), and when it pops up, type `python3` for Mac, or `python` for windows, and hit enter. I'll refer to the command as `python3` for now, and I'll be talking about the Terminal, though Windows users should know to type `python` and to use Command Prompt.

If you see something like this after typing `python3` and hitting enter, it means that Python has been installed:

```
Python 3.6.0 (v3.6.0:41df79263a11, Dec 23 2016, 07:18:10) [MSC v.1900 32 bit (Intel)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

When you typed `python3`, you entered the Python REPL. The REPL allows you to type code line by line, and see the
results of each line printed. It's a great way to prototype some code before actually committing it to your program.

Those three `>>>` symbols are urging you to type some Python code. So type `print("Hello World")` into the terminal, and see it print the famous first program.

{% highlight python %}
>>> print("Hello World")
Hello World
{% endhighlight %}

If you want to write an entire python program out and then run it, you can create it with your favorite text editor (I like [Atom](atom.io)) and save it with a `.py` extension. Then open the terminal, CD to the folder with that file, and then type `python3 filename.py` - it should run the file, and print any contents to the terminal. If you'd like to run the program and then have it enter a REPL, you can type `python3 -i filename.py`. Note that unlike Java, there is no compiling step, you just run the program, and the interpreter runs the program line by line.

If you'd rather do all of this remotely, you can do it on [www.repl.it](http://repl.it). Just create an account, open a new python3 workspace, and on the left hand side you'll have a text editor, and on the right hand side you'll have the REPL. I love this website a lot, and can't recommend it more highly.

If you want to use an IDE, the creators of IntelliJ also made one called [Pycharm](https://www.jetbrains.com/pycharm/), it is great and also free! There is also a professional edition that is free if you're a student. If you like the extra tools an IDE gives you, you should give it a shot!

# Basic Numbers and Operators

In Python, you have the same basic types as Java, though there isn't really the difference between "primitive" and "non-primitive" types that Java has. For your numbers, you have ints, which are basically the same as Java, and floats, which are the same as doubles in Java.

{% highlight python %}
2 # an integer
3.04 # a float
{% endhighlight %}

Also note - to comment in Python, you use the `#` sign.

You also have the same operators as Java, though with one extra helpful addition, the `**` operator (which raises one number to another). No need for Math.pow() anymore! Additionally with division,  unlike Java, if you divide two ints, you can get a float back. If you want to do integer division, you can use the `//` operator. Here they all are:

{% highlight python %}
print(5+2) # addition
print(5-2) # subtraction
print(5*2) # multiplication
print(5/2) # normal division: 2.5
print(5//2) # integer division: 2
print(5**2) # 2 to the power of 3
{% endhighlight %}

# Storing variables:

To store a variable in Python, you don't need to specify any types. Just name it well, and put an equal sign after the name.

{% highlight python %}
x = 4
y = 100.5
print(y/x)
{% endhighlight %}

There's also a pretty neat trick to swap variables (no more temp variable needed):

{% highlight python %}
x, y = y, x # swaps x and y
{% endhighlight %}

# Booleans

Just like Java, Python has the two basic boolean types, True and False. However, in Python, they are capitalized. You can derive them in mostly the same ways as Java.

{% highlight python %}
x = 2
y = 3
z = 3

print(x==y) # False (Equals)
print(x!=y) # True (Not Equals)
print(x>y) # False (Greater Than)
print(z>=y) # True (Greater Than or Equal To)
print(x<y) # True (Less Than)
print(z<=y) # False (Less Than or Equal To)
{% endhighlight %}

There are also the same logical operators as Java, though they're mostly spelled out in English, for ease of readability.

{% highlight python %}
print(True or False) # True (|| in Java)
print(True and False) # False (&& in Java)
print(not True) # False (! in Java)
{% endhighlight %}

# If Statements

The wording of `if` statements is mostly the same as Java, the only difference is that `else if` is spelled `elif` in order to have its own keyword. In terms of structure, there are no parentheses needed around the keywords, cleaning them up. Additionally, all the code for each block is just indented under the statement. Look for example at this code, which assigns a ticket price based on how fast you're going:

{% highlight python %}
speed = 50
if speed<60:
  ticket_price = 0
elif speed<60:
  ticket_price = 50
elif speed<70:
  ticket_price = 100
else:
  ticket_price = 300

print(ticket_price)
{% endhighlight %}

Try changing the value of speed, and see if the code does what you think it will:

<iframe height="400px" width="100%" src="https://repl.it/@misingnoglic/SpeedTicketIfElse?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals" width="100%" ></iframe>

The way that the `if` statements work is that if the thing in the `if` is true, it will execute all the code indented under the line with the if statement. This is a departure from Java, which uses curly braces to contain pieces of code. If this doesn't make sense, PLEASE read the part 1 to this. Thank you :)

If your if statement is only one line, you can also put it all on one line, like this:

{% highlight python %}
if x<10: print("x is less than 10")
else: print("x is not less than 10")
{% endhighlight %}

Some people prefer this style when writing short if statements, others prefer always having it always be indented on the next line. It's really a matter of preference, just make sure you have some consistency.

If statements can also be nested in other if statements - they just need to be indented inside the if statement they're nested in. I'm not saying this is the best way to write code, I'm just saying it is possible.

{% highlight python %}
if x<0:
  if y<0: print("both x and y are negative")
  else: print("only x is negative")
else:
  print("x is not negative")
{% endhighlight %}

In all, booleans and if/else statements are fairly similar between Java and Python, so your skills should transfer fairly easily!

# Functions

As discussed in part 1, functions are to Python what static methods are to Java. The main great thing about functions is that they do not need to be attached to a specific class. They can be defined anywhere in your program, and then called anywhere after the definition. You also don't need to announce any types. Here is an example of a few functions, just to jog your memory:

{% highlight python %}
def add(x, y):
  return x+y

x = add(2,3)
print(x) # 5

def print_name(name):
  print("Hello "+name)

print_name("Arya") # Hello Arya


{% endhighlight %}

Functions are defined with the `def` keyword - after writing def, you write the name of the function, and then in parentheses you put the parameters, and then add a colon. Just like if statements, everything indented under the first line is part of the function. Just like Java, functions end when you `return` some variable (which gets passed back to whatever called the function), or when you reach the end of the function and nothing is returned (like a `void` method in Java).

Just like `if` statements, if your function is only one line, you can define it all on the same line.

{% highlight python %}
def f(x): return x**2
print(f(10)) # 100
{% endhighlight %}

Also mentioned in the Part 1 was the "default" parameters of the function. These let you set a default for a parameter should you not pass it, and lets you write less code. The syntax is as following:

{% highlight python %}
def print_hello(name, uppercase=False): # caps is the default argument, if it isn't passed, it's set to False
  if uppercase:
    print("HELLO "+name.upper())
  else:
    print("hello "+name)

print("Arya", True) # HELLO Arya
print("christa") # hello christa (Nothing passed for 2nd argument)
print("snow", False) # hello snow
{% endhighlight %}

Just make sure that your parameters with defaults are listed after the ones with no defaults (you can think about why that's needed).

When calling functions, instead of just putting them in order, you can also name the parameters explicitly, like this:

{% highlight python %}
def pow(base, exponent):
  return base**exponent

x = pow(base=2, exponent=3)
print(x) # 8
{% endhighlight %}

This is helpful when you're writing code and don't want people to have to remember what the arguments to the functions are when it's called. By naming them explicitly, you also don't have to have them in the right order (though your code will be nicer if they are!). The common style is to not name the arguments that are necessary, and name the arguments that have defaults.

{% highlight python %}
# Score function for some game
def score(points, seconds, multiplier=1):
  return (points/seconds)*multiplier

x = score(100, 10, multiplier=3)
print(x)
{% endhighlight %}

In the end, you have to use your best judgement for naming arguments - deciding the fine line between being too verbose and being helpful. We don't want this to turn into Java.

The other thing to know about functions is that they are `first class objects`. This means that they are treated the same way as any other type, and you can do the same things to them. For example, you can assign a variable to a function.

{% highlight python %}
def f(x): return x**2 # x squared
g = f # g is now a variable for f
print(g(10)) # 100
{% endhighlight %}

You can also write functions that accept other functions as parameters. This is useful, for example, when using the `sorted` function, which returns a sorted list. One of its optional parameters is `key`, which is the function used to compare the different items. If left blank, it just sorts them from smallest to largest, but if you apply a `key` function, it will sort it according to that key. Let's say for example, you want to sort a list of numbers by their absolute value. You can do this:

{% highlight python %}
L = [1, 3, 4, -1, 12, 7, -5, 6]
L2 = sorted(L)
print(L2) # [-5, -1, 1, 3, 4, 6, 7, 12]
L3 = sorted(L, key=abs) # using the key abs(), which returns the absolute value of a number
print(L3) # [1, -1, 3, 4, -5, 6, 7, 12]
{% endhighlight %}

Another example: If we want to sort a list of strings, but sorted by the second letter, we can do something like this:

{% highlight python %}

def weirdsort(s):
  return s[1] # returns the second character

L = ["hello", "my", "name", "is", "arya"]
print(sorted(L)) # ['arya', 'hello', 'is', 'my', 'name']
print(sorted(L, key=weirdsort)) # ['name', 'hello', 'arya', 'is', 'my']
{% endhighlight %}

## Documenting your functions.

If you want to be a good coder, and make sure people know what your code is doing, you have to comment your code! In Java, you might have written a Javadoc comment on top of every method you wrote, so that if you produced documentation, those comments would be there to explain what your method does.

In Python, the standard is to have a multi-line string directly under the function header, that explains what the function does, and what parameters it takes. The way you make a multi-line string is by starting with three quotes, and then ending it with three quotes. Here is an example:

{% highlight python %}
def power(base, exponent):
  """
  returns 'base' to the power of 'exponent'
  in other words: base^exponent
  """
  return base**exponent
{% endhighlight %}

This doesn't do anything to the utility of the function, but it means whoever is reading your code knows what it does. Additionally, if someone was using your code and wanted to know what `power` does without having to read your code, they could call the built in `help` function, which prints out this `docstring` that you wrote, as such:

```
>>> help(power)
Help on function power in module __main__:

power(base, exponent)
    returns 'base' to the power of 'exponent'
    in other words: base^exponent
```

# Lists

We talked about lists in part 1, but I figured I'd go more in depth. To remind you, a list is a collection of any sort of objects.

{% highlight python %}
# Note how there can be ints and floats in the same list
grades = [90, 40, 80.5, 100]
names = ["Arya", "Joe", "Christa", "Snow"]
{% endhighlight %}

You can access and modify elements of a list with the same syntax as Java - using zero indexing.

{% highlight python %}
L = [40, 50, 60, 70, 80]
x = L[0] # x = 40
y = L[2] # x = 60
L[3] = 100 # L = [40,50,60,100,80]
{% endhighlight %}

Python also supports negative indexing, which allows you to index starting from the back of a list, with -1 being the last item, -2 being the second to last, etc...

{% highlight python %}
L = [40, 50, 60, 70, 80]
x = L[-1] # 80
y = L[-3] # 60
{% endhighlight %}

## Getting sections of lists

To get a section of a list, Python has this feature called "slicing," which effectively lets you get a "slice" of a list. The syntax is as follows:

{% highlight python %}
L = [40, 50, 60, 70, 80, 90, 100]
s = L[start:stop]
{% endhighlight %}

To get a slice of a list, you put the two parameters in square braces (same as getting one item), except you would put up to three values separated by colons. The first, `start` is the index you want to start at, and `stop` is the index you want to stop at, and not include. For example, L[1:4] will give you from index 1 up to index 4.

{% highlight python %}
L = [40, 50, 60, 70, 80, 90, 100]
s = L[1:4] # s = [50,60,70]
{% endhighlight %}

Negative indexing is also supported here. Let's say you want to go from the first to the last item. You can do something like this:

{% highlight python %}
L = [40, 50, 60, 70, 80, 90, 100]
s = L[1:-1] # s = [50,60,70, 80, 90]
{% endhighlight %}

Python also supports a shorthand for these slices, where you can leave one of the sides of the colon empty. If you leave the left side empty, it will start at the beginning, and if you leave the right side empty, it will go until the end.

{% highlight python %}
L = [5, 10, 15, 20, 25, 30]
s = L[:3] # same as L[0:3]
s = L[3:] # from index 3 until the end
s = L[:] # from the beginning to the end
{% endhighlight %}

Slicing also supports a third argument, the skip.

{% highlight python %}
L = [5, 10, 15, 20, 25, 30, 35, 40, 45, 50]
s = L[1:6:2]
print(s) # [10, 20, 30] - every other number in indexes 1 to 6
s = L[::3] # [5, 20, 35, 50] # every third number in the whole list
{% endhighlight %}

The skip gives you how many numbers it goes forward after each item in the slice. If your skip is 2, it gives you every 2nd number in that range. If the skip is 3, you'll get every third number, etc... If you leave the other two numbers blank but include a skip, you can get just the skip, while still including every item in the list. Use this repl.it frame to play with slicing, and try out whatever questions might be on your mind!

<iframe height="400px" width="100%" src="https://repl.it/@misingnoglic/List-Slicing-Examples?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals" width="100%" ></iframe>

Note that slicing creates a new list. If you modify a slice, the original list remains the same.

## Methods Mutating Lists

There are a few methods on lists that modify the list in place, without creating a new list. You can call these like Java methods, by doing listname.method(). You can see the methods below:

{% highlight python %}
grades = [90, 40, 80.5, 100]
grades.append(95) # Adds 95 to the end of the list
grades.extend([70,80,90]) # Adds 70,80,and 90 to the end of the list
grades.insert(1, 105) # inserts 105 into index 1
x = grades.pop() # "pops" the last item off the list, and returns it.
y = grades.pop(1) # "pops" the item at index 1
grades.remove(100) # removes the first instance of 100 from the lists
grades.reverse() # reverses the list
grades.sort() # sorts the list smallest to largest (can accept a key argument, like sorted)
grades.sort(reverse=True) # sorts list largest to smallest
grades.clear() # Empties the list

{% endhighlight %}
Notice how most of them don't return anything, except pop. I've included a pythontutor embed here, so you can see how each method affects the list. Click the "Forward" and "Backward" buttons to see how each call affects the list. You don't have to memorize these, but it's good to know what tools you have available to you!

<iframe width="800" height="500" frameborder="0" src="http://pythontutor.com/iframe-embed.html#code=grades%20%3D%20%5B90,%2040,%2080.5,%20100%5D%0Agrades.append%2895%29%20%23%20Adds%2095%20to%20the%20end%20of%20the%20list%0Agrades.extend%28%5B70,80,90%5D%29%20%23%20Adds%2070,80,and%2090%20to%20the%20end%20of%20the%20list%0Agrades.insert%281,%20105%29%20%23%20inserts%20105%20into%20index%201%0Ax%20%3D%20grades.pop%28%29%20%23%20%22pops%22%20the%20last%20item%20off%20the%20list,%20and%20returns%20it.%0Ay%20%3D%20grades.pop%281%29%20%23%20%22pops%22%20the%20item%20at%20index%201%0Agrades.remove%28100%29%20%23%20removes%20the%20first%20instance%20of%20100%20from%20the%20lists%0Agrades.reverse%28%29%20%23%20reverses%20the%20list%0Agrades.sort%28%29%20%23%20sorts%20the%20list%20%28can%20accept%20a%20key%20argument,%20like%20sorted%29%0Agrades.sort%28reverse%3DTrue%29%20%23%20sorts%20list%20largest%20to%20smallest%0Agrades.clear%28%29%20%23%20Empties%20the%20list&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=false&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

## Note about lists - "Pass By Name"

tl;dr: Read [this](https://nedbatchelder.com/text/names.html) post.

In Java, you had the idea of pass by reference vs pass by value. Any primitive types will be passed by value into methods, while any objects or arrays will be passed by reference. This means that if you passed an array.

{% highlight java %}
int x = 2;
int y = x;
x++; // y is still equal to two.
{% endhighlight %}

{% highlight java %}
int[] arr1 = {1,2,3};
int[] arr2 = arr1;
arr1[0] = 40; //arr2 is now modified.
{% endhighlight %}

In Python, this same idea does not work, as there are no "primitive" types under the hood. Everything in Python is an object, so you need to learn about a new idea - pass by name. I will explain it in a quick way, but for a more thorough idea of how values are passed in Python, read [this](https://nedbatchelder.com/text/names.html) blogpost by Ned Batchelder, which will explain very clearly how values are passed.

In Python, if you set one variable equal to another variable, they will both point to the same "item" in the computer's memory. This is not normally a problem for things like ints or strings, because they can't be mutated (there's no ++ in Python), so it effectively works like Java's pass by value.

However, if you pass

{% highlight python %}
x = 12
y = x # y is now pointing to the same thing as x
x = y + 1 # x is pointing to a new number 13

def f(x):
  x+=1 # remember x+=1 is shorthand for x = x+1, so a reassignment

f(x)
print(x) # still 13
{% endhighlight %}

See how this works out line by line:
<iframe width="800" height="500" frameborder="0" src="http://pythontutor.com/iframe-embed.html#code=x%20%3D%2012%0Ay%20%3D%20x%20%23%20y%20is%20now%20pointing%20to%20the%20same%20thing%20as%20x%0Ax%20%3D%20y%20%2B%201%20%23%20x%20is%20pointing%20to%20a%20new%20number%2013%0A%0Adef%20f%28x%29%3A%0A%20%20x%2B%3D1%20%23%20remember%20x%2B%3D1%20is%20shorthand%20for%20x%20%3D%20x%2B1,%20so%20a%20reassignment%0A%20%20%0Af%28x%29%0Aprint%28x%29%20%23%20still%2013&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=9&heapPrimitives=true&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

However for lists, you can easily modify them - by changing one of their indexes, appending to it, removing an item, etc. When you set one list equal to another, they are both pointing at the same object, so any mutations you do to one will change the other. Additionally, passing the list into a function will cause the variable to point to the same object outside the function as well.

{% highlight python %}
L1 = [1,2,3]
L2 = L
L2[0] = 40
print(L1) # [40,2,3]
L1.append(10)
print(L2) # [40,2,3,10]

def f(L):
  L.append(4)
  return sum(L)

f(L)
print(L1)
print(L2)
{% endhighlight %}

<iframe width="800" height="500" frameborder="0" src="http://pythontutor.com/iframe-embed.html#code=L1%20%3D%20%5B1,2,3%5D%0AL2%20%3D%20L1%0AL2%5B0%5D%20%3D%2040%0Aprint%28L1%29%20%23%20%5B40,2,3%5D%0AL1.append%2810%29%0Aprint%28L2%29%20%23%20%5B40,2,3,10%5D%0A%0Adef%20f%28L%29%3A%0A%20%20L.append%284%29%0A%20%20return%20sum%28L%29%0A%0As%20%3D%20f%28L1%29%0Aprint%28L1%29%0Aprint%28L2%29%0A&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=14&heapPrimitives=false&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

The exception to this is when you create a new list - either by adding two lists, or by getting a slice of a list. Look at where the arrows point here:

{% highlight python %}
L1 = [1,2,3]
L2 = L1 + [4,5,6]
L2[1] = 20
print(L1) # [1,2,3]
print(L2) # [1,20,3,4,5,6]

L3 = L2[1:4] # L2 from index 1 to 4
L3[1] = 50
print(L2) # [1, 20, 3, 4, 5, 6]
print(L3) # [20, 50, 4]
{% endhighlight %}

<iframe width="800" height="500" frameborder="0" src="http://pythontutor.com/iframe-embed.html#code=L1%20%3D%20%5B1,2,3%5D%0AL2%20%3D%20L1%20%2B%20%5B4,5,6%5D%0AL2%5B1%5D%20%3D%2020%0Aprint%28L1%29%20%23%20%5B1,2,3%5D%0Aprint%28L2%29%20%23%20%5B1,20,3,4,5,6%5D%0A%0AL3%20%3D%20L2%5B1%3A4%5D%0AL3%5B1%5D%20%3D%2050%0Aprint%28L2%29%20%23%20%5B1,%2020,%203,%204,%205,%206%5D%0Aprint%28L3%29%20%23%20%5B20,%2050,%204%5D%0A&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=9&heapPrimitives=false&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

So the key idea here is to know - if you want to make a copy of a list then mutate it (by calling basically any method on it that changes it), don't just create a new variable like you would do with an int or boolean. Instead, you can use the .copy() method to create a copy of the list, or you can use a special slicing trick, shown below:

{% highlight python %}
L = [1,2,3]
L2 = L.copy()
L3 = L[:] # Makes a copy
{% endhighlight %}


## Other List Methods

There are a few other methods that return information about lists. I'll include a few here:

{% highlight python %}
names = ["Arya", "Joe", "Snow", "Christa", "Snow"]
names2 = names.copy() # returns a copy of the list, that you can modify without affecting the original.
ct = names.count("Snow") # Counts number of times "Snow" is in the list.
idx = names.index("Christa") # Gives the first index of "Christa" in the list.
{% endhighlight %}



# Built In Functions

Python has a ton of built in functions - accessible without even having to import anything (which we'll talk about later). I'll go my favorites, just so you have an idea of the tools you have at your disposal. Just so you know though, if you ever need to know what a function does, you can always use the `help` function that was discussed in the last section. All of them are also documented on the [official Python website here](https://docs.python.org/3/library/functions.html).

# abs
As discussed before, `abs(x)` returns the absolute value of x. Fairly straightforward

{% highlight python %}
print(abs(10)) # 10
print(abs(-10)) # 10
{% endhighlight %}
