---
layout: post
title: Analog IC Design as a Hobby
author: Rentaro
---

I may have finally figured out how to tape-out my own analog IC designs without draining my bank account. even though I did poorly in analog IC design at school, I've wanted to know what it would take to start a company that designs analog ICs and RFICs. This [super old article](http://www.edn.com/electronics-blogs/anablog/4309610/Analog-IC-design-on-the-cheap) on EDN Network is very short and lacks detail, but it essentially shows how CAD software is unneccessary and fabrication can be cheaper using a service like [MOSIS](http://www.mosis.com/); it shows how it would be possible for anyone like me to start designing my own ICs.

CAD, or computer aided design, tools usually comes with a simulator and layout tool. The simulator is important because they help engineers simulate complex circuits with some level of accuracy before spending lots of money to fabricate a prototype. The layout tool can check if a design complies with the fabrication equipment's design rules. CAD can save lots of time and money by eliminating design iterations. However, the cost for something like what I used in school can run well over millions per year

After some more digging and thinking I found that LTSpice, a free SPICE simulator I've played with, actually can run BSIM3 models. BSIM3 is a highly parametric transistor model sufficiently accurate for analog IC simulation. It's actually the same model I used in school through Cadence. Simulating my designs would be a matter of finding the model parameters for the fabrication technology. 
