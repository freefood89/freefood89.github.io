---
layout: post
title: Learning More Python
author: Rentaro
---

Since my last post on [learning python]({% post_url 2015-04-12-learning-python %}) I've learned even more thanks to [The Hacker Guide to Python](https://julien.danjou.info/books/the-hacker-guide-to-python) by Julien Danjou. The book echoed my mental note to go over Python's builtin libraries so I went over my old work to see if I can apply these tools.

##urllib
About a year ago I was writing a lot of crawlers and API wrappers I ran into an issue trying to build my URLs. Even using a nice package like [requests](http://docs.python-requests.org) I ended up with unmanageably long line lengths.

```python
res = requests.get('http://hostname.com/uri?queryparam1=x&queryparam2=y')
```

Especially when I tried to call a web API that paginates results, things got really messy..

```python
res = requests.get('http://hostname.com/uri?queryparam1={}&queryparam2={}&start={}&count={}'.format(x,y,start,numItems))
```

Little did I know that the builtin library ```urllib``` had a url parser and builder.

...

##namedtuples

##abc

##@property and @foo.setter
