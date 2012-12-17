--- 
layout: post
title: I hate comments

type: post
published: true
---

I delete comments when I come across them. Comments are a crutch, to be used sparingly and only after all other options have been exhuasted. Comments are used for numerous purposes, so I'm going to enumerate the worst offenders:

{% highlight python %}
def incrementCounter(self):
    # Counter should never be greater than 5
    self.counter = min(self.counter + 1, 5)
{% endhighlight %}

This comment is worse than worthless. It adds no information because it simply restates the next line. The fact that it's taking up space makes it negative value, but by far the worst part is what happens over time: the code will change from refactoring and updates, but the comment will grow stale and eventually lie outright. A really common sequence is that 5 becomes a constant, and then that constant is changed but the comment isn't updated. So you end up with:

{% highlight python %}
MAX_COUNTER = 20
...
def incrementCounter(self):
    # Counter should never be greater than 5
    self.counter = min(self.counter + 1, MAX_COUNTER)
{% endhighlight %}

This, fundamentally, is the reason why I hate comments. What started with nothing but good intentions became an outright lie, and will eventually cause harm. Someone will read the comment, make the wrong assumptions and add bugs to the code. What should be done instead? A unit test. A simple unit test would not only provide significantly more value, but it will also evolve with the system:

{% highlight python %}
def test_incrementCounter_never_greater_than_5(self):
    c = Counter()
    for x in range(6):
        c.incrementCounter()

    assertEqual(c.getCounter(), 5)
{% endhighlight %}

Now what was a comment is a test case, and the results can be relied on over time. If the code changes for whatever reason, the test will fail, causing it to be updated.

**Tests are living comments.**

Another extremely common case is the "this shouldn't happen" comment:

{% highlight python %}
def acceptPayment(self, amount):
    # Amount should never be less than 0!
    self.balance -= amount
{% endhighlight %}

It seems so obvious to me that you should always translate that comment into this code:

{% highlight python %}
def acceptPayment(self, amount):
    assert amount >= 0
    self.balance -= amount
{% endhighlight %}

This code is dramatically more readable. Not because I'm claiming I can visually parse Python faster than I can parse human language, but because when I parse "assert amount >= 0" I can be certain of that condition. When I parse "Amount should never be less than 0" what I actually read is "I'm really hopeful that amount is never less than 0, but it could probably happen under certain conditions". Now I have to think through two cases of the code, amount >= 0 and amount < 0.

These simple examples are just the start. The same principles scale up to complex code with giant amounts of comments. Almost universally when I see large blocks of comments, I find the tests lacking. The tests aren't covering important functionality and they're unreadable. Ater adding significant amounts of tests, renaming test cases to be human readable and rearranging the test file to be read in-order then the comments become unnecessary. As a corollary, if you and your team aren't generally reading tests as source documentation, start doing that today.

I have seen heavily-commented code work well, but I find it only works in a few narrow contexts. The lone-programmer scenario, like Knuth's [literate programming](http://en.wikipedia.org/wiki/Literate_programming) is one. Another is code bases with a few people who spend a significant amount of time reading and reviewing every commit. In both cases, I think it works but the time spent maintaining the comments would be much more effectively spent maintaining awesome automated tests.

Comments are a crutch. Unfortunately, sometimes languages break your leg. You need the crutch. The more you optimize your code away from readability and towards performance, the more you'll end up needing comments. Additionally, you'll need to pay that much more attention to the accuracy of your comments every time you change the code. A good example of this is python's [garbage collection module](http://hg.python.org/cpython/file/fd57dbfa5765/Modules/gcmodule.c). It's complicated and performance-critical C code, and benefits from long-form high level comments at the top of most functions. The answer is to not write C code (or other low-level-over-readability languages) unless you absolutely have to.

Finally, when I see a comment I see it as a challenge: **can I make code that is as readable as the comment** and dissolves the need for the comment's text? In the cases above the assertions and automated tests needed were straightforward and obvious. In real code it'll be much more complex and nasty. When I succeed at removing a comment, I've made a significant improvement to the codebase.

## tl;dr: comments are crutch. delete them. replace them with code that *does* instead of *says*.
