---
layout: post
title:  "How I used Python to buy an out of stock Costco stand mixer and be a good boyfriend"
subtitle: "A story telling tutorial about Python web scraping."
date:   2020-07-05 00:10:00
categories: [Python, Technical, Educational]
hide: false
---

# Table of Contents

* TOC
{:toc}

# Prelude

So this whole story started because my girlfriend asked me for a KitchenAid
stand mixer for her birthday. We saw that Costco had a really nice one on sale
for $90 off, which was enough to trigger my "we need to get that price no matter
what it takes" instinct. Unfortunately, on the first day the item was available, it was sold out in-store and online. I tried calling every day to see if they
would get it back, but every day they said they had no more. One day I called,
and the employee mentioned that he saw it available online, which surprised me
since I've checked and it previously wasn't available. This is when I realized
that it must be going in and out of stock, and it would be the perfect
opportunity to write a script to automate the checking for me.

As with most web scraping projects, this one got pretty messy. Whenever I see technical blogs, I always think "wow, I could have never thought of that." This blog post is designed not just to tell you what I did, but how I got to my final code, so that you can learn how you could come up with a similar solution to the problem. We're gonna go through a journey of APIs, HTML parsing, and tons of Python.

![XKCD comic about automation](https://imgs.xkcd.com/comics/automation_2x.png)

# The Problem

The first thing I like to do when writing code is to abstractly think about what
I need to make happen. Surprisingly this isn't something that just intro CS
professors make you do, but a good way to problem solve. So what did I want
exactly? I wanted code that would do the following:

- Load the Costco product page.
- Determine if the item was in stock.
- If it was in stock, notify me.
- If it was not in stock, try again in a minute.

The thought is once we have the HTML, there must be something in it which
signifies whether it is in stock or not. So if I was going to write this out
with unwritten functions, it would look something like this:

{% highlight python %}
def check_inventory():
    page_html = get_page_html()
    if check_item_in_stock(page_html):
        send_notification()
        sys.exit(1)  # Terminate
    else:
        print("Out of stock still")

while True:
    check_inventory()
    time.sleep(60)  # Wait a minute and try again
{% endhighlight %}

I know this looks very similar to [the meme](https://www.reddit.com/r/ProgrammerHumor/comments/5ylndv/so_thats_how_they_did_it_its_brilliant/deraqcx?utm_source=share&utm_medium=web2x) about using "coding and algorithms"
to have drones not crash into each other...

{% highlight java %}
if(goingToCrashIntoEachOther) {
    dont();
}
{% endhighlight %}
But the difference is we're gonna fill everything in! So how do we actually do
it?

# Getting the page HTML

So how do we load the data from the Costco listing? Normally for getting HTML,
my first instinct is to use the [requests](https://requests.readthedocs.io/en/master/) library. `requests` is an extremely well-developed library, which makes it easy to make web requests from the internet. For example, if you wanted to get
the HTML for my website, you would just have to do the following (shown in REPL
format):

{% highlight python %}
>>> import requests
>>> page = requests.get("https://www.aryaboudaie.com")
>>> print(page.status_code)
200
>>> print(page.content)
b'<!DOCTYPE html>\n<html lang="en">\n    <head>\n        <meta name="google-site-verification" content="pkNMqDdS4_4zDGNUJ1hOKq5Of31wQEYHNkubK_pu_tY" />\n        <meta charset="UTF-8">\n<meta http-equiv="X-UA-Compatible" content="IE=edge">\n<meta name="viewport" content="width=device-width, initial-scale=1">\n<title> Arya Boudaie\'s Personal Site</title>\n<meta name="description" content="The personal site for Arya Boudaie, with his blog, portfolio, educational resources, and other various things.\n">\n\n<link rel="canonical" href="https://www.aryaboudaie.com/">..."
{% endhighlight %}

You can install the requests library by doing `pip install requests` in your terminal.

So that is pretty easy. 200 is the status code in HTTP which means "everything
went as expected," so if we get back a 200, we know we can get the HTML from the
`content` variable. So what happens if we try it on Costco's page?

{% highlight python %}
import requests
url = 'https://www.costco.com/kitchenaid-professional-series-6-quart-bowl-lift-stand-mixer-with-flex-edge.product.100485356.html'
requests.get(url)
{% endhighlight %}

Well... on my computer I got this really fun error from the requests library
after waiting about a minute:

{% highlight python %}
TimeoutError: [WinError 10060] A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond.
{% endhighlight %}

So that's when it hit me that this probably was not Costco's first rodeo, and
that people have probably tried to scrape their website before, so they must
have some kind of protection against it. So what could it have been...

My first thought was to check the [user agent](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/User-Agent), which is a string that browsers send across
with requests to let the server they're hitting know what kind of browser they
are. Fortunately for us, these strings are very easy to spoof, so we can try to
make it the same user agent as our own browser. You can see your own User Agent
in Chrome by opening up the [developer tools](https://developers.google.com/web/tools/chrome-devtools#:~:text=Open%20DevTools,-There%20are%20many&text=Or%20press%20Command%20%2B%20Option%20%2B%20C,%2C%20Linux%2C%20Chrome%20OS), clicking the `network` tab, refreshing the page, clicking
on the first network request to the stand mixer page, and then scrolling down `request headers` and then find user-agent.

![Imgur](https://i.imgur.com/Ky1NLj2.png)

From [this website](https://www.scrapehero.com/how-to-fake-and-rotate-user-agents-using-python-3/), I found out how to modify our request to include this user agent. So does it work?

{% highlight python %}
import requests
>>> url = 'https://www.costco.com/kitchenaid-professional-series-6-quart-bowl-lift-stand-mixer-with-flex-edge.product.100485356.html'
>>> headers = {"User-Agent":"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36"}
>>> page = requests.get(url, headers=headers)
>>> print(page.status_code)
200
{% endhighlight %}

Nice! We got back a 200 from the server, which means they accepted our request
and we can get the HTML from doing `return page.content`. So in all, the get_page_html function will look like this:

{% highlight python %}
import requests
def get_page_html():
    url = 'https://www.costco.com/kitchenaid-professional-series-6-quart-bowl-lift-stand-mixer-with-flex-edge.product.100485356.html'
    headers = {"User-Agent":"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36"}
    page = requests.get(url, headers=headers)
    return page.content
{% endhighlight %}

# Checking if it's in stock.

So now that we have the page HTML, how can we tell if the item is in stock or not?
Well, as you can see from the above screenshot, there's a huge "out of stock" banner on the stand mixer image. So let's see if we can use that. In Chrome, right
click on the "out of stock" banner, and select "inspect" to look at where is is in the HTML.

![screenshot](https://i.imgur.com/F3pphxb.png)

Here's what it looks like:

{% highlight html %}
<img class="oos-overlay img-responsive" src="/wcsstore/CostcoGLOBALSAS/images/OOS-overlay-en.png" alt="Out of Stock" title="Out of Stock">
{% endhighlight %}

So it looks like the "out of stock" overlay is an image tag, with the CSS classes
`oos-overlay` and `img-responsive`. The img-responsive one doesn't seem too useful, but oos-overlay is extremely specific. This is really handy for us, since we can use this info to tell if the item is out of stock. There's a really nice library for Python which is really good at parsing HTML, called [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/). You can install it by entering the command `pip install beautifulsoup4`. One of the things that's really easy to do with BeautifulSoup is find all of a specific kind of tag with certain attributes. [Here](https://stackoverflow.com/questions/5041008/how-to-find-elements-by-class) is what I found when I googled how to do this. So  let's make a first pass at this:

{% highlight python %}
from bs4 import BeautifulSoup
def check_item_in_stock(page_html):
    soup = BeautifulSoup(page_html, 'html.parser')
    out_of_stock_divs = soup.findAll("img", {"class": "oos-overlay"})
    return len(out_of_stock_divs) == 0
{% endhighlight %}

Let's see if this works on the stand mixer page, in conjunction with our `get_page_html()` function.

{% highlight python %}
>>> check_item_in_stock(get_page_html())
False
{% endhighlight %}

Cool! Looks like our code can tell that the stand mixer is out of stock! Ideally
we would like to make sure that if it was in stock, that the function would return `True`. But obviously we can't do that, or else we wouldn't be in this situation. But we can instead give it another product's page and see what happens. Let's make the URL for `get_page_html` a parameter so we can easily swap it.

{% highlight python %}
url = "https://www.costco.com/.product.100649288.html"
def get_page_html(url):
    headers = {"User-Agent":"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36"}
    page = requests.get(url, headers=headers)
    return page.content
{% endhighlight %}

Let's try it!

{% highlight python %}
>>> check_item_in_stock(get_page_html(url))
False
{% endhighlight %}

Hmm, that's really weird. Why is it saying that this in stock item is actually
out of stock. We only return True if there are 0 `img` tags with the class `oos-overlay` in them, so let's see what's going on in the new product page. Let's go
back to the "inspect" tool on this new page, and do ctrl+f for "oos-overlay" to
see where it could show up...

![screenshot](https://i.imgur.com/g50zdvU.png)

What gives! It looks like the overlay is still on the image in the code, but it isn't actually showing... On further inspection, it looks like this oos-overlay
image is slightly different.

{% highlight html %}
<img class="oos-overlay hide img-responsive" src="/wcsstore/CostcoGLOBALSAS/images/OOS-overlay-en.png" alt="Out of Stock" title="Out of Stock">
{% endhighlight %}

Did you catch it? The overlay has an additional CSS class, `hide`, which probably
has some CSS code telling it to hide the image. So the way Costco implemented this overlay is if the image is in stock, to add a "hide" class to the overlay so the user does not see it. We can use this in our code to instead look for hidden oos-overlay img tags - if one exists, that means the product is in stock!

{% highlight python %}
from bs4 import BeautifulSoup
def check_item_in_stock(page_html):
    soup = BeautifulSoup(page_html, 'html.parser')
    out_of_stock_divs = soup.findAll("img", {"class": "oos-overlay hide"})
    return len(out_of_stock_divs) != 0
{% endhighlight %}

Notice the two small changes - now we're looking for images with both the "oos-overlay" and "hide" classes, and if such a class exists, we return True.

Let's try it on our two products!

{% highlight python %}
>>> url = "https://www.costco.com/kitchenaid-professional-series-6-quart-bowl-lift-stand-mixer-with-flex-edge.product.100485356.html"
>>> check_item_in_stock(get_page_html(url))
False
>>> url = "https://www.costco.com/.product.100649288.html"
>>> check_item_in_stock(get_page_html(url))
True
{% endhighlight %}

Nice! We've successfully written the part which will tell us if the product is
in stock or not! Now we need it to notify me when it's in stock, so I can buy it.

# Notify me!

I chose to do two things to notify me once the item goes back in stock. First off, I wanted to get a text once the item came back in stock. [Twilio](https://www.twilio.com/) is an API that allows you to easily send text messages. Thankfully, they have a free trial period for the API, which allows you to send ~150 texts for free, given that the number you're sending to has been verified as yours. This works well for me, as I just needed the notification to go to me.

After making a twilio account and signing up for the free trial, I'm able to
follow their [Python quickstart](https://www.twilio.com/docs/sms/quickstart/python) and write the code to text myself. You can verify your number [here](https://www.twilio.com/console/phone-numbers/verified). You also have to install the Python package by entering the command `pip install twilio`


{% highlight python %}
import secrets
from twilio.rest import Client
def setup_twilio_client():
    account_sid = secrets.TWILIO_ACCOUNT_SID
    auth_token = secrets.TWILIO_AUTH_TOKEN
    return Client(account_sid, auth_token)

def send_notification():
    twilio_client = setup_twilio_client()
    twilio_client.messages.create(
        body="Your item is available for purchase.",
        from_=secrets.TWILIO_FROM_NUMBER,
        to=secrets.MY_PHONE_NUMBER
    )
{% endhighlight %}

You might have noticed that there's a lot of imports from `secrets`. In general,
it's not good to put secret information in your source code, so that you can
later put it on Github without people knowing that information. Specifically, the
account_sid and auth_token can be used to send texts on your behalf, which can get
very expensive if you're not on the trial. So you can make a file called `secrets.py` in the same folder, and define all of the variables. The first three
can be obtained from your [project console](https://www.twilio.com/console), and the last one is just your phone number.

To test this, you can run the function yourself and make sure you'll get the text.

I wanted to do one other thing though to make sure I knew when it would be in stock. If the item came back, I wanted my program to start playing a loud alarm sound. That way there would be no way to miss the notification. So I found this Python library called [playsound](https://pythonbasics.org/python-play-sound/). After reading the tutorial and doing `pip istall playsound`, I found an alarm sound online, named it "alarm.mp3", saved it in the same folder as my Python script, and added this code to `send_notification`:

{% highlight python %}
from playsound import playsound
...
while True:
    playsound('alarm.mp3')
{% endhighlight %}

So there you have it! All the parts of our code are fully written out, and able to be run together. We just have to chain everything together as follows:

{% highlight python %}
import time

from bs4 import BeautifulSoup
import requests
from twilio.rest import Client
from playsound import playsound

import secrets  # from secrets.py in this folder
def get_page_html(url):
    headers = {"User-Agent":"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36"}
    page = requests.get(url, headers=headers)
    return page.content


def check_item_in_stock(page_html):
    soup = BeautifulSoup(page_html, 'html.parser')
    out_of_stock_divs = soup.findAll("img", {"class": "oos-overlay hide"})
    return len(out_of_stock_divs) != 0

def setup_twilio_client():
    account_sid = secrets.TWILIO_ACCOUNT_SID
    auth_token = secrets.TWILIO_AUTH_TOKEN
    return Client(account_sid, auth_token)

def send_notification():
    twilio_client = setup_twilio_client()
    twilio_client.messages.create(
        body="Your item is available for purchase.",
        from_=secrets.TWILIO_FROM_NUMBER,
        to=secrets.MY_PHONE_NUMBER
    )
    while True:
        playsound('alarm.mp3')

def check_inventory():
    url = "https://www.costco.com/kitchenaid-professional-series-6-quart-bowl-lift-stand-mixer-with-flex-edge.product.100485356.html"
    page_html = get_page_html(url)
    if check_item_in_stock(page_html):
        send_notification()
    else:
        print("Out of stock still")

while True:
    check_inventory()
    time.sleep(60)  # Wait a minute and try again

{% endhighlight %}

And that's it! Just run this code on your computer, and eventually you'll be startled by the alarm once the item is back in stock. I hope you appreciated the walkthrough of how I got to this solution, and I hope you learned a thing or two!

# So what happened?

Well I ran the script, and a day later I heard the loud alarm sound! I went on my computer, and got the stand mixer! I even told a friend who was also interested in it, so we both got to score on the deal :) - so I'm glad that in the end the effort ended paying off. Hopefully it's useful for y'all as well in the projects you try to create.
