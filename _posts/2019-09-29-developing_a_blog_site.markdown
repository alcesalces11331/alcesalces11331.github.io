---
layout: post
title:      "Developing a Blog Site"
date:       2019-09-29 21:25:28 +0000
permalink:  developing_a_blog_site
---


Part of becoming a competent full-stack developer is developing applications for yourself. It means creating a personal portfolio site, developed and programmed by yourself. It means creating a personal blog site, without utilizing a "create-your-own" site like Squarespace or Wordpress. I've finalized v5 of my [portfolio site](https://rollin-metzger-portfolio.herokuapp.com), which was a great exercise in responsive web design, flexbox, and React components. It's not quite finished, but, then again, nothing ever quite is perfect. It will host all my projects when I get them polished and hosted as well. It will also be incorporate a personal, self-developed blog site. This is my next project and the second leg of Project: Portfolio.

> Part of becoming a competent full-stack developer is developing applications for yourself.
>

Almost anyone interacting with the web is familiar with blogs; how to write them, how to build them, how to browse them. But, what does it entail to build them? What questions do we have to ask? Luckily, all the concepts are familiar: persistent data with a relational database; RESTful design practices; responsive design; authentication and security. Here are the questions I needed to ask myself:

1. What will the blog app do?
2. What security, if any, will be required?
3. What features will need to be built?
4. What languages, database, will be used?

The blog will need to persist data, show data, update and delete data. In other words, this app will be a CRUD application. For security, it will not render any login portal. I will program in a backdoor with the representational state transfer endpoint being /admin. This is because it will be an application solely for myself. I will need to add a checkpoint for any CRUD actions being executed or called which will check for my admin credentials. Feature wise, it will be a basic text building application. It will need to be searchable by month, year, and keyword. 

I knew going in I was going to use this application as an opportunity to learn and practice a different back-end programming approach. I will build the back-end utilizing Python and Flask. With all the languages out there, Python is a swiss army knife and so versatile it should be a pocket-pick for all developers. For the web framework, I narrowed down the plethora of frameworks to three: Flask, Django, Pyramid. I really liked the scalability of Django and Pyramid. Django especially is well documented with many users and contributors. It is sturdy and provides everything I would, or could, require. However, I don't need everything. For this application, Flask, with its lightweight and simple approach, would suffice.

For database persistence, I would also utilize a new database: MongoDB. Why MongoDB? I had previously made use of SQLite3, but was unimpressed as my applications became more complicated. I am sure SQLite3 would be able to handle what I needed, but adapt, improvise, overcome. 

> ... adapt, improvise, overcome.
> 


