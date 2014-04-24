---
layout: post
title: Dual H-bridge Board
author: Rentaro
---

Below is the result of one full week of thinking, layout, and planning. These H-bridges are made to control two small dc motors. The H-bridge can take up to a 500 mA load. This board will probably be integrated into my scrapbot. The simulation for this circuit can be found [here]({% post_url 2011-06-30-H-bridge-simulation %}).

I am currently working on a microcontroller to modularize the h-bridge unit. The plan is to be able to send serial instructions to the H-bridge driver microcontroller to drive the motor.

![circuit from above](/2011-07-12-dual-H-top.jpg)
![circuit from below](/2011-07-12-dual-H-bottom.jpg)
![circuit design](/2011-07-12-dual-H-schem.jpg)