---
layout: post
title:  "Android Inception: a remote controller app"
date:   2014-03-08 12:21:59 -0500
categories: android remote
---

Accelerometer and gyro-meter are costly. And they were necessary for my master project (the one I mentioned in Last blog) . Spending money to buy them and then a micro-controller for interacting with them would have cost me heavily.

![Overview]({{ "/assets/android-inception/wifi.png" | absolute_url }})


I knew most of the android phones have these sensors in-built. So instead of spending ( around 10k rs), I thought of studying android API and then building an app which would send sensor data to the computer.

Android was surprisingly easy to learn. And also to my advantage, I already learned Java in 3rd semester. I started building small apps and was able to fetch and display sensor data. But then came the difficult part **making a connection to a remote computer**. There are many modes of communication, but I preferred two of them Bluetooth and WLAN. This was also the first time I came across something called `Socket`.

I didn’t have any android phone. I was trying out my apps on `Micromax Funbook p275`, a cheap but handy tablet. It didn’t have Bluetooth hardware module, so I had to go with wifi. It took me some time to learn `Sockets` because I had no freaking idea how computer networks worked.  And yeah Java doesn’t allow sockets to be created on main thread, so I had to learn `thread programming` too.
I preferred Java on remote server (your PC) because it has a common VM for linux, windows or OSX.

When I was browsing through Java library, I came across an awesome class `Robot`. Its functionality is as cool as its name , It can simulate mouse movement and key presses.
I already knew **making connection with a remote computer** , **sending data** and Robot class gave me the freedom to control my computer with my tablet. I implemented it , and here’s the output..

<iframe width="420" height="315" src="http://www.youtube.com/embed/IG2jsOm6hJI" frameborder="0" allowfullscreen></iframe>

I continued working on this project for 2-3 months and added features like automatic server detection (requires UDP broadcasting), Bluetooth support and what not!
