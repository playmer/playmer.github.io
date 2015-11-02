---
layout: post
title: "An Introduction to Prebuild Systems (As they pertain to C & C++)"
description: Why you should be using a prebuild system for your C or C++ project.
headline: "An Introduction to Prebuild Systems (As they pertain to C & C++)"
modified: 2015-05-16
date: '2015-01-16 06:55:21'
category: prebuild
tags: [C, C++, Cmake, Premake, Prebuild]
comments: true
---

This is the first in a series of articles I plan to write about the build process in software development. I have friends who've taught me more about it than I care to admit, and have written much better articles about it. However I can't write about the systems I've used and learned about without writing a bit on why you should think about using them.

So, developing software is a pretty large task. I know that may seem obvious, but it's important to know the steps involved so that you can reduce, and ideally automate, the tedious work. When you first start on a project, maybe you decide on a directory structure, this can change, but you do need to decide on something, even if it's the old "everything in one folder" method. Once you do that you write some code. And if you're a professional, it's probably in multiple files, and you'll likely have some external and internal dependencies. 

##Definitions

Let's define those quickly so there's no confusion:

<u>External Dependency</u>: You have a library like SDL, Boost, or GLFW you need to link to. Could be static or dynamic, ultimately it doesn't matter. The point is that this is code you're not compiling yourself. You need to keep track of these binary files, and the different versions for different compilers and platforms you might be supporting. 

<u>Internal Dependency</u>: Code that you compile yourself, into either a dynamic or static library. You still need to keep track of the dynamic files during the packaging step, but considering you'll be doing one compile per platform, this is much easier than doing so with your external dependancies. These files won't be kept in your repository and thus are only generated and worried about at compile/runtime. 

##Why and How

And now you have your first problem. How do you build this thing? You envisioned this as a multi platform program, but you don't want to write a make file from scratch for every compiler you might need. You'll have to edit it every time you make a new cpp. Besides, I have Visual Studio users on my team, they want to use the tool they know. Plus that person who does our Mac ports needs to be able to use XCode. 

This is where a Prebuild system comes into play. I want to be clear that I'm not actually trying to bash make here. Make is great, I've used it with three compilers before, and it's a champ. But if you want to use something like Visual Studio, you get nothing out of using make. I mean you can go through the Visual Studio wizard and make a project alongside your makefile, but now you have two things to keep up to date. What a Prebuild system does is allow you to define all the things you'd do with make or Visual Studio solutions/projects, but in one "language" so it's consistent. And in return you get to generate the project you'd like to work on at the moment. 

Feel like working with Vi/emacs and the terminal today? Generate a makefile project and start your coding/building. Person on Windows wants to use Visual Studio? They'll generate the appropriate files based on their preferred version and get going at it. 

Now it's never as easy as that. Your code and all of your libraries need to be cross platform, so don't go using obscure C++14 stuff if your Windows devs are stuck on VS 2013 or lower. (Even 2015 won't support everything in C++11, let alone 14). And you'll generally need to handle a bunch of edge cases depending on platform and/or compiler. So makefile hell is not beneath you, as this is arguably worse.

##Plans
I will be writing articles around various Prebuild systems I've used or plan to try out. I'll be working through various projects I've worked on and show off various Prebuild strategies. Here are the first few I plan to do over with links to their official sites:

* [CMake](cmake.org)  
* [Premake](http://industriousone.com/premake)
I recommend using [this instead.](http://sourceforge.net/projects/premake/files/Premake/nightlies/) As it contains binaries of the newest builds of premake.
* [FASTBuild](http://www.fastbuild.org/)


Now FASTBuild is not technically a Prebuild system, or cross platform, but they've got generating Visual Studio solutions from meta files in, and they're looking at doing cross platform. So it looks like it's becoming a hybrid of both a Prebuild and builder system. It's also really fast during the build step, utilizing a concept called "Unity builds" that sort of appends a bunch of source together into one file so that the compiler just compiles most or all of the project in one go. On many (if not all) compilers this tends to be quicker than actually compiling the files separately into their own object files. 

I'll likely go over more in time, I know I want to talk about the build process at some point, talking about the flags in the cl compiler (the compiler Microsoft provides in Visual Studio) that might interest you folks, but this is my current roadmap. Thanks for reading, check back soon for my series on how to get started with CMake!

##References
[Trent Reed](http://www.trentreed.net/wp/?p=102) has a really great write up on Build systems with some fantastic diagrams