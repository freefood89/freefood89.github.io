---
layout: post
title: Learning Python
author: Rentaro
---

I've come to a point where at least in my friend group I'm the python guy. Yet, I never feel like I know enough of it because I keep learning new things:

### Yield
A little while ago I came across [nvie's fantastic explanation of generators and iterables](http://nvie.com/posts/iterators-vs-generators/). I really hope that he never takes this page down. It introduced me to `yield`, which I find pretty cool and unique. I've converted some of my parsers to have generators, which can reduce the number of times you have to iterate over text inputs without changing your code structure. By allowing you to weave together functions, it removes the need for temporary intermediate variables.

### Built-in Libraries
Recently, I've been maintaining an API built for students at college hackathons and let's just say I've never felt I needed unit tests as much as I do now. After stupidly trying to `pip install unittest` for a little while I noticed that the documentation for [Unittest](https://docs.python.org/3.4/library/unittest.html) is on the python built-in libraries page. I found a cool [tutorial on unittest](http://pythontesting.net/framework/unittest/unittest-introduction/) by Brian Okken. I will definitely be using this write to help my first unit tests for python.

Within the same context I realized the need for [Logging](https://docs.python.org/3.4/library/logging.html), which also happens to be a built-in for python. This has even forced me to read python library source code since packages like [Flask](http://flask.pocoo.org/) require a custom logger setup (or perhaps they're following some pattern).

[Argparse](https://docs.python.org/3.4/library/argparse.html#module-argparse) is another cool and useful built-in library that I picked up as well; I wont have to manually parse command line arguments anymore, something I sadly admit I've been doing.

### Design Pattern using Logging and Argparse
I'm not entirely sure if this is any good or whether it already exits, but I've come up with a nice project structure that controls logging via commandline args based on what I saw in [Flask](http://flask.pocoo.org/)'s source code.

```
project
    some_script.py
    config.py
```

config.py:

```python
import logging
import argparse

parser = argparse.ArgumentParser()
parser.add_argument('--log', help='Selects log level. Options: DEBUG, INFO, WARNING, ERROR, CRITICAL')
parser.add_argument('--env', help='Selects deployment to: PROD or DEV(default)')
args = parser.parse_args()

if args.log:
	numeric_level = getattr(logging, args.log.upper(), None)
	if not isinstance(numeric_level, int):
	    raise ValueError('Invalid log level: %s' % args.log)
	logging.basicConfig(level=numeric_level, format='%(levelname)s: %(message)s')
logger = logging.getLogger('root')

```
some_script.py:

```python
import config
from config import logger
  
logger.debug('It Works!')
```

##Thoughts Goind Forward
At some point I should probably read the entire documentation for python, or at least the table of contents. Being a language I picked up entirely on my own I seem to only know things relevant to my personal projects.
