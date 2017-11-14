---
layout: post
title:  "Python for Java Programmers - Part 2 - The Nitty Gritty"
subtitle: "Learning Python as a Second Language"
date:   2017-11-20 23:56:45
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

The wording of `if` statements is mostly the same as Java. The only difference is that `else if` is spelled `elif` in order to have its own keyword. The only difference is the structure. Look for example at this code, which assigns a ticket price based on how fast you're going:

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

Try changing the value of

<iframe height="400px" width="100%" src="https://repl.it/@misingnoglic/SpeedTicketIfElse?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals" width="100%" ></iframe>

The way that the `if` statements work is that if the thing in the `if` is true, it will execute all the code indented under the line with the if statement. This is a departure from Java, which uses curly braces to contain pieces of code. If this doesn't make sense, PLEASE read the part 1 to this. Thank you :)
