---
layout: post
title:  "Your Next Technical Interview Should be Solved with Python"
subtitle: "Why Python is the superior interviewing language"
date:   2017-11-06 23:56:45
categories: [Interviews, Python, Technical]
---

# Introduction

Ah coding interviews - 45 minute long bursts of time where an interviewer expects you to care about some esoteric problem, so you can show them how you REALLY think. During a coding interview, you’re normally given a wide choice of programming languages to use for solving the problem, usually between C++, Java, and Python. This is mostly because, unless you’re applying for a very specific role at a company, they don’t really care that you know the specifics of any one specific language. Rather - they care that you’re able to take a technical problem that is explained to you, come up with a solution, and then write code to implement that solution. In short, they want to know if you’ll be a good coworker to have at the company, who has good problem solving skills, and will be pleasant to work with. In that regard, language choice doesn’t matter too much, except for choosing the one that you’re most able to express yourself in. 

However, the language you choose does have consequences when it comes to implementing the solution, as different languages offer different methods of solving different problems, some easier than others. Especially for an interview where you have to write code on a whiteboard and there's no IDE to autofill your statements, the differences are uniquely noticeable. If you’re unsure which main language to practice in to perform your best during interviews and are given the option, I will have to suggest that you should use Python for your next interview, as it has very clear advantages (both in writing it and reading it) that sometimes almost feel like cheating when compared to others. 

# Brief Overview of Coding Interviews

If you're already well acquainted with coding interviews, you can skip this section. If you haven't had the joy of interviewing for a software engineering job in the past few years though, I'll give you a brief overview. The basic idea is that either through some software, over the phone, or in person, your interviewer will give you a description of a problem that should be solved with code. For example, they might ask you given a list of people's schedules, to write code to select when the best meeting time is. Another example might be more abstract, such as given a list of numbers to return all the different orderings (or permutations) of those numbers. The point of this exercise is to see how you turn a real life problem into code, what kind of data structures you use to wrangle the data, what kind of algorithm you use to get the answer, how you can turn the algorithm into real code, and just generally seeing how you think and behave when working on a problem. There is some debate into how useful/necessary they are (I'm personally of the opinion that they are useful), but that is not the topic of this post. Rather, they are a system that already exists, so I want to help you do these interviews the best you can. But... how can Python help?

# Reason 1: Succinctness

The first reason why I suggest using Python is that it is much more succinct in expressing simple coding statements. The whole philosophy behind Python is to make it as easy to read as it is to write. That shows when you're solving the programming puzzles that software companies love giving. Since these problems are normally contrived and mostly related to manipulating lists, strings, and other data structures, Python's simple and short syntax gives major advantages to manipulating those data types. When you are at a whiteboard with sweaty hands, trying to write code to use a hashmap, would you rather type something like this

{% highlight java %}
Map d = new HashMap<String, Integer>();
{% endhighlight %}

Or something like this?:

{% highlight python %}
d = {}
{% endhighlight %}

If you want to update a key in the hashmap/dictionary to add 1 to it, would you rather do:

{% highlight java %}	
d.put(key, d.get(key)+1);
{% endhighlight %}

Or:

{% highlight python %}
d[key]+=1
{% endhighlight %}

Last example - if you want to update a list where you cube every element, would you rather do:

{% highlight java %}
for (int i = 0; i<L.length();  i++){
	L.set(i, Math.pow(L.get(i), 3))
}
{% endhighlight %}

Or:

{% highlight python %}
L = [i**3 for i in L]
{% endhighlight %}

In short, Python allows for quick string and list manipulation (with the same basic syntax), quick dictionary creation and modification, and many other benefits. Some of these might not seem like a big difference now, but when you’re nervous and given a short time to write code, you don’t want to get stuck on the verbiage in creating a new map, or the necessities of looping through every element of a list. Once you have the idea of how to do the problem in your head, you want to just get the code on the whiteboard/online interview website ASAP, so that you can test, debug, and discuss the solution you’ve come up with. As engineers, we’re not used to writing things with pens, so every character helps you get it done faster and more efficiently. Additionally, sometimes you don't realize that your approach is wrong until you have it in code written down. Finishing your coding faster means getting to that realization quicker, so you can figure out what you need to change. Getting the code on the board fast is good, so you can spend less time on the implementation, and more time on followups or discussions. 

# Reason 2: Readability

The next reason I think it’s better to use Python in an interview is because it’s just more damn readable! Just the way the language is structured with whitespace instead of lots of curly braces and parentheses makes it a lot easier to synthesize and digest what you just wrote. When you're trying to find errors or issues with your code, it helps to have everything very expressly written, so that you can see where your issues will pop up, and catch them much quicker. All of the syntax that allows for things to be done much more succinctly also means less information for your brain to take in. The fewer .charAt or .containsKey methods you need to parse, the sooner you can see what you're doing wrong, and apply the fix.  Fewer lines also means fewer steps to debug to get to the root of an error you might have made. 

To illustrate my point, I’ll write up solutions to a few interview questions - how I would do them in Java, and how I would do them in Python. You can decide for yourself which would look better. I have done my best to keep the same logic, and not use any tricks that makes Python look much better, unless expressly noted. 

# Example Interview Questions
## Question 0:

Given a string, return true if it's a palindrome (the same backwards and forwards).
e.g. isPalindrone("bob") = true

Java:

{% highlight java %}
public static boolean isPalindrone(String s){
	for (int i=0; i<s.length(); i++){
		if (s.charAt(i) != s.charAt(s.length()-i-1)){
			return false;
		}
	}
	return true;
}
{% endhighlight %}  
 
Python

{% highlight python %}
def isPalindrone(s):
	for i in range(len(s)):
		if s[i] != s[len(s)-i-1]: return False
	return True
{% endhighlight %}  

The differences aren't so stark in this case, but it's still easier to read, and fewer method calls to write, with s.length() vs len(s) and s.charAt(i) vs s[i]. 

## Question 1:

Given a string, return the first letter which is not repeated in the string. These solutions also look similar to the common. 

E.g: firstNonRepeated(“tootie”) -> ‘i’ 

Strategy: Count number of times each character appears in the string. Then go through the string again and find the first letter which has a count of 1. 

Java:

{% highlight java %}
import java.util.*;
public static char firstNonRepeated(String s){
	HashMap<Character, Integer> lookup = new HashMap <Character, Integer>();
	for( int i = 0; i <= s.length()-1;i++) {
		char letter = s.charAt(i);
		if (!lookup.containsKey(letter)){
			lookup.put(letter,1);
		} else {
			lookup.put(letter,lookup.get(letter)+1);
		}
	}	 
	for (int j = 0; j<=s.length()-1;j++) {
		if(lookup.get(s.charAt(j))==1){
			return s.charAt(j);
		}
	}
	return ' '; 
}
{% endhighlight %}

That `lookup.add(letter,lookup.get(letter)+1);` would be a real pain to write out, wouldn't it...

Python:

{% highlight python %}
def first_non_repeated(s):
	d = {}
	for letter in s:
		if letter not in d: d[letter] = 1
		else: d[letter]+=1
	for letter in s:
		if d[letter]==1: return letter
	return ""
{% endhighlight %}
	
Or in Python if you remember defaultdict (which allows you to make a dictionary which has a default value if that key is not in the dictionary):

{% highlight python %}
from collections import defaultdict
def first_non_repeated(s):
	d = defaultdict(int)
	for letter in s:
		d[letter]+=1
	for letter in s:
		if d[letter]==1: return letter
	return ""
{% endhighlight %}
	
This looks similar to how the questions "Return the most frequently used number in the array, " and "Find the only element in an array that only occurs once." Either way, lots of time and space saved by writing the solutions like this, and much easier to trace for errors/logical problems. 
 
## Question 2:

Write the code to print out the nth fibonacci number, recursively but using memoization. By storing the previous answers in a hashmap/dictionary, we can turn an O(2^n) solution to an O(n) solution, since we don't have to recompute the same numbers over and over. 

Java

{% highlight java %}
public class fib(int n, Map<Integer, Integer> memory){
	if (n==0 || n==1){
		return n;
	}
	if (memory.containsKey(n)){
		return memory.get(n);
	}
	else{
		memory.put(n, fib(n-1, memory)+fib(n-2, memory));
		return memory.get(n);
	}
}
{% endhighlight %}

Python

{% highlight python %}
memory = {} # or you can make it a parameter like Java
def fib(n):
	if n==0 or n==1: return n
	if n in memory: return memory[n]
	else:
		memory[n] = fib(n-1)+fib(n-2)
		return memory[n]
{% endhighlight %}

## Question 3: 

Given a list of numbers, return all permutations (or possible orderings of the elements) of a list. E.g. : {1,2,3} as input will give you { {1,2,3}, {2,1,3} {2,3,1}, {3,2,1}, {1,3,2} and {3,1,2} }

If you haven't seen this problem before, the idea is to do it recursively. If your list has one item, then your list of permutations is just the one item. Otherwise, it's every location you can place the first item in the list in every permutation of the rest of the list. So to do it for {2,3}, you make the permutations of {3}, which is just { {3} }. Then, you insert 2 into every possible location of this, so either {2,3} or {3,2}. To do it with {1,2,3}, we get the permutations of {2,3}, which we already figured out is { {2,3}, {3,2} }, and then we insert 1 into every possible location for each of these. So from the first array we can get {1,2,3}, {2,1,3}, {2,3,1}. From the second array, we get {1,3,2}, {3,1,2}, and {3,2,1}. 

Java:

{% highlight java %}
public static List<List<Integer>> permutations(List<Integer> L){
	List<List<Integer>> permList = new ArrayList<List<Integer>>();
	if (L.size() < 2){ // For size 0/1, there's only 1 permutation
		permList.add(L);
		return permList;
	}
	List<Integer> tail = L.subList(1,L.size()); // everything but the first
	List<List<Integer>> others = permutations(tail);
	for (List<Integer> other : others){ // for each possible permutation
		// for each slot you can put the first element in
		for (int slot = 0; slot<=other.size(); slot++){ 
			// make a copy of the list
			List<Integer> newList = new ArrayList<Integer>(other);
			newList.add(slot, L.get(0));
			permList.add(newList);
		}
	}
	return permList;
}
{% endhighlight %}


My hand hurt for every time I thought about writing List\<List\<Integer\>\> =(
		

Python:

Quick note - in Python, if L is a list, L[i:] is everything in the list starting at index i to the end. L[:i] is everything from the beginning up to (not including) the item at index i. 

{% highlight python %}
def permutations(L):
	if len(L)<2: return [L] 
	others = permutations(L[1:]) # Everything but the first
	perm_list = []
	for other in others: # for each possible permutation
		# for each slot to place the first item, place it.
		for slot in range(len(others)+1): 
			new_list = other[:] # copy of others
			new_list.insert(slot, L[0])
			perm_list.append(new_list)
			# These three lines can also just be perm_list.append(other[:slot]+[L[0]] + other[slot:])
	return perm_list
{% endhighlight %}

# Final Thoughts

In all, I believe that using Python for interviews will help you write cleaner code, help you write it faster, help you debug it more efficiently, and help you move onto the more interesting parts of the problem that your interviewer has prepared, or discussion about how to further extend it. This advice I feel holds true for timed hackerrank challenges, phone screens, or in person whiteboard interviews, even if they don't utilize an actual whiteboard. If you're starting your interview practice, I highly recommend doing it in Python, so that you can fully utilize it come your next interview!  

Disclaimer - I've never actually given an interview before, I've just done a lot of them, and have a lot of thoughts about them. I also don't know any C++ (besides the little C I wrote for the one professor I had that loved C), but I doubt that it would disprove any of these points. If you have any thoughts, or any counterexamples, I'd love to hear them! Please leave a comment, or tweet me at @misingnoglic. This is just something that's been on my mind for a while, and that I wanted to write about. I hope this advice will be useful to you, and that it makes you curious to check out the awesome world of Python. 

Also, this is my first blog post ever! Unless you count [the buzzfeed article I wrote](https://www.buzzfeed.com/misingnoglic/you-wont-believe-what-computers-cant-compute-1j8kv) about CS theory. Please leave a comment below and let me know what you thought, and how I could improve. 


# FAQ:

Q: I don't know Python, but your post inspired me to learn it! How can I learn?

A: If you know another programming language, [this website](http://www.learnpython.org) is great for getting up to speed with the language in a few short lessons. If you want a more guided tutorial, you can also do the [Python Codecademy](https://www.codecademy.com/learn/learn-python) (which is great for quickly getting up to speed). After that, try doing some programming on [codingbat](codingbat.com/python), or if you're more math inclined, there's [Project Euler](https://projecteuler.net/). You can also try implementing previous programming assignments you've had in Python (look at my website's [resources section](http://www.aryaboudaie.com/resources) for some programming assignments I've made), or just doing your own fun little projects. The author of Cracking the Coding Interview also has solutions to all the problems in Python [here](https://github.com/careercup/CtCI-6th-Edition-Python), though they're not always the most pythonic. And who knows, maybe I'll make a post soon about how to learn Python quick from your Java skillset. 

Q: But I'm better/more comfortable with Java! Should I still use Python?

A: If you're more comfortable using another language, then you should probably stick to that language. This was more meant for people who may have taken a beginner Java/C++ class, and then want to use that as their interview language. The barrier of entry to Python isn't bad though, so check it out and see if you can ever see yourself being comfortable with it. But in the end, it is a very personal choice, and this is just my opinion. 

Q: But you can do <insert esoteric trick> in Java!

A: Sure, but I guess my point is that the way things are done in Python is the natural way that is expected of beginners and advanced programmers alike, so there's no need to learn any crazy esoteric tricks. 

Q: But if Python is easier, won't my interviewer think less of me for using it. 

A: In my opinion, Python is easier in all the superficial ways that don't show your programming ability. It's not like the thought process that comes with generating a solution becomes easier, using Python just means you have to worry less about the bureaucracy surrounding getting to the solution. Because of this, I strongly doubt that an interviewer will judge you for not going with a more verbose language. 

Q: Why not use Haskell/Lisp/Scheme/Scala/Clojure/<Insert some hipster language>, these problems are much more succinct in those languages!!

A. Ugh, it's another one of those functional people. You guys seem to be able to pop up everywhere. Listen, I get that to you, this seems beautiful, but to someone who's never done Haskell/Lisp before, this is just not readable at all (2, 3):

{% highlight haskell %}
permutations :: Eq a => [a] -> [[a]]
permutations [] = [[]]
permutations as = do a <- as
                     let l = delete a as
                     ls <- permutations l
                     return $ a : ls
{% endhighlight %}
		
{% highlight lisp %}		
(define (remove x lst)
  (cond
    ((null? lst) '())
    ((= x (car lst))(remove x (cdr lst)))
    (else (cons (car lst) (remove x (cdr lst))))))

(define (permute lst)
  (cond
    ((= (length lst) 1)(list lst))
    (else (apply append(map(lambda (i) (map (lambda (j)(cons i j))
                                            (permute (remove i lst))))lst)))))
{% endhighlight %}


Plus, most companies won't let you interview in a language that's not Java/Python/C++ unless that's the language at their company (e.g. Go at Google). Probably not good to harness your abilities in it just for interviews unless you're already a functional nerd, to which I say go crazy! I will never understand you. 

Q: Technical interviews are an awful system, that don't test for actual ability to do well in the job, and are just a glorified IQ test. 

A: This isn't a question, but thanks for telling me your opinion. This post isn't about the merits/detriments of the coding interview, but if you'd like to see me write about my thoughts on that please let me know. 


# Sources:
1. [Where I got some questions from](https://www.reddit.com/r/cscareerquestions/comments/20ahfq/heres_a_pretty_big_list_of_programming_interview/)
2. [Implementation of permutations in haskell](https://stackoverflow.com/questions/40097116/get-all-permutations-of-a-list-in-haskell)
3. [Implementation of permutations in Lisp](https://stackoverflow.com/questions/23635911/permutation-in-scheme-using-recursion)


