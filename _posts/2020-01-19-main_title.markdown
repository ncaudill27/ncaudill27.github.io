---
layout: post
title:      "Main Title"
date:       2020-01-20 04:29:25 +0000
permalink:  main_title
---


## Creation Station
___
My introduction to frameworks and web development was quite the journey. The end however, I believe produced a good foundation for something that could be much bigger. My Sinatra project is a look into the building process of a Dungeons and Dragons character.


## Languages and Tools
___
* Languages: Ruby, HTML, CSS
*  Gems: Corneal, Sinatra, Active Record, Rake, Shotgun/Thin, Tux, Nokogiri, BCrypt
*  Tools: Trello, Justinmind Prototyper, VS Code, GitHub
*  Implementation: Model-building scraper, generator-backed seed file, 


## Main Features
___
* Concept driven styling them
* Five has_many/belong_to relationships
* Two has_many, through: relationships
* Easily resettable database

## Eager For A Challenge
___
Going into this project I wished to build something  with a little complexity. This was done with the intention getting a better perspective on how quickly things can scale up. Wow! Did I  get what I wished for. The goal wasn't just to build an in-depth character model, but also to get a first-take at CSS. What it can do, and how to get it to work for me. I got to see what it can do.

Starting off was made easy by using the the [Corneal](https://github.com/thebrianemory/corneal/) gem. Shout out to Brian Emory. Step two: run `git init` and get that fresh repo feeling. Next, build a Trello board and map out all my first routes. Everything went quite smoothly in the beginning. The perfect setting for a horror movie.

Day one went off with out a hitch. I began at the User controller continuing along with a RESTful mindset. Added a session controller to handle those pesky user needs. Dropped into the middleware to slide in a quick `Rack::MethodOverride` enabling all kinds of new fun. Made it all the way to having an almost complete Character controller with matching views.

Having flown through the core framework of my project I deemed it acceptable to turn my attention to design. I figured this was going to be an area that would slow me down, but only because I've never touched CSS. CSS was just property hashes though, right? It can't be that hard. I searched online for a free wireframing tool and instead came across a nifty prototyper [Justinmind](https://www.justinmind.com/).

Throwing together mock layouts to match to *did* make it easier to stick to an idea and bring it to life. Going blind-folded, full Leeroy Jenkins into CSS did *not*. While getting things arranged to plan was doable, but at what cost?  The next *two* whole days were spent ~~learning~~ playing with CSS.

To say the site looks good is a reach, but it certainly has potential. Stepping away from the WET mess I made, I knew my work was cut out for me. It was time to bring the data to life. For me that meant fetching the necessary information to fill out a relationship model that featured Characters having many skills and proficiencies through their Race and Class.

Adding depth (even if it was models that only had a name attribute) was an engaging process. Accomplishment of the primary objective was absolutely felt. Especially when considering how quickly things would scale digging deeping into just one facet of the project (e.g. inheritly applied math, randomized dice rolls, new views to accomodate all this new information).

The project was coming together and beginning to look tight. Enter the bugs. The main one being several Character show pages were throwing NoMethodError when attempting to retrieve the name attribute of it's inherited Race or Class(Klass) attribute. A lot of useful features were added trying to narrow down on the culprit behind the issue. What was the offender you ask? An incorrectly assumed relationship model placing the foreign key on the sad side of the equation.

## Learning Points
___
Some big take-a-ways were brought from this adventure. Besides being reminded not to overlook the details of building one's models tools associated with building said structure struck a big chord for me. Bug-hunting led me to trusting in version control, and learning how to build proper migrations. Diving into the database, destroying it, and reseeding it led me to the discovering of how to use the lib folder to create a clean seed file.

## What's next?
___
Finding features to add to this project will certainly not be difficult. Some were already mentioned, but my personal favorite would be adding to the scraper. Not just exploring how bulky the Character model can get, but how to decide to display that data. Stubbing specs is another big want, especially to make sure older features still work as intended when adding new ones.
