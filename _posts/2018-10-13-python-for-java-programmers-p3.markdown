---
layout: post
title:  "Python for Java Programmers - Part 3 - Lists and More"
subtitle: "In Depth Guide to Lists, Strings, Tuples, and Loops"
date:   2018-10-13 00:10:00
categories: [Java, Python, Technical, Educational]
hide: true
---

**Note: If you haven't read [part 1](https://aryaboudaie.com/java/python/technical/educational/2017/11/13/python-for-java-programmers.html) or [part 2](https://aryaboudaie.com/java/python/technical/educational/2018/09/16/python-for-java-programmers-p2.html), please do so! This post will be building off the previous material, and I promise they're at least semi-entertaining/useful.**

# Table of Contents

* TOC
{:toc}

# Introduction

Hello again! In [part 1](https://aryaboudaie.com/java/python/technical/educational/2017/11/13/python-for-java-programmers.html), we gave a bird's eye overview of the differences of Python and Java, which included lists. In [part 2](https://aryaboudaie.com/java/python/technical/educational/2018/09/16/python-for-java-programmers-p2.html), I talked about functions, and included some stuff about lists, including why updating them inside of the function changes them outside the function. At this point, you may think you know all there is to know about lists. And... you really do know most of it. So instead of just talking about lists, I'm going to be talking all about the different ways to collect and store your data in your programs. And yes, this will include lists, but also a lot of other types of `collections`, as well as how to access the data in them with loops.

Data is one of the most important parts of programming - once you have the data you need, you need to somehow store it. Lists are by far the most common way to store data in Python, so it's worth it for you to take your time in understanding how they work and how to properly use them. Topics we will cover include list basics, how to slice and index lists, methods on lists, functions related to lists, how to create lists from other lists without loops (list comprehensions), how to loop over a list, and how lists are similar to strings and tuples.

Note: This blog is full of interactive embeds from [repl.it](repl.it) and [pythontutor.org](pythontutor.org). If you see large blank spaces, please refresh the page and don't switch tabs until it's fully loaded.

# Lists

## Basics

As a quick reminder, lists are the Python's most common object for data collection. They are similar to the `ArrayList` in Java, where they don't have a specified length, but the syntax for dealing with them is much nicer. There isn't anything like the Java `Array` built into Python, since lists are good enough most of the time (though [they do exist](https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.array.html) in the library NumPy). Python lists are even more accepting than ArrayLists, as they can be of any type, and objects of multiple types can be in a list, including lists and dictionaries.

{% highlight python %}
nums = [1, 3, 5]
crazy_list = [True, 1.0, 4, "test", [1, 2, 3], {'a': 'b'}]
{% endhighlight %}

Lists are ordered, meaning that the order you insert items into the liast matters. To access an element of a list, you use the same indexing syntax as Java arrays. Python includes a useful extension of this, where you can also index starting from the back with negative indexing. The last item is index -1, the second to last item is index -2, etc...

{% highlight python %}
nums = [1, 3, 5]
print(nums[1])  # 3
print(nums[-2])  # Also 3
{% endhighlight %}

So you can access each element two different ways. Here's a visualization of the regular and negative indexing:

{% highlight python %}
# Regular:   0  1  2  3  4  5   6
# Negative: -7 -6 -5 -4 -3 -2  -1               
full_list = [1, 3, 5, 7, 9, 11, 13]
{% endhighlight %}

## Slices

Python also lets you grab a "slice" of a list, or a specific part of a list. Here is the most basic way to do that:

{% highlight python %}
nums[start:stop]

# example:
#            0  1  2  3  4  5   6
full_list = [1, 3, 5, 7, 9, 11, 13]
print(full_list[1:5])  # [3, 5, 7, 9]
{% endhighlight %}

This syntax will give you the elements of the list from `start` up until (not including) `stop`. So in this case, `full_list[1:5]` get back the list with the items at index 1, 2, 3, and 4, so [3, 5, 7, 9].

You can also use negative indexes in your list, so nums[1:-1] will give you everything starting at the item at index 1, up until the last element.

{% highlight python %}
nums = [4, 5, 6, 7]
print(nums[1:-1])  # [5, 6]
{% endhighlight %}

If you want to start at the beginning, or go until the end, you can also leave parts of the "slice" blank. Here are examples of those:

{% highlight python %}
nums = [10, 11, 12, 13, 14, 15]
print(nums[:3])  # Start from the beginning until index 3. [10, 11, 12]
print(nums[3:])  # Start from index 3, go to the end. [13, 14, 15]
print(nums[:])   # Start from the beginning, go to the end (so the whole list.)
{% endhighlight %}

That last one may seem useless, but it's a common way to make a copy of a list, so don't be too weirded out if you see one of those.

Finally, list slicing actually has a third optional parameter for a "skip", which lets you skip every N element in a list. Here's some examples:

{% highlight python %}
nums = [10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20]

# Starts at 1, up to 7, and only every 2nd item.
# So indexes 1, 3, and 5.
print(nums[1:7:2])

# From the beginning to the end, every other number.
# So indexes 0, 2, 4, 6, 8, 10
print(nums[::2])

# Every element, but skipping backwards.
# This will reverse the list!
print(nums[::-1])
{% endhighlight %}

Here's an interactive REPL you can play with. I suggest clicking the "debugger" button on the left so you can go through it line by line and see what is going on.

<iframe height="500px" width="100%" src="https://repl.it/@misingnoglic/ParallelPrevailingBlock?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

Just as a note: the slices you get back are copies of the original list, so if you modify them, you won't modify the original list. And there you have it, Python slices!

## Methods on lists.

Python lists have a few methods which are fairly useful. Note that any of these that change the list will also affect any variables that point to the same list. I'll list them below:

### append(x)

nums.append(x) will add the item `x` to the end of `nums`.

{% highlight python %}
nums = [1, 2, 3]
nums2 = nums
nums.append(5)
print(nums)  # [1, 2, 3, 5]
print(nums2) # Also [1, 2, 3, 5]
{% endhighlight %}

### clear()

nums.clear() will clear nums of all its items.
{% highlight python %}
nums = [1, 2, 3]
nums.clear()
print(nums)  # []
{% endhighlight %}

### copy()

nums.copy() will `return` a copy of nums, so that any changes you make to the copy won't affect the original. This is one of the unique methods that will return a new object.
{% highlight python %}
nums = [1, 2, 3]
nums_new = nums.copy()
nums.append(5)
print(nums_new)  # [1, 2, 3]
{% endhighlight %}

Remember that this can also be done with `nums[:]`.

### count(x)

nums.count(x) will return the number of times x is in nums.

{% highlight python %}
#       X  X     X  X
nums = [1, 1, 2, 1, 1, 3]
print(nums.count(1))  # 4
{% endhighlight %}

### extend(new)

nums.extend(new_list) will add all of the elements from new_list into nums. Here's an example:

{% highlight python %}
nums = [1, 2, 3]
new = [4, 5, 6]
nums.extend(new)
print(nums)  # [1, 2, 3, 4, 5, 6]
{% endhighlight %}

### index(item)

nums.index(item) will return the first index of `item` inside of `nums`.

{% highlight python %}
nums = [1, 2, 3, 1, 2, 3]
print(nums.index(2))  # 1
{% endhighlight %}

If the item isn't inside of `nums`, the program will raise a `ValueError`. I'll quickly show you how you can write code to catch one of these, so you can use the .index() method without worrying that it will crash your whole program.

{% highlight python %}
nums = [1, 2, 3]
try:
  print(nums.index(4))
except ValueError:
  print("4 is not in nums")
{% endhighlight %}

I'll probably talk a bit more about exceptions later, but that's the gist of it! You can also use the `in` operator to check if an item is in the list safely (`in` is discussed later in the post).

### insert(index, item)

nums.insert(index, item) will insert `item` into the index before `index`. Some examples:

{% highlight python %}
nums = [1, 2, 3]
nums.insert(0, 100)  # Insert 100 at the beginning.
print(nums)  # [100, 1, 2, 3]
nums.insert(2, 200)  # Insert 200 before index 2.
print(nums)  # [100, 1, 200, 2, 3]
nums.insert(-1, 300)  # Insert 300 before index -1 (second to last item).
print(nums)  # [100, 1, 200, 2, 300, 3]
{% endhighlight %}

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=nums%20%3D%20%5B1,%202,%203%5D%0Anums.insert%280,%20100%29%20%20%23%20Insert%20100%20at%20the%20beginning.%0Anums.insert%282,%20200%29%20%20%23%20Insert%20200%20before%20index%202.%0Anums.insert%28-1,%20300%29%20%20%23%20Insert%20300%20before%20index%20-1%20%28second%20to%20last%20item%29.%0Aprint%28nums%29%20%20%23%20%5B100,%201,%20200,%202,%20300,%203%5D&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

You might be thinking - but what if you want to add the item to the end? Well, just use `append`!

### pop(x=0)

`pop()` is an interesting method - it returns the last item of a list, but also removes it from the list. You can also pass it an index, and it will instead pop that index.

{% highlight python %}
nums = [1, 2, 3, 4]
x = nums.pop()  # 4
print(nums)  # [1, 2, 3]
y = nums.pop(0)  # 1
print(nums)  # [2, 3]
{% endhighlight %}


If you're an advanced reader, `pop` allows you to use a Python list like a stack or queue. If you don't know what those are, and don't mind a depressing example in capitalism: imagine you're a manager at a company whose policy for layoffs is "the last person to join will be the first person fired." You could have a Python program like this:

{% highlight python %}
employees = []

def hire_employee(employees, employee):
  employees.append(employee)
  print(employee+" was hired.")


def fire_employee(employees):
  fired_employee = employees.pop()
  print(fired_employee+" was fired.")
  print("Leftover employees: ")
  print(employees)  # All but the last item
{% endhighlight %}

You can play with it here - try to match the print statements to the calls to pop and append.

<iframe width="1000" height="600" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=employees%20%3D%20%5B%5D%0Adef%20hire_employee%28employees,%20employee%29%3A%0A%20%20employees.append%28employee%29%0A%20%20print%28employee%2B%22%20was%20hired.%22%29%0A%0Adef%20fire_employee%28employees%29%3A%0A%20%20fired_employee%20%3D%20employees.pop%28%29%0A%20%20print%28fired_employee%2B%22%20was%20fired.%22%29%0A%20%20print%28%22Leftover%20employees%3A%20%22%29%0A%20%20print%28employees%29%0A%0Ahire_employee%28employees,%20%22John%22%29%0Ahire_employee%28employees,%20%22Mark%22%29%0Ahire_employee%28employees,%20%22Cassidy%22%29%0Ahire_employee%28employees,%20%22Hassan%22%29%0Ahire_employee%28employees,%20%22Cindy%22%29%0Afire_employee%28employees%29%0Ahire_employee%28employees,%20%22Victor%22%29%0Afire_employee%28employees%29%0Afire_employee%28employees%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

<!-- <iframe height="900px" width="100%" src="https://repl.it/@misingnoglic/Python-Employee-Firing-Pop-Example?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe> -->

Now imagine you had a list of people you wanted to hire, but didn't have room for. You have now a list of `potential_employees`, and whenever you have room to hire someone, you want to hire the person who's been waiting the longest. You could do `potential_employees.pop(0)` to remove them from the front of potential_employees, and then add them to `employees`! That's a much better example! If you use a list in the `Last In First Out` (LIFO) model, it's called a `Stack`, and the list is used in the `First in First Out` (FIFO) model, it's called a `Queue`. These are good CS words to know, if you aren't already familiar. If you're studying for software interviews, correct usage of pop() will be extremely helpful in certain problems!

### remove(item)

nums.remove(item) will remove the first instance of `item` from `nums`. This is fairly self explanatory.

{% highlight python %}
nums = [1, 2, 3]
nums.remove(2)
print(nums)  # [1, 3]
{% endhighlight %}

### sort()

`nums.sort()` will sort `nums` in place. This is different from the `sorted` function I talked about in part 2, since `sorted` returns a new list while `sort` just modifies the list it was called on. With no parameters, `sort` will just sort the list from smallest to largest.

{% highlight python %}
nums = [8, 5, 6, 7, 1, 2, 3]
nums.sort()
print(nums)  # [1, 2, 3, 5, 6, 7, 8]
{% endhighlight %}

`sort` can take an optional argument `reversed`, that when set True will sort the list from largest to smallest.

{% highlight python %}
nums = [8, 5, 6, 7, 1, 2, 3]
nums.sort(reversed=True)
print(nums)  # [8, 5, 6, 7, 1, 2, 3]
{% endhighlight %}

`sort` can also take another optional argument, `key`, which is a function that you sort the list based on. For example, if you have some weird ranking where even numbers are worth 100 more than if they were odd, you could sort your list like this:

{% highlight python %}
nums = [1, 2, 3, 4, 5, 6, 191]

def sort_fn(x):
  # Add 100 to evens
  if x%2==0:
    return x+100
  else:
    return x

nums.sort(key=sort_fn)
print(nums)  # [1, 3, 5, 2, 4, 6, 191]
{% endhighlight %}

This basically sorts the list as if every element x of nums is sort_fn(x), but keeps each element the same. Another example: let's say you have a list of students, but you want to sort it by the last letter in the name to change things up a little. You could do something like this:

{% highlight python %}
names = ["Billy", "Parisa", "Sam"]
def sort_fn(name):
  # return last letter
  return name[-1]

names.sort(key=sort_fn)
# Sorts the list by the last letter.
print(names)  # ['Parisa', 'Sam', 'Billy']
{% endhighlight %}

<iframe height="800px" width="100%" src="https://repl.it/@misingnoglic/SkeletalSubduedVerification?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

Finally, let's say you have a list of lists (*#inception*), and you want to sort them by their sum. You could just pass in the built-in function `sum` which returns the sum of a list.

{% highlight python %}
test_scores = [[200, 300, 0], [90, 80, 75], [100, 150, 0]]
test_scores.sort(key=sum)  # Sort by sum function
print(test_scores)  # [[90, 80, 75], [100, 150, 0], [200, 300, 0]]
{% endhighlight %}

<iframe height="400px" width="100%" src="https://repl.it/@misingnoglic/SelfreliantTealKnowledge?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

`sort` is a great method for dealing with data, as it lets you have it ordered in a predictable way. In case you were wondering what Python's sorting algorithm is, it's not one you learn about normally in classes. It's called [timsort](https://en.wikipedia.org/wiki/Timsort), and it's named after Tim Peters, one of the earliest developers of Python itself. I hope one day I have an algorithm named after myself.

## Built In Functions for Lists

Besides the methods on lists, there are a lot of built in Python functions that are related to lists. I've already mentioned a lot of them, but I'll put them here for posterity's sake.

### in

`in` isn't actually a function, it's a keyword (like `and` or `if`), but this was the best section for it. You can use it to tell if an item is in a list, with surprisingly readable syntax.

{% highlight python %}
nums = [5, 7, 9, 11]
if 9 in nums:
  print("nums has a 9!")
else:
  print("no 9 in nums...")
{% endhighlight %}

`x in nums` will return a boolean that describes whether the variable `x` is in `nums` or not. This is one of my favorite python things to show new programmers, since it's amazing how readable this syntax is once you get used to it.

### range(stop)

`range()` is definitely one of the most important list functions, as it can create lists of numbers in a certain range, meaning you don't have to write the loops to do it. `range()` is a function that returns an "range object", which is kind of like a list that isn't evaluated until you actually need the item you're asking from it. It basically works the same as a list in terms of indexing and looping. This type of object is called an `iterable`, meaning it can be iterated over.

`range(stop)` will return an iterable from 0 up until the stop number. Just like list indexing, you can also give it a start, and a skip. For visuals I'll convert them to lists, but when you use them you mostly won't have to:

{% highlight python %}
>>> list(range(5))
[0, 1, 2, 3, 4]
>>> list(range(1, 5))
[1, 2, 3, 4]
>>> list(range(20, 100, 5))
[20, 25, 30, 35, 40, 45, 50, 55, 60, 65, 70, 75, 80, 85, 90, 95]
>>> list(range(10,0,-1))
[10, 9, 8, 7, 6, 5, 4, 3, 2, 1]
{% endhighlight %}

If you give range() one parameter, it will return the range object from 0 until the parameter (not including the parameter). If you give it two parameters, it will return an object starting from the first parameter up to the second parameter. If you give it three parameters, it will use the third one as a `skip`, so it will skip by that number for each entry. So `range(1, 5)` will give the numbers `[1, 2, 3, 4]`, and `range(20, 100, 5)` will give all the numbers from 20 up to 100, skipping by 5 every time.

If you don't convert it into a list, a range object will just show you this:

{% highlight python %}
>>> x = range(100)
>>> print(x)
range(0, 100)
{% endhighlight %}

So it hasn't actually computed anything. So why did the creators of Python decide to make range lazy? Let's say you wanted to do something for every number from 0 to a billion. If range() wasn't lazy, it would have to store each item from 0 to a billion in a list somewhere in memory, which would be highly inefficient. It's much easier to just not get the number until you need it, and then convert it into a list if you really need it as a list. So if anyone ever tells you being lazy is bad, tell them that sometimes it's the best policy :)

<iframe height="400px" width="100%" src="https://repl.it/@misingnoglic/InexperiencedCornyInstances?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

(Note, in the 2.x version of Python, range() returned a list, and you needed to use xrange() to return a range object).

### reversed(nums)

Sort of like range, `reversed` takes in a list, and returns an `iterator` with the reverse of a list. an `iterator` is another kind of lazy object, that you can look over. I'll talk more about looping at the end of this post, but here's an example:

an iterator for the reverse of the list. So you can loop over it as normal, or turn cast it into a list like this:
{% highlight python %}
nums = [1, 2, 3]
for i in reversed(nums):
  print(i)  # 3, 2, 1  
{% endhighlight %}

<iframe height="300px" width="100%" src="https://repl.it/@misingnoglic/ZestyThreadbareArraylist?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

If you want to just get a reversed list, remember you can always just do `nums[::-1]`

### sorted()

The sorted() function is exactly like the `.sort()` method on lists, except that it returns a new list. It can also take the optional parameters `reversed` and `key`.

{% highlight python %}
nums = [1, -3, 2, 5]
new_nums = sorted(nums)
print(new_nums)  # -3, 1, 2, 5
print(sorted(nums, reverse=True))  # 5, 2, 1, -3
# abs is the built in absolute value function
print(sorted(nums, key=abs))  # 1, 2, -3, 5
{% endhighlight %}

<iframe height="400px" width="100%" src="https://repl.it/@misingnoglic/BogusShoddyCosmos?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

### len()

len(nums) will just return the length of the list.

{% highlight python %}
nums = [1, -3, 2, 5]
print(len(nums))  # 4
{% endhighlight %}


### max()

max(nums) will  return the largest element of the list. Just like `sorted`, it can take a `key` function as a parameter to determine the `maximum` however you like. For example, you can pass `abs` (the absolute value function) if you want the number with the largest absolute value.

{% highlight python %}
nums = [1, -7, 2, 5]
print(max(nums))  # 5
print(max(nums, key=abs))  # -7
{% endhighlight %}

<iframe height="300px" width="100%" src="https://repl.it/@misingnoglic/RoughKnowingPostscript?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

### min()

min(nums) is the mirror of `max()`, where it will return the smallest element of the list. It can also take a `key` parameter.

### sum()

sum(nums) will return the sum of the list. Fairly straightforward.

And with all that, you have the built-in tools to use lists! Most calculations you need to do on lists can be done with these functions, for example:

{% highlight python %}
def average(nums):
  return sum(nums)/len(nums)

def range(nums):
  return max(nums)-min(nums)
{% endhighlight %}

<iframe height="500px" width="100%" src="https://repl.it/@misingnoglic/SwiftIdenticalSyntax?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

There is one more feature of lists though that's too awesome to not mention though, so hold on tight!

## List Comprehensions

I'll just say this: list comprehensions are amazing and beautiful. If you can master list comprehensions, you'll be able to take something that took several lines of Java to build, and do it in a single line. They're seriously quick, readable, and easy to start using once you get how they work. They have the added benefit of avoiding bugs as well! Ok - I think I've hyped them up enough - now what exactly do they do?

### Mapping

List comprehensions let you create a new list out of an old list, without using any sort of loops. If you give the list comprehension some kind of function to `map` onto the list, you'll get the new list. For example: let's say we have a list of grades for a test, and we want to curve everyone up by 10 points. In Java, that would look something like this:

{% highlight java %}
// let's say we already have our list of grades
int[] new_grades = new int[grades.length];
for (int i = 0; i<grades.length; i++){
  grades[i]+=10;
}
{% endhighlight %}

Ok, "not bad" you say. But take a look at this:

{% highlight python %}
new_grades = [x+10 for x in grades]
{% endhighlight %}

<iframe height="270px" width="100%" src="https://repl.it/@misingnoglic/BiodegradableRotatingExecutable?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

Ok, let's break this down:
`for x in grades` is basically saying "for each thing in grades, call it x." And `x+10` is saying what to do to each of those x's. So basically, this is saying "for each element in grades, add 10 to it." Instead of writing the loop, you just say what you want to happen to each element, and it happens! No chance of an off by one error, or array out of bounds exception.

![Explanation of list comprehension](/assets/blog_images/pythonjava3/list_comp.png)

If you read the list comprehension as it looks, "x plus ten for x in grades," I think it will start to make sense.

Example: You have a list of grades out of 100, and you want to turn it into a list of decimal grades:

{% highlight python %}
new_grades = [x/100 for x in grades]
{% endhighlight %}

<iframe height="250px" width="100%" src="https://repl.it/@misingnoglic/FancyFrequentChemistry?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

You can also use the range() function in list comprehensions to create a new list from an iterator returned by range. For example, if you want all of the numbers from 1 to 100 squared, you can do:

{% highlight python %}
squared = [x*2 for x in range(10)]
{% endhighlight %}

Your expression doesn't even have to involve `x`. For example, if you wanted a list of 100 zeroes, you could do something like this:

{% highlight python %}
zeroes = [0 for x in range(100)]
{% endhighlight %}

<iframe height="350px" width="100%" src="https://repl.it/@misingnoglic/AlertWorldlyReciprocal?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

Notice how the function part doesn't involve `x`, even though we called each item in the list `x`. You don't need to use your variable in your list comprehension, if the returned list doesn't need it. As another example, let's get the last character in a list of strings.

{% highlight python %}
names = ["Billy", "Parisa", "Sam"]
print([name[-1] for name in names])  # [y, a, m]
{% endhighlight %}

### Filtering

Lists comprehensions can also be used to filter lists based on some criteria. Here's a toy example - if you have a list, and you want to get all of the even numbers from that list:

{% highlight python %}
nums = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
even_nums = [x for x in nums if x%2==0]
{% endhighlight %}

<iframe height="400px" width="100%" src="https://repl.it/@misingnoglic/FelineIndigoMass?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

Or all of the numbers greater than 50:

{% highlight python %}
big_nums = [x for x in nums if x>50]
{% endhighlight %}

![Explanation of list comprehension with filter](/assets/blog_images/pythonjava3/list_comp2.png)

To break this down:

- `x for x in nums` just means to return just x, not some modification of x. If it was `x+2 for x in nums`, it would be adding 2 to each number.
- `if x > 50` will only put the numbers in the list if they are greater than 50. Note that the statement here should be some boolean statement that is `True` if you want to keep the item.

So the full form of the list comprehension is as follows (though the `if` part is optional):

{% highlight python %}
new_list = [manipulation(item) for item in old_list if some_criteria(item)]
{% endhighlight %}

Where `manipulation(item)` is some function that takes in `item` and returns something new, and `some_criteria` is some function that returns a boolean. You don't need to create a new function - as you see from the above examples you can just put the expressions in directly, but you can also use functions for more complicated manipulations or filters.

A complex example - let's get the squared value of all even numbers.

{% highlight python %}
crazy_list = [x**2 for x in nums if x%2==0]
{% endhighlight %}

You can also use `range` in a list comprehension with filtering. For example, if you had a function `is_prime` which returned `True` if a number is prime, you could do something like this to get all the primes from 1 to 1000:

{% highlight python %}
primes = [x for x in range(1,1000) if is_prime(x)]
{% endhighlight %}

<iframe height="400px" width="100%" src="https://repl.it/@misingnoglic/EssentialClientsideSynergy?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

### Going through nested lists.

A lot of times while programming, you will be dealing with functions and APIs that return nested lists to you. List comprehensions allow you to navigate through those lists and return the data you want in the format you want it in. For example, let's say you have a list of students, where each student is represented by a list of two items, their name and their grade in the class. So something like this:

{% highlight python %}
students = [["Sam", 80], ["Carly", 90], ["Dmitri", 65], ["Parisa", 100]]
{% endhighlight %}

If you want to get a list of all the students whose grades are under a 70, you can write a list comprehension like this:

{% highlight python %}
failing_students = [student[0] for student in students if student[1]<70]
{% endhighlight %}

Remember that students is a list of lists, so `student` in each case will be a list, where student[0] is the name and student[1] is the grade. To make this more clean, you can even do something like this:

{% highlight python %}
failing_students = [name for name, grade in students if grade<70]
{% endhighlight %}

<iframe height="400px" width="100%" src="https://repl.it/@misingnoglic/MasculineGlamorousComputer?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

Python lets you assign multiple variables in one line, kind of like this:

{% highlight python %}
x, y = [1, 2]
print(x)  # 1
print(y)  # 2
{% endhighlight %}

So by doing `for name, grade in students`, it's taking each list of two items in `students` and assigning the first item to `name` and the second item to `grade`. This second version is more `pythonic`, since it's more explicit and easier to read and know what's going on.

In the end, list comprehensions are a great tool that you should really work to master, as they'll eliminate many issues involving loops, and they'll elevate your code to the next level. They're also [great for coding interviews](https://aryaboudaie.com/interviews/python/technical/2017/11/06/python-for-interviews.html)!

# Iterators and Looping

Now that you have lists, and I've taught you how to use them without loops, you may still be wondering "well how do I actually loop through the list though?" Sigh... some people never break out of their Java habits.

But seriously, before you write a loop, think "can I do this without a loop?" If the answer is yes, then do it without a loop. However, if your problem is not simple enough to do in a list comprehension, then you may well use a loop.

Python has two kinds of loops. The first one, the `while` loop, works exactly like the Java while loop, except you don't need parentheses. You put a boolean statement next to the `while` keyword, and the loop will run until that is not true anymore. Here's a simple example:

{% highlight python %}
x = 0
while x<10:
  print(x)
  x += 1
{% endhighlight %}

<iframe width="800" height="300" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=x%20%3D%200%0Awhile%20x%3C10%3A%0A%20%20print%28x%29%0A%20%20x%20%2B%3D%201&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=true&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

This loop has the same issue as Java's, where if you're not careful, your loop can potentially go on forever (e.g. if I forgot to add `1` to `x` every time). There's not much more to say about this kind of loop. Note that there isn't a `do while` loop in Python.

The second kind of loop is the `for` loop. This kind of loop acts like the `for each` loop in Java:

{% highlight java %}
for (int num : nums){
  System.out.println(num);
}
{% endhighlight %}

The Python one is very similar. Here is the syntax:

{% highlight python %}
for x in nums:
  print(x)
{% endhighlight %}

Super simple, and readable right? The `for` loop takes any iterable object (like a list, range, string, etc...) and loops over each item. Just like the list comprehension, if you have a list (or any iterator), you can assign each item to a variable name, and then do something for each item in the list. In the above case, it will print every item of `nums`.

It helps to read this straight on, so "for [each] x in nums, print x."

You might wonder why there's nothing like the regular `for` loop in Java, like this:

{% highlight java %}
for (int i = 0; i<10; i++){
  System.out.println(i);
}
{% endhighlight %}

The reason is that you can mostly handle anything you need to do with these two kinds of loops, plus list comprehensions. If you want to loop through all the numbers from 0 to 10, you can do something like this:

{% highlight python %}
for i in range(10):
  print(i)  # prints 1-10
{% endhighlight %}

Or if you really need the indexes of items in the list, you can do something like this:

{% highlight python %}
nums = [1, 2, 3, 4, 5]
for i in range(len(nums)):
  if i>0:
    # Print each item plus the number before it.
    print(nums[i]+nums[i-1])
{% endhighlight %}

<iframe height="700px" width="100%" src="https://repl.it/@misingnoglic/EagerThunderousAxis?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

`range(len(list_name))` is a good pattern to remember for looping through each index of a list. Remember, since range() returns an iterable, you do not need to convert it back to a list.

If you need both the index and the item, you can use the `enumerate` function, which gives you both in a more readable format. Here's an example:

{% highlight python %}
def index_of_first_even(nums):
  for index, num in enumerate(nums):
    if num%2==0: return index
  return -1  # Not found

x = index_of_first_even([1, 3, 6, 4])  # returns 2
{% endhighlight %}

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=def%20index_of_first_even%28nums%29%3A%0A%20%20for%20index,%20num%20in%20enumerate%28nums%29%3A%0A%20%20%20%20if%20num%252%3D%3D0%3A%20return%20index%0A%20%20return%20-1%20%20%23%20Not%20found%0A%0Ax%20%3D%20index_of_first_even%28%5B1,%203,%206,%204%5D%29%20%20%23%20returns%202&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

If you want to loop over two lists of equal length at the same time, instead of using the indexes, you can use the `zip` function, which zips two lists together.

{% highlight python %}
# Using indexes
nums1 = [1, 2, 3]
nums2 = [10, 20, 30]
for i in range(len(nums1))
  print(nums1[i]+nums2[i])
{% endhighlight %}

{% highlight python %}
# Using zip (more readable)
nums1 = [1, 2, 3]
nums2 = [10, 20, 30]
for n1, n2 in zip(nums1, nums2):
  print(n1+n2)
{% endhighlight %}

Or even as a list comprehension, to store the new list:

{% highlight python %}
nums1 = [1, 2, 3]
nums2 = [10, 20, 30]
sums = [n1+n2 for n1, n2 in zip(nums1, nums2)]
{% endhighlight %}

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=nums1%20%3D%20%5B1,%202,%203%5D%0Anums2%20%3D%20%5B10,%2020,%2030%5D%0Afor%20n1,%20n2%20in%20zip%28nums1,%20nums2%29%3A%0A%20%20print%28n1%2Bn2%29%0Asums%20%3D%20%5Bn1%2Bn2%20for%20n1,%20n2%20in%20zip%28nums1,%20nums2%29%5D%0Aprint%28sums%29%0A&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

<iframe height="400px" width="100%" src="https://repl.it/@misingnoglic/MeatyShrillMisrac?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

Python really tries hard to give you the tools to loop through a list without having to use the indexes, to avoid messy code and hard to catch errors. Sometimes they're necessary, but make sure they are before looping through `range(len(nums))`.

In the end, if you wanted to make a list out of an old list, you could do something like this:

{% highlight python %}
nums = [1, 3, 3, 4, 5]
new_nums = []
# each i from 0 to length of nums
for i in range(len(nums)):
  new_nums.append(nums[i]*10)
{% endhighlight %}

But isn't it much nicer to write the equivalent:

{% highlight python %}
nums = [1, 3, 3, 4, 5]
new_nums = [x*10 for x in nums]
{% endhighlight %}

You can even combine list comprehensions with functions like `sum` and `max` to avoid these loops. Before writing a loop, make sure you can't do the same thing with range and a list comprehension. And when writing a loop, avoid using indexes if at all possible!

# List like objects.

To conclude this post, there are a few objects that behave very similarly to lists, and are worth going through here.

## Tuples

The first similar object is the `tuple`. The tuple is like a list, but it is `immutable`, meaning its contents cannot be changed or added to once it's created. In practice, this means that you cannot append to it, and you cannot change its items at any index. You define it with parentheses. For example, if you wanted to represent a point on an x, y plane, you could do so with tuples, where the first item is the x coordinate, and the second item is the y coordinate.

{% highlight python %}
point = (3, 2)
{% endhighlight %}

Actually, you don't even need the parentheses. This is equivalent:

{% highlight python %}
point = 3, 2
{% endhighlight %}

This is also useful in functions when you want to return two things.

{% highlight python %}
def complex_function():
  ...
  return answer1, answer2
{% endhighlight %}

This will return a tuple of (answer1, answer2). Generally you want your functions to just do one thing, but there are times that it's nicer to return two things (for example if you're doing some intense computation that you don't want to redo).

Tuples support the same slicing as Python lists, and can be passed into a for loop as well. Use them like you would any other variables, but when that idea needs to contain multiple parts (kind of like an object without methods). You can also always convert a list to a tuple using the `tuple`, or a tuple to a list using the `list` function.

{% highlight python %}
t = 1, 2, 3, 4, 5
print(len(t))  # 5
print(t[0])  # 1
print(t[-1])  # 5
print(t[1:-1])  # (2, 3, 4)
print(t.count(2))  # 1 (1 instance of 2)
for x in t:
  print(x)
print(list(t))  # [1, 2, 3, 4, 5]
print(6 in t)  # False
t[0] = 5  # TypeError: 'tuple' object does not support item assignment
{% endhighlight %}

<iframe height="400px" width="100%" src="https://repl.it/@misingnoglic/BeigePowerfulRuntimeenvironment?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

Tuples are great when you want to state that the data you're returning is not to be modified or appended to, and should be treated as a constant value, such as a tuple that represents a point in space.

## Strings

The other type of object in Python that's similar to a list is a String, which I won't describe in too much detail. This makes sense from a design standpoint, since what are strings but just an object that contains a list of single characters! But in Java, `Arrays` and `Strings` have completely different methods on them! You have to remember that arrays use `.length`, strings use `.length()`, and Lists use `.size()`. Additionally, for Java Strings, you have to use `.charAt()` to get the character at a certain index, or `.substring()` to get a substring. With Python, it's the same syntax as a list! You index the same way, slice the same way, even compare them in the same way with `==`. This is great, since it means you only have to learn one syntax! The only difference is like the tuple, strings are immutable (just like Java).

{% highlight python %}
>>> s = "Hello World"
>>> "Hello" in s
True
>>> s[:5]
'Hello'
>>> s.lower()=="hello world"
True
>>> for letter in s[:5]: print(letter)

H
e
l
l
o
>>> s.count("o")
2
{% endhighlight %}

Note that strings can be single quotes, or double quotes. Multiline strings can be three single quotes or three double quotes as well, you just have to be consistent. Note that multiline comments and docstrings are just regular strings.

{% highlight python %}
>>> s = '''
This is a very
long and large string
'''

def sq1(x):
  '''
  This function takes in a number and returns
  its squared value plus 1.
  '''
  return x**2 + 1
{% endhighlight %}

### String Methods

Strings also have their own methods that are useful for string manipulation, like `.upper()` and `.lower()`. You can see the full list of those [here](https://www.programiz.com/python-programming/methods/string). Here are some fun examples, whose results are fairly self explanatory. Note that they don't modify the string (as the string is immutable), but they instead return a new string.

{% highlight python %}
>>> s = "Hello world"
>>> s.upper()
'HELLO WORLD'
>>> s.lower()
'hello world'
>>> s.swapcase()
'hELLO WORLD'
>>> s.replace('o', '0')
'Hell0 w0rld'
>>> s.startswith('Hell')
True
>>> s.title()
'Hello World'
{% endhighlight %}

These string methods are great for dealing with user input, or just formatting strings in a way that makes them nicer to look at.

Probably the most useful string function that I know of is `split`, which splits a string into a list, based on whatever separator you give it. If you don't give split a parameter, it just splits on the space. The `split` method allows you to iterate through a string, searching for certain words or phrases.

{% highlight python %}
>>> s = "This is a long sentence"
>>> s.split()
['This', 'is', 'a', 'long', 'sentence']
# You can also split on characters besides a space
>>> s.split("s")
['Thi', ' i', ' a long ', 'entence']
# Sort the words based on length
>>> sorted(s.split(), key=len)
['a', 'is', 'This', 'long', 'sentence']
>>for word in s.split():
>>  print(word.swapcase())
tHIS
IS
A
LONG
SENTENCE
{% endhighlight %}

Remember that the return value of the `input` function is a string. You can combine `split` with list comprehensions to get all kinds of input though!

{% highlight python %}
input_str = input("Enter several numbers, separated by spaces: ")
nums = [int(x) for x in input_str.split()]
{% endhighlight %}

<iframe height="400px" width="100%" src="https://repl.it/@misingnoglic/RundownSplendidLock?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

Think about how annoying that would be with the Java scanner!

### Joining a List Into a String

Splitting a string into a list is fairly intuitive, but turning a list back into a string isn't, so I'll show you the preferred method for that. If you want to turn `["Hello", "World"]` into `"Hello World"`, you have to do something like this.

{% highlight python %}
words = ["Hello", "World"]
combined = " ".join(words)
print(combined)  # "Hello World"
{% endhighlight %}

Basically, you're taking the space string, and joining every word in the list based on it. I know it seems like it would make more sense to have the join method on the list instead of the string, but that's just the way it is. [Here](https://stackoverflow.com/questions/493819/python-join-why-is-it-string-joinlist-instead-of-list-joinstring) is the real reason, in case you are curious. Note that this is more space efficient than writing a loop to create a string, so interviewers love to see stuff like this. I know it's a strange syntax at first, but you will get used to it.

### Adding Variables to Strings

A common thing to want to do with Python is add variables to strings, so you can create some complex strings. I'll show you four ways to do this, from the best to the worst.

The easiest way to do this is with f strings, a fairly new feature introduced to Python.

{% highlight python %}
num = 4
s = f"{num} squared is {num**2}"
print(s)  # 4 squared is 16
{% endhighlight %}

Simply just put an `f` in front of the string (to signify that it's a format string), and then place your variables into the curly braces. Python will automatically format the string for you. This is amazing, but unfortunately this is only supported in Python 3.6 or above, so people with older versions of Python won't be able to run it.

Another common way is by manually calling the format function like this:

{% highlight python %}
num = 4
s = "{} squared is {}".format(num, num**2)
print(s)  # 4 squared is 16
{% endhighlight %}

Basically you just put `{}` wherever you want to place your variable, and then call `.format` on the string, placing each variable in order. Definitely not as nice, but you'll see this a lot when writing Python.

You can also use the printf formatting that's common with other programming languages like this:

{% highlight python %}
num = 4
s = "%d squared is %f" % num, num**2
print(s)  # 4 squared is 16
{% endhighlight %}

This is definitely not as nice, so I won't waste too much time explaining them. You can read about this kind of formatting [here](https://docs.python.org/3/library/stdtypes.html#old-string-formatting).

Finally, the clunkiest way you can do it is just by converting your variables to strings and adding them together.

{% highlight python %}
num = 4
s = str(num)+" squared is "+str(num**2)
print(s)  # 4 squared is 16
{% endhighlight %}

Strings are super useful, especially for reading files and user input, and Python makes them so pleasant to work with! I'll talk more about files, but this post is getting pretty long already!

# Conclusion

I know this was a LOT to take in, but I promise it all gets easier with practice. You definitely don't need to memorize all of this information about lists, tuples, strings, and loops, but as you program more and more in Python, it will all become second nature.

I hope this deep dive into lists was helpful, and has allowed you to more appreciate the wonderful syntax Python gives when dealing with data. In the next part, I'll talk about other kinds of objects used to store data, and some of their tradeoffs. Please [sign up for my mailing list](https://goo.gl/forms/jzaFhUpZ6x17oOJh2) to be notified when I post the next part. Additionally, please leave a comment and share with your friends if you found this useful.

Thank you everyone!
