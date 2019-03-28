---
layout: post
title:      "Adventures in JS"
date:       2019-03-28 23:39:23 +0000
permalink:  adventures_in_js
---


Another challenge and another garguantuan load of knowledge successfully synthesized. I always start these projects with the expectation they will take longer than I predict. This project was no different. In the project details it is said to build upon the previous Ruby on Rails project. Instead, I took the scenic route and pushed my Rails knowledge by creating another Rails program from scratch.  

Why, you ask? Why didn't I use the previously my previously built project and expand upon it, if only to save time? Well, I'll tell all. The prior project I built felt forced from start to finish, and because of my lack of interest in the topic I chose as my subject, I had trouble maintaining motivation. Even though at times I had push myself to keyboard, I learned a lot about working on a project you may be less than excited about. For me, programming stems from a center of pleasure: I get the opportunity to problem solve, examine scenarios logically, and absolutely go bonkers over revision; to take a project from nascency to finality is a unique feeling. So, when I built the Ruby on Rails project, I learned how to envision what a project had to look like objectively, dispassionately. To remove how one feels about something to be able to gain clarity is a necessary skill. We're not always going to love what we're tasked with. This is maturity and a chance for growth.  

### Drifting into D&D

A controlled turn. A proper engagement of braking. The throttle from the turning point. This time I was ready. I started out with a clear idea, an idea I was excited about. I knew how it would start, what it would be like through the trenches of MVC and RESTful routing. Through my studies, I even had an idea of *how* I would go about building in the Javascript features, but that would all come later. 

For the topic I chose something I had more passion for. I knew I wanted to build something I could use outside of Flatiron. I chose to build an 'Adventure Creator' for Dungeons and Dragons. I would -- eventually -- build the top layer 'Adventure' and its `has_many` relationships to Quests, Events, and all the other features I would develop. A user would be able to instantiate an Adventure arc and create quests/encounters/cities/npcs/characters... the list goes on. I settled with building out the Quests and the Events for this project, while coding in comments for future features. 

Begining coding, I built it from the ground up using `rails new Flatiron_RubyJs`. Utilizing this feature from Rails, I was able to save valuable time by taking out what I didn't need and adding in what I did. I thought differently about *how* I should approach any project I would work on in the future. This time around I would code and develope features in their own space. Then, I would add the features to the master branch. 

Immediately, I branched out into another branch called `sessions`. I then coded everything I would need in the `sessions` branch: model, controller, views, everything. Starting with the `sessions` branch enabled me to login the next feature, a User. Once both those branches were built, tested, and pushed to master, I could live test the program using our friend: `localhost:3000`. I
```
git add .
git commit <<message>>
git push void sessions
git checkout master
git merge sessions
git push void master
```
and I was off to the proverbial races. 

One feature I wanted to develop was using OAuth to connect through Twitch. It is way less used than Facebook or Github, but Twitch owns Curse which owns D&DBeyond. The end goal is to eventually partner with D&DBeyond and build an 'Adventure Creation Tool'. Or, do it on my own. I switched to another branch
```
git checkout -b omniauth
```
and grabbed the the `TWITCH_CLIENT_ID` and `TWITCH_CLIENT_SECRET` from Twitch. I put them in my `.env` and added `.env` to the `.gitignore` and pushed. I could now login to my app through using my Twitch account.

The rest followed en suite. I branched into more features, creating the necessary CRUD legs of the infant project all the while maintaining RESTful routes. For the Quests and the Events, I used namespaced routes representing their `has_many` and `belongs_to` relationships. Through it all, I learned effective ways to incorporate a `belongs_to` relationship. Up till now, I've been creating the table with the column, e.g., `t.integer :quest_id` for the relationship between Quests and Events. With an 'event' belonging to a 'quest', I found I could use `t.belongs_to :quest` as an [`alias of references`](https://github.com/rails/rails/blob/88aa2efd692619e87eee88dfc48d608bea9bcdb4/activerecord/lib/active_record/connection_adapters/abstract/schema_definitions.rb#L421)(line 429). It adds: `t.index ["user_id"], name: "index_events_on_user_id"` and a `t.integer "user_id"`; it reified the Users `has_many :events, through: :quests` relationship. Another useful piece of ActiveRecord information learned. This was a resource I utilized more during this project. It was a welcome challenge. I could no longer rely on what I already knew and had to adapt, improvise, overcome. I would return multiple times utilizing them often while implementing some of the more tricky sections of this project. 

### The Dragon's ~~Hoard~~ Javascript

With the pillars of the app created, it was time to begin focusing on developing the part of the app showcasing the skills learned over the past couple of months. Prior to the Javascript section of the curriculum, I had a small exposure to Javascript, but nothing close to what I learned in those couple of months. To begin, let's ask a question. What even is Javascript? 

Javascript (JS) is a scripting language used to modify the ~~hoard~~ DOM, a.k.a, a web developer's bread and butter. Then, we have our little compact, feature-reach Javascript library, JQuery. Between the two, we are able to make seamless execution of Ajax operation. Coding this project, I've found JQuery provides many shortcuts, something we developers love (when it's applicable). For instance, turning the Ajax request into a succinct line of beaty:
```
$.ajax(
    url: url,
		type: GET,
		data: data
);
```
vs
```
$.get(url, GET, data);
```
I was able to utilize JQuery's #get and #post functions, although I did find going back to primitive Ajax effective in certain circumstances.  Most noticably, when I was passing data through an html `data-` helper, which I explore more in detail below. Having multiple options from which to view information mighty helpful. 

Essentially, utilizing Javascript allowed allowed me to dynamically update my the DOM on my pages. I no longer had to continuously `redirect_to` page to page. With Javascript, I am able to construct objects:
```
class Quest {
    constructor(name, description, id) {
        this.name = name;
        this.description = description;
        this.id = id;
    };
}
```
With the two of them, I'm able to make API calls:
```
function getQuest(questId, questCallback) {
    $.ajax({
        url: '/api/quests',
        method: 'get',
        dataType: 'json'
    }).done(function(response){
        console.log('response: ', response);

        quest = new Quest(response.name, response.description, response.id);

        console.log("Here is the quest you were looking for:", quest);
        questCallback(quest);
    });
}
```
and create model objects appended to the DOM.  
 
The trickiest part for me was creating the form which renders and submits dynamically. I went through days of analyzing API docs, stackexchange questions, articles, blogs. I was growing to be exasperated, but I persevered. In my early attempts I was trying to pass information from the DOM using 
 ```
 data-quest="<<some data>>"
 ```
 and then grabbing it using JQuery
```
let questId = $.data("quest")
```
and then passing that using an Ajax request
 ```
 $.get(url, questId, function(response){
 ...
 });
 ```
 
I still think the way I ended up passing the needed parameter to the controller using a dynamically rendered form was incorrect.  The way I finalized what I was doing was by modifying the route used itself:
```
get '/quests/:quest_id/events/new_quest_event' => 'events#new_quest_event', as: :getevent
```
where I am able to pass the parameter visibly. I could not understand how to utilize the jQuery $.get() function for passing the parameters I needed to the method for the rendered form. This will be something to tackle as I proceed to polish the existing features and implementing future ones. Perhaps it is an issue with the `form_for` helper. Using namespaced routes, perhaps it's `form_for` with a nested `fields_for`. I spent *hours upon hours* testing for these, but came up short. I'm still learning, perhaps a gem of understanding lays hidden from my gaze.

### The Takeaway

With the project behind, I feel confident moving forward. I want to incorporate more of what I learned into furthering the features of the app, bringing it closer to what it will become. Let's see what React can do, eh?
