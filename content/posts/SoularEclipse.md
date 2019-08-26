---
layout: post
type: video
title: Soular Eclipse
headline: Project
modified: 2014-01-04
date: '2014-01-04 06:55:21'
category: projects
tags: [C, Games, projects]
comments: false
---

<iframe width="560" height="315" src="https://www.youtube.com/embed/A-eomzCX4ic?controls=0" frameborder="0" allowfullscreen></iframe>

Soular Eclipse was my second game at DigiPen, this time written in C, and I took a more backseat role on this team after a hellish first semester. I primarily managed the teams premake build system and built the game object and memory managers.

The memory manager was a basic fixed-size free-list page-based memory manager. Unfortunately I never got it quite right, and the game shipped with quite a bug in it. It was still usable, but a huge portion of it's functionality was unaccessable due to some pointer math errors I couldn't root out. Perhaps we'll explore the fixing of this manager in the future?
