---
layout: post
title:      "Sinatra Project: The Good, The Bad, and The Really Ugly"
date:       2018-06-09 22:21:54 +0000
permalink:  sinatra_project_the_good_the_bad_and_the_really_ugly
---

I'm always excited for do-it-yourself projects. The amount learned through completing a start-to-finish endeavour -- in this case, a CRUD web application -- easily synthesizes all the previous exercises, labs, and lessons covering the relevant material. The pieces start adding up, the links between them become visible through pathing errors, depencies unspecified, and scope errors. I'm proud of what I was able to compile (hehe ;) ), however ugly the end result is to me. 

## The Good
### Active Record
What Active Record is capable of is nothing short of awe inspiring. The way Active Record stitches together web apps makes me really appreciate web developing in the year 2018 than in the year 1995 (however, this sense of 'magic' has downsides too, which  I'll talk about below). From instantiating project through Ubuntu for windows and syncing the master repository with Github (my condolences, Github, but good for you) setting up and using Active Record was a piece of programming cake. Even when I felt I was struggling over a certain relationship within the code, Active Record was never the problem. If I ever thought Active Record could be letting me down, I knew it was a gap in my knowledge. 

And it was flexible. Projects like the Sinatra Portfolio Project evolve considerably from conception to finalization. The initial requirement becomes more along the lines of "What more can I do here? How far can I push this idea?" Then -- usually -- it's reevaluating the has_many and belongs_to relationships between the models. Sometimes, when this happens, it is perceptively prescient, and then the resulting feeling is one of sheer confidence. Other times, it organically evolves from the very first belongs_to to mulitple has_many as relationships are flying like [carrier pigeons flying over head](http://rollin-metzger.com/ip_avian_carries).

### SQL
Managing spreads of information at first seems daunting. However, it's only a matter of articulating to ActiveRecord through Sinatra, the matter of what is a table, what is a column, and what types of columns are present. Even adding columns is another migration away. Heck, creating and seeding a database is merely another coded file away, and it's built with nothing more than what is already known (you know hashes? you good). It's pure joy to pull up Shotgun and click through the web app, watching the waterfall of information from RESTful and CRUD functions visualizing data from a SQL database. That's all we're doing. Everything else is magic. 

### Debugging
Often looked at as reductively tedious -- it is tedious as f@%k -- debugging your code is one of **the best ways to learn**. Moreover, large integrated projects, such as the Sinatra Portfolio Project, come almost preordained with a shet ton of bugs. Or, as I like to call them, a shet of possible lessons. Debugging elucidates connections previously unglamorous, catapulting even the most mundane method to the lime. 
## The Bad
### Knowledge Limits
This is where the limits of my knowledge of how to use certain ActiveRecord validations shows its stanky head. It becomes even more apparent by trying to hook to a module without finding yourself into a circular loop where it's never not calling something and breaking everything (DEFCON 5 up in here). This isn't really a bad thing about ActiveRecord, but a shortfall of my own understanding of validations. I even learned a lot about validations by attempting to utilize more of them to shore up obvious redundancies in my code. Using unique validations really pushed the boundaries of my knowledge set... and broke it. This is why it is still a bit ugly. Functional, but ugly. 

###### Lesser Value: Return Values
I wrote a [blog post](http://rollin-metzger.com/understanding_programming_from_a_tests_perspective) about just how damn important return values are, from string, to array, to hash, to boolean, to method... etc. It's not worth delving into here, but it is worth mentioning. Quite a large number of my bugs had to do with me overlooking return values and could have been 100% avoided had I made more of an effort to remember return values. RETURN, RETURN, RETURN. Lesson learned. 

## The Really, Really Ugly
### Skeletons in the HTML Closet

It is abysmal to look at. Initially. The skeleton of the thing created without sinew and tissue. It has no styling only basic markdown. It is cringe worthy, and something worth seeing in a Dungeons and Dragons campaign. 
