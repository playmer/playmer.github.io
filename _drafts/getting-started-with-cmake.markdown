---
layout: post
title: ! 'Adventures in CMake Part 1: Getting Started'
---

So I've been asked by various friends to help them with their build system. The first recommendation I make is to switch to using a prebuild system. Keep in mind, most of these folks are using Visual Studio, although there's at least one user of makefiles running on Linux. 

I've already been pinned down to help a team with their build system for their current engine, so hopefully in continuing blog posts I'll describe that. This however is about getting your first CMakeLists.txt banged out. It'll get you up and running for a simple, one executable project without thinking about multiple directories, although I'll put some notes in for folks who want a little bit of organization. 

##Prerequisites
 - [CMake](http://www.cmake.org/download/): You'll need a working copy of CMake, I recommend putting it in your path.
 - [Python 3.x](https://www.python.org/downloads/): Although I won't go into it this time, I do recommend having Python installed. At least one later part will discuss using Python at length for writing generation scripts for easy invoking of CMake.

##The Hello World of CMake
    cmake_minimum_required(VERSION 2.8 FATAL_ERROR)
    project(Sleepy_Print C)
    message(STATUS "Hello World!")
So the first line is pretty self-explainatory, this tells CMake that 