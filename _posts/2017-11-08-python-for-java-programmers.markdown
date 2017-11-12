---
layout: post
title:  "Python for Java Programmers - Part 1"
subtitle: "Learning Python as a Second Language"
date:   2017-11-06 23:56:45
categories: [Java, Python, Technical, Educational]
---


Intended audience for this post: Someone who has taken a semester/year of Java, and wants to learn how to code in Python. Part 1: Explaining how to install Python, why learn Python, and the big picture differences between the two languages as you get started. I won't go into specific syntax in this part, but will instead just tell you what to look out for when learning Python.

# Introduction:

So, you've learned Java, probably from a class or on your own, and you've decided you want to learn now Python. Maybe it's because you learned Python is easier and quicker to write code in, or because you want to get into the fun world of creating websites using something like Flask or Django. Maybe you don't have a specific reason, but want to just see what all the fuss is about. If so, this guide will be perfect for you! Most other introduction to Python to guides which assume no prior experience in programming, which are a complete waste for people like you who already know how to all the fun stuff (loops, arrays, booleans, etc). It's either that, or they go really quickly through the language without much discussion, leaving people who've never learned a new language behind. Instead, I will try to take another approach, by using what you already know to give you a head start into being a Python expert. In this guide, I'll go through a list of all the topics you have learned in Java, and explain how you can do similar things in Python, as well as new tips and tricks to keep you learning!

# Note on learning new languages
 
As someone who has TAd many classes, one common misconception I've seen of programming is that it's all about learning languages, and once you learn six or seven different languages, then you're good to go. The way of becoming good at programming isn't taking one semester of Java, then one semester of Python, etc... Rather, when you learn one language, it should be fairly easy for you to pick up another one, or at least easy as learning your first one was. Additionally, learning another language should serve some purpose (I'll give you some reasons why you should learn Python), but don't think that after this, you need to be chasing a Ruby or Lisp tutorial (unless you decided you really don't like Python or Java, and want to try new things). Instead, try to expand your knowledge of HOW to do things, or just make some cool programs! Ok, mini rant over. Maybe I'll write a post about this later.

# Reasons why you should learn Python

You're probably already convinced, since you're on this tutorial, but just in case, here is my shortlist of why it will be useful for you to learn Python.

- It's much quicker and faster to write scripts in Python once you get good at it.
- There are thousands of packages you can easily install and include in your program.
- It's easier for doing interviews in.
- It's easier to debug, as it is much more readable.
- It's easier to work with others on it, as it's easier to read what other people wrote, and it's easier to modularize code (or write smaller pieces of code that work together).
- It's very easy to create your own website using Django or Flask (tutorials coming soon).
- It's easy to do data analysis using it.
- It's easier to teach other people, if you're the type (like me) that likes teaching people programming.

If you want to get a good idea of how much easier it is to write code for Python, check out my previous post on doing interviews in Python, and just see how much cleaner the code it.

I'll probably keep adding to this list as I get more ideas. Hopefully you're already pumped to learn this new language though.

# Downloading and Installing Python

If you don't want to download anythin, you can run any python code on [www.repl.it](http://www.repl.it). This website allows for coding online in several languages, including Python 3. Just make an account, and select Python 3 as your language.

To download Python, I suggest downloading the 3.6 version of Python from Anaconda - this is a distribution of Python that comes with a ton of packages built in. You can download that [here](https://www.anaconda.com/download/).

You can also download it from the official Python website [here](https://www.python.org/downloads/). Make sure on either installation to click the button to add it to the command line path.

After this, you can run any Python program from the command prompt/terminal, by CDing to the folder with your program and typing:

`python3 myfile.py` for Mac/Linux computers

`python myfile.py` for Windows computers

If you're more used to using IDEs, you can use the IDLE program (which should have been installed with Python) to run your code. If you want something more heavy, the creators of the IntelliJ IDE also made an IDE called Pycharm, which you can download [here](https://www.jetbrains.com/pycharm/). Pycharm is the IDE of my choice, and you can even have the professional version [for free as a student](https://www.jetbrains.com/student/). The community version is also free for everyone. It's a little annoying to get it set up in the beginning, but once you have it working, it's super powerful.

If you want a quick environment to code in, you can just type `python3` or `python` into your command line to get something called a REPL. REPL stands for read, evaluate, print, loop; but it basically means that you can type your code in the command line one line at a time, to quickly do some computation or see if something works.

(TODO: Include a picture of the REPL)

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

```
Main.java:3: error: bad operand types for binary operator '-'
    System.out.println("asd"-3);
                            ^
  first type:  String
  second type: int
1 error

exit status 1
```

This error is caught by the compiler, and your program has not compiled, since this error was found. Once you fix the error, you'll be able to easily compile and then run the program. The exception to this rule are runtime errors that the compiler can't catch, such as dividing by zero, or trying to go out of bounds on an array - these errors are only thrown after running the code.

In Python however, your programs are not compiled, and as such, they are not checked for errors (besides syntax errors) before running. The way Python will run your code is line by line, and if one line has an error in it, the program won't throw the error until it gets to that line. This means that when you write your Python programs, you should check them for errors first, as you might not catch them as easily as Java would be able to catch them.

{% highlight python %}
print("hello")
print("hello"-1)
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
	print("hello"-1) # this line is never run
{% endhighlight %}

NOTE: For some reason, repl.it prints "None" at the end of the output for its scripts. Ignore that "None"

<script src="//repl.it/embed/OAK4/0.js"></script>

One of the benefits of this line by line evaluation of Python however is the REPL, which was described above. Because the programs are interpreted line by line, you can also open your REPL (by typing `python3` or `python` into your command line,  by clicking Tools->Python Console in Pycharm, or just going on [repl.it](http://repl.it/languages/python3) ). This is one feature I suggest you spend a lot of time looking at, as it incredibly speeds up programming by letting you test things on the fly before committing them to your program.

## Structure of Programs

### Freedom from Classes

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

<script src="//repl.it/embed/OAK6/0.js"></script>

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
def f(x):
    return x+2
{% endhighlight %}

{% highlight python %}
if x>2:
    print("x is greater than two")
{% endhighlight %}

By using indentation instead of curly braces, I think the code is a lot easier to read, and it makes sure nobody annoyingly puts all their code on one line.

### Where's the Types???
You might have already noticed this, but in Python, you don't have to declare any types. In Java, you have to declare the type of:

- Any variables you declare
- The value a method returns
- Any inputs to methods

To make code generic to type in Java is a lot of work (see [this slideshow](TODO: PUT LINK)), but in Python, it's the default. You can declare a variable with one type, and then set it to something else later.

{% highlight python %}
x = 2
print(x+2)
x = False
print(x)
{% endhighlight %}

<script src="//repl.it/embed/OANw/0.js"></script>

This also means that you can write a function that can work on multiple types.

{% highlight python %}
def add(x, y):
	return x+y
print(add(1, 3))
print(add("hello ", "world"))
{% endhighlight %}

<script src="//repl.it/embed/OAOK/0.js"></script>

This is good, in that it's less bureaucracy to deal with when writing your programs. However, this may let you shoot yourself in the foot. If you pass variables of the wrong type to a function, Python won't catch the error until the code tries doing something it can't do with the inputs.

Additionally, since you don't have to declare if a function is void or if it returns something, the language won't check to make sure you didn't forget to return something.

{% highlight python %}
def is_even(x):
  if x%2==0: return True
  # No else statement!!!
{% endhighlight %}

If you called that function on x=3, it would return the type "None" - which is Python's way of having a type that means "nothing." It's kind of like null in Java, but not quite the same. Either way, it's up to you to check for errors like this. With great power comes great responsibility.

### Parentheses?

If you haven't noticed by now, a lot of statements that required parentheses in Java don't in Python. If this makes you nervous, you can keep the parentheses in Python, but seasoned Python programmers may look at it funny.

{% highlight python %}
x=2
if x==2:
	print("x is two!")

while x<10:
	print(x)
	x = x+1

{% endhighlight %}

<script src="//repl.it/embed/OAQX/1.js"></script>

There's really no downsides to this one. It's just nicer.

### It's All Lists From Here

In Java, the default way of having a bunch of items is the array. In the array, you have to specify the length and the type of the array.

{% highlight java %}
int[] x = new int[5];
{% endhighlight %}

They're also pretty useless, with not that many methods associated with arrays.

If you wanted to have a list of objects with an undefined length, you could use a List (like an ArrayList). However, these are defined objects, and are not as syntactically easy to use as arrays.

In Python, there are no arrays, only lists with the best of all worlds. The lists are very easy to create, use, and manipulate. Here are a few examples of the fun things you can do with lists out of the box:

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
L6 = L3[1:] # L3 from index 1 to the end
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
{% endhighlight %}

<script src="//repl.it/embed/OAUD/1.js"></script>

Lists can also contain items of multiple types with no issue.

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
{% endhighlight %}

<script src="//repl.it/embed/OAVU/0.js"></script>

Once you learn the syntax for lists, you'll already know the syntax for strings! Easy as that :)

### Different Loops

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

However, the for loop and the while loop are basically the same thing. Python sees this, and took out the for loop. Instead you just have the while loop (which is practically identical to the Java while loop), and a for loop that is the same as Java's for each loop. Here's an example (from the previous section).

{% highlight python %}
L = [1,2,3]
s = 0
for item in L: # for each loop
	s += item
print(s)
{% endhighlight %}

<iframe width="800" height="500" frameborder="0" src="http://pythontutor.com/iframe-embed.html#code=L%20%3D%20%5B1,2,3%5D%0As%20%3D%200%0Afor%20item%20in%20L%3A%20%23%20for%20each%20loop%0A%09s%20%2B%3D%20item%0Aprint%28s%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=false&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

You can run this to see what it does step by step. Basically - the "for item in L" is telling the loop - "For each thing in L, call it item, and do the stuff indented under me." So first it sets item equal to 1, then 2, then 3.

If you want a for loop that just goes through a series of numbers, Python programmers use this function called range to do that.


{% highlight python %}
for i in range(1,10): # for each loop
	print(i)
{% endhighlight %}

<script src="//repl.it/embed/OAWf/1.js"></script>

Range is a special function in python that returns a list from the first argument to (not including) the last argument. So range(1,10) is the same as [1,2,3,4,5,6,7,8,9]. This allows us to have a for loop that's similar to Java's.

### Boolean Logic in English

This one is pretty quick, but worth mentioning here anyway. In Java, to combine booleans, you would have to use `||` for or, and `&&` for and. In Python, you literally use the words "and" and "or" to do the same things. Also, True and False are uppercase.

{% highlight python %}
print(True and False) # False
print(True or False) # True
{% endhighlight %}  

# Conclusion

I hope this article gave you a good overview of all the different things to expect when looking at Python code, so you wouldn't feel too left out. In the next part, I will write about how to actually get to writing some Python - with direct translations from what you know from Java!
