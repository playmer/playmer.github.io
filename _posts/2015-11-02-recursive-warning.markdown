---
layout: post
title: "Unused Arguments Aren't a Problem When Recursing Right?"
description: You should let your compiler devs know about this.
headline: "An Introduction to Prebuild Systems (As they pertain to C & C++)"
modified: 2015-05-16
date: '2015-05-16 06:02:21'
category: C++
tags: [C, C++]
comments: false
---

So before I started interning with the fine folks of DigiPen R&D in the Summer of 2015, I was using one of their projects, [Zilch](http://zilch.digipen.edu/home/), as a scripting language in my game Ripple. As a side project I looked into making an Atom plug-in for Zilch. 

I didn't get particularly far, but I got far enough to realize that the code internal to Zilch that finds member functions was broken. 

Here's a snippet from the Zilch source code that was causing my problem.

{% highlight c++ %}
Function* BoundType::FindFunction(StringParam name, const Array<Type*>& parameters, Type* returnType) const
{
  const FunctionMultiMap* functions = /* It gets set somehow */;

  // Attempt to find the array
  const FunctionArray* foundFunctions = functions->findPointer(name);

  // Check if we found any functions by that name at this level
  if (foundFunctions != nullptr)
  {
    // Look through all the functions found and check if they signatures match.
    // return it if it does.
  }
  // If we found nothing...
  else
  {
    // Check our base type for this function.
    return this->BaseType->FindFunction(name, parameters, returnType, options);
  }

  return nullptr;
}
{% endhighlight %}

Heavily truncated, but essentially this function looks for a function on a BoundType, typically some Zilch class you've compiled, based on name, an array of parameter types, and return type. The problem lies in the fact that at the time, this code never actually looked for returnType. But we never got an unused parameter warning because the returnType was being used, in the recursive call into this function!

Wow, okay, well that's an interesting problem to run into. Took me an hour or two to find, and [the guy who eventually became my boss](http://motleycoder.com/) and I had a good laugh. His tests were actually relying on this bug, so that required some fixing on his part.

But then I gave this some more thought, and I wondered why this wasn't tracked by MSVC. So I went and tested it on the pre-release VC 2015 compiler. Turned out it still didn't work. So I messaged [STL](http://nuwen.net/stl.html) on reddit, and he suggested I file a Connect bug. [So I did.](https://connect.microsoft.com/VisualStudio/feedback/details/1189216)

But then I decided to make a test case for any given compiler and see if any of the compilers I would typically consider using solved this, and it turns out they don't.

Here's the test code: 

{% highlight c++ %}
#include <iostream>
using namespace std;


int Recursive(int num, const char *notUsed);

int main()
{
  const char *notUsedLocal = "Not used";

  cout << "Test: "
       << Recursive(1, notUsedLocal)
       << endl;
  return 0;
}

int Recursive(int num, const char *notUsed) 
{
  if (num > 5)
    return num;
  else
    return Recursive(++num, notUsed);
}
{% endhighlight %}

[And the absurd amount of flags I used to compile on g++ and clang](http://stackoverflow.com/questions/5088460/flags-to-enable-thorough-and-verbose-g-warnings):


{% highlight bash %}
g++ -pedantic -Wall -Wextra -Wcast-align -Wcast-qual -Wctor-dtor-privacy -Wdisabled-optimization -Wformat=2 -Winit-self -Wlogical-op -Wmissing-declarations -Wmissing-include-dirs -Wnoexcept -Wold-style-cast -Woverloaded-virtual -Wredundant-decls -Wshadow -Wsign-conversion -Wsign-promo -Wstrict-null-sentinel -Wstrict-overflow=5 -Wswitch-default -Wundef -Werror -Wno-unused source.cpp -o gccOut.exe


clang++ -pedantic -Wall -Wextra -Wcast-align -Wcast-qual -Wctor-dtor-privacy -Wdisabled-optimization -Wformat=2 -Winit-self -Wmissing-declarations -Wmissing-include-dirs -Wold-style-cast -Woverloaded-virtual -Wredundant-decls -Wshadow -Wsign-conversion -Wsign-promo -Wstrict-overflow=5 -Wswitch-default -Wundef -Werror -Wno-unused source.cpp -o clangOut.exe
{% endhighlight %}

So if you're interested in getting this fixed for the compilers you might use, let people know, and contact them through these bug reports (Will update with more when I can test on the bleeding edge versions of clang and g++):

[MSVC Connect Bug](https://connect.microsoft.com/VisualStudio/feedback/details/1189216)

