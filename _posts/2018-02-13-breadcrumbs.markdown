---
layout: post
title:      "Breadcrumbs"
date:       2018-02-13 17:17:25 +0000
permalink:  breadcrumbs
---


![](https://www.sustainweb.org/resources/images/cooking/breadcrumbs.jpg)

Since last inception, my studies have taken me through HTML/CSS, past procedural ruby, and straight on into OO ruby. The blitzkreig of lesson after lesson being endlessly consumed has provided an unforeseen gem of functionality. With this functionality, I move fluidly across the editor cutting and creating as *required*. It's a trial-and-error process which has its own claws. I find myself flabbergasted, but not completely: functionality is a trail of breadcrumbs. 

In my previous post, I mentioned standing on giants as a metaphor to utilize the creations before me. This is even more true now as I've progressed deeper into the course. As a reward, I've been provided tool after tool to manipulate the world around me. These tools I did not create, but I can create with them. I am a technological carpenter (more like an apprentice to an apprentice carpenter -- I basically return coffee when called). Although I have access to more and more tools, I am losing focus on the broader picture of *how they all fit together*. What I mean is, within Ruby the tools make sense and I can see their purpose. But, *how* they were created and *how* they work is, with few exceptions, a mystery I have not yet parsed apart. It's evident in the functionality of gems, methods, classess, etc... It's evident in Nokogiri. What I'm really getting at here is I know far less than when I started. What I know is bits of sawdust, an image of the tree become a home. 

This is a consequence of deepening my toolbox. I've begun creating programs of my own, and it's like playing with legos for the first time. Another sequence of trial-and-error and replicating from previous lessons. But, what is originality? This process of originality is recurssive and by, although not by definition, is built on learning from others. It's best shown in a rudimentary program I created to calculate my finances for me (and it still has a long way to go):

```
#iterate over expenses and output remaining amount
def finances
	expenses = {}
	total_remaining = nil
	puts "Input monthly total:"
	input = gets.chomp
	input = input.to_i 
	puts "Input varying Black Hills Energy bill:"
	bhe_new = gets.chomp
	bhe_new = bhe_new.to_i 
	expenses[:bhe] = bhe_new
	puts "Input varying LES bill:"
	les_new = gets.chomp
	les_new = les_new.to_i
	expenses[:LES] = les_new
	expenses.each do |bill_key, bill_value|
		input -= bill_value
	end
	total_remaining = input
	if total_remaining > 0
		puts "Total Amount Remaining: $#{total_remaining.round(2)}."
	else
		puts "Alert! Watch your spending."
		puts "Total Amount Over Spending: $#{total_remaining.round(2)}."
	end
end

finances
```
Which, will show you how much you have left over after all bills are paid. However, I have to manually input every key-value in expenses, which, once completed, rarely needs altered again. I know there is a better way to do this, but I haven't stumbled upon it.

This has been a rewarding enterprise. 

And I am so excited for what comes next.
