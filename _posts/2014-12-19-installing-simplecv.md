---
layout: post
title: Installing SimpleCV
author: Rentaro
---

Today I came across SimpleCV ([linked here](http://simplecv.org/)), which I discovered works very well with python. 

I've known OpenCV for a while, but I've never had a good experience using it. I've tried several times in high school and then in college, when I opted to use Matlab's vision package instead. First off, I'm not too great at C++. It takes too much effort to do the simplest things. Second, the documentation for OpenCV is pretty bad in my opinion. I also find their documentation pretty hard to read.

##Installation
Anyways, here's how I installed SimpleCV on my Ubuntu machine:

{% highlight %}
sudo aptget install libopencv-*
sudo aptget install python-opencv python-numpy python-scipy python-pygame
sudo pip2 install https://github.com/sightmachine/SimpleCV/zipball/develop
{% endhighlight %}

##Test Script
To test that my installation worked I used the first [demo script presented by Katherine Scott](https://www.youtube.com/watch?v=UZSm7Q2bZoc) at Pycon US 2013.

The code:
{% highlight python %}
from SimpleCV import Image, Display, Color, Camera
cam = Camera(0)
disp = Display((640,480))
while( disp.isNotDone()):
    img = cam.getImage().binarize()
    img.save(disp)
{% endhighlight %}

Checkout the results!
![image]({{ site.url }}/img/2014-12-19-test1.png)

