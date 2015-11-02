---
layout: post
title: about
date: '2015-01-16 11:23:25'
permalink: /about/
---

I'm currently a student at DigiPen Institute of Technology and working on a neat little game with a working title of Pixie Skate with Team Salt. I'm really into the build process of C and C++ and want to learn more about it. I'm also interested interested in memory management and related topics.

#Projects:

##Pixie Skate:
Team Skate is working on Pixie Skate. We're still working on prototyping and moving those prototypes into our engine so there aren't any videos yet. The general idea is to capture some

My responsibilities on the project were as such:
- Maintaining and extending our build system.  

- Maintaining the core engine.

- Creating and maintaining WWise integration.

- Maintaining the component/composition system.

- Creating and maintaining the input systems.

- Binding our engine to Zilch, a scripting language we use for some game play code.  

- Utilitizing the reflection system provided by Zilch to automatically serialize/deserialize both our Zilch and C++ components.

Tools and Languages used in these tasks:
- C++  
- CMake Script  
- Zilch  
- Python  

##Ripple:
<iframe width="560" height="315" src="https://www.youtube.com/embed/gUoXGoufYhE" frameborder="0" allowfullscreen></iframe>
The Adjective Noun completed Ripple during June of 2015, a "Poetic Experience" game.

My responsibilities on the project were as such:
- Maintaining and extending our build system.  
- Creating and maintaining the "core" systems that allow our other programmers to develop derivative systems.  
- Maintaining our Component system.  
- Binding our engine to Zilch, a scripting language we use for some game play code.  
- Creating gameplay components when needed.  

Tools and Languages used in these tasks:
- C++  
- CMake Script  
- Python  
- Zilch  

##Soular Eclipse:
<iframe width="560" height="315" src="//www.youtube.com/embed/A-eomzCX4ic" frameborder="0" allowfullscreen></iframe>
Soular Eclipse was my second game at DigiPen, this time written in C, and I took a more backseat role on this team after a hellish first semester. I primarily managed the teams premake build system and built the game object and memory managers.

The memory manager was a basic fixed-size free-list page-based memory manager. Unfortunately I never got it quite right, and the game shipped with quite a bug in it. It was still usable, but a huge portion of it's functionality was unaccessable due to some pointer math errors I couldn't root out. Perhaps we'll explore the fixing of this manager in the future?

##[Title_of\_Game]:

<iframe width="560" height="315" src="//www.youtube.com/embed/w-jULUaIg7c" frameborder="0" allowfullscreen></iframe>
[Title_of\_Game] was the first game I worked on at DigiPen. We were using Zero Engine, which is an engine built by the folks in R&D and can be described as essentially an in-house Unity. We chose to use Python, as Zilch wasn't well documented yet, and none of the upperclassmen had really used it.

My primary contributions were the menus and camera. I'm particularly proud of the shape creation work I did. The shape creation used some basic custom serialization to dynamically create the right click menus. I used a general tree structure I wrote in Python to generate the menus at level-load, and just placed them based on 

##[delayio](https://github.com/playmer/delayio):
delayio sprung out of a friend not being sure how to "create a console effect using print functions for the narrative portions of my text based adventure". After chatting a bit, I found that delaying output in C like how Role-Playing Games do is an interesting little bit of work. 

So after implementing that I decided to implement a function to process strings so that it wouldn't go past some defined line size, and would prevent word splits. (I should probably go back and make sure this is safe.)
