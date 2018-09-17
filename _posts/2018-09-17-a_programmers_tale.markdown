---
layout: post
title:      "A Programmer's Tale"
date:       2018-09-17 23:21:21 +0000
permalink:  a_programmers_tale
---

## There...

The last blog post I wrote I examined the Sinatra app I wrote. It was built from the ground up without any magic -- the magic, of course, of Rails. It was gritty and I only wish I knew what I know now when I first rolled my chair up to the keyboard to begin my project creating characters for Dungeons & Dragons. What Sinatra did well, Rails does great. I know this is glossing over the complete disregard for managing memory and load times. I don't care. I would care if managing load times and memory were of paramount importance at the moment. I will care when that is the case. I do care, I take it back, I do care. This is what is so enamorous about building apps from scratch: you learn most by doing and take what you learned from the previous app into the next one. In this way we'll all have a little stairway to heaven.

When starting an app from scratch we can either stub out every file and directory by summoning the powers of perseverence, or, we can use libraries to execute otherwise nonexistent commands. I'm impatient at times and navigating through the dogged paths of levels of complexity to simple birth MVC structure and root files is like placing me in the bottom of a well telling me to claw myself up the wet, steep walls. I used 

```
rails new Spell-Cats
```

to create the basic structure I would need for my code. It brought the base gems with it so I wouldn't have to copy pasta each into the gemfile.rb. When I had this finished, I looked to my right an on my yellow legal-pad where I had a list of to-dos. This is a highly prized step in my building process. I cherish this. The planning stage. The cloud bubble of sorting ideas and bringing them into existence. It always begins with the question: how do I get from here to there? It's a pattern of thought I diligently honed through my undergraduate experience as I was studying the even more arcane realm of mathematics. It begins with myself, a strong cup of coffee, and my six foot chalkboard proudly displayed behind me only a chair swivle away. 

### Provisioning the Road Ahead

Sometimes I begrudgingly begin an app. It's not because I dislike what I'm about to do. It happens when I am so uncertain about what to *build* I have trouble. The chalkboard helps and if there's anything I learned in school it's thought clouds are *really effective*. They help reduce mental clutter by putting a thought down to [chalkboard]. Explore the idea by bringing a solid, yellow, legal-pad with your guiding questions written on it. Start checking off questions. "*If* I choose this topic, what will my join tables be like? What will the objects be and what properties do those objects have? Will my objects *own* other objects?" And then all the *how* questions follow. "How many models will I need to have? What will those look like?" I like to think of creating an app like Spell-Cats as imagining how Bilbo felt when his house was bombarded by a fusillade of dwarves... and Gandalf. "Rollin, my dear boy..." and so on. From simpler beginnings than these tougher questions have been answered. 

This all gets put on **The Board**, and when it's all on the board the it's the time to decide what to do. Usually, the above process narrows the ideas down to no more than three. The final decision about what app to build is largely a personal one, like Bilbo bringing his hankie on the quest. But, in the end, there can only be one master of the ring, err app. I choose one I will have fun with. I've noticed, however, this tends to lend itself to the more simple apps. What we have at the end is what we are going to bring with us, as well as a map to direct us towards what we have to create to get us to the final destination of Smaug's lair -- for Thorin, of course. 

### Thou Shall Not ( def maybe? #gandalf end ) Pass
###### (I know, jumping metaphors)

Now, we know where we are headed. Let's jump right back into *the flow*. Following the snippet up above we'll have a basic, basic, basic point of where to start. We'll also have answered some questions pertaining to what gems we'll have to add to our Gemfile and what model's we'll need to create. Because models are so important for OOP Ruby I always start by defining the models I need. This makes our testing much easier as we won't be slowed down by having to jump from one train of thought to another, i.e., creating a model, then testing again, repeat ad infinitum. It is at this stage I am thankful for David Heinemeier Hansson for his creation of Rails in 2004. Running

```
rails g model <model> --no-test-framework --no-helper --no-assets
```

provides us with a boilerplate model without the extra detritus. I prefer to create the rest by hand as I *need* them. This keeps the dir looking clean without added files cluttering up our app. I will run this again and again for each model I'll need before moving onto something else. By compartmentalizing the programming process I can focus longer on each specific part of the app. To test our app we need to then create our migrations. Running

```
rails g migration <migration> <columnOne>:<type> <columnTwo>:<type>
```

will generate our migration with the columns. By knowing how Rails reads the command it is possible to specify everything you'll need with one command. For instance, running

```
rails g migration CreateUsers username:string email:string password_digest:string 
```

will create

```
class CreateUsers < ActiveRecord::Migration
  def change
    create_table :users do |t|
      t.string :username
      t.string :email
      t.string :password_digest
    end
  end
end
```

Familiarizing myself with the implicit power of Rails really paid dividends the further I trekked into the swampy regions of the app. I was glad I took the time to learn how to tell Rails what to do. I am a firm believer in cutting seconds to maximize the level of efficiency brought to the time you're programming and learning the ins-and-outs of a framework is a great way to get better at coding. 

We can rinse and repeat this many times, running rspec with our created tests to verify our code is doing what it should be doing. This project was the first time I found myself creating tests while I was building the app and I am oh so thankful I went about it this way. This saved time in the future when a minor bug would've thrown my app into distraught troubleshoot nood-mode. This is what I call it when I have stepped into a filthy quagmire and have no idea how I got there."A common beginner mistake," I tell myself (although I've been programming a little under a year at this point I am a beginner. Besides, have a beginner's mindset is an advantageous mindset to have when learning new things.)

### Through the Mines

We'll need routes. Up above as we 'provisioned' for the task of building components for the task, we also decided what we wanted our routes to look like. Whether this will require namespacing, shallow, scope, modules, whatever; we may have to experiment to get it just right. I found reading the API for this part of the project elucidating. I'll share what mine looked like and a few thoughts on how I reached this decision:

```
# user paths #new #create
  get '/signup', to: 'users#new'
  post '/signup', to: 'users#create', as: 'users'

  # shallow nested routing to represent model relationships with ease of view
  resources :users, only: [:show] do
    resources :cats, shallow: true do
      resources :spells, shallow: true
    end
  end

  get '/cats', to: 'cats#index'

  resources :schools, only: [:show] do
    resources :spells, only: [:show], shallow: true
  end

  get '/spells', to: 'spells#index'

  # session paths
  get '/signin', to: 'sessions#new'
  post '/signin', to: 'sessions#create'
  post '/signout', to: 'sessions#destroy'

  # omniauth path
  get '/auth/facebook/callback' => 'sessions#create'

  root 'static#welcome'
```

The best part of learning how to create the routes I needed while getting my paths to appear as I wanted was experimenting with nesting routes using the specification `shallow: true`. This allowed me to show namespaced routes for *particular* aspects of the objects, i.e., ownership of one object on another as they relate to `GET show` methods for the objects. Triple nesting as I did for the `users` objects is typically frowned upon. However, accompanied by the `shallow: true` key-value command limited the usually overly complex routes for all methods to only the `#show` method.

### The Battle of Five Models

Creating the rest of the app follows the same process: create, test, add, test... etc. This is true for controllers and Rails provides commands for controllers just as it does for migrations and models. The methods follow suit too. For creating the models we very carefully follow the principle "follow the returns, follow the retuuuurrrrnnns". The hardest and trickiest part was integrating controller actions with objects to be passed to our views. Validating secure access to certain views required a `before_action :<method>, only: [:actions]` which was simple enough. Following boolean logic gates was of absolute importance and greatly cluttered the controllers before I DRY'd it all up for the finishing touches. I always feel that when manipulating boolean logic I have to be very careful about keeping in mind *exactly* what it is I need to pass through or am checking. I find if I haphazardly write logic I can 'lose' properties I'm trying to keep, so to speak. For instance, in creating the following code I had to begin passing through extra params. You'll see.

```
def show
  if params[:cat_id]
    @cat = Cat.find_by(id: params[:cat_id])
  elsif params[:spell_id]
    @spell = Spell.find_by(id: params[:spell_id])
    @cat = Cat.find_by(id: @spell.cat_id)
  else
    find_cat
  end
end
```

and the following code from the corresponding view in the cats#show view and spells#index view:

`<%= link_to "#{@cat.name}'s Spells", spells_path(@cat, :cat_id => @cat.id) %>`

and:

```
<% if s.cat_id %>
  <p><%= link_to "Created By", cat_path(s, :cat_id => s.cat_id)%></p>
<% else %>
  <p><%= link_to "Created By", spell_path(s, :spell_id => s.id)%></p>
<% end %>
```

which allows views of the spells by owners of the cats and nonowners delineated so. But -- and a major but! -- I did get stuck on managing params of checkboxes which spiraled me down into a path of regex and extra method creating. Here's the view:

```
<% @power_types.each do |p| %>
  <%= f.label p %>
  <%= f.check_box :power_type, { multiple: true }, p, false %><br>
<% end %>
```

which is waaaay simple but for some reason (I think it was the long day of work coupled actively with a long evening of programming which did it) was uber complicated at the moment. I learned a s\*\*t ton about regex manipulation while API researching for Rails#check_box. I returned to the basics and followed the return values. My params were a string generated by an array and implicit regex. It was annoying, but I felt invigorated having powered through it. 

## ... And Back Again

The final result of Spell-Cats suffered from scope creep as the vision I held between me and **The Board** had way more interaction and functionality. The sheer size of it eventually utilizes 3D modeling either through A-Frame or Unity. Either way, I desperately need another tool in belt: Javascript.

TTFN

-Alcesalces (NA Moose)
