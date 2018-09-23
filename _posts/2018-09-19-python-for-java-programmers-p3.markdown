---
layout: post
title:  "Python for Java Programmers - Part 3 - Collections and Using Them"
subtitle: "Lists, Strings, Tuples, and Loops"
date:   2018-09-16 00:10:00
categories: [Java, Python, Technical, Educational]
---

**Note: If you haven't read [part 1](https://aryaboudaie.com/java/python/technical/educational/2017/11/13/python-for-java-programmers.html) or [part 2](https://aryaboudaie.com/java/python/technical/educational/2018/09/16/python-for-java-programmers-p2.html), please do so! This post will be building off the previous material, and I promise they're at least semi-entertaining/useful.**

# Introduction

Hello again! In part 1, we gave a bird's eye overview of the differences of Python and Java, which included lists. In part 2, I talked about functions, and included some stuff about lists, including why updating them inside of the function changes them outside the function. At this point, you may think you know all there is to know about lists. And... you really do know most of it. So instead of just talking about lists, I'm going to be talking all about the different ways to collect and store your data in your programs. And yes, this will include lists, but also a lot of other types of `collections`, as well as how to access the data in them with loops.

Data is one of the most important parts of programming - once you have the data you need, you need to somehow store it. The way you store your data could be the difference between clean code that runs efficiently, and slow ugly code that you'll cringe at several years later. Let's go through them, and then we can talk about when to use one over the other.

# Lists

## Basics

As a quick reminder, lists are the Python's most common object for data collection. They are similar to the `ArrayList` in Java, where they don't have a specified length, but the syntax for dealing with them is much nicer. There isn't anything like the Java `Array` built into Python, since lists are good enough most of the time (though [they do exist](https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.array.html) in the library NumPy). Python lists are even more accepting than ArrayLists, as they can be of any type, and objects of multiple types can be in a list.

{% highlight python %}
nums = [1, 3, 5]
{% endhighlight %}

To access an element of a list, you use the same indexing syntax as Java arrays. Python includes a useful extension of this, where you can also index starting from the back with negative indexing. The last item is index -1, the second to last item is index -2, etc...

{% highlight python %}
print(nums[1])  # 3
print(nums[-2])  # Also 3
{% endhighlight %}

So you can access each element two different ways. Here's a visualization of that:

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

This syntax will give you the elements of the list from `start` up until (not including) `stop`. So in this case, you will get back the list with the items at index 1, 2, 3, and 4, so [3, 5, 7, 9].

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

Just as a note: the slices you get back are copies of the original list, so if you modify them, you won't modify the original list. And there you have it, Python slices!

## Methods on lists.

Python lists have a few methods which are fairly useful. Note that any of these that change the list will also affect any variables that point to the same list. I'll list them below:

### append(x)

nums.append(x) will add the item x to the end of l.

{% highlight python %}
nums = [1, 2, 3]
nums2 = nums
nums.append(5)
print(nums)  # [1, 2, 3, 5]
print(nums2) # Also [1, 2, 3, 5]
{% endhighlight %}

### clear()

nums.clear() will clear nums, and all references to it.
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

nums.count(x) will count the number of times x is in nums.

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

nums.index(item) will give you the first index of `item` inside of `nums`.

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

I'll probably talk a bit more about this later, but that's the gist of it! There's an easier way to check if an item is just in a list too, which I'll discuss in a bit.

### insert(index, item)

nums.insert(index, item) will insert `item` into the index before `index`. Some examples:

{% highlight python %}
nums = [1, 2, 3]
nums.insert(0, 100)  # Insert 100 at the beginning.
print(nums)  # [100, 1, 2, 3]
nums.insert(2, 200)  # Insert 100 before index 2.
print(nums)  # [100, 1, 100, 2, 3]
nums.insert(2, 300)  # Insert 300 before index -1 (second to last item).
print(nums)  # [100, 1, 100, 2, 3, 300]
{% endhighlight %}

You might be thinking - but what if you want to add the item to the end? Well, just use `append`!

### pop(x=0)

`pop()` is an interesting method - it returns the last item of a list, but also removes it from the list. You can also give it an index, and it will instead pop that index. If you're an advanced reader, `pop` allows you to use a Python list like a stack or queue. If you don't know what those are, and don't mind a depressing example in capitalism: imagine you're a manager at a company whose policy for layoffs is "the last person to join will be the first person fired." You could have a Python program like this:

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

You can play with it here:

<iframe height="400px" width="100%" src="https://repl.it/@misingnoglic/Python-Employee-Firing-Pop-Example?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

Now imagine you had a list of people you wanted to hire, but didn't have room for. You have now a list of `potential_employees`, and whenever you have room to hire someone, you want to hire the person who's been waiting the longest. You could do `potential_employees.pop(0)` to remove them from potential_employees, and then add them to `employees`! That's a much better example! If you use a list in the `Last In First Out` (LIFO) model, it's called a `Stack`, and the list is used in the `First in First Out` (FIFO) model, it's called a Queue. These are good CS words to know, if you aren't already familiar.

### remove(item)

nums.remove(item) will remove the first instance of `item` from `nums`. This is fairly self explanatory.

{% highlight python %}
nums = [1, 2, 3]
nums.remove(2)
print(nums)  # [1, 3]
{% endhighlight %}

### reverse()

We'll get to this one later.

### sort()

`nums.sort()` will sort `nums` in place. This is different from the `sorted` function I talked about in part 2, since that returns a new list. With no parameters, `sort` will just sort the list from smallest to largest.

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
  if x%2==0:
    return x+100
  else:
    return x
nums.sort(key=sort_fn)
print(nums)  # [1, 3, 5, 2, 4, 6, 191]
{% endhighlight %}

This basically sorts the list as if every element x of of nums is sort_fn(x), but keeps each element the same. Another example: let's say you have a list of students, but you want to sort it by the last letter in the name to change things up a little. You could do something like this:

{% highlight python %}
names = ["Billy", "Parisa", "Sam"]
def sort_fn(name):
  return name[-1]

names.sort(key=sort_fn)
print(names)  # ['Parisa', 'Sam', 'Billy']
{% endhighlight %}

Finally, let's say you have a list of lists (#inception), and you want to sort them by their sum. You could just pass in the built-in function `sum` which returns the sum of a list.

{% highlight python %}
test_scores = [[90, 80, 75], [100, 150, 0], [200, 300, 0]]
test_scores.sort(key=sum)  # Sort by sum function
print(test_scores)  # [[90, 80, 75], [100, 150, 0], [200, 300, 0]]
{% endhighlight %}

`sort` is a great method for dealing with data, as it lets you have it ordered in a predictable way. In case you were wondering what Python's sorting algorithm is, it's not one you learn about normally in classes. It's called [timsort](https://en.wikipedia.org/wiki/Timsort), and it's named after Tim Peters, one of the earliest developers of Python itself. I hope one day I have an algorithm named after myself.

## Built In Functions for Lists

Besides the methods on lists, there are a lot of built in Python functions that operate on lists. I've already mentioned a lot of them, but I'll put them here for posterity's sake.

### in

`in` isn't actually a function, it's a keyword. You can use it to tell if an item is in a list, with surprisingly readable syntax.

{% highlight python %}
nums = [5, 7, 9, 11]
if 9 in nums:
  print("nums has a 9!")
else:
  print("no 9 in nums...")
{% endhighlight %}

`x in nums` will return a boolean that describes whether the variable `x` is in `nums` or not.

### sorted

The sorted() function is exactly like the `.sort()` method on lists, except that it returns a new list. It can also take the optional parameters `reversed` and `key`.

### len

len(nums) will just return the length of the list.

### max

max(nums) will  return the largest element of the list. Just like `sorted`, it can take a `key` function as a parameter to determine the `maximum` however you like.

### min

min(nums) will  return the smalled element of the list. Can also take a `key` parameter.

### sum

sum(nums) will return the sum of the list. Fairly straightforward.

And with all that, you have the built-in tools to use lists! Most calculations you need to do on lists can be done with these functions, for example:

{% highlight python %}
def average(nums):
  return sum(nums)/len(nums)

def range(nums):
  return max(nums)-min(nums)
{% endhighlight %}

There is one more feature of lists though that's too awesome to not mention.

## List Comprehensions

I'll just say this: list comprehensions are amazing. If you can master list comprehensions, you'll be able to take something that took several lines of Java to build, and do it in a single line. They're seriously quick, readable, and easy to start using once you get how they work. They have the added benefit of avoiding bugs as well! Ok - I think I've hyped them up enough - now what exactly do they do?

List comprehensions let you create a new list out of an old list, without using any sort of loops. For example: let's say we have a list of grades for a test, and we want to curve everyone up by 10 points. In Java, that would look something like this:

{% highlight java %}
// let's say we already have our list of grades
int [] new_grades = new int[grades.length];
for (int i = 0; i<grades.length; i++){
  grades[i]+=10;
}
{% endhighlight %}

Ok, "not bad" you say. But take a look at this:

{% highlight python %}
new_grades = [x+10 for x in grades]
{% endhighlight %}

Ok, let's break this down:
`for x in grades` is basically saying "for each thing in grades, call it x." And `x+10` is saying what to do to each of those x's. So basically, this is saying "for each element in grades, add 10 to it." Instead of writing the loop, you just say what you want to happen to each element, and it happens! No chance of an off by one error, or array out of bounds exception.

If you read the list comprehension as it looks, "x plus ten for x in grades," I think it will start to make sense.

TODO: add some examples.

Example: First element of every list in list.

List comprehensions can also help you filter down lists, based on criteria. For example: let's say you have a list of students, where each student is represented as a list of `[name, has_extra_time]`, where `has_extra_time` is a boolean
