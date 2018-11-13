---
layout: post
title:      "Returns and Purity"
date:       2018-11-12 19:33:35 -0500
permalink:  following_returns
---


Earlier in the year I posted about the necessity of following return values. In brief, following the output -- or *return*  -- of the operation will provide the programmer with a steady tracking system. This is incredibly beneficial while developing functionality for a program from a hard-coded state to an abstract state. Although this immediately appears to be a mental method to calling *debugger* or *pry*, by studying and isolating the return values of what they are coding, the programmer will have a keen insight to how mathematicians go about proving and/or disproving a hypothesis. Namely, by knowing what is the desired return value, it's simple to work backwards asking, "How do I get to this point? How do I return that exact value?"

### And Back Again

Alright, so, maybe not so simple. The idea is straight forward and easy enough to execute. You may be asking, "Why not start from the creation of the function and work your way down?" and its corollary, "Why not *simply* use one of the aforementioned debugger methods?" Those methods provide the programmer -- especially the learning programmer -- with an opt-out route: often times they provide a less beneficial route to understanding *what* the code is doing. 

When programming backwards, we already begin in the final level of scope we need. In addition, we usually have code, whether they be variables or other functions, to begin with. We can write the code needed to provide the result we desire and then recursively apply the strategy until we are at the global scope level. When recursively applying this method of analyzing the problems it further strengthens the programmer's understanding of just what exactly their code is doing, and, furthermore, *going to do*. (It also helps in the proving of theorems, lemmas, and theories in whatever rigorously valid field you may someday find yourself in.)

In practice, I'll be honest, I use it as a beacon to pave the path to the result. I know where I'm going and what I need to end up with. Then, it's a bit of a sandwich: starting simultaneously at both ends and working towards the middle. This helps by ensuring more of your functions are *pure* functions.

## Why rely on a program to do what you can do for yourself?

In the second half of this blog post, I want to discuss the definition of a *pure* function from a broader point of view. By definition a pure function is: 
> If a pure function is repeatedly invoked with the same set of arguments, the function will always return the same result. Its behavior is predictable. Additionally, invoking the function has no external side-effects such as making a network or database call or altering any object(s) passed to it as an argument.

This definition should be refined to say:
> If a pure function is repeatedly invoked with the same set of arguments, the funciton will always **act the same way although returning different results**. Additionally, invoking the function has no external side-effects such as making a network or database call or altering any object(s) passed to it as an argument.

This begs a slight alteration to an impure function:
> the return value is not predictable, and invoking the function might make network or database calls or alter any objects passed in as arguments.

to:
> invoking the function might make network or database calls or alter any objects passed in as arguments.

thus maintaining system consistency while allowing random processes, i.e., *desired effects* to occur. The separation along the lines of "making database calls or altering any objects passed in as arguments" presents a cleaner interpretation to the ever evolving nature of programming while allowing the use of *pure* and *impure* nomenclature. 

###### However, I may be overly particular about this. BUT I CARE.
