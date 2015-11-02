---
layout: post
title: node.js C++ Addon Debugging
---

It's surprisingly difficult to find out how to do this. It took me a few days of on and off googling, but I ended up finding a [Youtube video explaining what was required.](https://www.youtube.com/watch?v=KvjHn59C-uQ)

I'm going to do a write-up so that people don't have to watch a video and scrub through it to figure out what they need to do. I'll also try to improve the workflow introduced in the video and post up the stuff required to do that too.

I'm assuming some basic familiarity with typical tasks like setting up your path, but I'll detail most of what you need here. I'm also (forgive me) assuming Windows and Visual Studio 2012. This should be usable regardless, but you'll have to tweak some things here and there for whatever other OS your using. I don't use the debuggers on Linux, and rarely use XCode, so I'm just documenting this for my current project which is Windows based at the moment. I'm also not sure on the VS2012 requirement, but as far as I can tell node.js defaults to be compiled by it, so I'm just keeping it all in the same compiler.

###The Setup

* [Python](https://www.python.org/downloads/)  
The first thing you're going to want to do is install Python 2.7 and have it in your path. Unfortunately they're using it for their build script currently and Python 3 just will not work.
* [Git](http://git-scm.com/downloads)
* [node.js](https://github.com/joyent/node)
You'll want to clone the repo. I suggest using the latest version:
    git clone https://github.com/joyent/node.git -b v0.12.0-release
    


