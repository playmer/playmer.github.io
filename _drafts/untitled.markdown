---
layout: post
title: Tricksy C-->++
---

I hate obfuscated C++ code. [And I don't mean the competition stuff either.](http://www.ioccc.org/) 

It's that stuff you write because you saw it on hacker news, stack overflow or reddit <include links>, and decided you wanted to be cool and adopt someone else's thinking. You show it to your friends or, worse yet, a newbie C or C++ user and they all adopt the practice. Now you've infected the freshmen (both literal and figurative) and they need someone like Meyers to tell them it's wrong when he gets around to writing another book about it. 

Now not all of its bad, but I don't want to have to parse out some crazy one-liner you did because you thought it was funny. Some of it should be obvious to any seasoned C programmer who really knows their precedence chart and operators. However, I'm here writing about it, and why I hate it. 

##The "Gos-to" Operator
It all started out innocently enough. You though you'd be clever because white space doesn't matter between tokens and separated the post-decrement from your variable. Then you thought it'd be hilarious if you paired it to the left of the greater than operator. 

And then your buddie across the hall light flame to his desk and spiraled out of control with his Hearthstone addiction. They say he's still sitting there today, trying to beat Naxxramas with a slightly melted keyboard. 

The --> "operator" is a clever yet heinous way to abuse C/C++ and my hatred for it is why it's in the title. 

##r-value references as return values
I love the idea of these things, and darn it  I know there are fantastic uses for them. Just consider this one a cautionary tale rather than one you "Must Adhere To." Also this is quite long, and more of an explanation of why I got rid of them. So only read if you're also curious about the architecture squabbles of a sophomore game engine. 

When I first read about r-value references I was amazed, I could return something from the stack of a function without a copy? This is amazing! Sign me up immediately! This works with std::unique_ptr? How quickly can Fedex send my cash-money to Stroustrup?

You see I had just recently decided to refactor my entire engine, and I chose in my infinite wisdom to try to use more C++11/14. I may go into why I think that was a hilariously foolish idea and why I want to strip them out another day. 

So we have a factory class that manages components, it's templates and gets specialized so it can do various cool things. We even have and even more special snowflake version for our script components. It's all very well and good. 

Here's the deal though: the templated ones need to be instantiated at some point. So how do we do this? Well we use some preprocessing magic and macros to make and tell the component system about all these different types of components. 

That's a whole 'nother blog right there. 

Anyway that worked great when it was global, but our factories no longer live in a static map on the base factory class. Now they live in a ComponentSystem instance, which lives on a Space Instance, which lives on a Universe instance. (That awful naming convention, tasty.) 

How do we do it now and how do r-value refs come into the picture?

Well we still use the include trick, though I'm planning on making core engine components more explicit. But our macro has changed. As you can see we're making some kind of function that'll return an unordered map with strings to unique pointers to factories. If that's all you've got you're solid. 

Why is this awful?
Well for one, technically speaking, what if that map your returning gets added to another map with like keys? Maybe you don't care. But if you do care, you've just made a bunch of factories for no reason! You're also creating a map just to end up moving all of the stuff out of it immediately after the function is called. 
