---
layout: post
title:  "Python for Java Programmers - Part 2 - The Nitty Gritty"
subtitle: "Variables, Types, If Statements, and Functions"
date:   2018-09-16 23:10:00
categories: [Java, Python, Technical, Educational]
---

# Table of Contents

* TOC
{:toc}

# Introduction

**Note: If you haven't read part 1, please do so [here](https://aryaboudaie.com/java/python/technical/educational/2017/11/13/python-for-java-programmers.html). If it's been a while (I did write it last year), just give it a quick skim!**

Hi everyone! This is part two of a series on learning Python when you're already familiar with
Java. If you haven't seen the first part, click [here](https://aryaboudaie.com/java/python/technical/educational/2017/11/13/python-for-java-programmers.html)
to read it, as it will give you a big picture overview of what to expect when learning Python, as well as reasons to learn Python and a guide to installing and running Python code. I highly recommend reading it first, so you can have all the high level ideas about the differences between Python and Java, but I'm biased as I wrote it. Sorry about taking so long to write this new version - it turns out that jobs at tech companies are hard, and I didn't have much free time outside of work to build this blog up more.

With the big ideas out of the way, I wanted the next parts to just be a quick run through of the details
of each aspect of Python, while pointing out any "gotchas" that could trip up people going from Java to Python. There might be some repetition from the first part, but I'd rather be clear than concise (though I'll try to be both). Plus, it's good to see things more than once, to get you to remember better. And because this post assumes you already understand Java, I'll try not to over-explain some of the things that should carry over between the two languages. If anything is confusing, you can always leave a comment!

With that out of the way, let's get started!

# Installing and Running Python Programs

This was discussed in part 1, so if you already have everything installed, sorry for the repetition. You want to first download a distribution of Python online. I recommend the 3.7 version of Miniconda, which is Python plus a bunch of libraries that are annoying to install. [You can download it from here.](https://conda.io/miniconda.html) If you don't want to download that much stuff, you can also download the vanilla Python from [here](https://www.python.org/downloads/). For either of these, be sure to download the 3.7 version, and when installing, be sure to select the option for adding it to the command line. It's been a while since I installed either of these, so please [email me](mailto:arya@aryaboudaie.com) if you have any questions.

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

If you want to write an entire python program out and then run it, you can create it with your favorite text editor (I like [Atom](https://www.atom.io)) and save it with a `.py` extension. Then open the terminal, CD to the folder with that file, and then type `python3 filename.py` - it should run the file, and print any contents to the terminal. If you'd like to run the program and then have it enter a REPL, you can type `python3 -i filename.py`. Note that unlike Java, there is no compiling step, you just run the program, and the interpreter runs the program line by line.  

If the last paragraph didn't make sense, or if you'd rather do all of this remotely, you can do it on [www.repl.it](http://repl.it). Just create an account, open a new python3 workspace, and on the left hand side you'll have a text editor, and on the right hand side you'll have the REPL. I love this website a **ton**, and can't recommend it more highly. I'll also be adding snippets from the www.repl.it website that you can run directly on this website, just like my last post.

![Image of www.repl.it website](https://i.imgur.com/xggILvd.png)

If you're advanced and want to use an IDE, the creators of IntelliJ also made one called [Pycharm](https://www.jetbrains.com/pycharm/), it is great and also free! There is also a professional edition that is free if you're a student. If you like the extra tools an IDE gives you, you should give it a shot! It's a little annoying to setup, but if you're sufficiently motivated you should be able to get it running. Just be sure to install Python first. With that out of the way, let's start our deep dive!

# Storing Variables

To store a variable in Python, you don't need to specify any types. Just name it well, and put an equal sign after the name.

{% highlight python %}
x = 4
y = 100.5
print(y/x)
{% endhighlight %}

<iframe height="400px" width="100%" src="https://repl.it/@misingnoglic/Simple-Variable-Example?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

In Java, you name variables with camelCase when it has multiple words. With Python, we use "snake_case," which separates the words by underscores, and where all the letters are lowercase. The same convention is used for function names.

{% highlight python %}
num_pizzas = 5
{% endhighlight %}

There's also a pretty neat trick to swap variables (no more temp variable needed):

{% highlight python %}
x = 3
y = 4
x, y = y, x # swaps x and y
print(x)  # 4
{% endhighlight %}

<iframe height="400px" width="100%" src="https://repl.it/@misingnoglic/Variable-Swap-Example?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

Variables are fairly straightforward, but they can get more nuanced. I'll return to more ideas about variables in the section on functions.

# Basic Types and Operators

In Python, you have the same basic types as Java, though there isn't really the difference between "primitive" and "non-primitive" types that Java has. For your numbers, you have ints, which are basically the same as Java, and floats, which are the same as doubles in Java.

{% highlight python %}
x = 2  # an integer
y = 3.04  # a float
{% endhighlight %}

Also note - to comment in Python, you use the `#` sign. You can also have a multiline comment by putting it triple quotes, like this:

{% highlight python %}
"""
This is a long comment that can span
multiple lines. It's technically just
a string that is not stored to any variable.
"""
x = 2
{% endhighlight %}

{% highlight python %}
x = 2  # an integer
y = 3.04  # a float
{% endhighlight %}

You also have the same operators as Java, though with one extra helpful addition - the `**` operator which raises one number to another. No need for Math.pow() anymore! Additionally with division,  unlike Java, if you divide two ints, you can get a float back. If you want to do integer division, you can use the `//` operator. Here they all are:

{% highlight python %}
print(5+2)  # addition
print(5-2)  # subtraction
print(5*2)  # multiplication
print(5/2)  # normal division: 2.5
print(5//2)  # integer division: 2
print(5**2)  # 2 to the power of 3
{% endhighlight %}

Note: In the old version of Python, the division was integer division, just like in Java. If you're forced to use Python 2, you can get the new division by putting this statement at the top of your program:

{% highlight python %}
from __future__ import division
{% endhighlight %}

You can convert values to different types by using the different casting functions that are built in. Here's some examples (sorry for my boring names) - try messing around with it and seeing what happens:

{% highlight python %}
a = 100
b = float(a)  # Turns b into the decimal version of a
print(b)  # 100.0
c = 200.5
d = int(c)
print d  # 200
e = str(d)  # Turns e into the string version of d
print(e)  # '200'
print(e[0])  # '2'
f = "150.6"
g = float(f)
print(g + 100)  # 250.6
h = "200"
print(int(h)+100)  # 300
{% endhighlight %}

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=a%20%3D%20100%0Ab%20%3D%20float%28a%29%20%20%23%20Turns%20b%20into%20the%20decimal%20version%20of%20a%0Aprint%28b%29%20%20%23%20100.0%0Ac%20%3D%20200.5%0Ad%20%3D%20int%28c%29%0Aprint%28d%29%20%20%23%20200%0Ae%20%3D%20str%28d%29%20%20%23%20Turns%20e%20into%20the%20string%20version%20of%20d%0Aprint%28e%29%20%20%23%20'200'%0Aprint%28e%5B0%5D%29%20%20%23%20'2'%0Af%20%3D%20%22150.6%22%0Ag%20%3D%20float%28f%29%0Aprint%28g%20%2B%20100%29%20%20%23%20250.6%0Ah%20%3D%20%22200%22%0Aprint%28int%28h%29%2B100%29%20%20%23%20300&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

# Booleans

Just like Java, Python has the two basic boolean types, True and False. However, in Python, they are capitalized. You can derive them in mostly the same ways as Java.

{% highlight python %}
x = 2
y = 3
z = 3

print(x==y)  # False (Equals)
print(x!=y)  # True (Not Equals)
print(x>y)  # False (Greater Than)
print(z>=y)  # True (Greater Than or Equal To)
print(x<y)  # True (Less Than)
print(z<=y)  # False (Less Than or Equal To)
{% endhighlight %}

There are also the same logical operators as Java, though they're mostly spelled out in English, for ease of readability.

{% highlight python %}
print(True or False)  # True (|| in Java)
print(True and False)  # False (&& in Java)
print(not True)  # False (! in Java)
{% endhighlight %}

# If Statements

The wording of `if` statements is mostly the same as Java, the only difference is that `else if` is spelled `elif` in order to have its own keyword. In terms of structure, there are no parentheses needed around the keywords, cleaning up how they look (though you can still add them if you want). Additionally, all the code for each block is just indented under the statement. Look for example at this code, which assigns a ticket price based on how fast you're going:

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

The way that the `if` statements work is that if the thing in the `if` is true, it will execute all the code indented under the line with the if statement. This is a departure from Java, which uses curly braces to contain pieces of code. If this doesn't make sense, PLEASE read the part 1 to this.

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

## Truthy values in if statements.

You can also pass values that aren't booleans into `if` statements. Most values will act as True, except for the following values:

{% highlight python %}
0
0.0
False  # Obviously.
[]  # Empty list.
{}  # Empty dictionary.
None  # The "nothing" value (will explain later).
{% endhighlight %}

This allows for more clear code in certain cases. For example, if you want to do something special if a list is empty, instead of doing:

{% highlight python %}
if len(nums)==0:
  # do something special
{% endhighlight %}

You can just do:

{% highlight python %}
if not nums:
  # do something special
{% endhighlight %}

This may look weird now, but eventually you'll appreciate the fact that there's less code to read and write with this special syntax.

# Functions

As discussed in Part 1, functions are to Python what static methods are to Java. The great thing about functions is that they do not need to be attached to a specific class. They can be defined anywhere in your program, and then called anywhere after the definition. You also don't need to announce any types of inputs or return outputs. Here is an example of a few functions, just to jog your memory:

{% highlight python %}
def add(x, y):
  return x+y

x = add(2,3)
print(x)  # 5

def print_name(name):
  print("Hello "+name)

x = add(5, 10)

print_name("Arya") # Hello Arya


{% endhighlight %}

Functions are defined with the `def` keyword - after writing def, you write the name of the function, and then in parentheses you put the parameters, and then add a colon. Just like if statements, everything indented under the first line is part of the function. Just like Java, functions end when you `return` some variable (which gets passed back to whatever called the function), or when you reach the end of the function and nothing is returned (like a `void` method in Java).

Just like `if` statements, if your function is only one line, you can define it all on the same line.

{% highlight python %}
def f(x): return x**2
print(f(10))  # 100
{% endhighlight %}

## None value in functions

If you have a function that doesn't return anything, it will technically return the value `None`. `None` is a special value in Python, and it literally just means "nothing."

{% highlight python %}
def hello(name):
  print("Hello "+name)  # Nothing is returned

x = hello("Arya")
print(x)
{% endhighlight %}

<iframe height="400px" width="100%" src="https://repl.it/@misingnoglic/Function-Return-None-Example?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

When you run this, you'll see the following output:

{% highlight python %}
Hello Arya
None
{% endhighlight %}

This is because when you run the line `x = hello("Arya")`, the function `hello` will run, which prints out `Hello Arya`. Then the return value of this function, which is `None` (because we didn't return anything) gets stored to `x`. Then, when you print x, it prints None. In Java, you would get some kind of error here, but with Python you have to watch out yourself. This is particularly insidious in situations like this:

{% highlight python %}
def is_even(x):
  if x%2==1:
    return False

if is_even(2):
  print("two is even!")
else:
  print("two is odd!")
{% endhighlight %}

<iframe height="400px" width="100%" src="https://repl.it/@misingnoglic/Python-Function-Return-None-2?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

Why doesn't this work? Try adding print statements to understand the issue, and modifying the code to fix it.

## Default Function Parameters

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

<iframe height="400px" width="100%" src="https://repl.it/@misingnoglic/Default-Parameter-Example?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

Just make sure that your parameters with defaults are listed after the ones with no defaults (you can think about why that's needed). Python doesn't have overloading like Java does, but using default variables can remove a lot of the use cases for overloading.

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

<iframe height="400px" width="100%" src="https://repl.it/@misingnoglic/Default-Parameter-Example-2?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

In the end, you have to use your best judgement for naming arguments - deciding the fine line between being too verbose and being helpful. We don't want this to turn into Java.

The other thing to know about functions is that they are `first class objects`. This means that they are treated the same way as any other type, and you can do the same things to them. For example, you can assign a variable to a function.

{% highlight python %}
def f(x): return x**2  # x squared
g = f  # g is now a variable for f
print(g(10))  # 100
{% endhighlight %}

You can also write functions that accept other functions as parameters. This is useful, for example, when using the `sorted` function, which returns a sorted list. One of its optional parameters is `key`, which is the function used to compare the different items. If left blank, it just sorts them from smallest to largest, but if you apply a `key` function, it will sort it according to that key. Let's say for example, you want to sort a list of numbers by their absolute value. You can do this:

{% highlight python %}
L = [1, 3, 4, -1, 12, 7, -5, 6]
L2 = sorted(L)
print(L2)  # [-5, -1, 1, 3, 4, 6, 7, 12]
L3 = sorted(L, key=abs)  # using the key abs(), which returns the absolute value of a number
print(L3)  # [1, -1, 3, 4, -5, 6, 7, 12]
{% endhighlight %}

Now L3 is sorted based on the absolute value, so -5 is between 4 and 6. This is useful when you're sorting lists of objects, and need a way to compare each object.

You can even write your own functions that accept functions as arguments. Of course if this is all too confusing for now, you don't have to use any of these new features you're learning. It's just good to know what you can use if you ever want to go back to look it up.

## Documenting Functions.

Just as a quick note, Python has a standard way to document functions, called a `docstring`. The docstring is just a string that's listed under the function definition that explains what the function does, and any other nuances about the function. Here is an example, using the score method I defined previously:
{% highlight python %}
def score(points, seconds, multiplier=1):
  '''
  Calculates the total end score of the player when
  the game ends. Divides the number of points earned
  by the number of seconds it took them to complete
  the level. It also accepts a parameter multiplier,
  which is the end multiplier of the score.
  '''
  return (points/seconds)*multiplier
{% endhighlight %}

Notice how much clear my design becomes with the docstring. It's good practice to give your functions docstrings, so that anyone reading your code will know what your function does. It's also looks SUPER impressive, trust me.

## Variable Scope

When you call a function and pass in parameters, the name of the parameters exist inside of the function, and only inside of the function. If you try to call them outside of the function, you will get an error.

{% highlight python %}
def f(x, y, z):
  return x+y+z

# Inside of f, this will create three variables
# x = 1, y = 2, z = 3
print(f(1, 2, 3))  
print(x)  # Error, x does not exist in this scope.
{% endhighlight %}

Additionally, if you have variables with similar names inside of and outside of a function, their value depends on the scope that you're in. For example:

{% highlight python %}
x = 10
y = 20
def f(x):
  y = x+2
  return y+2

z = f(y)
print(x)  # Still 10
print(y)  # Still 20
{% endhighlight %}

Try to follow the pythontutor step by step for this, and try to see where everything is passed. But the basic idea is that the x and y variables inside of `f` have nothing to do with the variables outside of `f`. When you pass `y` into `f`, it's called `x` inside of `f`, and that `x` has nothing to do with the `x` outside of `f`.

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=x%20%3D%2010%0Ay%20%3D%2020%0Adef%20f%28x%29%3A%0A%20%20%20%20y%20%3D%20x%20%2B%202%0A%20%20%20%20return%20y%2B2%0A%0Az%20%3D%20f%28y%29%0Aprint%28x%29%20%20%23%20Still%2010%0Aprint%28y%29%20%20%23%20Still%2020&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=true&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

This is similar to Java, but I wanted to bring it up now, because of the next point, which is not at all similar to Java.

## Pass by Name

In Java, you may have learned that some variables are "pass by value", and others are "pass by reference." This does not hold true in Python, and is one of the main reasons that Java programmers think that Python is confusing and illogical. If you want to see it explained by someone better than I can, see Ned Bachelder's post about Python names [here](https://nedbatchelder.com/text/names.html). But I'll try to summarize the ideas below.

When you assign a variable to a value, that variable then points to the value in memory. For example, if you have the following code, then it might look like this (image created by www.pythontutor.com).

{% highlight python %}
x = 2
y = 3
{% endhighlight %}

![Arrow pointing from x to 2, and from y to 3](https://i.imgur.com/ao18QVX.png)

When a variable is reassigned, it stops pointing to the old value, and starts pointing to the new value. A common misconception is that doing `x+=2` will add 2 to the value of x, but what happens is actually more complicated. Remember that `x+=2` is a shorthand for `x = x+2`. So when you do `x+=2`, you're storing the value of x+2 to x, completely reassigning it. That's why when you do this, the value of x does not change:

{% highlight python %}
x = 2
y = x
x+=2
print(y)  # y is still 2, even though x is now 4.
{% endhighlight %}

You can see it visualized on www.pythontutor.com here:

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=x%20%3D%202%0Ay%20%3D%20x%20%0Ax%2B%3D2%0Aprint%28y%29%20%20%23%20y%20is%20still%202,%20even%20though%20x%20is%20now%204.&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=true&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

Another thing to remember is that when you pass variables to a function, that is another way of naming variables. So in this code:

{% highlight python %}
x = 2
def f(num):
  num += 2
  return num

print(f(x))  # 4
print(x)  # 2
{% endhighlight %}

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=x%20%3D%202%0Adef%20f%28num%29%3A%0A%20%20num%20%2B%3D%202%0A%20%20return%20num%0A%0Aprint%28f%28x%29%29%20%20%23%204%0Aprint%28x%29%20%20%23%202&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=true&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

In this code snippet, when the variable `x` is passed into the function `f`, the variable `num` inside of `f` points to the same 2 as `x` does. However, when we reassign num with `num += 2`, the original `x` is unaffected, because += reassigns. So far, this acts exactly like Java does with ints, but the reasons are completely different. And the true is same even for "complex" data like lists. For example:

{% highlight python %}
nums = [1, 2, 3]
nums2 = nums
nums2 = nums + [5]
print(nums)  # [1, 2, 3]
print(nums2)  # [1, 2, 3, 5]
{% endhighlight %}

When you add a list to a list, it returns a new list with the two lists added together.

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=nums%20%3D%20%5B1,%202,%203%5D%0Anums2%20%3D%20nums%0Anums2%20%3D%20nums%20%2B%20%5B5%5D%0Aprint%28nums%29%20%20%23%20%5B1,%202,%203%5D%0Aprint%28nums2%29%20%20%23%20%5B1,%202,%203,%205%5D&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=false&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

So what happens if instead of reassigning, we do something else? Take this code for example:

{% highlight python %}
nums = [1, 2, 3]
nums2 = nums
nums2.append(5)
print(nums)  # [1, 2, 3, 5]
print(nums2)  # [1, 2, 3, 5]
{% endhighlight %}

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=nums%20%3D%20%5B1,%202,%203%5D%0Anums2%20%3D%20nums%0Anums2.append%285%29%0Aprint%28nums%29%20%20%23%20%5B1,%202,%203,%205%5D%0Aprint%28nums2%29%20%20%23%20%5B1,%202,%203,%205%5D&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=false&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

With this code, after we assign nums2 to nums, they both point to the same object in memory. So when we call `nums2.append(5)` (which appends a 5 to the end of the list), since both variables point to the same list, both variables will be pointing to the list with the 5 appended to the end!

Notice that in the first list example I didn't use the `+=` shortcut. That's because Python defines += as .append() for lists, since it's more efficient to add to an existing list than to create a new one. But the consequence of this is that doing += to a list will "mutate" it, as well as any other variables that point to the same list. And remember, as explained above, function calls are done by renaming. So by passing a list (or any other object) to a function, if you modify it in the function, it will be modified outside the function. To avoid this, you can just make a copy of the list, like this:

{% highlight python %}
nums = [1, 2, 3]
def add_5(nums):
  '''
  Adds 5 to the end of a list. Does not mutate the
  original list.
  '''
  nums = nums.copy()
  nums.append(5)
  return nums

nums2 = add_5(nums)
print(nums)  # [1, 2, 3]
{% endhighlight %}

Sorry, I know that was a lot, but I hope this gives you a good deep dive into all the nuances of functions, so you can write code that suits your needs and does not surprise you.

# Built In Functions

Speaking of functions, I should mention the functions that are built into Python, that make working in Python super pleasant and quick. I won't go through all of them, but just a few that stand out to me as important. You can view the full list [here](https://docs.python.org/3/library/functions.html).

## abs

We've seen this before, but I'll list it here for completeness. The abs() function takes in a number (float or int), and returns its absolute value, or its distance from 0.

{% highlight python %}
print(abs(-10))  # 10
{% endhighlight %}

## bool

This function turns any variable into it's boolean value. As discussed before, most values will be `True` except for the special cases outlined in the boolean section.

{% highlight python %}
print(bool(10))  # True
print(bool([]))  # False
{% endhighlight %}

## eval

`eval` is a function which takes a string, and then evaluates that string as Python code. PLEASE do not use `eval` in any serious code you write - there is probably a better way to do it, and it has [serious security concerns](https://security.stackexchange.com/questions/94017/what-are-the-security-issues-with-eval-in-javascript). However, in some cases it is useful to use eval when you're just testing code on your own.

{% highlight python %}
x = eval("5 + 5")
print(x)  # 10
{% endhighlight %}

## float

`float` turns any value into a float, or decimal value.

{% highlight python %}
x = float(10)
print(x)  # 10.0
y = float("12.23")
print(y + 1)  # 13.23
{% endhighlight %}

## input

`input` is a function that lets you get a string from user input. This is good for making scripts that other people use. It is like the Scanner from Java, except that it can only get strings from the user. If you want to use the value as an int value, you'll have to cast the input. Here's an example REPL for you to play with:

<iframe height="400px" width="100%" src="https://repl.it/@misingnoglic/Input-example?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

Note that there are better ways to add other values to strings, but we'll talk about that in another section.

## int

`int` is a function that turns any value you give it into an int, just like `float`.

{% highlight python %}
print(int("10")+5)  # 15
{% endhighlight %}

## len

`len` gives you the length of a list.
{% highlight python %}
L = [1, 2, 3]
print(len(L))  # 3
{% endhighlight %}

## max

`max` gives you the maximum value of a list.
{% highlight python %}
L = [1, 2, 3]
print(max(L))  # 3
{% endhighlight %}

## min

`max` gives you the minimum value of a list.
{% highlight python %}
L = [1, 2, 3]
print(min(L))  # 1
{% endhighlight %}

## print

You've probably noticed this by now, but `print` will print out the value that you give it. You can do some other things with print though, like print out multiple values, choose what goes between each value, and choose what goes at the end of the statement. Here are some examples:

<iframe height="400px" width="100%" src="https://repl.it/@misingnoglic/print-example?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

## round

The `round` function takes in a number, and rounds it to a number of digits. Here are some examples in the REPL:

{% highlight python %}
>>> x = 3.1415926343
>>> round(x, 3)
3.142
>>> round(x, 2)
3.14
{% endhighlight %}

## sorted

We've seen this before, but `sorted` will sort a list, based on a key that you give it. You can also pass in a parameter to reverse the sorting.

{% highlight python %}
>>> L = [1, 4, 5, 3, 6, -7, -2, 2, 3]
>>> sorted(L)
[-7, -2, 1, 2, 3, 3, 4, 5, 6]
>>> sorted(L, reverse=True)
[6, 5, 4, 3, 3, 2, 1, -2, -7]
>>> # Let's sort based on distance from 2.
>>> def f(x): return abs(abs(x)-2)
# The numbers closest to 2 will be first.
>>> sorted(L, key=f)
[-2, 2, 1, 3, 3, 4, 5, 6, -7]
{% endhighlight %}

## str

`str` turns a value into a string. This is useful for adding it to another string, since you can't add other values to strings.

{% highlight python %}
x = 3
print("Your value is :"+str(x))  # Your value is: 3
{% endhighlight %}

## sum

`sum` returns the sum of a list.
{% highlight python %}
nums = [1, 2, 3]
print(sum(nums))  # 6
{% endhighlight %}


## dir

`dir` is a function that will not be useful in your actual code, per se. However, it's exceptionally useful when you're dealing with some kind of new object, and you want to find out what kind of attributes it has. Here's an example of me playing with it in the REPL, in case I forget what method adds to a list.

{% highlight python %}
>>> l = [1,2,3]
>>> dir(l)
['__add__', '__class__', '__contains__', '__delattr__', '__delitem__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__gt__', '__hash__', '__iadd__', '__imul__', '__init__', '__init_subclass__', '__iter__', '__le__', '__len__', '__lt__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__reversed__', '__rmul__', '__setattr__', '__setitem__', '__sizeof__', '__str__', '__subclasshook__', 'append', 'clear', 'copy', 'count', 'extend', 'index', 'insert', 'pop', 'remove', 'reverse', 'sort']
{% endhighlight %}

## help

`help()` is a function similar to `dir()`, in that it's useful for debugging and quick testing. When you pass it a function, it will show you the docstring help text for that function. Here is an example in the REPL:

{% highlight python %}
>>> help(score)  # the score function we defined before.
"""
Help on function score in module __main__:

score(points, seconds, multiplier=1)
    Calculates the total end score of the player when
    the game ends. Divides the number of points earned
    by the number of seconds it took them to complete
    the level. It also accepts a parameter multiplier,
    which is the end multiplier of the score.
"""

>>> l = [1, 2, 3]
>>> help(l.copy)
"""
Help on built-in function copy:

copy() method of builtins.list instance
    Return a shallow copy of the list.
"""

>>> help(l.append)
"""
Help on built-in function append:

append(object, /) method of builtins.list instance
    Append object to the end of the list.
"""
{% endhighlight %}

help() goes along really well with dir(), for when you're just starting and exploring a codebase.

# Summary

Damn, that was much longer than I thought it was going to be. I guess it turns out that there's a lot to say about Python! Anyway, I hope that this blog has continued to give you a good understanding of all the nuances with Python, while bridging your knowledge from your understanding of Java. I'm definitely going to write another part to this to talk about lists, strings, dictionaries, and other fun collections, as well as how to make your own classes. If you liked this post, please share it with your friends, and sign up [for my mailing list](https://goo.gl/forms/jzaFhUpZ6x17oOJh2) to get notified about when the next one will come out. Hopefully it will take shorter than 9 months! Thank you again, and see you next time :)

Note: [Part 3](https://aryaboudaie.com/java/python/technical/educational/2018/10/15/python-for-java-programmers-p3.html) has now come out!
