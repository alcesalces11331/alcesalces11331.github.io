---
layout: post
title:      "Javascript Data Structures: An Introduction to Properties"
date:       2019-09-15 23:13:55 +0000
permalink:  javascript_data_structures_an_introduction_to_properties
---


When programmers discuss the tools worked with, a common thing discussed is data structures. Now, programmers of differing backgrounds and languages of speciality will have different names for their data structures. Ruby, for instance, talks of programming languages declared in a key-value pair a 'hash' whereas in Javascript this organization of data is called an object. However, when a Javascript programmer talks about an object, they're not only talking about a key-value paired programming object. Here's how Marijn Haverbeke defines an object in Eloquent Javascript Third Edition:
> "... [objects] are arbitrary collections of properties"

What does this mean, exactly? When a data structure is discussed -- or, rather, data in general -- it is talked about *how* and *why* it holds data in the ways it does. 

Before this post delves into the *what* of a Javascript object, it is beneficial to first understand what is meant by a data property. Let's look at some examples:
```
const propString = "flabbergast"
const propArray = [1, 2, 3, 4, 5]
const propObject = {
    animal: {
		    "sun bear": "mammal",
				"two-toed sloth": "mammal"
		}
}
```
Now, all of the above have properties attached to them. A property of all the first two is one quite familiar: *.length*. When *.length* is called on *propString* or *propArray*, it calls a method to literally count the length of the string and the length of the array, respectively. Knowing and becoming familiar with the properties associated with different data structures is necessary to being a proficient programmer. Moreover, knowing how to *call* the properties and which type of properties can be called in certain ways. 

Two ways exist to call the properties data structures have. First, the easiest is to use a plain string and use a period, i.e.,
```
propString.length
```
The second is to use square brackets:
```
propArray[0]
```
Either one will produce the same result, but only complete strings can be used when calling properties using the period method. Furthermore, it is worth pointing out both *null* and *undefined* are without properties and trying to access them results in an error. 

Properties are what makes classes into classes and functional programming exist. When property after property is called, functional programming is occurring. For instance, utilizing the above example:
```
propArray.shift().pop().slice(1,)
```
is functional programming where the properties being accessed are properties associated with an array data-type. When a class is defined for object-oriented programming, the methods associated with them are accessed like normal properties. Essentially, properties are being define for the 'class' object and accessed similarly. 

A great example for this is when object-oriented programming is being used for a back-end API. Namely, defining a controller for RESTful routing is done by utilizing properties of SQL. Here's an example controller from a controller I built for a project earlier this year:
```
def index
        @user = User.find_by(id: current_user.id)
        if params[:quest_id] == nil
            @events = Event.where(user_id: @user.id)
            @quests = []
            @events.each do |e|
                quest = Quest.where(id: e.quest_id, user_id: @user.id)
                @quests << quest
            end
            render 'index'
        else
            @events = Event.where(quest_id: params[:quest_id])
            @quest = Quest.find_by(id: params[:quest_id])
        end
    end
```
Notice how many times a property is called within one simple method: ".find_by"; ".where"; params[:quest_id]. Notice how many times properties are called when programming virtually anything.

Particularly of importance is how objects are built. Take the example above:
```
const propObject = {
    animal: {
		    "sun bear": "mammal",
				"two-toed sloth": "mammal"
		}
}
```
The object has properties which we, the programmer, have defined. We can access them by `propObject.animal` which will produce another an array of objects. Let's look at this example more in detail:
```
propObject.animal
// {"sun bear": "mammal", "two-toed sloth": "mammal"}
propObject.animal["two-toed sloth"]
// "mammal"
```
Because the keys "sun bear" and "two-toed sloth" do not appear like normal binding names, they have to be accessed with square brackets. It is of importance to recognize the near identical structure of JSON and regular Javascript objects. With JSON came the standard way data is sent throughout the internet.
>Javascript Object Notation is widely used as a data storage and communication format on the web, even in languages other than Javascript.

However, all property names in JSON have to be surrounded by double quotes. This can easily be done by calling properties of JSON objects:
```
JSON.stringify
// will convert data to the correct format
JSON.parse
// will convert data from JSON format
```


I hope you've enjoyed this brief introduction to properties.
