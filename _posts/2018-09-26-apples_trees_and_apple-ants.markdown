---
layout: post
title:      "Apples, Trees, and Apple-Ants"
date:       2018-09-26 19:45:26 -0400
permalink:  apples_trees_and_apple-ants
---


To begin, it is best to understand how I got here. In my previous post I discussed the 'process' and through using the 'process' I utilize the gigantic chalkboard right behind where I program. It's useful, and if you want to know more about the *how* of approaching applications read this [here](http://http://rollin-metzger.com/a_programmers_tale). Through the creation and problem-solving required to guide and application from start to finish, I lost sight of the joins table between two of my tables. Here is what I learned.

### The Many to Many

As the name of the relationship implies, it's a relationship of two things in which transitively the first thing *has many of* the third thing through the second thing. In other words, let's look at an example of an apple tree. Let's say our apple tree needs three models (for simplicity's sake): 

1. A Tree
2. An apple
3. Apple ants (an exotic genus of hymenoptera)

Our models will look like this:

```
class Tree < ActiveRecord::Base
  has_many :apples
	has_many :insects, through: :apples
end
```

```
class Apple < ActiveRecord::Base
	belongs_to :tree
	belongs_to :insect
end
```

```
class Insect < ActiveRecord::Base
	has_many :apples
	has_many :trees, through: :apples
end
```

Now we see the transitive property in action. It is *through* the Apple table in which our tree is infested with apple ants! This method is used above is a shortcut through nested has_many associations. The presented many-to-many relationship has the 'center' table belonging to each of the others, so that the 'outer' tables will each pull to each other from the 'center' one. Each way is viable. 

I did go down some rabbit holes and found some cool stuff, like this [star schema](https://en.wikipedia.org/wiki/Star_schema). More than anything, researching and implementing the many-to-many relationship in my Spell-Cat application gave me an appreciation for SQL. Understanding and efficiently navigating queries is at the heart of what any application with multiple sources of data does. 

#### Did You Know?

The roughcut way of utilizing `git commit -m <message>` is out the window! I used to think the 'message' portion of the commit just had to be precise yet the formatting could be whatever pleased the author. I wasn't just wrong, I was wrong because I was looking at a commit and its message in the wrong way. Then I read this [post](https://chris.beams.io/posts/git-commit/) by Chris Beams and all the transparent shards shifted ever so slightly in the new illumination. The shards fell into place and I began a serious investigation into the history of my commits with new level of insight I had. I dare not repeat them here, not in front of the children, but they were atrocious and varied far too widely. The precision I was aiming for only came across as clunky, like peanut butter with nuts *shudders*.

I closed the arcane tome of knowledge written by Chris and wiped my sweat beaded brow with a towel. "A user's git log should read like a professional bibliography," I hoarsely spoke aloud. I paranoidly looked around the empty room, my chalkboard looming ominously behind me. It was because I was the only one reading them. I hung my head in despair and let the truth sink in. *It's not about you, it's about having code, commits, messages accessible to* any. 


