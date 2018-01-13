---
layout: post
title:  "My First Project!"
date:   2014-03-08 12:21:59 -0500
categories: c blender game
---
I knew C language before my Engineering course. As a first year student of Computer Science, I had no idea how things are going to be in CSE.

First year didn’t help much. During my second year I started trying out things. Eager to make my own game, I made a snake game with no knowledge of any of the graphics libraries. How? With the use of `char` matrix as the view port, linked list for the snake, `o` as the snake body and `*` as the fruit.

![Snake Game]({{ "/assets/my-first-project/snake.jpg" | absolute_url }})

## Why First Person Shooter Game ?
Ever since my first year (2011), I had a master project in my mind. A wearable display (with accelerometer and gyroscope) to track rotation and tilt. And a motion controller to track hand movement (Wouldn’t it be cool if you were the protagonist in your favourite FPS game, and you could look around, and shoot your enemies by mere physical movements). It was this project that inspired me to work on most of the subsequent projects.

![VR]({{ "/assets/my-first-project/wear.jpg" | absolute_url }})

I planned to work on this project with one of my friend (doing Electronics Eng.), I were to focus on the software part and He on the hardware. So I thought of building my own game to interact with the hardware.

## Decision: Design a game or Simulate key presses

I had the option to simulate mouse movements and key presses with signals from sensors (`space = jump` , `left click = shoot` etc.)(and run this on top of any of the FPS games) but major flaw was that the player’s hands are fixed to the camera (there is no independent movement of head and hands). Because this was the most unique thing about our project, as we head separate sensors to track head movement and hand movement, I thought of making my own game.

![FPS Game]({{ "/assets/my-first-project/fps.jpg" | absolute_url }})

## Game Engine, which one?

It was absurd to build my own game engine and then build a game, so I started searching for the best ready-made game engine for me, which was easy and gave me enough freedom. I went through Unity, Ogre3D, Panda3D and then finally found the perfect game engine `BLENDER`. Blender is free and open source and allowed me to design characters and side by side script their logic in Python. You don’t need me to tell you how cool python is, right?

![Game Engine]({{ "/assets/my-first-project/blender.png" | absolute_url }})

## Blender, Done! What next?

I studied blender’s documentation and followed their video tutorials. Found a nice enough character, rigged it. I couldn’t attach mouse triggers for ‘looking’ because it would be triggered by our sensors.
It took me nearly 2 months to finish my first Project-level application.
And I was happy with the output…

<iframe width="420" height="315" src="https://www.youtube.com/embed/P6g6Wfi70og" frameborder="0" allowfullscreen></iframe>

you can [get the game here]({{ "/assets/my-first-project/FPS.zip" | absolute_url }}).

Keys:
* W: move forward
* I, K, J, L: look up, down, left, right
* Space: reposition after looking
* Shift: jump
* Numpad 8, 2, 4, 6: move gun up, down, left, right
* R: reload
