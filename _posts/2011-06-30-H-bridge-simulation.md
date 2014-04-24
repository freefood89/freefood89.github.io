---
layout: post
title: H-bridge simulation
author: Rentaro
---

I always believed that to build an H-bridge I need to use FETs. I'm guessing that it was because of the small device package of Bipolar Transistors that I thought that it will not be able to power it. Well today I realized that some of my motors are probably small enough (low power) to be powered by BJTs. This also made for a great opportunity to test LTSpice some more. Eventually I hope to improve my mobot H-bridge design in efficiency using these tools.

Below are the results. You can see that the flyback diodes really do help protect by limiting the various potential differences to below their respective breakdown levels. The blue trace represents the input signal and the green trace is the voltage at one end of the inductor with respect to ground.

![no flyback](/2011-06-30-noflyback.png)
![with flyback](/2011-06-30-withflyback.png)
