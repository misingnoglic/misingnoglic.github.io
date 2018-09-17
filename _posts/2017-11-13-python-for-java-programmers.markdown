---
layout: post
title:  "Python for Java Programmers - Part 1 - The Big Picture"
subtitle: "Learning Python as a Second Language"
date:   2017-11-13 23:56:45
categories: [Java, Python, Technical, Educational]
---


Intended audience for this post: Someone who has taken a semester/year of Java, and wants to learn how to code in Python.

<b>Part 1:</b> Explaining how to install Python, why learn Python, and the big picture differences between the two languages as you get started. I won't go into specific syntax in this part, but will instead just tell you what to look out for when learning Python.

# Quick Note:

I've made a mailing list! If you'd like to get an email whenever I update the site, [please enter your email here](https://goo.gl/forms/jzaFhUpZ6x17oOJh2). I promise they will be non-intrusive (about once a week)!

# Table of Contents

{:toc}

# Introduction:

So, you've learned Java, probably from a class or on your own, and you've decided you want to learn now Python. Maybe it's because you heard Python is easier and quicker to write code in, or because you want to get into the fun world of creating websites using something like [Flask](http://flask.pocoo.org/) or [Django](https://www.djangoproject.com). Maybe you don't have a specific reason, but want to just see what all the fuss is about. If so, this guide will be perfect for you! Most other introduction to Python to guides which assume no prior experience in programming, which are a complete waste for people like you who already know how to all the fun stuff (loops, arrays, booleans, etc). It's either that, or they go really quickly through the language without much discussion, leaving people who've never learned a new language behind. Instead, I will try to take another approach, by using what you already know to give you a head start into being a Python expert. In this guide, I'll go through a list of all the topics you have learned in Java, and explain how you can do similar things in Python, as well as new tips and tricks to keep you learning!

# Note on learning new languages

As someone who has been a TA for many intro to programming classes, one common misconception I've seen of programming is that it's all about learning languages, and once you learn six or seven different languages, then you're good to go. The way of becoming good at programming isn't taking one semester of Java, then one semester of Python, etc... Rather, when you learn one language, it should be fairly easy for you to pick up another one, or at least easy as learning your first one was. Additionally, learning another language should serve some purpose (I'll give you some reasons why you should learn Python), but don't think that after this, you need to be chasing a Ruby or Lisp tutorial (unless you decided you really don't like Python or Java, and want to try new things). Instead, try to expand your knowledge of HOW to do things, or just make some cool programs! Ok, mini rant over. Maybe I'll write a post about this later.

# Reasons why you should learn Python

You're probably already convinced, since you're on this tutorial, but just in case, here is my shortlist of why it will be useful for you to learn Python.

- It's much quicker and faster to write scripts in Python once you get good at it.
- There are thousands of packages (code other people wrote) you can easily install and include in your program.
- It's easier for doing interviews in.
- It's easier to debug, as it is much more readable.
- It's easier to work with others on it, as it's easier to read what other people wrote, and it's easier to modularize code (or write smaller pieces of code that work together).
- It's very easy to create your own website using Django or Flask (tutorials coming soon).
- It's easy to do data analysis using it.
- It's easier to teach other people, if you're the type (like me) that likes teaching people programming.

If you want to get a good idea of how much easier it is to write code for Python, check out [my previous post](http://aryaboudaie.com/interviews/python/technical/2017/11/06/python-for-interviews.html) on doing interviews in Python, and just see how much cleaner the code is.

I'll probably keep adding to this list as I get more ideas. Hopefully you're already pumped to learn this new language though.

# Downloading and Installing Python

If you don't want to download anything, you can run any python code on [www.repl.it](http://www.repl.it). This website allows for coding online in several languages, including Python 3. Just make an account, and select Python 3 as your language. My post will also contain snippets for running, right on this page!

To download Python, I suggest downloading the 3.6 version of Python from Anaconda - this is a distribution of Python that comes with a ton of packages built in. You can download that [here](https://www.anaconda.com/download/).

You can also download it from the official Python website [here](https://www.python.org/downloads/). Make sure on either installation to click the button to add it to the command line path.

After this, you can run any Python program from the command prompt/terminal, by CDing to the folder with your program and typing:

`python3 myfile.py` for Mac/Linux computers

`python myfile.py` for Windows computers

If you're more used to using IDEs, you can use the IDLE program (which should have been installed with Python) to run your code. If you want something more heavy, the creators of the IntelliJ IDE also made an IDE called Pycharm, which you can download [here](https://www.jetbrains.com/pycharm/). Pycharm is the IDE of my choice, and you can even have the professional version [for free as a student](https://www.jetbrains.com/student/). The community version is also free for everyone. It's a little annoying to get it set up in the beginning, but once you have it working, it's super powerful.

If you want a quick environment to code in, you can just type `python3` or `python` into your command line to get something called a REPL. REPL stands for read, evaluate, print, loop; but it basically means that you can type your code in the command line one line at a time, to quickly do some computation or see if something works.

![Picture of REPL](https://i.imgur.com/EofwtHA.png)

## Note about Python versions

You'll often hear people talking about a version 2 of Python, and a version 3. Version 3 is the current updated version, while version 2 is a version that has been discontinued for several years now. This tutorial will assume you're using Python 3 (3.6 if I'm lucky) - this will be the version you'll have if you installed it according to these steps.

# General Differences between the Two - Structure and Interpretation:

## Compiling vs Interpreting

In Java, when you write a program, before you can run it, you have to first compile it. Maybe your teacher was cruel and required you to manually do the step where you turn your .java file into a .class file by typing:

`javac MyClass.java`

Or maybe you got to use an IDE like Eclipse or DrJava, and just clicked the play button to run your code. Regardless, when you compiled the program, if there were some errors in it, you would have gotten a message before any of the code was actually run. For example, if you try to run this program:

{% highlight java %}
public class Main{
  public static void main(String[] args){
    System.out.println("asd"-3);
  }
}
{% endhighlight %}

You might get an error like this:

{% highlight java %}
Main.java:3: error: bad operand types for binary operator '-'
    System.out.println("asd"-3);
                            ^
  first type:  String
  second type: int
1 error

exit status 1
{% endhighlight %}


This error is caught by the compiler, and your program has not compiled, since this error was found. Once you fix the error, you'll be able to easily compile and then run the program. The exception to this rule are runtime errors that the compiler can't catch, such as dividing by zero, or trying to go out of bounds on an array - these errors are only thrown after running the code.

In Python however, your programs are not compiled, and as such, they are not checked for errors (besides syntax errors) before running. The way Python will run your code is line by line, and if one line has an error in it, the program won't throw the error until it gets to that line. This means that when you write your Python programs, you should check them for errors first, as you might not catch them as easily as Java would be able to catch them.

{% highlight python %}
print("hello")
print("hello"-1) # throws error, you can't subtract from strings
{% endhighlight %}

Gives this output:

{% highlight python %}
hello
Traceback (most recent call last):
  File "python", line 2, in <module>
TypeError: unsupported operand type(s) for -: 'str' and 'int'
{% endhighlight %}

If the error is in an if statement that isn't evaluated, it won't even be caught. The following code runs with no errors:

{% highlight python %}
print("hello")
x = 2
if x==3:
	print("hello"-1) # this line is never run, so the error is never thrown
{% endhighlight %}

The following is an embedded snippet on www.repl.it - feel free to run it, and mess around with the code! It may take a second for it to become runnable, though. Try turning the statement in the "if" to `if x==2`.

<iframe height="400px" width="100%" src="https://repl.it/@misingnoglic/Never-Run-Error?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals" width="100%" ></iframe>

One of the benefits of this line by line evaluation of Python however is the REPL, which was described above. Because the programs are interpreted line by line, you can also open your REPL (by typing `python3` or `python` into your command line,  by clicking Tools->Python Console in Pycharm, or just going on [repl.it](http://repl.it/languages/python3) ). This is one feature I suggest you spend a lot of time looking at, as it incredibly speeds up programming by letting you test things on the fly before committing them to your program. You can also try it on the right hand side of the repl.it embedded snippets of code.

# Structure of Programs

## Freedom from Classes

In Java, if you want to write any code, it has to be inside of a class, inside of its own file. Just to print out one single statement, you need all of this code:

{% highlight java %}
public class HelloProgram{
    public static void main(String[] args){
        System.out.println("Hello");
    }
}
{% endhighlight %}

If you want to make a method, you have to put it in the class, and then test it in the main method:

{% highlight java %}
public class AddProgram{
    public static void main(String[] args){
        System.out.println(addTest(2,3));
    }
    public static int addTwoNumbers(int a, int b){
        return a+b;
    }
}
{% endhighlight %}

Additionally, if you want two classes, you have to put them in separate files. This is different from Python, where your code doesn't have to be contained in classes. Your Python file can just have the statements free form in the program. This means that you don't have to have all the structure, but also it's up to you to keep your program organized and easy to read. Whatever you put, the Python interpreter will read it line by line, and interpret it as it goes.

{% highlight python %}
print("Hello")
print(2+3)

def add_two_nums(x, y):
    return x+y

print(add_two_nums(2,3))
{% endhighlight %}

<iframe height="400px" width="100%" src="https://repl.it/@misingnoglic/Unstructured-Code?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals" width="100%" ></iframe>

### White Space

In Java, if you want to indicate that a block of code is "inside" another block of code, you will use curly braces to contain that statement within another one. Two examples:

{% highlight java %}
public static void someMethod{
    ...
}
{% endhighlight %}

{% highlight java %}
if (some_boolean_is_true){
    ...
}
{% endhighlight %}

In general, to be nice to whoever is reading the code in the future, you also indent the code inside of these curly braces, so that it's easy to see what code is inside other code. This isn't required, however, and your whole Java program could be just one line (but nobody would want to work with you).

In Python, they cut out the middle man, and the indentation is part of the syntax. If you want a block of code to be inside another block of code, you end the line with a colon, and then everything under it gets indented, like such:

{% highlight python %}
def f(x): # example function
    return x+2
{% endhighlight %}

{% highlight python %}
if x>2:
    print("x is greater than two")
print("this will always print out")
{% endhighlight %}

Once the indent level is decreased, Python knows that the block of code is over. By using indentation instead of curly braces, I think the code is a lot easier to read, and it makes sure nobody annoyingly puts all their code on one line.

## Methods vs Functions

In Java, you learned about methods - pieces of code that take in inputs, and return some output. The thing about these methods were that they had to be inside of a class - even if they had no need to be part of a specific object. This lead to the annoying problem of having to make a class just to write your simple method.

In Python, the main way of writing this kind of code is through functions. The difference is that functions do not need to be inside of classes, and can exist on the same realm as an integer or any other type of object that can be created. In other words, functions in Python are ["first class citizens"](https://stackoverflow.com/questions/23037519/are-functions-first-class-objects-in-python)

Here is an example of a simple function:
{% highlight python %}
def f(x, y, z): # f is the name of the function, x,y,z are the parameters.
  return x+y-z
print(f(1,2,3)) # would print 0 (1+2-3)
{% endhighlight %}

The `def` keyword is what triggers the definition of the function, and can be done anywhere in code. To return a value, you use the same `return` keyword as in Java. Once the indentation is over, Python knows that the code for that specific function has ended. Then, anywhere in the same scope as f, you can call f with three parameters, and it will return the inner workings of the computations. Notice how you don't have to declare any types (more on that later).

One cool thing about Python functions is that you can have default values for parameters you don't pass in. For example:

{% highlight python %}
def f(x, y=4):
  return x+y
{% endhighlight %}

If you called this function with two parameters, it would simply add them together. However, if you called it with just one parameter, it would add that parameter to 4, since the code sets y=4 if no other value is passed.

<iframe height="400px" width="100%" src="https://repl.it/@misingnoglic/Default-Values-for-Functions?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals" width="100%" ></iframe>

Another cool thing about Python functions is since they are first class citizens, they can be passed into other functions! This is key for making your code generic and reusable (though make sure you don't abuse it). In general, I find python functions a lot easier to work with than Java methods, and it makes writing and testing them a snap!

## Where's the Types???
You might have already noticed this, but in Python, you don't have to declare any types. In Java, you have to declare the type of:

- Any variables you declare
- The value a method returns
- Any inputs to methods

To make code generic to type in Java is a lot of work (see [this slideshow](https://docs.google.com/presentation/d/10Cj_z8h1Cvxr4aEAchDQPUqlJTKxz4_10w0QT-JgUhw/edit)), but in Python, it's the default. You can declare a variable with one type, and then set it to something else later.

{% highlight python %}
x = 2
print(x+2)
x = False # No problem here
print(x)
{% endhighlight %}

<iframe height="400px" width="100%" src="https://repl.it/@misingnoglic/No-Types?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals" width="100%" ></iframe>

This also means that you can write a function that can work on multiple types.

{% highlight python %}
def add(x, y):
	return x+y
print(add(1, 3)) # adding two ints adds them
print(add("hello ", "world")) # adding two strings concatenates them
{% endhighlight %}

<iframe height="400px" width="100%" src="https://repl.it/@misingnoglic/Function-works-on-different-types?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals" width="100%" ></iframe>

This is good, in that it's less bureaucracy to deal with when writing your programs. However, this may let you shoot yourself in the foot. If you pass variables of the wrong type to a function, Python won't catch the error until the code tries doing something it can't do with the inputs.

{% highlight python %}
def subtract(x, y):
  return x-y

x = subtract("3", "2") # Will try to call subtract, and will throw error in the return x-y line
{% endhighlight %}


Additionally, since you don't have to declare if a function is void or if it returns something, the language won't check to make sure you didn't forget to return something.

{% highlight python %}
def is_even(x):
  if x%2==0: return True
  # No else statement!!!
{% endhighlight %}

If you called that function on x=3, it would return the type "None" - which is Python's way of having a type that means "nothing." It's kind of like null in Java, but not quite the same. Either way, it's up to you to check for errors like this. With great power comes great responsibility.

## Parentheses?

If you haven't noticed by now, a lot of statements that required parentheses in Java don't in Python. If this makes you nervous, you can keep the parentheses in Python, but seasoned Python programmers may look at it funny.

{% highlight python %}
x=2
if x==2:
  print("x is two!")

while x<10:
  print(x)
  x = x+1

{% endhighlight %}

<iframe height="400px" width="100%" src="https://repl.it/@misingnoglic/No-Parentheses-Needed?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals" width="100%" ></iframe>

There's really no downsides to this one. It's just nicer.

### It's All Lists From Here

In Java, the default way of having a bunch of items is the array. In the array, you have to specify the length and the type of the array.

{% highlight java %}
int[] x = new int[5];
{% endhighlight %}

They're also pretty simple, with not that many methods associated with arrays.

If you wanted to have a list of objects with an undefined length, you could use a List (like an ArrayList). However, these are just regular objects, and are not as syntactically easy to use as arrays.

In Python, there are no arrays, only lists with the best of all worlds. The lists are very easy to create, use, and manipulate. Just like in Java, their indexing also starts at 0. Here are a few examples of the fun things you can do with lists out of the box:

{% highlight python %}
L = [4,9,7]
L.append(10) # adds 10 to the end
print(L) # [4,9,7,10]
print(L[0]) # Item at index 0 - 4
print(L[1]) # Item at index 1 - 9
print(L[-1]) # Python supports negative indexing, so l[-1] is the last item - 10
print(len(L)) # len is built in function that gets length: 4
L2 = [9,9,9]
L3 = L + L2 # adds l2 to the end of l
print(L3) # [4,9,7,10,9,9,9]
# You can also get segments of lists easily
L4 = L3[1:4] # l3 from index 1 to (not including) index 4
print(L4) # [9,7,10]
L5 = L3[1:-1] # L3 from index 1 to (not including) last item.
print(L5) # [9,7,10,9,9]
L6 = L3[1:] # L3 from index 1 to the end (leaving out the second parameter)
print(L6) # [9,7,10,9,9,9]

# sum of each thing in L3
s = 0
for item in L3: # for each loop
	s += item
print(s)

# but there's a built in function for that! and more!
print(sum(L3)) # sum of all items in L3
print(len(L3)) # length of L3
print(max(L3)) # largest item in L3
print(min(L3)) # smallest item in L3
print(sorted(L3)) # L3 but sorted (smallest to largest)

# testing for membership in list (no need to loop)
print(9 in L3)
print(11 in L3)

# Using the "sorted" function to return a sorted list
sorted_l3 = sorted(L3)
print(sorted_l3) # [4, 7, 9, 9, 9, 9, 10]
{% endhighlight %}

Again - please feel free to mess with this code and then run it. See what happens! Try it with different lists too.

<iframe height="400px" width="100%" src="https://repl.it/@misingnoglic/Fun-with-Lists?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals" width="100%" ></iframe>

Lists can also contain items of multiple types with no issue.

{% highlight python %}
L = [1, 2.0, True, "s"]
{% endhighlight %}

Another thing that's great - in Java, you have to learn a whole new syntax for Strings, even though they basically do the same things as arrays/lists (keep a collection of items). In Python, the syntax is basically the same for both collections!

{% highlight python %}
s = "hello"
s2 = " world"
s3 = s + s2
print(s3)

print(s3[1:4])
print(s3[1:-1])
print(s3[1:])

for letter in s3:
	print(letter)

print(len(s3))

print("e" in s3)
print("x" in s3)

print(sorted(s3)) # [' ', 'd', 'e', 'h', 'l', 'l', 'l', 'o', 'o', 'r', 'w']
{% endhighlight %}

<iframe height="400px" width="100%" src="https://repl.it/@misingnoglic/Fun-with-Strings?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals" width="100%" ></iframe>

Once you learn the syntax for lists, you'll already know the syntax for strings! Easy as that :)

### List Comprehensions

Python also has this sweet thing called a list comprehension. Let's say you have an array of grades in Java, and you want to add ten to all of them, as a curve. You would have to do something like this:

{% highlight java %}
for (int i = 0; i<grades.length; i++){
  grades[i] = grades[i]+10;
}
{% endhighlight %}

In Python, using this special syntax, you can create a new list based on the contents of an old list. So like this:
{% highlight python %}
grades_new = [x+10 for x in grades]
{% endhighlight %}

And that's it! grades_new will now be everything in grades, but with 10 added to it.

## Different Loops

In Java, there are three different kinds of loops. There's the for loop:

{% highlight java %}
for (int i = 0; i<10; i++){
	System.out.println("hi");
}
{% endhighlight %}

Then the while loop:

{% highlight java %}
int i = 0;
while (i<10){
	System.out.println("hi");
	i++;
}
{% endhighlight %}

And there's the for each loop:

{% highlight java %}
int[] someListOfInts = {1,2,3,4};
for (int i : someListOfInts){
	System.out.println(i);
}
{% endhighlight %}

However, the for loop and the while loop are basically the same thing. Python sees this, and took out the for loop. Instead you just have the while loop (which is practically identical to the Java while loop), and a for loop that is the same as Java's for each loop. Here's an example of the Python for loop:

{% highlight python %}
L = [1,5,8]
s = 0
for item in L: # for each loop
	s += item
print(s)
{% endhighlight %}

The `for item in L:` is basically saying - for each thing in L, call it `item` and do everything in the indented section with `item`.

This is a snippet from www.pythontutor.com - a great website to step through Python code one line at a time and really see what's going on, by visualizing all the variables all at once. It's a great way to find bugs in your code, or figure out why a script is doing something in a certain way!

<iframe width="800" height="500" frameborder="0" src="http://pythontutor.com/iframe-embed.html#code=L%20%3D%20%5B1,5,8%5D%0As%20%3D%200%0Afor%20item%20in%20L%3A%20%23%20for%20each%20loop%0A%09s%20%2B%3D%20item%0Aprint%28s%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=false&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

You can run this to see what it does step by step. You can see how `item` first equals 1, then 5, then 8.

If you want a for loop that just goes through a series of numbers, Python programmers use this function called `range()` to do that.

{% highlight python %}
for i in range(1,10): # for each loop
	print(i)
{% endhighlight %}

Range is a special function in python that returns a list from the first argument to (not including) the last argument. So range(1,10) is the same as [1,2,3,4,5,6,7,8,9]. This allows us to have a for loop that's similar to Java's.

Range can actually take either one, two, or three parameters:

`range(10)` - list from zero to 10, not including 10.
`range(2,10)` - list from 2 to 10, not including 10
`range(1,10, 2)` - list from 2 to 10, not including 10 and skipping by 2


<iframe height="400px" width="100%" src="https://repl.it/@misingnoglic/For-with-Range?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals" width="100%" ></iframe>

If you've noticed, these are the same parameters that are taken in by the list slicing (e.g. where L[2:10] gives all the items in L from index 2 to 10, not including 10).

## Dictionaries

In Python, if you want to make some sort of mapping between two things, like a HashMap in Java, you can use a dictionary. Dictionaries are extremely easy to use, and extremely versatile. To create one, we use this syntax:

{% highlight python %}
dna_mapping = {"A": "T", "T":"A", "G":"C", "C":"G"}
{% endhighlight %}

This example uses an idea from biology, where each letter (signifying a DNA nucleotide) is mapped to another letter. A maps to T, T maps to A, G maps to C, and C maps to G. To create a dictionary, you wrap it in `{ }` curly braces, and have a list of pairs key:value, separated by commas, like above. Then, you can easily look up the value associated with any given key, by using the same syntax as getting an element from a list, but putting the key in the square braces, like such:

{% highlight python %}
base = "A"
pair = dna_mapping[base]
{% endhighlight %}

`pair` will then equal "T", as "T" is the value for "A" in the dictionary.

You can also add new pairs or update old ones with the same syntax as setting variables:

{% highlight python %}
dna_mapping["X"] = "Y"
{% endhighlight %}

The dictionary will then be updated with the pair x:y.

If you want to loop through each key in the dictionary, it's the same syntax as looping through a list:

{% highlight python %}
for key in dna_mapping:
  print("The pair of "+key+" is "+dna_mapping[key])
{% endhighlight %}

Dictionaries are great when you have some kind of pairing data that you want to store, to easily look up later. Here is a full example of using a dictionary:

<iframe height="400px" width="100%" src="https://repl.it/@misingnoglic/Dictionary-Example?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals" width="100%" ></iframe>

Sorry if this was rushed, I will write more on dictionaries in part two!

## Boolean Logic in English

This one is pretty quick, but worth mentioning here anyway. In Java, to combine booleans, you would have to use `||` for or, and `&&` for and. In Python, you literally use the words "and" and "or" to do the same things. Also, True and False are uppercase.

{% highlight python %}
print(True and False) # False
print(True or False) # True
x = 2
print(x==2 or x==3) # True
{% endhighlight %}

You're gonna love this one too. To negate a boolean, you just put the word `not` in front of it. Again, no parentheses needed. Amazing.

The only time you want to use parentheses is like in Java, to make it clear what order you want everything to happen. As with most languages, whatever you put in the parentheses will come first.

{% highlight python %}
b = not True
print(b) # False
b = (True or False) and False
print(b) # False
b = True or (False and False)
print(b) # True
{% endhighlight %}


Related to booleans, if/else statements are mostly constructed the same way. The only difference is that in python, `else if` is called elif

{% highlight python %}
def ticket_price(speed):
  if speed<50:
    return 0
  elif speed<60:
    return 50
  else:
    return 100
{% endhighlight %}

Again, more on this in part 2.

## Getting/Converting User input

In Java, to get user input, you probably learned to make a Scanner object, and then call various methods to get the user input, such as `nextLine()` or `nextInt()`

In Python, all input is just gotten from the `input()` function, which you do not need to import. As a parameter to the input function, you give the prompt for the user. For example, if you wanted to get a user's name, you would have the following code.

{% highlight python %}
name = input("Hello, please enter your name: ")
{% endhighlight %}

The issue with this is that whatever you get from `input()` will be a string. Thankfully, it is very easy to convert a string to a different type. Just wrap the string around the type you want it to be, such as  `int()` to turn it into an integer, or  `float()` to turn it into a floating point number (like a double in Java). Here is an example of getting user input.

<iframe height="400px" width="100%" src="https://repl.it/@misingnoglic/Input-Example?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals" width="100%" ></iframe>

Note: If you're using version 2 of Python (which I highly discourage), you should use `raw_input`.

## Stylistic Naming Conventions

This one is also short. In Java, most things are named in camelCase, where multi-word variables are joined with the second word starting with a capital letter. In the Python world, we prefer snake_case - where the words are joined using underscores. The difference is when defining classes in Python, we use the same CamelCaseConvention.

{% highlight java %}
int largestNumber = 2;
{% endhighlight %}

{% highlight python %}
largest_number = 2
{% endhighlight %}

If you're curious, [this document](https://www.python.org/dev/peps/pep-0008/) is the official Python style guide, known as PEP8. PEP8 is like a sacred text for Python programmers, as it was written by our [Benevolent Dictator for Life](https://en.wikipedia.org/wiki/Benevolent_dictator_for_life), [Guido Van Rossum](https://en.wikipedia.org/wiki/Guido_van_Rossum), the creator of Python. There is also [Google's Python Style Guide](https://google.github.io/styleguide/pyguide.html), which is pretty widely used.

# Conclusion

EDIT: Part 2 is now out! Read it [here](https://aryaboudaie.com/java/python/technical/educational/2018/09/16/python-for-java-programmers-p2.html). 

I hope this article gave you a good overview of all the different things to expect when looking at Python code, so you wouldn't feel too left out. You might not have a solid grasp at Python fundamentals, but in the next part, I will write about how to actually get to writing some Python - with direct translations from what you know from Java! You've seen that Python gives you a lot of freedom, but with this freedom comes the responsibility to make sure you keep writing good code! Please let me know if you have any questions in the comments below, or if you think there are any mistakes/confusing bits to it. If you're already a Python expert, please let me know what I missed. And of course, if I helped you out, please let me know, and share this article with any friends you think might like it. I am very new at writing tutorials like this, but I want to get really good at it!

Again, if you want to be notified when part 2 comes out, please sign up for my [email updates here](https://goo.gl/forms/jzaFhUpZ6x17oOJh2)! See you next time.

Special thanks to my brother and to my friends who read this before and offered their thoughts!
