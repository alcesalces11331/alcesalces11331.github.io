---
layout: post
title:      "Following Returns"
date:       2018-11-13 00:33:34 +0000
permalink:  following_returns
---


Earlier in the year I posted about the necessity of following return values. In brief, following the output -- or *return*  -- of the operation will provide the programmer with a steady tracking system. This is incredibly beneficial while developing functionality for a program from a hard-coded state to an abstract state. Although this immediately appears to be a mental method to calling *debugger* or *pry*, by studying and isolating the return values of what they are coding, the programmer will have a keen insight to how mathematicians go about proving and/or disproving a hypothesis. Namely, by knowing what is the desired return value, it's simple to work backwards asking, "How do I get to this point? How do I return that exact value?"

### And Back Again

Alright, so, maybe not so simple. The idea is straight forward and easy enough to execute. You may be asking, "Why not start from the creation of the function and work your way down?" and its corollary, "Why not *simply* use one of the aforementioned debugger methods?" Those methods provide the programmer -- especially the learning programmer -- with an opt-out route: often times they provide a less beneficial route to understanding *what* the code is doing. 

When programming backwards, we already begin in the final level of scope we need. In addition, we usually have code, whether they be variables or other functions, to begin with. We can write the code needed to provide the result we desire and then recursively apply the strategy until we are at the global scope level. When recursively applying this method of analyzing the problems it further strengthens the programmer's understanding of just what exactly their code is doing, and, furthermore, *going to do*. (It also helps in the proving of theorems, lemmas, and theories in whatever rigorously valid field you may someday find yourself in.)

In practice, I'll be honest, I use it as a beacon to pave the path to the result. I know where I'm going and what I need to end up with. Then, it's a bit of a sandwich: starting simultaneously at both ends and working towards the middle. This helps by ensuring more of your functions are *pure* functions.

## Why rely on a program to do what you can do for yourself?
