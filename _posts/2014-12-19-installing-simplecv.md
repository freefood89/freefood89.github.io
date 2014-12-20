---
layout: post
title: Installing SimpleCV
author: Rentaro
---
Today I came across SimpleCV ([linked here](http://simplecv.org/)), a simplified computer vision library which works very well with python. I've known and tried to use OpenCV, what people typically use for CV, for a while, but I've never had a good experience using it. Given the choice I've always opted to use Matlab's vision package instead. I'm just not great at C++; it takes too much effort to do the simplest things and its confusing documentation doesn't help much either. Finding SimpleCV and reading up on how easy it can be to use it has been pretty exciting. 

##Installation
Anyways, below I show how I installed SimpleCV on my Ubuntu 14 machine. Thanks to [jayrambhia](http://jayrambhia.wordpress.com/2012/05/02/install-opencv-2-3-1-and-simplecv-in-ubuntu-12-04-precise-pangolin-arch-linux/) for his blog post.

{% highlight bash %}
sudo aptget install libopencv-*
sudo aptget install python-opencv python-numpy python-scipy python-pygame
sudo pip2 install https://github.com/sightmachine/SimpleCV/zipball/develop
{% endhighlight %}

##Test Script
To test that my installation worked I used the first [demo script presented by Katherine Scott](https://www.youtube.com/watch?v=UZSm7Q2bZoc) at Pycon US 2013. The code is unbelievably simple and short. Check out the result below!

{% highlight python %}
from SimpleCV import Image, Display, Color, Camera
cam = Camera(0)
disp = Display((640,480))
while( disp.isNotDone()):
    img = cam.getImage().binarize()
    img.save(disp)
{% endhighlight %}

![image](/img/2014-12-19-simplecv-test1.png)


